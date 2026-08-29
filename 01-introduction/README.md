# 01 — Introduction: Generative AI → AI Agent → Agentic AI

[← Home](../README.md) · [Next: Lab 1 →](../02-build-ai-agent/README.md)

🎯 **Goal**  เข้าใจองค์ประกอบของ Agentic AI, autonomy spectrum และกรณีศึกษา Business Request Management

⏱ **Estimated Time**  20 นาที

📖 **Reference**  [คำศัพท์พื้นฐาน Agentic AI: Agent, Skill, Tool, Connector, MCP, Workflow และ Guardrail](glossary.md)

## Timebox

| นาที | เนื้อหา |
|---:|---|
| 0–4 | 1. Generative AI คืออะไร |
| 4–8 | 2. AI Agent คืออะไร |
| 8–12 | 3. Agentic AI คืออะไร + คำศัพท์ในระบบ |
| 12–15 | Autonomy Spectrum และ Make vs Manus |
| 15–18 | Business Request Management + Managerial AI |
| 18–20 | Discussion และ Checkpoint |

## 1. Generative AI คืออะไร

Generative AI (AI สำหรับสร้างเนื้อหา) รับ Prompt แล้วสร้างคำตอบ ข้อความ ภาพ หรือเนื้อหาอื่น

```text
Prompt
↓
Generate
↓
Response
```

ตัวอย่าง: “ช่วยสรุปข้อร้องเรียนลูกค้านี้” ระบบตอบเป็นข้อความแล้วหยุด

## 2. AI Agent คืออะไร

AI Agent คือระบบ AI ที่ได้รับ **Goal** แล้วใช้ Guidance และ Context เพื่อสังเกต ให้เหตุผล และตัดสินใจว่าจะทำอะไรต่อ Agent อาจจบที่ Recommendation หรือเรียก Tool เพื่อทำงานต่อก็ได้

```text
Business Goal
↓
AI Agent
├─ Guidance: Instructions + Skill + Business Rules
├─ Context: Input + Data / Memory
└─ Agent Loop: Observe → Reason → Decide
                              ↓
                    Recommend OR Use Tool
```

| องค์ประกอบของ Agent | หน้าที่ | ตัวอย่าง Lab 1 |
|---|---|---|
| Goal | กำหนดผลลัพธ์ที่ต้องการ | จัดลำดับคำร้องอย่างสม่ำเสมอ |
| Instructions | กำหนด Role, behavior และ output | Business Request Assistant |
| Skill / Playbook | วิธีทำงานที่นำกลับมาใช้ซ้ำ | Triage method + validation checklist |
| Context | ข้อมูลที่ใช้ประกอบการตัดสินใจ | Request text และ Priority rules |
| Reasoning | ประเมินหลักฐานและผลกระทบ | Customer, financial, operational impact |
| Decision | เลือกข้อสรุปหรือขั้นตอนถัดไป | `Priority = HIGH` |
| Tool (ถ้ามี) | เพิ่มความสามารถเฉพาะงาน | Calculator, parser หรือ file generator |

ใน **Lab 1** Agent จะทำถึง Decision + Recommendation ใน Google AI Studio แต่ยังไม่เชื่อมระบบภายนอก จึงไม่ต้องมี Connector หรือ MCP

## 3. Agentic AI คืออะไร

Agentic AI คือการออกแบบระบบ end-to-end ที่นำ AI Agent ไปเชื่อมกับ execution, tools, actions, data, feedback, human oversight และ guardrails เพื่อบรรลุ Business Goal ไม่ใช่เพียงสร้างคำตอบ

```text
Business Goal
↓
AI Agent: Observe → Reason → Decide
↓
Execution Coordination
├─ Human-designed Workflow
└─ Agent-planned Execution
↓
Capability Access
├─ Local Tool
├─ Tool → Connector / API → External System
└─ MCP Client → MCP Server → Resources / Prompts / Tools
↓
Action / Artifact
↓
Validation → Human Review → Feedback → Data / Memory
                                      ↺ New Context
```

| คำศัพท์ใน Agentic AI System | อยู่ตรงไหนและทำอะไร | ตัวอย่าง Workshop |
|---|---|---|
| Workflow / Agent Plan | ประสานลำดับ execution | Make Scenario หรือ Manus execution plan |
| Tool | ความสามารถที่ระบบเรียกใช้ | Parse JSON, `Add a row`, create report |
| Connector / API | เชื่อมระบบพร้อม authentication และ permission | Make เชื่อม Gemini หรือ Google Sheets |
| MCP | มาตรฐานที่ Host ใช้ค้นพบ Resources, Prompts และ Tools จาก Server | แนวคิดประกอบ; Labs หลักไม่ติดตั้ง MCP Server |
| Action / Artifact | เปลี่ยนสถานะจริงหรือสร้างชิ้นงาน | บันทึก Sheet, alert หรือ PDF report |
| Data / Memory | เก็บข้อมูลเพื่อใช้ภายหลัง | Request History |
| Feedback / Audit | ตรวจผล เรียนรู้ และตรวจย้อนหลัง | Manager override และ run log |
| Guardrail | จำกัด ตรวจ อนุมัติ หยุด และกู้คืน | Allowed values, least privilege, approval, fallback |

**Guardrails ครอบทุกช่วงของระบบ** ตั้งแต่ input, instructions และ permissions ไปจนถึง output validation, approval gates, audit trail และ stop/recovery conditions

Connector เป็นคำกว้างสำหรับ product integration ส่วน MCP เป็น protocol เฉพาะรูปแบบหนึ่ง Connector ไม่จำเป็นต้องใช้ MCP และ MCP ไม่ได้แทน Workflow หรือ Guardrail

ใน Workshop นี้:

- **Lab 2–3:** Make Workflow ประสาน Agent reasoning, native connectors, actions, data และ report
- **Lab 4:** Manus Agent วางแผน execution และสร้าง artifacts โดยไม่ประกอบ Workflow หรือเชื่อมระบบภายนอก

> **Agent decides. Skill guides. Tool does. Connector grants access. MCP standardizes access. Workflow coordinates. Guardrail limits and checks.**

> Workflow ที่ส่ง email ตามกฎคงที่อาจเป็น Automation แต่ยังไม่จำเป็นต้องเป็น Agentic AI และ Agent ที่ไม่มี Connector/MCP ก็ยังเป็น Agent ได้

> **Agentic AI is not a product name. It is a way of designing AI-enabled business systems.**

ดูนิยามและ Quick Check เพิ่มเติมใน [Glossary](glossary.md)

## 4. Autonomy Spectrum

Autonomy (ระดับความเป็นอิสระ) ควรมองเป็นสเปกตรัม:

| ระดับ | ระบบทำอะไร | ตัวอย่าง Workshop | Human Role |
|---|---|---|---|
| 0: Manual | คนทำทุกขั้นตอน | อ่านและจัด Priority เอง | ตัดสินใจทั้งหมด |
| 1: Assist | AI สร้างคำแนะนำ | Lab 1 | คนตรวจและลงมือทำ |
| 2: Conditional Action | Workflow ทำ Action ที่ความเสี่ยงต่ำ | Lab 2 บันทึก Sheet | คนตรวจ HIGH |
| 3: Bounded Autonomy | ระบบเลือกและทำหลายขั้นตอนภายในขอบเขต | สร้าง/ส่ง weekly report | คนกำหนด policy และ exception |
| 4: Higher Autonomy | ระบบวางแผนและเลือก tools กว้างขึ้น | Optional agent comparison | ต้องมี guardrails และ monitoring เข้มขึ้น |

“อัตโนมัติมากกว่า” ไม่ได้แปลว่า “ดีกว่า” เสมอไป ระดับที่เหมาะสมขึ้นกับ impact, reversibility, data sensitivity และ accountability

### Preview Lab 4 — Make Workflow vs Manus Agent

Workshop จะให้ผู้เรียนแก้โจทย์ Business Request Management สองวิธี:

| Human-designed Workflow | Goal-based Autonomous Agent |
|---|---|
| คนออกแบบ Trigger, route และ action ทีละขั้น | คนกำหนด Goal แล้ว Agent วางแผนขั้นตอนมากขึ้น |
| เส้นทางคาดการณ์และ audit ง่ายกว่า | ยืดหยุ่นกับงานปลายเปิดมากกว่า |
| เปลี่ยน process ต้องแก้ workflow | Agent อาจปรับแผนตาม context |
| เหมาะกับงานซ้ำและ policy ชัด | เหมาะกับงานสำรวจ/วางแผนที่ขอบเขตชัดและตรวจสอบได้ |

ใน Lab 2–3 ผู้เรียนจะประกอบ Workflow เอง ส่วน Lab 4 จะให้ Manus Agent รับ Goal และ dataset เดียวกันแล้ววางแผนทำ triage กับ management report โดยไม่สร้าง Workflow ผู้เรียนต้องสังเกตว่า “ความเป็นอิสระมากขึ้น” ทำให้ต้องกำหนด boundary, approval, evidence และ validation เพิ่มขึ้นอย่างไร

## 5. Business Request Management

องค์กรได้รับคำร้องจากลูกค้าหรือพนักงาน Agent ต้อง:

```text
Read → Summarize → Classify → Explain → Recommend
```

### Priority Rules

**HIGH**

- กระทบลูกค้าทันที
- กระทบรายได้/การเงินอย่างมีนัยสำคัญ
- ระบบงานสำคัญหยุดชะงัก
- ความเสี่ยง compliance หรือ reputation รุนแรง
- deadline สั้นและหากพลาดจะเกิดผลกระทบธุรกิจสำคัญ

**MEDIUM**

- สำคัญแต่ยังไม่ critical
- ต้องการ management attention
- มี deadline ภายในหลายวัน
- Operations ยังทำต่อได้

**LOW**

- Routine administration
- General information
- ไม่มีผลกระทบทันทีและไม่มี urgent deadline

### Anti-keyword Rule

คำว่า “ด่วน” หรือ “ASAP” เป็นเพียงสัญญาณ ไม่ใช่หลักฐานของผลกระทบ

```text
“ขอวิธีเปลี่ยนรูป Profile ด่วนมาก”
```

ควรเป็น LOW หากไม่มี customer, financial, operational, compliance หรือ time impact ที่สำคัญ

## 6. Operational AI กับ Managerial AI

> **Operational AI:** “What should we do with this request?”

> **Managerial AI:** “What are all these requests telling us about the business?”

เชื่อมกับ Management Information Systems (MIS):

```text
Data → Information → Insight → Decision → Action
```

| ชั้น | ตัวอย่าง |
|---|---|
| Data | คำร้องแต่ละรายการ |
| Information | Summary + Priority |
| Insight | รูปแบบซ้ำ ความเสี่ยง และหน่วยงานที่ต้องสนใจ |
| Decision Support | Management recommendation |
| Action | แก้ process, จัดสรรคน, อนุมัติหรือ escalate |

## 💬 Discussion

1. Chatbot ที่ตอบคำถามแต่ไม่ใช้ Tools เป็น Agentic AI หรือไม่?
2. Workflow ที่ส่ง email ตามเวลาโดยไม่มี AI reasoning เป็น Agentic AI หรือไม่?
3. การจัด Priority ผิดอาจสร้างผลกระทบต่อใครบ้าง?
4. Action ใดควรให้ AI ทำอัตโนมัติ และ Action ใดต้องรอคนอนุมัติ?

## ✅ Checkpoint

- [ ] อธิบาย Generative AI, Agent, Workflow และ Agentic AI ด้วยคำของตนเองได้
- [ ] แยก Agent, Skill, Tool, Connector, MCP, Workflow และ Guardrail ได้
- [ ] ยกตัวอย่าง Decision และ Action อย่างละหนึ่งตัวอย่าง
- [ ] อธิบายว่า autonomy เป็น spectrum ได้
- [ ] แยก Operational AI กับ Managerial AI ได้

## 🏁 Completed

พร้อมเปลี่ยน Prompt ธรรมดาให้เป็น Business Request Agent ใน Google AI Studio

---

[← Home](../README.md) · [Next: Lab 1 →](../02-build-ai-agent/README.md)
