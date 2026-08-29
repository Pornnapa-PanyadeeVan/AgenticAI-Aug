# Instructor Checklist — 50-person Workshop

[← Home](../../README.md) · [Troubleshooting](../../troubleshooting/README.md)

ใช้ checklist นี้ก่อนสอน `Build Your First Agentic AI for Business` ทุกครั้ง เพราะ free-tier eligibility, quota และ UI เปลี่ยนได้

## 7–14 วันก่อนสอน

### Account and Access

- [ ] ผู้เรียนมี Google Account ที่ได้รับอนุญาตให้ใช้บริการภายนอก
- [ ] ทดสอบ [Google AI Studio](https://aistudio.google.com/) ด้วยบัญชีประเภทเดียวกับผู้เรียน
- [ ] ทดสอบว่ามองเห็นพื้นที่ System Instructions
- [ ] ทดสอบ Make account creation/verification
- [ ] ทดสอบ Google Forms, Google Sheets, Google Docs, Google Drive และ Gmail
- [ ] ตรวจว่าบัญชีตัวอย่างสร้าง Gemini API key แบบ free tier ได้โดยไม่เปิด billing
- [ ] ตรวจ restrictions ของบัญชีโรงเรียน/องค์กรและประเทศ
- [ ] ไม่ใช้ instructor API key ร่วมกันทั้งห้อง
- [ ] ตรวจเครื่องผู้เรียนว่า install [Google Antigravity](https://antigravity.google/download) ได้ตาม OS requirement และ Sign in ได้
- [ ] ทดสอบ Antigravity individual tier, New Project, Project Settings, plan review และการสร้าง report หนึ่งไฟล์
- [ ] เตรียมหนึ่งเครื่อง/หนึ่ง dedicated project ต่อทีม ไม่เปิดทั้ง Desktop หรือ Downloads เป็น project scope

### Make Connections

- [ ] ทดสอบ connection ไป Gemini ด้วย key สำหรับ demo
- [ ] ทดสอบ Google Sheets read/write
- [ ] ทดสอบ Form → response sheet → `Watch New Rows` และเห็น `Row number`
- [ ] ทดสอบ `Update a Row` ทั้ง HIGH และ MEDIUM/LOW โดยไม่เกิดแถวซ้ำ
- [ ] ทดสอบ Router/filters ด้วย exact Priority values
- [ ] ทดสอบ Lab 3 โดยต่อ report/PDF modules บน HIGH route และ map `Row number` จาก `Watch New Rows`
- [ ] ทดสอบ `Create a File from Text` → Convert to Google Docs ด้วยบัญชีปัจจุบัน
- [ ] ทดสอบ `Download a File` → PDF หรือเตรียมทางเลือก `Google Docs — Download a Document`
- [ ] ทดสอบ `Upload a File` ว่าได้รับ binary PDF มากกว่า 0 bytes และ link ยัง Restricted
- [ ] ทดสอบ Update HIGH row เดิมด้วย Row number, Report Status/Link และ Follow-up = OPEN
- [ ] ทดสอบ Gmail ส่งถึงอีเมลทดสอบของผู้สอนเอง
- [ ] ปิด schedule ของ scenario หลังทดสอบ

### Free-tier and Capacity

- [ ] ตรวจ [Gemini API Pricing](https://ai.google.dev/gemini-api/docs/pricing)
- [ ] ตรวจ [Gemini API Rate Limits](https://ai.google.dev/gemini-api/docs/rate-limits)
- [ ] ตรวจ [Make Pricing/Credits](https://www.make.com/en/pricing)
- [ ] ตรวจ [Antigravity Pricing](https://antigravity.google/pricing), [Download](https://antigravity.google/download), [Docs](https://antigravity.google/docs/home) และ [Changelog](https://antigravity.google/changelog)
- [ ] ยืนยันว่าไม่มี Lab บังคับ paid model, paid Make feature, Antigravity paid plan, multi-agent teamwork หรือ Cloud Billing
- [ ] จำกัด Lab 2 คนละ 3–5 Gemini requests
- [ ] Lab 3 ใช้ HIGH row จำลองเพียงหนึ่งรายการต่อทีม
- [ ] Lab 4 ใช้ dataset 4 rows, หนึ่ง task, หนึ่ง output file และหนึ่ง Antigravity project/conversation ต่อทีม
- [ ] วางแผนกระจายเวลาสร้าง API keys ไม่ให้ 50 คนทำพร้อมกันวินาทีเดียว
- [ ] เตรียม quota/rate-limit fallback

## 2–3 วันก่อนสอน

### Materials

- [ ] เปิดลิงก์ทุก Lab จาก [README](../../README.md)
- [ ] ส่ง [Glossary คำศัพท์พื้นฐาน](../../01-introduction/glossary.md) เป็น pre-read และเตรียมอธิบาย Agent, Skill, Tool, Connector, MCP, Workflow, Guardrail
- [ ] ตรวจ Previous / Home / Next navigation
- [ ] เตรียม [Sample Requests](sample-requests.md) อย่างน้อย 20 รายการ
- [ ] เตรียม Google Form และ linked response sheet สำหรับ Lab 2 fallback
- [ ] เตรียมสำเนา sample data ใน Sheet ของผู้สอน
- [ ] เตรียม fallback JSON จาก [Lab 2 Prompts](../02-build-agentic-workflow/prompts.md#fallback-json)
- [ ] เตรียม fallback HIGH case และ Situation Report จาก [Lab 3 Prompts](../03-generate-management-report/prompts.md)
- [ ] เตรียม [Antigravity Lab Input](business-requests.md) และ [Lab 4 Prompts](../04-antigravity/prompts.md)
- [ ] Run Antigravity project ล่วงหน้าและเก็บ Instructor fallback ที่เห็น short plan, human proceed และ `business-request-management-report.md`
- [ ] เตรียม blank Google Doc และ Drive folders สำหรับ fallback
- [ ] เตรียม PDF ตัวอย่างที่ไม่มีข้อมูลจริง
- [ ] เตรียม architecture comparison สำหรับ 13–17 ทีม
- [ ] เตรียม Optional MBA Challenge worksheet สำหรับ Assignment หากใช้
- [ ] เตรียม Exit Ticket

### Screenshots and Demo

- [ ] ตรวจรายการภาพประกอบในคู่มือของแต่ละ Lab
- [ ] ถ่าย Lab 2 ให้ครบ `L2-01` ถึง `L2-17` และ Lab 3 ให้ครบ `L3-01` ถึง `L3-13`
- [ ] เตรียมภาพหลัก Lab 4: Create Project, Guardrails, Agent Plan และ Plan Approval
- [ ] ปิด API key, email, IDs และ webhook URLs ในทุกภาพ
- [ ] ใส่ `UI MAY VARY` และวันที่ถ่าย
- [ ] ทดสอบ flow สดหนึ่งรอบ HIGH/MEDIUM/LOW
- [ ] บันทึกภาพหรือวิดีโอ fallback ของ run ที่สำเร็จ
- [ ] หากสาธิต LINE OA ให้ใช้ demo account/channel เท่านั้น
- [ ] เตรียม LINE architecture-only fallback
- [ ] ถ่าย Antigravity Project Settings, plan review และ report หนึ่งไฟล์ โดยปิด account/path details ที่ไม่จำเป็น
- [ ] เตรียม Antigravity recorded/instructor project fallback หาก install, quota หรือ sign-in ไม่พร้อม

### Room and Network

- [ ] Wi‑Fi รองรับ browser sessions ประมาณ 50 คน
- [ ] เตรียม QR/short link ไป repository
- [ ] แนะนำจับคู่ 2 คนต่อเครื่องหาก Wi‑Fi หรือ account จำกัด
- [ ] เตรียม projector scaling และ browser zoom
- [ ] มีช่องทางประกาศ “หยุด API test” เมื่อ quota เริ่มมีปัญหา
- [ ] แบ่งผู้ช่วยดูแลประมาณ 1 คนต่อผู้เรียน 12–15 คนหากทำได้

## วันสอน — ก่อนเริ่ม 60 นาที

- [ ] Sign in Google AI Studio และ Make ด้วย demo account
- [ ] ตรวจว่า model ที่เลือกยังมี free-tier access
- [ ] Run Lab 1 test case หนึ่งรายการ
- [ ] Submit Google Form แล้ว Run Lab 2 HIGH request end-to-end
- [ ] ตรวจว่า response row ใน Business Request Log ถูกอัปเดตโดยไม่สร้างแถวซ้ำ
- [ ] Run Lab 3 ด้วย HIGH request ใหม่และตรวจว่า report/PDF modules ใช้ bundle กับ Row number เดิม
- [ ] ตรวจ Lab 3 path `Create text → Google Doc → Download PDF → Upload PDF → Update same row`
- [ ] ตรวจว่า PDF ยังเป็น DRAFT และ Scheduling ยัง OFF
- [ ] เปิด PDF จาก Drive
- [ ] ส่ง Gmail ถึงตนเองและเปิด attachment
- [ ] ตรวจ Make credit/quota dashboard
- [ ] เปิด Antigravity และตรวจว่า Instructor fallback project/conversation ยังเข้าถึงได้
- [ ] ตรวจ Project มี dedicated folder เดียว, Security Preset = Default และ Artifact Review = Always Ask
- [ ] เปิด Lab 4 short plan และ `business-request-management-report.md` ให้พร้อมสาธิต
- [ ] เปิด browser tabs: repository, AI Studio, Forms, Make, Sheets, Drive, Gmail และเปิด Antigravity desktop แยกไว้
- [ ] เปิด troubleshooting และ fallback files
- [ ] ลบผล demo เก่าที่อาจทำให้ผู้เรียนสับสน แต่ไม่ลบ audit ที่ต้องเก็บ

## Class Setup สำหรับ 50 คน

### Grouping

- [ ] ให้ผู้เรียนทำ Lab 1 รายบุคคลหรือคู่
- [ ] Lab 2–3 อนุญาตจับคู่เพื่อช่วยเรื่อง connection/quota
- [ ] กำหนดตัวแทนทีมเพียงหนึ่งคนกด Run ใน Make
- [ ] Lab 4 ทีมละ 3–4 คนและมี Operator เพียงหนึ่งคนควบคุม Antigravity project/approval
- [ ] MBA Challenge เป็น Optional Assignment ไม่อยู่ใน core 3 ชั่วโมง

### Timing Guardrails

- [ ] 00:20 เริ่ม Lab 1
- [ ] 00:50 หยุด Lab 1 และเริ่ม Lab 2
- [ ] 01:15 ผู้ที่ API ยังไม่ผ่านเปลี่ยนเป็น fallback JSON
- [ ] 01:30 พัก 10 นาที
- [ ] 01:40 เริ่ม Lab 3 โดยเปิด Scenario ของ Lab 2 เดิม ต่อ report/PDF modules บน HIGH route แล้ว Submit HIGH request ใหม่
- [ ] 01:55 ผู้ที่ PDF connector ไม่ผ่านใช้ manual document fallback
- [ ] 02:05 เริ่ม LINE OA Instructor Demo
- [ ] 02:15 เริ่ม Lab 4 Antigravity พร้อมกันเป็นทีม
- [ ] 02:20 ทีมที่ installation/sign-in/quota ไม่พร้อมใช้ Instructor project fallback
- [ ] 02:30 เริ่ม Responsible AI + Architecture Comparison + Wrap-up

## Risk Register

| Risk | Early warning | Mitigation | Fallback |
|---|---|---|---|
| Gemini API rate limit | 429/quota messages หลายคน | ลด run, stagger teams, ใช้สั้นลง | Lab 1 manual AI + fallback JSON |
| Free-tier model unavailable | Model หาย/ขอ billing | ใช้ model ฟรีที่บัญชีแสดง | Instructor output/sample JSON |
| API key creation blocked | ไม่มี create option/permission | จับคู่กับผู้เรียนที่มีสิทธิ์โดยไม่แชร์ key | Instructor scenario หรือ manual simulation |
| Make module differences | หา action ตามชื่อไม่พบ | สอนตาม function และ screenshot วันที่ล่าสุด | Architecture card/manual mapping |
| Make account verification | เข้า builder ไม่ได้ | ตรวจล่วงหน้า/จับคู่ | ผู้เรียนออกแบบบน worksheet |
| Make credits low | dashboard ใกล้ limit | จำกัด 3 runs ปิด schedule | Use recorded run/sample output |
| Slow Wi‑Fi | หน้าโหลดช้า/timeouts | จับคู่ ลด tabs หยุด simultaneous runs | Instructor-led walkthrough |
| Google account restrictions | OAuth blocked | ใช้บัญชีที่สถาบันอนุญาต | Manual copy/paste path |
| Form/Watch Rows ไม่ทำงาน | Form ไม่ได้ link Sheet, เลือก tab/start point ผิด | link Sheet และกด `Run once` ก่อน Submit | Prepared response bundle |
| Sheets connection fail | file/columns ไม่แสดง | refresh headers/connection | Paste rows manually |
| Update Row ผิดแถว/เกิดแถวซ้ำ | ใช้ Add Row หรือไม่ได้ map `Row number` | ใช้ Update Row และ map row number จาก trigger | Update prepared row ด้วยมือ |
| Gmail authorization fail | OAuth denied | ใช้ email ตนเอง/ตรวจ permission | Save Drive link only |
| PDF generation fail | ได้ text/link ไม่ใช่ PDF | ตรวจ export/binary path | Google Docs manual export |
| 50 API keys พร้อมกัน | throttling/verification delay | stagger 5 กลุ่ม | แชร์ผลผ่าน projector ไม่แชร์ key |
| Antigravity install/sign-in ไม่พร้อม | App เปิดไม่ได้, OS ไม่รองรับ หรือ account blocked | ติดตั้ง/ทดสอบล่วงหน้าและจับทีม | Instructor completed project/recording |
| Antigravity quota ไม่พอ | Agent start ไม่ได้หรือ usage warning | หนึ่ง project/conversation ต่อทีม, dataset 4 rows, compact prompt | Plan-only หรือ Instructor project |
| Project scope/permission กว้างเกิน | เลือก Desktop/Downloads หรือ Agent ขอ access นอก folder | dedicated folder + review-driven settings + reject permission | สร้าง project ใหม่หรือใช้ recorded run |
| Antigravity ทำงานนอกขอบเขต | เสนอ app, browser, MCP, schedule, package install หรือ external action | Stop, ใช้ boundary correction prompt และ review plan ใหม่ | วิเคราะห์ prepared artifacts |
| Sensitive data ถูก paste | พบชื่อ/email จริง | หยุด run และลบจาก workspace/history ตาม policy | ใช้ sample dataset ใหม่ |

## Fallback Ladder

ใช้ระดับต่ำสุดที่ยังรักษา Learning Objective:

### Level A — Full Hands-on

```text
Google Form → Sheet → Make → Gemini → JSON → Router
→ Update Row/HIGH Alert → if HIGH → DRAFT Situation Report
→ PDF → Restricted Drive → OPEN Tracker → Human Review
```

### Level B — AI Manual, Workflow Hands-on

```text
Input → Google AI Studio → Copy JSON → Make Router → Sheet
```

### Level C — Prepared Output

```text
Prepared JSON → Make Router → HIGH row → Prepared DRAFT report
```

### Level D — Manual Simulation

```text
Input card → Team applies AI rules → Decision card → Action card
→ HIGH case card → Follow-up report + Human Review discussion
```

> Workshop ต้องสำเร็จได้แม้ automation connectors fail ผู้เรียนยังต้องอธิบาย Goal, Reasoning, Decision, Action, Data และ Human Oversight

### Antigravity Lab Fallback

```text
Student project + reviewed plan
↓ unavailable
Instructor completed project
↓ unavailable
Plan-only / Chat comparison
↓ unavailable
Team simulates Goal Owner → Planner → Tool Operator → Reviewer
```

Learning Objective คือการเปรียบเทียบ orchestration, bounded tool use และ approval ไม่ใช่การใช้ quota ให้หมด

## Security Checklist

- [ ] ใช้ข้อมูลจำลองเท่านั้น
- [ ] ไม่ใส่ API key ใน GitHub, Prompt, Sheet หรือ screenshot
- [ ] ไม่มีอีเมลจริงใน repository; ใช้ `[Your Email]`
- [ ] ใช้ least-privilege connections
- [ ] ส่ง Gmail ถึงตนเองเท่านั้น
- [ ] Drive files private/restricted
- [ ] ปิด Scenario schedule หลังจบ
- [ ] Rotate/revoke demo key หลัง class หากไม่ใช้ต่อ
- [ ] ไม่บันทึกหน้าจอที่มี secret
- [ ] ไม่สาธิต high-impact automatic action
- [ ] Antigravity ใช้ dedicated project และ `business-requests.md`; ไม่เปิด browser, Connector, MCP, terminal, schedule, package install หรือ external action
- [ ] Review short plan และ report หนึ่งไฟล์ก่อนยอมรับ และ reject access นอก project

## หลังสอน

- [ ] ปิด scenario schedules/webhooks ที่ไม่ใช้
- [ ] ลบหรือ anonymize test data ตาม retention plan
- [ ] Rotate/revoke workshop API keys ที่ไม่ใช้
- [ ] ตรวจ Make credits/quota
- [ ] ตรวจ Antigravity project/conversation/artifact retention และลบ local demo project ตามแผนเมื่อไม่ใช้
- [ ] เก็บ feedback ว่า issue ใดเกิดบ่อย
- [ ] Update troubleshooting และ screenshots
- [ ] ตรวจลิงก์ free-tier/pricing ก่อนรอบถัดไป
- [ ] บันทึก UI/module ที่เปลี่ยน แต่หลีกเลี่ยงคำรับประกันชื่อเมนู

---

[← Home](../../README.md) · [Troubleshooting](../../troubleshooting/README.md)
