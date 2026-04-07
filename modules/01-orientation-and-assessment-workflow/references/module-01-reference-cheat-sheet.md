<div align="center">

# Module 01 Field Reference

**Orientation and Assessment Workflow**

*Phase I - Orientation and Surface Mapping*

</div>

---

> **Use This For**
>
> Fast reminders when you need to re-anchor yourself in the course workflow, the lab baseline, the note artifacts, and the observation versus inference discipline that Module 02 will immediately rely on.

| Best paired with | Main job | Assumption |
|---|---|---|
| Lesson 1.3, Lab 01, and Lesson 1.4 | Keep the learner aligned to the real Module 01 baseline and handoff | Legal lab use only |

| Preserve these outputs | Avoid these habits |
|---|---|
| scope note, VM inventory, network notes, snapshot map, first analyst note | random tool hopping, vague environment memory, untracked changes, sloppy confidence |

---

## Table of Contents

- [1. Module 01 Completion Flow](#1-module-01-completion-flow)
- [2. Course Success Model](#2-course-success-model)
- [3. Assessment Lifecycle](#3-assessment-lifecycle)
- [4. Scope and Lab Discipline](#4-scope-and-lab-discipline)
- [5. Baseline Lab Model](#5-baseline-lab-model)
- [6. Required Module 01 Artifacts](#6-required-module-01-artifacts)
- [7. Observation vs Inference vs Validation](#7-observation-vs-inference-vs-validation)
- [8. Daily Analyst Questions](#8-daily-analyst-questions)
- [9. Minimal Assessment Note Template](#9-minimal-assessment-note-template)

---

## 1. Module 01 Completion Flow

> **Mental Model**
>
> Orientation first, structure second, build third, reasoning fourth.

1. Understand what the course is trying to teach.
2. Understand the assessment lifecycle.
3. Define scope, asset roles, and the reset model.
4. Build the lab and workspace.
5. Write notes like an analyst before Module 02 begins.

---

## 2. Course Success Model

This course is designed to produce learners who can explain:

- what they observed
- what they inferred
- what they validated
- why the next step made sense

### Strong learning habits

- read the lessons in sequence on the first pass
- build the environment while documenting it
- treat artifacts as working tools, not bonus files
- use exact nouns in notes
- return to the workflow question before chasing tools

---

## 3. Assessment Lifecycle

| Phase | Main question |
|---|---|
| Orientation | what is the environment, what is authorized, and what constraints define the work? |
| Surface mapping | what is visible and reachable from here? |
| Service and app understanding | what do the visible services and routes probably mean? |
| Validation and access | what deserves direct testing or authenticated interaction next? |
| Post-access and expansion | what changed after access and what new paths now exist? |
| Reporting and close-out | what evidence and findings must survive beyond the session? |

### Quick reminder

Module 01 mainly lives in Orientation, but it is building the exact baseline that Surface Mapping will use next.

---

## 4. Scope and Lab Discipline

### Non-negotiables

- work only inside authorized lab environments
- record what assets are in scope
- keep the targets on an isolated host-only subnet
- document environment changes while they happen
- snapshot clean target states before later drift begins
- keep the operator environment separate from the targets mentally and in notes

### Scope prompts

- what assets are in scope?
- what assets are excluded?
- what network am I standing on right now?
- what action am I about to take, and why is it authorized here?

---

## 5. Baseline Lab Model

### Operator environment

- Windows 11 host
- Kali WSL as the attack and analysis platform
- VMware Workstation Pro for the target VMs

### Core target roles

| Asset | Role |
|---|---|
| `GOAD-Mini-DC01` | domain controller target |
| `GOAD-Mini-WS01` | domain-joined workstation target |
| `META-TGT` | intentionally vulnerable Linux target |

### Stable target subnet

| Label | Subnet | Notes |
|---|---|---|
| `LAB-NET` | `192.168.57.0/24` | VMware host-only network for the target VMs |

### Expected target IPs

| Asset | Expected IP |
|---|---|
| `GOAD-Mini-DC01` | `192.168.57.10` |
| `GOAD-Mini-WS01` | `192.168.57.31` |
| `META-TGT` | `192.168.57.25` |

---

## 6. Required Module 01 Artifacts

Before Module 02 starts, these should exist:

- `scope.md`
- `vm-inventory.md`
- `network-notes.md`
- `snapshot-map.md`
- one first analyst note using observation, inference, validation, and next-step language

### Why these matter

- `scope.md` keeps the environment bounded
- `vm-inventory.md` preserves names, roles, hostnames, and IPs
- `network-notes.md` preserves the learner's network position
- `snapshot-map.md` preserves the reset model
- the analyst note turns setup into workflow instead of memory

---

## 7. Observation vs Inference vs Validation

| Category | Meaning |
|---|---|
| Observation | what you directly saw |
| Inference | what you think that evidence probably suggests |
| Validation | what still needs confirmation |

### Example

```text
Observation: 192.168.57.10 answers on 53, 88, 135, 389, and 445 from Kali WSL.
Inference: the host is likely the domain controller in the course baseline.
Validation: confirm identity during later enumeration and preserve the result in host tracking notes.
```

---

## 8. Daily Analyst Questions

- What phase of the lifecycle am I in?
- What question am I trying to answer right now?
- What is directly observed versus only inferred?
- What note artifact should this step update?
- What should happen next if this succeeds?
- What should happen next if this fails?

---

## 9. Minimal Assessment Note Template

```text
Assessment context:
Current phase:
Scope:
Network position:
Target or asset:
Question being asked:
Action taken:
Observation:
Inference:
Validation needed:
Next step:
```

---

<div align="center">

**Module 01 is complete when the learner can explain the baseline, trust the notes, and begin Module 02 without rebuilding context from memory.**

</div>
