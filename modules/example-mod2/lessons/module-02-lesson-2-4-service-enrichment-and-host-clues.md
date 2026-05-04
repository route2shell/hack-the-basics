# Lesson 2.4 - Service Enrichment and Host Clues

---

> **Lesson Objective**
>
> Learn to enrich open ports with service, version, script, and host-role clues without treating automated labels as final truth.

| Course | Module | Lesson | Type | Estimated time |
|---|---|---|---|---:|
| Hack the Basics | 02 - Map the Visible Network | 2.4 | Workflow lesson | 50-70 min |

| You have | You will produce | Lab checkpoint |
|---|---|---|
| TCP/UDP triage output | saved enrichment scans and service clues | Checkpoint D |

---

## Why This Lesson Matters

A port-state scan tells us where something may be reachable. It does not fully tell us what that something is.

Service enrichment asks the next question:

> What appears to be behind the open port, and what clues should we preserve for follow-up?

This is where Nmap becomes more than a port scanner. Version detection, default scripts, and focused NSE scripts can reveal protocol behavior, product names, hostnames, certificates, titles, SMB posture, LDAP naming context, and other details that shape Module 03.

But enrichment output can also mislead. Banners can be wrong. Version guesses can be approximate. Scripts can fail. A title can describe a default page but not the full application. OS detection can suggest a family but not prove the exact operating system.

The learner's job is to collect clues and label confidence honestly.

---

## Enrichment Is Follow-Up, Not Noise

A strong enrichment pass is based on triage evidence.

If TCP triage shows FTP, SSH, and HTTP on `META-TGT`, enrichment should focus on those open ports. If `GOAD-Mini-DC01` shows DNS, Kerberos, LDAP, and SMB, enrichment should capture identity and Windows infrastructure clues. If a workstation exposes RDP, a focused RDP script may reveal useful naming or certificate context.

The mistake is to run every script category everywhere.

That creates noise, takes time, and produces output the learner does not know how to use.

The better habit is:

```text
Open ports first.
Then service identity.
Then targeted scripts only where they answer a question.
```

---

## Version Detection

Version detection asks services to reveal more about themselves.

```bash
nmap -sV -Pn -p <open-ports> -oA "$M2SCAN"/meta-version-YYYY-MM-DD 192.168.57.25
```

This may produce product names, versions, protocol guesses, or banners.

Those clues matter because they help Module 03 decide which service family to footprint and what exact nouns to preserve.

But version detection should be written carefully:

```text
Nmap reports OpenSSH-like service on 22/tcp.
```

is better than:

```text
The box is vulnerable because OpenSSH is old.
```

Version is a clue. Vulnerability requires separate validation.

---

## Default Scripts

Default scripts can provide useful first-pass context.

```bash
nmap -sV -sC -Pn -p <open-ports> -oA "$M2SCAN"/meta-defaultscripts-YYYY-MM-DD 192.168.57.25
```

The value of default scripts is that they may reveal extra protocol context without the learner choosing every script manually. The risk is that learners treat the output as a complete audit.

It is not complete.

It is an enrichment layer.

Good notes should say what the script output changed:

```text
http-title script returned a page title. This confirms HTTP responds with web content and gives a first web clue for Module 04, but it does not map routes or functionality.
```

---

## Focused Scripts

Focused scripts are strongest when the learner already knows the question.

Examples:

```bash
nmap --script smb-os-discovery,smb-security-mode -p 445 -oA "$M2SCAN"/dc01-smb-focused-YYYY-MM-DD 192.168.57.10
```

This asks:

> What SMB host and posture clues can we safely collect for Module 03?

Another example:

```bash
nmap --script http-title,ssl-cert -p 80,443 -oA "$M2SCAN"/meta-web-focused-YYYY-MM-DD 192.168.57.25
```

This asks:

> What web title or certificate clues should be preserved for later web recon?

The command matters less than the question.

---

## OS and Host Clues

OS detection and host clues can help, but they are easy to overread.

OS detection may suggest Linux, Windows, or a device family. SMB or RDP scripts may reveal hostnames. Certificates may reveal names. TTLs and service combinations may suggest platform patterns.

Those clues can sharpen host-role hypotheses, but they should not become unsupported certainty.

Weak note:

```text
Nmap says Windows, so confirmed Windows 10.
```

Stronger note:

```text
Nmap OS and service clues suggest a Windows host. SMB and RDP output should be correlated before writing a stronger host-role claim.
```

This is the style Module 03 will depend on.

---

## Worked Example: Enriching for Module 03

Suppose TCP triage on `192.168.57.10` showed:

```text
53/tcp open
88/tcp open
389/tcp open
445/tcp open
```

The enrichment question is:

> What service clues confirm whether this host is naming or identity infrastructure?

A useful focused pass might include version detection and selected scripts:

```bash
nmap -sV -sC -Pn -p 53,88,389,445 -oA "$M2SCAN"/dc01-service-enriched-YYYY-MM-DD 192.168.57.10
```

The note should not simply paste output. It should interpret:

```text
Observed:
DNS, Kerberos, LDAP, and SMB services respond on 192.168.57.10. Enrichment output includes Windows and directory-oriented service clues.

Inference:
This host likely participates in identity infrastructure and deserves Module 03 service footprinting for naming, LDAP, Kerberos, and SMB context.

Validation needed:
Module 03 should capture exact domain, realm, naming context, SMB posture, and host-role evidence.
```

That is a real handoff.

---

## Checkpoint

Open the module lab and complete Checkpoint D.

Run enrichment against:

- one Linux-style or mixed-service host
- one Windows or identity-style host

Then write:

```text
Observed service clues:

Names or versions captured:

What changed about the host story:

What Module 03 should inspect:

Evidence path:
```

---

## Key Takeaways

- Enrichment should follow triage evidence.
- Version detection gives clues, not final vulnerability claims.
- Default scripts are useful first-pass context, not complete audits.
- Focused scripts are strongest when tied to a question.
- Module 03 needs service clues, exact nouns, and uncertainty boundaries.

---

## Next Lesson Bridge

You now have discovery, triage, and enrichment evidence.

The final lesson turns those individual scan actions into a repeatable workflow: output conventions, artifact preservation, host tracking, and a follow-up queue that makes Module 03 effective.

