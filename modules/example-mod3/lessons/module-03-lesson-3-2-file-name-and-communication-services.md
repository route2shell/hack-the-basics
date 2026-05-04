# Lesson 3.2 - File, Naming, and Communication Services

---

> **Lesson Objective**
>
> Learn how file, naming, and communication services reveal the nouns of an environment: hosts, domains, shares, paths, mail surfaces, and access posture.

| Course | Module | Lesson | Type | Estimated time |
|---|---|---|---|---:|
| Hack the Basics | 03 - Interpret Exposed Services | 3.2 | Workflow lesson | 60-80 min |

| You have | You will produce | Lab checkpoint |
|---|---|---|
| host-role hypotheses from Lesson 3.1 | captured nouns and updated service-role notes | Checkpoint B |

---

## Why This Lesson Matters

After Lesson 3.1, the learner has initial hypotheses about what each host might be. Those hypotheses are useful, but they are still mostly based on the shape of the port list.

This lesson teaches how to sharpen that shape with service-specific evidence.

File, naming, and communication services are valuable because they often reveal the language of the environment. They can expose hostnames, domains, share names, export paths, mailbox names, certificates, capability strings, or directory structures. Those details may seem small, but they become the connective tissue of an assessment.

A share named `backups` is different from a share named `print$`. A DNS record for `dc01.corp.lab` is different from a generic PTR failure. An FTP banner that reveals software and allows anonymous access changes priority more than a banner alone. A mail service that exposes authentication capabilities gives different follow-up context than a closed or filtered mail port.

The point is not to memorize every protocol. The point is to learn how to ask what each service is designed to reveal.

---

## The Mental Model: Exact Nouns Matter

Early enumeration is often won by capturing exact nouns.

Names are not decorative details. They are handles the environment gives us. They let us correlate outputs across tools, write cleaner notes, build better wordlists, recognize role patterns, and later explain findings with precision.

If a learner writes:

```text
SMB had some shares.
```

the note is weak because it cannot support a decision.

If the learner writes:

```text
SMB anonymous listing on 192.168.57.25 revealed shares named public, tmp, and backup. The backup name raises follow-up priority because it may contain operational data or configuration history.
```

the note becomes useful. It preserves the exact nouns and explains why one of them changes priority.

That is the habit this lesson builds.

---

## File Services: Convenience Becomes Context

File services exist because people and systems need to move or share data. In normal environments, that is not suspicious. Administrators need file shares. Applications need deployment paths. Users need shared folders. Backups need somewhere to land.

For an assessor, that normal convenience becomes context.

An exposed file service may reveal how the organization names departments, where scripts live, whether old backups exist, whether anonymous access is allowed, or whether a host behaves more like a file server, workstation, application server, or lab target.

This is why file-service enumeration should start gently. We are not trying to loot everything. We are trying to understand access posture and host role.

### FTP

FTP is often one of the easiest services to reason about because its first questions are direct:

- Does it answer?
- What banner does it show?
- Does anonymous login work?
- What directories or files are visible?
- Are files readable or writable?

Those questions become meaningful only when tied to interpretation.

If FTP answers with a banner but denies anonymous login, the result is still useful but limited. It tells us the service exists, gives possible software context, and may become relevant after credentials. If anonymous login succeeds, the service moves up in priority because unauthenticated users can see something. If writable directories appear, the result may route into later service-attack or foothold workflows, but Module 03 should still avoid destructive testing.

Representative first checks:

```bash
nc -nv 192.168.57.25 21
ftp 192.168.57.25
```

What to record:

```text
Observed:
FTP banner returned from 192.168.57.25. Anonymous login accepted. Directory listing showed public files.

Inference:
The service exposes unauthenticated file visibility on the Linux target.

Validation needed:
Record exact filenames and permissions. Avoid writing or modifying files in this module.

Next workflow:
Service attack playbook later if file permissions or web linkage create a safe validation path.
```

### SMB

SMB is richer than FTP because it often blends file sharing, host identity, Windows domain context, and authentication behavior.

SMB can reveal share names, domain or workgroup strings, signing posture, hostnames, and whether guest or anonymous access is allowed. But SMB also teaches restraint. A failed anonymous share listing is not a dead end. It is an access-posture observation. The service may become more useful after credentials exist.

Representative first checks:

```bash
smbclient -N -L //192.168.57.10/
smbclient -N -L //192.168.57.31/
nmap --script smb-os-discovery,smb-security-mode -p 139,445 192.168.57.10
```

A beginner might write:

```text
SMB closed to anonymous.
```

A stronger note says:

```text
Anonymous SMB share listing did not expose shares on 192.168.57.10. SMB remains relevant because the host also exposes DNS, Kerberos, and LDAP, which suggests Windows identity infrastructure. Revisit SMB after credentials exist and preserve current anonymous failure as access-posture evidence.
```

The stronger note keeps the service in context.

---

## Naming Services: The Environment Describes Itself

Naming services matter because they help systems find each other. During an assessment, they help us understand how the environment describes itself.

DNS can reveal hostnames, domains, mail routing, service records, and authority relationships. NetBIOS naming can reveal Windows host names or workgroup context. Certificates can reveal alternate names. LDAP naming contexts can validate identity infrastructure.

Naming clues are powerful because they connect otherwise separate pieces of evidence.

Suppose a reverse lookup gives us `dc01.example.lab`, SMB output mentions the same domain, and LDAP rootDSE exposes a matching naming context. Those clues reinforce one another. The host-role hypothesis becomes stronger because multiple services tell the same story.

Representative first checks:

```bash
host 192.168.57.10
dig @192.168.57.10 -x 192.168.57.10
nmap --script ldap-rootdse -p 389 192.168.57.10
```

The learner should not treat a single name as proof of everything. Names can be stale, misleading, or lab-specific. But repeated names across services are strong evidence.

What this changes:

> We should capture exact names and look for repetition across services before deciding how confident we are about host role.

---

## Communication Services: Mail and Message Surfaces

Mail services may not always exist in the default lab, but the reasoning matters because they appear often in real environments and training networks.

SMTP, IMAP, and POP3 can reveal mail hostnames, TLS names, authentication mechanisms, mailbox access posture, and sometimes user-enumeration behavior. In Module 03, we care about their footprinting value, not password attacks.

A mail service is interesting because it often sits close to identity. Users authenticate to mail. Domains route mail. Certificates and banners may reveal naming. Capability output may show supported auth methods or transport requirements.

If mail services are not live in the baseline, mark them as reference-only. Do not pretend to perform live checks your lab does not support.

Representative checks when scoped and live:

```bash
nc -nv <target> 25
openssl s_client -connect <target>:993
openssl s_client -connect <target>:995
```

Strong interpretation:

```text
SMTP greeting reveals mail hostname mail01.example.lab and STARTTLS capability. This supports messaging infrastructure context and may later inform credential or identity workflows. No user validity or mailbox access has been validated.
```

That note is careful. It does not overclaim.

---

## Worked Example: Updating the Host Story

Return to the baseline.

After Lesson 3.1, your note for `192.168.57.10` might say:

```text
Likely Windows identity infrastructure host based on DNS, Kerberos, LDAP, SMB, and RPC exposure.
```

After naming and SMB checks, it can become stronger:

```text
DNS and LDAP checks return domain-oriented naming context. SMB anonymous listing does not expose shares, but SMB service remains consistent with Windows identity infrastructure. The host-role hypothesis is now stronger because DNS, Kerberos, LDAP, and SMB all align around centralized identity.
```

Notice what changed. The note did not simply gain more commands. It gained a better reason.

That is the goal.

---

## What Not to Overclaim

This lesson deals with services that can reveal a lot of metadata. Metadata is useful, but it is not magic.

Avoid these overclaims:

| Weak claim | Better framing |
|---|---|
| SMB is open, so shares are vulnerable. | SMB is reachable. Share visibility and permissions need validation. |
| DNS exists, so this is definitely a domain controller. | DNS exposure supports naming infrastructure; correlate with Kerberos, LDAP, hostnames, and domain context. |
| FTP banner means exploitable FTP. | FTP is reachable and reveals software; exploitability depends on version, configuration, access, and validation. |
| Mail service means valid users can be enumerated. | Mail exposure may reveal identity context; user enumeration requires scoped validation. |

The course is teaching the learner to sound precise because precision reflects better thinking.

---

## Checkpoint

Open the module lab and complete Checkpoint B.

Your goal is to update the service-role worksheet with exact nouns and revised interpretations.

For each useful output, write:

```text
Observed:

Captured nouns:

Inference:

Validation needed:

Next workflow:
```

If a service family is not live in your baseline, mark it as optional or reference-only. Honesty about the lab state is part of the workflow.

---

## Key Takeaways

- File services reveal access posture, paths, shares, and operational clues.
- Naming services reveal how the environment describes itself.
- Communication services often connect to identity and user-facing workflows.
- Exact nouns matter more than vague service labels.
- Failed unauthenticated access is still evidence.
- Strong notes explain what changed about the host story.

---

## Next Lesson Bridge

File, naming, and communication services often reveal the nouns of the environment.

The next lesson looks at services that can reveal value and control: databases, monitoring, and remote management.

Those services may not always expose useful information immediately, but when they do, they can change priority quickly.

