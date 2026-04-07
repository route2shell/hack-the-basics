# Module 03 Lab 01 - Service Triage And Follow-Up Planning

---

> **🛠 Lab Objective**
>
> Turn the real Module 01 baseline and the saved Module 02 scan evidence into service-role notes, host-role hypotheses, captured nouns, and a prioritized follow-up queue.

| Module | Position | Main output |
|---|---|---|
| Module 03 - Service Footprinting and Common Infrastructure Enumeration | Progressive module lab | host-role notes, service evidence notes, triage queue, workflow routing decisions |

| Prerequisites | Use while working |
|---|---|
| Module 01 baseline, Module 02 saved scans, Lessons 3.1-3.4 | [field reference](../references/module-03-reference-cheat-sheet.md), [service role matrix](../references/module-03-service-role-matrix.md) |

---

## How To Use This Lab

This is not a lab to open only after Lesson 3.4.

Use it progressively:

1. complete Checkpoint A after Lesson 3.1
2. complete Checkpoint B after Lesson 3.2
3. complete Checkpoint C after Lesson 3.3
4. complete Checkpoint D after Lesson 3.4

> **🧠 Mental Model**
>
> Module 02 taught us to save scan evidence.
> Module 03 should now teach us to read that evidence like infrastructure clues, validate a few of those clues with small live checks, and route the right next step.

---

## Lab Baseline

Use the default course baseline unless you have deliberately added more service states.

| Role | Host | IP | Why it matters here |
|---|---|---|---|
| Windows infrastructure host | `GOAD-Mini-DC01` | `192.168.57.10` | naming, identity, SMB, and Windows-infrastructure clues |
| Windows workstation | `GOAD-Mini-WS01` | `192.168.57.31` | SMB and RDP-oriented workstation or host-role clues |
| Linux target | `META-TGT` | `192.168.57.25` | FTP, SSH, HTTP, and early Linux service reasoning |

If your environment exposes additional services such as SNMP, MySQL, SMTP, or Oracle, you may extend this lab.
But the default required flow should still work against the baseline above.

---

## Workspace Outputs

Write into the same `assessment-workspace/` used in Modules 01 and 02.

Recommended working locations:

- `assessment-workspace/01-target-notes/host-tracking.md`
- `assessment-workspace/02-evidence/scans/module-02/`
- `assessment-workspace/02-evidence/services/module-03/`
- `assessment-workspace/03-analysis/module-03-host-role-notes.md`
- `assessment-workspace/03-analysis/follow-up-queue.md`

### By the end of the module, you should have:

- one host-role note for each baseline host
- captured nouns from live or saved service evidence
- a record of which service families were live, optional, or reference-only
- a prioritized follow-up queue with owning workflows

---

## Practice Model

| Mode | What it means |
|---|---|
| **Required live** | the default baseline supports this check and the learner should perform it |
| **Optional live** | run it if the service exists in your environment |
| **Reference-only** | preserve the command and workflow knowledge, but do not require it live in the default baseline |

| Family | Examples | Mode |
|---|---|---|
| FTP | `ftp`, `nc -nv`, `telnet`, `openssl s_client -starttls ftp` | required live on `META-TGT` where practical |
| SMB / RPC | `smbclient`, `rpcclient`, `smbmap`, `crackmapexec smb`, `enum4linux-ng.py` | required live where tools are available |
| DNS / naming | `dig`, `host` | required live |
| LDAP / identity | `ldapsearch`, `nmap --script ldap-rootdse` | required live |
| Linux management | `ssh`, `ssh -i`, `ssh -o PreferredAuthentications=password`, `ssh-audit.py` | required live where practical |
| Windows management | `rdp-sec-check.pl`, `xfreerdp`, `evil-winrm`, `wmiexec.py` | optional live or reference-only depending on exposed services and safe access |
| Mail, NFS, SNMP, databases, Oracle, IPMI, public recon | `telnet 25`, `showmount`, `snmpwalk`, `mysql`, `mssqlclient.py`, `odat.py`, `crt.sh`, `shodan` | optional or reference-only in the default baseline |

---

## Checkpoint A - Lesson 3.1

> **🎯 Goal**
>
> Turn saved scan evidence into service-role and host-role hypotheses before running any new tool-heavy follow-up.

### Input

Use the saved Module 02 evidence first.

Expected sources:

- `assessment-workspace/02-evidence/scans/module-02/`
- `assessment-workspace/01-target-notes/host-tracking.md`

### Task

For each baseline host:

1. review the saved Module 02 scan outputs
2. list the exposed services
3. classify each service by role:
   - naming
   - identity
   - storage
   - messaging
   - management
   - monitoring
   - data
4. write one host-role hypothesis
5. separate observation from inference

### Suggested note table

| Host | Visible services | Service roles | Host-role hypothesis | What still needs validation |
|---|---|---|---|---|
| `GOAD-Mini-DC01` | `53`, `88`, `135`, `389`, `445` | naming, identity, SMB context | likely Windows identity / infrastructure host | what exact directory and naming details are exposed |
| `GOAD-Mini-WS01` | `135`, `139`, `445`, `3389` | SMB context, management | likely Windows workstation or managed Windows service host | whether it reveals stronger naming or domain clues |
| `META-TGT` | `21`, `22`, `23`, `80` | file transfer, management, web | likely Linux or lab-style mixed service target | what hostnames, banners, and auth posture clues appear |

### Required artifact updates

- create or update `assessment-workspace/03-analysis/module-03-host-role-notes.md`
- add a short host-role entry for each baseline host

---

## Checkpoint B - Lesson 3.2

> **🎯 Goal**
>
> Run small live checks for file, naming, and related service clues without replacing analyst judgment with noisy output.

### Suggested live checks

Run only the checks that fit your baseline and tool availability.

#### Naming and identity on `GOAD-Mini-DC01`

```bash
host 192.168.57.10
dig @192.168.57.10 -x 192.168.57.10
nmap --script ldap-rootdse -p 389 192.168.57.10
ldapsearch -x -H ldap://192.168.57.10 -s base namingcontexts defaultnamingcontext
```

#### SMB and file-context checks on the Windows hosts

```bash
smbclient -N -L //192.168.57.10/
smbclient -N -L //192.168.57.31/
rpcclient -U "" -N 192.168.57.10
```

#### FTP checks on `META-TGT`

```bash
nc -nv 192.168.57.25 21
telnet 192.168.57.25 21
ftp 192.168.57.25
```

### What to capture

For every useful result, record:

1. the exact command or first check
2. the exact nouns it revealed
3. what role clue it strengthened
4. what still needs validation

### If a family is not live in your baseline

If you do not have live mail or NFS services:

- mark them as `reference-only in current baseline`
- use the lesson examples to practice interpretation
- do not fake a live exercise that your lab does not actually support

### Required artifact updates

- add captured nouns and notes to `assessment-workspace/03-analysis/module-03-host-role-notes.md`
- save any new command output in `assessment-workspace/02-evidence/services/module-03/`

---

## Checkpoint C - Lesson 3.3

> **🎯 Goal**
>
> Use a few high-signal management and infrastructure checks to decide which later workflows deserve attention first.

### Suggested live checks

#### Windows management clues on `GOAD-Mini-WS01`

```bash
nmap --script rdp-ntlm-info,ssl-cert -p 3389 192.168.57.31
```

#### Identity and service context on `GOAD-Mini-DC01`

```bash
nmap -sV -p 53,88,135,389,445 192.168.57.10
```

#### Linux management on `META-TGT`

```bash
ssh <user>@192.168.57.25
ssh -o PreferredAuthentications=password <user>@192.168.57.25
```

If `ssh-audit.py` is available in your toolset, it is also appropriate here.

### Optional and reference-only families

Use this checkpoint to classify the command families from the footprinting cheat sheet into:

- `live in my baseline now`
- `optional if I add or discover the service`
- `reference-only for the current default baseline`

Examples that usually remain optional or reference-only here:

- `snmpwalk`
- `onesixtyone`
- `braa`
- `mysql`
- `mssqlclient.py`
- `odat.py`
- IPMI Metasploit modules

### Required artifact updates

Create or extend a section in `assessment-workspace/03-analysis/module-03-host-role-notes.md` that records:

- which families were confirmed live
- which families were not present
- which commands should be preserved for later modules or later service states

---

## Checkpoint D - Lesson 3.4

> **🎯 Goal**
>
> Convert everything gathered in this module into a ranked, workflow-owned follow-up queue.

### Build the queue

Using the notes from Checkpoints A-C, produce a ranked queue for at least the three baseline hosts.

### Questions to answer for each entry

1. Why does this host or service cluster matter?
2. What direct observation supports that?
3. What is the main inference?
4. What still needs validation?
5. Which later workflow owns the next step?

### Suggested queue format

| Priority | Host / Service | Why it matters | Direct observation | Next question | Owning workflow |
|---|---|---|---|---|---|
| 1 | `GOAD-Mini-DC01` / DNS + LDAP + Kerberos + SMB | identity and trust relevance | naming and directory-related ports plus directory checks respond | what stronger directory and naming context can be confirmed next? | Windows / credential / later AD path |
| 2 | `GOAD-Mini-WS01` / SMB + RDP | Windows host with management relevance | SMB and RDP clues visible from the baseline | what host naming, auth, and management clues are strongest? | Windows / credential / foothold-adjacent path |
| 3 | `META-TGT` / FTP + SSH + HTTP | mixed Linux service target with multiple follow-up directions | FTP, SSH, and web exposure are all visible | which service offers the cleanest next-step validation first? | common service or web handoff |

### Required artifact updates

- update `assessment-workspace/03-analysis/follow-up-queue.md`
- ensure each queue entry has an owner workflow, not just a priority label

---

## What A Strong Module Close-Out Looks Like

By the end of this lab, the learner should be able to explain:

- what each baseline host most likely is
- which clues are direct observations and which are inference
- which commands were actually useful live in the current baseline
- which service families are covered conceptually but not required live yet
- what should happen next in Modules 04, 06, 09, and later Windows / AD work

> **💡 Tip**
>
> If another operator could open your `follow-up-queue.md` and continue the work without starting from scratch, the lab did its job.
