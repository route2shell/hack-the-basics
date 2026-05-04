<div align="center">

# Module 02 - Map the Visible Network

**Phase I - Build and See**

### Learn to turn the Module 01 lab into saved scan evidence, host notes, and a service follow-up queue.

*This redesigned Module 02 teaches Nmap as an evidence-gathering instrument. The learner defines scope, discovers live hosts, interprets port states, enriches service clues, and preserves everything in the shared assessment workspace.*

</div>

---

> **Mission Contract**
>
> **You have:** a stable Module 01 lab, Kali WSL, an approved target subnet, and a shared assessment workspace.
>
> **You need to determine:** which hosts appear reachable from your position, which ports respond to your probes, what service clues are worth preserving, and what Module 03 should inspect next.
>
> **You will produce:** a scan plan, saved discovery output, saved triage and enrichment scans, host-tracking updates, and a follow-up queue.
>
> **You are done when:** your scan artifacts are saved, your host notes separate observation from inference, and Module 03 has a clear service-footprinting queue.

---

## Start Here

Open the lab before reading the lessons:

[Module 02 Lab - Map the Visible Network](labs/module-02-lab-01-map-the-visible-network.md)

The lab is the spine of the module. Each lesson prepares one checkpoint.

| Step | Read | Then do |
|---|---|---|
| 1 | [Lesson 2.1 - Scanning as Evidence Collection](lessons/module-02-lesson-2-1-scanning-as-evidence-collection.md) | Lab Checkpoint A |
| 2 | [Lesson 2.2 - Target Definition and Host Discovery](lessons/module-02-lesson-2-2-target-definition-and-host-discovery.md) | Lab Checkpoint B |
| 3 | [Lesson 2.3 - Port States and Probe Interpretation](lessons/module-02-lesson-2-3-port-states-and-probe-interpretation.md) | Lab Checkpoint C |
| 4 | [Lesson 2.4 - Service Enrichment and Host Clues](lessons/module-02-lesson-2-4-service-enrichment-and-host-clues.md) | Lab Checkpoint D |
| 5 | [Lesson 2.5 - Repeatable Scan Workflow and Handoff](lessons/module-02-lesson-2-5-repeatable-scan-workflow-and-handoff.md) | Lab Checkpoint E |

Keep these references open while you work:

- [Module 02 Field Reference](references/module-02-field-reference.md)
- [Scan Planning Worksheet](references/module-02-scan-planning-worksheet.md)
- [Host Discovery Playbook](references/playbooks/host-discovery.md)
- [Port State Playbook](references/playbooks/port-states.md)
- [Service Enrichment Playbook](references/playbooks/service-enrichment.md)

---

## Why This Module Exists

Module 01 built the lab and the note system. Module 02 is where the learner starts using that environment to answer live technical questions.

The point is not to memorize Nmap flags. The point is to learn how scanning turns a network position into evidence.

A scan is always asking a scoped question from a specific vantage point:

> When I send this kind of probe from here, what response pattern do I observe?

That response pattern may show a host is alive, a port appears open, a port appears closed, a network path appears filtered, or a service may be present. But none of those labels are magic truth. They are scanner interpretations based on observed behavior.

This module teaches the learner to preserve that distinction.

---

## Required Baseline

| Layer | Expected baseline |
|---|---|
| Operator position | Kali WSL |
| Virtualization platform | VMware Workstation Pro on Windows 11 host |
| Target subnet | `192.168.57.0/24` |
| Windows infrastructure host | `GOAD-Mini-DC01` at `192.168.57.10` |
| Windows workstation | `GOAD-Mini-WS01` at `192.168.57.31` |
| Linux target | `META-TGT` at `192.168.57.25` |
| Workspace | `assessment-workspace/` |

If your lab differs, write down the difference before scanning.

Scanning without environment context creates weak evidence.

---

## What You Will Produce

| Artifact | Purpose |
|---|---|
| scan planning worksheet | records scope, target form, scan intent, and output paths |
| discovery output | records which hosts appear reachable from Kali WSL |
| target list | preserves a reusable live-host set |
| TCP/UDP triage scans | identifies visible attack surface |
| enrichment scans | captures service, script, version, and host-role clues |
| host-tracking updates | turns output into target notes |
| follow-up queue | hands service families into Module 03 |

The deliverable is not "I ran Nmap."

The deliverable is an evidence trail that another learner could reopen and understand.

---

## Lesson Design

| Lesson | Type | Job |
|---|---|---|
| 2.1 | Anchor lesson | builds the probe -> observe -> infer -> validate mental model |
| 2.2 | Workflow lesson | teaches target definition and host discovery as scope-aware visibility work |
| 2.3 | Tactical lesson | teaches TCP, UDP, and port-state interpretation without treating labels as truth |
| 2.4 | Workflow lesson | teaches service/version/script enrichment as host-role evidence collection |
| 2.5 | Synthesis lesson | turns individual scans into a repeatable saved workflow and Module 03 handoff |

Deep command variants live in references and playbooks.

---

## Completion Gate

Module 02 is complete when the learner can answer:

1. What target set was in scope?
2. What network position were the scans run from?
3. Which hosts appeared alive, and what evidence supported that?
4. Which ports appeared open, closed, filtered, or ambiguous?
5. Which service clues were saved for Module 03?
6. Which results are observations, and which are inferences?
7. Where are the saved artifacts?
8. What should Module 03 inspect first?

If the learner cannot answer from their own notes and saved outputs, the module is not done.

---

## Handoff to Module 03

Module 03 needs more than a port list.

It needs:

- live hosts
- open services
- service guesses
- version clues
- hostnames or OS hints
- ambiguous results that deserve care
- a prioritized list of service families to footprint

The learner should not enter Module 03 with "scan complete."

They should enter with a saved attack-surface map and a reasoned follow-up queue.

