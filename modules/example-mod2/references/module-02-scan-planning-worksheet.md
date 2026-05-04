# Module 02 Scan Planning Worksheet

---

> **Worksheet Purpose**
>
> Use this worksheet to define scan intent, preserve scope, choose target forms, and connect Nmap output to notes and follow-up decisions.

This worksheet should be updated throughout Module 02, not filled once and forgotten.

---

## Assessment Context

| Prompt | Your entry |
|---|---|
| Current lab state | |
| Network position | |
| Scope source | |
| Approved target range | |
| Why this scan matters now | |
| Output root | |

---

## Baseline Check

| Item | Expected | Your entry |
|---|---|---|
| Attack platform | Kali WSL | |
| Target subnet | `192.168.57.0/24` | |
| Windows infrastructure host | `GOAD-Mini-DC01 / 192.168.57.10` | |
| Windows workstation | `GOAD-Mini-WS01 / 192.168.57.31` | |
| Linux target | `META-TGT / 192.168.57.25` | |
| Workspace | `assessment-workspace/` | |

If any assumption is wrong, document the difference before scanning.

---

## Scan Question Planner

| Stage | Question | Target form | Planned command | Output basename |
|---|---|---|---|---|
| Discovery | Which hosts appear alive? | | | |
| TCP triage | Which TCP ports respond? | | | |
| UDP triage | Which UDP ports deserve attention? | | | |
| Enrichment | What service clues appear? | | | |
| Focused follow-up | Which service family needs sharper evidence? | | | |

---

## Observation, Inference, Validation

Use after each meaningful scan.

```text
Scan:

Evidence path:

Observation:

Inference:

Confidence:

Validation needed:

Next step:
```

---

## Host Tracker Entry

```text
## <host>

Status:

Discovery evidence:

Open or interesting ports:

Service clues:

Host-role inference:

Validation needed:

Module 03 follow-up:
```

---

## Close-Out Checklist

- [ ] Scope and network position are recorded.
- [ ] Discovery output is saved.
- [ ] Live-host set is preserved.
- [ ] TCP triage output is saved.
- [ ] UDP was used only where it served a real question.
- [ ] Enrichment output is saved.
- [ ] Host tracker is updated.
- [ ] Follow-up queue is updated for Module 03.
- [ ] Observations and inferences are separated.

