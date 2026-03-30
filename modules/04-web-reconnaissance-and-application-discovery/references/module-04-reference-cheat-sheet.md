<div align="center">

# Module 04 Field Reference

**Web Reconnaissance and Application Discovery**

*Phase II - Web Understanding and Exposure Analysis*

</div>

---

> **🧭 Use This For**
>
> Fast first-pass web recon when you need to collect names, certificates, technologies, routes, auth clues, and next-step test ideas without jumping too early into proxy manipulation or exploit testing.

| Best paired with | Main job | Assumption |
|---|---|---|
| Lesson 4.4 and the module lab | Help you move from “web is open” into a usable route map and first testing queue | Authorized lab use only |

| Preserve these outputs | Avoid these habits |
|---|---|
| hostnames, redirects, cert names, technologies, route classes, auth context, priority flows | calling every page a “web app,” skipping exact paths, treating headers as certainty |

---

## Table of Contents

- [1. Quick Workflow](#1-quick-workflow)
- [2. Surface Layers](#2-surface-layers)
- [3. Passive Recon Sources](#3-passive-recon-sources)
- [4. Active Recon Commands](#4-active-recon-commands)
- [5. What to Capture](#5-what-to-capture)
- [6. Route Classification](#6-route-classification)
- [7. Priority Lenses](#7-priority-lenses)
- [8. Handoff Routing](#8-handoff-routing)
- [9. Minimal Web Recon Note Template](#9-minimal-web-recon-note-template)

---

## 1. Quick Workflow

> **🧠 Mental Model**
>
> inventory -> confirm -> map -> classify -> prioritize -> route the next step

### Fast operator rhythm

1. Collect known hostnames, URLs, and scope notes.
2. Expand likely names from certificates, DNS clues, and prior module notes.
3. Confirm live web targets and redirects.
4. Record technologies, titles, headers, and auth signals.
5. Map important routes, forms, parameters, APIs, and admin paths.
6. Build a route map and first test queue.
7. Hand the most important flows into proxy work.

### Fast first-pass examples

```bash
curl -I https://target.example
curl -k https://target.example/
whatweb https://target.example
httpx -u https://target.example -title -tech-detect -status-code
openssl s_client -connect target.example:443 -servername target.example </dev/null
```

---

## 2. Surface Layers

| Layer | What you are trying to learn |
|---|---|
| Naming | hostnames, subdomains, virtual hosts, redirects |
| Transport | HTTP vs HTTPS, TLS behavior, ports, certificate clues |
| Identity | login surfaces, SSO clues, role separation, session hints |
| Application | routes, forms, actions, APIs, admin panels, uploads |
| Technology | frameworks, server banners, libraries, CMS or platform indicators |
| Trust | public vs authenticated, user vs admin, internal vs external hints |

> **🔍 Interpretation**
>
> A web target is rarely just one page. It is usually a set of names, routes, components, and trust boundaries that need to be mapped deliberately.

---

## 3. Passive Recon Sources

| Source | What it may reveal |
|---|---|
| scope docs and prior notes | approved targets, known names, environment context |
| Nmap / Module 03 output | HTTP ports, TLS services, cert subjects, service banners |
| certificate transparency | alternate hostnames, wildcard coverage, reused naming patterns |
| public search results and cached references | product names, documentation portals, exposed subdomains |
| DNS and naming context already collected | environment conventions, likely web naming schemes |
| screenshots and previous walkthrough notes | login paths, dashboards, distinct app roles |

### Passive recon questions

- Is this likely one app or several?
- Which names appear external versus internal?
- Do cert names suggest admin, API, staging, or portal roles?
- Does naming imply role separation like `app`, `api`, `admin`, `auth`, or `files`?
- Which names should be validated first once active recon starts?

---

## 4. Active Recon Commands

### Basic confirmation

```bash
curl -I https://target.example
curl -k https://target.example/
curl -k -L https://target.example/
```

### TLS and certificate review

```bash
openssl s_client -connect target.example:443 -servername target.example </dev/null
curl -vkI https://target.example 2>&1 | sed -n '1,25p'
```

### Technology and route clues

```bash
whatweb https://target.example
httpx -u https://target.example -title -tech-detect -status-code -follow-redirects
curl -k https://target.example/robots.txt
curl -k https://target.example/sitemap.xml
curl -k https://target.example/login
```

### JavaScript and asset clue capture

```bash
curl -k https://target.example/ | rg 'script|api|login|admin|fetch'
curl -k https://target.example/static/app.js | rg '/api/|token|auth|graphql'
```

> **⚠️ Warning**
>
> Module 04 is for first-pass mapping. Do not turn every command into deep automation or force content discovery workflows that belong to Module 07.

---

## 5. What to Capture

### Exact nouns matter

- hostnames and alternate names
- redirect destinations
- certificate subject and SAN entries
- page titles and visible product names
- frameworks, CMS clues, or server technologies
- login paths, admin paths, docs paths, API roots
- parameters, form actions, upload features, search inputs
- status codes, response size patterns, and auth requirements

### Strong notes look like

```text
portal.acme.lab redirects to https://app.acme.lab/login; cert SANs include api.acme.lab and admin.acme.lab; navbar exposes Dashboard, Reports, Upload, and API Docs; /admin redirects to SSO.
```

Not:

```text
Website found. Maybe React.
```

---

## 6. Route Classification

| Route type | Common examples | Why it matters |
|---|---|---|
| Public content | `/`, `/about`, `/docs`, `/help` | reveals app purpose and naming |
| Authentication | `/login`, `/logout`, `/register`, `/forgot-password` | prepares auth analysis later |
| User workflow | `/dashboard`, `/profile`, `/orders`, `/reports` | shows state-changing business logic |
| Admin / ops | `/admin`, `/manage`, `/console`, `/metrics`, `/health` | often high-priority trust boundaries |
| API | `/api`, `/graphql`, `/v1`, `/swagger`, `/openapi.json` | important for request mapping and later testing |
| File handling | `/upload`, `/download`, `/export`, `/import` | points toward high-value input and output paths |

---

## 7. Priority Lenses

| Lens | What to ask |
|---|---|
| Value | If we understand this route better, what does it unlock? |
| Trust | Is this public, authenticated, privileged, or operational? |
| Input | Does it accept user data, files, search terms, or IDs? |
| State | Does it create, update, delete, or export anything? |
| Visibility | Can we inspect it now, or do we need the proxy next? |

### High-priority clues

- multiple hostnames point to different roles of the same app
- redirects reveal SSO, tenants, or segmented admin flows
- public pages expose docs, API references, or JavaScript route hints
- uploads, exports, search, or report builders appear early
- hidden-but-linked operational paths like `/metrics`, `/health`, or `/admin` exist

---

## 8. Handoff Routing

| If you see this | Route it toward |
|---|---|
| important multi-step flows, cookies, tokens, redirects | Module 05 proxy instrumentation |
| login, MFA, password reset, SSO, role changes | Module 06 authentication reasoning |
| likely hidden content, alternate vhosts, parameter expansion | Module 07 content discovery and fuzzing |
| interesting inputs, uploads, exports, and state changes | Module 08 vulnerability analysis |

> **📝 Note**
>
> Module 04 should leave later modules a cleaner map, not steal their jobs.

---

## 9. Minimal Web Recon Note Template

```text
Primary URL:
Alternate names:
Redirect behavior:
Certificate names:
Observed technologies:
Key public routes:
Auth routes:
Admin or ops routes:
API clues:
Interesting inputs or file features:
Observation:
Inference:
Needs proxy capture next:
Later module handoff:
```

---

<div align="center">

**Map the web surface before you instrument it: capture the names, classify the routes, and route the next step deliberately.**

</div>
