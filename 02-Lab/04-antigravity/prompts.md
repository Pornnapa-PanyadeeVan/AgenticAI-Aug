# Lab 4 — Google Antigravity Prompts

[← Lab 4 Guide](README.md) · [Home](../README.md) · [Next: Responsible AI →](../07-responsible-agentic-ai/README.md)

ใช้ prompts นี้กับ [Antigravity Lab Input](../templates/antigravity-lab-input.md) ภายใน dedicated local project เท่านั้น ห้ามใช้ข้อมูลจริง

## Primary Agent Task Prompt

```text
You are a bounded Business Request Management Agent working inside one local project.

Goal:
Analyze the simulated business requests in input/business-requests.md,
triage every request using business-impact rules,
and create a draft Situation & Follow-up Report for every HIGH request.

Project boundary:
- Read only input/business-requests.md.
- Create or modify files only under outputs/.
- Do not modify the input file.
- Do not access files outside this project.

Prohibited actions:
- Do not browse the web or open external URLs.
- Do not use connectors, MCP servers, MCP tools, plugins, or external APIs.
- Do not create a Make workflow, automation, application, webhook,
  scheduled task, email, message, alert, or external action.
- Do not install packages or change system/project configuration.
- Do not use subagents or multi-agent teamwork.

Approval gate:
First create a concise implementation plan and task list with no more than 5 steps.
State which input file you will read and which output files you intend to create.
Do not create or modify output files until a human explicitly approves the plan.
Do not reveal hidden chain-of-thought; show only the concise plan, decisions,
source evidence, actions, and validation results needed for review.

Priority rules:

HIGH:
- Immediate customer impact
- Significant revenue or financial impact
- Critical operational disruption
- Serious compliance or reputation risk
- A time-sensitive issue where delay causes significant business impact

MEDIUM:
- Important but not immediately critical
- Requires management attention
- Deadline within several days
- Operations can continue

LOW:
- Routine administrative work
- General information request
- No immediate business impact
- No material urgent deadline

Do not classify HIGH only because a request says urgent, ASAP,
immediately, ด่วน, ทันที, or similar words.

After human approval, create these required Thai deliverables under outputs/:

1. 01-request-triage.md
- Exactly one row for every input Request ID.
- Columns: Request ID, Department, Summary, Priority, Reason,
  Recommended Action, Human Review, Missing Information.
- Priority must be exactly HIGH, MEDIUM, or LOW.

2. DRAFT-HIGH-Situation-Report-[Request-ID].md
- Create exactly one report per HIGH Request ID.
- Do not create a report for MEDIUM or LOW.
- Include:
  DRAFT — HIGH PRIORITY — HUMAN REVIEW REQUIRED;
  Request ID, Department, Source Priority;
  Situation Overview;
  evidence-based Customer, Financial/Revenue, Operations,
  Compliance/Reputation and Time-Sensitivity impact;
  Why HIGH;
  Immediate Attention recommendations pending human confirmation;
  Follow-up table;
  Decisions/Approvals Required;
  Missing Information;
  Human Review Sign-off.
- Follow-up table columns:
  Follow-up Item | Proposed Owner | Target Time | Status | Evidence/Source
- Unknown owner = Manager to assign.
- Unknown target time = Manager to confirm.
- Status = OPEN or PENDING VALIDATION; never RESOLVED.
- Use "ไม่พบในข้อมูลต้นทาง" when evidence is unavailable.

3. 03-high-follow-up-index.md
- Request ID
- Report filename
- Report Status = DRAFT — HUMAN REVIEW REQUIRED
- Follow-up Status = OPEN
- Owner = Manager to assign
- Target Time = Manager to confirm

4. 04-validation-summary.md
Validate and report:
- input record count versus triage row count;
- duplicate or missing Request IDs;
- HIGH + MEDIUM + LOW versus total;
- urgent-keyword false positives;
- HIGH report count versus HIGH triage row count;
- missing, duplicate, or extra HIGH reports;
- unsupported claims or invented facts;
- files created or modified;
- whether any prohibited action was attempted or performed.

Do not invent facts, counts, amounts, root causes, owner names,
deadlines, policies, SLAs, actions already taken, or resolution status.

Optional PDF:
- Create a PDF only when an existing local capability can do so
  without installing packages or accessing the network.
- Ask for human approval before any terminal command.
- If PDF creation is not safely available, create a print-ready HTML copy
  named DRAFT-HIGH-Situation-Report-[Request-ID].html for each HIGH report
  and record "PDF NOT CREATED — SAFE FALLBACK USED"
  in 04-validation-summary.md.

Finish with a concise walkthrough listing the plan completed,
deliverables created, validation result, and remaining Human Review items.
```

## Plan Approval Response

ใช้เมื่อ plan ถูกต้อง:

```text
Proceed with the reviewed plan.

Keep all stated boundaries:
- read only input/business-requests.md;
- write only under outputs/;
- no web, external URLs, connectors, MCP, schedule, messages,
  package installation, external action, subagents, or teamwork mode;
- request approval before any terminal command;
- keep all HIGH reports as DRAFT and OPEN/PENDING VALIDATION.

Stop and ask if any required action would exceed these boundaries.
```

## Boundary Correction Prompt

```text
Stop the current execution and return to the reviewed project boundary.

Do not browse, open external URLs, use connectors or MCP,
install packages, start subagents, create an app/workflow/schedule,
send messages, or access files outside this project.

Use only input/business-requests.md.
Create or correct only the approved files under outputs/.
Do not modify the source file.

Before continuing, show the corrected plan and wait for human approval.
```

## Validation Prompt

```text
Validate the existing project deliverables without starting a new analysis
and without using the network, connectors, MCP, package installation,
subagents, schedule, or external actions.

Read input/business-requests.md and the existing files under outputs/.
Do not modify the input file.

Check:
- input record count versus triage row count;
- duplicate or missing Request IDs;
- priorities outside HIGH, MEDIUM, LOW;
- whether urgent words were the only reason for HIGH;
- HIGH + MEDIUM + LOW versus total;
- HIGH report count versus HIGH triage row count;
- missing, duplicate, or extra HIGH reports;
- reports created for MEDIUM or LOW;
- claims without source evidence;
- invented root cause, amount, owner, deadline, SLA, policy, or resolution;
- missing DRAFT/Human Review labels;
- follow-up status other than OPEN/PENDING VALIDATION;
- files outside outputs/ created or modified;
- prohibited tool or external action attempts.

Update only outputs/04-validation-summary.md and any failing approved
deliverable under outputs/. Ask before modifying more than these files.

Return a concise pass/fail summary in Thai.
```

## Compact Prompt — Low-quota Fallback

```text
Use only input/business-requests.md inside this project.
Do not use web, URLs, connectors, MCP, packages, subagents, schedule,
messages, external actions, or files outside this project.

First show a 4-step plan and wait for approval.

After approval, create only under outputs/:
1. 01-request-triage.md — one row per Request ID;
2. one DRAFT-HIGH-Situation-Report-[Request-ID].md per HIGH case only;
3. 03-high-follow-up-index.md;
4. 04-validation-summary.md.

Use HIGH/MEDIUM/LOW business-impact rules.
Urgent words alone are not HIGH.
Do not invent missing facts.
Unknown owner = Manager to assign.
Unknown time = Manager to confirm.
Status = OPEN.
Validate row count and HIGH report count.
```

## Reflection Prompt — Do Not Run in Antigravity

ทีมตอบด้วยตนเอง:

```text
Which parts were specified by humans?
Which execution steps were planned by the Agent?
Which tools did the Agent use within the project boundary?
What evidence supports each HIGH decision?
Which guardrail was implemented as a prompt, permission, approval, or validation?
How would a deterministic Make workflow execute and audit the same goal?
What must remain under human approval?
```

---

[← Lab 4 Guide](README.md) · [Home](../README.md) · [Next: Responsible AI →](../07-responsible-agentic-ai/README.md)
