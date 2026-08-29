# 06 — Lab 4: Google Antigravity — Solve Lab 2 + Lab 3 without Building a Workflow — Step by Step

[← Previous: LINE OA Demo](../05-line-oa-demo/README.md) · [Home](../README.md) · [Next: Responsible AI →](../07-responsible-agentic-ai/README.md)

🎯 **Goal**  ให้ Google Antigravity รับ Goal และไฟล์คำร้องจำลอง วางแผนเอง แล้วสร้าง Request Triage กับ DRAFT Situation & Follow-up Report สำหรับทุก HIGH case โดยผู้เรียนไม่ประกอบ Make Workflow ทีละ module

⏱ **Estimated Time**  30 นาที

👥 **Team**  3–4 คน ใช้หนึ่ง local project และหนึ่ง conversation ต่อทีม

🧰 **Tool**  [Google Antigravity 2.0](https://antigravity.google/) แบบ standalone desktop; Antigravity IDE/CLI/SDK ไม่จำเป็นสำหรับ Lab นี้

ผู้เรียนไม่ต้องเขียน code เอง Core lab ใช้ conversation, project settings, plan review และ file artifacts

## วิธีใช้คู่มือนี้

แต่ละ Step บอกให้ครบว่า **คลิกที่ไหน → ตั้งค่าอะไร → ต้องเห็นอะไร → ถ่ายภาพตรงไหน** รหัส `L4-xx` เป็นตำแหน่ง screenshot ที่ผู้สอนนำภาพจริงมาใส่ภายหลังได้ ดูชื่อไฟล์ทั้งหมดที่ [Screenshot Guide](../images/README.md)

คำเรียก UI อ้างอิงจาก [Getting Started with Google Antigravity](https://codelabs.developers.google.com/getting-started-google-antigravity), [Projects](https://antigravity.google/docs/projects/) และ [Artifact Review](https://antigravity.google/docs/artifact-review) ของ Google แต่ตำแหน่งเมนูอาจต่างตามระบบปฏิบัติการและ rollout

> 📷 คู่มืออ่านและทำตามได้ก่อนมีภาพจริง ห้ามใช้ screenshot ที่เปิดเผย path ส่วนตัว, account, email หรือไฟล์งานจริง

## Antigravity ใน Lab นี้เป็น Agentic AI แบบใด

Lab นี้ใช้ **Bounded Goal-based Workspace Agent for Analysis and Artifact Creation** หรือ Agent แบบรับเป้าหมายที่ทำงานหลายขั้นภายใน project scope ที่จำกัด

```text
Human defines Goal + Rules + Project Boundary
↓
Antigravity creates Plan + Task List
↓
Human reviews and presses Proceed
↓
Agent reads local dataset → reasons → decides → writes files
↓
Agent validates deliverables and creates Walkthrough
↓
Human reviews evidence and accepts/rejects changes
```

ระดับ autonomy เป็น **ปานกลางและมีขอบเขตชัดเจน**: Agent เลือกลำดับการทำงานและใช้ local file tools เอง แต่คนกำหนด input, allowed outputs, permissions, approval gate และ acceptance criteria

## สิ่งที่ Lab นี้ทำ — และไม่ทำ

### Agent ทำภายใน project เดียว

- อ่านคำร้องจำลอง 4 รายการจากไฟล์ local
- สร้าง implementation plan และ task list
- รอ Human Review ก่อนแก้หรือสร้างไฟล์
- จัด Priority ตาม business impact
- สร้าง report เฉพาะ HIGH cases
- สร้าง follow-up index และ validation summary
- สรุปสิ่งที่ทำใน walkthrough/artifacts

### Lab นี้ไม่ทำ

- ไม่สร้าง Make Scenario, automation หรือ application
- ไม่เปิด browser, web research หรือ URL ภายนอก
- ไม่ใช้ scheduled task หรือ background automation
- ไม่เชื่อม Google Sheets, Drive, Gmail, LINE หรือ production system
- ไม่เปิด Connector หรือ MCP Server
- ไม่ติดตั้ง package และไม่ใช้ paid-only multi-agent/teamwork feature
- ไม่ส่ง email, alert, message หรือเปลี่ยนข้อมูลภายนอก
- ไม่ใช้ข้อมูลจริงหรือ confidential data

> จุดประสงค์คือเปรียบเทียบ **Human-designed deterministic Workflow** กับ **Agent-planned bounded execution** ไม่ใช่ให้ Agent แทน Workflow ในทุกสถานการณ์

## Agent, Tool, Skill, Connector, MCP และ Guardrail

| แนวคิด | ใช้อย่างไรใน Lab 4 |
|---|---|
| Agent | Antigravity รับ Goal วาง plan ตัดสิน Priority สร้างและตรวจ artifacts |
| Tool | อ่าน/เขียนไฟล์ภายใน project; ใช้ local terminal เฉพาะเมื่อผู้ใช้อนุมัติและจำเป็นต่อ PDF |
| Skill | Core lab ไม่สร้าง Skill; Prompt + rules + dataset เป็น task specification ก่อน |
| Connector | ไม่ใช้ เพราะไม่มีการเชื่อม application/account ภายนอก |
| MCP | ปิด/ไม่เพิ่ม MCP Server หรือ MCP Tool ใน project นี้ |
| Guardrail | Project scope, Review-driven approval, simulated data, output allowlist, no web/external action, validation และ Human Review |

หากองค์กรทำงานนี้ซ้ำ จึงค่อยเปลี่ยน rules/checklist ที่ผ่านการทดสอบเป็น workspace **Skill**; การทำเป็น Skill ไม่ได้อนุญาตให้เปิด Connector หรือ MCP โดยอัตโนมัติ

ดูนิยามกลางที่ [Skill](../01-introduction/glossary.md#skill), [Connector](../01-introduction/glossary.md#connector), [MCP](../01-introduction/glossary.md#mcp-model-context-protocol) และ [Guardrail](../01-introduction/glossary.md#guardrail)

## เปรียบเทียบโจทย์เดียวกัน

| Lab 2–3: Make + Gemini | Lab 4: Antigravity |
|---|---|
| ผู้เรียนกำหนด Form, Trigger, AI step, Parser, Router และ Actions | ผู้เรียนกำหนด Goal, Project Boundary, Rules, Inputs และ Deliverables |
| เส้นทางถูกออกแบบล่วงหน้าและทำซ้ำได้ | Agent สร้าง plan/task list และเลือกวิธีทำภายในขอบเขต |
| ทำ Action กับ Sheet/Drive/Gmail ตาม module ที่กำหนด | Core lab สร้างไฟล์ local เท่านั้น |
| เหมาะกับ event-driven recurring process | เหมาะกับ bounded one-off analysis และ artifact creation |
| Audit ผ่าน run history, mappings และ route | Audit ผ่าน plan, task list, file changes, source IDs, validation และ walkthrough |

## Free-plan และ Installation Guardrail

Antigravity มี individual tier ราคา $0 พร้อม basic weekly rate limits แต่ model/limits และ UI เปลี่ยนได้ ตรวจ [Pricing](https://antigravity.google/pricing), [Download](https://antigravity.google/download), [Docs](https://antigravity.google/docs/home) และ [Official Getting Started Codelab](https://codelabs.developers.google.com/getting-started-google-antigravity) ก่อนสอน

- ติดตั้ง Antigravity 2.0 ล่วงหน้า ไม่ใช้เวลาห้องเรียน download พร้อมกัน 50 คน
- ใช้หนึ่งเครื่อง/หนึ่ง project/หนึ่ง conversation ต่อทีม
- ใช้ model ที่ individual tier เปิดให้และไม่ซื้อ plan เพื่อผ่าน Workshop
- ไม่เปิด multi-agent teamwork, subagents, browser หรือ schedule
- หาก quota, installation หรือ account ไม่พร้อม ใช้ [Fallback](#fallback) ทันที

> **UI MAY VARY:** ชื่อ Security Preset, Agent Behaviour, Review Policy, Project Settings, Artifacts และ Proceed/Review controls อาจเปลี่ยน ให้เลือก function ที่จำกัด project และให้คน review ก่อน execution ตาม UI ที่เห็นจริง

## Timebox

| นาที | งาน |
|---:|---|
| 0–4 | เปรียบเทียบ Make Workflow กับ Antigravity Agent |
| 4–8 | เตรียม local project folder และ dataset |
| 8–13 | เปิด Antigravity สร้าง Project และตั้ง Guardrails |
| 13–18 | ส่ง bounded task และ review plan |
| 18–24 | Agent สร้าง artifacts ภายใน project |
| 24–28 | Validate triage, HIGH report และ files |
| 28–30 | Compare architecture และสรุป |

## ก่อนเริ่ม

- [ ] รวมทีม 3–4 คนและเลือก Operator หนึ่งคน
- [ ] ติดตั้ง Antigravity 2.0 และ Sign in เรียบร้อยก่อน Workshop
- [ ] ดาวน์โหลด/เปิด [Antigravity Lab Input](../templates/antigravity-lab-input.md)
- [ ] เปิด [Lab 4 Prompts](prompts.md)
- [ ] สร้างโฟลเดอร์ใหม่ที่ไม่มีไฟล์ธุรกิจจริง
- [ ] ยืนยันว่าจะไม่เปิด browser, schedule, MCP, Connector หรือ external action
- [ ] ปิดหน้าต่างหรือ notification ที่อาจเปิดเผยข้อมูลส่วนตัวก่อนถ่าย screenshot

## 📌 Step 1 — Frame the Business Goal

### Click / Do

1. รวมทีม 3–4 คน
2. เลือก Operator หนึ่งคนเป็นผู้ควบคุม Antigravity และกด approval
3. เลือก Reviewer หนึ่งคนอ่าน Plan และ file changes โดย Reviewer ต้องไม่เป็นคนเดียวกับ Operator ถ้าจำนวนคนพอ
4. เปิด Notes หรือกระดาษ แล้วให้ทีมเขียน Goal หนึ่งประโยคก่อนเปิด Agent:

```text
ช่วยผู้จัดการจัดลำดับคำร้องทางธุรกิจอย่างสม่ำเสมอ
และสร้างร่างรายงานสถานการณ์พร้อมรายการติดตามสำหรับทุก HIGH case
โดยใช้เฉพาะข้อมูลจำลองใน project และยังคง Human Review
```

💡 **Why This Matters**  Workflow เริ่มจาก Trigger และ route ที่คนออกแบบ ส่วน Workspace Agent เริ่มจาก Goal + context + constraints + acceptance criteria

✅ **Checkpoint**  Goal ระบุ stakeholder, outcome, project boundary และ Human Review

> 📷 **L4-01 — Goal and team roles**: ให้เห็น Goal, Operator, Reviewer และข้อห้าม external action โดยไม่เห็นชื่อจริง

## 📌 Step 2 — Prepare a Dedicated Local Project

### 2.1 Create the Folder Structure

1. เปิด Finder บน macOS หรือ File Explorer บน Windows
2. เลือกพื้นที่ local ที่ใช้สำหรับ Workshop และไม่มีไฟล์ธุรกิจจริง
3. สร้างโฟลเดอร์ใหม่ชื่อ `lab4-antigravity-business-triage`
4. เปิดโฟลเดอร์นี้ แล้วสร้างโฟลเดอร์ย่อย `input` และ `outputs`

โครงสร้างต้องเป็น:

```text
lab4-antigravity-business-triage/
├── input/
└── outputs/
```

> 📷 **L4-02 — Dedicated project folder**: ให้เห็นเฉพาะโฟลเดอร์ `input/` และ `outputs/` ภายใต้ project folder

### 2.2 Add the Simulated Dataset

1. เปิด [antigravity-lab-input.md](../templates/antigravity-lab-input.md)
2. Save a copy หรือคัดลอกเนื้อหาไปเป็นไฟล์:

```text
input/business-requests.md
```

3. เปิดไฟล์แล้วตรวจว่ามี Request ID `BR-001` ถึง `BR-004` อย่างละหนึ่งรายการ
4. ตรวจว่า `outputs/` ยังว่าง
5. อย่าวาง repository, Downloads, Desktop ทั้งหมด หรือโฟลเดอร์งานจริงเป็น project scope

> 📷 **L4-03 — Input dataset preview**: ให้เห็น path `input/business-requests.md`, BR-001 ถึง BR-004 และข้อความว่า simulated data

💡 **Why This Matters**  Project folder คือ permission boundary และ context boundary ของ Agent ไม่ใช่เพียงที่เก็บไฟล์

✅ **Checkpoint**  Project มี input file หนึ่งไฟล์ จำนวน 4 records และไม่มีข้อมูลจริง

⚠️ **Common Problem**  หากเลือกโฟลเดอร์กว้างเกินไป ให้หยุดและสร้าง dedicated folder ใหม่ก่อนเริ่ม Agent

## 📌 Step 3 — Create a Review-driven Antigravity Project

### 3.1 Create the Project

1. เปิด Google Antigravity application ที่ติดตั้งไว้ ไม่ใช้ Antigravity IDE/CLI ใน Core lab
2. Sign in ด้วยบัญชี Workshop ของทีม
3. จากหน้าแรก คลิก `Select Project`
4. เลือก `New Project`
5. ในหน้าจอ Select folder(s) คลิก `Add Folder`
6. เลือกเฉพาะโฟลเดอร์ `lab4-antigravity-business-triage`
7. ตรวจรายการ folder ต้องมีเพียงหนึ่งรายการ แล้วกด `Next`
8. ตั้งชื่อ Project `MBA Lab 4 — Business Triage`
9. กด `Create`

> 📷 **L4-04 — Select Project and New Project**: ให้เห็นจุดเริ่มสร้าง Project โดยปิด account detail

> 📷 **L4-05 — Add one project folder**: ให้เห็นว่าเลือก dedicated folder เพียงหนึ่งรายการ ไม่ใช่ Desktop หรือ Downloads

### 3.2 Configure Project Guardrails

1. เปิด Project Settings ของ `MBA Lab 4 — Business Triage`
2. ตรวจ Folder/Workspace list ว่ามีเฉพาะ dedicated folder
3. ที่ execution/conversation mode เลือก `Planning Mode` ถ้า UI แสดงตัวเลือกนี้
4. ที่ `Artifact Review Policy` หรือ `Agent Behaviour` เลือก `Request Review`
5. ที่ `Terminal Command Auto Execution` เลือก `Request Review`
6. เปิด Workspace Isolation/Strict Mode หรือ function ที่ปิด non-workspace file access หากบัญชีแสดง
7. ไม่เพิ่ม URL allowlist, browser permission, Connector, MCP Server หรือ MCP Tool
8. กด `Save` หรือปิด Settings เมื่อค่าถูกบันทึกแล้ว

| Guardrail | ค่าที่ต้องการ |
|---|---|
| Project folders | Dedicated folder 1 รายการ |
| Mode | Planning Mode |
| Artifact review | Request Review |
| Terminal commands | Request Review |
| Non-workspace access | Disabled / Strict / Isolated |
| Browser/URLs | ไม่ใช้ใน Lab |
| MCP/Connector | ไม่เพิ่มและไม่อนุญาต |

> 📷 **L4-06 — Project review and permission settings**: ให้เห็น Planning/Request Review, terminal review และ workspace isolation โดยปิด path ส่วนตัว

> Antigravity project สามารถมี settings และ permissions แยกจาก global settings ได้ ผู้เรียนต้องตรวจ project-specific settings ไม่พึ่ง default โดยไม่อ่าน

💡 **Why This Matters**  Guardrail ที่มีผลจริงต้องอยู่ทั้ง Prompt และ Tool/Permission layer

✅ **Checkpoint**  Agent เห็นเฉพาะ dedicated folder และทีมรู้ว่าจุดใดต้องกดอนุมัติ

⚠️ **Common Problem**  หาก UI ไม่มีชื่อ `Planning Mode` หรือ `Request Review` ให้เลือก preset/policy ที่ต้อง review plan, artifacts, file changes และ terminal actions มากที่สุดที่บัญชีแสดง

## 📌 Step 4 — Submit the Bounded Goal and Review the Plan

ใช้ [Primary Agent Task Prompt](prompts.md#primary-agent-task-prompt)

### 4.1 Start the Conversation

1. กลับหน้า Project `MBA Lab 4 — Business Triage`
2. กด `New conversation` หรือปุ่ม `+` ที่สร้าง conversation ใหม่
3. ตรวจชื่อ Project ที่แสดงใน conversation ต้องเป็น `MBA Lab 4 — Business Triage`
4. ตรวจ mode เป็น `Planning` ไม่ใช่ `Fast`
5. ถ้ามีตัวเลือก model ให้ใช้ model ที่ individual tier เปิดให้ ไม่ซื้อ plan เพื่อผ่าน Lab
6. ยังไม่แนบไฟล์อื่น เพราะ Agent อ่าน `input/business-requests.md` จาก project ได้

> 📷 **L4-07 — New conversation in Planning Mode**: ให้เห็น Project ที่ถูกเลือก, conversation ใหม่ และ Planning Mode

### 4.2 Submit the Task

1. เปิด [Primary Agent Task Prompt](prompts.md#primary-agent-task-prompt) อีกหน้าต่าง
2. Copy prompt ทั้ง block ตั้งแต่ `You are a bounded...` จนถึง validation requirement
3. Paste ลงช่องสนทนาใน Antigravity
4. อ่านบรรทัด boundary อีกครั้งก่อนส่ง:
   - read only `input/business-requests.md`;
   - write only `outputs/`;
   - no web, Connector, MCP, package, schedule หรือ external action;
   - show plan and wait for approval first
5. กด Send หนึ่งครั้งและรอ Plan อย่าส่ง prompt ซ้ำระหว่าง Agent กำลังคิด

> 📷 **L4-08 — Bounded task prompt**: ให้เห็น Project boundary, prohibited actions, required outputs และ approval gate โดยไม่เห็น account detail

### 📋 Prompt Preview

> ใช้ [Primary Agent Task Prompt](prompts.md#primary-agent-task-prompt) ฉบับเต็มในการทำ Lab จริง ส่วน block นี้เป็น preview สำหรับอธิบายโครงสร้างหน้าชั้นเรียน

```text
You are a bounded Business Request Management Agent working inside one local project.

Use only input/business-requests.md.
Do not browse the web, open external URLs, use MCP or connectors,
schedule tasks, send messages, install packages, or modify files outside this project.

First create a concise implementation plan and task list with no more than 5 steps.
Do not create or modify output files until a human approves the plan.

After approval, triage all requests using business impact rather than urgency words.
Create these required deliverables under outputs/:
1. 01-request-triage.md
2. one DRAFT-HIGH-Situation-Report-[Request-ID].md per HIGH case
3. 03-high-follow-up-index.md
4. 04-validation-summary.md

Do not create a HIGH report for MEDIUM or LOW cases.
Do not invent facts, amounts, root causes, owners, deadlines, policies, SLAs,
actions already taken, or resolution status.
Unknown owner = Manager to assign.
Unknown target time = Manager to confirm.
Follow-up status = OPEN or PENDING VALIDATION; never RESOLVED.

Optional: create DRAFT-HIGH-Situation-Report-[Request-ID].pdf only if an
existing local capability can do so without
installing packages. Ask for approval before any terminal command.
Otherwise create DRAFT-HIGH-Situation-Report-[Request-ID].html as a
print-ready fallback and state why PDF was not created.

End by validating file names, row counts, HIGH-report counts, evidence,
and confirming that no external action was performed.
```

เมื่อ Agent แสดง plan/task list:

### 4.3 Review the Implementation Plan

1. เปิด `Implementation Plan` จาก conversation หรือ Auxiliary/Artifacts pane
2. ยังไม่กด `Proceed`
3. ให้ Reviewer ตรวจทีละข้อ:

- input มีเพียง `input/business-requests.md`
- output ทั้งหมดอยู่ใต้ `outputs/`
- plan มีไม่เกิน 5 ขั้น
- มี triage ครบทุก Request ID
- report count ผูกกับจำนวน HIGH cases
- มี follow-up index และ validation summary
- ไม่มี app, Make Workflow, browser, schedule, MCP, Connector, external action หรือ package install
- PDF เป็น optional และต้องขออนุมัติก่อน terminal command

4. เปิด `Task List` ถ้ามี และตรวจว่า task สอดคล้องกับ Plan
5. ถ้า Plan ไม่ผ่าน ให้เปิด Plan แล้วใส่ comment หรือส่ง [Boundary Correction Prompt](prompts.md#boundary-correction-prompt)
6. กด Submit comment แล้วรอ Plan ฉบับแก้
7. กด `Proceed` เฉพาะเมื่อ checklist ผ่านทั้งหมด

> 📷 **L4-09 — Implementation Plan review**: ให้เห็น input/output boundary, required deliverables และปุ่ม Proceed โดยยังไม่เปิดเผย path ส่วนตัว

> 📷 **L4-10 — Task List before execution**: ให้เห็น task ไม่เกิน 5 ขั้นและสถานะก่อนเริ่มเขียนไฟล์

💡 **Why This Matters**  Human Approval อยู่ก่อน Tool execution ไม่ใช่ตรวจเฉพาะผลลัพธ์หลัง Agent ทำเสร็จ

✅ **Checkpoint**  Plan ผ่าน review และยังไม่พบการเปลี่ยนไฟล์ก่อน approval

⚠️ **Common Problem**  หาก Agent เริ่มเขียนไฟล์ทันที ให้กด Stop, ปรับ project review policy และเริ่มจาก plan เดิมโดยไม่เพิ่ม permission

## 📌 Step 5 — Observe Agent Execution and Artifacts

### 5.1 Approve Only In-scope Actions

หลังทีมกด Proceed ให้สังเกตเฉพาะ evidence ที่ UI แสดง ไม่ขอ hidden chain-of-thought:

- implementation plan และ task list
- ไฟล์ที่ Agent อ่าน/สร้าง
- permission request สำหรับ terminal หรือ file access
- progress/status ของ tasks
- file diffs หรือ artifact review
- validation result และ walkthrough

เมื่อมี permission dialog:

1. อ่าน command/action และ target path ทุกครั้ง
2. อนุมัติเฉพาะการอ่าน `input/business-requests.md` หรือเขียนไฟล์ที่อนุมัติไว้ใต้ `outputs/`
3. หากเป็น terminal command สำหรับ optional PDF ต้องตรวจว่าใช้ capability ที่มีอยู่แล้วและไม่ติดตั้ง package
4. Reject ทันทีหากขอ network, browser, URL, package install, schedule, MCP, Connector หรือ path นอก project
5. หลัง Reject ให้ส่ง [Boundary Correction Prompt](prompts.md#boundary-correction-prompt) ถ้า Agent ยังต้องทำงานต่อ

> 📷 **L4-11 — Permission review**: ใช้ตัวอย่าง permission ที่ปลอดภัยหรือ permission ที่ต้อง Reject โดยปิด full local path

### 5.2 Monitor Task Progress

1. เปิด Task List จาก Artifacts/Auxiliary pane
2. ดูสถานะ task จาก pending → in progress → complete
3. ตรวจ Source Files/File Changes หลัง Agent สร้างแต่ละไฟล์
4. ห้ามกด Accept all โดยไม่เปิดรายชื่อไฟล์ก่อน
5. ตรวจว่า `input/business-requests.md` ไม่มี diff
6. ตรวจว่าทุกไฟล์ใหม่อยู่ใต้ `outputs/`

ไฟล์ที่คาดหวัง:

```text
outputs/
├── 01-request-triage.md
├── DRAFT-HIGH-Situation-Report-BR-001.md
├── 03-high-follow-up-index.md
└── 04-validation-summary.md
```

อาจมี `.pdf` หรือ `.html` เพิ่มเฉพาะตามเงื่อนไข optional PDF ใน Prompt

> 📷 **L4-12 — Task progress and file changes**: ให้เห็น Task List และไฟล์ใหม่เฉพาะใต้ outputs

> 📷 **L4-13 — Output file tree**: ให้เห็นไฟล์หลัก 4 รายการและไม่มีไฟล์ HIGH report สำหรับ MEDIUM/LOW

💡 **Why This Matters**  ความเป็น Agentic อยู่ที่ Goal → Plan → Tool Use → Artifact → Validation ภายในขอบเขต ไม่ได้วัดจากข้อความที่ดูฉลาดเพียงอย่างเดียว

✅ **Checkpoint**  มีไฟล์ใน `outputs/` โดย input file ไม่ถูกแก้และไม่มี external action

## 📌 Step 6 — Validate the Deliverables

### 6.1 Open and Check Each File

1. เปิด `01-request-triage.md` จาก Source Files หรือ file list
2. นับ data rows ต้องได้ 4 และ Request ID ต้องเป็น BR-001 ถึง BR-004
3. เปิด `DRAFT-HIGH-Situation-Report-BR-001.md`
4. ตรวจ DRAFT banner, source evidence, missing information และ Human Review
5. เปิด `03-high-follow-up-index.md` แล้วคลิก/ตรวจชื่อ report file ที่อ้างถึง
6. เปิด `04-validation-summary.md` แล้วตรวจ counts, file list และ no external action statement
7. ถ้าข้อใดไม่ผ่าน ใช้ [Validation Prompt](prompts.md#validation-prompt) หรือแก้ผ่าน reviewed change เท่านั้น

> 📷 **L4-14 — Request triage results**: ให้เห็น 4 Request IDs, HIGH/MEDIUM/LOW และ BR-004 ที่ไม่ถูกยกเป็น HIGH เพราะ urgent keyword อย่างเดียว

> 📷 **L4-15 — HIGH report and follow-up index**: ให้เห็น DRAFT banner, BR-001, OPEN status, Manager to assign/confirm และ index link

### 🧪 Test A — Request Triage

- [ ] `01-request-triage.md` มี 4 rows และ Request IDs ไม่หาย/ซ้ำ
- [ ] Priority มีเพียง `HIGH`, `MEDIUM`, `LOW`
- [ ] `BR-004` ไม่เป็น HIGH เพียงเพราะมี urgent/ASAP
- [ ] Recommended Action เป็นข้อเสนอ ไม่ใช่ Action ที่อ้างว่าทำแล้ว
- [ ] Missing Information และ Human Review แสดงเมื่อเหมาะสม

### 🧪 Test B — HIGH Reports and Index

- [ ] ตาม Business Rules มี HIGH report สำหรับ `BR-001` เพียงรายการเดียว
- [ ] จำนวน HIGH reports เท่ากับจำนวน HIGH rows
- [ ] ไม่มี MEDIUM/LOW Request ID ถูกสร้างเป็น HIGH report
- [ ] Report มี DRAFT/Human Review banner และ source Request ID
- [ ] Impact claims อ้างหลักฐาน; ช่องที่ขาดใช้ `ไม่พบในข้อมูลต้นทาง`
- [ ] Unknown owner/time ใช้ `Manager to assign` / `Manager to confirm`
- [ ] Follow-up Status เป็น `OPEN` หรือ `PENDING VALIDATION` ไม่ใช่ `RESOLVED`
- [ ] `03-high-follow-up-index.md` อ้าง report file ถูกต้อง
- [ ] `04-validation-summary.md` ยืนยัน row count, report count และ no external action

### 🧪 Test C — File and Permission Boundary

- [ ] Input file ไม่ถูกแก้
- [ ] ไม่มีไฟล์นอก `outputs/` ถูกสร้างหรือแก้
- [ ] ไม่มี browser, network, Connector, MCP หรือ schedule execution
- [ ] ไม่มี package ถูกติดตั้ง
- [ ] PDF มีเฉพาะเมื่อทีมอนุมัติ local command; ไม่เช่นนั้นมี Markdown/HTML fallback

ใช้ [Validation Prompt](prompts.md#validation-prompt) เมื่อจำเป็น หรือให้ Reviewer ตรวจด้วยมือเพื่อประหยัด quota

✅ **Checkpoint**  ทีมย้อนจาก HIGH report ไปยัง source Request ID และ evidence ได้ทุก claim

### 6.2 Review the Walkthrough

1. เปิด `Walkthrough` จาก Artifacts pane หลัง Agent จบงาน
2. เทียบ deliverables ใน Walkthrough กับไฟล์จริง
3. ตรวจ validation result และ remaining Human Review items
4. ตรวจว่า Agent ไม่อ้างว่าได้ส่ง email, แก้ระบบจริง หรือ RESOLVED case แล้ว
5. เปิด File Changes/Review Changes เพื่อตรวจรายการสุดท้ายก่อน Accept
6. ถ้าไฟล์และ validation ผ่าน จึง Accept/keep changes ตาม UI
7. หากไม่ผ่าน ให้ Reject/Undo เฉพาะ changes ที่ผิด แล้วใช้ correction prompt

> 📷 **L4-16 — Validation summary and Walkthrough**: ให้เห็น PASS/FAIL counts, file list, no external action และ remaining Human Review

## 📌 Step 7 — Compare Architecture

1. วางหน้าจอ Lab 2–3 Make Flow คู่กับ Lab 4 Walkthrough
2. ให้ทีมเติมตารางจากหลักฐานที่เห็นจริง ไม่ตอบจากความรู้สึก
3. วงจุดที่ Human ออกแบบลำดับใน Make และจุดที่ Agent เสนอ Plan ใน Antigravity
4. ระบุ approval gate และ audit evidence ของแต่ละแบบ
5. เลือกว่าโจทย์ recurring, one-off หรือ hybrid เหมาะกับ architecture ใด

| Criteria | Make Workflow — Lab 2+3 | Antigravity Agent — Lab 4 |
|---|---|---|
| ใครกำหนดลำดับขั้น | Human ออกแบบ modules/routes | Agent เสนอ plan; Human review |
| Trigger | Google Form/Watch New Rows | Human starts bounded conversation |
| Tool use | Connectors/actions ที่กำหนดล่วงหน้า | Local file tools และ terminal ที่ขออนุมัติ |
| Repeatability | สูงเมื่อ schema/process คงที่ | ขึ้นกับ Goal, context, model และ review |
| External action | Sheet/Drive/Gmail ตาม workflow | ปิดใน core lab |
| Audit evidence | Run history, mappings, routes | Plan, task list, diffs, files, validation, walkthrough |
| Best fit | Recurring event-driven process | One-off multi-step analysis/artifact creation |

### 💬 Discussion

1. ถ้าต้องประมวลผลคำร้องทุก 5 นาที เหตุใด Make จึงเหมาะกว่า Antigravity conversation?
2. ส่วนใดของ Lab 4 แสดง Agentic behavior มากกว่าการใช้ Chatbot?
3. Project scope กับ Prompt prohibition ต่างกันอย่างไรในฐานะ Guardrail?
4. ถ้าเปิด MCP ให้ Agent เขียน Google Sheets ความเสี่ยงและ approval gate ต้องเพิ่มอะไร?
5. Architecture แบบ Hybrid จะให้ Make คุม Trigger/Action และให้ Antigravity ทำ bounded analysis อย่างไร?

## Fallback

### Fallback A — Instructor Completed Project

ผู้สอนเปิด project ที่ทำสำเร็จล่วงหน้า ให้ผู้เรียนตรวจ plan, task list, file changes, triage, HIGH report, follow-up index, validation และ walkthrough โดยไม่ใช้ quota ของผู้เรียน

### Fallback B — Antigravity Plan-only

หาก Agent run หรือ quota ไม่พร้อม ให้ผู้เรียนส่ง Prompt แล้วหยุดหลัง implementation plan จากนั้นตรวจว่า plan ใช้ Tools, Files, Guardrails และ approval gate ถูกต้องหรือไม่

### Fallback C — Chat Comparison

ใช้ Prompt เดียวใน Chat Mode/AI Studio และเปรียบเทียบว่าไม่มี project permission, file change review, task list หรือ walkthrough แบบเดียวกับ Workspace Agent

### Fallback D — Manual Team Simulation

ทีมแบ่งบทบาท Goal Owner, Planner, Triage Analyst, HIGH Report Analyst และ Reviewer แล้วจำลอง plan → approval → files → validation บน dataset เดียวกัน

> Fallback ต้องรักษา Learning Objective เรื่อง Goal-based planning, bounded tool use, artifacts, approval และ validation ไม่จำเป็นต้องบังคับให้ installation สำเร็จในห้อง

## 🏁 Completed

- [ ] สร้าง dedicated Antigravity project แบบ review-driven
- [ ] ใช้ dataset จำลอง 4 records
- [ ] Review plan ก่อน Agent เขียนไฟล์
- [ ] ได้ Request Triage และ HIGH report เฉพาะ `BR-001`
- [ ] ได้ Follow-up Index และ Validation Summary
- [ ] ไม่มี external action, MCP, browser, schedule หรือ package install
- [ ] อธิบายได้ว่า Antigravity ใน Lab นี้คือ bounded goal-based workspace agent
- [ ] เลือกได้ว่า use case ใดเหมาะกับ Make, Antigravity หรือ Hybrid

---

[← Previous: LINE OA Demo](../05-line-oa-demo/README.md) · [Home](../README.md) · [Next: Responsible AI →](../07-responsible-agentic-ai/README.md)
