<div align="center">

# Module 02 Field Reference

**Network Enumeration with Nmap**

*Phase I - Orientation and Surface Mapping*

</div>

---

> **🧭 Use This For**
>
> Fast scanning during Module 02 checkpoints, the module lab, and later review when you need compact reminders for host discovery, scan types, enrichment, artifact capture, and handoff thinking.

| Best paired with | Main job | Assumption |
|---|---|---|
| Lesson 2.5 and Module 02 Lab 01 | Help you move from discovery to saved evidence to next-step routing | Kali WSL scanning the Module 01 baseline lab |

| Preserve these outputs | Avoid these habits |
|---|---|
| live hosts, open ports, version clues, saved artifacts, host notes, next-step queue | blind `-Pn`, overtrusting silence, treating labels as certainty, saving results outside the shared workspace |

---

## Table of Contents

- [1. Quick Workflow](#1-quick-workflow)
- [2. Baseline Targets](#2-baseline-targets)
- [3. Command Anatomy](#3-command-anatomy)
- [4. Target Definition](#4-target-definition)
- [5. Host Discovery](#5-host-discovery)
- [6. Port Scanning and States](#6-port-scanning-and-states)
- [7. Enrichment and NSE](#7-enrichment-and-nse)
- [8. Output and Artifact Capture](#8-output-and-artifact-capture)
- [9. Tuning and Troubleshooting](#9-tuning-and-troubleshooting)
- [10. Interpretation Rules](#10-interpretation-rules)
- [11. Minimal Note Template](#11-minimal-note-template)

---

## 1. Quick Workflow

> **🧠 Mental Model**
>
> define -> discover -> triage -> enrich -> save -> interpret -> route the next step

### Fast first pass

```bash
M2SCAN=assessment-workspace/02-evidence/scans/m02
mkdir -p "$M2SCAN"
nmap -sn -oA "$M2SCAN"/lab-discovery-YYYY-MM-DD 192.168.57.0/24
nmap -sS -Pn --top-ports 1000 -oA "$M2SCAN"/meta-triage-YYYY-MM-DD 192.168.57.25
nmap -sV -sC -Pn -p <open-ports> -oA "$M2SCAN"/meta-enriched-YYYY-MM-DD 192.168.57.25
```

### If UDP likely matters

```bash
sudo nmap -sU -Pn --top-ports 25 -oA "$M2SCAN"/dc01-udp-YYYY-MM-DD 192.168.57.10
sudo nmap -sU -sV -Pn -p <interesting-udp-ports> -oA "$M2SCAN"/dc01-udp-focused-YYYY-MM-DD 192.168.57.10
```

### If the host is already known to be up

```bash
nmap -sS -Pn -p- -oA "$M2SCAN"/meta-fulltcp-YYYY-MM-DD 192.168.57.25
nmap -sV -sC -Pn -p <open-ports> -oA "$M2SCAN"/meta-service-pass-YYYY-MM-DD 192.168.57.25
```

### Default operator rhythm

1. Define scope correctly.
2. Identify live hosts.
3. Run a fast TCP triage scan.
4. Expand only where the evidence justifies it.
5. Enrich open ports with `-sV` and targeted scripts.
6. Save results every time.
7. Update host notes and the follow-up queue.

---

## 2. Baseline Targets

| Asset | IP | Why it is useful in Module 02 |
|---|---|---|
| `GOAD-Mini-DC01` | `192.168.57.10` | Strong Windows and identity-oriented discovery target |
| `META-TGT` | `192.168.57.25` | Strong Linux and multi-service exposure target |
| `GOAD-Mini-WS01` | `192.168.57.31` | Helpful for Windows workstation visibility and comparison |

---

## 3. Command Anatomy

```bash
nmap [host-discovery] [scan-type] [port-selection] [enrichment] [timing] [output] <target>
```

| Part | Question it answers |
|---|---|
| Host discovery | Is the target up from here? |
| Scan type | How am I probing the ports? |
| Port selection | Which ports am I asking about? |
| Enrichment | What more can I learn from open ports? |
| Timing | How fast or careful should I be? |
| Output | How will I save this for later? |

---

## 4. Target Definition

### Common target forms

```bash
nmap 192.168.57.25
nmap 192.168.57.0/24
nmap 192.168.57.10,25,31
nmap -iL assessment-workspace/02-evidence/scans/m02/targets.txt
nmap 192.168.57.0/24 --exclude 192.168.57.31
```

### Helpful DNS controls

```bash
nmap -n <target>
nmap -R <target>
```

> **🔍 Interpretation**
>
> Good target definition reduces wasted scanning and makes later artifacts easier to compare.

---

## 5. Host Discovery

| Mode | Meaning |
|---|---|
| `-sn` | Host discovery only |
| `-Pn` | Skip discovery; treat hosts as up |
| `-sL` | List targets only |

| Probe | Meaning |
|---|---|
| `-PR` | ARP ping on local Ethernet |
| `-PE` | ICMP echo |
| `-PS<ports>` | TCP SYN discovery |
| `-PA<ports>` | TCP ACK discovery |
| `-PU<ports>` | UDP discovery |

### Examples

```bash
nmap -sn 192.168.57.0/24
nmap -sn -PS22,80,445 -PA80,445 192.168.57.0/24
nmap -Pn 192.168.57.25
```

### Quick reminders

- local subnet: ARP is often strong
- remote target: TCP probes may outperform ICMP-only logic
- `-Pn` is useful but expensive and easy to misuse
- discovery is always vantage-point dependent

---

## 6. Port Scanning and States

### Good defaults

| Goal | Pattern |
|---|---|
| Fast TCP triage | `nmap -sS --top-ports 1000 <target>` |
| Full TCP sweep | `nmap -sS -p- <target>` |
| Focused follow-up | `nmap -sV -sC -p <ports> <target>` |
| Quick UDP triage | `sudo nmap -sU --top-ports 25 <target>` |

### Common scan types

| Scan | Flag | Use |
|---|---|---|
| SYN scan | `-sS` | Fast TCP scan with strong default utility |
| Connect scan | `-sT` | When raw packets are not available |
| UDP scan | `-sU` | Identify UDP exposure carefully |
| ACK scan | `-sA` | Test whether the path looks filtered or reachable enough to return a reset |
| NULL scan | `-sN` | Compare how an unusual no-flags probe behaves |
| FIN scan | `-sF` | Test whether a FIN probe changes what the target reveals |
| Xmas scan | `-sX` | Compare behavior with a multi-flag unusual TCP probe |

### Quick state reminders for alternate scans

| Scan | Common interpretation pattern |
|---|---|
| `-sA` | Often distinguishes `filtered` from `unfiltered`, not `open` from `closed` |
| `-sN`, `-sF`, `-sX` | Often produce `closed` or `open\|filtered`; interpretation depends heavily on target and middleboxes |

> **📝 Note**
>
> Alternate scan types are best used to clarify ambiguity or filtering, not as magical stealth settings.

### Port states

| State | Meaning |
|---|---|
| `open` | The port appears to accept traffic |
| `closed` | The port is reachable but not listening |
| `filtered` | Something likely interfered with visibility |
| `open|filtered` | Nmap cannot clearly distinguish the two |
| `closed|filtered` | Rare ambiguous state |
| `unfiltered` | Reachable, but not clearly open or closed in that scan context |

### Quiet scanning mindset

| Goal | Pattern |
|---|---|
| Reduce extra lookup traffic | `nmap -n <target>` |
| Start with a smaller TCP question | `nmap -sS --top-ports 100 <target>` |
| Slow the pace deliberately | `nmap -T2 <target>` |
| Re-check filtering with a focused scan | `nmap -sA -p <ports> <target>` |

### Advanced awareness, not default workflow

| Option | What it does | Why it is not a default |
|---|---|---|
| `-f` | Fragment packets | Can complicate interpretation and does not guarantee invisibility |
| `-D` | Use decoys | Changes traffic shape but does not replace scope discipline or clean evidence |

> **⚠️ Warning**
>
> A port state is a scanner label based on observed behavior, not a permanent truth about the host.

---

## 7. Enrichment and NSE

### Common enrichment patterns

```bash
nmap -sV -sC -Pn -p <ports> <target>
nmap -O --traceroute <target>
nmap --script <script-name> -p <ports> <target>
```

| Area | What it gives you |
|---|---|
| `-sV` | service and version clues |
| `-sC` | useful default scripts |
| `-O` | OS inference |
| `--traceroute` | network path context |
| selective NSE | protocol-aware deeper checks |

### NSE reminder

- use scripts to deepen understanding
- do not treat scripts like a slot machine
- validate important findings manually

---

## 8. Output and Artifact Capture

### Useful output modes

```bash
nmap -oN scan.nmap <target>
nmap -oX scan.xml <target>
nmap -oA "$M2SCAN"/<basename> <target>
```

| Output | Best use |
|---|---|
| `-oN` | readable notes for humans |
| `-oX` | structured parsing and reuse |
| `-oA` | best default habit for saving everything together |

### Save alongside the scan

- the exact command used
- your network position or pivot context
- notable open ports
- uncertainty notes
- host-tracking updates
- follow-up queue entries

### Default note destinations

- `assessment-workspace/01-target-notes/host-tracking.md`
- `assessment-workspace/03-analysis/follow-up-queue.md`

---

## 9. Tuning and Troubleshooting

### Four main tuning levers

| Lever | Why it matters |
|---|---|
| Port selection | Scope usually matters more than aggression |
| Timing templates | Pace affects reliability and visibility |
| Retries / timeouts | Patience can change the result |
| Name resolution / discovery choices | Noise control matters |

### Common troubleshooting patterns

| Problem | First adjustment |
|---|---|
| Discovery says host is down | Try `-Pn` or explicit discovery probes |
| Results feel incomplete | widen ports, slow down, save output |
| UDP feels empty | narrow focus and enrich specific ports |
| Output is hard to compare | use `-oA` and standardize filenames |

---

## 10. Interpretation Rules

> **🔍 Interpretation**
>
> Use these as fast reminders when reading scan output.

- silence is ambiguous
- `open` is not the same as safe
- `closed` still proves reachability
- `filtered` means uncertainty, not absence
- service detection is evidence, not magic
- the same host can look different from different positions
- every useful scan should end with a follow-up question

---

## 11. Minimal Note Template

```text
Target:
Network position:
Scan command:
Observation:
Inference:
Validation needed:
Saved artifacts:
Next module or workflow owner:
```

---

<div align="center">

**Use Nmap to reduce uncertainty, not to pretend uncertainty is gone.**

</div>
