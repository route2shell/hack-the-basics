# Hack the Basics — Implementation Blueprint

## 1. Document Purpose

This document is the master implementation blueprint for the full **Hack the Basics** series. It is not a learner-facing README and it is not lesson prose. It is the structural source of truth used to build the course from beginning to end.

It reflects the design rules in `course-outline.md`: progressive sequencing, self-paced scaffolding, clean module roles, strong prerequisite flow, meaningful lesson titles, practice integration, and enough detail that future lesson authors can expand each lesson into a complete file without inventing the curriculum as they go. fileciteturn15file0 fileciteturn15file3 fileciteturn15file4

It also preserves the substance of the original source modules—Nmap, footprinting, web recon, web proxies, fuzzing, credentials, SQLi, XSS, file inclusion, file uploads, command injection, common services, shells and payloads, file transfers, privilege escalation, pivoting, Active Directory, reporting, and the final enterprise capstone—while reorganizing them into a more cohesive learning journey.

---

## 2. Locked Course Spine

| # | Module | Role in the Journey |
|---|---|---|
| 01 | Orientation and Assessment Workflow | Sets the operating model, scope mindset, lab rhythm, and how the whole course fits together |
| 02 | Network Enumeration with Nmap | Teaches host discovery, port scanning, service detection, interpretation, and repeatable network mapping |
| 03 | Service Footprinting and Common Infrastructure Enumeration | Moves from ports to actual service understanding across common enterprise protocols |
| 04 | Web Reconnaissance and Application Discovery | Begins the contiguous web track with surface mapping, discovery, and web context gathering |
| 05 | Web Proxies and HTTP Traffic Analysis | Teaches how web traffic works in practice and how to inspect, replay, and reason about requests and responses |
| 06 | Authentication, Credentials, and Password Operations | Builds a cross-cutting credential mental model before deeper attack-path modules |
| 07 | Web Content Discovery and Fuzzing | Expands the web track into content enumeration, hidden surface discovery, and parameter fuzzing |
| 08 | Core Web Vulnerabilities and Exploit Chains | Covers foundational web exploitation patterns and how to reason about chaining them |
| 09 | Attacking Common Services and Applications | Applies enumeration and attack-path reasoning to common enterprise services and widely deployed applications |
| 10 | Footholds, Shells, Payloads, and File Operations | Covers initial execution, session handling, payload choices, file movement, and practical foothold operations |
| 11 | Linux Privilege Escalation | Builds local enumeration and privesc reasoning on Linux systems |
| 12 | Windows Privilege Escalation | Builds local enumeration and privesc reasoning on Windows systems |
| 13 | Pivoting, Tunneling, and Port Forwarding | Teaches post-foothold movement into deeper network segments |
| 14 | Active Directory Enumeration and Attacks | Brings together Windows, credentials, lateral movement, and graph-based enterprise reasoning |
| 15 | Documentation, Reporting, and Assessment Communication | Converts raw technical work into evidence, findings, and professional deliverables |
| 16 | Attacking Enterprise Networks Capstone | Synthesizes the full workflow in an end-to-end simulated engagement |

---

## 3. Build Rules for Lesson Authors

| Principle | Implementation Guidance |
|---|---|
| Teach in sequence | Every lesson should answer: why now, what it builds on, and what it prepares the learner to do next |
| First lesson rule | When a module introduces a new major domain, the first lesson explains how that domain works under the hood before tactics begin |
| No tool worship | Tools appear as part of workflows, not as isolated personality-driven modules |
| Concepts before exploitation | Enumeration, interpretation, and validation must come before attack execution in each domain |
| Practice in every module | Each module should include mini exercises, end-of-lesson checks, and at least one natural lab or applied walkthrough |
| Repetition must deepen | When a concept returns later, the new lesson must add context, complexity, or a new surface—not repeat the same explanation |
| GitHub-first writing | Lesson files should be easy to navigate, copy, and expand with diagrams, screenshots, commands, and clean sectioning |

---

## 4. Suggested Status Vocabulary

| Status | Meaning |
|---|---|
| Planned | Not yet written, but structure is approved |
| In Draft | Outline-to-lesson expansion is underway |
| In Review | Lesson exists and is being reviewed for flow, accuracy, and tone |
| Finalized | Lesson is ready for repo publication |

Default status throughout this blueprint is **Planned**.

---

## 5. Module-by-Module Implementation Blueprint

## Module 01 — Orientation and Assessment Workflow

**Purpose:** Establish the learner mindset, assessment lifecycle, course workflow, lab expectations, note-taking discipline, and how the rest of the series fits together.  
**Why here:** Self-paced learners need a clear frame before technical depth begins.

| Lesson | Lesson Purpose | Topics & Sub-topics | Practice / Artifacts | Status |
|---|---|---|---|---|
| 1.1 — What Hack the Basics Is and How to Learn Through It | Introduce the series, learner expectations, and how the self-paced experience is designed to work. | **Series scope and learner profile** — what this course family covers, who it is for, what it is not; **How to use the material** — sequential learning, reference use, revisiting modules, when to slow down; **What success looks like** — building methodology, not memorizing commands, creating repeatable workflows | Short orientation checklist; learner workspace setup notes | Planned |
| 1.2 — The Assessment Lifecycle from First Contact to Final Deliverable | Give learners a high-level model of how real assessments progress. | **Assessment phases** — scoping, recon, enumeration, validation, exploitation, post-exploitation, reporting; **Why sequence matters** — reducing randomness, prioritizing signal, building hypotheses; **Workflow handoffs** — how findings in one phase create the next step | Mini exercise: map a sample finding to the next phase; lifecycle diagram asset | Planned |
| 1.3 — Scope, Rules of Engagement, and Lab Discipline | Teach operational boundaries and how to work safely and intentionally in labs. | **Scope and authorization** — targets, exclusions, time windows, communication paths; **Why boundaries matter** — false confidence, collateral noise, and bad methodology; **Lab discipline** — snapshots, notes, command history, evidence capture, file organization | Course workspace template; note-taking structure starter | Planned |
| 1.4 — Hypothesis-Driven Testing and the Analyst Mindset | Shift the learner from tool usage to reasoning. | **Hypothesis-driven work** — observation, inference, validation, revision; **Signal vs noise** — identifying useful artifacts, discarding distractions; **From output to decision** — why findings must drive the next step | End-of-lesson reflection prompt; sample evidence triage walkthrough | Planned |

## Module 02 — Network Enumeration with Nmap

**Purpose:** Teach learners how to discover hosts, ports, services, and network context with Nmap as a foundational enumeration tool.  
**Why here:** It is the earliest practical attack-surface mapping skill and a prerequisite for later service, web, and credential work.

| Lesson | Lesson Purpose | Topics & Sub-topics | Practice / Artifacts | Status |
|---|---|---|---|---|
| 2.1 — How Network Scanning Works and Why Nmap Matters | Build the packet-level and workflow-level mental model before commands begin. | **What scanning actually observes** — packets, responses, timeouts, inference; **Targets and scope** — hosts, ranges, CIDR, exclusions, local vs routed networks; **Nmap’s role in assessments** — discovery, triage, validation, follow-on planning | Diagram: host discovery vs port scanning vs service detection | Planned |
| 2.2 — Host Discovery and Target Definition in Practice | Teach learners how to identify live systems and define efficient scan scope. | **Discovery methods** — ARP, ICMP, TCP, UDP-based discovery; **Target input methods** — lists, ranges, files, exclusions; **Discovery tradeoffs** — false negatives, rate limiting, network position | Mini lab: discover hosts across a small subnet | Planned |
| 2.3 — TCP, UDP, and Port State Interpretation | Explain the main scan types and how to interpret states correctly. | **TCP scan mechanics** — SYN vs connect, privilege implications, expected responses; **UDP reality** — ambiguity, slowness, open\|filtered cases; **Port states** — open, closed, filtered, open\|filtered, closed\|filtered, what each implies | Output interpretation worksheet | Planned |
| 2.4 — Service Detection, OS Clues, and Script-Assisted Enumeration | Teach how Nmap moves beyond open ports into richer service context. | **Version detection** — banners, fingerprints, ambiguity; **OS and topology clues** — OS detection, traceroute, device hints; **NSE foundations** — what scripts add, choosing useful script categories, when not to overuse them | Guided scan profile lab; compare basic vs enriched scan output | Planned |
| 2.5 — Saving Results, Tuning Scans, and Building a Repeatable Nmap Workflow | Convert ad hoc usage into a disciplined workflow. | **Output formats** — normal, grepable mindset, XML, why structured output matters; **Scan tuning** — timing, retries, port selection, noise control; **Repeatable workflow** — triage scan, deepen scan, capture artifacts, note follow-ups | Module lab: full Nmap workflow on a mini environment | Planned |

## Module 03 — Service Footprinting and Common Infrastructure Enumeration

**Purpose:** Teach learners how to interrogate common enterprise services and infrastructure protocols after ports are identified.  
**Why here:** After network discovery, learners need to turn service exposure into concrete understanding and actionable follow-up.

| Lesson | Lesson Purpose | Topics & Sub-topics | Practice / Artifacts | Status |
|---|---|---|---|---|
| 3.1 — How Common Infrastructure Services Behave Under the Hood | Provide the mental model for why these services exist and what questions they answer. | **Service roles in real environments** — identity, name resolution, storage, messaging, management; **Protocol thinking** — default ports vs real behavior, server/client relationships, trust assumptions; **From discovery to footprinting** — what service exposure tells you about host role | Service-role matrix artifact | Planned |
| 3.2 — Enumerating File, Name, and Messaging Services | Cover high-frequency enterprise protocols and what to look for first. | **File and share protocols** — FTP, SMB, NFS, what metadata and access patterns matter; **Naming and mail protocols** — DNS, SMTP, IMAP, POP3, common information leaks; **Enumeration outcomes** — hostnames, users, shares, records, service posture | Mini exercises against sample outputs or lab services | Planned |
| 3.3 — Enumerating Databases, Monitoring, and Management Services | Expand into admin and back-end services that often yield strong signal. | **Database services** — MySQL, MSSQL, Oracle TNS, versioning and access clues; **Monitoring and management** — SNMP, IPMI, WinRM, SSH, RDP, remote management context; **Risk-centered interpretation** — anonymous access, misconfigurations, weak exposure | Service-specific quick-reference sheet | Planned |
| 3.4 — Prioritizing Follow-Up from Service Footprints | Teach learners how to reason from enumeration into attack-path decisions. | **High-value questions** — where credentials may be validated, where sensitive data may reside, where remote execution may emerge; **Cross-service patterns** — overlapping names, shared identity context, duplicated technologies; **Handoff discipline** — what belongs to web modules, credential modules, common service attack modules | End-of-module triage scenario; service prioritization notes | Planned |

## Module 04 — Web Reconnaissance and Application Discovery

**Purpose:** Begin the contiguous web track with web-specific discovery, mapping, technology identification, and target surface understanding.  
**Why here:** Web applications are a primary attack surface and deserve a dedicated, progressive learning arc.

| Lesson | Lesson Purpose | Topics & Sub-topics | Practice / Artifacts | Status |
|---|---|---|---|---|
| 4.1 — How Web Applications Work and What We Are Actually Discovering | Establish core web mental models before recon tactics. | **Web request/response model** — clients, servers, routes, methods, status codes, headers; **Application surface types** — static assets, dynamic pages, APIs, auth portals, admin interfaces; **What discovery means in web contexts** — domains, subdomains, technologies, content, trust relationships | Diagram: browser to server to app to data store | Planned |
| 4.2 — Passive Recon for Web Targets | Teach low-friction information gathering before active interaction deepens. | **Passive sources** — WHOIS, DNS history, certificate transparency mindset, search engine discovery; **Historical visibility** — web archives, cached content, legacy endpoints; **Technology clues without touching much** — headers, public metadata, exposed documentation | Passive recon worksheet; asset inventory table | Planned |
| 4.3 — Active Recon and Surface Mapping | Teach direct discovery of live web assets and application boundaries. | **Domain and subdomain enumeration** — resolution, prioritization, false positives; **Crawling and asset collection** — links, scripts, forms, APIs, hidden references; **Fingerprinting** — frameworks, CMSs, server stacks, front-end libraries | Guided recon lab on a sample target | Planned |
| 4.4 — From Web Discovery to Test Plan | Turn recon output into a practical next-step map for later modules. | **Surface classification** — public pages, login surfaces, admin paths, upload points, dynamic endpoints; **What to test later** — auth flows, input points, content discovery, common app checks; **Evidence capture** — screenshots, route maps, recon notes | Web recon report stub; route map artifact | Planned |

## Module 05 — Web Proxies and HTTP Traffic Analysis

**Purpose:** Teach learners to inspect, replay, modify, and reason about web traffic using proxies as workflow tools rather than standalone products.  
**Why here:** Once the learner knows what web assets exist, the next step is understanding how those assets behave in traffic.

| Lesson | Lesson Purpose | Topics & Sub-topics | Practice / Artifacts | Status |
|---|---|---|---|---|
| 5.1 — How HTTP Traffic Flows Through Real Applications | Build the mental model required for effective proxy use. | **HTTP structure** — methods, paths, parameters, headers, bodies, cookies; **State and sessions** — tokens, redirects, CSRF context, browser behavior; **Multi-step interactions** — forms, async requests, APIs, hidden state | HTTP anatomy cheat sheet | Planned |
| 5.2 — Setting Up and Using a Web Proxy Workflow | Introduce proxy tooling and the mechanics of interception. | **Proxy setup** — browser configuration, certificate handling, traffic capture basics; **Core workflow actions** — intercept, forward, drop, repeat, compare; **Project hygiene** — scoping, history, notes, target separation | Setup lab using Burp or ZAP on a demo app | Planned |
| 5.3 — Reading and Manipulating Requests and Responses | Teach learners how to reason about the meaning of what they see. | **Request analysis** — parameters, headers, auth tokens, hidden fields; **Response analysis** — status codes, reflected input, data leakage, feature exposure; **Controlled modification** — method changes, parameter changes, cookie and header edits | Repeat/replay exercise pack | Planned |
| 5.4 — Proxy-Assisted Testing Workflows | Position the proxy as a central instrument for later web modules. | **Traffic from other tools** — proxying browsers and auxiliary tooling; **Quick testing patterns** — replay, compare, baseline vs modified request; **Preparing for fuzzing and vuln work** — identifying promising endpoints and stable test cases | Module lab: instrument an app and document key flows | Planned |

## Module 06 — Authentication, Credentials, and Password Operations

**Purpose:** Provide a cross-cutting foundation for how authentication works and how credentials are discovered, validated, attacked, reused, and defended across services and web applications.  
**Why here:** Learners now understand major surfaces; they are ready to study one of the most common access pathways before going deeper into fuzzing and exploitation.

| Lesson | Lesson Purpose | Topics & Sub-topics | Practice / Artifacts | Status |
|---|---|---|---|---|
| 6.1 — How Authentication Works Across Systems | Build the conceptual foundation for later password and auth testing. | **Identity basics** — subjects, identifiers, secrets, sessions, tokens; **Auth models** — local vs remote auth, interactive vs service auth, web vs network service auth; **Authorization and trust** — roles, groups, access checks, why auth bugs matter | Authentication model diagram | Planned |
| 6.2 — Credential Surfaces, Password Storage, and Attack Types | Explain where credentials appear and how different attack classes work. | **Credential surfaces** — login forms, HTTP auth, SSH, FTP, SMB, files, configs, browsers; **Storage and protection** — hashes, password managers, archives, protected files; **Attack categories** — online brute force, spraying, offline cracking, reuse, default creds, stuffing | Credential surface inventory exercise | Planned |
| 6.3 — Wordlists, Mutations, Validation, and Cracking Workflows | Turn theory into practical credential operations. | **Wordlist strategy** — defaults, context-aware lists, organization-aware vocabulary; **Mutations and generation** — seasonal patterns, company naming, user-informed variation; **Validation workflows** — safe testing order, rate limits, lockout awareness, offline cracking basics | Mini lab: build a target-aware wordlist and test logic flow | Planned |
| 6.4 — Credential Hunting and Reuse Across Environments | Show how credentials become a cross-module bridge. | **Credential hunting sources** — config files, history, notes, shares, browsers, scripts; **Reuse and pivot value** — same creds across services, local-to-remote transitions, web-to-infra patterns; **Defensive thinking** — policies, MFA, least privilege, monitoring considerations | End-of-module scenario: prioritize credential avenues | Planned |

## Module 07 — Web Content Discovery and Fuzzing

**Purpose:** Teach learners how to uncover hidden web content, parameters, vhosts, and unlinked attack surface using disciplined fuzzing workflows.  
**Why here:** After recon, proxy fluency, and credential foundations, learners can enumerate hidden web surface with far better judgment.

| Lesson | Lesson Purpose | Topics & Sub-topics | Practice / Artifacts | Status |
|---|---|---|---|---|
| 7.1 — How Web Content Discovery Works and What Fuzzing Can Reveal | Build the conceptual model before running tools. | **Why hidden content exists** — legacy routes, admin panels, internal features, disabled pages, alternate vhosts; **Discovery targets** — directories, files, parameters, values, hostnames; **Signal vs false positives** — status code traps, redirects, wildcard responses, noise | Discovery decision tree artifact | Planned |
| 7.2 — Directory, File, and Vhost Discovery Workflows | Teach the most common fuzzing patterns for web surface expansion. | **Wordlist-based discovery** — route selection, extension logic, recursion choices; **Virtual host discovery** — host headers, subdomain patterns, response differentiation; **Interpreting results** — filtering boring noise, validating hits, noting auth boundaries | Guided ffuf-style lab on a sample site | Planned |
| 7.3 — Parameter and Input Surface Discovery | Expand from routes to functional inputs. | **Parameter discovery** — GET, POST, JSON, hidden fields, app-specific naming; **Value fuzzing** — role changes, feature toggles, enum candidates, numeric ranges; **Proxy-assisted fuzzing** — stable baselines, replayed requests, parameter isolation | Parameter map worksheet | Planned |
| 7.4 — Building a Web Discovery Playbook | Convert techniques into a repeatable web enumeration routine. | **Sequencing** — recon first, baseline traffic, content discovery, parameter discovery; **Documentation** — discovered routes, suspected admin paths, auth-relevant inputs; **Hand-off to exploitation** — what findings suggest SQLi, XSS, file upload, IDOR, or command injection potential | Module lab: produce a content discovery map and prioritized test queue | Planned |

## Module 08 — Core Web Vulnerabilities and Exploit Chains

**Purpose:** Teach the foundational vulnerability classes that appear repeatedly in web applications and how to reason about exploitability, impact, and chaining.  
**Why here:** Learners now know how to find web assets and inspect traffic, so deeper vulnerability reasoning becomes meaningful.

| Lesson | Lesson Purpose | Topics & Sub-topics | Practice / Artifacts | Status |
|---|---|---|---|---|
| 8.1 — A Framework for Reasoning About Web Vulnerabilities | Establish a common decision model before diving into classes of bugs. | **Input, trust, and sink thinking** — where user input enters and where it becomes dangerous; **Impact categories** — disclosure, auth bypass, code execution, account compromise; **Exploit chain mindset** — why one bug often matters because of what it enables next | Web vuln reasoning matrix | Planned |
| 8.2 — Injection and Data Access Vulnerabilities | Cover data-layer and execution-layer patterns. | **SQL injection foundations** — query logic, inference, auth bypass, data extraction; **Command injection foundations** — shell contexts, operators, filters, environment differences; **XXE and parser-driven data access** — local file reads, SSRF-style effects, parser trust | Focused practice prompts based on request snippets | Planned |
| 8.3 — Client-Side and Access Control Vulnerabilities | Cover browser-facing and authorization flaws. | **XSS foundations** — reflected, stored, DOM-based, impact paths; **IDOR and access control failures** — object references, horizontal vs vertical access, trust boundary mistakes; **HTTP method and workflow abuse** — verb tampering, hidden features, broken assumptions | Mini case studies with exploit-path reasoning | Planned |
| 8.4 — File Handling Vulnerabilities and Exploit Chaining | Cover high-value file-related patterns and how bugs combine. | **File inclusion and path traversal** — local file access, wrapper abuse, traversal logic; **File upload attacks** — extension checks, MIME checks, parser assumptions, web shell routes; **Chaining examples** — upload to execution, IDOR to data theft, SQLi to credential abuse | Module lab: analyze a multi-step vulnerable app path | Planned |
| 8.5 — Automation, Validation, and Tool Support in Web Exploitation | Place helper tools in their right role without making them the curriculum center. | **Where automation fits** — SQLMap-like assistance, replay tools, scanners as validators not teachers; **Manual before automation** — proving the bug and understanding the condition; **Artifact discipline** — reproducer steps, evidence capture, impact notes | Tool-assisted validation checklist | Planned |

## Module 09 — Attacking Common Services and Applications

**Purpose:** Teach learners how to move from enumeration to focused testing against common enterprise services and widely deployed applications.  
**Why here:** By now learners can enumerate, reason about creds, and work web workflows, so they are ready for targeted attack paths. 

| Lesson | Lesson Purpose | Topics & Sub-topics | Practice / Artifacts | Status |
|---|---|---|---|---|
| 9.1 — From Enumeration to Attack Surface Triage | Teach how to prioritize service and application attack paths. | **Attack objectives** — sensitive data, user enumeration, credential validation, remote execution, privilege gain; **Service-family triage** — mail, file services, DBs, management planes, web apps, developer tooling; **Context-driven prioritization** — exposure, auth surface, business function, likely blast radius | Attack-surface prioritization matrix | Planned |
| 9.2 — Testing Common Network Services | Apply structured thinking to enterprise protocols first. | **Network service checks** — SMB, FTP, NFS, SMTP, IMAP/POP3, SNMP, DB services; **Common weakness categories** — anonymous access, weak creds, user enum, misconfigurations, legacy exposure; **Validation discipline** — safe credential testing, banner vs behavior, documentation of reachable attack paths | Service attack worksheet | Planned |
| 9.3 — Testing Common Web and Platform Applications | Shift to popular enterprise and internet-facing applications. | **CMS and portal families** — WordPress, Drupal, Joomla, admin panels, ticketing systems; **Dev and infra applications** — Jenkins, GitLab, Splunk, Tomcat, PRTG, similar platforms; **Application-specific thinking** — versioning, plugins, misconfigurations, default paths, known auth workflows | Common application triage checklist | Planned |
| 9.4 — Building Reusable Service and Application Playbooks | Turn ad hoc attack knowledge into reusable process. | **Playbook structure** — discovery, auth checks, default paths, version cues, high-value files, known post-auth pivots; **When to research further** — version-driven questions, plugins, exposed docs, public advisories; **Hand-offs** — when a common app issue becomes a web vuln, foothold, or privilege escalation problem | Module lab: write a mini playbook for one service and one app | Planned |

## Module 10 — Footholds, Shells, Payloads, and File Operations

**Purpose:** Teach learners how to establish execution, manage shells and payloads, move files, and operate effectively once initial access is gained.  
**Why here:** It follows naturally after exploitation and common-service attack paths, and prepares learners for post-exploitation modules.

| Lesson | Lesson Purpose | Topics & Sub-topics | Practice / Artifacts | Status |
|---|---|---|---|---|
| 10.1 — How Footholds Work and What Makes a Shell Useful | Build the conceptual model for shell and payload decisions. | **Foothold types** — command execution, web shells, reverse shells, bind shells, agents; **Session characteristics** — interactivity, stability, transport, privileges, environment; **Operational goals after access** — orient, stabilize, verify, document | Foothold comparison chart | Planned |
| 10.2 — Payload Selection and Shell Delivery Workflows | Teach how payload choices depend on target context. | **Payload dimensions** — staged vs stageless, architecture, interpreter availability, web vs native contexts; **Delivery methods** — exploit result, upload, command injection, script execution, living-off-the-land launchers; **Tooling support** — MSFvenom/Metasploit-like workflows in the right context | Payload decision worksheet | Planned |
| 10.3 — File Transfer and Tool Movement in Practice | Fold file operations into the actual post-foothold workflow where they belong. | **Transfer methods** — web servers, native utilities, copy channels, one-liners, archives; **Living-off-the-land movement** — built-in tools on Windows and Linux, environment-aware choices; **Detection and OPSEC basics** — artifact minimization, server logs, obvious binaries, cleanup considerations | Guided exercise: move a file in and out of a target VM | Planned |
| 10.4 — Session Management, Stabilization, and Operator Hygiene | Turn “I got a shell” into “I can work from here.” | **Shell stabilization** — terminal upgrades, interactive shells, environment fixing; **Session management** — multiple shells, jobs, note discipline, timeline awareness; **Operator hygiene** — command logging, evidence capture, avoiding unforced errors | End-of-module foothold operations lab | Planned |

## Module 11 — Linux Privilege Escalation

**Purpose:** Teach learners how to enumerate Linux systems deeply and identify realistic privilege escalation paths.  
**Why here:** Linux privesc depends on solid foothold handling and local enumeration discipline.

| Lesson | Lesson Purpose | Topics & Sub-topics | Practice / Artifacts | Status |
|---|---|---|---|---|
| 11.1 — How Linux Privilege Escalation Really Works | Build the local mental model before techniques. | **Users, groups, and execution context** — effective identity, group memberships, sudo, service accounts; **The role of enumeration** — system info, services, files, capabilities, scheduled tasks; **Categories of Linux privesc** — misconfigurations, credentials, service abuse, kernel-level paths | Linux enumeration checklist | Planned |
| 11.2 — Enumerating the Host for High-Value PrivEsc Paths | Teach systematic local triage. | **System and environment enumeration** — kernel, distro, patches, processes, network context; **File and permission review** — SUID/SGID, writable paths, config files, cron, service definitions; **Credential and secret hunting** — histories, configs, keys, tokens | Guided host triage lab | Planned |
| 11.3 — Common Linux PrivEsc Patterns | Cover the most common realistic paths. | **Permission and sudo abuse** — unsafe rules, writable scripts, privileged binaries; **Service and library abuse** — vulnerable services, PATH hijacks, shared object and environment abuse; **Credential-driven escalation** — reused creds, keys, protected file recovery | Technique comparison matrix | Planned |
| 11.4 — Kernel and Edge Cases, Validation, and Hardening Context | Keep advanced cases in proportion and teach good judgment. | **Kernel exploit logic** — when it is relevant and when it is a poor first choice; **Context-driven oddities** — containers, one-off service configs, strange operational drift; **Validation and hardening** — proving the path, preserving evidence, remediation framing | Module lab: end-to-end Linux privesc workflow | Planned |

## Module 12 — Windows Privilege Escalation

**Purpose:** Teach learners how to enumerate Windows hosts, reason about local trust and privilege, and identify common escalation opportunities.  
**Why here:** Windows local privilege escalation is a distinct surface that feeds directly into pivoting and AD work.

| Lesson | Lesson Purpose | Topics & Sub-topics | Practice / Artifacts | Status |
|---|---|---|---|---|
| 12.1 — How Windows Privilege Escalation Works | Provide the conceptual model for Windows privilege decisions. | **Windows security context** — users, groups, integrity, tokens, services; **What local enumeration should reveal** — patch level, installed software, service configs, privileges, user context; **Common categories** — weak service permissions, token/privilege misuse, credentials, vulnerable software | Windows privesc mental model chart | Planned |
| 12.2 — Enumerating Windows Systems for Escalation Paths | Teach disciplined local discovery. | **Host posture** — OS version, patch state, AV/EDR awareness, installed apps; **Privilege and configuration review** — groups, user rights, services, scheduled tasks, registry, startup paths; **Credential opportunities** — stored creds, browser artifacts, scripts, config files | Guided Windows enumeration lab | Planned |
| 12.3 — Common Windows PrivEsc Patterns | Cover high-frequency techniques and why they matter. | **Service and permission abuse** — weak ACLs, unquoted paths, writable services, dangerous task configs; **Credential and user-focused paths** — saved creds, attack-the-user opportunities, misused privileges; **Legacy vs modern realities** — differences across desktop and server environments | Technique-to-precondition matrix | Planned |
| 12.4 — Validation, Modern Constraints, and Defensive Perspective | Help learners reason beyond copy-paste techniques. | **Validation discipline** — confirming exploitability without guesswork; **Modern controls** — AV/EDR friction, patching, UAC context, endpoint hardening; **How to report and remediate** — evidence, impact, and realistic fixes | Module lab: full Windows privesc case study | Planned |

## Module 13 — Pivoting, Tunneling, and Port Forwarding

**Purpose:** Teach learners how to reach deeper network segments and services through a foothold using safe, understandable pivoting workflows.  
**Why here:** This module depends on foothold management and makes later AD work possible in realistic environments.

| Lesson | Lesson Purpose | Topics & Sub-topics | Practice / Artifacts | Status |
|---|---|---|---|---|
| 13.1 — Why Pivoting Exists and What Problem It Solves | Build the network and workflow model for indirect access. | **Indirect reachability** — dual-homed hosts, segmented networks, internal-only services; **Key concepts** — pivoting, port forwarding, tunneling, proxying; **Operational planning** — what to reach, why, and from where | Network path diagram exercise | Planned |
| 13.2 — Local and Remote Port Forwarding Workflows | Teach the most understandable pivot mechanics first. | **Port forwarding basics** — local vs remote, listener placement, service mapping; **Common transports** — SSH-style forwards, netcat/socat-style bridges, tool-assisted forwards; **Validation** — verifying reachability, avoiding confusion about where traffic is flowing | Simple port-forward lab | Planned |
| 13.3 — Proxying and Tunnel-Based Access | Expand into broader connectivity patterns. | **Proxy chaining and socks workflows** — layered access, tooling considerations, DNS implications; **Tunnel-based reachability** — encapsulated traffic, stability, performance tradeoffs; **Operational caveats** — latency, troubleshooting, authentication, visibility | Proxychains-style route validation exercise | Planned |
| 13.4 — Pivoting Playbooks for Real Assessments | Turn pivot techniques into practical workflows. | **Sequencing** — foothold, orient, identify internal targets, establish path, enumerate through pivot; **Artifact discipline** — tunnel maps, port maps, route notes; **Preparing for AD and internal app work** — where pivoting becomes essential later | Module lab: reach and enumerate an internal-only service via pivot | Planned |

## Module 14 — Active Directory Enumeration and Attacks

**Purpose:** Teach learners how enterprise identity environments are structured, how to enumerate AD effectively, and how common attack paths emerge across users, hosts, permissions, and trust relationships.  
**Why here:** AD depends on earlier Windows, credential, service, foothold, and pivoting knowledge and works best when introduced after those foundations exist.

| Lesson | Lesson Purpose | Topics & Sub-topics | Practice / Artifacts | Status |
|---|---|---|---|---|
| 14.1 — How Active Directory Works and Why It Is a Central Attack Surface | Build the mental model before tactics. | **AD foundations** — domains, forests, trusts, OUs, DCs, identity flows; **Core protocols and services** — LDAP, Kerberos, SMB, DNS, GPOs, why they matter together; **Why AD is different** — graph-like trust, delegated administration, inherited risk | AD architecture diagram | Planned |
| 14.2 — Enumerating AD from External and Internal Positions | Teach phased enumeration depending on access level. | **External signals** — naming, exposed services, VPNs, OWA-style portals, domain clues; **Internal enumeration** — users, groups, computers, shares, ACL cues, GPO context; **Tool roles** — native tools, BloodHound-style graphing, focused enumeration utilities | Guided AD recon worksheet | Planned |
| 14.3 — Common Credential and Access Attacks in AD | Cover the most frequent practical attack paths. | **Credential-focused attacks** — password spraying, Kerberoasting, AS-REP-related paths, weak secret hygiene; **Name resolution and relay-adjacent concepts** — LLMNR/NBT-NS context and why they matter; **Validation and prioritization** — avoiding noisy randomness, documenting preconditions | Attack-path decision matrix | Planned |
| 14.4 — Privilege Relationships, ACL Abuse, and Trusts | Move into the graph reasoning that makes AD distinct. | **Group and delegation reasoning** — nested groups, inherited rights, delegated admin; **ACL-based abuse concepts** — object control, rights misconfigurations, path-to-admin thinking; **Trusts and lateral reach** — cross-domain movement, trust relationships, chained access | Trust-path mapping exercise | Planned |
| 14.5 — Native Actions, Hardening, and Reporting AD Findings | Close the module with operational realism. | **Using native capabilities** — when and why built-in tools matter; **Defensive and hardening context** — tiering, admin hygiene, protocol hardening, monitoring; **Reporting AD findings** — path diagrams, blast radius, actionable remediation | Module lab: enumerate an AD path and write a concise finding summary | Planned |

## Module 15 — Documentation, Reporting, and Assessment Communication

**Purpose:** Teach learners how to transform commands, screenshots, notes, and attack paths into professional technical communication.  
**Why here:** By this stage, learners have enough technical context to understand what good documentation must preserve.

| Lesson | Lesson Purpose | Topics & Sub-topics | Practice / Artifacts | Status |
|---|---|---|---|---|
| 15.1 — How to Take Notes That Survive the Whole Engagement | Build the discipline that supports reporting and troubleshooting. | **Note structure** — hosts, users, creds, commands, evidence, timestamps; **Why note quality matters** — reproducibility, incident questions, handoffs, report accuracy; **Workspace organization** — screenshots, loot, logs, raw outputs, diagrams | Course note-taking template | Planned |
| 15.2 — Writing Technical Findings Clearly and Accurately | Teach the anatomy of a strong finding. | **Finding structure** — title, summary, evidence, impact, reproduction, remediation; **Evidence quality** — exact steps, screenshots, redaction, command context; **Writing with precision** — avoiding hype, proving impact, distinguishing confirmed vs inferred | Finding skeleton template | Planned |
| 15.3 — Reporting for Different Audiences | Show how one body of work must be communicated at different levels. | **Audience layers** — technical staff, managers, leadership, engineering teams; **Executive vs technical summary** — what changes and what does not; **Communicating risk honestly** — severity, exploitability, dependencies, uncertainty | Audience mapping exercise | Planned |
| 15.4 — Packaging the Assessment Story from Start to Finish | Turn scattered notes into a coherent final deliverable. | **Assessment narrative** — timeline, initial access, pivots, escalation, business impact; **Artifacts and appendices** — screenshots, host tables, credential handling, scope notes; **Professional communication habits** — update cadence, clarification requests, vulnerability notifications | Module lab: draft a miniature report section from a provided scenario | Planned |

## Module 16 — Attacking Enterprise Networks Capstone

**Purpose:** Synthesize the full course in a start-to-finish simulated engagement that requires planning, enumeration, validation, exploitation, post-exploitation reasoning, and reporting discipline.  
**Why here:** It is the final proof that the learner can connect the modules into one professional workflow.

| Lesson | Lesson Purpose | Topics & Sub-topics | Practice / Artifacts | Status |
|---|---|---|---|---|
| 16.1 — Reading the Engagement and Planning the Attack Surface | Start the capstone with scope understanding and a deliberate plan. | **Engagement intake** — scope, assumptions, exclusions, objectives; **Initial strategy** — external recon, likely surfaces, workflow ordering; **Artifact planning** — how evidence and notes will be captured throughout | Capstone planning template | Planned |
| 16.2 — External Enumeration, Validation, and Initial Access | Apply earlier modules under realistic conditions. | **Surface mapping** — Nmap, service footprinting, web discovery; **Validation and attack-path selection** — credentials, common services, web workflows; **Initial foothold** — selecting and documenting the path that worked | Capstone checkpoint 1 | Planned |
| 16.3 — Internal Expansion, Privilege Escalation, and Pivoting | Force the learner to connect mid-course modules as one system. | **Host triage after access** — local enumeration, credential hunting, internal visibility; **Escalation choices** — Linux or Windows path selection based on evidence; **Pivoting** — reaching deeper services and preparing for identity-centric work | Capstone checkpoint 2 | Planned |
| 16.4 — Active Directory, Objective Completion, and Reporting | Finish the capstone with enterprise reasoning and deliverable quality. | **AD-focused follow-up** — enumerate paths, validate opportunities, avoid unnecessary noise; **Objective completion** — data access, privilege proof, or target milestone depending on scenario; **Final report package** — evidence curation, findings, narrative, remediation | Final capstone deliverable outline | Planned |

---

## 6. Module-to-Module Learning Flow

The sequence is intentionally shaped around **dependency and workflow** rather than the original standalone module names.

- **Module 01** establishes the learner operating model.
- **Modules 02–03** teach external and internal-facing enumeration across networks and services.
- **Modules 04–08** form one contiguous **web learning arc**: discover the web surface, understand traffic, understand authentication as a cross-cutting surface, enumerate hidden content, then study core vulnerability classes and exploit-chain reasoning.
- **Module 09** broadens from web into common services and applications that appear repeatedly in real environments.
- **Modules 10–13** form the **post-foothold arc**: gain execution, operate sessions, escalate locally, then move deeper through pivots.
- **Module 14** uses everything prior to teach AD with the right prerequisites in place.
- **Module 15** teaches how to communicate the work professionally.
- **Module 16** proves the learner can perform the full workflow coherently.

This structure keeps foundational “how it works” content at the front of the module where it is immediately applied, avoids detached theory islands, and reduces shallow redundancy between modules. That follows the sequencing and anti-redundancy guidance in `course-outline.md`. fileciteturn15file3 fileciteturn15file4 fileciteturn15file6

---

## 7. Practice / Lab / Project Placement Strategy

| Practice Layer | Placement Strategy |
|---|---|
| Mini practice tasks | End of most lessons, especially where the learner must interpret output, classify a finding, or choose a next step |
| Guided labs | At the end of Modules 02, 04, 05, 07, 10, 11, 12, 13, and 14 where applied workflow matters most |
| Scenario-based exercises | Especially valuable in Modules 03, 06, 08, 09, and 15 where reasoning and triage matter as much as commands |
| Cross-module synthesis labs | One mid-course synthesis after Module 10 and one final capstone in Module 16 |
| Artifacts to generate | Recon maps, service triage sheets, route maps, wordlists, payload decision notes, privilege escalation checklists, pivot maps, AD path diagrams, and report stubs |

---

## 8. Recommended Repo Build Order

| Wave | Modules | Reason |
|---|---|---|
| Wave 1 | 01–03 | Establishes the overall workflow and the non-web technical foundations |
| Wave 2 | 04–08 | Builds the contiguous web block end-to-end |
| Wave 3 | 09–10 | Moves into common service attack paths and foothold operations |
| Wave 4 | 11–14 | Covers local escalation, movement, and enterprise identity environments |
| Wave 5 | 15–16 | Finishes with communication quality and the capstone engagement |

---

## 9. Final Notes for Future Lesson Writers

- Keep the tone serious, practical, and workflow-first.
- Teach **why this step exists** before **how to do it**.
- Prefer mental models and interpretation over giant command dumps.
- Use tools as supporting instruments inside workflows, not as the story of the lesson.
- Preserve the continuity of the web arc, the post-foothold arc, and the AD arc.
- Make every lesson leave behind an artifact, checklist, map, or decision model the learner can reuse.
- When revisiting a concept later, deepen it with new context rather than restating the earlier lesson.
- Keep each lesson GitHub-friendly: strong headings, readable diagrams, copyable commands, concise tables, and clear transitions.
