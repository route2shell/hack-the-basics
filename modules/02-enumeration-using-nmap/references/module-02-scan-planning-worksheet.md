# Module 02 Scan Planning Worksheet

---

> **📝 Worksheet Purpose**
>
> Use this worksheet before and during scanning so scope, target choice, output paths, and follow-up notes are intentional instead of improvised.

| Best used with | Main job | Default baseline |
|---|---|---|
| Lessons 2.1, 2.2, 2.5, and Module 02 Lab 01 | Turn scan intent into a repeatable plan and artifact trail | Kali WSL scanning `LAB-NET` on `192.168.57.0/24` |

---

## Table of Contents

- [1. Assessment Context](#1-assessment-context)
- [2. Baseline Assumptions](#2-baseline-assumptions)
- [3. Target Definition Plan](#3-target-definition-plan)
- [4. Scan Plan](#4-scan-plan)
- [5. Artifact Paths](#5-artifact-paths)
- [6. Observation, Inference, and Validation Prompts](#6-observation-inference-and-validation-prompts)
- [7. Close-Out Checklist](#7-close-out-checklist)

---

## 1. Assessment Context

Fill this before the first scan.

| Prompt | Your entry |
|---|---|
| Assessment context |  |
| Current module / lesson |  |
| Scope source |  |
| Network position |  |
| Why this scan matters right now |  |

---

## 2. Baseline Assumptions

Use this section to confirm you are standing in the expected Module 01 environment.

| Item | Expected value | Your entry |
|---|---|---|
| Attack platform | Kali WSL |  |
| Target subnet | `192.168.57.0/24` |  |
| Windows targets | `GOAD-Mini-DC01`, `GOAD-Mini-WS01` |  |
| Linux target | `META-TGT` |  |
| Shared note workspace | `assessment-workspace/` |  |

> **🚨 Important**
>
> If any of these assumptions are untrue, record the difference before scanning.
> Module 02 depends on perspective and environment context.

---

## 3. Target Definition Plan

| Prompt | Your entry |
|---|---|
| Targets in scope |  |
| Targets excluded |  |
| Why these targets matter |  |
| Target form to use |  |
| If using a target file, where does it live? |  |
| What would count as a good first discovery result? |  |

### Common target-form reminders

```text
Single host:
CIDR range:
Short list:
Input file:
Range with exclusions:
```

---

## 4. Scan Plan

Plan each pass before you run it.

| Scan stage | Question being asked | Planned command | What result would count as useful? |
|---|---|---|---|
| Discovery |  |  |  |
| TCP triage |  |  |  |
| UDP follow-up |  |  |  |
| Enrichment |  |  |  |
| Focused re-check |  |  |  |

### Practical prompts

- Which scan absolutely needs saved output?
- Which scan may require `-Pn`, and why?
- Which host is the best first enrichment candidate?
- Which service families look likely to hand off into Module 03?

---

## 5. Artifact Paths

Use the shared Module 01 workspace by default.

| Artifact | Recommended path | Your chosen path |
|---|---|---|
| Discovery outputs | `assessment-workspace/02-evidence/scans/module-02/` |  |
| Host list | `assessment-workspace/02-evidence/scans/module-02/module-02-targets.txt` |  |
| Host notes | `assessment-workspace/01-target-notes/host-tracking.md` |  |
| Follow-up queue | `assessment-workspace/03-analysis/follow-up-queue.md` |  |

### Naming convention prompt

```text
<target-or-targetset>-<scan-purpose>-<YYYY-MM-DD>
```

Examples:

```text
lab-net-discovery-2026-04-06
meta-tgt-triage-2026-04-06
goad-mini-dc01-enriched-2026-04-06
```

---

## 6. Observation, Inference, and Validation Prompts

Use this after each meaningful scan pass.

| Category | Prompt | Your entry |
|---|---|---|
| Observation | What did the scan directly show? |  |
| Inference | What does that evidence probably suggest? |  |
| Validation | What still needs confirmation outside this scan? |  |
| Next step | What should happen next, and which module or workflow owns it? |  |

---

## 7. Close-Out Checklist

Mark each item before you consider the workflow complete.

- [ ] Scope and network position were written down before scanning.
- [ ] Scan outputs were saved in the shared workspace.
- [ ] Live hosts were preserved in a reusable list or note.
- [ ] At least one host note was updated with observation, inference, and validation language.
- [ ] A next-step entry was added to the follow-up queue.
- [ ] The learner can explain why the next move belongs to Module 03 or another later workflow.

---

## Design Notes

This worksheet is meant to be reused across the whole module, not filled once and forgotten.
It should travel with the learner from first plan through the full Module 02 lab.
