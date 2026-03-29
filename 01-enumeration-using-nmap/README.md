<div align="center">

# Hack the Basics — Enumeration Using Nmap

### Learn how to *think* with Nmap, not just run it.

*A premium, open-source, self-paced course on host discovery, port scanning, service profiling, and enumeration workflow design.*

</div>

---

## Overview

This course teaches **Enumeration using Nmap** as a disciplined workflow, not a collection of disconnected flags.

It is part of the broader **Hack the Basics** series and is designed for learners who want to build strong fundamentals in offensive security, lab work, and real-world technical reasoning.

Rather than treating Nmap as a one-command port scanner, this course shows you how to use it to:

- define scan scope intentionally
- discover hosts and exposed services
- interpret results correctly
- identify what you know vs. what you only suspect
- use NSE in a focused way
- build a repeatable enumeration workflow you can carry into later courses

---

## At a Glance

| Area | Details |
|---|---|
| **Series** | Hack the Basics |
| **Course** | Enumeration Using Nmap |
| **Format** | Open-source, self-paced, Markdown-first |
| **Level** | Beginner → early intermediate |
| **Primary Goal** | Build a real enumeration mindset and repeatable Nmap workflow |
| **Style** | Practical, structured, premium-feeling, GitHub-friendly |

---

## Who This Course Is For

This course is a strong fit if you are:

- getting started in offensive security or technical lab work
- learning how host discovery and service enumeration really work
- preparing for CTFs, HTB-style labs, or junior-level assessment workflows
- trying to move beyond “copy commands from cheat sheets” into actual understanding

This course is **not** built as a giant reference dump.
It is meant to be read in sequence, with each module preparing you for the next.

---

## What You’ll Learn

By the end of this course, you should be able to:

- explain what enumeration is and where Nmap fits in the workflow
- choose scan scope and scan types more intentionally
- understand the difference between host discovery, port scanning, service detection, and deeper enumeration
- interpret TCP and UDP results with better accuracy
- use version detection, OS detection, and NSE without treating output as magic
- document findings clearly and turn raw scan results into useful next steps
- build a phased, repeatable enumeration process for lab and real-world practice

---

## Course Path

The course is structured as a clean progression from foundations to workflow synthesis.

| Module | Focus |
|---|---|
| **Module 1** | Orientation, enumeration mindset, network mental models, and lab setup |
| **Module 2** | Host discovery, TCP/UDP scanning, port states, and scan reliability |
| **Module 3** | Service identification, version detection, OS detection, and network context |
| **Module 4** | Nmap Scripting Engine (NSE) and deeper targeted enumeration |
| **Module 5** | Real enumeration workflows for common service families and output handling |
| **Module 6** | Constraints, performance tradeoffs, troubleshooting, and capstone synthesis |

<details>
<summary><strong>Why this order?</strong></summary>

The sequence is intentional.

You first learn how to think about enumeration, then how Nmap actually discovers hosts and ports, then how to interpret what those results mean, then how to deepen that understanding with NSE, and finally how to combine everything into a real workflow.

That progression matters because Nmap is easy to use badly.
This course is designed to build judgment, not just command familiarity.

</details>

---

## How to Use This Repository

### Recommended approach

1. Start at the beginning and move through the modules in order.
2. Treat each lesson as part of a larger workflow, not an isolated note.
3. Run the example commands in your own lab when possible.
4. Take notes on what Nmap is actually telling you, not just what command you ran.
5. Revisit later modules as reference once you complete the course once front-to-back.

### Best experience

You will get the most out of this course if you:

- have a small lab or VM environment to practice in
- compare scan results across multiple runs
- save outputs and keep notes on interpretation
- use the repo as both a course and a long-term field reference

---

## Repository Structure

```text
.
├── README.md
├── module-01-orientation-and-foundations/
├── module-02-discovery-and-port-scanning-mechanics/
├── module-03-service-version-and-os-enumeration/
├── module-04-nse-and-deeper-enumeration/
├── module-05-building-real-enumeration-workflows/
├── module-06-constraints-advanced-usage-and-synthesis/
├── labs/
├── assets/
└── reference/
```

Each module folder is expected to contain lesson files in reading order, along with any supporting diagrams, examples, or guided practice material.

---

## What Makes This Course Different

Most beginner Nmap content focuses on flags.
This course focuses on **reasoning**.

That means we care about:

- why you are running a scan
- what assumptions the scan makes
- how reliable the result is
- what the output actually implies
- what the next step should be

The goal is not to memorize commands.
The goal is to build a technical workflow you can trust.

---

## Prerequisites

You do **not** need deep prior experience.

Helpful starting knowledge:

- basic comfort using a terminal
- very light networking familiarity
- willingness to work through results carefully

If you are early in your journey, that is fine.
This course is designed to help build the mental models that later offensive security work depends on.

---

## Lab Mindset

This course assumes practice in environments you own, control, or are explicitly authorized to test.

Use a small personal lab, local VMs, or approved training environments where you can safely observe how scan choices affect results.

---

## Start Here

If you are beginning the course for the first time:

- go to **Module 1**
- complete the lessons in order
- set up your lab early
- keep a notebook or Markdown file for scan observations

If you are returning later as a reference:

- jump directly to the relevant module
- use the **reference/** material alongside lesson content
- compare new findings against the workflow patterns taught earlier in the course

---

## In the Context of Hack the Basics

**Hack the Basics** is meant to build strong foundational skill in a way that still feels serious, structured, and technically honest.

This Nmap course is one of the early building blocks in that journey.
It teaches the kind of enumeration discipline that later work depends on, whether that later work involves web testing, internal infrastructure, Active Directory, service analysis, or broader offensive security workflows.

---

## Status

This repository is being developed as a structured self-paced course.
Lessons, labs, diagrams, and reference material may be added iteratively over time.

---

<div align="center">

**Start with Module 1 and build the habit of intentional enumeration.**

</div>
