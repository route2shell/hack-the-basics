# Module 03 Service Role Worksheet

---

> **Worksheet Purpose**
>
> Use this worksheet to turn exposed services into host-role hypotheses, confidence levels, and follow-up decisions.

This worksheet is not a checklist of ports. It is a reasoning aid.

The goal is to make the learner write down how evidence changes their interpretation.

---

## Host Summary

| Host | Direct observations | Initial host-role hypothesis | Confidence | Validation needed |
|---|---|---|---|---|
| | | | Low / Medium / High | |
| | | | Low / Medium / High | |
| | | | Low / Medium / High | |

---

## Service Role Classification

| Host | Service | Role | Exact evidence | What it suggests | What it does not prove |
|---|---|---|---|---|---|
| | | naming / identity / storage / messaging / data / monitoring / management / web | | | |
| | | naming / identity / storage / messaging / data / monitoring / management / web | | | |
| | | naming / identity / storage / messaging / data / monitoring / management / web | | | |

---

## Captured Nouns

Exact nouns matter because they become search terms, note anchors, route-map entries, credential context, and later report evidence.

| Type | Value | Source | Why it matters |
|---|---|---|---|
| Hostname | | | |
| Domain / realm | | | |
| Share | | | |
| DNS record | | | |
| Certificate name | | | |
| Service version | | | |
| Instance name | | | |
| User or group clue | | | |

---

## Observation, Inference, Validation

Use this section for the top three interpretations from the module.

### Interpretation 1

```text
Observation:

Inference:

Confidence:

Validation needed:

Next workflow owner:
```

### Interpretation 2

```text
Observation:

Inference:

Confidence:

Validation needed:

Next workflow owner:
```

### Interpretation 3

```text
Observation:

Inference:

Confidence:

Validation needed:

Next workflow owner:
```

---

## Priority Queue

| Priority | Host | Service | Reason | Owner workflow | Evidence path |
|---:|---|---|---|---|---|
| 1 | | | | | |
| 2 | | | | | |
| 3 | | | | | |
| 4 | | | | | |
| 5 | | | | | |

---

## Worked Example

| Field | Example |
|---|---|
| Host | `192.168.57.10` |
| Direct observations | DNS, Kerberos, LDAP, SMB, and Windows RPC ports exposed |
| Initial host-role hypothesis | likely Windows identity infrastructure host, possibly domain controller |
| Confidence | Medium before LDAP/DNS naming validation; High after naming context confirms domain role |
| Validation needed | DNS records, LDAP rootDSE, SMB host/domain identity |
| Next workflow owner | Module 14 later for AD reasoning; Module 06 for credential context; Module 03 now for service interpretation |

Notice that the example does not say "domain controller confirmed" until the evidence supports it.

