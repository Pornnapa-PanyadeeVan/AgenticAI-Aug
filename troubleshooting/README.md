# Troubleshooting Guide

[← Home](../README.md) · [Instructor Checklist](../templates/instructor-checklist.md)

ทุกหัวข้อมี `Problem → Likely Cause → Quick Fix → Instructor Fallback` เพื่อให้ Workshop เดินต่อได้ภายใน 3 ชั่วโมง

> **UI MAY VARY:** ใช้ชื่อเมนูที่เห็นจริงในบัญชีและเลือก function เทียบเท่า อย่าเปิด paid tier เพียงเพื่อแก้ปัญหาในห้อง

## Cannot access Google AI Studio

| | |
|---|---|
| **Problem** | เปิด Google AI Studio ไม่ได้, redirect loop, service unavailable หรือบัญชีไม่มีสิทธิ์ |
| **Likely Cause** | Account/age/country/admin restriction, browser cookie, network หรือ service availability |
| **Quick Fix** | ตรวจ account ที่ sign in, ใช้ browser profile/incognito ที่ได้รับอนุญาต, refresh และตรวจ network; อย่าใช้ข้อมูลจริง |
| **Instructor Fallback** | จับคู่กับผู้เรียนที่เข้าได้ หรือให้ดู Instructor screen แล้วใช้ expected outputs/prompts ใน repository |

## System Instructions not visible

| | |
|---|---|
| **Problem** | ไม่พบพื้นที่ System Instructions |
| **Likely Cause** | Panel ถูกพับ, session/mode ต่างกัน หรือ UI rollout เปลี่ยน |
| **Quick Fix** | หา run/model settings หรือ function ที่กำหนด persistent model behavior ตาม [AI Studio quickstart](https://ai.google.dev/gemini-api/docs/ai-studio-quickstart) |
| **Instructor Fallback** | Paste System Instructions ไว้ส่วนต้นของ Prompt พร้อม delimiter แล้วทำ test ใน session ใหม่ อธิบายว่าคำสั่งไม่ได้ persistent แบบเดียวกัน |

## Gemini output not in expected format

| | |
|---|---|
| **Problem** | ขาดหัวข้อ, ตอบยาว, Priority ไม่ใช่ค่าเดียว หรือภาษาไม่ตรง |
| **Likely Cause** | Instruction ไม่ครบ, chat context รบกวน หรือ model ตีความ output format ไม่ชัด |
| **Quick Fix** | ย้ำ exact format/allowed values/Thai output แล้วเริ่ม session ใหม่; ลดคำสั่งที่ขัดกัน |
| **Instructor Fallback** | ใช้ expected output ตัวอย่างและให้ผู้เรียนตรวจว่าแต่ละ field มาจาก rule ใด |

## Cannot create API key

| | |
|---|---|
| **Problem** | ไม่มีตัวเลือกสร้าง key, permission denied หรือหน้าจอขอ billing |
| **Likely Cause** | Account/admin/country/project restriction หรือ free-tier eligibility ต่างกัน |
| **Quick Fix** | ตรวจบัญชีและหน้าจัดการ key; ใช้ตัวเลือก free ที่บัญชีมี; ไม่เปิด billing เพื่อ Workshop |
| **Instructor Fallback** | Lab 1 ต่อได้โดยไม่มี key; Lab 2 ใช้ [fallback JSON](../03-build-agentic-workflow/prompts.md#fallback-json) หรือ Instructor scenario โดยไม่แชร์ key |

## Gemini API quota issue

| | |
|---|---|
| **Problem** | Error `429`, quota exceeded, rate limit หรือ model unavailable |
| **Likely Cause** | 50 คน run พร้อมกัน, free-tier RPM/TPM/daily limit, preview model limit หรือ request ใหญ่เกิน |
| **Quick Fix** | หยุด 1–2 นาที, stagger team runs, ลด dataset/output, ใช้ model ฟรีที่ available และไม่ retry รัว |
| **Instructor Fallback** | ใช้ Google AI Studio manual output หรือ prepared JSON/report แล้วทำ Router/Action ต่อ |

## Make cannot connect to Gemini

| | |
|---|---|
| **Problem** | Connection rejected, authentication error หรือ Gemini action run ไม่ผ่าน |
| **Likely Cause** | Key ผิด/หมดอายุ/ถูก block, model unavailable, quota หรือ connection configuration |
| **Quick Fix** | สร้าง connection ใหม่ด้วย key ของตนเอง ตรวจ key/model/quota และดู error detail โดยไม่แชร์ secret |
| **Instructor Fallback** | ตัด AI step ชั่วคราวแล้วป้อน fallback JSON เข้า parsing/Router เพื่อรักษา Learning Objective |

## Make cannot connect to Google Sheets

| | |
|---|---|
| **Problem** | OAuth fail, ไม่เห็น Spreadsheet/Sheet หรือ permission denied |
| **Likely Cause** | Sign in ผิด account, admin blocks OAuth, file ownership/permission หรือ stale connection |
| **Quick Fix** | ตรวจ Google account, เปิด Sheet โดยตรง, reconnect และเลือก file ของตนเอง |
| **Instructor Fallback** | แสดง mapping บน Scenario แล้ว paste output ลง prepared Sheet ด้วยตนเอง |

## Google Form response is not detected

| | |
|---|---|
| **Problem** | Submit Form แล้วไม่มี response row หรือ `Watch New Rows` ไม่ได้รับ bundle |
| **Likely Cause** | Form ยังไม่ได้ link Sheet, เลือก Spreadsheet/tab ผิด, Submit ก่อน `Run once` หรือ starting point ข้ามแถว |
| **Quick Fix** | Link response destination ให้ถูก เลือก `Form Responses 1`, ตั้ง start เป็น `From now on`, กด `Run once` แล้ว Submit ข้อมูลจำลองใหม่ 1 รายการ |
| **Instructor Fallback** | ใช้ prepared response sheet/bundle ที่มี `Row number`, Form fields และข้อมูลจำลอง |

## Router condition does not match

| | |
|---|---|
| **Problem** | Bundle ไม่เข้า HIGH หรือ MEDIUM/LOW route |
| **Likely Cause** | Mapping ผิด field, lowercase, whitespace หรือ filter ใช้ค่าที่ไม่ตรง |
| **Quick Fix** | ดู parsed `priority`, trim/normalize และใช้ exact match กับ `HIGH`, `MEDIUM`, `LOW` |
| **Instructor Fallback** | ใช้ prepared JSON ที่ priority สะอาด แล้วสาธิตทีละ route |

## Priority contains extra text

| | |
|---|---|
| **Problem** | ค่าเป็น `Priority: HIGH`, `HIGH because...` หรือมี code fence |
| **Likely Cause** | Prompt ไม่บังคับ schema หรือ map จาก full response แทน parsed field |
| **Quick Fix** | ใช้ JSON prompt, ย้ำ allowed values และ map `priority` หลัง parse ไม่ใช้ full text |
| **Instructor Fallback** | แก้ค่าใน fallback JSON เพื่อสาธิต Router และอภิปรายว่าทำไม structured output สำคัญ |

## JSON cannot parse

| | |
|---|---|
| **Problem** | JSON parser error หรือไม่มี 4 fields |
| **Likely Cause** | Markdown fence, single quotes, trailing comma, ข้อความก่อน/หลัง JSON หรือ output ถูกตัด |
| **Quick Fix** | ตรวจ raw output, ย้ำ `Return ONLY valid JSON`, ลด verbosity และ run ใหม่หนึ่งครั้ง |
| **Instructor Fallback** | ใช้ [valid fallback JSON](../03-build-agentic-workflow/prompts.md#fallback-json) แล้วทำขั้นตอนถัดไป |

## Update a Row writes the wrong row or creates a duplicate

| | |
|---|---|
| **Problem** | AI result ไปผิด row, response เดิมถูกล้าง หรือจำนวน rows เพิ่มเป็นสองเท่า |
| **Likely Cause** | ใช้ `Add a Row`, พิมพ์ row number เอง, map row number ผิด module หรือไม่ map Form fields เดิมกลับไป |
| **Quick Fix** | ใช้ `Update a Row`; map `Row number` และ Form fields จาก `Watch New Rows`; map ผล AI จาก `Parse JSON` แล้วทดสอบ 1 response |
| **Instructor Fallback** | อัปเดต prepared row ด้วยมือและตรวจ mapping table ใน Lab 2 |

## Scenario runs but Sheet fields are missing

| | |
|---|---|
| **Problem** | Scenario ผ่านแต่ไม่มี row หรือ row อยู่ผิด Sheet |
| **Likely Cause** | Action ไม่ได้ run, route ไม่ match, เลือก Spreadsheet/Sheet ผิด, header changed หรือ permission |
| **Quick Fix** | เปิด run history ตาม bundle, ตรวจ selected file/tab และ refresh column mapping |
| **Instructor Fallback** | อัปเดต prepared row ด้วยตนเองและให้ผู้เรียนวาด mapping Form/AI fields → 13 Sheet columns |

## Lab 3 cannot find or update the HIGH row

| | |
|---|---|
| **Problem** | สร้าง PDF ได้แต่ Report Link/Follow-up Status ไม่อัปเดตใน row เดิม |
| **Likely Cause** | Request ID ว่าง/ซ้ำ, ค้นหาผิด Sheet, เลือก `Search Rows (Advanced)` ซึ่งไม่คืน row number, ใช้ add-row หรือ row number mapping หาย |
| **Quick Fix** | ใช้ `Search Rows` แบบมาตรฐาน, filter exact Request ID + Priority = HIGH, Limit 1; ตรวจ output ว่ามี `Row number` แล้ว map ไป `Update a Row` พร้อม Report Status/Link/Follow-up |
| **Instructor Fallback** | อัปเดตสาม fields ด้วยตนเองเป็น `DRAFT — HUMAN REVIEW REQUIRED`, filename/link และ `OPEN`; ห้ามสร้าง duplicate row |

## Google Drive text file does not become a Google Document

| | |
|---|---|
| **Problem** | `Create a File from Text` สร้าง `.txt`, ไม่ได้ Document ID หรือเปิดเป็น Google Docs ไม่ได้ |
| **Likely Cause** | ไม่ได้เปิด Convert to Google Docs, เลือก folder/account ผิด หรือ module UI ของบัญชีต่างกัน |
| **Quick Fix** | เปิด `Convert to Google Docs = Yes`, ตรวจ My Drive/folder และ Run module เดียว; ถ้าไม่มีตัวเลือกให้ใช้ Google Docs create action ที่ทำหน้าที่เทียบเท่า |
| **Instructor Fallback** | Copy draft ไป Google Docs ด้วยตนเอง แล้วทำ validation/export PDF ต่อ |

## Gmail connection unavailable

| | |
|---|---|
| **Problem** | OAuth denied, send action unavailable หรือ policy block |
| **Likely Cause** | Google Workspace admin policy, account type, connection scope หรือ Make plan/UI difference |
| **Quick Fix** | ใช้บัญชีของตนเองที่อนุญาต ส่งถึงตนเอง และ reconnect โดยอ่าน permission ก่อนยอมรับ |
| **Instructor Fallback** | Lab 2 ใช้ `Processing Status = HIGH — HUMAN REVIEW REQUIRED`; Lab 3 เก็บ PDF/Drive link และสร้าง email draft text |

## PDF cannot generate

| | |
|---|---|
| **Problem** | ได้ text/link แทน PDF, file 0 bytes หรือเปิดไม่ได้ |
| **Likely Cause** | ยังไม่ได้ export binary, document ID ผิด, conversion action/format ไม่รองรับ |
| **Quick Fix** | ตรวจ Document ID ก่อน แล้วใช้ Drive `Download a File` พร้อม PDF conversion หรือ Docs `Download a Document`; ตรวจ output ว่ามี binary data ก่อน map ไป Upload a File |
| **Instructor Fallback** | Copy report ไป Google Docs แล้ว download/export PDF ด้วยตนเองตาม UI ปัจจุบัน |

## Google Drive permission issue

| | |
|---|---|
| **Problem** | หา folder ไม่พบ, upload denied หรือ link เปิดไม่ได้ |
| **Likely Cause** | ผิด account/Drive, folder ownership, insufficient scope หรือ shared-drive restriction |
| **Quick Fix** | ใช้ My Drive ของตนเอง สร้าง `Agentic-AI-Reports/HIGH-Follow-up` และ reconnect |
| **Instructor Fallback** | เก็บ PDF local ชั่วคราวและบันทึก intended Drive path ใน worksheet; ไม่เปิด public sharing |

## HIGH report invents facts or says RESOLVED

| | |
|---|---|
| **Problem** | Report แต่ง root cause/owner/deadline หรือใช้สถานะ RESOLVED ทั้งที่ source ไม่ยืนยัน |
| **Likely Cause** | Source fields ไม่ครบ, Prompt ไม่บังคับ evidence หรือ AI เติมช่องว่างให้ดูสมบูรณ์ |
| **Quick Fix** | ใช้ [Correction Prompt](../04-generate-management-report/prompts.md#correction-prompt), แทนข้อมูลที่ขาดด้วย `ไม่พบในข้อมูลต้นทาง` และคง `OPEN` |
| **Instructor Fallback** | ใช้ [Fallback HIGH Case](../04-generate-management-report/prompts.md#fallback-high-case), ตรวจด้วย checklist และสร้าง DRAFT PDF ด้วยมือ |

## Workflow does not run

| | |
|---|---|
| **Problem** | Run once รออยู่, trigger ไม่เข้าหรือ Scenario หยุดกลางทาง |
| **Likely Cause** | Trigger ไม่ได้รับ event, schedule off, invalid connection, unmapped required field หรือ previous error |
| **Quick Fix** | เริ่มจาก trigger test ใหม่ ส่ง payload หลัง Scenario รอฟัง ตรวจ required fields และ run history จากซ้ายไปขวา |
| **Instructor Fallback** | เดิน architecture ด้วย prepared bundles ทีละขั้น: Input → JSON → Router → Sheet |

## Duplicate rows or alerts

| | |
|---|---|
| **Problem** | คำร้องเดียวเกิดหลาย row/email |
| **Likely Cause** | กด Run ซ้ำ, webhook redelivery, overlapping routes หรือ retry หลัง timeout |
| **Quick Fix** | ใช้ request/event ID, exact mutually exclusive filters และตรวจผลก่อน retry |
| **Instructor Fallback** | ลบ duplicate ในข้อมูลจำลอง แล้วอภิปราย idempotency และ audit trail |

## API key may have leaked

| | |
|---|---|
| **Problem** | Key ปรากฏใน screenshot, chat, Sheet, run input หรือ Git commit |
| **Likely Cause** | Paste ผิดที่หรือ connection ไม่เก็บเป็น secret |
| **Quick Fix** | หยุดใช้และ revoke/rotate key ทันที จากนั้นลบข้อมูลที่เปิดเผยตาม policy; อย่าคิดว่าการลบข้อความอย่างเดียวทำให้ key ปลอดภัย |
| **Instructor Fallback** | ใช้ prepared output ต่อ ห้ามแจก key ใหม่แบบ shared key |

## Cannot install, open, or sign in to Antigravity

| | |
|---|---|
| **Problem** | App เปิดไม่ได้, OS ไม่รองรับ, Sign in ไม่ผ่าน หรือไม่มีสิทธิ์ใช้ Agent |
| **Likely Cause** | ยังไม่ติดตั้งล่วงหน้า, OS requirement, account/admin/region restriction หรือ rollout/version ต่างกัน |
| **Quick Fix** | ตรวจ [Download requirements](https://antigravity.google/download), version และ Google Account; อย่าติดตั้งทั้งห้องพร้อมกันระหว่าง Lab |
| **Instructor Fallback** | ใช้ Instructor completed project/recording หรือทำ Plan-only/manual team simulation แล้วอภิปราย architecture ต่อ |

## Antigravity quota unavailable

| | |
|---|---|
| **Problem** | Agent เริ่มไม่ได้, quota warning หรือระบบเสนอ plan upgrade |
| **Likely Cause** | Weekly/model limit, task complexity, concurrent demand หรือ plan availability เปลี่ยน |
| **Quick Fix** | หนึ่ง project/conversation ต่อทีม ใช้ dataset 4 rows, compact prompt และไม่ retry ก่อนตรวจผลเดิม; ไม่ซื้อ plan เพื่อผ่าน Lab |
| **Instructor Fallback** | หยุดหลัง plan หรือใช้ Instructor project แล้วให้ทีม validate files ด้วย source Request IDs |

## Antigravity project cannot read the dataset

| | |
|---|---|
| **Problem** | Agent ไม่เห็น `input/business-requests.md`, อ่านจำนวน records ผิด หรือข้าม Request IDs |
| **Likely Cause** | เลือก project folder ผิด, file ไม่ได้ copy เข้า `input/`, permission block หรือ conversation อยู่คนละ project |
| **Quick Fix** | ตรวจ Project Settings/folder, เปิดไฟล์จาก project view และยืนยัน 4 Request IDs ก่อน approve plan |
| **Instructor Fallback** | ใช้ Instructor project หรือให้ทีมอ่าน [Antigravity Lab Input](../templates/antigravity-lab-input.md) และตรวจ row count ด้วยตนเอง |

## Agent writes before approval or outside outputs

| | |
|---|---|
| **Problem** | Agent เริ่มแก้ไฟล์ก่อน Human Proceed, แก้ input หรือสร้างไฟล์นอก `outputs/` |
| **Likely Cause** | Conversation อยู่ Fast Mode, Artifact Review/Agent Behaviour ไม่ได้ตั้ง Request Review, project scope กว้าง, prompt/plan ไม่ระบุ output allowlist หรือผู้ใช้ approve เร็วเกิน |
| **Quick Fix** | Stop execution, reject/revert changes, เริ่ม conversation ใหม่ใน Planning Mode, ตั้ง Artifact Review และ Terminal เป็น Request Review, ใช้ dedicated folder แล้วส่ง [Boundary Correction Prompt](../06-antigravity/prompts.md#boundary-correction-prompt) |
| **Instructor Fallback** | ใช้ prepared plan/file diff ให้ทีมระบุว่าจุดใดควรถูก reject ก่อนดำเนินการ |

## Antigravity does not show Proceed or pauses in a different place

| | |
|---|---|
| **Problem** | ไม่เห็น Proceed, Agent เริ่มทำต่อเอง หรือชื่อ Artifact/Review control ต่างจากคู่มือ |
| **Likely Cause** | Fast Mode, Artifact Review = Always Proceed, project-specific settings สืบทอดค่า global หรือ UI rollout ต่างกัน |
| **Quick Fix** | กด Stop ก่อนมี file changes, เปิด Project Settings, เลือก Planning Mode และ Request Review ที่ artifact/agent behaviour; เริ่ม conversation ใหม่และตรวจ Plan ก่อนส่ง approval |
| **Instructor Fallback** | ใช้ Instructor Plan screenshot ให้ทีมทำ review checklist และตอบว่าจะ approve/reject เพราะเหตุใด |

## Antigravity proposes prohibited tools or external action

| | |
|---|---|
| **Problem** | Agent เสนอ app, browser, URL, MCP, Connector, schedule, package install, email หรือ access นอก project |
| **Likely Cause** | Goal กว้าง, project permission กว้าง หรือข้อห้ามไม่อยู่ใน reviewed plan |
| **Quick Fix** | Reject permission, กด Stop และใช้ [Boundary Correction Prompt](../06-antigravity/prompts.md#boundary-correction-prompt); อย่าเพิ่มสิทธิ์เพื่อให้ task ผ่าน |
| **Instructor Fallback** | ใช้ prepared analysis-only artifacts แล้วอภิปราย Prompt guardrail เทียบกับ Permission guardrail |

## Antigravity triage or HIGH reports fail validation

| | |
|---|---|
| **Problem** | Row count ไม่ใช่ 4, HIGH report count ไม่ตรง HIGH rows, file ซ้ำ/หาย, แต่ง facts หรืออ้างว่าทำ Action แล้ว |
| **Likely Cause** | Agent ข้าม record, input context หาย, hallucination, filename ไม่ตรง plan หรือ validation ไม่ถูกทำ |
| **Quick Fix** | ตรวจ checklist ใน Lab 4 และใช้ [Validation Prompt](../06-antigravity/prompts.md#validation-prompt) โดยอนุญาตให้แก้เฉพาะ approved files ใน `outputs/` |
| **Instructor Fallback** | ให้ทีมทำ reviewer role ระบุ fail points และเปรียบเทียบกับ deterministic validation ใน Make |

## Escalation Rule

หากแก้ไม่สำเร็จภายใน 3 นาที ให้ใช้ fallback เพื่อรักษาเวลา Workshop:

```text
Full Automation
↓ fails
Manual AI + Workflow
↓ fails
Prepared JSON + Router
↓ fails
Paper/Sheet Simulation
```

---

[← Home](../README.md) · [Instructor Checklist](../templates/instructor-checklist.md)
