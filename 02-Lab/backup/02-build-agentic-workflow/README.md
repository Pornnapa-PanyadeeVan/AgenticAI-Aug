# 03 — Lab 2: Build an Agentic Workflow with Make

[← Previous: Lab 1](../02-build-ai-agent/README.md) · [Home](../README.md) · [Next: Lab 3 →](../04-generate-management-report/README.md)

🎯 **Goal**  รับ Business Request จาก Google Form ให้ Google Sheets เก็บคำตอบ แล้วใช้ Make + Gemini วิเคราะห์และเขียนผลกลับแถวเดิม โดยส่ง Gmail เฉพาะรายการ `HIGH`

🧰 **Tools**  Google Forms + Google Sheets + Make + Gemini API key + Gmail

## Completed Flow

```text
Google Form
↓ submit response
Google Sheets — Form Responses 1
↓
Make: Google Sheets — Watch New Rows
↓
Google Gemini AI — Simple Text Prompt
↓
JSON — Parse JSON
↓
Router
├─ Route 1: Priority = HIGH
│  ↓
│  Google Sheets — Update a Row
│  ↓
│  Gmail — Send an Email
│
└─ Route 2: Priority = MEDIUM OR LOW
   ↓
   Google Sheets — Update a Row
```

> Google Form ไม่ได้ต่อเข้า Make โดยตรงใน Flow นี้ เมื่อมีคนกด Submit คำตอบจะถูกเพิ่มใน response sheet ก่อน แล้ว `Watch New Rows` จึงอ่านแถวใหม่ไปประมวลผล

> **ส่วนที่เติมจากภาพ:** Route 2 ต้องมี `Google Sheets — Update a Row` เช่นกัน เพื่อให้ผลวิเคราะห์ของ `MEDIUM/LOW` ถูกเขียนกลับแถวเดิม ส่วน Gmail อยู่เฉพาะ Route 1

### Tool, Connector และ Workflow ใน Lab นี้

- **Channel/Input:** Google Form รับคำร้องจำลอง
- **Data Store:** Google Sheets เก็บคำตอบจาก Form และผล AI ในแถวเดียวกัน
- **Tool/Action:** `Parse JSON`, `Update a Row` และ `Send an Email`
- **Connector:** connection พร้อม authentication และ permission ที่ให้ Make เข้าถึง Gemini, Google Sheets หรือ Gmail
- **Workflow:** Make ประสาน Form response → AI → JSON → Router → Update/Alert

Connector ทำให้ระบบเข้าถึงบริการได้ แต่ไม่ได้ตัดสินว่าควรทำอะไร ใช้เฉพาะ Form, Sheet และอีเมลทดสอบตามหลัก Least Privilege ดูเพิ่มที่ [Connector ใน Glossary](../01-introduction/glossary.md#connector)

> **MCP clarification:** Lab นี้ใช้ native connectors ของ Make ไม่ได้ติดตั้ง MCP Client/Server จึงไม่ควรเรียกทุก connection ว่า MCP ดูความแตกต่างที่ [MCP ใน Glossary](../01-introduction/glossary.md#mcp-model-context-protocol)



## ก่อนเริ่ม

- [ ] ผ่าน Lab 1 หรือมี [Lab 1 System Instructions](../01-build-ai-agent/README.md)
- [ ] Make account เปิด Scenario builder ได้
- [ ] Google Account ใช้ Forms, Sheets และ Gmail ได้
- [ ] ใช้ข้อมูลจำลองเท่านั้น
- [ ] เปิด [Lab 2 Prompts and Test Data](prompts.md) อีก tab

## 📌 Step 1 — Create the Google Form

1. สร้าง Google Form ชื่อ `Business Request Intake — Workshop`
2. เพิ่มคำอธิบายว่า `ใช้ข้อมูลจำลองเท่านั้น ห้ามกรอกข้อมูลจริงหรือข้อมูลลับ`
3. ปิดการเก็บ email address ถ้าไม่จำเป็น
4. สร้างคำถามและเปิด `Required` ทั้ง 3 ข้อ:

| Question | Type | Example |
|---|---|---|
| Requester | Short answer | `Demo Customer` |
| Department | Dropdown | `Sales`, `Marketing`, `Finance`, `HR`, `Operations`, `IT`, `Customer Service` |
| Business Request | Paragraph | `ลูกค้ารายใหญ่ไม่สามารถชำระเงินผ่านระบบได้...` |
| Required Date | Date | `เวลาที่ต้องการ.` |

5. อย่าแชร์ Form เป็นสาธารณะ ใช้ลิงก์ทดสอบกับตนเองหรือภายในห้องเท่านั้น

💡 **Why This Matters**  Form เป็น Channel/Input ที่กำหนดโครงสร้างข้อมูลก่อนเข้า Workflow แต่ตัว Form เองไม่ใช่ Agent

✅ **Checkpoint**  เปิด Preview แล้วเห็น 3 คำถาม แต่ยังไม่ต้องกด Submit

## 📌 Step 2 — Link Form Responses to Google Sheets

1. เปิด tab `Responses` ของ Form
2. เลือก `Link to Sheets` หรือ `Select destination for responses` ตาม UI ที่เห็น ([Google Forms Help](https://support.google.com/docs/answer/2917686))
3. สร้าง Spreadsheet ใหม่ชื่อ `Business Request Log`
4. เปิด tab ที่ Google Forms สร้างให้ เช่น `Form Responses 1`
5. คง 4 headers แรกไว้ แล้วเพิ่ม result columns ทางขวาให้ครบ:

```text
Timestamp
Requester
Department
Request
Summary
Priority
Reason
Recommended Action
Processing Status
```

> อย่าเปลี่ยนชื่อหรือลบคอลัมน์คำตอบ 4 ช่องแรกหลังเชื่อม Form แล้ว หากแก้คำถามใน Form ให้กลับมา refresh field mapping ใน Make

💡 **Why This Matters**  Google Sheets เป็นทั้ง response log, audit trail และ Request History ที่จะใช้ต่อใน Lab 3

✅ **Checkpoint**  Sheet มี 9 columns และ `Summary` ถึง `Processing Status` ยังว่าง

⚠️ **Common Problem**  Make มองไม่เห็น columns หาก header ว่างหรือซ้ำ ให้แก้ header แล้ว refresh/reselect data structure ใน connection

## 📌 Step 3 — Create a Gemini API Key

> ⚠️ **SECURITY: Never paste your API key into Form, Sheet, Prompt, screenshot, chat หรือ public GitHub files.**

1. เปิดหน้าจัดการ API keys จาก [Google AI Studio](https://aistudio.google.com/)
2. สร้าง key สำหรับบัญชี/โปรเจกต์ของตนเองตามตัวเลือกที่หน้า UI แสดง
3. คัดลอก key ไปใส่ใน Make connection โดยตรง
4. ไม่ส่ง key ให้เพื่อนและไม่ใช้ shared instructor key
5. หลัง Workshop ให้ลบ/rotate key หากไม่ใช้ต่อ

> **UI MAY VARY:** บัญชีองค์กร โรงเรียน บางประเทศ หรือบาง project อาจสร้าง key ไม่ได้ ดู [Gemini API key documentation](https://ai.google.dev/gemini-api/docs/api-key)

### Free-tier Safety

- เลือก model ที่บัญชีระบุว่าใช้ได้ใน Free Tier
- ไม่เปิด billing เพื่อผ่าน Workshop
- จำกัดการทดสอบคนละ 3–5 ครั้ง
- หากสร้าง key ไม่ได้ ไปที่ [Fallback without API](#fallback-without-api)

✅ **Checkpoint**  Make connection บันทึก key แบบ secret/credential และไม่มี key ปรากฏในไฟล์หรือภาพ

## 📌 Step 4 — Watch New Form Responses

สร้าง Scenario ใหม่ใน Make แล้วเพิ่ม:

```text
Google Sheets → Watch New Rows
```

ใช้ Google Sheets connector ที่ Make รองรับ ([Make Google Sheets documentation](https://apps.make.com/google-sheets)) แล้วตั้งค่า:

- Spreadsheet: `Business Request Log`
- Sheet: `Form Responses 1` หรือชื่อ tab ที่ Form สร้างจริง
- Table contains headers: `Yes` ถ้ามีตัวเลือกนี้
- Limit: `1–3` สำหรับการทดสอบในห้อง
- Choose where to start: `From now on` สำหรับ Lab นี้

ลำดับการทดสอบ trigger:

1. กด `Run once` ใน Make ให้ Scenario รอแถวใหม่
2. กลับไป Google Form แล้ว Submit ข้อมูลทดสอบ 1 รายการ
3. ตรวจ output bundle ว่ามี `Row number`, `Timestamp`, `Requester`, `Department` และ `Request`

> `Watch New Rows` เป็น scheduled trigger ไม่ใช่ instant webhook เมื่อเปิด schedule จริงอาจมีช่วงเวลารอตาม plan ของ Make สำหรับ Workshop ใช้ `Run once` ได้

💡 **Why This Matters**  Trigger ระบุว่า Workflow เริ่มเมื่อใด ส่วน agentic behavior มาจาก AI reasoning, decision และ action ที่ตามมา

✅ **Checkpoint**  Make อ่านแถวที่เพิ่งมาจาก Form ได้ และเห็น `Row number`

⚠️ **Common Problem**  ถ้า Make ไม่พบแถว ให้กด `Run once` ก่อน Submit รายการใหม่ ตรวจชื่อ tab และ starting point อย่า Submit ซ้ำรัว ๆ

## 📌 Step 5 — Analyze the Request with Gemini

1. เพิ่ม `Google Gemini AI — Simple Text Prompt` ต่อจาก `Watch New Rows`
2. สร้าง connection ด้วย API key ของตนเอง
3. เลือก text-generation model ที่ Free Tier เปิดให้บัญชี
4. Copy Prompt จาก [Lab 2 Prompts](prompts.md#business-request-json-prompt)
5. Map `Requester`, `Department` และ `Request` จาก `Watch New Rows` ไปยัง placeholder ที่ตรงกัน

Gemini ต้องตอบ JSON object เดียวในโครงสร้างนี้:

```json
{
  "summary": "",
  "priority": "HIGH",
  "reason": "",
  "recommended_action": ""
}
```

ค่าของ `priority` อนุญาตเฉพาะ `HIGH`, `MEDIUM` หรือ `LOW`

💡 **Why This Matters**  JSON ที่มี key/value ชัดเจนทำให้ Workflow นำผล AI ไปใช้ใน Condition และ Action ได้คาดการณ์กว่าข้อความอิสระ

✅ **Checkpoint**  Raw output ไม่มีข้อความหรือ Markdown code fence ก่อน/หลัง JSON

## 📌 Step 6 — Parse the JSON

เพิ่ม `JSON — Parse JSON` แล้ว:

1. Map text output จาก Gemini ไปที่ `JSON string`
2. สร้าง data structure จาก [Expected Data Structure](prompts.md#expected-data-structure)
3. Run once แล้วตรวจว่าได้ 4 fields แยกกัน:

```text
summary
priority
reason
recommended_action
```

✅ **Checkpoint**  เลือก field `priority` เดี่ยว ๆ ไปใช้ใน filter ได้

⚠️ **Common Problem**  หาก Parse ไม่ผ่าน ให้ตรวจ quote, comma, code fence และย้ำ `Return ONLY valid JSON` ดู [Troubleshooting](../troubleshooting/README.md#json-cannot-parse)

## 📌 Step 7 — Complete the Router

เพิ่ม Router หลัง `Parse JSON` แล้วสร้าง 2 routes ที่ไม่ทับกัน:

### Route 1 — HIGH

```text
priority Equal to HIGH
```

### Route 2 — MEDIUM/LOW

```text
priority Equal to MEDIUM
OR
priority Equal to LOW
```

อย่าใช้ `contains HIGH` และไม่แนะนำให้ตั้ง Route 2 เป็นเพียง `priority != HIGH` เพราะค่าผิดรูปแบบอาจถูกบันทึกเป็นผลปกติ

💡 **Why This Matters**  Router คือ Decision step: ผล AI ไม่ได้เป็นเพียงข้อความ แต่กำหนดว่า Workflow จะทำอะไรต่อ

✅ **Checkpoint**  `HIGH` เข้า Route 1 ส่วน `MEDIUM` และ `LOW` เข้า Route 2 เท่านั้น

## 📌 Step 8 — Update the Same Row on Both Routes

เพิ่ม `Google Sheets — Update a Row` ใน Route 1 และ Route 2

### Mapping ที่สำคัญ

| Update a Row field | Source |
|---|---|
| Row number | `Row number` จาก `Watch New Rows` |
| Timestamp | `Timestamp` จาก `Watch New Rows` |
| Requester | `Requester` จาก `Watch New Rows` |
| Department | `Department` จาก `Watch New Rows` |
| Request | `Request` จาก `Watch New Rows` |
| Summary | `summary` จาก `Parse JSON` |
| Priority | `priority` จาก `Parse JSON` |
| Reason | `reason` จาก `Parse JSON` |
| Recommended Action | `recommended_action` จาก `Parse JSON` |

ตั้ง `Processing Status` ให้ต่างกันตาม route:

| Route | Processing Status |
|---|---|
| HIGH | `HIGH — HUMAN REVIEW REQUIRED` |
| MEDIUM/LOW | `TRIAGED` |

> ต้องใช้ `Update a Row` และ map `Row number` จาก trigger เพื่อเขียนผลกลับแถวที่ Form สร้างไว้ ห้ามใช้ `Add a Row` ในขั้นนี้ เพราะจะสร้างแถวซ้ำ

> Map ค่าคำตอบเดิมกลับไปด้วย หาก module ที่บัญชีแสดงเขียนทั้งแถว เพราะ field ที่ปล่อยว่างอาจถูกล้างได้

✅ **Checkpoint**  Submit Form 1 ครั้งแล้ว Sheet ยังมีเพียง 1 response row และมีผลวิเคราะห์ครบในแถวเดียวกัน

## 📌 Step 9 — Send Gmail Only for HIGH

หลัง `Update a Row` ใน Route 1 เพิ่ม `Gmail — Send an Email`

- To: อีเมลของผู้เรียนเอง `[Your Email]`
- Subject: ใช้ [HIGH Alert Email Template](prompts.md#high-alert-email-template)
- Body: Map Form fields และ parsed JSON fields

อย่าใส่ Gmail module ใน Route 2

> Email นี้เป็น alert เพื่อให้คนตรวจ ไม่ใช่การอนุมัติ การคืนเงิน การลงโทษ หรือการแก้ปัญหาโดยอัตโนมัติ

✅ **Checkpoint**  HIGH ได้ทั้งผลใน Sheet และอีเมล 1 ฉบับ ส่วน MEDIUM/LOW อัปเดต Sheet แต่ไม่มีอีเมล

⚠️ **Common Problem**  หาก Gmail connection unavailable ให้ใช้ `Processing Status = HIGH — HUMAN REVIEW REQUIRED` เป็น alert marker ซึ่งถือว่าผ่าน Lab 2

## 📌 Step 10 — Test HIGH, MEDIUM, LOW

ใช้ [Test Requests](prompts.md#test-requests) ทีละรายการ โดยกด `Run once` ให้รอก่อนแล้วจึง Submit Form

| Test | Expected Route | Sheet | Gmail |
|---|---|---|---|
| HIGH | Route 1 | Update row + human review status | ส่ง 1 ฉบับ |
| MEDIUM | Route 2 | Update row + `TRIAGED` | ไม่ส่ง |
| LOW | Route 2 | Update row + `TRIAGED` | ไม่ส่ง |

### 🧪 Test Checklist

- [ ] Form มี responses 3 รายการ
- [ ] Sheet มี 3 rows ไม่ใช่ 6 rows
- [ ] ทุก row มี Summary, Priority, Reason และ Recommended Action
- [ ] HIGH email ถูกส่งเพียง 1 ฉบับถึงตนเอง
- [ ] Route filters ไม่ทับกัน
- [ ] ไม่มี API key ใน input/output history ที่แชร์กับผู้อื่น
- [ ] ปิด Scenario schedule หลัง Lab

✅ **Checkpoint**  HIGH, MEDIUM และ LOW เข้า route ถูกต้อง และทุก response มีผล AI ในแถวเดิม

## Optional Recovery Route

หากมีเวลา เพิ่ม error handler สำหรับกรณี Gemini/JSON ผิดรูปแบบ แล้วตั้ง `Processing Status = ERROR — MANUAL REVIEW` โดยไม่ส่ง Gmail อัตโนมัติ

แนวคิดคือระบบต้อง fail visibly: รายการที่ประมวลผลไม่สำเร็จควรเห็นสถานะ ไม่ควรหายเงียบ

## 💬 Discussion

```text
Generative AI: Prompt → Response

AI Agent: Goal → Reason → Decision → Recommendation

Agentic Workflow: Trigger → AI Reasoning → Decision → Tool → Action
```

1. เพราะเหตุใด Google Form เป็น Channel แต่ไม่ได้เป็น Agent?
2. ถ้าใช้ `Add a Row` แทน `Update a Row` จะกระทบ audit trail อย่างไร?
3. เหตุใด HIGH จึงควรแจ้งคน แต่ไม่ควรอนุมัติ action ที่มีผลกระทบสูงเอง?
4. จะป้องกันการประมวลผลซ้ำเมื่อ Scenario retry ได้อย่างไร?

## Fallback without API

หากสร้าง key ไม่ได้, quota เต็ม หรือ Make เชื่อม Gemini ไม่สำเร็จ:

1. ให้ Google Form และ `Watch New Rows` ทำงานตามเดิม
2. ใช้ Google AI Studio จาก Lab 1 วิเคราะห์คำร้องด้วยมือ หรือใช้ [Fallback JSON](prompts.md#fallback-json)
3. ป้อน JSON เข้า Scenario หลังจุด AI หรือใช้ Instructor scenario
4. ทำ Parse JSON, Router และ Update Row ต่อให้ครบ
5. ไม่แชร์ API key ของผู้สอน

```text
Google Form → Sheet → AI (manual/prepared JSON)
→ Router → Update Row → Optional HIGH Alert
```

ผู้เรียนยังได้เรียนรู้ architecture แม้ AI connector ล้มเหลว

## Free-tier Reminder

- Make Free มี credit และ scheduling limits; ตรวจ [Make Pricing](https://www.make.com/en/pricing)
- Gemini Free Tier มี model/rate limits; ไม่รับประกันว่าจะรองรับ 50 accounts พร้อมกัน
- จำกัดการทดสอบและปิด Scenario schedule หลังจบ
- Lab ผ่านเมื่อเห็น decision และ action ไม่จำเป็นต้องเปิดระบบ production

## 🏁 Completed


---

[← Previous: Lab 1](../02-build-ai-agent/README.md) · [Home](../README.md) · [Next: Lab 3 →](../04-generate-management-report/README.md)
