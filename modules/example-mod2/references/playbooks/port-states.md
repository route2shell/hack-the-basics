# Port State Playbook - Module 02

---

> **Playbook Role**
>
> Use this when interpreting TCP, UDP, and ambiguous Nmap state labels.

Port states are scanner conclusions based on probe behavior. They are useful, but they are not permanent truths about the host.

---

## Core Question

Ask:

> When this probe was sent from this position to this port, what response pattern did Nmap observe?

That framing prevents overclaiming.

---

## Common TCP Pattern

| Observed behavior | Common label | Careful meaning |
|---|---|---|
| target responds as though it accepts a TCP conversation | `open` | service appears reachable |
| target rejects the attempt | `closed` | host/path reachable, no listener on that port |
| no decisive response or filtering message | `filtered` | visibility is blocked or unclear |

---

## UDP Pattern

UDP is more ambiguous because silence can mean several things.

| Result | Careful reading |
|---|---|
| UDP response | strong clue that a service is reachable |
| ICMP port unreachable | often supports `closed` |
| silence | may be open, filtered, dropped, rate-limited, or application-silent |

This is why UDP should be narrower and more deliberate in beginner workflows.

---

## Scan Types

```bash
nmap -sS <target>
nmap -sT <target>
sudo nmap -sU <target>
nmap -sA <target>
```

Interpretation:

- `-sS` is a strong default TCP triage scan when available.
- `-sT` is useful when raw-packet scanning is unavailable.
- `-sU` requires patience and careful interpretation.
- `-sA` is often about filtering behavior, not discovering open services.

---

## Strong Note Example

```text
Observed:
TCP triage on 192.168.57.25 reported 21, 22, and 80 open. Several other ports returned closed. No large filtered pattern observed.

Inference:
The host appears reachable and exposes FTP, SSH, and HTTP from Kali WSL.

Validation needed:
Run service detection on the open ports and route FTP/HTTP into Module 03 and Module 04 follow-up.
```

