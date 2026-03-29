<div align="center">

# Module 03 Field Reference

**Service Footprinting and Common Infrastructure Enumeration**

*Phase I - Orientation and Surface Mapping*

</div>

---

> **🧭 Use This For**
>
> Fast service triage during labs and box work when you need to classify infrastructure services, extract high-value clues, correlate host-role signals, and route the right next step.

| Best paired with | Main job | Assumption |
|---|---|---|
| Lesson 3.4 and the module triage lab | Help you move from service exposure into prioritization and follow-up routing | Authorized lab use only |

| Preserve these outputs | Avoid these habits |
|---|---|
| hostnames, domains, shares, records, instance names, role clues, triage priorities | treating protocol names as enough, skipping exact nouns, mixing observation with inference |

---

## Table of Contents

- [1. Quick Workflow](#1-quick-workflow)
- [2. Service Triage Pattern](#2-service-triage-pattern)
- [3. Service Role Classification](#3-service-role-classification)
- [4. Protocol Families at a Glance](#4-protocol-families-at-a-glance)
- [5. Common Commands by Service Family](#5-common-commands-by-service-family)
- [6. What to Capture](#6-what-to-capture)
- [7. Priority Lenses](#7-priority-lenses)
- [8. Handoff Routing](#8-handoff-routing)
- [9. Minimal Triage Note Template](#9-minimal-triage-note-template)

---

## 1. Quick Workflow

> **🧠 Mental Model**
>
> identify -> enumerate -> correlate -> prioritize -> route -> document

### Quick service-footprinting rhythm

1. Enrich the host with `-sV`, selected scripts, and service-aware checks.
2. Classify services by role: naming, identity, storage, messaging, data, monitoring, or management.
3. Capture exact nouns: hostnames, domains, shares, exports, versions, certificates, instance names.
4. Correlate repeated names and service combinations.
5. Build a follow-up queue instead of chasing everything at once.
6. Route each finding into the right later workflow.

### Fast first-pass examples

```bash
nmap -sV -sC -Pn -p <open-ports> <target>
nmap --script smb-os-discovery,smb-enum-shares -p 139,445 <target>
nmap --script mysql-info,ms-sql-info -p 3306,1433 <target>
nmap --script rdp-ntlm-info,ssl-cert -p 3389 <target>
```

---

## 2. Service Triage Pattern

```text
Identify -> Enumerate -> Correlate -> Prioritize -> Route -> Document
```

| Triage question | Why it matters |
|---|---|
| What does this service do for the environment? | Clarifies host role |
| What exact metadata did it reveal? | Preserves the reusable evidence |
| Does it point to identity, data, or admin value? | Helps rank priority |
| Does it align with other visible services? | Strengthens confidence |
| Which later workflow should own the next step? | Prevents random tool hopping |

---

## 3. Service Role Classification

| Role | Typical services | What it often reveals |
|---|---|---|
| Naming | DNS, NetBIOS naming | hostnames, domains, routing clues |
| Identity | LDAP, Kerberos, SMB auth context | directory relevance, trust, centralized auth |
| Storage | SMB, NFS, FTP, SFTP | shares, exports, backups, configs |
| Messaging | SMTP, IMAP, POP3 | mail hostnames, auth posture, transport clues |
| Data | MySQL, MSSQL, Oracle TNS | application back-end role, instance clues |
| Monitoring | SNMP | device identity, interface and topology hints |
| Management | SSH, WinRM, RDP, IPMI | administrative access paths and control-plane relevance |

> **🔍 Interpretation**
>
> Services are not just ports. They are environment functions with trust implications.

---

## 4. Protocol Families at a Glance

| Family | Start by asking | High-value clues |
|---|---|---|
| FTP / SMB / NFS | what directories, shares, or exports are visible? | names, paths, auth posture, backups |
| DNS | what names and records map the environment? | domains, MX, NS, PTR, SRV |
| SMTP / IMAP / POP3 | what does the mail surface reveal? | mail hostnames, auth methods, TLS names |
| MySQL / MSSQL / Oracle | what software and instance clues appear? | versions, banners, database role |
| SNMP / IPMI | what device or management context is exposed? | host identity, interfaces, hardware context |
| SSH / WinRM / RDP | what admin pathway is visible? | host role, auth context, remote-management value |

---

## 5. Common Commands by Service Family

### File and storage

```bash
nc <target> 21
smbclient -L //<target>/ -N
showmount -e <target>
nmap --script smb-os-discovery,smb-enum-shares,smb-security-mode -p 139,445 <target>
```

### Naming and identity

```bash
dig @<dns-server> <domain> A
dig @<dns-server> -x <ip>
dig @<dns-server> axfr <domain>
nmap --script ldap-rootdse -p 389,636 <target>
ldapsearch -x -H ldap://<target> -s base namingcontexts defaultnamingcontext
```

### Data, monitoring, and management

```bash
nmap --script mysql-info,ms-sql-info -p 3306,1433 <target>
snmpwalk -v2c -c public <target> 1.3.6.1.2.1.1
nmap --script rdp-ntlm-info,ssl-cert -p 3389 <target>
nmap -sV -p 22,5985,5986,3389,623 <target>
```

---

## 6. What to Capture

### Exact nouns matter

- hostnames
- domains and realms
- share names
- export paths
- MX, NS, PTR, SRV records
- instance names
- certificate names
- signs of centralized identity

### Strong notes look like

```text
SMB host identifies as FS01.corp.lab; shares Engineering and Backups visible; signing required.
```

Not:

```text
SMB open.
```

---

## 7. Priority Lenses

| Lens | What to ask |
|---|---|
| Value | If this pays off, what does it tell us or enable? |
| Access | Do we have a clean next-step validation from here? |
| Trust | Does this sit close to identity, admin, or shared infrastructure? |
| Reachability | Can we interact with it meaningfully right now? |

### Red flags that usually raise priority

- identity services align across DNS, LDAP, Kerberos, SMB, and host naming
- anonymous or weakly protected access appears possible
- admin services are exposed unexpectedly
- naming reveals internal structure or high-value hosts
- storage paths suggest backups, configs, or business data

---

## 8. Handoff Routing

| If you see this | Route it toward |
|---|---|
| web stack context, app servers, HTTP exposure | later web recon and web testing modules |
| login surfaces, auth posture, reusable names | credential and authentication workflows |
| rich service posture with common enterprise apps | common-service and common-application attack paths |
| remote execution or admin pathways | foothold and post-access workflows |
| identity-heavy infrastructure clues | later Windows and Active Directory work |

> **⚠️ Warning**
>
> This module is for first-pass interpretation and routing, not for doing every later module early.

---

## 9. Minimal Triage Note Template

```text
Host:
Visible service mix:
Likely host role:
High-value nouns captured:
Observation:
Inference:
Most likely next workflow:
Priority level:
Open questions:
```

---

<div align="center">

**Read services as systems: classify the role, capture the nouns, and route the next step deliberately.**

</div>
