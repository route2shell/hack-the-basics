<div align="center">

# Module 01 Field Reference

**Orientation and Assessment Workflow**

*Phase I - Orientation and Surface Mapping*

</div>

---

> **🧭 Use This For**
>
> Fast reminders when you need to re-anchor yourself in the course workflow, the assessment lifecycle, scope discipline, workspace habits, and note quality before or during later technical modules.

| Best paired with | Main job | Assumption |
|---|---|---|
| Lesson 1.4 and the module lab | Help you work like an analyst instead of a tool collector | Legal lab use only |

| Preserve these outputs | Avoid these habits |
|---|---|
| clear scope notes, lifecycle awareness, usable evidence, route-ready notes, lab hygiene | random tool hopping, vague notes, untracked screenshots, sloppy scope assumptions |

---

## Table of Contents

- [1. Quick Workflow](#1-quick-workflow)
- [2. Course Success Model](#2-course-success-model)
- [3. Assessment Lifecycle](#3-assessment-lifecycle)
- [4. Scope and Lab Discipline](#4-scope-and-lab-discipline)
- [5. VMware Lab Baseline](#5-vmware-lab-baseline)
- [6. Note-Taking Rules](#6-note-taking-rules)
- [7. Observation vs Inference vs Validation](#7-observation-vs-inference-vs-validation)
- [8. Daily Analyst Questions](#8-daily-analyst-questions)
- [9. Minimal Assessment Note Template](#9-minimal-assessment-note-template)

---

## 1. Quick Workflow

> **🧠 Mental Model**
>
> orient -> define scope -> build workspace -> gather evidence -> reason carefully -> choose the next step

### Fast operator rhythm

1. Confirm what environment you are in and what is authorized.
2. Identify the current assessment phase.
3. Write the current question before you start the next action.
4. Capture exact evidence, not vague impressions.
5. Separate what you know from what you suspect.
6. Leave behind notes that later modules can build on.

---

## 2. Course Success Model

This course is designed to produce learners who can explain:

- what they observed
- what they inferred
- what they validated
- why the next step made sense

### Strong learning habits

- read lessons in sequence on the first pass
- keep a stable lab and note structure
- repeat workflows, not only commands
- prefer exact nouns over loose summaries
- revisit references while practicing

---

## 3. Assessment Lifecycle

| Phase | Main question |
|---|---|
| Orientation | what is the environment, goal, and current constraint set? |
| Surface mapping | what is visible and reachable from here? |
| Service and app understanding | what do the visible services and apps probably mean? |
| Validation and access | what can be tested or verified next? |
| Post-access and expansion | what changed after we gained visibility or execution? |
| Reporting and close-out | what evidence and findings are worth preserving? |

### Quick lifecycle reminders

- every later module is one part of this larger flow
- different phases ask different questions
- strong notes should always name the current phase

---

## 4. Scope and Lab Discipline

### Non-negotiables

- work only inside authorized lab environments
- record scope and exclusions before testing
- isolate the lab from anything unintended
- snapshot important VMs before risky changes
- document what you changed in the environment
- do not let convenience erase evidence quality

### Scope prompts

- what hosts or domains are in scope?
- what hosts or domains are excluded?
- what network are you standing on right now?
- what action are you about to take, and why is it authorized here?

---

## 5. VMware Lab Baseline

### Host platform

- VMware Workstation Pro

### Core VM roles

| VM | Role |
|---|---|
| Kali | primary attack and analysis workstation |
| Metasploit / Metasploitable practice target | intentionally vulnerable target for early lessons and safe attack-path practice |
| Basic Linux VM | configurable service and privilege-escalation target |
| Windows 11 VM | later Windows, authentication, and AD-related learning path |

### Good lab habits

- use clear VM names
- keep a VM inventory table
- decide which NICs are host-only, NAT, or isolated
- snapshot before major configuration changes
- note credentials, IPs, and network purpose in one place

---

## 6. Note-Taking Rules

### Capture exact things

- IPs
- hostnames
- URLs
- commands
- output snippets
- timestamps
- screenshots with context

### Avoid vague notes

Weak:

```text
Interesting host. Maybe web app.
```

Strong:

```text
10.10.10.15 responds on 80/tcp and 443/tcp; cert name portal.lab.local; HTTP root redirects to /login.
```

---

## 7. Observation vs Inference vs Validation

| Category | Meaning |
|---|---|
| Observation | what you directly saw |
| Inference | what you think that evidence suggests |
| Validation | what still needs to be confirmed |

### Example

```text
Observation: 443/tcp open; cert SAN includes admin.lab.local
Inference: target may host an admin-related surface
Validation: confirm whether admin.lab.local resolves and responds distinctly
```

---

## 8. Daily Analyst Questions

- What phase of the assessment am I in?
- What question am I trying to answer right now?
- What evidence will count as useful?
- What is directly observed versus inferred?
- What should happen next if this succeeds?
- What should happen next if this fails?

---

## 9. Minimal Assessment Note Template

```text
Assessment context:
Current phase:
Scope:
Network position:
Target or host:
Question being asked:
Action taken:
Observation:
Inference:
Validation needed:
Next step:
```

---

<div align="center">

**The point of Module 01 is not to slow you down. It is to make every later action more deliberate and more reusable.**

</div>
