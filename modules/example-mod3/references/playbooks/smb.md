# SMB Playbook - Module 03

---

> **Playbook Role**
>
> Use this when SMB appears in Module 03 and you need focused service-footprinting guidance without turning the main lesson into an SMB manual.

SMB matters because it often sits close to identity, file sharing, workstation behavior, domain membership, and administrative workflows. An exposed SMB service is not automatically a vulnerability, but it is rarely meaningless.

The first question is not "Can I exploit SMB?"

The first question is:

> What does SMB reveal about this host's role and access posture?

---

## First-Pass Questions

Ask these in order:

1. Does the host expose SMB over `139`, `445`, or both?
2. Does it reveal a hostname, domain, or workgroup?
3. Does anonymous or guest access show anything?
4. Are shares visible?
5. Do share names suggest users, departments, backups, deployments, or administration?
6. Does signing posture matter for later modules?
7. Should SMB be revisited after credentials exist?

---

## Commands

```bash
nmap -sV -p 139,445 <target>
nmap --script smb-os-discovery,smb-security-mode,smb-enum-shares -p 139,445 <target>
smbclient -N -L //<target>/
rpcclient -U "" -N <target>
```

If credentials exist later:

```bash
smbclient -L //<target>/ -U '<domain>/<user>'
smbclient //<target>/<share> -U '<domain>/<user>'
```

Do not invent credentials or guess passwords in Module 03. Credential validation belongs to later scoped workflows.

---

## Interpretation

### Anonymous listing succeeds

This raises priority because the service is exposing structure without credentials. The next question is whether the names or permissions reveal business function, host role, or possible sensitive material.

Do not jump directly to "critical finding." First preserve:

- host
- command
- visible shares
- access posture
- whether files were readable
- what exact names appeared

### Anonymous listing fails

This is still useful.

It tells you that low-friction unauthenticated access did not reveal shares from your position. SMB may still matter after credentials exist, especially on Windows infrastructure hosts.

### Host/domain names appear

Names are reusable evidence. They can shape later DNS, credential, Windows, and AD reasoning.

Capture the exact strings.

---

## Strong Note Example

```text
Observed:
445/tcp reachable on 192.168.57.10. smb-os-discovery reports host-like Windows identity strings. Anonymous share listing did not expose shares.

Inference:
SMB supports the hypothesis that this is a Windows infrastructure host, but current unauthenticated access does not expose file shares.

Validation needed:
Correlate with DNS/LDAP/Kerberos naming context. Revisit SMB after credentials exist.

Next workflow:
Module 06 for credential context; Module 14 for AD reasoning later.
```

