<div align="center">

# Hack the Basics

### Build real offensive security fundamentals — the right way, in the right order.

*An open-source, self-paced course built to teach offensive security as a progression of thinking, not a pile of disconnected tools.*

</div>

---

## What This Project Is

**Hack the Basics** is a structured offensive security course series designed for learners who want more than scattered notes, isolated walkthroughs, or copy-paste commands.

It is built around a simple idea:

> teach the basics without making them feel basic.

That means the course is designed to feel:

- **progressive** instead of random
- **technical** without becoming overwhelming
- **practical** without becoming shallow
- **open-source** while still feeling polished, intentional, and premium

This repository is the home for that learning journey.

---

## What We Are Building

Most beginner-friendly security content tends to break down in one of two ways:

- it gives learners commands without enough systems understanding
- it introduces tools and topics in an order that does not match how real assessments actually unfold

**Hack the Basics** is meant to fix that.

This series is being built as a **deliberate learning path** that follows the shape of real offensive work:

1. orient to the workflow
2. map the attack surface
3. understand exposed services and applications
4. analyze authentication and trust boundaries
5. validate weaknesses carefully
6. gain and operate through footholds in a lab setting
7. escalate, pivot, and expand visibility
8. document the work like a professional

The goal is not just to teach *what to type*.

The goal is to teach learners how to think through an assessment from beginning to end.

---

## The Philosophy Behind the Series

| Instead of this... | We are building this... |
|---|---|
| Tool-first learning | Workflow-first learning |
| Memorizing flags | Understanding systems |
| One-off tricks | Transferable methodology |
| Random topic order | Progressive prerequisites |
| “Run this exploit” | “Explain why this is the next step” |
| Loose notes repo | A designed course experience |

That difference is the point of the project.

---

## Who This Is For

**Hack the Basics** is for learners who are serious about building offensive security skill the right way, even if they are still early in that journey.

It is a strong fit for people who want to:

- move from curiosity into structured, lab-based learning
- understand how technical assessments actually flow
- build real fundamentals before diving deeper into specialized areas
- connect enumeration, exploitation, escalation, and reporting into one coherent process
- learn in a way that rewards good notes, repetition, and technical honesty

This is not meant to be a hype-driven “instant hacker” repo.
It is meant to be a clean, serious foundation.

---

## What Makes It Different

### It is built like a course.

Each module should prepare the learner for the next one.
The order matters.
The pacing matters.
The transitions matter.

### It treats fundamentals as serious work.

“Basics” here does **not** mean watered down.
It means learning the material that everything else depends on:

- enumeration
- service reasoning
- web behavior
- authentication and credential logic
- shells and operating system context
- privilege boundaries
- pivoting and internal expansion
- evidence handling and reporting

### It puts tools inside workflows.

Tools matter, but tools are not the curriculum.
Wherever possible, tools are taught inside a larger question:

- what problem is this tool helping solve?
- why does it belong here in the workflow?
- how much confidence should we place in the result?
- what should happen next?

### It is open-source, but it should still feel premium.

The writing, diagrams, labs, notes, and progression should feel designed.
The learner should feel like they are moving through a structured experience, not browsing a folder full of fragments.

---

## The Learning Journey

The new course spine is designed around a full offensive workflow.
Each phase has a job.
Each phase builds the next one.

| Phase | Focus | What the learner is building |
|---|---|---|
| **Phase I** | Orientation and attack-surface mapping | Lab workflow, assessment mindset, network visibility, service reasoning |
| **Phase II** | Web understanding and exposure analysis | Web discovery, traffic analysis, auth context, fuzzing, and core web attack thinking |
| **Phase III** | Access and platform operations | Common service attack paths, shells, payloads, and foothold management |
| **Phase IV** | Escalation and internal expansion | Linux, Windows, pivoting, and enterprise movement |
| **Phase V** | Professional output and synthesis | Active Directory reasoning, reporting discipline, and end-to-end capstone execution |

<details>
<summary><strong>Why this structure?</strong></summary>

A learner can memorize commands quickly and still have no idea how to operate during a real assessment.

This series is structured to prevent that.

We start with orientation and surface mapping, then move into application understanding, then access and foothold operations, then privilege and internal expansion, and finally into professional deliverables and enterprise reasoning.

That is how the series stays approachable **without** becoming shallow.

</details>

---

## Course Roadmap

The roadmap below reflects the current implementation blueprint for the full course.
It is intentionally high-level on the landing page: enough to show the journey, without turning the README into a giant syllabus.

### Phase I — Orientation and Surface Mapping

| Module | Focus |
|---|---|
| **01. Orientation and Assessment Workflow** | How the course works, how assessments flow, how to think, and how to build a repeatable learner workflow |
| **02. Network Enumeration with Nmap** | Host discovery, port scanning, service detection, output interpretation, and repeatable attack-surface mapping |
| **03. Service Footprinting and Common Infrastructure Enumeration** | Turning ports into actual understanding across common enterprise services and infrastructure protocols |

### Phase II — Web Understanding and Exposure Analysis

| Module | Focus |
|---|---|
| **04. Web Reconnaissance and Application Discovery** | Web asset mapping, content discovery, fingerprinting, and first-pass web context gathering |
| **05. Web Proxies and HTTP Traffic Analysis** | Inspecting, replaying, modifying, and reasoning about requests and responses |
| **06. Authentication, Credentials, and Password Operations** | Login surfaces, password logic, credential operations, and authentication as a cross-cutting attack surface |
| **07. Web Content Discovery and Fuzzing** | Directories, parameters, virtual hosts, hidden routes, and systematic web surface expansion |
| **08. Core Web Vulnerabilities and Exploit Chains** | Foundational web vulnerability classes and how to reason about exploiting and chaining them |

### Phase III — Access and Platform Operations

| Module | Focus |
|---|---|
| **09. Attacking Common Services and Applications** | Applying attack-path reasoning to frequently encountered services, platforms, and exposed applications |
| **10. Footholds, Shells, Payloads, and File Operations** | Initial execution, shells, payload choices, session handling, and practical post-foothold operations |

### Phase IV — Escalation and Internal Expansion

| Module | Focus |
|---|---|
| **11. Linux Privilege Escalation** | Local enumeration, misconfigurations, and privilege boundary reasoning on Linux |
| **12. Windows Privilege Escalation** | Local Windows context, services, permissions, credentials, and privilege escalation patterns |
| **13. Pivoting, Tunneling, and Port Forwarding** | Reaching internal-only services and moving through segmented environments after a foothold |
| **14. Active Directory Enumeration and Attacks** | Identity, trust, privilege relationships, graph-based reasoning, and enterprise attack paths |

### Phase V — Professional Output and Capstone Synthesis

| Module | Focus |
|---|---|
| **15. Documentation, Reporting, and Assessment Communication** | Turning technical work into notes, evidence, findings, and professional communication |
| **16. Attacking Enterprise Networks Capstone** | A start-to-finish simulated engagement that ties the entire series together |

---

## What the Repository Will Eventually Contain

As the course is built out, this repository is intended to include:

- module overviews
- lesson files
- guided labs
- screenshots and diagrams
- command walkthroughs
- reference notes and cheat sheets
- templates for notes, findings, and reporting
- capstone materials and supporting artifacts

The goal is for the repo to be useful in two ways at once:

- as a **sequential learning path**
- and later, as a **high-quality reference** learners can return to while practicing

---

## Build Principles

The implementation blueprint for the series is guided by a few simple rules:

- new domains begin with a **how it works** lesson before tactics
- enumeration comes before exploitation
- repeated ideas should return with **more depth**, not just repetition
- tool coverage should support a workflow, not replace one
- every module should create a natural handoff into the next module
- the course should remain GitHub-friendly, readable, and easy to expand over time

---

## Current Direction

This repository is being built around a full implementation blueprint with:

- a locked module spine
- module-by-module lesson structure
- topic and sub-topic breakdowns
- practice placement strategy
- a progression designed for self-paced learners

So while the course is open-source, it is being designed with the same seriousness you would expect from a premium training product.

---

<div align="center">

### Hack the Basics is about learning the craft in the right order.

**Strong fundamentals. Clean workflows. Serious progression.**

</div>
