# Lab 3 — HIGH Priority Situation & Follow-up Report Prompts

[← Lab 3 Guide](README.md) · [Home](../README.md) · [Next: LINE OA Demo →](../05-line-oa-demo/README.md)

## HIGH Priority Situation Report Prompt

แทน `{{HIGH_CASE_DATA}}` ด้วย HIGH row จำลองหนึ่งรายการจาก Lab 2

```text
You are a managerial incident-reporting assistant.

Create a concise Thai draft report for ONE simulated business request
that has already been classified as HIGH.

If the supplied Priority is not exactly HIGH, stop and return:
"STOP — Source Priority is not HIGH; no report created."

Use only the supplied case data. Do not invent facts, counts, monetary values,
root causes, owner names, deadlines, resolution status, policies, or SLAs.
If information is unavailable, write "ไม่พบในข้อมูลต้นทาง".

Do not approve, authorize, compensate, discipline, contact external parties,
or claim that any corrective action has already occurred.

Title:
# ร่างรายงานสถานการณ์เร่งด่วนและรายการติดตาม

Required sections:

## สถานะรายงาน
- DRAFT — HIGH PRIORITY — HUMAN REVIEW REQUIRED

## ข้อมูลอ้างอิง
- Report Generated At
- Request ID
- Department
- Source Priority

## ภาพรวมสถานการณ์
- What happened
- What is affected
- What is known now

## ผลกระทบที่มีหลักฐาน
- Customer
- Financial / Revenue
- Operations
- Compliance / Reputation
- Time Sensitivity
Mark unsupported dimensions as "ไม่พบในข้อมูลต้นทาง".

## เหตุผลที่จัดเป็น HIGH
- Explain using evidence from the source only

## สิ่งที่ต้องได้รับ Attention ทันที
- Provide proposed checks, containment, or escalation steps
- Label every item as a recommendation pending human confirmation

## รายการติดตาม
Create a table with:
Follow-up Item | Proposed Owner | Target Time | Status | Evidence / Source
Use "Manager to assign" and "Manager to confirm" when not provided.
Use OPEN or PENDING VALIDATION as status; never write RESOLVED.

## การตัดสินใจหรือการอนุมัติที่ต้องการ

## ข้อมูลที่ยังขาด

## Human Review Sign-off
- Reviewer
- Decision / Changes
- Owner Confirmed
- Target Time Confirmed
- Review Date

End with:
"รายงานนี้สร้างจากข้อมูลจำลองเพื่อการเรียนรู้ ต้องตรวจสอบข้อเท็จจริง
และได้รับการยืนยันจากผู้รับผิดชอบก่อนดำเนินการหรือเผยแพร่"

HIGH Case Data:
{{HIGH_CASE_DATA}}
```

## Correction Prompt

ใช้เมื่อ draft แต่งข้อมูลหรือแสดงสถานะเกินหลักฐาน:

```text
Revise the report using only the supplied source fields.

- Remove invented root causes, counts, amounts, owner names, deadlines,
  SLAs, policies, actions already taken, and resolution claims.
- Replace unsupported facts with "ไม่พบในข้อมูลต้นทาง".
- Label proposed actions as recommendations pending human confirmation.
- Use "Manager to assign" for unknown owners.
- Use "Manager to confirm" for unknown target times.
- Keep Follow-up Status as OPEN or PENDING VALIDATION.
- Keep the banner DRAFT — HIGH PRIORITY — HUMAN REVIEW REQUIRED.
- Preserve the original Request ID.

Return the complete corrected Thai report.
```

## Fallback HIGH Case

```text
Report Generated At: 2026-08-28 14:00 Asia/Bangkok
Request ID: BR-001
Requester: Demo Requester A
Department: Sales
Original Request: ลูกค้ารายใหญ่ไม่สามารถชำระเงินผ่านระบบได้และอาจยกเลิกคำสั่งซื้อ
AI Summary: ลูกค้ารายใหญ่ชำระเงินไม่ได้และคำสั่งซื้อสำคัญมีความเสี่ยงถูกยกเลิก
Priority: HIGH
Priority Reason: มีผลกระทบต่อลูกค้าและรายได้ทันที พร้อมข้อจำกัดด้านเวลา
Recommended Action: ตรวจสถานะ payment service แจ้ง owner ที่รับผิดชอบ และติดตามผลกับ Manager
Current Follow-up Status: OPEN
```

## Case Payload Template

```text
Report Generated At: {{TIMESTAMP}}
Request ID: {{REQUEST_ID}}
Requester: {{REQUESTER}}
Department: {{DEPARTMENT}}
Original Request: {{REQUEST}}
AI Summary: {{SUMMARY}}
Priority: {{PRIORITY}}
Priority Reason: {{REASON}}
Recommended Action: {{RECOMMENDED_ACTION}}
Current Follow-up Status: {{FOLLOW_UP_STATUS_OR_OPEN}}
```

## Email Template

**Subject**

```text
[DRAFT][HIGH][Human Review] {{REQUEST_ID}} — โปรดติดตามสถานการณ์เร่งด่วน
```

**Body**

```text
พบคำร้องจำลองที่ถูกจัดเป็น HIGH และสร้างร่างรายงานเพื่อ Human Review แล้ว

Request ID: {{REQUEST_ID}}
Department: {{DEPARTMENT}}
Situation: {{SUMMARY}}
Follow-up Status: OPEN

สิ่งที่ต้องทำต่อ:
1. ตรวจสอบข้อเท็จจริงและผลกระทบ
2. ยืนยันหรือแก้ไข Priority
3. มอบหมาย Owner
4. ยืนยัน Target Time
5. บันทึกการตัดสินใจและสถานะล่าสุด

ไฟล์แนบเป็น DRAFT และไม่ใช่การอนุมัติให้ดำเนินการ
```

## Report Quality Checklist

- [ ] ใช้ HIGH case เพียงหนึ่ง Request ID
- [ ] HIGH มี evidence ไม่ใช่ urgent keyword อย่างเดียว
- [ ] ไม่มีข้อเท็จจริง root cause, amount, owner หรือ deadline ที่แต่งขึ้น
- [ ] Unsupported fields ใช้ `ไม่พบในข้อมูลต้นทาง`
- [ ] Proposed actions รอ Human Confirmation
- [ ] Follow-up status เป็น OPEN/PENDING VALIDATION
- [ ] มี Missing Information และ Human Review Sign-off
- [ ] PDF/filename ระบุ DRAFT และ Request ID
- [ ] ไม่มีข้อมูลจริงหรือข้อมูลลับ

---

[← Lab 3 Guide](README.md) · [Home](../README.md) · [Next: LINE OA Demo →](../05-line-oa-demo/README.md)
