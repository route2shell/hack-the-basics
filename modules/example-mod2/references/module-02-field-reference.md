# Module 02 Field Reference

---

> **Use This For**
>
> Fast support during Module 02 scanning. This reference keeps command patterns and interpretation reminders out of the main lesson path.

---

## Core Rhythm

```text
Define -> Discover -> Triage -> Enrich -> Preserve -> Interpret -> Route
```

Nmap is the instrument. The assessment product is saved evidence and a defensible next-step queue.

---

## Baseline Targets

| Host | IP | Why it matters |
|---|---:|---|
| `GOAD-Mini-DC01` | `192.168.57.10` | Windows identity and infrastructure-oriented exposure |
| `GOAD-Mini-WS01` | `192.168.57.31` | Windows workstation and management-surface comparison |
| `META-TGT` | `192.168.57.25` | Linux-style multi-service exposure |

---

## Workspace Setup

```bash
M2SCAN=assessment-workspace/02-evidence/scans/m02
mkdir -p "$M2SCAN"
```

Use readable basenames:

```text
lab-discovery-YYYY-MM-DD
meta-tcp-triage-YYYY-MM-DD
dc01-service-enriched-YYYY-MM-DD
ws01-rdp-focused-YYYY-MM-DD
targets.txt
```

---

## Command Anatomy

```bash
nmap [discovery] [scan type] [port selection] [enrichment] [output] <target>
```

| Piece | Question |
|---|---|
| discovery | should Nmap decide whether hosts are up first? |
| scan type | what kind of probe is being sent? |
| port selection | which ports are being asked about? |
| enrichment | what service context is being requested? |
| output | how will the evidence survive the terminal session? |

---

## Common Patterns

### Discovery

```bash
nmap -sn -oA "$M2SCAN"/lab-discovery-YYYY-MM-DD 192.168.57.0/24
```

### Fast TCP triage

```bash
nmap -sS -Pn --top-ports 1000 -oA "$M2SCAN"/meta-tcp-triage-YYYY-MM-DD 192.168.57.25
```

### Full TCP when justified

```bash
nmap -sS -Pn -p- -oA "$M2SCAN"/meta-fulltcp-YYYY-MM-DD 192.168.57.25
```

### Service enrichment

```bash
nmap -sV -sC -Pn -p <open-ports> -oA "$M2SCAN"/meta-service-enriched-YYYY-MM-DD 192.168.57.25
```

### Focused service checks

```bash
nmap --script smb-os-discovery,smb-security-mode -p 445 -oA "$M2SCAN"/dc01-smb-focused-YYYY-MM-DD 192.168.57.10
nmap --script http-title,ssl-cert -p 80,443 -oA "$M2SCAN"/meta-web-focused-YYYY-MM-DD 192.168.57.25
```

### UDP triage

```bash
sudo nmap -sU -Pn --top-ports 25 -oA "$M2SCAN"/dc01-udp-triage-YYYY-MM-DD 192.168.57.10
```

---

## Port State Interpretation

| State | Careful reading |
|---|---|
| `open` | the port responded as though a service accepts the probe |
| `closed` | the target/path responded as reachable but not listening |
| `filtered` | Nmap could not see a decisive answer, likely because something interfered |
| `open|filtered` | common with UDP and unusual probes; silence leaves ambiguity |
| `unfiltered` | reachable by the probe type, but not classified as open or closed |

Use careful language:

```text
appears open from Kali WSL
reported filtered in this scan
needs validation with focused follow-up
```

Avoid:

```text
firewall confirmed
service exploitable
host definitely down
```

---

## Strong Note Pattern

```text
Observed:

Inference:

Confidence:

Validation needed:

Evidence path:

Module 03 follow-up:
```

