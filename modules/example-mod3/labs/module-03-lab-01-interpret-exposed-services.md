# Module 03 Lab 01 - Interpret Exposed Services

---

> **Lab Objective**
>
> Use saved scan evidence and small live service checks to build host-role notes, complete a service-role worksheet, and create a prioritized follow-up queue.

| Module | Lab type | Main output |
|---|---|---|
| Module 03 - Interpret Exposed Services | Progressive module lab | service-role worksheet, host-role notes, saved evidence, follow-up queue |

---

## Scope Gate

This lab is for legal lab environments only.

Use the course baseline unless your instructor or lab notes explicitly authorize a different target set:

| Host | IP | Allowed in this lab |
|---|---:|---|
| `GOAD-Mini-DC01` | `192.168.57.10` | service footprinting and safe enumeration |
| `GOAD-Mini-WS01` | `192.168.57.31` | service footprinting and safe enumeration |
| `META-TGT` | `192.168.57.25` | service footprinting and safe enumeration |

Do not run broad brute force, password guessing, destructive tests, exploit modules, or out-of-scope scans. Module 03 is about interpretation and careful service checks, not exploitation.

---

## Scenario

Module 02 left you with saved scan outputs and a host tracker. You know which hosts appear reachable and which services appear exposed.

Now your job is to make those results meaningful.

You are not trying to "attack every port." You are trying to decide what the exposed services suggest about each host and which future workflow should own the next step.

A good service footprint should answer:

- What service appears reachable?
- What is that service normally for?
- What exact names or metadata did it reveal?
- What host-role hypothesis does it support?
- What still needs validation?
- Which later module or workflow should handle the next action?

---

## Workspace

Use the same workspace from Modules 01 and 02.

Recommended paths:

```text
assessment-workspace/
  01-target-notes/
    host-tracking.md
  02-evidence/
    scans/module-02/
    services/module-03/
  03-analysis/
    module-03-host-role-notes.md
    follow-up-queue.md
```

Create missing folders before starting:

```bash
mkdir -p assessment-workspace/02-evidence/services/module-03
mkdir -p assessment-workspace/03-analysis
touch assessment-workspace/03-analysis/module-03-host-role-notes.md
touch assessment-workspace/03-analysis/follow-up-queue.md
```

---

## Checkpoint A - Read the Scan Evidence Before Running More Tools

Complete this after Lesson 3.1.

Start with what you already have. Open your Module 02 scan outputs and host tracker. The purpose of this checkpoint is to build initial host-role hypotheses from existing evidence before you generate new output.

For each baseline host, write a short note:

```text
## <host>

Observed services:

Initial service roles:

Host-role hypothesis:

Confidence:

Validation needed:
```

The important discipline here is to keep observation and inference separate.

Weak note:

```text
DC01 is the domain controller.
```

Stronger note:

```text
Observed DNS, Kerberos, LDAP, SMB, and Windows RPC exposure on 192.168.57.10. This combination strongly suggests a Windows identity infrastructure role and may indicate a domain controller, but I still need naming context, realm/domain, and SMB/LDAP identity clues to validate the role.
```

Save the result in:

```text
assessment-workspace/03-analysis/module-03-host-role-notes.md
```

---

## Checkpoint B - Capture File, Naming, and Communication Clues

Complete this after Lesson 3.2.

The goal is not to run every command. The goal is to ask cheap, protocol-correct questions that improve your host-role notes.

### DNS and naming checks

Start with the host most likely to provide naming clues.

```bash
host 192.168.57.10 | tee assessment-workspace/02-evidence/services/module-03/dc01-host-lookup.txt
dig @192.168.57.10 -x 192.168.57.10 | tee assessment-workspace/02-evidence/services/module-03/dc01-ptr.txt
```

If you know the lab domain, query it deliberately:

```bash
dig @192.168.57.10 <domain> A
dig @192.168.57.10 <domain> NS
```

Do not invent a domain if your notes do not support one yet.

### SMB first checks

Use SMB to learn identity and share posture. Start with anonymous checks because they are low-friction and show whether the service exposes anything without credentials.

```bash
smbclient -N -L //192.168.57.10/ | tee assessment-workspace/02-evidence/services/module-03/dc01-smb-null-shares.txt
smbclient -N -L //192.168.57.31/ | tee assessment-workspace/02-evidence/services/module-03/ws01-smb-null-shares.txt
```

If anonymous listing fails, that is still useful. It tells you something about access posture.

Record whether you observed:

- hostname or domain/workgroup names
- share names
- guest or anonymous behavior
- signing posture from Nmap or other tools
- differences between the infrastructure host and workstation

### FTP first checks

Use FTP on `META-TGT` if it is exposed in your baseline.

```bash
nc -nv 192.168.57.25 21 | tee assessment-workspace/02-evidence/services/module-03/meta-ftp-banner.txt
ftp 192.168.57.25
```

During the interactive FTP session, test only safe, low-impact behavior such as banner reading and anonymous login if allowed by the lab.

After this checkpoint, update your host-role notes. The update should explain what changed.

Example:

```text
Update: SMB anonymous share listing did not expose shares on DC01, but DNS and LDAP-related service exposure still support identity infrastructure follow-up. SMB should remain in the queue for authenticated revisit after credential work.
```

---

## Checkpoint C - Capture Data, Management, and Remote Access Clues

Complete this after Lesson 3.3.

This checkpoint asks whether any exposed service suggests administration, control, back-end data, or later access value.

### RDP posture on the Windows workstation

```bash
nmap --script rdp-ntlm-info,ssl-cert -p 3389 192.168.57.31 -oN assessment-workspace/02-evidence/services/module-03/ws01-rdp-info.txt
```

This does not prove you can log in. It tells you the host exposes a remote desktop surface and may reveal naming or certificate clues.

### SSH posture on the Linux target

```bash
nmap -sV -p 22 192.168.57.25 -oN assessment-workspace/02-evidence/services/module-03/meta-ssh-version.txt
```

If you have `ssh-audit` installed, you may use it for posture clues, but do not let this become a hardening audit.

### Database and monitoring checks

If your scan evidence shows database or monitoring services, run focused checks. If not, mark those families as reference-only for this baseline.

Examples:

```bash
nmap --script mysql-info -p 3306 <target>
nmap --script ms-sql-info -p 1433 <target>
snmpwalk -v2c -c public <target> 1.3.6.1.2.1.1
```

Do not run them blindly across the whole subnet. The question is whether a specific exposed service changes host priority.

---

## Checkpoint D - Build the Follow-Up Queue

Complete this after Lesson 3.4.

Open:

```text
assessment-workspace/03-analysis/module-03-host-role-notes.md
assessment-workspace/03-analysis/follow-up-queue.md
```

For each meaningful service or host, write a queue entry:

```text
## Follow-up item

Host:
Service:
Observed evidence:
Inference:
Confidence:
Validation needed:
Next workflow owner:
Priority:
Reason:
```

Use workflow owners, not vague next actions:

| Workflow owner | Use when |
|---|---|
| Module 04 - Web recon | HTTP/HTTPS exposure needs route, name, or application mapping |
| Module 06 - Credentials | auth surfaces, possible credential reuse, login portals, or exposed credential material appear |
| Module 09 - Service attacks | a common service needs safe validation against known weakness patterns |
| Module 10 - Footholds | a validated path may lead to initial access |
| Module 12 - Windows privesc | Windows host context matters after access |
| Module 14 - AD | identity, domain, trust, or privilege graph context is central |

Your final queue should be short enough to act on. If everything is priority 1, nothing is prioritized.

---

## Validation Questions

Before leaving this module, answer:

1. Which host appears most identity-relevant, and what evidence supports that?
2. Which host appears most likely to provide early low-friction follow-up, and why?
3. Which services are only interesting after credentials exist?
4. Which outputs contain exact nouns worth preserving?
5. Which conclusions did you avoid because the evidence was not strong enough yet?
6. Which queue entry should Module 04 receive first?

---

## Lab Close-Out

End with a short close-out note:

```text
Module 03 close-out

Most important observed services:

Strongest host-role hypothesis:

Highest-priority follow-up:

Deferred until credentials:

Deferred until later modules:

Evidence paths:
```

The close-out note is the handoff into the next phase.

