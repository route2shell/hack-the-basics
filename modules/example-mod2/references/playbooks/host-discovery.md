# Host Discovery Playbook - Module 02

---

> **Playbook Role**
>
> Use this when deciding how to find live hosts without confusing silence for absence.

Host discovery answers a visibility question:

> Which hosts appear alive from this network position using this discovery method?

It does not prove that every silent address is empty.

---

## First Questions

Ask:

1. What scope is approved?
2. What network position am I scanning from?
3. Is this local subnet discovery or remote discovery?
4. Which discovery methods are likely to work here?
5. What output path will preserve the result?

---

## Commands

```bash
nmap -sn 192.168.57.0/24
nmap -sn -oA "$M2SCAN"/lab-discovery-YYYY-MM-DD 192.168.57.0/24
nmap -sL 192.168.57.0/24
```

For remote or filtered contexts:

```bash
nmap -sn -PS22,80,445 -PA80,445 <target-range>
```

Use `-Pn` only when you deliberately want to skip discovery:

```bash
nmap -Pn <target>
```

---

## Interpretation

If a host appears up, record what evidence caused that conclusion if Nmap reports it.

If a host is silent, record the uncertainty:

```text
Host not reported up by this discovery method. This may mean down, filtered, or not responsive to selected probes. Validate if expected by baseline.
```

---

## Strong Note Example

```text
Observed:
Discovery sweep against 192.168.57.0/24 reported .10, .25, and .31 up from Kali WSL.

Inference:
The expected baseline hosts appear reachable from the current network position.

Validation needed:
Run TCP triage against each host and preserve output.

Evidence path:
assessment-workspace/02-evidence/scans/m02/lab-discovery-2026-05-04.nmap
```

