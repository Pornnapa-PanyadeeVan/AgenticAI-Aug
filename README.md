# AgenticAI-Aug

## จาก Generative AI สู่ Agentic AI สำหรับงานธุรกิจ

โปรเจกต์ Workshop แบบลงมือทำสำหรับเรียนรู้การออกแบบ **Business Request Management** ด้วย AI ตั้งแต่การสร้างผู้ช่วยวิเคราะห์คำร้อง การเชื่อม Workflow อัตโนมัติ การสร้างรายงานผู้บริหาร ไปจนถึงการเปรียบเทียบ Workflow ที่มนุษย์ออกแบบกับ Agent ที่วางแผนงานจาก Goal

[เริ่มเรียน: Introduction →](01-introduction/README.md) · [คำศัพท์ Agentic AI](01-introduction/glossary.md) · [ไปที่ Lab 1](02-Lab/01-build-ai-agent/README.md)

## โปรเจกต์นี้ทำอะไร

ใช้โจทย์เดียวกันตลอด Workshop: รับคำร้องทางธุรกิจ แล้วทำให้ AI สามารถสรุป ประเมินผลกระทบ จัดลำดับความสำคัญ และแนะนำสิ่งที่ควรทำต่อได้อย่างมีหลักเกณฑ์

```text
Business Request
↓
AI Analysis
↓
Summary + Priority + Reasoning + Next Action
↓
Workflow, Alert และ Request History
↓
Management Report
↓
Human Review
```

ผู้เรียนจะเห็นพัฒนาการจาก AI ที่สร้างคำตอบเพียงครั้งเดียว ไปสู่ระบบ Agentic AI ที่เชื่อมข้อมูล เครื่องมือ การตัดสินใจ Action และ Human Oversight เข้าด้วยกัน

## มีอะไรบ้าง

| Module | สิ่งที่จะทำ | เครื่องมือ | คู่มือและ Prompt |
|---|---|---|---|
| Introduction | เข้าใจ Generative AI, AI Agent, Agentic AI, Autonomy Spectrum และ Guardrail | แนวคิดและกรณีศึกษา | [คู่มือ](01-introduction/README.md) · [Glossary](01-introduction/glossary.md) |
| Lab 1 — Business Request AI Agent | สร้างผู้ช่วยที่สรุปคำร้อง จัด Priority อธิบายเหตุผล และแนะนำ Next Action | Google AI Studio | [คู่มือ](02-Lab/01-build-ai-agent/README.md) · [Prompts](02-Lab/01-build-ai-agent/prompts.md) |
| Lab 2 — Agentic Workflow | รับคำร้องจาก Form วิเคราะห์ด้วย Gemini เขียนผลกลับ Sheet และส่ง Gmail เฉพาะรายการ HIGH | Google Forms, Google Sheets, Make, Gemini, Gmail | [คู่มือ](02-Lab/02-build-agentic-workflow/README.md) · [Prompts](02-Lab/02-build-agentic-workflow/prompts.md) |
| Lab 3 — Managerial AI | ต่อยอด HIGH route จาก Lab 2 เพื่อสร้าง DRAFT situation report, ส่งออก PDF, อัปเดต tracker และรอ Human Review | Make, Gemini, Google Docs, Drive, Gmail | [คู่มือ](02-Lab/03-generate-management-report/README.md) · [Prompts](02-Lab/03-generate-management-report/prompts.md) |
| Lab 4 — Manus AI | ให้ Agent วางแผนทำ Request Triage และ Management Report แบบ end-to-end ภายในงานที่กำหนดขอบเขต | Manus | [คู่มือ](02-Lab/04-manus-ai/README.md) · [Prompts](02-Lab/04-manus-ai/prompts.md) |

## เรียนแล้วได้อะไร

เมื่อจบ Workshop ผู้เรียนจะสามารถ:

- อธิบายความแตกต่างระหว่าง Generative AI, AI Agent, Workflow และ Agentic AI ได้
- ออกแบบ Role, Goal, Business Rules, Output Format และ Guardrails สำหรับ AI Agent ได้
- สร้าง `Business Request Assistant` ที่ให้ผลลัพธ์เป็น `Summary`, `Priority`, `Reasoning` และ `Next Action`
- สร้าง Workflow ที่รับข้อมูล วิเคราะห์ ตัดสินใจแยกเส้นทาง บันทึกผล และแจ้งเตือนได้
- เปลี่ยนข้อมูลคำร้องสะสมให้เป็น Management Insight และรายงานสำหรับผู้บริหารได้
- เปรียบเทียบข้อดีและข้อจำกัดของ Human-designed Workflow กับ Goal-based Agent execution ได้
- วาง Human Review, Least Privilege และการใช้ข้อมูลจำลองไว้ในกระบวนการตั้งแต่ต้นได้

### ผลงานที่ได้จาก Workshop

1. Business Request AI Agent พร้อม Business Rules และ Test Cases
2. Workflow `Form → Sheet → Gemini → Router → Update/Alert`
3. Request History ที่มีผลวิเคราะห์และ Priority อย่างเป็นระบบ
4. Management Report พร้อมเอกสาร/PDF และขั้นตอนการจัดส่ง
5. Agent-generated Triage และ Report สำหรับใช้เปรียบเทียบกับ Workflow แบบกำหนดล่วงหน้า

## เริ่มต้นใช้งาน

1. เริ่มจาก [Introduction](01-introduction/README.md) เพื่อทำความเข้าใจภาพรวมและคำศัพท์
2. ทำ [Lab 1](02-Lab/01-build-ai-agent/README.md) เพื่อสร้าง Agent และทดสอบ Business Rules
3. ต่อด้วย [Lab 2](02-Lab/02-build-agentic-workflow/README.md) เพื่อเชื่อม Agent เข้ากับ Workflow และ Action
4. เปิด Scenario เดิมและต่อยอด HIGH route ใน [Lab 3](02-Lab/03-generate-management-report/README.md)
5. ปิดท้ายด้วย [Lab 4](02-Lab/04-manus-ai/README.md) เพื่อเปรียบเทียบวิธีทำงานแบบ Workflow กับ Agent

> แต่ละ Lab มีไฟล์ `prompts.md` สำหรับ Copy/Paste Prompt และข้อมูลทดสอบ ควรเปิดคู่กับคู่มือของ Lab นั้น

## โครงสร้างโปรเจกต์

```text
AgenticAI-Aug/
├── README.md
├── 01-introduction/
│   ├── README.md
│   └── glossary.md
└── 02-Lab/
    ├── 01-build-ai-agent/
    ├── 02-build-agentic-workflow/
    ├── 03-generate-management-report/
    └── 04-manus-ai/
```

## ข้อควรระวัง

- ใช้ข้อมูลจำลองเท่านั้น ห้ามใช้ข้อมูลลูกค้า ข้อมูลส่วนบุคคล หรือข้อมูลลับขององค์กร
- ห้ามบันทึก API key, password หรือ credential ลงใน Prompt, Google Sheet หรือ GitHub
- ใช้บัญชีและสิทธิ์เชื่อมต่อเท่าที่จำเป็นตามหลัก Least Privilege
- ตรวจผลลัพธ์ของ AI ด้วย Human Review ก่อนนำไปตัดสินใจหรือดำเนินการจริง
- ชื่อเมนู รุ่นโมเดล และข้อจำกัดของ Free plan อาจเปลี่ยนได้ ให้ยึดผลลัพธ์ของแต่ละขั้นตอนเป็นหลัก

---

พร้อมเริ่มแล้วไปที่ [Introduction →](01-introduction/README.md)
