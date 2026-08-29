# Lab 2 — Google Form Workflow Prompts and Test Data

[← Lab 2 Guide](README.md) · [Home](../README.md) · [Next: Lab 3 Prompts →](../04-generate-management-report/prompts.md)

> ใช้ simulated data เท่านั้น ปิดการเก็บ email ใน Form ถ้าไม่จำเป็น และห้ามวาง API key ใน Prompt, Form หรือ Sheet

## Business Request JSON Prompt

Map ค่า `{{REQUESTER}}`, `{{DEPARTMENT}}` และ `{{BUSINESS_REQUEST}}` จาก output ของ `Google Sheets — Watch New Rows`

```text
You are a Business Request Assistant.

Analyze the request using business impact, not urgency words alone.

Return ONLY one valid JSON object.
Do not use Markdown or code fences.

Use exactly these keys:

{
  "summary": "",
  "priority": "HIGH",
  "reason": "",
  "recommended_action": ""
}

The priority value must be exactly one of:
HIGH, MEDIUM, LOW

Priority rules:

HIGH:
- immediate customer impact
- significant revenue or financial impact
- critical operations disruption
- serious compliance or reputation risk
- a short deadline with material business impact if missed

MEDIUM:
- important and needs attention
- a deadline within several days
- operations can continue

LOW:
- routine administration or general information
- no immediate impact
- no material urgent deadline

Do not classify HIGH only because the request says
"urgent", "ASAP", "ทันที", "ด่วน" or similar words.

Requester:
{{REQUESTER}}

Department:
{{DEPARTMENT}}

Business Request:
{{BUSINESS_REQUEST}}

Respond in Thai except the priority value.
```

## Test Requests

Submit ผ่าน Google Form ทีละรายการหลัง Make อยู่ในสถานะ `Run once`

### HIGH

```text
Requester: Demo Customer
Department: Customer Service
Request: ลูกค้ารายใหญ่ไม่สามารถชำระเงินผ่านระบบได้ และอาจยกเลิกคำสั่งซื้อหากแก้ไม่ทันวันนี้
```

Expected:

```text
Route 1 → Update a Row → Gmail
Processing Status = HIGH — HUMAN REVIEW REQUIRED
```

### MEDIUM

```text
Requester: Demo Marketing Manager
Department: Marketing
Request: ต้องการรายงานผลแคมเปญเพื่อประชุมผู้บริหารในอีกสี่วัน ขณะนี้งานการตลาดยังดำเนินต่อได้
```

Expected:

```text
Route 2 → Update a Row
Processing Status = TRIAGED
No email
```

### LOW

```text
Requester: Demo Employee
Department: HR
Request: ขอทราบขั้นตอนเปลี่ยนรูป Profile ในระบบประชุมออนไลน์ ไม่มี deadline และไม่กระทบงานปัจจุบัน
```

Expected:

```text
Route 2 → Update a Row
Processing Status = TRIAGED
No email
```

### Anti-keyword Test

```text
Requester: Demo Employee
Department: HR
Request: ด่วนมาก ASAP กรุณาส่งคู่มือการตั้งค่าธีมสีของระบบ ไม่มีลูกค้า รายได้ หรือ operations ได้รับผลกระทบ
```

Expected: `LOW` → Route 2 → Update a Row → No email

## Fallback JSON

ใช้เมื่อ Gemini API/connection ไม่พร้อม เพื่อฝึก `Parse JSON → Router → Update a Row` ต่อ

### HIGH JSON

```json
{
  "summary": "ลูกค้ารายใหญ่ไม่สามารถชำระเงินและอาจยกเลิกคำสั่งซื้อภายในวันนี้",
  "priority": "HIGH",
  "reason": "มีผลกระทบต่อลูกค้าและรายได้ทันที พร้อมข้อจำกัดด้านเวลาที่สำคัญ",
  "recommended_action": "แจ้งเจ้าของระบบชำระเงินและผู้จัดการทันที พร้อมติดตามสถานะเป็นระยะ"
}
```

### MEDIUM JSON

```json
{
  "summary": "ฝ่ายการตลาดต้องการรายงานผลแคมเปญสำหรับการประชุมในอีกสี่วัน",
  "priority": "MEDIUM",
  "reason": "เป็นงานสำคัญที่มี deadline แต่ operations ยังดำเนินต่อได้",
  "recommended_action": "มอบหมายผู้รับผิดชอบและยืนยันเวลาส่งรายงานก่อนวันประชุม"
}
```

### LOW JSON

```json
{
  "summary": "พนักงานขอวิธีเปลี่ยนรูป Profile ในระบบประชุมออนไลน์",
  "priority": "LOW",
  "reason": "เป็นคำขอข้อมูลทั่วไป ไม่มีผลกระทบทันทีและไม่มี deadline",
  "recommended_action": "ส่งลิงก์คู่มือหรือบทความช่วยเหลือมาตรฐาน"
}
```

## Expected Data Structure

ใช้ object นี้สร้าง data structure ใน `JSON — Parse JSON`:

```json
{
  "summary": "ลูกค้ารายใหญ่ไม่สามารถชำระเงินและอาจยกเลิกคำสั่งซื้อภายในวันนี้",
  "priority": "HIGH",
  "reason": "มีผลกระทบต่อลูกค้าและรายได้ทันที พร้อมข้อจำกัดด้านเวลาที่สำคัญ",
  "recommended_action": "แจ้งเจ้าของระบบชำระเงินและผู้จัดการทันที พร้อมติดตามสถานะเป็นระยะ"
}
```

ค่าที่อนุญาตสำหรับ `priority` มีเพียง:

```text
HIGH
MEDIUM
LOW
```

## HIGH Alert Email Template

ส่งถึงอีเมลของตนเองเท่านั้น

**Subject**

```text
[TEST] HIGH Priority Business Request — Human Review Required
```

**Body**

```text
นี่คือการแจ้งเตือนจาก Workshop ด้วยข้อมูลจำลอง

ผู้ร้อง: {{REQUESTER}}
หน่วยงาน: {{DEPARTMENT}}
คำร้อง: {{BUSINESS_REQUEST}}
สรุป: {{SUMMARY}}
Priority: {{PRIORITY}}
เหตุผล: {{REASON}}
การดำเนินการที่แนะนำ: {{RECOMMENDED_ACTION}}

โปรดตรวจสอบข้อเท็จจริงก่อนดำเนินการ
```

## Sheet Alert Marker Fallback

```text
HIGH — HUMAN REVIEW REQUIRED
```

## Mapping Checklist

- [ ] `Row number` มาจาก `Watch New Rows` ไม่ใช่ค่าที่พิมพ์เอง
- [ ] Form fields มาจาก `Watch New Rows`
- [ ] ผลวิเคราะห์ 4 fields มาจาก `Parse JSON`
- [ ] Route 1 filter เป็น exact `HIGH`
- [ ] Route 2 filter เป็น exact `MEDIUM OR LOW`
- [ ] ทั้ง 2 routes ใช้ `Update a Row`
- [ ] Gmail อยู่หลัง Update Row ใน Route 1 เท่านั้น

---

[← Lab 2 Guide](README.md) · [Home](../README.md) · [Next: Lab 3 Prompts →](../04-generate-management-report/prompts.md)
