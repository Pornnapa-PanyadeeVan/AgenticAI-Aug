# 04 — Lab 3: Managerial AI — HIGH Priority Situation & Follow-up PDF — Step by Step

[← Previous: Lab 2](../03-build-agentic-workflow/README.md) · [Home](../README.md) · [Next: LINE OA Demo →](../05-line-oa-demo/README.md)

🎯 **Goal**  ค้นหา `BR-001` ที่ Lab 2 ตัดสินเป็น `HIGH` แล้วสร้างร่างรายงานสถานการณ์เร่งด่วนสำหรับ Manager, แปลงเป็น PDF, เก็บแบบ restricted และเขียนสถานะกลับแถวเดิม โดยยังต้องมี Human Review

⏱ **Estimated Time**  25 นาที

🧰 **Tools**  Make + Google Sheets + Gemini + Google Drive; Gmail เป็น optional delivery

## วิธีใช้คู่มือนี้

แต่ละ Step บอกให้ครบว่า **คลิกที่ไหน → map อะไร → ต้องเห็นอะไร → ถ่ายภาพตรงไหน** รหัส `L3-xx` เป็นตำแหน่งภาพที่ผู้สอนนำ screenshot จริงมาใส่ภายหลังได้ ดูชื่อไฟล์ทั้งหมดที่ [Screenshot Guide](../images/README.md)

Lab นี้สร้าง Scenario แยกแบบ **run-on-demand** เพื่อค้นหา HIGH row ที่มีอยู่แล้ว ไม่ต้อง Submit Form ซ้ำ และไม่ต่อ module เพิ่มหลัง Lab 2 ระหว่างเรียน

## Continuity from Lab 2

```text
Lab 2
Business Request → Gemini → Priority = HIGH → BR-001 ใน Business Request Log
                                                        ↓
Lab 3
Search BR-001 → Draft Report → Validate → Google Doc → PDF
             → Update BR-001 → Follow-up Status = OPEN → Human Review
```

Lab 3 ไม่สรุปยอดรายสัปดาห์และไม่วิเคราะห์หลายคำร้อง แต่ขยาย **HIGH case หนึ่งรายการ** ให้เป็น management artifact ที่ตอบว่า:

1. เกิดสถานการณ์อะไรและกระทบอะไร?
2. เหตุใดจึงจัดเป็น HIGH จากหลักฐานใด?
3. เรื่องใดต้องได้รับ attention ทันที?
4. ใครต้องรับไปติดตามและต้องยืนยันอะไร?
5. ข้อมูลใดยังขาด?

> รายงานคือ **Decision Support + Follow-up Artifact** ไม่ใช่คำสั่งอนุมัติ ไม่ใช่หลักฐานว่าสาเหตุได้รับการยืนยัน และไม่ใช่การแก้สถานการณ์อัตโนมัติ

## Completed Flow

```text
Google Sheets — Search Rows (Request ID = BR-001 AND Priority = HIGH)
↓
Google Gemini AI — Simple Text Prompt
↓
Human inspects first draft in Run once
↓
Filter — Draft Report Passed
↓
Google Drive — Create a File from Text → convert to Google Docs
↓
Google Drive — Download a File → convert to PDF
↓
Google Drive — Upload a File
↓
Google Sheets — Update a Row (same Row number)
↓
Optional Gmail — Send an Email to self
↓
Human Review / Assign Owner / Confirm Target Time
```

> ใช้ `Google Sheets — Search Rows` แบบมาตรฐาน เพราะ output มี `Row number` สำหรับอัปเดตแถวเดิม อย่าเลือก `Search Rows (Advanced)` ใน Lab นี้ เพราะ module แบบ Advanced ไม่คืน row number

## Timebox

| นาที | งาน |
|---:|---|
| 0–3 | สร้าง restricted folder และ Scenario ใหม่ |
| 3–6 | ค้นหา BR-001 HIGH row |
| 6–11 | สร้างและตรวจ draft report |
| 11–13 | ตั้ง validation filter |
| 13–19 | สร้าง Google Doc, download PDF และ upload PDF |
| 19–22 | อัปเดต BR-001 row เดิม |
| 22–25 | Run once, เปิด PDF และตรวจ tracker |

> **UI MAY VARY:** ชื่อช่องของ Google Drive/Docs, ตำแหน่ง connection และชื่อ output อาจเปลี่ยนตาม Make version และบัญชี ให้ยึดหน้าที่ `create text document → download as PDF → upload PDF` และใช้ [Manual Document Fallback](#manual-document-fallback) หากบัญชีไม่มี module ที่ต้องการ ไม่ต้องซื้อ paid feature เพื่อจบ Lab

## ก่อนเริ่ม

- [ ] Lab 2 มี Spreadsheet `Business Request Log`
- [ ] แถว `BR-001` มี `Priority = HIGH`
- [ ] BR-001 มี Request, Summary, Reason และ Recommended Action
- [ ] Google Drive เป็นบัญชีของตนเอง
- [ ] เปิด [Lab 3 Prompts](prompts.md) อีก tab
- [ ] ใช้ข้อมูลจำลองเท่านั้น
- [ ] Lab 2 และ Lab 3 Scheduling เป็น `OFF`

## 📌 Step 1 — Prepare a Restricted Drive Folder

### Click

1. เปิด [Google Drive](https://drive.google.com/)
2. กด `New` → `New folder`
3. ตั้งชื่อ folder แรก `Agentic-AI-Reports`
4. เปิด folder แล้วสร้าง folder ย่อย `HIGH-Follow-up`
5. คลิกขวาที่ `HIGH-Follow-up` → `Share`

### Configure

1. ตรวจ `General access`
2. ต้องเป็น `Restricted`
3. ไม่เลือก `Anyone with the link`
4. ไม่เพิ่มผู้รับจริงใน Workshop

> 📷 **L3-01 — Restricted Drive folder**: ให้เห็น path `Agentic-AI-Reports/HIGH-Follow-up` และ General access = Restricted โดยปิดชื่อบัญชี

✅ **Checkpoint**  folder อยู่ใน Drive ของตนเองและ permission เป็น Restricted

⚠️ **Common Problem**  ถ้าเป็น Shared Drive และเปลี่ยน permission ไม่ได้ ให้ใช้ My Drive ของตนเองหรือบันทึก PDF local ตาม fallback

## 📌 Step 2 — Create a Separate Report Scenario

### Click

1. เปิด Make → `Scenarios`
2. กด `Create a new scenario`
3. คลิกชื่อ Scenario ด้านบน

### Configure

1. ตั้งชื่อ `Lab 3 — HIGH Situation Follow-up`
2. ตรวจ Scheduling = `OFF`
3. กด `Save`

> 📷 **L3-02 — New report scenario**: ให้เห็นชื่อ Scenario, canvas ว่าง และ Scheduling = OFF

✅ **Checkpoint**  Scenario ใหม่แยกจาก Lab 2 และยังไม่มี trigger ที่รันตามเวลา

## 📌 Step 3 — Search the Existing HIGH Row

### Click

1. คลิกวงกลม `+` กลาง canvas
2. ค้นหา `Google Sheets`
3. เลือก **`Search Rows` แบบมาตรฐาน**
4. อย่าเลือก `Search Rows (Advanced)`

### Configure

| Field | Value |
|---|---|
| Connection | บัญชีเดียวกับ Lab 2 |
| Spreadsheet | `Business Request Log` |
| Sheet | `Form Responses 1` หรือชื่อ tab จริง |
| Table contains headers | `Yes` |
| Range | `A:M` หรือ range ที่ครอบคลุม 13 columns |
| Filter 1 | `Request ID` Equal to `BR-001` |
| Filter 2 | `Priority` Equal to `HIGH` |
| Filter relationship | `AND` |
| Limit | `1` |

ถ้า UI ให้ sort ให้เรียง Timestamp ล่าสุดก่อน แต่ Request ID ใน Workshop ต้องไม่ซ้ำอยู่แล้ว

### Test This Module First

1. กด `OK`
2. คลิกขวาที่ module แล้วเลือก `Run this module only` ถ้ามี หรือกด `Run once`
3. คลิก operation bubble เหนือ module
4. ขยาย `Bundle 1`
5. ต้องเห็น `Row number`, Request ID = BR-001, Priority = HIGH และข้อมูลต้นทางครบ

> 📷 **L3-03 — Search HIGH row**: ให้เห็น filter BR-001 + HIGH, Limit 1 และ output Row number

✅ **Checkpoint**  Search คืน 1 bundle พร้อม `Row number`

⚠️ **Common Problem**  ถ้าได้ 0 bundles ให้ตรวจตัวสะกด `BR-001`, ค่า `HIGH`, ชื่อ tab และ header row ถ้าไม่มี Row number แปลว่าเลือก Advanced module ให้เปลี่ยนเป็น Search Rows แบบมาตรฐาน

## 📌 Step 4 — Generate and Inspect the Draft Report

### Click

1. คลิก `+` หลัง Search Rows
2. เลือก `Google Gemini AI`
3. เลือก `Simple Text Prompt` หรือ text-generation action ที่ทำหน้าที่เดียวกัน

### Configure

1. เลือก Gemini connection เดียวกับ Lab 2
2. เลือก model ที่บัญชีใช้ได้ใน Free Tier
3. Copy prompt ฉบับเต็มจาก [HIGH Priority Situation Report Prompt](prompts.md#high-priority-situation-report-prompt)
4. ในส่วน `HIGH Case Data` map tokens จาก Search Rows ตามโครงนี้:

```text
Report Generated At: {{current run time}}
Request ID: {{Request ID}}
Requester: {{Requester}}
Department: {{Department}}
Original Request: {{Request}}
AI Summary: {{Summary}}
Priority: {{Priority}}
Priority Reason: {{Reason}}
Recommended Action: {{Recommended Action}}
Current Follow-up Status: {{Follow-up Status}}
```

5. ช่องที่ไม่มีข้อมูลให้ใส่ `NOT PROVIDED` อย่าให้ AI เดา
6. กด `OK` และ `Save`

> 📷 **L3-04 — Report prompt mapping**: ให้เห็น prompt และ tokens จาก Search Rows โดยไม่เห็น secret

### Run a Draft-only Test

ก่อนต่อ Drive modules ให้ทดสอบเพียง Search Rows + Gemini:

1. กด `Run once`
2. คลิก bubble ของ Gemini
3. เปิด text output และอ่านเนื้อหา
4. ตรวจว่ามีข้อความต่อไปนี้:
   - `DRAFT — HIGH PRIORITY — HUMAN REVIEW REQUIRED`
   - `Request ID: BR-001`
   - เหตุผลที่จัดเป็น HIGH จาก source
   - ข้อมูลที่ยังขาด
   - Human Review Sign-off
5. ตรวจว่าไม่มี owner, deadline, amount หรือ root cause ที่ source ไม่ได้ให้
6. ตรวจว่าไม่มีคำว่า `RESOLVED`
7. ถ้าไม่ผ่าน ใช้ [Correction Prompt](prompts.md#correction-prompt) แล้ว Run once ใหม่

> 📷 **L3-05 — Draft report output**: ให้เห็น DRAFT banner, Request ID, missing information และ Human Review section

✅ **Checkpoint**  Draft อ่านได้และอ้างอิงแค่ BR-001 โดยไม่แต่งข้อเท็จจริง

## 📌 Step 5 — Add a Structural Validation Filter

Filter นี้ช่วยกัน output ที่ผิดโครงสร้าง แต่ **ไม่แทนการอ่านและอนุมัติของคน**

### Click

1. คลิกเส้นด้านขวาหลัง Gemini หรือเพิ่ม module ถัดไปก่อนแล้วคลิกเส้นเชื่อม
2. เลือก `Set up a filter`
3. ตั้งชื่อ `Draft report passed`

### Configure

ตั้ง condition แบบ `AND`:

| Check | Condition |
|---|---|
| Source priority | Priority จาก Search Rows `Equal to` `HIGH` |
| Draft label | Gemini text `Contains` `DRAFT — HIGH PRIORITY — HUMAN REVIEW REQUIRED` |
| Traceability | Gemini text `Contains` Request ID จาก Search Rows |
| Open status | Gemini text `Does not contain` `RESOLVED` |

> Filter ตรวจรูปแบบและ traceability เท่านั้น คนยังต้องตรวจ evidence, unsupported claims และความเหมาะสมของ action

> 📷 **L3-06 — Report validation filter**: ให้เห็นชื่อ filter และเงื่อนไขทั้ง 4 ข้อ

✅ **Checkpoint**  Draft ที่ไม่มี label หรือเขียน RESOLVED จะไม่ผ่านไปสร้าง PDF

## 📌 Step 6 — Create a Google Document from the Draft

### Click

1. คลิก `+` หลัง validation filter
2. เลือก `Google Drive`
3. เลือก `Create a File from Text`

### Configure

| Field | Value |
|---|---|
| Connection | บัญชี Google Drive ของตนเอง |
| Drive | `My Drive` |
| Folder/Location | `Agentic-AI-Reports/HIGH-Follow-up` |
| File name | `DRAFT HIGH Situation Report — {{Request ID}} — {{YYYY-MM-DD}}` |
| Content/Data | text output จาก Gemini |
| Convert to Google Docs | `Yes` |

ใช้วันที่จาก Make date function หากทำได้ หรือพิมพ์วันที่ Workshop สำหรับการทดลองหนึ่งครั้ง

> 📷 **L3-07 — Create a File from Text**: ให้เห็น folder, filename tokens, content mapping และ Convert to Google Docs = Yes

✅ **Checkpoint**  Run once แล้ว Drive มี Google Document เปิดอ่านได้และชื่อมี BR-001

⚠️ **Common Problem**  ถ้าได้ไฟล์ `.txt` ให้ตรวจ `Convert to Google Docs = Yes` ถ้าบัญชีไม่มีตัวเลือกนี้ ใช้ Google Docs `Create a Document` หรือ [Manual Document Fallback](#manual-document-fallback)

## 📌 Step 7 — Convert to PDF and Upload It

### 7.1 Download the Google Document as PDF

1. คลิก `+` หลัง Create a File from Text
2. เลือก Google Drive → `Download a File`
3. ที่ File ID map ID จาก module ที่สร้าง Google Document
4. ที่ conversion/export format เลือก `PDF`
5. กด `OK`

> 📷 **L3-08 — Download as PDF**: ให้เห็น File ID token และ PDF export format

### 7.2 Upload the PDF

1. คลิก `+` หลัง Download a File
2. เลือก Google Drive → `Upload a File`
3. เลือก folder `Agentic-AI-Reports/HIGH-Follow-up`
4. ตั้งชื่อ `DRAFT-HIGH-Situation-Report-{{Request ID}}-{{YYYY-MM-DD}}.pdf`
5. ที่ File/Data map binary data จาก Download a File
6. ถ้ามีช่อง MIME type ให้ใช้ `application/pdf`
7. กด `OK`

> 📷 **L3-09 — Upload PDF**: ให้เห็น restricted folder, PDF filename และ binary data mapping

### Check the Artifact

1. Run once
2. เปิด Drive folder
3. เปิด PDF และเลื่อนดูทุกหน้า
4. ตรวจว่าขนาดไฟล์มากกว่า 0 bytes
5. เปิด Share dialog ตรวจว่ายัง Restricted

✅ **Checkpoint**  PDF เปิดได้ ชื่อไฟล์มี BR-001 และเนื้อหายังมี DRAFT/Human Review label

⚠️ **Alternative module path**  ถ้า Google Drive `Download a File` ในบัญชีไม่ให้เลือก PDF ให้ใช้ `Google Docs → Download a Document` แล้วเลือก PDF จากนั้น map binary output เข้า Upload a File

## 📌 Step 8 — Update the Original BR-001 Row

### Click

1. คลิก `+` หลัง Upload a File
2. เลือก Google Sheets → `Update a Row`
3. เลือก Spreadsheet และ Sheet เดียวกับ Lab 2

### Configure

| Field | Mapping / Value |
|---|---|
| Row number | `Row number` จาก Search Rows |
| Timestamp ถึง Recommended Action | map ค่าเดิมจาก Search Rows กลับทุกช่อง |
| Processing Status | map ค่าเดิมจาก Search Rows |
| Report Status | `DRAFT — HUMAN REVIEW REQUIRED` |
| Report Link | restricted web-view link จาก Upload a File |
| Follow-up Status | `OPEN` |

> ถ้า Upload module ไม่คืน web-view link ให้เปิด Drive แล้ว copy restricted link มาใส่ใน Sheet ด้วยตนเองสำหรับ Workshop

> ต้องใช้ `Update a Row` และ Row number จาก **standard Search Rows** ห้ามใช้ `Add a Row` เพราะ BR-001 ต้องมี audit trail อยู่แถวเดียว

> 📷 **L3-10 — Update follow-up row**: ให้เห็น Row number token, Report Status, Report Link mapping และ Follow-up Status = OPEN

✅ **Checkpoint**  BR-001 แถวเดิมมี report link และ OPEN โดยไม่มีแถวใหม่

⚠️ **Common Problem**  ถ้าข้อมูลเดิมหาย แปลว่า module เขียนทั้งแถวและไม่ได้ map source values กลับ ให้ map A–J จาก Search Rows แล้ว Run once ใหม่กับแถวเดิม

## 📌 Step 9 — Optional Gmail to Self

ข้ามขั้นนี้ได้หาก Gmail connection ไม่พร้อม PDF + tracker ที่อัปเดตแล้วถือว่าผ่าน Lab

### Click and Configure

1. คลิก `+` หลัง Update a Row
2. เลือก Gmail → `Send an Email`
3. ใส่ To เป็นอีเมลของตนเองเท่านั้น
4. ตั้ง Subject:

```text
[DRAFT][HIGH][Human Review] {{Request ID}} — โปรดติดตามสถานการณ์เร่งด่วน
```

5. Copy body จาก [Lab 3 Email Template](prompts.md#email-template) แล้ว map Request ID, Department, Summary และ restricted link
6. ถ้าต้องการแนบ PDF ให้ map File name และ Data จาก Download a File
7. ถ้า attachment mapping ไม่พร้อม ให้ใส่ restricted Drive link แทน

> 📷 **L3-11 — Optional report email**: ให้เห็น subject, body tokens และ PDF attachment mapping โดยปิด email address

✅ **Checkpoint**  ได้รับอีเมล DRAFT หนึ่งฉบับที่ inbox ของตนเอง ไม่มีผู้รับภายนอก

## 📌 Step 10 — Save and Run the Complete Scenario Once

1. กด `Save`
2. ตรวจ Scheduling = `OFF`
3. กด `Run once`
4. ไล่คลิก operation bubble จาก Search Rows ถึง Update a Row
5. Search Rows ต้องคืน 1 bundle
6. Validation filter ต้องผ่าน 1 bundle
7. PDF download/upload ต้องมี file data และขนาดมากกว่า 0
8. เปิด PDF จาก Drive และตรวจทุกหน้า
9. เปิด Business Request Log ตรวจ BR-001 row เดิม
10. ตรวจว่าไม่มี row ซ้ำและ Gmail ส่งไม่เกินหนึ่งฉบับ

> 📷 **L3-12 — Complete report scenario**: ให้เห็น flow ครบจาก Search Rows ถึง Update Row/Gmail และ Scheduling = OFF

> 📷 **L3-13 — Final PDF and tracker**: ให้เห็น PDF แบบ DRAFT และ BR-001 row ที่ Report Status/Link/Follow-up ถูกอัปเดต โดยปิดข้อมูลบัญชี

### Final Validation Checklist

- [ ] Source เป็น Request ID เดียวและ Priority = HIGH
- [ ] รายงานมี DRAFT — HUMAN REVIEW REQUIRED
- [ ] ไม่มี root cause, amount, owner, deadline หรือ SLA ที่ source ไม่ได้ให้
- [ ] ทุก proposed action ระบุว่า pending human confirmation
- [ ] Follow-up status เป็น OPEN หรือ PENDING VALIDATION ไม่ใช่ RESOLVED
- [ ] PDF เปิดได้และ permission เป็น Restricted
- [ ] BR-001 row เดิมถูกอัปเดต ไม่มี row ซ้ำ
- [ ] Scenario schedule ยังปิด

✅ **Checkpoint**  Manager เปิด PDF ตรวจเหตุการณ์ได้ และ tracker ยังบอกชัดว่างานต้องติดตามต่อ

## Manual Document Fallback

หาก Create/Download/Upload module ไม่พร้อม:

1. Run Search Rows + Gemini ใน Make
2. ตรวจ report ด้วย Final Validation Checklist
3. Copy text ไป Google Docs ด้วยตนเอง
4. เลือก `File` → `Download` → `PDF Document (.pdf)`
5. Upload PDF ไป restricted folder
6. Copy restricted link
7. อัปเดต Report Status, Report Link และ Follow-up Status ใน BR-001 row ด้วยตนเอง
8. อธิบายว่าในระบบจริง Make จะ automate จุดใด

Fallback ยังคง Learning Path:

```text
HIGH Decision → Situation Report → Validate → PDF → OPEN Follow-up → Human Review
```

## 💬 Discussion

1. เหตุใด PDF ของ HIGH case ต้องติดป้าย DRAFT?
2. หาก AI แต่ง owner หรือ deadline เอง จะเกิดความเสี่ยงอะไร?
3. เหตุใด Lab นี้ใช้ Search Rows แล้ว Update Row แทน Add Row?
4. เมื่อใด OPEN จึงเปลี่ยนเป็น RESOLVED และใครมีสิทธิ์เปลี่ยน?
5. Filter ตรวจโครงสร้างได้ แต่เหตุใดจึงยังแทน Human Review ไม่ได้?

## Bridge to LINE Demo and Lab 4

- LINE Demo เปลี่ยน Channel ที่รับคำร้อง แต่ HIGH decision ยังต้องเข้า report/follow-up control เดียวกัน
- Lab 4 ให้ Antigravity Workspace Agent triage dataset แล้วสร้าง draft report files สำหรับทุก HIGH case ภายใน project scope โดยไม่ประกอบ Make Workflow และไม่ทำ external action

ให้จดว่า Lab 2–3 ต้องกำหนด Trigger/Search, Router, document, PDF, Drive และ tracker update เอง เพื่อนำไปเปรียบเทียบ control, repeatability และ setup effort กับ Lab 4

## 🏁 Completed

- [ ] ค้นหา BR-001 HIGH row ด้วย standard Search Rows
- [ ] สร้าง Situation & Follow-up Report จาก source evidence เท่านั้น
- [ ] ตรวจ draft ก่อนเปิดเส้นทางสร้าง PDF
- [ ] ใช้ validation filter เป็น structural guardrail
- [ ] สร้าง Google Document และ PDF หรือใช้ manual fallback
- [ ] เก็บไฟล์แบบ restricted
- [ ] อัปเดต BR-001 row เดิมเป็น Report Status = DRAFT และ Follow-up Status = OPEN
- [ ] ส่งอีเมลถึงตนเองหรือข้าม optional delivery
- [ ] เปิดตรวจ PDF และปิด Scenario schedule

---

[← Previous: Lab 2](../03-build-agentic-workflow/README.md) · [Home](../README.md) · [Next: LINE OA Demo →](../05-line-oa-demo/README.md)
