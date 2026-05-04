# Module 03 Redesign Notes

## Purpose of This Example

This folder shows what Module 03 could look like under the redesigned `Hack the Basics` delivery model.

It uses the original module as the content source, but changes the learning experience in four ways:

1. The module is framed as a mission: interpret exposed services.
2. The lab is opened early and used as the module spine.
3. The lessons teach through connected prose and reasoning instead of long workshop-style bullet scaffolding.
4. Deep protocol detail moves into references and playbooks so the main lesson path can stay focused on how to think.

This is not a final production replacement for the existing Module 03. It is a concrete prototype of the redesign direction.

---

## New File Roles

| File | Role |
|---|---|
| `README.md` | mission contract, learner path, completion gate, and handoff |
| `lessons/` | rewritten teaching path with anchor, workflow, and synthesis lessons |
| `labs/module-03-lab-01-interpret-exposed-services.md` | progressive lab spine used throughout the module |
| `references/module-03-field-reference.md` | compact command and interpretation reference |
| `references/module-03-service-role-worksheet.md` | learner artifact for host-role and service-role reasoning |
| `references/playbooks/` | deeper service-specific execution guidance |

---

## What Changed From the Original Module

### 1. The README is now a mission contract

The original README is thorough, but it carries a lot of explanatory weight.

The redesigned README is more operational. It tells the learner:

- what they have
- what they need to determine
- what they will produce
- where to start
- when the module is done
- how Module 04 depends on the output

### 2. The lab is the central spine

The redesigned lab is meant to be opened before the first lesson.

Each lesson points back into a checkpoint:

| Lesson | Checkpoint |
|---|---|
| 3.1 | Read scan evidence and write host-role hypotheses |
| 3.2 | Capture file, naming, and communication clues |
| 3.3 | Capture data, management, and remote-access clues |
| 3.4 | Build the follow-up queue |

This prevents the learner from passively reading four lessons and only practicing at the end.

### 3. Lessons are rewritten as reasoning chapters

The original lessons contain strong ideas, but many sections lean on lists, tables, and repeated structure.

The rewritten lessons use more explanatory prose:

- why the concept matters
- how the evidence changes interpretation
- where a beginner might overclaim
- what a stronger note looks like
- how the next workflow is selected

Bullets and tables remain, but they support the explanation instead of replacing it.

### 4. Protocol depth is moved into playbooks

The original Module 03 can easily become too broad because every service family has its own tools, defaults, outputs, and edge cases.

The prototype keeps the main path focused on service meaning and puts deeper operational detail into playbooks.

The example includes:

- SMB
- DNS and naming
- FTP

Additional playbooks could be added for:

- LDAP
- RDP
- SSH
- SNMP
- MSSQL
- MySQL
- NFS
- mail services

---

## Evaluation Criteria

This redesigned module should be judged by whether a learner can:

1. explain what service footprinting is for
2. start from saved scan evidence instead of immediately running more tools
3. translate services into environment functions
4. capture exact nouns that matter later
5. separate observation, inference, validation, and next step
6. create a prioritized follow-up queue
7. hand Module 04 a cleaner web-recon starting point

If those outcomes are stronger than the original module path, the redesign is moving in the right direction.

