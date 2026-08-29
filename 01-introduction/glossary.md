# คำศัพท์พื้นฐาน Agentic AI สำหรับผู้เรียน MBA

[← Introduction](README.md) · [Home](../README.md) · [Next: Lab 1 →](../02-build-ai-agent/README.md)

ใช้หน้านี้เป็น pre-read หรือ reference ระหว่าง Workshop ไม่ต้องท่องจำทุกคำ ให้จำว่าองค์ประกอบทั้งหมดอยู่ใน end-to-end Agentic AI Path เดียวกัน:

```text
Business Goal
↓
AI Agent: Guidance + Context → Observe → Reason → Decide
↓
Execution: Human-designed Workflow OR Agent-planned Execution
↓
Capabilities: Local Tool OR Connector / API OR MCP
↓
Action / Artifact
↓
Validation → Human Review → Feedback → Data / Memory
                                      ↺ New Context
```

Guardrails ครอบทุกชั้น:

```text
Input Rules
+ Instructions
+ Permission Boundaries
+ Output Validation
+ Approval Gates
+ Audit Trail
+ Stop / Recovery Conditions
```

## จำ 6 คำนี้ก่อน

| คำศัพท์ | คำอธิบายสั้น | เปรียบเทียบกับการทำงานในองค์กร |
|---|---|---|
| **Agent** | ระบบ AI ที่ทำงานสู่ Goal โดยสังเกต ให้เหตุผล ตัดสินใจ และอาจใช้ Tools | ผู้รับผิดชอบงาน |
| **Skill** | วิธีทำงานหรือความสามารถที่จัดเป็นชุดและนำกลับมาใช้ซ้ำ | SOP / Playbook |
| **Tool** | ความสามารถที่ใช้ทำงานหนึ่งอย่าง | เครื่องมือบนโต๊ะทำงาน |
| **Connector** | การเชื่อมต่อและสิทธิ์ที่ทำให้ระบบหนึ่งเข้าถึงอีกระบบ | ประตูพร้อมบัตรผ่าน |
| **Workflow** | ลำดับขั้นตอนที่เชื่อม Trigger, Decision และ Action | Process map |
| **Guardrail** | ขอบเขต ตัวตรวจ การอนุมัติ และกลไกหยุดระบบ | Policy + Control + Approval gate |

> **Agent decides. Skill guides. Tool does. Connector grants access. MCP standardizes access. Workflow coordinates. Guardrail limits and checks.**

## A–Z Glossary

### Action

สิ่งที่ระบบลงมือทำแล้วเปลี่ยนสถานะของงานหรือระบบ เช่น เพิ่มแถวใน Sheet, สร้าง PDF หรือส่ง alert ต่างจาก Recommendation ซึ่งเป็นเพียงคำแนะนำ

### Agent

ระบบ AI ที่ได้รับ Goal และ Instructions แล้วใช้ Reasoning เพื่อเลือกขั้นตอน ตัดสินใจ หรือใช้ Tools ภายในขอบเขตที่กำหนด Agent ไม่จำเป็นต้องมีอิสระเต็มที่

### Agent Mode

โหมดที่ระบบวางแผนและทำ multi-step task มากกว่าการตอบข้อความหนึ่งครั้ง ชื่อและความสามารถต่างกันตามผลิตภัณฑ์ ใน Lab 4 ใช้ Manus Agent Mode เท่าที่ Free plan เปิดให้

### Agentic AI

แนวทางออกแบบระบบที่รวม Goal, Reasoning, Decision, Tools, Actions, Workflow, Data, Feedback และ Human Oversight เพื่อบรรลุผลลัพธ์ธุรกิจ ไม่ใช่ชื่อผลิตภัณฑ์

### API

Application Programming Interface (ช่องทางมาตรฐานที่ระบบใช้สื่อสารกัน) เช่น Make ส่ง request ไป Gemini API แล้วรับ JSON กลับมา

### API Key

Secret ที่ใช้ยืนยันว่าใครมีสิทธิ์เรียก API ต้องเก็บใน credential/secret field ห้ามใส่ใน GitHub, Prompt, Sheet หรือ screenshot

### Approval Gate

จุดที่ Workflow หรือ Agent ต้องหยุดรอคนอนุมัติก่อนทำ Action โดยเฉพาะงานการเงิน บุคลากร กฎหมาย compliance หรือข้อมูลอ่อนไหว

### Artifact

ชิ้นงานที่ระบบสร้างและนำไปใช้ต่อได้ เช่น Markdown report, ตาราง, PDF, slide หรือไฟล์วิเคราะห์ Artifact ยังต้องผ่าน validation และ Human Review

### Audit Trail

หลักฐานย้อนหลังว่า input คืออะไร ใช้ prompt/rule/model version ใด ตัดสินอะไร ทำ Action ใด เมื่อใด และใคร approve/override

### Autonomy

ระดับความเป็นอิสระของระบบ ตั้งแต่ AI แนะนำอย่างเดียว ไปจนถึงเลือกขั้นตอนและทำ Action หลายอย่าง Autonomy เป็น spectrum และมากกว่าไม่ได้แปลว่าดีกว่าเสมอ

### Business Rule

กฎธุรกิจที่บอกว่าระบบควรตัดสินหรือดำเนินงานอย่างไร เช่นเงื่อนไข HIGH/MEDIUM/LOW ต่างจาก Guardrail ซึ่งเน้นจำกัด ตรวจ อนุมัติ หรือหยุดระบบ กฎบางข้ออาจเป็นส่วนหนึ่งของ Guardrail ได้

### Chat Mode

โหมดสนทนาที่เน้นการตอบคำถามหรือสร้างข้อความ ไม่ควรสรุปว่าเป็น Agentic AI เพียงเพราะคำตอบซับซ้อน ต้องดูว่ามี Goal, planning, tool use, action และ validation จริงหรือไม่

### Condition

เงื่อนไขที่ตัดสินว่าเส้นทางใดควรทำงาน เช่น `Priority = HIGH` Condition อาจมาจากกฎคงที่ ไม่จำเป็นต้องใช้ AI

### Connector

ส่วนเชื่อมระหว่างแพลตฟอร์มกับระบบภายนอก พร้อมกลไก authentication และ permission เช่น Make เชื่อม Google Sheets หรือ Gmail

Connector อาจเปิดให้:

- Read data
- Create/update data
- Send content
- Receive events

Connector ไม่ได้แปลว่า Agent ควรใช้ทุก Action ที่มี ต้องจำกัดสิทธิ์แบบ Least Privilege

### Context

ข้อมูลที่ AI ใช้ประกอบการทำงาน เช่น Prompt, System Instructions, conversation history, attached dataset, policy หรือ knowledge file Context ไม่เท่ากับ Memory ถาวรเสมอไป

### Decision

การเลือกสิ่งที่จะเกิดขึ้นถัดไป เช่น จัด Priority หรือเลือกว่าจะบันทึก แจ้งเตือน หรือส่งให้ Human Review ต้องแยก Decision ออกจาก Action

### Feedback Loop

การนำผลจริงหรือการแก้ของมนุษย์กลับมาปรับ rule, prompt, process หรือ evaluation เช่น Manager เปลี่ยน MEDIUM เป็น HIGH และบันทึกเหตุผล

### Generative AI

AI ที่สร้างเนื้อหาจาก Prompt เช่น สรุปข้อความหรือร่างรายงาน โดยตัวมันเองอาจยังไม่มี Goal, Tool หรือ Action

### Goal

ผลลัพธ์ธุรกิจที่ต้องการ ไม่ใช่เพียงคำสั่งให้ “ใช้ AI” ตัวอย่าง: “ลดเวลาคัดแยกคำร้อง พร้อมรักษา Human Review สำหรับกรณีผลกระทบสูง”

### Guardrail

กลไกที่ป้องกัน จำกัด ตรวจจับ หรือหยุดพฤติกรรมที่ไม่ต้องการ Guardrail ไม่ใช่การรับประกันว่า AI จะไม่ผิด และไม่ควรพึ่ง System Instructions เพียงชั้นเดียว

ตัวอย่าง Guardrail:

- Input: ห้ามข้อมูลจริงและตรวจ required fields
- Reasoning/output: จำกัด Priority และบังคับอ้าง Request ID
- Tool: allowlist เฉพาะ Action ที่อนุญาต
- Permission: Connector อ่าน/เขียนเฉพาะไฟล์ทดสอบ
- Human: HIGH หรือ sensitive case ต้อง approve
- Monitoring: ตรวจ error, duplicate, quota และ override
- Recovery: stop condition, retry limit และ manual fallback

### Hallucination

กรณี AI สร้างข้อเท็จจริง ตัวเลข สาเหตุ หรือแหล่งอ้างอิงที่ไม่มีหลักฐาน ต้องใช้ source IDs, validation และ Human Review

### Human-in-the-loop

การให้คนมีบทบาทตรวจ แก้ อนุมัติ หรือหยุดระบบในจุดที่เหมาะสม ไม่จำเป็นต้องตรวจทุก Action แต่ต้องสอดคล้องกับความเสี่ยง

### LLM / Model

Large Language Model คือโมเดลที่ประมวลผลและสร้างภาษา เช่น Gemini ตัว Model ไม่เท่ากับ Agent; Agent ต้องเพิ่ม Goal, Instructions, Context, Tools หรือ execution logic

### Memory / Data Store

ข้อมูลที่ระบบเก็บเพื่อใช้ภายหลัง เช่น Request History ใน Google Sheets ต้องกำหนดว่าเก็บอะไร นานเท่าใด ใครเข้าถึง และลบอย่างไร

### MCP (Model Context Protocol)

มาตรฐานเปิดที่กำหนดวิธีให้ AI/LLM application เชื่อมและแลกเปลี่ยน context กับระบบภายนอกอย่างเป็นรูปแบบเดียวกัน โดยมีองค์ประกอบหลัก:

- **MCP Host:** AI application ที่ประสานการเชื่อมต่อ เช่น AI-enabled IDE หรือ chat application
- **MCP Client:** component ภายใน Host ที่สื่อสารกับ MCP Server
- **MCP Server:** program ที่เปิด context และ capabilities ให้ Client

MCP Server เปิด primitive หลักได้สามแบบ:

| Primitive | หน้าที่ |
|---|---|
| **Resources** | ข้อมูลหรือ context เช่นไฟล์และ database schema |
| **Prompts** | template หรือ instructions ที่นำกลับมาใช้ได้ |
| **Tools** | ฟังก์ชันที่ Model เรียกเพื่ออ่านข้อมูล คำนวณ หรือทำ Action |

```text
MCP Host → MCP Client → MCP Server → Resources / Prompts / Tools
```

MCP เน้นมาตรฐานการเชื่อมและแลกเปลี่ยน context ไม่ได้กำหนด Business Goal, Workflow หรือ Guardrail ให้โดยอัตโนมัติ การเชื่อม MCP Server จึงยังต้องตรวจแหล่งที่มา จำกัด permission, allowlist tools, ขอ consent/approval และเก็บ audit trail

**MCP ต่างจาก Connector:** Connector เป็นคำกว้างระดับผลิตภัณฑ์สำหรับ integration, authentication และ permission ส่วน MCP เป็น protocol เฉพาะรูปแบบหนึ่ง MCP Client อาจทำหน้าที่เป็น connector component ใน Host แต่ Connector จำนวนมากใช้ native API/OAuth โดยไม่ใช้ MCP

**MCP ต่างจาก Skill:** Skill คือวิธีทำงานหรือ playbook ส่วน MCP คือช่องทางมาตรฐานที่ใช้ค้นพบและเรียก capabilities ปัจจุบันมี `Skills over MCP` เป็น optional extension แต่ Skill ไม่จำเป็นต้องส่งผ่าน MCP เสมอไป

อ่านต่อ: [MCP Specification](https://modelcontextprotocol.io/specification/latest) และ [Architecture Overview](https://modelcontextprotocol.io/docs/learn/architecture)

### Module

หน่วยงานหนึ่งขั้นใน Make Scenario เช่น รับข้อมูล เรียก AI แปลง JSON หรือเพิ่มแถว Module อาจเป็น Trigger, Action, Search หรือ data transformation

### Orchestrator

ระบบที่ประสานลำดับงานและส่งข้อมูลระหว่างขั้น เช่น Make ใน Lab 2–3 ทำหน้าที่ควบคุม Trigger → Gemini → Router → Action

### Prompt

ข้อความที่ผู้ใช้ส่งให้ Model สำหรับงานหนึ่งครั้ง Prompt อาจมี Goal, data และคำถาม แต่ไม่ใช่ policy ถาวรเสมอไป

### Reasoning

กระบวนการใช้ข้อมูลและกฎเพื่อเลือกข้อสรุปหรือขั้นตอน ผู้เรียนควรตรวจ concise rationale และ evidence ไม่ควรขอหรือพึ่ง hidden chain-of-thought

### Router

ส่วนที่แบ่งข้อมูลไปหลายเส้นทางตาม Condition เช่น HIGH, MEDIUM และ LOW Router ไม่ได้ตัดสินเองเสมอไป แต่ใช้ค่าที่ได้จาก AI หรือกฎ

### Skill

ชุดวิธีทำงาน ความรู้ คำสั่ง หรือทรัพยากรที่ทำให้ Agent ทำงานเฉพาะด้านได้สม่ำเสมอขึ้น เช่น `Business Request Triage Skill`

Skill อาจประกอบด้วย:

- Instructions และ Business Rules
- Template หรือ Output Schema
- Reference files
- Validation checklist
- Script/Tool guidance

คำว่า Skill ไม่ใช่มาตรฐานเดียวกันทุกแพลตฟอร์ม บางระบบใช้คำว่า capability, playbook, template หรือ reusable instruction แทน ใน Workshop นี้ไม่บังคับสร้าง Manus Skill; Lab 4 ใช้ Prompt + dataset เพื่อให้เห็นแนวคิดก่อน

### System Instructions

คำสั่งระดับบนที่กำหนด Role, behavior, rules และ output expectations ของ Model/Agent มีน้ำหนักมากกว่า user prompt ในการออกแบบทั่วไป แต่ยังต้องมี validation และ guardrails ชั้นอื่น

### Tool

ความสามารถที่ Agent หรือ Workflow เรียกใช้ เช่น อ่านไฟล์ คำนวณ สร้างเอกสาร หรือเพิ่มแถวใน Sheet Tool คือ “ทำอะไรได้” ส่วน Connector คือ “เชื่อมและได้รับสิทธิ์เข้าระบบใด”

### Trigger

เหตุการณ์ที่เริ่ม Workflow เช่น form submission, webhook, row ใหม่ หรือการกด Run สำหรับทดสอบ Trigger ไม่ได้ทำให้ระบบเป็น Agentic AI ด้วยตัวเอง

### Validation

การตรวจว่า output ตรง schema, count ถูกต้อง, evidence ครบ และ Action อยู่ในขอบเขต เช่นตรวจว่า HIGH + MEDIUM + LOW เท่ากับจำนวนคำร้องทั้งหมด

### Workflow

ลำดับขั้นตอนที่ออกแบบไว้เพื่อส่งข้อมูลจาก Trigger ผ่าน Decision ไปยัง Action Workflow อาจมี AI หรือไม่มีก็ได้ จึงไม่ใช่ Agentic AI ทุก Workflow

## ตัวอย่างเดียวให้เห็นทุกคำ

กรณี Business Request Management:

| Component | ตัวอย่าง |
|---|---|
| Goal | ช่วย Manager จัดลำดับคำร้องและเห็นปัญหาซ้ำ |
| Agent | Business Request Assistant |
| Skill | Playbook สำหรับสรุป จัด Priority และตรวจผล |
| Tool | Analyze text, add row, create report |
| Connector | Gemini API, Google Sheets, Gmail connection |
| MCP | หาก AI Host ใช้ MCP Server เพื่อเปิด Resources/Prompts/Tools; Labs หลักไม่ได้ใช้ MCP |
| Workflow | Input → Gemini → JSON → Router → Sheet/Alert |
| Guardrail | ใช้ข้อมูลจำลอง, 3 Priority values, anti-urgent rule, Human Review |
| Memory | Business Request Log |
| Artifact | Weekly Management Report PDF |
| Audit Trail | Request ID, reason, route, timestamp, approver |
| Feedback | Manager override และเหตุผล |

## Connector, Skill และ Guardrail ต่างกันอย่างไร

สมมติ Agent ต้อง “แจ้ง Manager เมื่อคำร้องมีผลกระทบสูง”:

- **Skill:** บอกวิธีประเมินผลกระทบและรูปแบบ alert
- **Connector:** ให้สิทธิ์ระบบเข้าถึง Gmail หรือ Google Sheets
- **Tool/Action:** ส่ง email หรือเพิ่ม alert marker
- **Workflow:** กำหนดว่าเมื่อใดจะเรียก AI, route และทำ Action
- **Guardrail:** บังคับให้ HIGH มี evidence, ส่งถึง allowlist และหยุดรอ approval เมื่อ sensitive

หากขาด Connector ระบบอาจแนะนำได้แต่ทำ Action ภายนอกไม่ได้ หากขาด Skill ผลอาจไม่สม่ำเสมอ หากขาด Guardrail ระบบอาจทำสิ่งที่ technically possible แต่ไม่ควรทำ

## Quick Check

ลองระบุคำศัพท์:

1. `Priority = HIGH` แล้วไปเส้นทางแจ้งเตือน → **Condition + Router**
2. สิทธิ์ที่ Make ใช้เขียน Sheet → **Connector + Permission**
3. คู่มือจัด Priority ที่นำกลับมาใช้ซ้ำ → **Skill / Playbook**
4. มาตรฐานที่ Host ใช้ค้นพบ Resources/Prompts/Tools จาก Server → **MCP**
5. ห้าม HIGH จากคำว่า urgent เพียงอย่างเดียว → **Business Rule + Guardrail**
6. ผู้จัดการต้องอนุมัติก่อนคืนเงิน → **Human-in-the-loop + Approval Gate**
7. PDF ที่ Agent สร้าง → **Artifact**

---

[← Introduction](README.md) · [Home](../README.md) · [Next: Lab 1 →](../02-build-ai-agent/README.md)
