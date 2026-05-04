# Lesson 3.4 - Building the Service Triage Queue

---

> **Lesson Objective**
>
> Turn service-footprinting evidence into a prioritized follow-up queue that routes each important service to the right later workflow.

| Course | Module | Lesson | Type | Estimated time |
|---|---|---|---|---:|
| Hack the Basics | 03 - Interpret Exposed Services | 3.4 | Synthesis lesson | 50-70 min |

| You have | You will produce | Lab checkpoint |
|---|---|---|
| service evidence, host-role notes, worksheet entries | prioritized follow-up queue | Checkpoint D |

---

## Why This Lesson Matters

Enumeration only becomes useful when it changes what we do next.

By now, the learner has seen how exposed services can reveal host role, names, data value, and management surfaces. But a real assessment does not reward collecting endless evidence without direction. At some point, the learner must decide what matters most.

That decision is hard because multiple services can look interesting at once.

A domain controller-like host may expose DNS, LDAP, Kerberos, and SMB. A Linux target may expose FTP, SSH, and web. A Windows workstation may expose SMB and RDP. Each service suggests a possible path. The learner needs a way to route those paths without chasing everything randomly.

This lesson teaches that routing process.

The output is a follow-up queue: a short, evidence-backed list of what deserves attention next, why it matters, and which later module should own it.

---

## Triage Is Not Guessing

Prioritization can sound subjective, but good triage is not guessing. It is a structured decision based on evidence.

The learner should ask:

- What was directly observed?
- What host role does it suggest?
- How confident are we?
- What value or trust relationship might be involved?
- What can be validated safely now?
- What should wait for credentials or later modules?
- Which next action reduces uncertainty the most?

This is why Module 03 spends so much time separating observation from inference. If the notes are sloppy, the queue will be sloppy. If the notes are precise, prioritization becomes easier.

---

## The Priority Model

A service becomes higher priority when it helps answer one of four assessment questions.

### 1. Does it reveal identity?

Identity surfaces matter because they shape who users are, where credentials may apply, and how trust is organized.

DNS, LDAP, Kerberos, SMB, WinRM, RDP, and mail services can all contribute identity context. A host that appears to sit near identity infrastructure deserves careful handling because later credential and AD work may depend on it.

### 2. Does it reveal data?

Data surfaces matter because they may contain business information, credentials, configuration, backups, logs, or application state.

SMB shares, FTP directories, NFS exports, databases, web downloads, and backup-like paths can all raise priority. The important question is not just "can I see files?" but "what do these files suggest, and what decision do they support?"

### 3. Does it reveal management or control?

Management surfaces matter because they may become access paths after validation.

SSH, RDP, WinRM, WMI, IPMI, and administrative web panels should often be queued for later revisits, especially if credentials appear.

### 4. Does it connect to a clear next workflow?

Some findings are valuable because they route cleanly into the next part of the course.

HTTP routes to Module 04. Login surfaces route to Module 06. Service weakness patterns route to Module 09. Shell access routes to Module 10. Windows and domain identity context route to Modules 12 and 14.

The best queue entries identify the owner workflow.

---

## Priority Is About Timing

A common beginner mistake is to think priority means "most dangerous."

In this course, priority means:

> the next item most likely to reduce uncertainty or advance the assessment safely.

That distinction matters.

RDP on a workstation may be important later, but if we have no credentials, it may not be the best immediate action. A web service on the Linux target may be more actionable now because Module 04 can map routes and visible behavior. SMB on a domain controller-like host may be important, but if anonymous access reveals little, it may belong in a revisit queue after credential discovery.

Good prioritization is not just ranking value. It is ranking value in time.

---

## Building a Queue Entry

A strong queue entry should be small but complete.

Use this structure:

```text
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

Example:

```text
Host:
192.168.57.25

Service:
HTTP on 80/tcp

Observed evidence:
Nmap shows HTTP reachable. Host also exposes FTP and SSH.

Inference:
This may be a mixed Linux service target where web and FTP clues can reinforce each other.

Confidence:
Medium.

Validation needed:
Map HTTP title, redirects, routes, visible files, and relationship to FTP paths.

Next workflow owner:
Module 04 - Web Reconnaissance and Application Discovery.

Priority:
1.

Reason:
Web mapping is low-friction, safe, and likely to produce route or function evidence for later modules.
```

This entry is actionable. It tells the learner what to do next and why.

---

## Routing Services to Later Modules

The queue should use course workflows as owners.

| Service clue | Natural owner | Why |
|---|---|---|
| HTTP/HTTPS, redirects, certificates, route hints | Module 04 | web surface mapping |
| login surfaces, credential material, password policy clues | Module 06 | authentication and credential reasoning |
| hidden routes, parameters, content gaps | Module 07 | discovery and fuzzing |
| validated web weakness patterns | Module 08 | vulnerability reasoning |
| service-specific weakness patterns | Module 09 | attack playbooks |
| validated initial access path | Module 10 | foothold handling |
| Linux host context after access | Module 11 | Linux privilege escalation |
| Windows host context after access | Module 12 | Windows privilege escalation |
| indirect reachability or internal services | Module 13 | pivoting |
| domain, Kerberos, LDAP, trust, group, ACL clues | Module 14 | AD reasoning |
| evidence that may become a finding | Module 15 | reporting |

This routing prevents Module 03 from trying to own everything.

---

## Worked Queue: Baseline Hosts

### Queue item 1: Web on `META-TGT`

HTTP on the Linux target is often a strong immediate follow-up because it is visible, safe to map, and naturally belongs to Module 04.

```text
Observed:
80/tcp reachable on 192.168.57.25. Host also exposes FTP and SSH.

Inference:
The host may provide a web surface that correlates with file-transfer or Linux management context.

Validation needed:
Map title, redirects, visible routes, and any relationship between web paths and FTP-visible content.

Owner:
Module 04.

Priority:
High immediate priority.
```

### Queue item 2: Identity infrastructure on `GOAD-Mini-DC01`

The infrastructure host is high value, but not every action belongs immediately.

```text
Observed:
DNS, Kerberos, LDAP, SMB, and Windows RPC-style services exposed on 192.168.57.10.

Inference:
Host likely participates in Windows identity infrastructure and may be a domain controller.

Validation needed:
Preserve DNS, LDAP, SMB, and naming evidence. Deeper AD path analysis belongs later.

Owner:
Module 14 later, with supporting context from Module 06 if credentials appear.

Priority:
High strategic priority, but not necessarily first immediate action unless the next module needs identity context.
```

### Queue item 3: RDP on `GOAD-Mini-WS01`

RDP is important but likely credential-dependent.

```text
Observed:
3389/tcp reachable on 192.168.57.31.

Inference:
Host exposes remote interactive management. It may become useful after credentials exist.

Validation needed:
Capture certificate or NTLM naming clues. Revisit after credential discovery.

Owner:
Module 06 for credentials, Module 12 after access, Module 14 if domain context matters.

Priority:
Medium now, higher after credentials.
```

The queue now reflects timing, not just interest.

---

## What Makes a Queue Weak

A weak queue looks like this:

```text
1. SMB
2. FTP
3. RDP
4. DNS
5. HTTP
```

That is not a queue. It is a list of services.

A strong queue explains:

- host
- evidence
- interpretation
- confidence
- owner workflow
- reason for priority

The learner should be able to reopen the queue tomorrow and understand why the next step was chosen.

---

## Checkpoint

Open the module lab and complete Checkpoint D.

Build a follow-up queue with at least five entries:

1. one immediate web follow-up
2. one identity or AD-related follow-up
3. one credential-dependent revisit
4. one service-specific playbook candidate
5. one deferred or reference-only item

For each entry, include:

```text
Observed:
Inference:
Confidence:
Validation needed:
Owner:
Priority:
Reason:
```

The purpose is not to fill a form. The purpose is to practice defensible assessment decision-making.

---

## Key Takeaways

- Enumeration becomes useful when it changes the next step.
- Priority depends on timing, not only severity or excitement.
- A service queue should route work to the right later module.
- Some services are high strategic value but low immediate action.
- A strong queue preserves evidence, inference, validation, owner, and reason.

---

## Module Close-Out

Before leaving Module 03, the learner should have:

- host-role notes for the baseline hosts
- exact nouns captured from service evidence
- a completed service-role worksheet
- saved service output in the workspace
- a follow-up queue that prepares Module 04

Module 04 should not begin with "find websites."

It should begin with:

> Here are the web surfaces that Module 03 identified, here is why they matter, and here is what we need to map first.

That is the handoff.

