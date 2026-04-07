# Module 03 Gap Analysis And Revision Spec

---

> **🎯 Review Objective**
>
> Turn the Module 03 audit into a concrete, implementation-ready revision plan that realigns the module to the Module 01 baseline, the Module 02 workflow discipline, and the course goal of theory plus hands-on repetition.

| Area | Decision |
|---|---|
| Module | 03 - Service Footprinting and Common Infrastructure Enumeration |
| Verdict | Strong conceptually, but requires meaningful structural revision for self-paced practice flow |
| Main issue | Hands-on work is too generic, too weakly tied to the real baseline, and not accumulated through shared artifacts |
| Immediate implementation scope | `README.md`, `labs/module-03-lab-01-service-triage-and-follow-up-planning.md`, this revision spec |

| Primary sources used | Why they matter |
|---|---|
| `hack-the-basics/README.md` | course role and module handoff expectations |
| `hack-the-basics/hack-the-basics-implementation-blueprint.md` | Module 03 contract and required outputs |
| Module 01 and Module 02 READMEs and labs | baseline lab model and artifact workflow standard |
| `_misc/Footprinting - cheatsheet.pdf` | command coverage expectations for service-footprinting workflows |

---

## Overall Verdict

Module 03 already teaches the right mental model:

- turn open ports into service meaning
- turn service meaning into host-role reasoning
- turn host-role reasoning into triage and handoff

That part is sound.

What is weak is the delivery system for self-learners.

Module 02 established a better standard:

- every lesson has a concrete learner checkpoint
- the checkpoints write into the same shared workspace
- the final lab is synthesis, not the first real keyboard use

Module 03 does not yet preserve that pattern strongly enough.

The module should be revised so that:

1. the real Module 01 baseline is the default practice environment
2. the learner updates shared artifacts throughout the module
3. the standalone lab becomes the module spine rather than a placeholder
4. command coverage from the footprinting cheat sheet is preserved without pretending every service family exists live in the default baseline

---

## Findings

### Finding 1 - The module dropped the shared-workspace checkpoint pattern

- **Severity:** High
- **Category:** self-paced support
- **Issue:** Module 03 currently frames practice mostly as generic mini tasks and an end-of-module lab, instead of explicit per-lesson checkpoints that update the shared assessment workspace.
- **Learner impact:** A self-learner is more likely to read the module as interpretation theory instead of using it to build a reusable service-footprinting workflow.
- **Smallest sound fix:** Realign the README and lab so the learner uses one progressive module workflow after each lesson and writes into known workspace paths.

### Finding 2 - The module is not honest enough about what the baseline actually exposes

- **Severity:** High
- **Category:** hands-on realism
- **Issue:** The default Module 01 baseline clearly guarantees `GOAD-Mini-DC01`, `GOAD-Mini-WS01`, and `META-TGT`, but Module 03 practice prompts imply service families like SMTP, IMAP, POP3, NFS, MySQL, MSSQL, Oracle, SNMP, and IPMI as if they are generally available live.
- **Learner impact:** The learner either wastes time hunting for non-existent services or assumes they built the lab incorrectly.
- **Smallest sound fix:** Split command coverage into three modes:
  - required live baseline reps
  - optional live reps if the service exists in the learner's environment
  - reference-only or future-state commands that the module should teach, but not require live in the default baseline

### Finding 3 - The standalone lab is still a placeholder

- **Severity:** High
- **Category:** reference artifact / practice density
- **Issue:** The blueprint requires a real triage scenario, the README points learners to a module lab, but the standalone lab file is not yet implemented.
- **Learner impact:** Module navigation promises a core artifact that does not yet exist as a usable lab.
- **Smallest sound fix:** Move the real progressive workflow into the standalone lab file and use it throughout the module, not only after Lesson 3.4.

### Finding 4 - The service-role matrix is too thin to function as a serious worksheet

- **Severity:** Medium
- **Category:** support artifacts
- **Issue:** The matrix is useful as a compact reminder, but not yet strong enough as the central learner worksheet.
- **Learner impact:** The learner still has to invent their own note structure in the middle of a dense interpretation module.
- **Smallest sound fix:** In a later pass, revise the matrix into a true worksheet with worked examples, observation vs inference columns, and host-role correlation fields.

---

## Target State

By the end of the revised Module 03, a learner should be able to:

1. reopen their Module 02 saved scans and turn them into service-role and host-role hypotheses
2. run a small set of live service-aware checks against the real Module 01 baseline
3. capture exact nouns into the shared workspace
4. distinguish live required reps from optional or future-state service families
5. build a prioritized follow-up queue that cleanly hands into Modules 04, 06, 09, and later Windows / AD work

The module should feel like:

- theory and practice moving together
- one module-long analyst workshop
- a bridge between scanning and service-specific reasoning

---

## Revision Spec

### 1. README Realignment

Revise the module README so it explicitly includes:

- the Module 01 baseline hosts and subnet
- the shared workspace paths the learner should update
- a progressive sequence:
  - Lesson 3.1 -> Lab Checkpoint A
  - Lesson 3.2 -> Lab Checkpoint B
  - Lesson 3.3 -> Lab Checkpoint C
  - Lesson 3.4 -> Lab Checkpoint D
- a lesson-path table with required learner checkpoints
- a clear command coverage model:
  - baseline-live
  - optional-if-service-exists
  - reference-only or future-state

### 2. Standalone Lab Realignment

Replace the placeholder lab with a real progressive lab that:

- uses the Module 01 baseline by default
- reuses saved Module 02 scan artifacts
- contains four checkpoints mapped to the lesson sequence
- updates reusable artifacts inside `assessment-workspace/`
- ends with a prioritized follow-up queue in `03-analysis/follow-up-queue.md`

### 3. Lesson Follow-Up Revisions

These are not part of the current implementation pass, but should happen next:

- update each lesson's mini practice task into a required learner checkpoint
- reference the same workspace paths named in the README and lab
- explicitly mark which commands are:
  - required live now
  - optional if the learner has the service
  - held for later-state or reference-only use

### 4. Support Artifact Follow-Up Revisions

Also not part of the current implementation pass:

- upgrade the service-role matrix into a real worksheet
- refresh the reference cheat sheet so it matches the baseline-live vs optional vs reference-only model
- add a curated evidence pack only if we decide Module 03 should require service families that are not in the baseline

---

## Command Coverage Map

The footprinting cheat sheet expands the command coverage the module should preserve.
That does **not** mean every command must be a required live exercise in the default baseline.

The right split is below.

| Service family / workflow | Command coverage to preserve | Practice mode in Module 03 | Notes |
|---|---|---|---|
| Public recon and external discovery | `curl -s https://crt.sh/?q=<target-domain>&output=json | jq .`, `shodan host <ip>` | Reference-only in the default lab | Useful concepts, but not required against the internal baseline |
| FTP | `ftp`, `nc -nv <host> 21`, `telnet <host> 21`, `openssl s_client -connect <host>:21 -starttls ftp`, `wget -m --no-passive ftp://...` | Required live on `META-TGT` where appropriate | Good baseline Linux repetition |
| SMB / RPC | `smbclient -N -L`, `smbclient //<host>/<share>`, `rpcclient -U ""`, `samrdump.py`, `smbmap -H`, `crackmapexec smb --shares`, `enum4linux-ng.py -A` | Required live where tools are available; otherwise partial live plus reference | Core to `GOAD-Mini-DC01` and `GOAD-Mini-WS01` reasoning |
| NFS | `showmount -e`, `mount -t nfs`, `umount` | Optional-if-service-exists | Do not require in the default baseline unless later-state services are added |
| DNS | `dig ns`, `dig any`, `dig axfr`, `dnsenum` | Required live for simple queries; zone-transfer brute work optional | Should stay bounded to enumeration and naming clues |
| SMTP / IMAP / POP3 | `telnet <host> 25`, `curl -k imaps://... --user ...`, `openssl s_client -connect <host>:993`, `openssl s_client -connect <host>:995` | Optional-if-service-exists or reference-only | Preserve the workflow, but do not pretend the default baseline exposes mail by default |
| SNMP | `snmpwalk -v2c -c ...`, `onesixtyone`, `braa` | Optional-if-service-exists or reference-only | Strong service family, but not a required default-baseline live rep yet |
| MySQL | `mysql -u <user> -p<password> -h <host>` | Optional-if-service-exists or reference-only | Keep in command coverage and lesson framing |
| MSSQL | `mssqlclient.py ... -windows-auth` | Optional-if-service-exists or reference-only | Important handoff family for later modules |
| IPMI | `msfconsole` auxiliary `scanner/ipmi/ipmi_version`, `scanner/ipmi/ipmi_dumphashes` | Reference-only unless explicitly added to a later lab state | Mention, but do not require in the default baseline |
| Linux remote management | `ssh-audit.py`, `ssh`, `ssh -i`, `ssh -o PreferredAuthentications=password` | Required live where practical on `META-TGT` | Great for banner, identity, and management-surface reasoning |
| Windows remote management | `rdp-sec-check.pl`, `xfreerdp`, `evil-winrm`, `wmiexec.py` | Required only where the service is known to exist and the learner can test legally; otherwise optional / reference | RDP on `GOAD-Mini-WS01` is relevant to the baseline; WinRM / WMI should stay honest |
| Oracle TNS | `odat.py all`, `sqlplus`, `odat.py utlfile ... --putFile ...` | Reference-only unless explicitly added to a later service state | Keep coverage, but do not require live use now |

---

## Concrete File Changes

### Implement Now

- `modules/03-service-footprinting-and-common-infrastructure-enumeration/README.md`
  - add working baseline section
  - add shared workspace section
  - change module flow from end-loaded lab to progressive checkpoints
  - make command coverage mode explicit

- `modules/03-service-footprinting-and-common-infrastructure-enumeration/labs/module-03-lab-01-service-triage-and-follow-up-planning.md`
  - replace placeholder with full progressive lab
  - tie each checkpoint to the lesson sequence
  - define exact artifacts and workspace paths
  - end with a follow-up queue and workflow handoff

- `modules/03-service-footprinting-and-common-infrastructure-enumeration/reviews/module-03-gap-analysis.md`
  - replace pending note with this revision spec

### Defer To Next Pass

- lesson-body checkpoint rewrites
- service-role matrix rewrite
- reference cheat sheet refresh
- curated evidence pack, if we decide to require non-baseline service families

---

## Success Criteria For The Realigned Module

The Module 03 realignment is successful when all of the following are true:

- the learner knows exactly which hosts to use first
- the learner knows which artifacts to update after each lesson
- the standalone lab is usable during the module, not only after it
- the learner can complete meaningful live reps against the default baseline
- command coverage from the footprinting cheat sheet is preserved honestly
- the module ends with a triage queue that naturally hands into later workflows

If those are true, Module 03 will feel much closer to the Module 02 quality bar while preserving its stronger infrastructure-reasoning focus.
