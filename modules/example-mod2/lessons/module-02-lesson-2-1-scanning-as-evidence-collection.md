# Lesson 2.1 - Scanning as Evidence Collection

---

> **Lesson Objective**
>
> Learn to treat Nmap scanning as a controlled evidence process: define a question, send probes, observe behavior, infer carefully, and validate before overclaiming.

| Course | Module | Lesson | Type | Estimated time |
|---|---|---|---|---:|
| Hack the Basics | 02 - Map the Visible Network | 2.1 | Anchor lesson | 55-75 min |

| You have | You will produce | Lab checkpoint |
|---|---|---|
| Module 01 lab and workspace | first scan question and output path | Checkpoint A |

---

## Why This Lesson Matters

This is the first module where the learner uses the course lab to ask live technical questions.

That makes the first habit important.

A weak habit is to treat Nmap like a vending machine: type a familiar command, receive a table, copy the open ports, and move on. That approach can work in a small lab by accident, but it does not teach reliable assessment thinking.

A stronger habit is to treat each scan as an evidence-gathering action.

Every scan has a position, a scope, a probe type, a target set, an output location, and an interpretation boundary. The output does not say "here is the full truth about the target." It says, "from this position, these probes produced these responses, and Nmap classified them this way."

That distinction is the center of this module.

---

## The Core Mental Model

Scanning follows a simple loop:

```text
Probe -> Observe -> Infer -> Validate
```

The loop is simple, but it changes how the learner reads every result.

### Probe

A probe is intentional traffic. It might be ARP, ICMP, TCP, UDP, a version-detection payload, or a script-driven protocol interaction.

The probe matters because different probes ask different questions. ARP on a local network asks a different question than a TCP SYN to port 445. A UDP packet asks a different question than a TCP connect attempt. A version-detection probe asks a different question than a simple port-state check.

If we do not know what question the probe asked, we cannot interpret the answer well.

### Observe

Observation is what came back, or did not come back.

An ARP reply, TCP SYN/ACK, TCP RST, ICMP unreachable, banner, TLS certificate, script response, delayed reply, or silence can all become evidence.

Silence deserves special respect. Silence can mean the host is down, the service is filtered, the application ignores the probe, the network path dropped the packet, or the scan timing missed the response.

### Infer

Inference is where Nmap and the operator assign meaning.

Nmap may label a host up, a port open, a port closed, or a port filtered. The operator may infer that the host is likely Windows, that a service deserves SMB follow-up, or that a web service should be mapped in Module 04.

Inference is necessary. It is also where overclaiming starts if the learner is careless.

### Validate

Validation is the follow-up that strengthens, corrects, or limits the inference.

If Nmap says HTTP is open, validation might mean a browser request, `curl`, a focused script, or later web mapping. If a UDP port is silent, validation might mean a narrower UDP scan, packet capture, or simply recording that the result is ambiguous.

What this changes:

> Scan output should create better questions, not premature conclusions.

---

## What Nmap Actually Gives Us

Nmap gives us structured observations and labels that help prioritize work.

It may help answer:

- which hosts appear alive
- which ports appear open, closed, or filtered
- which service might be listening
- which version or product clues appear
- which scripts produce useful protocol context
- which hosts deserve deeper follow-up

It does not directly prove:

- that a service is vulnerable
- that a host has no hidden services
- that a firewall is definitely present
- that a banner is fully accurate
- that an operating system guess is certain
- that a login surface can be accessed

This is why the course keeps separating observation from inference.

Weak note:

```text
Firewall blocks most ports.
```

Stronger note:

```text
Nmap reports many ports as filtered from Kali WSL. Filtering is likely, but the scan does not identify whether the cause is host firewalling, network controls, dropped probes, or timing. Focused validation is needed before making stronger claims.
```

The stronger note is not longer for style. It is longer because it is more accurate.

---

## Scanning as a Sequence of Questions

A useful scan workflow starts with questions, not flags.

At the beginning of Module 02, the questions are:

1. Which addresses are in scope?
2. Which hosts appear alive from Kali WSL?
3. Which ports respond on those hosts?
4. Which services appear behind the open ports?
5. Which results should Module 03 inspect first?

Nmap flags are tools for answering those questions.

If the learner starts with `nmap -A -p-` before defining the question, they may collect output, but they have not built a workflow. They have made the tool do a lot of work before deciding what evidence they need.

The course should train the opposite habit:

```text
Question first.
Probe second.
Output saved.
Interpretation written.
Next step chosen.
```

---

## Worked Example: The First Scan Question

Suppose your Module 01 notes say the lab network is `192.168.57.0/24` and you expect three hosts:

- `192.168.57.10`
- `192.168.57.25`
- `192.168.57.31`

The first scan question is not:

> How do I run Nmap?

It is:

> Do the expected lab hosts appear reachable from Kali WSL right now?

That question suggests a discovery scan, saved output, and a host-tracking update.

The scan might be:

```bash
nmap -sn -oA "$M2SCAN"/lab-discovery-YYYY-MM-DD 192.168.57.0/24
```

If all expected hosts appear up, the inference is simple but still scoped:

```text
The expected baseline hosts appear reachable from Kali WSL using this discovery pass.
```

If one expected host is missing, the correct conclusion is not immediately "host down." The stronger note is:

```text
The host was not reported up by this discovery method. Validate power state, IP assignment, VMware network attachment, and whether the host ignores this probe type before treating it as unavailable.
```

That is the scan mindset this module teaches.

---

## Checkpoint

Open the module lab and complete Checkpoint A.

Write:

```text
Network position:

Approved scope:

First scan question:

Expected baseline:

Output path:
```

Do not run the discovery scan until those fields are clear.

The goal is to make the scan intentional before it becomes technical.

---

## Key Takeaways

- Nmap is an evidence instrument, not an oracle.
- Every scan should start with a question.
- Probe behavior becomes observation; observation supports inference; inference requires validation.
- Silence and filtering need careful language.
- Saved output is part of the assessment record from the beginning.

---

## Next Lesson Bridge

Now that we know what a scan is trying to prove, we need to define exactly who or what we are asking about.

The next lesson teaches target definition and host discovery: how to choose the right target form, discover live hosts, and preserve the first visible map of the lab.

