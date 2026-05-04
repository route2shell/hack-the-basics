# Module 02 Lab 01 - Map the Visible Network

---

> **Lab Objective**
>
> Use the Module 01 baseline to move from scope and target definition into saved scan artifacts, host notes, and a Module 03 service-footprinting queue.

| Module | Lab type | Main output |
|---|---|---|
| Module 02 - Map the Visible Network | Progressive module lab | scan plan, saved Nmap outputs, host tracker, follow-up queue |

---

## Scope Gate

Use only the course lab unless explicitly authorized otherwise.

| Asset | IP / range | Allowed in this lab |
|---|---:|---|
| `LAB-NET` | `192.168.57.0/24` | host discovery and scoped scanning |
| `GOAD-Mini-DC01` | `192.168.57.10` | TCP/UDP/service scanning |
| `GOAD-Mini-WS01` | `192.168.57.31` | TCP/UDP/service scanning |
| `META-TGT` | `192.168.57.25` | TCP/UDP/service scanning |

Do not scan networks outside the approved lab. Do not use decoys, fragmentation, spoofing, or stealth-oriented options unless a later scoped exercise explicitly asks for them.

---

## Scenario

You are standing in Kali WSL with access to the Module 01 lab.

Your job is to answer four questions:

1. Which hosts appear reachable from here?
2. Which ports respond in a way Nmap can classify?
3. What service clues are worth preserving?
4. What should Module 03 inspect next?

The lab should produce evidence, not just terminal output.

---

## Workspace

Use the shared workspace from Module 01.

```bash
M2SCAN=assessment-workspace/02-evidence/scans/m02
mkdir -p "$M2SCAN"
touch assessment-workspace/01-target-notes/host-tracking.md
touch assessment-workspace/03-analysis/follow-up-queue.md
```

Recommended paths:

```text
assessment-workspace/
  01-target-notes/
    host-tracking.md
  02-evidence/
    scans/m02/
  03-analysis/
    follow-up-queue.md
```

---

## Checkpoint A - Define the Scan Question

Complete this after Lesson 2.1.

Before scanning, write:

```text
Network position:

Approved scope:

First question:

Expected baseline:

Output path:
```

Example:

```text
Network position:
Kali WSL on the Windows host, scanning into VMware host-only LAB-NET.

Approved scope:
192.168.57.0/24.

First question:
Which expected course-lab hosts appear reachable from this position?

Expected baseline:
GOAD-Mini-DC01, GOAD-Mini-WS01, META-TGT.

Output path:
assessment-workspace/02-evidence/scans/m02/
```

The point is to make the scan intentional before it becomes technical.

---

## Checkpoint B - Discover Live Hosts

Complete this after Lesson 2.2.

Run a discovery pass and save it:

```bash
nmap -sn -oA "$M2SCAN"/lab-discovery-YYYY-MM-DD 192.168.57.0/24
```

Then create a reusable target list:

```bash
printf "192.168.57.10\n192.168.57.25\n192.168.57.31\n" > "$M2SCAN"/targets.txt
```

Only include hosts your evidence and lab notes support.

Update `host-tracking.md`:

```text
## Host Discovery - Module 02

Observed live hosts:

Expected but not observed:

Discovery method:

Uncertainty:
```

If an expected host is silent, do not immediately assume it is down. Record what discovery method you used and what else may need validation.

---

## Checkpoint C - Run TCP and UDP Triage

Complete this after Lesson 2.3.

Choose at least two hosts and run saved TCP triage scans.

```bash
nmap -sS -Pn --top-ports 1000 -oA "$M2SCAN"/meta-tcp-triage-YYYY-MM-DD 192.168.57.25
nmap -sS -Pn --top-ports 1000 -oA "$M2SCAN"/dc01-tcp-triage-YYYY-MM-DD 192.168.57.10
```

Run a small UDP check only where it supports a real question.

```bash
sudo nmap -sU -Pn --top-ports 25 -oA "$M2SCAN"/dc01-udp-triage-YYYY-MM-DD 192.168.57.10
```

Write a short interpretation:

```text
Observed:

Inference:

Ambiguity:

Validation needed:
```

The important habit is treating `open`, `closed`, and `filtered` as scanner labels based on probe behavior.

---

## Checkpoint D - Enrich the Most Important Hosts

Complete this after Lesson 2.4.

Choose one Linux-style target and one Windows/identity-style target.

```bash
nmap -sV -sC -Pn -p <open-ports> -oA "$M2SCAN"/meta-service-enriched-YYYY-MM-DD 192.168.57.25
nmap -sV -sC -Pn -p <open-ports> -oA "$M2SCAN"/dc01-service-enriched-YYYY-MM-DD 192.168.57.10
```

If the host exposes specific service families, run one focused script pass:

```bash
nmap --script smb-os-discovery,smb-security-mode -p 445 -oA "$M2SCAN"/dc01-smb-focused-YYYY-MM-DD 192.168.57.10
nmap --script http-title,ssl-cert -p 80,443 -oA "$M2SCAN"/meta-web-focused-YYYY-MM-DD 192.168.57.25
```

Capture:

- service names
- version clues
- hostnames
- certificate names
- script output that changes priority
- ambiguity that needs manual validation

---

## Checkpoint E - Build the Module 03 Handoff

Complete this after Lesson 2.5.

Update `host-tracking.md` with at least three host entries:

```text
## <host>

Observed:

Open or interesting ports:

Service clues:

Inference:

Validation needed:

Module 03 follow-up:
```

Update `follow-up-queue.md`:

```text
## Module 03 follow-up queue

1. Host:
   Services:
   Reason:
   Evidence path:

2. Host:
   Services:
   Reason:
   Evidence path:

3. Host:
   Services:
   Reason:
   Evidence path:
```

End with a close-out note:

```text
Module 02 close-out

Direct observations:

Inferences:

Unresolved ambiguity:

Most important saved artifacts:

Recommended Module 03 starting point:
```

---

## Validation Questions

Before leaving the module, answer:

1. Did every important scan use saved output?
2. Can you explain why `-Pn` was or was not used?
3. Can you explain which hosts appeared alive and how you know?
4. Can you explain at least one filtered or ambiguous result without overclaiming?
5. Did service enrichment change your understanding of any host?
6. Does Module 03 have enough evidence to begin service footprinting?

