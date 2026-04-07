# Module 02 Lab 01 - Repeatable Nmap Workflow

---

> **🛠 Lab Objective**
>
> Use the real Module 01 lab baseline to move from target definition to saved scan artifacts, host notes, and a prioritized Module 03 follow-up queue.

| Module | Position | Main output |
|---|---|---|
| Module 02 - Network Enumeration with Nmap | End-of-module lab | saved discovery set, triage and enrichment scans, updated host tracking, follow-up queue |

| Prerequisites | Use while working |
|---|---|
| Lessons 2.1-2.5 and the Module 01 baseline lab | [field reference](../references/module-02-reference-cheat-sheet.md), [scan planning worksheet](../references/module-02-scan-planning-worksheet.md), Module 01 note workspace |

---

## Scenario

You are standing in Kali WSL with the Module 01 course lab available on `LAB-NET` at `192.168.57.0/24`.

Your job is not to “scan everything loudly.”
Your job is to run a disciplined workflow that answers:

- which hosts appear alive from this position?
- which hosts deserve deeper TCP or UDP attention?
- what services and clues should be preserved for Module 03?
- what should be written down so you do not have to rediscover context later?

Use the shared `assessment-workspace/` built in Module 01.

---

## Expected Learner Artifacts

- a completed scan planning worksheet
- saved discovery output for `LAB-NET`
- at least one saved TCP triage scan
- at least one saved enrichment scan
- an updated `host-tracking.md` entry
- an updated `follow-up-queue.md` entry
- a short close-out note separating observation, inference, and validation

---

## Working Paths

Use these defaults unless your Module 01 notes already define a stronger equivalent.

| Artifact | Recommended path |
|---|---|
| Discovery and scan outputs | `assessment-workspace/02-evidence/scans/module-02/` |
| Host notes | `assessment-workspace/01-target-notes/host-tracking.md` |
| Follow-up queue | `assessment-workspace/03-analysis/follow-up-queue.md` |
| Planning worksheet answers | same file or notes alongside `scope.md` / lesson notes |

---

## Lab Workflow

### Checkpoint 1 - Re-anchor the environment

Before scanning, record:

1. the scope source you are using
2. the current network position, explicitly noting Kali WSL
3. the expected target subnet `192.168.57.0/24`
4. the three baseline targets if your notes already know them:
   `GOAD-Mini-DC01`, `META-TGT`, `GOAD-Mini-WS01`

If any of those assumptions are unclear, stop and fix the notes first.

### Checkpoint 2 - Complete the scan planning worksheet

Use the worksheet to define:

- which target form you will use first
- which discovery method fits your current position
- where output will be saved
- which host is the most likely first enrichment candidate

Do not skip this step.
The lab is meant to reinforce deliberate scan planning, not just execution.

### Checkpoint 3 - Run the discovery sweep

Perform a discovery pass against the full lab segment and save the result.

Example:

```bash
mkdir -p assessment-workspace/02-evidence/scans/module-02
nmap -sn -oA assessment-workspace/02-evidence/scans/module-02/lab-net-discovery-YYYY-MM-DD 192.168.57.0/24
```

Then record:

- which hosts were reported up
- whether any expected hosts were silent
- what evidence likely caused Nmap to treat each visible host as alive

### Checkpoint 4 - Preserve the live-host set

Turn the discovery result into a reusable host list or summary.

Good outputs include:

- a short live-host file such as `module-02-targets.txt`
- an update to `host-tracking.md`
- a note of which hosts should move into TCP triage first

At minimum, preserve:

- IP
- likely asset identity
- why it matters
- whether confidence is direct or inferred

### Checkpoint 5 - Run TCP triage on at least one host

Choose at least one interesting host and run a saved TCP triage scan.

Recommended first choices:

- `META-TGT` at `192.168.57.25` for broad Linux-style exposure
- `GOAD-Mini-DC01` at `192.168.57.10` for Windows and identity-oriented exposure

Example:

```bash
nmap -sS -Pn --top-ports 1000 -oA assessment-workspace/02-evidence/scans/module-02/meta-tgt-triage-YYYY-MM-DD 192.168.57.25
```

Capture:

- open ports
- closed ports that still prove reachability
- filtered or ambiguous ports that may shape later decisions

### Checkpoint 6 - Run one focused enrichment pass

Choose one host from the triage step and enrich the scan.

Example:

```bash
nmap -sV -sC -Pn -oA assessment-workspace/02-evidence/scans/module-02/meta-tgt-enriched-YYYY-MM-DD 192.168.57.25
```

If conditions support it and the result would be meaningful, optionally add:

```bash
nmap -O --traceroute -Pn -oA assessment-workspace/02-evidence/scans/module-02/meta-tgt-os-YYYY-MM-DD 192.168.57.25
```

Capture:

- version clues
- service titles or certificate names
- host-role hints
- uncertainty that still needs manual validation

### Checkpoint 7 - Add one protocol-aware follow-up

Use the triage and enrichment results to run one narrower follow-up scan.

Examples:

```bash
nmap -p 80,443 -sV --script http-title,ssl-cert -oA assessment-workspace/02-evidence/scans/module-02/meta-tgt-web-YYYY-MM-DD 192.168.57.25
```

```bash
nmap -p 445 --script smb-os-discovery,smb-enum-shares -oA assessment-workspace/02-evidence/scans/module-02/goad-mini-dc01-smb-YYYY-MM-DD 192.168.57.10
```

The goal is not to exploit anything.
The goal is to sharpen the handoff into Module 03.

### Checkpoint 8 - Update host tracking

Add or update at least one host entry in `assessment-workspace/01-target-notes/host-tracking.md`.

For each host you touched, write:

- what was directly observed
- what you now infer about host role or service mix
- what still needs validation
- which service family should be followed up next

### Checkpoint 9 - Update the follow-up queue

Add a short entry to `assessment-workspace/03-analysis/follow-up-queue.md`.

Good entries look like:

- `192.168.57.10 -> strong Windows / identity clues -> prioritize service footprinting on DNS, Kerberos, LDAP, SMB`
- `192.168.57.25 -> multiple Internet-facing style services -> prioritize service-role interpretation and web follow-up`

### Checkpoint 10 - Write the close-out note

End with a short note that answers:

1. What was directly observed?
2. What is inferred but not yet confirmed?
3. Which saved scan artifacts matter most?
4. What should Module 03 do next with this evidence?

---

## Validation Questions

Use these questions to decide whether the lab is complete:

1. Can you explain why each scan was run?
2. Can you point to where every output file was saved?
3. Can you identify at least one Windows-oriented and one Linux-oriented follow-up path?
4. Have you updated shared course artifacts instead of inventing a one-off workspace?
5. Could you reopen the notes tomorrow and continue into Module 03 without rescanning everything from memory?

---

## Close-Out Standard

This lab is complete when the learner has:

- a defensible discovery result
- saved scan artifacts
- at least one enriched host profile
- a reusable note trail
- a clear Module 03 handoff

If the only result is “I ran some scans,” the workflow is still incomplete.

---

## Design Notes

This lab is intentionally checklist-like.
Module 02 is where scanning should stop feeling like isolated commands and start feeling like reusable assessment work.
