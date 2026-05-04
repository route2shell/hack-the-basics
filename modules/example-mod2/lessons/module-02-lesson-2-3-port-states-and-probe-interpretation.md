# Lesson 2.3 - Port States and Probe Interpretation

---

> **Lesson Objective**
>
> Learn to read TCP, UDP, and ambiguous port states as scanner interpretations of probe behavior, not absolute truths about the target.

| Course | Module | Lesson | Type | Estimated time |
|---|---|---|---|---:|
| Hack the Basics | 02 - Map the Visible Network | 2.3 | Tactical lesson | 55-75 min |

| You have | You will produce | Lab checkpoint |
|---|---|---|
| live-host set | saved TCP and selected UDP triage output | Checkpoint C |

---

## Why This Lesson Matters

Port states are where many learners start overclaiming.

They see `open` and think "vulnerable." They see `closed` and think "irrelevant." They see `filtered` and think "firewall confirmed." They see no UDP response and think "nothing there."

Those interpretations are too strong.

A port state is Nmap's label for what a probe appeared to show from the scanner's position. That label is useful, but it is still shaped by the target, the network path, packet loss, filtering, timing, and the specific scan type.

The learner needs to understand what the label means before deciding what to do next.

---

## TCP Feels Clearer Because It Talks More

TCP scanning often feels clearer than UDP scanning because TCP has more visible conversation structure.

When a TCP service accepts the start of a connection, the scanner often receives a response consistent with an open port. When no service is listening, the target may reject the attempt. When something blocks visibility, the scanner may receive no decisive reply or a filtering-related message.

That is why TCP triage is a practical starting point.

But even with TCP, the learner should keep the language careful:

```text
Port 80 appears open from Kali WSL.
```

is stronger and more accurate than:

```text
Port 80 is definitely open to everyone.
```

The scan result belongs to a position and a probe.

---

## UDP Is Ambiguous by Nature

UDP does not provide the same conversation structure. Some UDP services reply. Some stay silent until given a specific valid payload. Some filtering paths also produce silence. Some networks rate-limit ICMP errors.

That means silence in UDP is especially difficult.

If Nmap reports `open|filtered`, it is not being indecisive because it is poorly designed. It is reflecting a real evidence problem: the observed behavior does not cleanly distinguish an open silent service from filtering.

This is why UDP scanning should be deliberate.

The learner should ask:

- Which UDP services matter for this host role?
- Is a broad UDP scan worth the time and ambiguity?
- Would a focused check answer a better question?
- Does Module 03 need this result now?

---

## Common State Meanings

Once the caution is clear, the state labels are useful.

| State | Careful interpretation |
|---|---|
| `open` | the port responded as though a service accepts this probe |
| `closed` | the target/path responded, but no service appears to listen there |
| `filtered` | Nmap could not get a decisive answer, likely because visibility was blocked or unclear |
| `open|filtered` | Nmap cannot distinguish open silence from filtering |
| `unfiltered` | the path appears reachable for that probe, but open/closed is not clear |

The wording matters because it shapes later notes.

---

## SYN, Connect, UDP, and ACK Scans

The main scan types in this lesson answer different questions.

### SYN scan

```bash
nmap -sS <target>
```

A SYN scan is a strong default TCP triage method when raw packet scanning is available. It tests whether ports appear willing to start a TCP conversation.

### Connect scan

```bash
nmap -sT <target>
```

A connect scan asks the operating system to attempt a normal TCP connection. It is useful when SYN scanning is not available, but it usually completes connections to open ports and may create different logs.

### UDP scan

```bash
sudo nmap -sU <target>
```

UDP scanning asks a harder question. Use it with narrower intent and careful interpretation.

### ACK scan

```bash
nmap -sA <target>
```

ACK scanning is often more about filtering behavior than discovering open services. It can help test whether a path returns resets or appears filtered, but it should not be treated like a normal open-port scan.

The point is not to memorize flags. The point is to understand what evidence each scan type can and cannot produce.

---

## Worked Example: Same Host, Different Evidence

Suppose TCP triage on `META-TGT` reports:

```text
21/tcp open
22/tcp open
80/tcp open
```

A useful first interpretation is:

```text
FTP, SSH, and HTTP appear reachable from Kali WSL. This host likely deserves service enrichment and Module 03 follow-up for file transfer, management, and web exposure.
```

Now suppose a UDP scan against `GOAD-Mini-DC01` reports a mix of `open`, `closed`, and `open|filtered`.

The stronger note is not:

```text
UDP is weird.
```

It is:

```text
UDP triage produced ambiguous results on DC01. Any `open|filtered` labels should be treated as uncertain and followed only where a specific service question matters, such as DNS. Broad UDP ambiguity should not distract from stronger TCP identity-service evidence.
```

That note chooses the next move.

---

## What Not to Overclaim

| Weak claim | Better framing |
|---|---|
| `open` means vulnerable | `open` means the port appears to accept this probe |
| `closed` means useless | `closed` can still prove host/path reachability |
| `filtered` means firewall confirmed | `filtered` means visibility was blocked or unclear from this scan |
| UDP silence means nothing exists | UDP silence is ambiguous |
| ACK scan found open ports | ACK scan often speaks more to filtering/reachability than service openness |

This is not pedantry. It is technical honesty.

---

## Checkpoint

Open the module lab and complete Checkpoint C.

Run saved TCP triage scans and at least one deliberate UDP or filtering-related check if it supports a real question.

For each result, write:

```text
Observed:

Inference:

Ambiguity:

Validation needed:
```

The key is to explain what the state labels actually support.

---

## Key Takeaways

- Port states are scanner labels based on observed probe behavior.
- TCP often gives clearer first-pass evidence than UDP.
- UDP silence is ambiguous and should be handled carefully.
- Different scan types answer different questions.
- Strong notes use careful language like "appears," "reported," and "from this position."

---

## Next Lesson Bridge

Port states tell us where conversations may be possible.

The next lesson asks what may be behind those ports: service names, versions, scripts, certificates, titles, OS hints, and other clues that Module 03 can interpret.

