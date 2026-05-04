# Module 02 Redesign Notes

## Purpose of This Example

This folder shows what Module 02 could look like under the redesigned `Hack the Basics` delivery model.

It uses the original Module 02 as source material, but changes the learning experience in four ways:

1. The module is framed as a mission: map the visible network.
2. The lab is opened early and used after every lesson.
3. The lessons teach scan reasoning through connected prose instead of long workshop-style sections.
4. Command variants and quick reminders move into references and playbooks.

This is a prototype, not a final production replacement for the existing module.

---

## New File Roles

| File | Role |
|---|---|
| `README.md` | mission contract, learner path, completion gate, and Module 03 handoff |
| `lessons/` | rewritten teaching path using anchor, workflow, tactical, and synthesis lessons |
| `labs/module-02-lab-01-map-the-visible-network.md` | progressive lab spine |
| `references/module-02-field-reference.md` | compact scanning and interpretation reference |
| `references/module-02-scan-planning-worksheet.md` | reusable planning and note artifact |
| `references/playbooks/` | focused guidance for discovery, port states, and enrichment |

---

## What Changed From the Original Module

### 1. The README is a mission contract

The original README is already strong, but the redesigned README is more operational.

It tells the learner:

- what they have
- what they need to determine
- what they will produce
- when the module is complete
- what Module 03 needs from them

### 2. The lab is the module spine

The original lab is strong as a synthesis exercise.

The redesign moves that model earlier. The learner opens the lab first and completes one checkpoint after each lesson.

| Lesson | Checkpoint |
|---|---|
| 2.1 | define the scan question |
| 2.2 | discover live hosts |
| 2.3 | run TCP and UDP triage |
| 2.4 | enrich service clues |
| 2.5 | build the Module 03 handoff |

### 3. Lessons teach Nmap as reasoning, not flags

The original module already tries to avoid flag worship.

The redesigned lessons push that further by making the central lesson voice:

```text
What question is this scan asking?
What did the probe observe?
What inference is justified?
What still needs validation?
Where should the evidence be saved?
```

### 4. References absorb command density

The original Module 02 has enough command coverage that the main lessons can become heavy.

The prototype keeps representative commands in the lessons and moves fast command patterns into:

- field reference
- host discovery playbook
- port state playbook
- service enrichment playbook

---

## Evaluation Criteria

This redesigned module should be judged by whether a learner can:

1. define scope and scan questions before scanning
2. discover hosts without overclaiming silence
3. interpret port states as scanner labels
4. enrich services with focused intent
5. save evidence consistently
6. update host tracking with observation, inference, validation, and next step
7. hand Module 03 a useful service-footprinting queue

If those outcomes are clearer than the original module path, the redesign is moving in the right direction.

