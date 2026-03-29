<div align="center">

# Module 02 Field Reference

**Network Enumeration with Nmap**

*Phase I - Orientation and Surface Mapping*

</div>

---

> **🧭 Use This For**
>
> Fast scanning during labs, note-backed practice, and post-lesson review when you need a compact reminder of host discovery, scan types, enrichment, interpretation, and artifact capture.

| Best paired with | Main job | Assumption |
|---|---|---|
| Lesson 2.5 and the module lab | Help you move from quick triage to deliberate follow-up | Authorized lab use only |

| Preserve these outputs | Avoid these habits |
|---|---|
| live hosts, open ports, version clues, saved artifacts, next-step notes | blind `-Pn`, overtrusting silence, treating labels as certainty |

---

## Table of Contents

- [1. Quick Workflow](#1-quick-workflow)
- [2. Command Anatomy](#2-command-anatomy)
- [3. Target Definition](#3-target-definition)
- [4. Host Discovery](#4-host-discovery)
- [5. Port Scanning and States](#5-port-scanning-and-states)
- [6. Enrichment and NSE](#6-enrichment-and-nse)
- [7. Output and Artifact Capture](#7-output-and-artifact-capture)
- [8. Tuning and Troubleshooting](#8-tuning-and-troubleshooting)
- [9. Interpretation Rules](#9-interpretation-rules)
- [10. Minimal Note Template](#10-minimal-note-template)

---

## 1. Quick Workflow

> **🧠 Mental Model**
>
> discover -> scan -> enrich -> save -> interpret -> route the next step

### Fast first pass

```bash
nmap -sn <target-or-range>
nmap -sS -Pn --top-ports 1000 <target>
nmap -sV -sC -Pn -p <open-ports> <target>
```

### If UDP likely matters

```bash
nmap -sU -Pn --top-ports 50 <target>
nmap -sU -sV -Pn -p <interesting-udp-ports> <target>
```

### If the host is already known to be up

```bash
nmap -sS -Pn -p- <target>
nmap -sV -sC -Pn -p <open-ports> <target>
```

### Default operator rhythm

1. Define scope correctly.
2. Identify live hosts.
3. Run a fast TCP triage scan.
4. Expand only where the evidence justifies it.
5. Enrich open ports with `-sV` and targeted scripts.
6. Save results every time.
7. Manually validate high-value services.

---

## 2. Command Anatomy

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

## 3. Target Definition

### Common target forms

```bash
nmap 10.10.10.5
nmap 10.10.10.0/24
nmap 10.10.10.1-50
nmap -iL targets.txt
nmap 10.10.10.0/24 --exclude 10.10.10.1
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

## 4. Host Discovery

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
nmap -sn 10.10.10.0/24
nmap -sn -PS22,80,443 -PA80,443 10.10.10.0/24
nmap -Pn 10.10.10.15
```

### Quick reminders

- local subnet: ARP is often strong
- remote target: TCP probes may outperform ICMP-only logic
- `-Pn` is useful but expensive and easy to misuse
- discovery is always vantage-point dependent

---

## 5. Port Scanning and States

### Good defaults

| Goal | Pattern |
|---|---|
| Fast TCP triage | `nmap -sS --top-ports 1000 <target>` |
| Full TCP sweep | `nmap -sS -p- <target>` |
| Focused follow-up | `nmap -sV -sC -p <ports> <target>` |
| Quick UDP triage | `nmap -sU --top-ports 50 <target>` |

### Common scan types

| Scan | Flag | Use |
|---|---|---|
| SYN scan | `-sS` | Fast TCP scan with strong default utility |
| Connect scan | `-sT` | When raw packets are not available |
| UDP scan | `-sU` | Identify UDP exposure carefully |

### Port states

| State | Meaning |
|---|---|
| `open` | The port appears to accept traffic |
| `closed` | The port is reachable but not listening |
| `filtered` | Something likely interfered with visibility |
| `open|filtered` | Nmap cannot clearly distinguish the two |
| `closed|filtered` | Rare ambiguous state |
| `unfiltered` | Reachable, but not clearly open or closed in that scan context |

> **⚠️ Warning**
>
> A port state is a scanner label based on observed behavior, not a permanent truth about the host.

---

## 6. Enrichment and NSE

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

## 7. Output and Artifact Capture

### Useful output modes

```bash
nmap -oN scan.nmap <target>
nmap -oX scan.xml <target>
nmap -oA scans/triage <target>
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
- manual validation ideas

---

## 8. Tuning and Troubleshooting

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

## 9. Interpretation Rules

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

## 10. Minimal Note Template

```text
Target:
Network position:
Scan command:
Discovery result:
Open ports:
Version / service clues:
Ambiguities:
Next manual checks:
Saved artifacts:
```

---

<div align="center">

**Use Nmap to reduce uncertainty, not to pretend uncertainty is gone.**

</div>
