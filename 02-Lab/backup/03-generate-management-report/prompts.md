# Lab 3 — Management Report Prompts

[← Lab 3 Guide](README.md) · [Home](../README.md) · [Next: LINE OA Demo →](../05-line-oa-demo/README.md)

## Weekly Management Report Prompt

แทน `{{REQUEST_DATA}}` ด้วยข้อมูลจำลองที่รวมจาก Google Sheets

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

## Optional Data-quality Guardrail

เพิ่มก่อน `Business Request Data:` เมื่อต้องการความระมัดระวังมากขึ้น:

```text
Do not invent counts, departments, causes, or risks that are not supported by the data.

If the dataset is too small or incomplete, state that limitation clearly.

Separate observed patterns from hypotheses.

Do not make final financial, legal, compliance, or employee decisions.
Place those items under Human Review Required.
```

## Aggregated Data Format

```text
Record 1
Department: IT
Request: ระบบรับคำสั่งซื้อหยุดทำงานที่หนึ่งสาขา
Summary: สาขาไม่สามารถรับคำสั่งซื้อได้
Priority: HIGH
Reason: กระทบ operations และลูกค้าทันที
Recommended Action: แจ้ง IT owner และสาขา พร้อมติดตามการกู้ระบบ

Record 2
Department: Customer Service
Request: ลูกค้าหลายรายร้องเรียนว่าสินค้าส่งล่าช้า
Summary: มีข้อร้องเรียนการส่งล่าช้าซ้ำ
Priority: MEDIUM
Reason: กระทบประสบการณ์ลูกค้าแต่ยังดำเนินงานได้
Recommended Action: ตรวจ SLA และสาเหตุร่วมกับ Operations
```

## Email Template

**Subject**

```text
Weekly Business Request Report
```

**Body**

```text
รายงาน Weekly Business Request Report สร้างเรียบร้อยแล้ว

จำนวนคำร้องทั้งหมด:
{{TOTAL}}

HIGH Priority:
{{HIGH_COUNT}}

ประเด็นสำคัญ:
{{KEY_ISSUE}}

ไฟล์ PDF ฉบับเต็มแนบมากับ Email นี้

หมายเหตุ: รายงานนี้สร้างจากข้อมูลจำลองสำหรับ Workshop และต้องผ่าน Human Review
```

## Notification Template

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

## Report Quality Checklist

- [ ] ไม่สรุปทีละ request อย่างเดียว
- [ ] แยก observed pattern ออกจาก hypothesis
- [ ] Total และ Priority Distribution ตรงกับข้อมูล
- [ ] มี recurring issues และ departments requiring attention
- [ ] Recommendation ระบุ owner/time horizon เมื่อข้อมูลรองรับ
- [ ] High-impact decision อยู่ใน Human Review
- [ ] ไม่มีข้อมูลจริงหรือข้อมูลลับ

---

[← Lab 3 Guide](README.md) · [Home](../README.md) · [Next: LINE OA Demo →](../05-line-oa-demo/README.md)
