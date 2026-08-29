# Antigravity Lab Input — Simulated Business Requests

ใช้สำหรับ [Lab 4: Google Antigravity](../04-antigravity/README.md) เท่านั้น โดยใช้ 4 test cases เดียวกับ Lab 2 เพื่อเปรียบเทียบ Human-designed Workflow กับ Agent-planned workspace execution อย่างตรงไปตรงมา

> ข้อมูลทั้งหมดเป็นข้อมูลจำลอง ห้ามแทนที่ด้วยข้อมูลลูกค้า พนักงาน หรือข้อมูลลับจริง

| Request ID | Requester | Department | Business Request | Context / Deadline |
|---|---|---|---|---|
| BR-001 | Demo Requester A | Sales | ลูกค้ารายใหญ่ไม่สามารถชำระเงินผ่านระบบได้และอาจยกเลิกคำสั่งซื้อ | ต้องแก้ภายในวันนี้; order มีมูลค่าสำคัญ |
| BR-002 | Demo Requester B | Marketing | ต้องการรายงานผลแคมเปญเพื่อประชุมผู้บริหาร | ใช้ในอีก 4 วัน; งานการตลาดยังดำเนินต่อได้ |
| BR-003 | Demo Requester C | HR | ขอทราบขั้นตอนเปลี่ยนรูป Profile ในระบบประชุมออนไลน์ | ไม่มี deadline และไม่กระทบงานปัจจุบัน |
| BR-004 | Demo Requester D | HR | ด่วนมาก ASAP กรุณาส่งคู่มือการตั้งค่าธีมสีของระบบ | ไม่มีลูกค้า รายได้ หรือ operations ได้รับผลกระทบ |

## Business Rules

**HIGH**

- Immediate customer impact
- Significant revenue or financial impact
- Critical operational disruption
- Serious compliance or reputation risk
- A time-sensitive issue where delay causes significant business impact

**MEDIUM**

- Important but not immediately critical
- Requires management attention
- Deadline within several days
- Operations can continue

**LOW**

- Routine administrative work
- General information request
- No immediate business impact
- No material urgent deadline

> `urgent`, `ASAP`, `immediately`, `ด่วน` หรือ `ทันที` ไม่ใช่เหตุผลเพียงพอสำหรับ HIGH ต้องพิจารณา business impact และระบุ missing information เมื่อข้อมูลไม่พอ
