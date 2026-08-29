# Lab 4 — Manus AI Prompts

[← Lab 4 Guide](README.md) · [Home](../README.md) · [Next: Responsible AI →](../07-responsible-agentic-ai/README.md)

ใช้ prompts นี้กับ [Manus Lab Input](../templates/manus-lab-input.md) เท่านั้น ห้ามใช้ข้อมูลจริง

## Primary Agent Task Prompt

```text
You are a Business Request Management Agent.

Your goal is to analyze the attached simulated business-request dataset,
prioritize each request using business-impact rules,
and turn the request history into a concise management report.

This is a bounded analysis task.

Do NOT create a workflow, automation, Make scenario, scheduled task,
application, integration, webhook, email, message, or external action.

Do NOT browse the web or use external sources.
Use only the attached file.

First, present a concise execution plan with no more than 5 steps.
Then execute the plan.

For each request:
1. Preserve the Request ID.
2. Summarize it in one concise Thai sentence.
3. Classify priority as exactly HIGH, MEDIUM, or LOW.
4. Explain the business-impact reason briefly.
5. Recommend the next business action.
6. Set Human Review to YES when information is missing,
   the impact is high, or a sensitive decision may be involved.
7. List missing information when applicable.

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
- No urgent deadline

Do not classify HIGH only because the request contains words such as
urgent, ASAP, immediately, or as soon as possible.

Create two deliverables in Thai:

Deliverable 1: Request Triage
- A table with Request ID, Department, Summary, Priority, Reason,
  Recommended Action, Human Review, and Missing Information.
- Include exactly one row for every input record.

Deliverable 2: Weekly Management Report
- Executive Summary
- Total Requests
- Priority Distribution
- Key Issues
- Recurring Patterns
- Departments Requiring Attention
- Business Risks
- Recommended Management Actions
- Human Review Required
- Data Limitations

Validate that:
- the triage row count equals the input record count;
- HIGH + MEDIUM + LOW equals the total;
- every management claim cites supporting Request IDs;
- observed facts are separated from hypotheses;
- no external action was performed.

End with a short Validation Summary.
```

## Compact Prompt — Low-credit Fallback

ใช้เมื่อ Instructor ต้องลดความซับซ้อน ไม่รับประกันจำนวน credits ที่ใช้:

```text
Analyze only the attached simulated dataset.

Do not browse, build a workflow, create an app, schedule a task,
connect external services, or perform external actions.

Use the business-impact rules in the file context.

Produce in Thai:
1. One triage table with exactly one row per Request ID:
   ID, Department, Summary, HIGH/MEDIUM/LOW, Reason,
   Recommended Action, Human Review, Missing Information.
2. One concise management report:
   Total, Priority Distribution, Recurring Patterns,
   Departments Requiring Attention, Risks, Actions,
   Human Review, Data Limitations.

Validate row count, totals, and cite Request IDs for every pattern.
Do not treat urgent words alone as HIGH.
```

## Boundary Correction Prompt

ใช้เมื่อ Agent เสนอทำสิ่งนอกขอบเขต:

```text
Stop the proposed external or automation work.

Return to the original bounded task.

Do not create a workflow, app, integration, scheduled task,
webhook, email, message, or external action.

Use only the attached simulated dataset.

Complete only the Request Triage, Weekly Management Report,
and Validation Summary.
```

## Validation Prompt

ใช้เฉพาะเมื่อ output ขาดส่วนสำคัญและทีมยังมี credits:

```text
Validate the existing deliverables without starting a new analysis.

Check:
- input record count versus triage row count;
- duplicate or missing Request IDs;
- priorities outside HIGH, MEDIUM, LOW;
- whether urgent words were incorrectly used as the only reason for HIGH;
- HIGH + MEDIUM + LOW versus total;
- claims without supporting Request IDs;
- missing Human Review flags;
- any statement that implies an external action was performed.

Return only:
1. Validation findings
2. Corrected rows or report sections, if needed
3. Final pass/fail summary

Respond in Thai.
```

## Reflection Prompt — Do Not Run in Manus

ทีมตอบด้วยตนเองเพื่อไม่เพิ่ม credits:

```text
Which parts of the task were planned by humans?
Which parts were planned by the agent?
What evidence supports each decision?
What would make this task repeatable?
What would require a deterministic workflow?
What must remain under human approval?
```

---

[← Lab 4 Guide](README.md) · [Home](../README.md) · [Next: Responsible AI →](../07-responsible-agentic-ai/README.md)
