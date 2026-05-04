<div align="center">

# Module 03 - Interpret Exposed Services

**Phase I - Build and See**

### Turn open ports into host-role hypotheses, service evidence, and a prioritized follow-up queue.

*This redesigned Module 03 teaches service footprinting as infrastructure reasoning. The learner starts from saved Module 02 scan evidence, performs small service-aware checks against the course lab, captures exact nouns, and decides which later workflow should own each next step.*

</div>

---

> **Mission Contract**
>
> **You have:** a stable Module 01 lab, saved Module 02 scan outputs, and a host tracker.
>
> **You need to determine:** what the exposed services suggest about host role, trust, data, identity, management, and follow-up priority.
>
> **You will produce:** host-role notes, a completed service-role worksheet, saved service evidence, and a prioritized follow-up queue.
>
> **You are done when:** every important exposed service has an evidence-backed interpretation, a confidence level, and a next workflow owner.

---

## Start Here

Open the lab before reading the lessons:

[Module 03 Lab - Interpret Exposed Services](labs/module-03-lab-01-interpret-exposed-services.md)

The lab is not an end-of-module appendix. It is the practice spine for the whole module.

Work in this order:

| Step | Read | Then do |
|---|---|---|
| 1 | [Lesson 3.1 - Reading Services as Environment Evidence](lessons/module-03-lesson-3-1-reading-services-as-environment-evidence.md) | Lab Checkpoint A |
| 2 | [Lesson 3.2 - File, Naming, and Communication Services](lessons/module-03-lesson-3-2-file-name-and-communication-services.md) | Lab Checkpoint B |
| 3 | [Lesson 3.3 - Data, Management, and Remote Access Services](lessons/module-03-lesson-3-3-data-management-and-remote-access-services.md) | Lab Checkpoint C |
| 4 | [Lesson 3.4 - Building the Service Triage Queue](lessons/module-03-lesson-3-4-building-the-service-triage-queue.md) | Lab Checkpoint D |

Keep these references open while you work:

- [Module 03 Field Reference](references/module-03-field-reference.md)
- [Service Role Worksheet](references/module-03-service-role-worksheet.md)
- [SMB Playbook](references/playbooks/smb.md)
- [DNS and Naming Playbook](references/playbooks/dns.md)
- [FTP Playbook](references/playbooks/ftp.md)

---

## Why This Module Exists

Module 02 taught the learner how to discover reachable hosts and exposed ports. That is necessary, but it is not enough.

A scan can tell us that `445/tcp` is open, but it cannot explain by itself whether the host is a domain controller, workstation, file server, forgotten lab system, or something behind a filtering path. It can tell us that `53/tcp` is reachable, but it does not automatically tell us whether the host is authoritative for a domain, resolving internal names, or simply exposing a service in a lab.

Module 03 is where the learner starts interpreting exposure as environment evidence.

That means the central question changes from:

> What ports are open?

to:

> What does this service exposure suggest about the role, trust, and follow-up value of this host?

That shift matters because offensive work quickly becomes overwhelming if every open service receives equal attention. A learner who sees FTP, SMB, DNS, RDP, SSH, HTTP, LDAP, and database ports all at once needs a way to decide what each service means and what deserves attention first.

This module teaches that decision layer.

---

## Required Baseline

This redesigned module assumes the course lab established in Module 01 and exercised in Module 02.

| Role | Host | IP | Why it matters in this module |
|---|---|---:|---|
| Windows infrastructure host | `GOAD-Mini-DC01` | `192.168.57.10` | naming, identity, SMB, LDAP, Kerberos, and Windows infrastructure clues |
| Windows workstation | `GOAD-Mini-WS01` | `192.168.57.31` | SMB, RDP, workstation role, and management-surface reasoning |
| Linux target | `META-TGT` | `192.168.57.25` | FTP, SSH, HTTP, and mixed-service Linux footprinting |

If your local lab differs, keep the same reasoning pattern. Replace the IPs, but do not skip the artifact discipline.

---

## What You Will Produce

By the end of this module, the learner should have:

| Artifact | Purpose |
|---|---|
| `module-03-host-role-notes.md` | records host-role hypotheses and the evidence behind them |
| service evidence files | preserves useful command output and manual observations |
| completed service-role worksheet | turns ports into service roles, host clues, and next-step owners |
| `follow-up-queue.md` updates | routes web, credential, service-attack, Windows, AD, and reporting work |

The important output is not a longer list of commands.

The important output is a more defensible interpretation of the environment.

---

## Lesson Design

This redesigned module uses different lesson weights.

| Lesson | Type | Job |
|---|---|---|
| 3.1 | Anchor lesson | Builds the mental model for reading services as environment evidence |
| 3.2 | Workflow lesson | Teaches file, naming, and communication services through interpretation, not protocol trivia |
| 3.3 | Workflow lesson | Teaches data, management, and remote-access services as value and control-plane clues |
| 3.4 | Synthesis lesson | Converts service evidence into a prioritized follow-up queue |

The lessons are written to explain how an assessor thinks. Deep command detail moves into field references and playbooks.

---

## Completion Gate

Module 03 is complete when the learner can answer these questions from their own notes:

1. Which services were directly observed on each baseline host?
2. What exact names, shares, records, banners, realms, or management clues were captured?
3. Which host-role hypotheses are supported by more than one clue?
4. Which conclusions are still only guesses?
5. Which follow-up items belong to Module 04 web recon, Module 06 credential work, Module 09 service attacks, Module 12 Windows work, or Module 14 AD reasoning?
6. What should be tested first, and why?

If those answers are vague, the module is not done yet.

---

## Handoff to Module 04

Module 04 starts with web targets.

Module 03 should hand it a cleaner queue:

- which hosts expose HTTP or HTTPS
- what service role those hosts appear to have
- whether web exposure sits on a domain controller, workstation, Linux server, or mixed-service host
- what names or certificates might shape web recon
- what should be mapped first

The learner should not enter Module 04 with "port 80 open."

They should enter with a service-aware reason for why a web surface matters.

