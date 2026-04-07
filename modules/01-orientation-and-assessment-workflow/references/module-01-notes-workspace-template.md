# Module 01 Notes Workspace Template

---

> **Template Purpose**
>
> Use this template to build the assessment note workspace for the course baseline: one Windows 11 host, one Kali WSL attack platform, and three target VMs.

## Lab Asset Inventory

| Asset | Primary role | Suggested notes to preserve |
|---|---|---|
| Windows 11 host | operator platform running WSL2 and VMware | hostname, storage paths, VMware version, WSL notes |
| Kali WSL | attack and analysis platform | output paths, core tools, package changes, aliases, shared locations |
| `GOAD-Mini-DC01` | domain controller target | domain facts, IP, snapshot state, service observations |
| `GOAD-Mini-WS01` | domain-joined workstation target | IP, local/domain context notes, snapshot state |
| `META-TGT` | intentionally vulnerable Linux target | credentials, IP, exposed services, snapshot state |

### Topology prompts

```text
Windows host name:
WSL distro name:
VMware Workstation Pro version:
Host-only network(s):
Target subnet:
Snapshot naming convention:
Target NAT policy:
Where scan output will be saved:
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
    goad-instances.md
  01-target-notes/
    target-summary.md
    host-tracking.md
    ad-host-tracking.md
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
    goad-install-notes.md
    kali-wsl-baseline.md
```

---

## Lab Automation Planning

### Intended future pattern

| Area | Purpose |
|---|---|
| `initial-config/` | baseline scripts or notes that prepare a clean target state |
| `per-lab/` | later module or lab scripts that intentionally configure a target into a specific scenario |
| `snapshot-map.md` | records which clean snapshot to revert to before re-running a scenario |
| `kali-wsl-baseline.md` | records the trusted attack-platform baseline outside the VMware snapshot model |

### Planning prompts

```text
Kali WSL baseline note:
GOAD baseline snapshot names:
Metasploitable2 baseline snapshot name:
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
Environment or asset in use:
Question being answered:
Commands or actions:
Observation:
Inference:
Validation needed:
Next step:
```

---

## Design Notes

This template is meant to support the whole course, not just the first build.
