# 04 — Lab 3: Managerial AI — Generate and Deliver a Management Report

[← Previous: Lab 2](../03-build-agentic-workflow/README.md) · [Home](../README.md) · [Next: LINE OA Demo →](../05-line-oa-demo/README.md)

🎯 **Goal**  เปลี่ยน Request History ให้เป็น Management Insight สร้างเอกสาร/PDF เก็บใน Google Drive และส่ง Gmail

⏱ **Estimated Time**  25 นาที

🧰 **Tools**  Make + Google Sheets + Gemini + Google Docs/Drive + Gmail

## Architecture

```text
Request History
↓
Gemini
↓
Pattern Analysis
↓
Management Insight
↓
Generate Report
↓
Create Document
↓
Create PDF
↓
Google Drive
↓
Email
```

## Timebox

| นาที | งาน |
|---:|---|
| 0–4 | เตรียม Request History |
| 4–10 | รวมข้อมูลและให้ Gemini วิเคราะห์ |
| 10–16 | สร้าง Document/PDF |
| 16–21 | บันทึก Drive และส่ง Gmail |
| 21–25 | ตรวจผลและอภิปราย |

> **UI MAY VARY:** ชื่อ action สำหรับอ่านหลายแถว รวมข้อความ สร้าง document แปลง/export PDF อัปโหลด Drive และส่ง Gmail อาจต่างตาม Make version/connection ให้เลือก action ตาม “ผลลัพธ์ที่ต้องการ” และใช้ fallback หากบัญชีไม่แสดง function นั้น อย่าอัปเกรด plan เพื่อจบ Lab

## ก่อนเริ่ม

- [ ] มี `Business Request Log` จาก Lab 2 หรือใช้ [Sample Data](../templates/sample-requests.md)
- [ ] มีอย่างน้อย 6–10 rows และมี pattern ซ้ำ
- [ ] Make เชื่อม Gemini ได้ หรือพร้อมใช้ Google AI Studio fallback
- [ ] Google Drive และ Gmail เป็นบัญชีของตนเอง
- [ ] เปิด [Lab 3 Prompts](prompts.md)

## 📌 Step 1 — Use Request History

เลือกข้อมูลหนึ่งทาง:

1. **Preferred:** rows ที่สะสมจาก Lab 2
2. **Fallback:** คัดลอก subset จาก [Prepared Sample Data](../templates/sample-requests.md)

ตรวจว่าแต่ละรายการมีอย่างน้อย `Department`, `Request`, `Summary`, `Priority`, `Reason`, `Recommended Action`

💡 **Why This Matters**  รายงานผู้บริหารต้องอาศัยหลาย observations เพื่อหา pattern ไม่ใช่สรุปคำร้องเดียว

✅ **Checkpoint**  Dataset มี HIGH/MEDIUM/LOW และมีปัญหาซ้ำอย่างน้อยสอง theme เช่น payment failures, customer complaints หรือ IT access

⚠️ **Common Problem**  ถ้ามีเพียง 3 rows รายงานอาจสรุปได้แต่หา pattern ได้น้อย ให้เพิ่มข้อมูลจำลองจาก template

## 📌 Step 2 — Collect and Aggregate Rows

ใน Make:

1. สร้าง Scenario ใหม่ หรือทำต่อเป็นส่วน report แยกจาก Lab 2
2. ใช้ starting point แบบ run-on-demand สำหรับ Workshop
3. อ่าน rows จาก `Business Request Log`
4. จำกัดจำนวน เช่น 10–20 rows เพื่อลด token/quota
5. รวม rows เป็นข้อความเดียวที่ยังเห็น column labels

ตัวอย่างรูปแบบข้อมูลที่ส่งเข้า Gemini:

```text
Department: IT | Priority: HIGH | Summary: ระบบรับคำสั่งซื้อหยุดทำงาน | Reason: กระทบ operations
Department: Customer Service | Priority: MEDIUM | Summary: ข้อร้องเรียนส่งสินค้าล่าช้าซ้ำ | Reason: ต้องติดตาม
Department: IT | Priority: LOW | Summary: ขอวิธี reset access | Reason: คำขอทั่วไป
```

> อย่าส่งทั้ง Spreadsheet โดยไม่จำกัดขนาด และไม่รวม API key, email จริง หรือ identifiers

💡 **Why This Matters**  Aggregation เปลี่ยนหลาย transactions ให้เป็น analysis context สำหรับ managerial view

✅ **Checkpoint**  Preview ของ aggregated text มีหลาย rows คั่นกันชัดและไม่มีข้อมูลลับ

## 📌 Step 3 — Generate the Management Report

เพิ่ม Gemini step แล้ว map aggregated text ไปยัง `{{REQUEST_DATA}}`

### 📋 Copy This Prompt

```text
You are a management reporting assistant.

Analyze the following business requests
and create a concise weekly management report.

Your goal is NOT to summarize each request separately.

Identify patterns across all requests.

The report must include:

1. Executive Summary
2. Total Requests
3. Priority Distribution
4. Key Issues
5. Recurring Problems
6. Departments Requiring Attention
7. Business Risks
8. Recommended Management Actions
9. Items Requiring Human Review

Write the final report in Thai.

Use this structure:

# Weekly Business Request Report

## Executive Summary

## Request Overview

## Priority Distribution

## Key Issues

## Recurring Patterns

## Departments Requiring Attention

## Business Risks

## Recommended Management Actions

## Human Review Required

Business Request Data:

{{REQUEST_DATA}}
```

💡 **Why This Matters**

> **Operational AI:** “What should we do with this request?”
>
> **Managerial AI:** “What are all these requests telling us about the business?”

เชื่อมกับ MIS:

```text
Data → Information → Insight → Decision → Action
```

| ระดับ | Workshop artifact |
|---|---|
| Data | Individual request |
| Information | Summary + Priority |
| Insight | Patterns + Risks |
| Decision Support | Management recommendation |
| Action | Follow-up owner/approval |

🧪 **Test**  ตรวจว่ารายงานจัดกลุ่ม pattern ข้ามหลาย rows ไม่ใช่ bullet สรุปทุกคำร้องเรียงกัน

✅ **Checkpoint**  รายงานมี 9 sections, total/distribution สอดคล้องกับข้อมูล และ Human Review ระบุชัด

⚠️ **Common Problem**  ถ้าจำนวนไม่ตรง ให้คำนวณ count ใน Sheet/Make แล้วส่งตัวเลขจริงเป็น context อย่าให้ Gemini เดาจำนวนจากข้อมูลที่ถูกตัด

## 📌 Step 4 — Create a Document

1. เพิ่ม Google Docs หรือ document-generation action ที่บัญชี Make รองรับ
2. สร้างเอกสารใหม่จาก report text
3. ตั้งชื่อ:

```text
Weekly Business Request Report — YYYY-MM-DD
```

4. บันทึก source document ใน Drive folder ที่กำหนด

> **UI MAY VARY:** หาก Make ไม่มี action สร้าง Google Doc ในบัญชีปัจจุบัน ให้สร้าง Doc เปล่าด้วยตนเองแล้วใช้ action ที่เขียน/แทน content หรือใช้ [Manual Document Fallback](#manual-document-fallback)

💡 **Why This Matters**  Document เป็น artifact ที่คนอ่าน ตรวจแก้ และอนุมัติได้ก่อนแจกจ่าย

✅ **Checkpoint**  เปิดเอกสารแล้วเห็นหัวข้อและเนื้อหารายงาน ไม่ใช่ JSON หรือ raw array

## 📌 Step 5 — Generate PDF

ใช้ action ที่ทำหน้าที่ export/convert document เป็น PDF

ตั้งชื่อไฟล์:

```text
Weekly-Business-Request-Report-YYYY-MM-DD.pdf
```

ตรวจ MIME/file type ว่าเป็น PDF และขนาดไฟล์มากกว่า 0 bytes

💡 **Why This Matters**  PDF รักษารูปแบบ เหมาะกับการแจกจ่ายและเก็บหลักฐาน แต่การสร้าง PDF เพียงอย่างเดียวไม่ได้ทำให้ระบบเป็น Agentic AI

✅ **Checkpoint**  เปิด PDF ได้และไม่มี API key หรือข้อมูลจริง

⚠️ **Common Problem**  ถ้าได้ link แทนไฟล์ ให้เพิ่มขั้นตอนที่ดาวน์โหลด/export binary ก่อนนำไป attach

## 📌 Step 6 — Save to Google Drive

สร้างโครงสร้าง:

```text
Agentic-AI-Reports/
└── Weekly-Reports/
```

บันทึก PDF ลง `Weekly-Reports`

เหตุผลทางธุรกิจ:

- Single source of truth
- แชร์และควบคุม permission ง่าย
- มี audit trail
- รองรับการค้นย้อนหลัง

✅ **Checkpoint**  เห็น PDF ใน folder ที่กำหนดและ permission เป็น private/restricted โดยค่าเริ่มต้น

⚠️ **Common Problem**  Make หา folder ไม่พบ ให้ตรวจ account/Drive connection และ folder ownership ไม่ต้องเปิด “Anyone with the link”

## 📌 Step 7 — Send Email

ใช้ Gmail action ส่งถึงอีเมลของผู้เรียนเองเท่านั้น

**Subject**

```text
Weekly Business Request Report
```

**Body**

```text
รายงาน Weekly Business Request Report สร้างเรียบร้อยแล้ว

จำนวนคำร้องทั้งหมด:
[Total]

HIGH Priority:
[High Count]

ประเด็นสำคัญ:
[Key Issue]

ไฟล์ PDF ฉบับเต็มแนบมากับ Email นี้
```

Attach `Weekly-Business-Request-Report-YYYY-MM-DD.pdf`

💡 **Why This Matters**  Insight ถูก Deliver ไปยังคนที่รับผิดชอบ แต่ผู้รับยังต้องตรวจและตัดสินใจ

✅ **Checkpoint**  ได้รับอีเมลทดสอบที่ inbox ของตนเองและเปิด attachment ได้

⚠️ **Common Problem**  หาก Gmail authorization ไม่ผ่าน ให้ข้าม email แล้วบันทึก Drive link ใน Sheet/รายงาน ถือว่า Lab สำเร็จด้วย fallback

## 📌 Step 8 — Optional Notification

หากมี notification method ฟรีที่ผู้สอนทดสอบแล้ว สามารถส่งข้อความสั้น:

```text
📊 Weekly Business Request Report พร้อมแล้ว

📄 File:
Weekly-Business-Request-Report-YYYY-MM-DD.pdf

📁 Location:
Google Drive → Agentic-AI-Reports → Weekly-Reports

🔗 Open Report:
[Report Link]

📧 ส่งรายงานทาง Email แล้ว
```

ไม่ใช่ requirement ของ Lab และห้ามใช้ช่องทางองค์กรจริงโดยไม่ได้รับอนุญาต

## Manual Document Fallback

หาก document/PDF/Gmail connector ล้มเหลว:

1. Run management prompt ใน Google AI Studio ด้วย prepared sample data
2. Copy report ไปยัง Google Docs ด้วยตนเอง
3. ใช้ Google Docs download/export เป็น PDF ตาม UI ปัจจุบัน
4. Save ใน Drive folder ของตนเอง
5. Draft email แต่ไม่จำเป็นต้องส่ง หาก permission ไม่พร้อม
6. อธิบายตำแหน่งที่ Workflow จะ automate แต่ละขั้น

Fallback นี้ยังคงเส้นทาง:

```text
Data → AI Analysis → Insight → Artifact → Human Decision
```

## 💬 Discussion

> การสร้าง PDF อย่างเดียวทำให้ระบบเป็น Agentic AI หรือไม่?

ไม่ เพราะ agentic behavior มาจากการรวม:

```text
Observe → Analyze → Decide → Generate → Create Artifact
→ Store → Deliver → Human Decision
```

ถามต่อ:

1. รายงานใดควรส่งอัตโนมัติ และรายงานใดควรให้ Manager approve ก่อน?
2. หากข้อมูลต้นทางไม่ครบ Insight จะน่าเชื่อถือเพียงใด?
3. จะเก็บ feedback ว่าคำแนะนำใดถูกนำไปใช้จริงได้อย่างไร?

## Bridge to LINE Demo and Lab 4

- LINE Demo เปลี่ยน Channel ที่ส่ง Business Request เข้าสู่ Workflow แต่ architecture Lab 2–3 ยังเหมือนเดิม
- Lab 4 ใช้ Business Goal และข้อมูลคล้ายกัน แต่ให้ Manus Agent วางแผนทำ triage + report ใน task เดียว โดยไม่สร้าง Workflow และไม่ทำ external action

ให้จดว่า Lab 2–3 ต้องกำหนด module ใดบ้าง เพื่อนำไปเปรียบเทียบ setup effort, control และ repeatability ใน Lab 4

## 🏁 Completed

- [ ] ใช้ Request History หลายรายการ
- [ ] Gemini สร้าง pattern-based management report
- [ ] สร้าง document และ PDF หรือทำ manual fallback
- [ ] เก็บ PDF ใน Google Drive
- [ ] ส่ง Gmail ถึงตนเองหรือบันทึก Drive link เป็น fallback
- [ ] ระบุ Human Review Required

---

[← Previous: Lab 2](../03-build-agentic-workflow/README.md) · [Home](../README.md) · [Next: LINE OA Demo →](../05-line-oa-demo/README.md)
