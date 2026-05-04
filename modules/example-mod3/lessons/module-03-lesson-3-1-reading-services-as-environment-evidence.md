# Lesson 3.1 - Reading Services as Environment Evidence

---

> **Lesson Objective**
>
> Learn to read exposed services as evidence about host role, trust, data, management, and follow-up priority instead of treating them as a flat list of ports.

| Course | Module | Lesson | Type | Estimated time |
|---|---|---|---|---:|
| Hack the Basics | 03 - Interpret Exposed Services | 3.1 | Anchor lesson | 50-70 min |

| You have | You will produce | Lab checkpoint |
|---|---|---|
| Module 02 scan outputs and host tracker | initial host-role hypotheses | Checkpoint A |

---

## Why This Lesson Matters

After Module 02, the learner can discover reachable hosts and exposed services. That is a major step, but it is still only the beginning of assessment reasoning.

A port list is like seeing lights on in a building from the street. It tells us where something appears active, but it does not tell us what the rooms are used for, who depends on them, what trust relationships exist, or which door deserves attention first.

Service footprinting is the work of making that next layer visible.

When we see DNS, SMB, LDAP, Kerberos, RDP, SSH, FTP, HTTP, database ports, or management services, we are not just collecting protocol names. We are collecting clues about how the environment works. Some services help machines find each other. Some move files. Some enforce identity. Some expose administrative access. Some store application data. Some reveal names that later become search terms, login context, report evidence, or Active Directory targets.

The skill in this module is learning how to slow down just enough to ask:

> What does this service normally do, what did it reveal here, and what does that change about our next step?

That is a different skill from running more commands.

---

## The Practical Problem

Imagine Module 02 left you with this simplified scan picture:

```text
192.168.57.10
53/tcp   open  domain
88/tcp   open  kerberos-sec
389/tcp  open  ldap
445/tcp  open  microsoft-ds

192.168.57.31
135/tcp  open  msrpc
445/tcp  open  microsoft-ds
3389/tcp open  ms-wbt-server

192.168.57.25
21/tcp   open  ftp
22/tcp   open  ssh
80/tcp   open  http
```

A weak interpretation stops at the service names:

```text
DC has DNS, Kerberos, LDAP, SMB.
WS has RDP.
Linux box has FTP, SSH, web.
```

Those notes are not false. They are just too shallow to guide action.

A stronger interpretation starts looking for role and relationship:

```text
192.168.57.10 exposes DNS, Kerberos, LDAP, and SMB together. That combination strongly suggests Windows identity infrastructure and may indicate a domain controller, but the role still needs validation through naming, LDAP, SMB, and domain clues.

192.168.57.31 exposes SMB and RDP. That suggests a Windows host with file or management exposure, possibly a workstation or server. It may not be useful anonymously, but it may become important after credentials exist.

192.168.57.25 exposes FTP, SSH, and HTTP. That suggests a Linux target with multiple user-facing or admin-facing services. FTP and web may provide earlier low-friction clues than SSH, depending on access posture.
```

The difference is not vocabulary. The difference is reasoning.

The stronger notes give us decisions:

- Validate whether `192.168.57.10` is identity infrastructure.
- Check whether SMB reveals names or shares.
- Check whether FTP allows anonymous access.
- Route web exposure into Module 04.
- Revisit SMB, RDP, SSH, or WinRM after credentials exist.

That is what service footprinting should produce.

---

## Services Are Environment Functions

The first mental model is simple:

> A service is a visible function of the environment.

Ports are how we notice services. Protocols are how services speak. But the real assessment value comes from understanding what function the service performs.

DNS is not just port `53`; it is naming. SMB is not just port `445`; it is file sharing, Windows identity context, and sometimes administrative behavior. LDAP and Kerberos are not just directory-related ports; they indicate centralized identity. RDP is not just a login screen; it is a remote interactive management surface. FTP is not just old file transfer; it may reveal anonymous access, software banners, or operational files.

This is why the same service can mean different things on different hosts.

SMB on a domain controller does not tell the same story as SMB on a workstation. HTTP on a public web server does not tell the same story as HTTP on an internal admin appliance. SSH on a Linux server does not tell the same story as SSH on a network device. The service name is the start of the sentence, not the whole sentence.

What this changes:

> We should stop asking only "what port is open?" and start asking "what environment function does this exposure suggest?"

---

## A Role-Based View of Common Services

Once the idea is clear, the categories become useful.

| Role | Common services | What they may reveal |
|---|---|---|
| Naming | DNS, NetBIOS | hostnames, domains, records, naming authority |
| Identity | Kerberos, LDAP, SMB auth context | realms, domain clues, directory relevance |
| Storage | SMB, FTP, NFS, TFTP, Rsync | shares, exports, files, backup or deployment clues |
| Messaging | SMTP, IMAP, POP3 | mail hostnames, user-facing auth, TLS and capability clues |
| Data | MySQL, MSSQL, Oracle | application back-end role, versions, instance names |
| Monitoring | SNMP | device identity, interfaces, topology, system metadata |
| Management | SSH, RDP, WinRM, WMI, IPMI | administrative access paths and control-plane value |
| Web | HTTP, HTTPS | routes, names, app behavior, auth flows |

Do not treat this table as a memorization target. Treat it as a translation layer.

When a scan says `53`, translate it to naming. When it says `389`, translate it to directory and identity. When it says `3389`, translate it to remote interactive management. That translation helps the learner decide which questions are worth asking next.

---

## Observation, Inference, Validation, Next Step

Module 03 should use the course's core reasoning pattern constantly.

### Observation

An observation is what the evidence directly shows.

Example:

```text
389/tcp open on 192.168.57.10 in saved Nmap output.
```

That is direct. It is grounded in evidence.

### Inference

An inference is what the observation may suggest.

Example:

```text
LDAP exposure suggests the host may participate in directory or identity services.
```

That is reasonable, but it is not yet the same as proving the host is a domain controller.

### Validation

Validation is the next evidence needed to strengthen or correct the inference.

Example:

```text
Run a safe LDAP rootDSE query or correlate with Kerberos, DNS, SMB, and hostname evidence.
```

### Next step

The next step is the workflow decision created by the interpretation.

Example:

```text
Keep this host high priority for identity context and later AD reasoning.
```

This pattern keeps notes honest. It also teaches the learner how to avoid sounding more certain than the evidence allows.

---

## Worked Example: Three Hosts, Three Stories

Let us build an interpretation from the baseline hosts.

### Host 1: `192.168.57.10`

The first host exposes DNS, Kerberos, LDAP, SMB, and Windows RPC-style services. A beginner might immediately label it "the domain controller." In this lab, that may be true, but the course should train a better habit than guessing correctly.

The stronger move is to say:

```text
This host exposes several services commonly associated with Windows identity infrastructure. DNS suggests naming. Kerberos suggests domain authentication. LDAP suggests directory access. SMB and RPC suggest Windows host and file or management context. Together, these clues make a domain-controller hypothesis reasonable, but I should validate the naming context and domain clues before treating the role as confirmed.
```

That paragraph does more than name ports. It explains how the ports reinforce one another.

### Host 2: `192.168.57.31`

The second host exposes SMB and RDP. This is a different story. SMB can reveal Windows identity, shares, or domain context. RDP tells us an interactive remote access surface exists. But those services may be locked down until credentials exist.

A strong note might say:

```text
This host appears to expose Windows file or management surfaces. RDP increases later value if credentials are found, while SMB may reveal host and domain context now. If anonymous SMB access fails, the host should not be discarded; it should be marked for authenticated revisit after credential work.
```

The note connects current evidence to a later module.

### Host 3: `192.168.57.25`

The third host exposes FTP, SSH, and HTTP. This looks less like centralized identity and more like a Linux or mixed-service target. FTP may reveal files or anonymous access. SSH likely matters after credentials. HTTP routes into web recon.

The service mix gives a practical priority:

```text
Check FTP and HTTP first for low-friction metadata and visible application surface. Record SSH as a management surface that becomes more useful if credentials appear later.
```

The learner now has a plan.

---

## What Good Service Footprinting Produces

Good service footprinting does not produce a messy pile of terminal output.

It produces a tighter understanding of the target set.

At the end of this first pass, the learner should have:

- exact observed services
- service roles
- host-role hypotheses
- captured nouns
- confidence levels
- validation needs
- next workflow owners

The most important part is the link between evidence and decision.

Weak output:

```text
FTP, SSH, HTTP open on META-TGT.
```

Stronger output:

```text
META-TGT exposes FTP, SSH, and HTTP. FTP should be checked for banner, anonymous access, and visible files. HTTP routes to Module 04 web recon. SSH is a management surface but likely depends on credentials, so it should be revisited after credential discovery or validation.
```

The stronger version tells the learner what to do next and why.

---

## Checkpoint

Open the module lab and complete Checkpoint A.

Use only saved Module 02 evidence at first. Do not run new service commands yet.

Write one host-role note for each baseline host:

```text
Observed:

Service roles:

Host-role hypothesis:

Confidence:

Validation needed:

Likely next workflow:
```

This checkpoint matters because it prevents tool-chasing. It forces the learner to think before generating more output.

---

## Key Takeaways

- Ports are discovery clues; services are environment functions.
- Service footprinting turns exposure into host-role and follow-up meaning.
- A good note separates observation, inference, validation, and next step.
- Service combinations are often more meaningful than individual ports.
- The output of this module is not "more commands"; it is a prioritized interpretation of the environment.

---

## Next Lesson Bridge

Now that we can read services as environment evidence, we can start asking service-specific questions.

The next lesson begins with file, naming, and communication services because those families often reveal exact nouns early: hostnames, shares, domains, records, mail names, paths, and access posture.

Those nouns become the raw material for better assessment decisions.

