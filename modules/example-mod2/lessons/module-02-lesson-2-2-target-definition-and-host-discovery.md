# Lesson 2.2 - Target Definition and Host Discovery

---

> **Lesson Objective**
>
> Learn to define targets deliberately and discover live hosts without confusing a discovery result for complete truth.

| Course | Module | Lesson | Type | Estimated time |
|---|---|---|---|---:|
| Hack the Basics | 02 - Map the Visible Network | 2.2 | Workflow lesson | 45-65 min |

| You have | You will produce | Lab checkpoint |
|---|---|---|
| scan question and output path | saved discovery output and live-host notes | Checkpoint B |

---

## Why This Lesson Matters

Most scanning mistakes start before the scan runs.

If the target set is wrong, the output is wrong in a practical sense even if Nmap performs perfectly. If the learner scans too broadly, they may leave scope. If they scan too narrowly, they may miss hosts the module depends on. If they fail to save target lists, later scans become inconsistent and hard to compare.

Target definition is not administrative overhead. It is how the learner turns scope into a technical question.

Host discovery then asks a visibility question:

> Which hosts appear alive from this position using this discovery method?

That wording matters. Discovery is vantage-point dependent. A host that appears silent to one method may respond to another. A host that blocks ICMP may answer TCP. A local subnet may reveal hosts through ARP. A filtered environment may hide almost everything until the learner chooses a different approach.

The lesson is simple: define the target set carefully, then interpret discovery as evidence, not certainty.

---

## Target Definition Is Part of Scope Discipline

The approved target set lives in notes before it lives in a command.

If your scope says `192.168.57.0/24`, then a CIDR scan can be appropriate. If your scope names only three hosts, a short list may be better. If one host is temporarily excluded, the command should reflect that.

Nmap supports many target forms:

```bash
nmap 192.168.57.25
nmap 192.168.57.0/24
nmap 192.168.57.10,25,31
nmap -iL "$M2SCAN"/targets.txt
nmap 192.168.57.0/24 --exclude 192.168.57.31
```

The learner should not memorize these as random formats. Each form expresses a different scope decision.

What this changes:

> The target expression in the command should match the assessment question in the notes.

---

## Host Discovery Is About Reachability From Here

Host discovery asks whether a host appears alive before deeper port scanning.

On a local lab network, ARP-based discovery is often strong because local Ethernet behavior can reveal hosts even when ICMP is blocked. In other environments, ICMP, TCP SYN probes, TCP ACK probes, or UDP probes may behave differently.

The default beginner mistake is to assume discovery silence means absence.

That is unsafe. Silence may mean:

- the host is down
- the host ignores the selected probe
- filtering blocks the probe or response
- the target is on a different segment
- the VM is misconfigured
- the scan was run from the wrong network position

This is why discovery output should be written carefully.

Weak note:

```text
Only three hosts exist.
```

Stronger note:

```text
Discovery scan from Kali WSL reported three expected baseline hosts up on 192.168.57.0/24. This supports the current lab baseline but does not prove no other hosts exist unless scope and discovery method support that claim.
```

---

## The Discovery Pass

For the course baseline, a saved discovery pass is a good first move:

```bash
nmap -sn -oA "$M2SCAN"/lab-discovery-YYYY-MM-DD 192.168.57.0/24
```

The command asks:

> Which hosts in the lab subnet appear alive without doing a port scan?

The `-oA` output matters because discovery results become the foundation for later scans. If they are not saved, the learner either trusts memory or repeats work.

After the scan, the learner should record:

- which hosts were reported up
- which expected hosts were missing
- what discovery method was used
- what needs validation

That turns output into an assessment artifact.

---

## Preserving the Live-Host Set

A live-host set is a working target list, not a permanent truth.

It should be saved so future scans can use the same input:

```bash
printf "192.168.57.10\n192.168.57.25\n192.168.57.31\n" > "$M2SCAN"/targets.txt
```

In a real workflow, you might generate that file from output. In this course, the important habit is consistency: the same host set should be reusable across triage, enrichment, notes, and follow-up.

If the learner adds or removes a host, the note should say why.

Example:

```text
192.168.57.31 was expected but not reported up in the first discovery pass. I am not adding it to targets.txt until VM power state and network attachment are validated.
```

That note protects the workflow.

---

## Worked Example: Discovery Changes the Plan

Suppose the discovery scan reports:

```text
192.168.57.10 up
192.168.57.25 up
```

but `192.168.57.31` is expected and missing.

A rushed learner might start scanning only the two visible hosts. A more careful learner pauses.

The right question is:

> Is `GOAD-Mini-WS01` actually down, or did this discovery method fail to see it?

The next step may be:

- check VMware power state
- check IP assignment
- check host-only network attachment
- try a targeted probe
- use `-Pn` only after deciding to treat the host as up for port scanning

The lesson is not "always use `-Pn`." The lesson is "know why you are using it."

---

## Checkpoint

Open the module lab and complete Checkpoint B.

Run a saved discovery pass, create or update `targets.txt`, and update `host-tracking.md`.

Your note should answer:

```text
Which hosts appeared alive?

Which expected hosts were missing?

What discovery method was used?

What uncertainty remains?

What target set will be used for triage?
```

---

## Key Takeaways

- Target definition is scope translated into a command.
- Host discovery reports visibility from a position; it does not prove universal absence.
- `-Pn` is a deliberate choice, not a default shortcut.
- Live-host sets should be preserved so later scans are comparable.
- Good discovery notes record uncertainty as well as results.

---

## Next Lesson Bridge

Now that we have a target set, we can ask what each host exposes.

The next lesson teaches port-state interpretation: how TCP and UDP probes produce labels like `open`, `closed`, and `filtered`, and how to read those labels without overclaiming.

