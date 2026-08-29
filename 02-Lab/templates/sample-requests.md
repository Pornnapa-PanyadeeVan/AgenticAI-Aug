# Sample Business Requests — ข้อมูลจำลอง

[← Home](../../README.md) · [Lab 2](../02-build-agentic-workflow/README.md) · [Lab 3](../03-generate-management-report/README.md) · [Lab 4 Antigravity Input](business-requests.md)

ใช้ข้อมูลจำลองนี้สำหรับทดสอบ Lab 1–3 ห้ามแทนที่ด้วยคำร้องจริงของลูกค้าหรือพนักงาน

## วิธีใช้

- Lab 1: เลือก 3 core cases และ 2 optional cases เพื่อทดสอบ Business Rules
- Lab 2: Submit ผ่าน Google Form โดยเลือก HIGH/MEDIUM/LOW อย่างละ 1 รายการ
- Lab 3: ต่อ report/PDF modules บน HIGH route แล้ว Submit HIGH request จำลองใหม่; แนะนำข้อมูลแถว `01`
- Lab 4: Copy [business-requests.md](business-requests.md) เข้า dedicated Antigravity project; ไฟล์ตัด Expected Priority ออกเพื่อทดสอบ Agent อย่างยุติธรรม
- `AMBIGUOUS` หมายถึงข้อมูลยังไม่พอ ผู้เรียนต้องระบุ missing information ก่อนตัดสิน ไม่ใช่ Priority ที่ส่งเข้า Router

## Dataset

| ID | Requester | Department | Business Request | Context / Deadline | Expected | Rationale | Repeated Theme |
|---:|---|---|---|---|---|---|---|
| 01 | ผู้ร้องจำลอง A | Sales | ลูกค้ารายใหญ่ไม่สามารถชำระเงินผ่านระบบได้และอาจยกเลิกคำสั่งซื้อ | ต้องแก้ภายในวันนี้; มี order มูลค่าสำคัญ | HIGH | Customer + revenue + time impact | Payment failure |
| 02 | ผู้ร้องจำลอง B | Sales | ขอรายงานยอดขายแยกตามสาขาสำหรับ review ประจำสัปดาห์ | ใช้ในอีก 4 วัน; งานขายยังเดินต่อ | MEDIUM | Management attention; operations continue | Urgent report |
| 03 | ผู้ร้องจำลอง C | Sales | ด่วนมาก ขอเปลี่ยนสีใน template ใบเสนอราคา | ไม่มีลูกค้าหรือ order รออยู่ | LOW | Keyword “ด่วน” แต่ไม่มี impact | Routine request |
| 04 | ผู้ร้องจำลอง D | Sales | ลูกค้าต้องการแก้ใบเสนอราคาโดยเร็วที่สุด | ไม่ระบุ deadline, order value หรือผลกระทบ | AMBIGUOUS | ต้องถาม deadline/revenue/dependency | Quote change |
| 05 | ผู้ร้องจำลอง E | Marketing | ผู้จัดการต้องการรายงานผลแคมเปญสำหรับประชุมวันศุกร์หน้า | มีเวลา 5 วัน; campaign ทำงานต่อได้ | MEDIUM | Deadline หลายวัน; management use | Urgent report |
| 06 | ผู้ร้องจำลอง F | Marketing | มีโพสต์กล่าวหาบริษัทเรื่องความปลอดภัยและกำลังถูกแชร์อย่างรวดเร็ว | Public reputation risk กำลังขยาย | HIGH | Serious reputation impact | Customer complaint |
| 07 | ผู้ร้องจำลอง G | Marketing | ขอโลโก้ไฟล์ความละเอียดสูงสำหรับเก็บในคลังทีม | ไม่มี deadline และไม่กระทบ campaign | LOW | Routine information/artifact | Routine request |
| 08 | ผู้ร้องจำลอง H | Marketing | ด่วน ขอข้อมูล conversion ของแคมเปญล่าสุด | ไม่บอกว่าจะใช้เมื่อใดหรือ decision ใดขึ้นกับข้อมูล | AMBIGUOUS | ขาด deadline/decision impact | Urgent report |
| 09 | ผู้ร้องจำลอง I | Finance | ระบบรับชำระเงินล้มเหลวหลายช่องทาง ลูกค้าไม่สามารถจ่ายได้ | เกิดอยู่ขณะนี้; กระทบหลาย order | HIGH | Revenue + customer + operational impact | Payment failure |
| 10 | ผู้ร้องจำลอง J | Finance | ต้องการ reconciliation report เพื่อปิดงบในอีกสามวัน | มี deadline; ยังทำงานส่วนอื่นต่อได้ | MEDIUM | Financial process สำคัญแต่ไม่หยุดทันที | Urgent report |
| 11 | ผู้ร้องจำลอง K | Finance | ขอสำเนาแบบฟอร์มเบิกค่าเดินทางฉบับล่าสุด | ไม่มี deadline | LOW | Routine administrative information | Routine request |
| 12 | ผู้ร้องจำลอง L | Finance | พบยอดต่างจากที่คาด กรุณาตรวจสอบ ASAP | ไม่ระบุจำนวนเงิน สาเหตุ หรือ deadline | AMBIGUOUS | ขาด materiality และ business impact | Financial discrepancy |
| 13 | ผู้ร้องจำลอง M | HR | ระบบ payroll คำนวณเงินเดือนผิดสำหรับพนักงานจำนวนมากก่อนวันจ่าย | อาจกระทบค่าจ้างและ compliance | HIGH | Financial + employee + compliance impact | HR system issue |
| 14 | ผู้ร้องจำลอง N | HR | ต้องจัดทำ headcount report ให้ผู้บริหารในอีกสี่วัน | HR operations ยังทำต่อได้ | MEDIUM | Important management report | Urgent report |
| 15 | ผู้ร้องจำลอง O | HR | พนักงานใหม่ขอวิธีเปลี่ยนรูป Profile ในระบบประชุมออนไลน์ | ไม่มี deadline | LOW | General information | Routine HR question |
| 16 | ผู้ร้องจำลอง P | HR | พนักงานแจ้งปัญหาสิทธิ์เข้าระบบและบอกว่าด่วน | ไม่ระบุว่าจะเริ่มงานใดหรือมีใครได้รับผลกระทบ | AMBIGUOUS | ต้องถาม role/task/impact | IT access issue |
| 17 | ผู้ร้องจำลอง Q | Operations | ระบบรับคำสั่งซื้อของหนึ่งสาขาหยุดทำงาน พนักงานรับ Order ไม่ได้ | เริ่มตั้งแต่ 10:00 และไม่ทราบเวลาแก้เสร็จ | HIGH | Critical operational disruption | System outage |
| 18 | ผู้ร้องจำลอง R | Operations | ลูกค้าหลายรายร้องเรียนการส่งสินค้าล่าช้าซ้ำในสัปดาห์นี้ | ยังส่งได้แต่ SLA เริ่มเสีย | MEDIUM | Recurring customer/operational issue | Customer complaint |
| 19 | ผู้ร้องจำลอง S | Operations | ขอแก้ชื่อห้องประชุมในปฏิทินทีม | ไม่มี deadline หรือ impact | LOW | Routine administration | Routine request |
| 20 | ผู้ร้องจำลอง T | Operations | เครื่องจักรแจ้งเตือนผิดปกติและขอให้ตรวจทันที | ไม่ระบุว่าหยุดสายการผลิตหรือเป็น safety warning หรือไม่ | AMBIGUOUS | ต้องถาม safety/production impact | Operational problem |
| 21 | ผู้ร้องจำลอง U | IT | ผู้ใช้ทุกสาขาเข้า ERP ไม่ได้และไม่สามารถออกใบสั่งซื้อ | เกิดอยู่ขณะนี้; core operations หยุด | HIGH | Major multi-site disruption | IT access issue |
| 22 | ผู้ร้องจำลอง V | IT | ทีมใหม่ 8 คนต้องได้สิทธิ์ dashboard ก่อนเริ่มโครงการในสามวัน | มี deadline; workaround ยังมี | MEDIUM | Important access setup | IT access issue |
| 23 | ผู้ร้องจำลอง W | IT | ขอคู่มือ reset password สำหรับบัญชีทดสอบ | ไม่มี deadline | LOW | General information | IT access issue |
| 24 | ผู้ร้องจำลอง X | IT | เข้าโฟลเดอร์ไม่ได้ ช่วยแก้ ASAP | ไม่ระบุโฟลเดอร์ งานที่หยุด หรือจำนวนผู้ใช้ | AMBIGUOUS | ขาด scope และ operational impact | IT access issue |
| 25 | ผู้ร้องจำลอง Y | Customer Service | ลูกค้าหลายรายถูกตัดเงินแต่ระบบไม่สร้างคำสั่งซื้อ | เกิดอยู่ขณะนี้; มี financial/reputation risk | HIGH | Customer + financial + reputation impact | Payment failure |
| 26 | ผู้ร้องจำลอง Z | Customer Service | ข้อร้องเรียนส่งล่าช้าเพิ่มขึ้นและต้องสรุปสาเหตุภายในสัปดาห์ | Operations ยังเดินต่อแต่ trend ต้องแก้ | MEDIUM | Recurring issue requiring attention | Customer complaint |
| 27 | ผู้ร้องจำลอง AA | Customer Service | ลูกค้าขอทราบเวลาทำการของสาขา | ไม่มีเหตุเร่งด่วน | LOW | Routine information | Routine request |
| 28 | ผู้ร้องจำลอง AB | Customer Service | ลูกค้าบอกว่าไม่พอใจมากและต้องการคำตอบทันที | ไม่ระบุเหตุการณ์ มูลค่า หรือความเสียหาย | AMBIGUOUS | Emotion/urgent words ไม่พอ ต้องถาม facts | Customer complaint |

## Suggested Lab 2 Set

| Priority | ID | เหตุผลที่เลือก |
|---|---:|---|
| HIGH | 01 | เห็น customer/revenue/time impact |
| MEDIUM | 05 | เห็น deadline แต่ operations continue |
| LOW | 15 | เห็น routine information |
| Anti-keyword | 03 | ทดสอบว่าคำว่า “ด่วน” ไม่ทำให้ HIGH |

## Suggested Lab 3 HIGH Cases

เลือกเพียงหนึ่งรายการเพื่อสร้าง Situation & Follow-up PDF:

| แนะนำ | ID | เหตุผลที่เหมาะกับ Lab 3 |
|---|---:|---|
| Preferred | 01 | Customer + revenue + time impact ชัด และต่อจาก Suggested Lab 2 Set |
| Alternative | 06 | Reputation risk; เหมาะกับการอภิปราย evidence กับ hypothesis |
| Alternative | 09 | Payment outage หลายช่องทาง; เห็น operational + financial impact |
| Alternative | 13 | Payroll/compliance; ต้องเน้น Human Approval |
| Alternative | 17 | Operational outage; owner/target time ยังต้องยืนยัน |
| Alternative | 21 | Core ERP disruption หลายสาขา |
| Alternative | 25 | ลูกค้าถูกตัดเงินแต่ไม่มี order; high-impact follow-up ชัด |

## Discussion Questions

1. ข้อความใดเป็น source evidence และข้อความใดเป็น hypothesis?
2. ข้อมูลใดยังขาดก่อน Manager มอบหมาย owner หรือยืนยัน target time?
3. Recommendation ใดทำได้ทันที และข้อใดต้องมี approval?
4. ใครมีสิทธิ์เปลี่ยน Follow-up Status จาก OPEN เป็น RESOLVED?

---

[← Home](../../README.md) · [Lab 2](../02-build-agentic-workflow/README.md) · [Lab 3](../03-generate-management-report/README.md) · [Lab 4 Antigravity Input](business-requests.md)
