# 01 — Introduction: Generative AI → AI Agent → Agentic AI

[← Home](../README.md) · [Next: Lab 1 →](../02-Lab/01-build-ai-agent/README.md)

🎯 **Goal**  เข้าใจพัฒนาการจาก Generative AI ไปสู่ AI Agent และ Agentic AI รวมถึงองค์ประกอบ ระดับความเป็นอิสระ และบทบาทของมนุษย์ในระบบ

📑 **Slide Deck**  [AI at Work: From Automation to Agentic AI](01-Introduction.pdf)

📖 **Reference**  [คำศัพท์พื้นฐาน Agentic AI: Agent, Skill, Tool, Connector, MCP, Workflow และ Guardrail](glossary.md)

## Learning Flow

เนื้อหาเรียงตาม Flow ใน Slide Deck:

```text
The Complete Map of Agentic AI
↓
Generative AI
↓
AI Agent
↓
Agent + Tools | Connectors | MCP
↓
Agent Loop: Observe → Reason → Decide
↓
Agentic AI System: Observe → Reason → Decide → Act → Improve
↓
Autonomy Spectrum
↓
Learning Path → Workshop Labs
```

## 1. The Complete Map of Agentic AI

มอง Agentic AI เป็นระบบซ้อนกัน 4 ชั้น จากพื้นฐานไปสู่ระดับองค์กร:

| ชั้น | ความหมาย | ตัวอย่างองค์ประกอบ |
|---|---|---|
| **LLMs** | โมเดลภาษาขนาดใหญ่ เป็นพื้นฐานสำหรับสร้างและทำความเข้าใจภาษา | Prompt engineering, inference, embeddings, LLM APIs |
| **AI Agents** | นำ LLM มารวมกับ Goal, planning, memory, reasoning และ tools เพื่อทำงานตามเป้าหมาย | Task planning, function calling, memory, agent reasoning |
| **Agentic Systems** | หลาย Agent หรือหลายองค์ประกอบประสานงาน แบ่งบทบาท และจัดการสถานะร่วมกัน | Routing, scheduling, shared memory, agent teams |
| **Agentic Ecosystem** | ระบบระดับองค์กรที่เชื่อมภายนอก พร้อม security, governance, observability และ control | Access control, audit trail, human-in-the-loop, recovery, cost management |

```text
Agentic Ecosystem
└─ Agentic Systems
   └─ AI Agents
      └─ LLMs
```

> การมี LLM เพียงอย่างเดียวยังไม่ทำให้ระบบเป็น Agentic AI ต้องดูว่าระบบมี Goal, reasoning, execution, tools, feedback, oversight และ guardrails ครบในระดับที่โจทย์ต้องการหรือไม่

ที่มาของแผนที่แนวคิดใน Slide Deck: [The Complete Map of Agentic AI](https://www.flotorch.ai/blogs/best-agentic-ai-workflow-automation-tools-for-enterprises-in-2026)

## 2. Generative AI คืออะไร

Generative AI คือ AI สำหรับสร้างเนื้อหา รับ Prompt แล้วสร้างคำตอบ ข้อความ ภาพ หรือเนื้อหาอื่น

```text
Prompt
↓
Generate
↓
Response
```

| ขั้น | ระบบทำอะไร |
|---|---|
| Prompt | ผู้ใช้ป้อนคำสั่งหรือคำถามเพื่อบอกสิ่งที่ต้องการ |
| Generate | AI ประมวลผลและสร้างเนื้อหาตาม Prompt |
| Response | ระบบส่งผลลัพธ์กลับมาในรูปแบบที่ต้องการ |

ตัวอย่าง:

> “ช่วยสรุปข้อร้องเรียนลูกค้านี้” → ระบบตอบเป็นข้อความแล้วหยุด

เครื่องมือในกลุ่มนี้อาจสร้างข้อความ ภาพ งานค้นคว้า หรือสื่อ เช่น ChatGPT, Gemini, Claude, Microsoft Copilot, Midjourney, Perplexity, Canva Magic Studio และ NotebookLM

**จุดสำคัญ:** Generative AI เน้นการสร้าง Response แต่ยังไม่ได้หมายความว่าระบบมี Goal, ตัดสินใจ หรือทำ Action ต่อเอง

## 3. AI Agent คืออะไร

AI Agent คือตัวแทน AI ที่ทำงานสู่เป้าหมาย โดยใช้ Goal, Instructions, Context และ Reasoning เพื่อวิเคราะห์ ตัดสินใจ และเลือกสิ่งที่ควรทำต่อ

```text
Goal
↓
Observe Input
↓
Apply Instructions and Rules
↓
Reason
↓
Decide
↓
Recommend OR Use Tool
```

| ขั้น | ความหมาย |
|---|---|
| Goal | กำหนดผลลัพธ์ที่ต้องการบรรลุ |
| Observe Input | รับและทำความเข้าใจข้อมูล คำร้อง หรือสถานการณ์ |
| Apply Instructions and Rules | ใช้ Role, ข้อกำหนด และกฎธุรกิจที่กำหนดไว้ |
| Reason | วิเคราะห์ เชื่อมโยง ประเมินหลักฐานและผลกระทบ |
| Decide | เลือกข้อสรุป แนวทาง หรือขั้นตอนถัดไป |
| Recommend / Use Tool | ให้ข้อเสนอแนะ หรือเรียกเครื่องมือเพื่อทำงานต่อ |

### ประโยชน์ของ AI Agent ในทางธุรกิจ

- เพิ่มประสิทธิภาพและลดงานซ้ำ
- ประหยัดต้นทุนและทรัพยากร
- ลดความผิดพลาดและเพิ่มความสม่ำเสมอ
- ช่วยตัดสินใจได้รวดเร็วขึ้นจากข้อมูลและกฎที่กำหนด
- ให้บริการหรือประมวลผลงานได้ต่อเนื่องเมื่อมีการควบคุมที่เหมาะสม

> AI Agent ไม่ควร “ตัดสินใจแทนมนุษย์ทุกเรื่อง” โดยอัตโนมัติ ขอบเขตการตัดสินใจต้องสอดคล้องกับความเสี่ยงและ accountability

## 4. เครื่องมือและตัวอย่างการใช้งาน AI Agent

### 4.1 กลุ่มเครื่องมือสำหรับสร้าง Agent และ Workflow

| กลุ่ม | เหมาะกับอะไร | ตัวอย่างใน Slide Deck |
|---|---|---|
| No-code / Low-code Agent Builder | สร้าง Agent ผ่านหน้าจอและ configuration | Microsoft Copilot Studio, Google Vertex AI Agent Builder, Dify, Flowise |
| Workflow / Automation | เชื่อม trigger, data, AI step, routing และ action | Make, Zapier, n8n, Pipedream |
| Developer Framework / Multi-Agent | พัฒนา Agent และ orchestration ด้วยโค้ด | LangChain, LlamaIndex, CrewAI, AutoGen |

ชื่อผลิตภัณฑ์และความสามารถอาจเปลี่ยนได้ ให้เลือกเครื่องมือจากความต้องการของงาน ความเสี่ยง การเชื่อมต่อ และความสามารถในการตรวจสอบย้อนหลัง

### 4.2 ตัวอย่างการใช้งาน

| งาน | ตัวอย่าง |
|---|---|
| Customer Service | ตอบคำถาม แจ้งปัญหา และช่วยคัดกรองงานก่อนส่งต่อคน |
| Accounting & Finance | ตรวจสอบการชำระเงิน คัดกรองเอกสาร และประมวลผลค่าใช้จ่าย |
| Personalized Marketing | วิเคราะห์ข้อมูลลูกค้าและเลือกข้อเสนอที่เหมาะกับบริบท |
| Data Analytics | วิเคราะห์แนวโน้ม ประเมินความเสี่ยง และช่วยวางแผน |
| Email & Document Processing | แยกประเภท ดึงข้อมูลสำคัญ และจัดลำดับงานจากเอกสารจำนวนมาก |

### 4.3 Agent + Tools | Connectors | MCP

Agent สามารถเรียก Tool เพื่ออ่านหรือเปลี่ยนสถานะในระบบอื่นได้ เช่น:

```text
Google Sheets — เก็บ Request History
                 ↘
Google Drive — เก็บ PDF → Agent → Gmail — ส่ง Alert / Report
                 ↗
LINE OA — รับข้อความจากลูกค้า
```

| คำศัพท์ | หน้าที่ | ตัวอย่าง Workshop |
|---|---|---|
| Tool | ความสามารถเฉพาะงานที่ระบบเรียกใช้ | Parse JSON, update row, create report |
| Connector / API | ช่องทางเข้าถึงระบบภายนอก พร้อม authentication และ permission | Make เชื่อม Gemini, Google Sheets หรือ Gmail |
| MCP | Protocol ที่ Host ใช้ค้นพบ Resources, Prompts และ Tools จาก MCP Server | แนวคิดประกอบ; Labs หลักไม่ได้ติดตั้ง MCP Server |
| Workflow | ประสานลำดับ Trigger, AI step, route และ action | Make Scenario |
| Guardrail | จำกัด ตรวจ อนุมัติ หยุด และกู้คืน | Allowed values, least privilege, approval, fallback |

> ใช้ Tool เพิ่มประโยชน์ แต่ก็เพิ่มความเสี่ยง จึงต้องจำกัด permission, แยกบัญชีทดสอบ และกำหนด approval ให้เหมาะกับผลกระทบ

Connector เป็นคำกว้างสำหรับ product integration ส่วน MCP เป็น protocol เฉพาะรูปแบบหนึ่ง Connector ไม่จำเป็นต้องใช้ MCP และ MCP ไม่ได้แทน Workflow หรือ Guardrail

## 5. AI Agent ทำงานอย่างไร

AI Agent รับ Business Goal แล้วทำงานโดยอาศัย Guidance, Context และ Agent Loop:

```text
Business Goal
↓
AI Agent
├─ Guidance: Instructions + Skill + Rules
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

### Agent Loop

```text
1. Observe — รับข้อมูลและสังเกตสถานการณ์
      ↓
2. Reason — ให้เหตุผล ประเมินหลักฐานและผลกระทบ
      ↓
3. Decide — เลือกแนวทางหรือขั้นตอนถัดไป
      ↓
Recommendation OR Use Tool
      ↺
```

ใน **Lab 1** Agent จะทำถึง Decision + Recommendation ใน Google AI Studio แต่ยังไม่เชื่อมระบบภายนอก จึงไม่ต้องมี Connector หรือ MCP

## 6. Agentic AI คืออะไร

Agentic AI คือการออกแบบระบบ end-to-end ที่นำ AI Agent ไปเชื่อมกับ execution, tools, actions, data, feedback, human oversight และ guardrails เพื่อบรรลุ Goal ไม่ใช่เพียงสร้างคำตอบ

```text
Observe
↓
Reason
↓
Decide
↓
Act
↓
Improve from Feedback
↺
```

### องค์ประกอบของ Agentic AI System

| องค์ประกอบ | หน้าที่และตัวอย่างใน Workshop |
|---|---|
| Workflow / Agent Plan | ประสานลำดับ execution เช่น Make Scenario หรือ Antigravity agent plan |
| Tool | ความสามารถที่ระบบเรียกใช้ เช่น Parse JSON, `Add a row`, create report |
| Connector / API | เชื่อมระบบพร้อม authentication และ permission |
| MCP | มาตรฐานสำหรับค้นพบ Resources, Prompts และ Tools จาก Server; Labs หลักไม่ติดตั้ง MCP Server |
| Action / Artifact | เปลี่ยนสถานะจริงหรือสร้างชิ้นงาน เช่น บันทึก Sheet, alert หรือ PDF report |
| Data / Memory | เก็บข้อมูลเพื่อใช้ภายหลัง เช่น Request History |
| Feedback / Audit | ตรวจผล เรียนรู้ และตรวจย้อนหลัง เช่น Manager override และ run log |
| Guardrail | จำกัด ตรวจ อนุมัติ หยุด และกู้คืน เช่น allowed values, least privilege และ fallback |

**Guardrails ครอบทุกช่วงของระบบ** ตั้งแต่ input, instructions และ permissions ไปจนถึง output validation, approval gates, audit trail และ stop/recovery conditions

> **Agent decides. Skill guides. Tool does. Connector grants access. MCP standardizes access. Workflow coordinates. Guardrail limits and checks.**

> Workflow ที่ส่ง email ตามกฎคงที่อาจเป็น Automation แต่ยังไม่จำเป็นต้องเป็น Agentic AI และ Agent ที่ไม่มี Connector/MCP ก็ยังเป็น Agent ได้

> **Agentic AI is not a product name. It is a way of designing AI-enabled business systems.**

### ประโยชน์ของ Agentic AI

1. ลดภาระงานซ้ำซ้อน และคืนเวลาให้คนทำงานเชิงกลยุทธ์
2. ตัดสินใจและดำเนินงานได้รวดเร็วในขอบเขตที่กำหนด
3. ปรับการทำงานตามข้อมูลและ feedback โดยยังต้องมี validation และ oversight

### ตัวอย่างการใช้ในธุรกิจ

- Automated trading และการติดตามความเสี่ยง
- Warehouse, logistics และการวางแผนเส้นทาง
- Manufacturing และการตรวจจับความผิดปกติ
- Customer service และ CRM
- Programmatic advertising
- HR และ recruitment
- Retail และ e-commerce
- Software engineering

## 7. Autonomy Spectrum

Autonomy หรือระดับความเป็นอิสระควรมองเป็นสเปกตรัม ไม่ใช่สวิตช์เปิด-ปิด:

| ระดับ | ระบบทำอะไร | ตัวอย่าง Workshop | Human Role |
|---|---|---|---|
| 0: Manual | คนทำทุกขั้นตอน | อ่านและจัด Priority เอง | ตัดสินใจทั้งหมด |
| 1: Assist | AI สร้างคำแนะนำ | Lab 1 | คนตรวจและลงมือทำ |
| 2: Conditional Action | Workflow ทำ Action ที่ความเสี่ยงต่ำ | Lab 2 บันทึก Sheet | คนตรวจ HIGH |
| 3: Bounded Autonomy | ระบบเลือกและทำหลายขั้นตอนภายในขอบเขต | สร้าง/ส่ง weekly report | คนกำหนด policy และ exception |
| 4: Higher Autonomy | ระบบวางแผนและเลือก tools กว้างขึ้น | Optional agent comparison | ต้องมี guardrails และ monitoring เข้มขึ้น |

> “อัตโนมัติมากกว่า” ไม่ได้แปลว่า “ดีกว่า” เสมอไป ระดับที่เหมาะสมขึ้นกับ impact, reversibility, data sensitivity และ accountability

### Human-designed Workflow vs Goal-based Agent

| Human-designed Workflow | Goal-based Agent |
|---|---|
| คนออกแบบ Trigger, route และ action ทีละขั้น | คนกำหนด Goal แล้ว Agent วางแผนขั้นตอนมากขึ้น |
| เส้นทางคาดการณ์และ audit ง่ายกว่า | ยืดหยุ่นกับงานปลายเปิดมากกว่า |
| เปลี่ยน process ต้องแก้ workflow | Agent อาจปรับแผนตาม context |
| เหมาะกับงานซ้ำและ policy ชัด | เหมาะกับงานวิเคราะห์หลายขั้นที่มีขอบเขตและตรวจสอบได้ |

ใน Lab 2–3 ผู้เรียนจะประกอบ Workflow เอง ส่วน Lab 4 จะให้ Google Antigravity รับ Goal และ dataset เดียวกัน แล้ววางแผนสร้าง management report หนึ่งไฟล์โดยไม่สร้าง Workflow ผู้เรียนต้องสังเกต boundary, approval และ evidence ของ Agent

## 8. Learning Path: จาก Gen AI ไปสู่ Agentic AI

เส้นทางการเรียนรู้ใน Workshop พัฒนาทีละขั้น:

```text
1. Generative AI — สร้างเนื้อหา / ตอบคำถาม
↓
2. AI Agent — รับเป้าหมายและลงมือคิด
↓
3. Agent + Rules — ทำงานตามเงื่อนไขที่กำหนด
↓
4. Workflow — เชื่อมหลายขั้นตอนเข้าด้วยกัน
↓
5. Decision — ประเมินทางเลือกและเลือกแนวทาง
↓
6. Action — ลงมือทำงานหรือสั่งงานระบบ
↓
7. Data / Memory — เก็บข้อมูลและใช้ความจำประกอบการทำงาน
↓
8. Management Report — สรุปผลเพื่อผู้บริหาร
↓
9. Insight — แปลข้อมูลเป็นข้อค้นพบ
↓
10. Human Decision — มนุษย์ตัดสินใจขั้นสำคัญ
↓
11. Agentic AI — ระบบวางแผน ตัดสินใจ และทำงานร่วมกับคน
```

| ช่วงของ Learning Path | Workshop |
|---|---|
| Generative AI → AI Agent → Agent + Rules | Lab 1: Business Request Assistant |
| Workflow → Decision → Action → Data / Memory | Lab 2: Make + Gemini Workflow |
| Management Report → Insight → Human Decision | Lab 3: Managerial AI Report |
| Agent วางแผนงานภายในขอบเขต | Lab 4: Google Antigravity comparison |

## 9. Case Study: Business Request Management

ทุก Lab ใช้โจทย์เดียวกันเพื่อให้เห็นการพัฒนาของระบบอย่างต่อเนื่อง:

```text
Read → Summarize → Classify → Explain → Recommend
```

### Priority Rules

**HIGH**

- กระทบลูกค้าทันที
- กระทบรายได้หรือการเงินอย่างมีนัยสำคัญ
- ระบบงานสำคัญหยุดชะงัก
- มีความเสี่ยงด้าน compliance หรือ reputation รุนแรง
- มี deadline สั้นและหากพลาดจะเกิดผลกระทบธุรกิจสำคัญ

**MEDIUM**

- สำคัญแต่ยังไม่ critical
- ต้องการ management attention
- มี deadline ภายในหลายวัน
- Operations ยังทำต่อได้

**LOW**

- งานธุรการทั่วไปหรือคำถามข้อมูล
- ไม่มีผลกระทบทันที
- ไม่มี deadline ที่ส่งผลสำคัญต่อธุรกิจ

### Anti-keyword Rule

คำว่า “ด่วน” หรือ “ASAP” เป็นเพียงสัญญาณ ไม่ใช่หลักฐานของผลกระทบ

```text
“ขอวิธีเปลี่ยนรูป Profile ด่วนมาก”
```

ควรเป็น LOW หากไม่มี customer, financial, operational, compliance หรือ time impact ที่สำคัญ

### Operational AI → Managerial AI

> **Operational AI:** “What should we do with this request?”

> **Managerial AI:** “What are all these requests telling us about the business?”

```text
Data → Information → Insight → Decision → Action
```

| ชั้น | ตัวอย่าง |
|---|---|
| Data | คำร้องแต่ละรายการ |
| Information | Summary + Priority |
| Insight | รูปแบบซ้ำ ความเสี่ยง และหน่วยงานที่ต้องสนใจ |
| Decision Support | Management recommendation |
| Action | แก้ process, จัดสรรคน, อนุมัติ หรือ escalate |

## 💬 Discussion

1. Chatbot ที่ตอบคำถามแต่ไม่ใช้ Tools เป็น AI Agent หรือ Agentic AI หรือไม่ เพราะอะไร?
2. Workflow ที่ส่ง email ตามเวลาโดยไม่มี AI reasoning เป็น Agentic AI หรือไม่?
3. การจัด Priority ผิดอาจสร้างผลกระทบต่อใครบ้าง?
4. Action ใดควรให้ AI ทำอัตโนมัติ และ Action ใดต้องรอคนอนุมัติ?
5. ระดับ Autonomy ใดเหมาะกับข้อมูลอ่อนไหวหรือ Action ที่ย้อนกลับไม่ได้?

---

[← Home](../README.md) · [Next: Lab 1 →](../02-Lab/01-build-ai-agent/README.md)
