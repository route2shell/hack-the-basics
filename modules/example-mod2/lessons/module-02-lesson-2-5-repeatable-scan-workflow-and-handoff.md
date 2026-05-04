# Lesson 2.5 - Repeatable Scan Workflow and Handoff

---

> **Lesson Objective**
>
> Learn to turn individual Nmap commands into a repeatable assessment workflow with saved artifacts, host notes, and a clean Module 03 handoff.

| Course | Module | Lesson | Type | Estimated time |
|---|---|---|---|---:|
| Hack the Basics | 02 - Map the Visible Network | 2.5 | Synthesis lesson | 50-70 min |

| You have | You will produce | Lab checkpoint |
|---|---|---|
| discovery, triage, and enrichment scans | host tracker and Module 03 queue | Checkpoint E |

---

## Why This Lesson Matters

Running a good scan once is useful. Building a repeatable scan workflow is better.

In real work, the scan output must survive beyond the terminal session. The learner needs to compare results, revisit evidence, update notes, explain uncertainty, and hand off service clues to later modules. If outputs are scattered, unsaved, or named vaguely, the work becomes fragile.

This lesson turns scanning into an artifact pipeline.

The pipeline is:

```text
Define -> Discover -> Triage -> Enrich -> Preserve -> Interpret -> Route
```

Each step has a job. If one step breaks, the whole workflow weakens.

---

## Saving Output Is Part of the Work

The terminal is not a durable evidence store.

If the learner runs a scan and only reads the live output, several problems appear:

- the output scrolls away
- details are copied inaccurately
- results cannot be compared later
- reporting becomes harder
- Module 03 has no reliable source evidence
- the learner may rerun noisy scans because they lost context

Saved output is not just convenience. It is part of the assessment record.

Use a short output root:

```bash
M2SCAN=assessment-workspace/02-evidence/scans/m02
mkdir -p "$M2SCAN"
```

Then use readable basenames:

```text
lab-discovery-YYYY-MM-DD
meta-tcp-triage-YYYY-MM-DD
dc01-service-enriched-YYYY-MM-DD
targets.txt
```

The goal is that another learner can open the folder and understand what happened.

---

## A Repeatable Scan Sequence

A practical Module 02 sequence looks like this:

### 1. Define

Write the scope, network position, and first scan question.

### 2. Discover

Find which hosts appear reachable.

```bash
nmap -sn -oA "$M2SCAN"/lab-discovery-YYYY-MM-DD 192.168.57.0/24
```

### 3. Preserve targets

Create or update a target list.

```bash
printf "192.168.57.10\n192.168.57.25\n192.168.57.31\n" > "$M2SCAN"/targets.txt
```

### 4. Triage

Run focused TCP triage against important hosts.

```bash
nmap -sS -Pn --top-ports 1000 -oA "$M2SCAN"/meta-tcp-triage-YYYY-MM-DD 192.168.57.25
```

### 5. Enrich

Ask what appears behind the open ports.

```bash
nmap -sV -sC -Pn -p <open-ports> -oA "$M2SCAN"/meta-service-enriched-YYYY-MM-DD 192.168.57.25
```

### 6. Interpret

Write what was observed and what it suggests.

### 7. Route

Add follow-up items for Module 03.

This sequence is intentionally plain. A repeatable workflow does not need to be dramatic. It needs to be clear, saved, and defensible.

---

## Host Tracking Turns Output Into Assessment Memory

The host tracker is where scan output becomes target knowledge.

It should not be a pasted port list. It should summarize the meaning of the output.

Weak entry:

```text
192.168.57.25: 21, 22, 80 open.
```

Stronger entry:

```text
192.168.57.25 appears reachable from Kali WSL. TCP triage reports FTP, SSH, and HTTP open. This suggests a Linux or mixed-service target with file-transfer, management, and web surfaces. Module 03 should footprint FTP and SSH posture; Module 04 should later map HTTP.
```

The stronger entry gives future work a starting point.

---

## The Follow-Up Queue

The follow-up queue is where Module 02 hands work to Module 03.

Good queue entries are not just "check SMB" or "look at web." They explain why the service matters.

Example:

```text
Host:
192.168.57.10

Services:
53, 88, 389, 445

Reason:
Service combination suggests naming and identity infrastructure. Module 03 should footprint DNS, LDAP, Kerberos, and SMB to validate host role and capture exact domain or host clues.

Evidence path:
assessment-workspace/02-evidence/scans/m02/dc01-service-enriched-YYYY-MM-DD.nmap
```

This gives Module 03 a job.

---

## What a Strong Module 02 Close-Out Looks Like

A good close-out note should say:

```text
Direct observations:
Discovery scan reported .10, .25, and .31 reachable from Kali WSL. TCP triage found identity-oriented services on .10, FTP/SSH/HTTP on .25, and SMB/RDP-style services on .31.

Inferences:
.10 likely has Windows identity infrastructure relevance. .25 appears to be a mixed Linux service target. .31 appears to be a Windows host with file and remote-access exposure.

Validation needed:
Module 03 should footprint service roles and exact nouns. Module 04 should later map HTTP. Credential-dependent services should be revisited after Module 06.

Evidence:
Saved under assessment-workspace/02-evidence/scans/m02/.
```

This note is the difference between scanning and enumeration.

---

## Checkpoint

Open the module lab and complete Checkpoint E.

Update:

- `host-tracking.md`
- `follow-up-queue.md`
- close-out note

Make sure every important claim points back to saved evidence.

---

## Key Takeaways

- A repeatable scan workflow saves evidence by default.
- Output names should explain what the scan was for.
- Host tracking turns scan output into assessment memory.
- Follow-up queues route service work into Module 03.
- Module 02 is complete only when evidence, notes, and next steps all exist.

---

## Module Close-Out

Module 03 should receive a saved surface map, not a vague memory.

Before moving on, the learner should be able to say:

> These hosts appeared reachable. These ports responded. These services deserve footprinting. Here are the saved files. Here is what I think they suggest, and here is what still needs validation.

That is the standard.

