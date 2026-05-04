# Module 03 Field Reference

---

> **Use This For**
>
> Fast service-footprinting support while working the Module 03 lab. This reference keeps command and interpretation reminders out of the main lesson path.

---

## Core Rhythm

```text
Observe -> Classify -> Extract nouns -> Correlate -> Prioritize -> Route
```

Service footprinting is not "run every enum tool."

It is the controlled process of asking what each exposed service does for the environment and whether it changes the next step.

---

## Service Roles

| Role | Services | What to capture |
|---|---|---|
| Naming | DNS, NetBIOS | hostnames, domains, PTR, NS, MX, SRV |
| Identity | Kerberos, LDAP, SMB auth context | realms, naming contexts, domain/workgroup, trust clues |
| Storage | SMB, FTP, NFS, TFTP, Rsync | shares, exports, paths, anonymous/guest behavior |
| Messaging | SMTP, IMAP, POP3 | mail hostnames, capabilities, TLS names, auth methods |
| Data | MySQL, MSSQL, Oracle | versions, instance names, exposed database role |
| Monitoring | SNMP | device identity, interfaces, location, topology clues |
| Management | SSH, RDP, WinRM, WMI, IPMI | admin pathways, remote access posture, host role |
| Web | HTTP, HTTPS | titles, certificates, redirects, hostnames, routes |

---

## First Checks by Family

### DNS and naming

```bash
host <ip>
dig @<dns-server> -x <ip>
dig @<dns-server> <domain> A
dig @<dns-server> <domain> NS
dig @<dns-server> <domain> MX
```

Interpretation:

- PTR names can sharpen host-role hypotheses.
- NS and SOA records can identify naming authority.
- MX records route into mail and identity context.
- Failed queries still say something about what the server will or will not answer.

### SMB

```bash
smbclient -N -L //<target>/
nmap --script smb-os-discovery,smb-security-mode,smb-enum-shares -p 139,445 <target>
rpcclient -U "" -N <target>
```

Interpretation:

- Share names are high-value nouns.
- Anonymous failure is still useful access-posture evidence.
- Domain/workgroup strings can sharpen identity context.
- SMB should often be revisited after credentials exist.

### FTP

```bash
nc -nv <target> 21
ftp <target>
nmap -sV -p 21 <target>
```

Interpretation:

- Banners may reveal software and host naming.
- Anonymous access changes priority.
- Writable paths are higher risk than readable paths, but require careful validation.

### LDAP and identity

```bash
nmap --script ldap-rootdse -p 389 <target>
ldapsearch -x -H ldap://<target> -s base namingcontexts defaultnamingcontext
```

Interpretation:

- Naming contexts can validate domain identity.
- LDAP exposure does not automatically mean exploitable access.
- Identity clues often route into credential and AD modules later.

### RDP and remote management

```bash
nmap --script rdp-ntlm-info,ssl-cert -p 3389 <target>
nmap -sV -p 22,3389,5985,5986 <target>
```

Interpretation:

- Remote access surfaces often matter after credentials exist.
- Certificate and NTLM info may reveal host/domain names.
- Do not treat a login prompt as access.

### Databases and monitoring

```bash
nmap --script mysql-info -p 3306 <target>
nmap --script ms-sql-info -p 1433 <target>
snmpwalk -v2c -c public <target> 1.3.6.1.2.1.1
```

Interpretation:

- Database exposure suggests application back-end value.
- SNMP can expose host and network context quickly.
- These services deserve priority when they reveal data, management, or credential paths.

---

## Strong Note Pattern

Use this shape:

```text
Observed:

Interpretation:

Confidence:

Validation needed:

Next workflow:

Evidence path:
```

Example:

```text
Observed:
192.168.57.31 exposes SMB and RDP. RDP script output returns a Windows hostname. Anonymous SMB share listing fails.

Interpretation:
The host likely behaves like a managed Windows workstation or Windows server with remote desktop enabled. SMB is not currently exposing anonymous share data, but it may become useful after credentials exist.

Confidence:
Medium.

Validation needed:
Confirm hostname/domain context and revisit SMB with credentials later.

Next workflow:
Module 06 for credentials if found; Module 12 after access; Module 14 if domain context matters.

Evidence path:
assessment-workspace/02-evidence/services/module-03/ws01-rdp-info.txt
```

---

## Priority Lenses

A service becomes higher priority when it:

- reveals exact names
- touches identity
- exposes data
- exposes administrative access
- allows anonymous or guest interaction
- appears on a high-value host
- correlates with other services
- creates a clean next step for a later module

Priority is not the same as exploitability.

Priority means the service is likely to reduce uncertainty or advance the assessment.

