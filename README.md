<div align="center">

# Hack the Basics

*An open-source, self-paced course designed to teach offensive security as a progression of reasoning, evidence, and workflow, not a pile of disconnected tools.*

</div>

---

> **🧭 Start Here**
>
> If you are new to the project, read this page first, then go to [Module 01 - Orientation and Assessment Workflow](modules/01-orientation-and-assessment-workflow/README.md). If you want the full source-of-truth curriculum and repository plan, open the [master implementation blueprint](hack-the-basics-implementation-blueprint.md).

## What This Project Is

`Hack the Basics` is a structured offensive security course for learners who want more than scattered notes, one-off walkthroughs, and command-copying habits.

The course is built around a simple idea:

> teach the basics without making them feel basic

That means the repository is designed to feel:

- progressive instead of random
- technical without becoming overwhelming
- practical without becoming shallow
- open-source while still feeling deliberate, polished, and premium

The goal is not just to teach what to type.
The goal is to teach how to think through an assessment from beginning to end.

---

## Why This Exists

Most beginner-friendly offensive security content breaks down in one of two ways:

- it teaches commands without enough systems understanding
- it teaches topics in an order that does not match how real assessments actually unfold

`Hack the Basics` is meant to fix that by teaching a cleaner workflow:

1. orient to the assessment
2. map the visible surface
3. understand what exposed services and applications mean
4. analyze credentials, trust, and validation paths
5. gain and operate through footholds carefully
6. escalate, pivot, and expand visibility
7. document and report the work professionally

---

## The Course

By the end of the course, the learner should be able to move through a realistic lab assessment while explaining:

- what they observed
- what they inferred
- what they validated
- why the next step made sense

This course is designed to produce:

- stronger mental models
- cleaner workflow habits
- more trustworthy technical reasoning
- reusable notes, worksheets, maps, and references

---

## What Makes It Different

| Instead of.. | We are building.. |
|---|---|
| Tool-first learning | Workflow-first learning |
| Memorizing flags | Understanding systems |
| One-off tricks | Transferable methodology |
| Random topic order | Progressive prerequisites |
| "Run this exploit" | "Explain why this is the next step" |
| Loose notes repo | A designed course experience |

> **🧠 Mental Model**
>
> Tools matter in this course, but tools are never the curriculum.
> The curriculum is the sequence of questions, evidence, and decisions that make technical work meaningful.

---

## Who This Is For

This course is a strong fit for learners who want to:

- move from curiosity into structured lab-based learning
- understand how offensive assessments actually flow
- build strong fundamentals before specializing
- connect enumeration, exploitation, escalation, movement, and reporting into one coherent system
- learn in a way that rewards notes, repetition, and technical honesty

This project is not meant to be:

- hype-driven
- shortcut-first
- an "instant hacker" repo
- a giant exploit catalog

It is meant to be a serious foundation.

---

## Learning Journey

The course is organized around one full offensive workflow.
Each phase has a clear job.
Each phase prepares the next one.

| Phase | Focus | What the learner is building |
|---|---|---|
| **I** | Orientation and surface mapping | Lab workflow, assessment mindset, network visibility, service reasoning |
| **II** | Web understanding and exposure analysis | Web discovery, traffic analysis, auth context, fuzzing, and core web attack thinking |
| **III** | Access and foothold operations | Common service attack paths, shells, payloads, and initial-access handling |
| **IV** | Local escalation and internal movement | Linux, Windows, pivoting, and deeper internal visibility |
| **V** | Enterprise reasoning, communication, and synthesis | Active Directory reasoning, reporting discipline, and capstone execution |

<details>
<summary><strong>Why this structure?</strong></summary>

A learner can memorize commands quickly and still have no idea how to operate during a real assessment.

This series is structured to prevent that.

We start with orientation and attack-surface mapping, move into web understanding and exposure analysis, then into access and foothold operations, then local escalation and internal movement, and finally into enterprise reasoning, reporting, and full-course synthesis.

</details>

---

## Course Roadmap

### Phase I - Orientation and Surface Mapping

| Module | Focus |
|---|---|
| [01. Orientation and Assessment Workflow](modules/01-orientation-and-assessment-workflow/README.md) | Course workflow, assessment lifecycle, scope discipline, and analyst mindset |
| [02. Network Enumeration with Nmap](modules/02-enumeration-using-nmap/README.md) | Host discovery, port scanning, service clues, and repeatable attack-surface mapping |
| [03. Service Footprinting and Common Infrastructure Enumeration](modules/03-service-footprinting-and-common-infrastructure-enumeration/README.md) | Turning ports into host-role, service, and follow-up understanding |

### Phase II - Web Understanding and Exposure Analysis

| Module | Focus |
|---|---|
| [04. Web Reconnaissance and Application Discovery](modules/04-web-reconnaissance-and-application-discovery/README.md) | Web asset mapping, fingerprinting, and first-pass discovery |
| [05. Web Proxies and HTTP Traffic Analysis](modules/05-web-proxies-and-http-traffic-analysis/README.md) | Inspecting, replaying, modifying, and reasoning about HTTP traffic |
| [06. Authentication, Credentials, and Password Operations](modules/06-authentication-credentials-and-password-operations/README.md) | Login surfaces, password logic, credential operations, and auth as a cross-cutting attack surface |
| [07. Web Content Discovery and Fuzzing](modules/07-web-content-discovery-and-fuzzing/README.md) | Hidden routes, parameters, vhosts, and systematic web surface expansion |
| [08. Core Web Vulnerabilities and Exploit Chains](modules/08-core-web-vulnerabilities-and-exploit-chains/README.md) | Foundational web vulnerability classes and exploit-chain reasoning |

### Phase III - Access and Foothold Operations

| Module | Focus |
|---|---|
| [09. Attacking Common Services and Applications](modules/09-attacking-common-services-and-applications/README.md) | Applying attack-path reasoning to frequently encountered services and exposed apps |
| [10. Footholds, Shells, Payloads, and File Operations](modules/10-footholds-shells-payloads-and-file-operations/README.md) | Initial execution, shell handling, payload choice, and practical post-access workflow |

### Phase IV - Local Escalation and Internal Movement

| Module | Focus |
|---|---|
| [11. Linux Privilege Escalation](modules/11-linux-privilege-escalation/README.md) | Local enumeration and privilege boundary reasoning on Linux |
| [12. Windows Privilege Escalation](modules/12-windows-privilege-escalation/README.md) | Local Windows context, privilege, configuration, and escalation patterns |
| [13. Pivoting, Tunneling, and Port Forwarding](modules/13-pivoting-tunneling-and-port-forwarding/README.md) | Reaching internal-only services and moving through segmented environments |
| [14. Active Directory Enumeration and Attacks](modules/14-active-directory-enumeration-and-attacks/README.md) | Identity, trust, delegated privilege, and enterprise attack-path reasoning |

### Phase V - Enterprise Reasoning, Communication, and Synthesis

| Module | Focus |
|---|---|
| [15. Documentation, Reporting, and Assessment Communication](modules/15-documentation-reporting-and-assessment-communication/README.md) | Turning technical work into notes, evidence, findings, and professional communication |
| [16. Attacking Enterprise Networks Capstone](modules/16-attacking-enterprise-networks-capstone/README.md) | A start-to-finish simulated engagement that ties the full series together |

---

## What the Repository Is Meant to Contain

As the course is built out, the repository is intended to include:

- module landing pages
- lesson files
- guided labs
- diagrams and screenshots
- field references and cheat sheets
- worksheets and note-taking aids
- reporting templates
- capstone materials

The repo is meant to work in two modes at once:

- as a sequential course
- as a long-term reference set learners can return to later

---


## Useful Entry Points

| If you want to... | Start here |
|---|---|
| begin the course as a learner | [Module 01](modules/01-orientation-and-assessment-workflow/README.md) |
