# Module 01 Notes Workspace Template

---

> **📝 Template Purpose**
>
> Use this template to build both the assessment note workspace and the VMware lab inventory that the course will rely on from Module 01 onward. It also reserves a place for the future baseline configure scripts and per-lab setup scripts the course can grow into later.

## VMware Lab Inventory

| VM | Primary role | Suggested notes to preserve |
|---|---|---|
| Kali | attack and analysis workstation | IPs, interface setup, tool changes, shared folders |
| Metasploit / Metasploitable practice target | intentionally vulnerable early target | snapshot state, services enabled, creds, network placement |
| Basic Linux VM | configurable Linux service and privesc target | distro, users, service roles, later lab changes |
| Windows 11 VM | later Windows, auth, and AD-adjacent work | local users, network role, snapshot history |

### Lab topology prompts

```text
VMware Workstation Pro version:
Host-only network(s):
NAT network(s):
Isolated segments:
Snapshot naming convention:
Shared-folder policy:
Credential storage approach:
```

---

## Assessment Note Workspace Structure

```text
assessment-workspace/
  00-admin/
    scope.md
    rules-of-engagement.md
    vm-inventory.md
    network-notes.md
  01-target-notes/
    target-summary.md
    host-tracking.md
  02-evidence/
    scans/
    screenshots/
    outputs/
  03-analysis/
    observations.md
    hypotheses.md
    follow-up-queue.md
  04-reporting/
    findings-drafts.md
    timeline.md
  05-lab-automation/
    initial-config/
    per-lab/
    snapshot-map.md
```

---

## Lab Automation Planning

### Intended future pattern

| Area | Purpose |
|---|---|
| `initial-config/` | baseline scripts that prepare a clean VM for the course |
| `per-lab/` | later module or lab scripts that intentionally configure a VM into a specific scenario |
| `snapshot-map.md` | records which clean snapshot to revert to before re-running a setup script |

### Planning prompts

```text
Kali baseline script name:
Practice target baseline script name:
Linux baseline script name:
Windows baseline script name:
Per-lab script naming rule:
Which snapshot should each script assume?
Reset workflow before a new lab:
```

---

## Minimal Daily Note Skeleton

```text
Date:
Current module / lesson:
Assessment phase:
Environment or VM in use:
Question being answered:
Commands or actions:
Observation:
Inference:
Validation needed:
Next step:
```

---

## Design Notes

This template is meant to be practical rather than decorative. It should support the whole course, not just the first lab.
