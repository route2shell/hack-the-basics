# Module 04 Lab 01 - Web Recon and Surface Mapping

---

> **🛠 Lab Objective**
>
> Use the Module 04 workflow to move from a newly identified web target into a documented asset inventory, route map, and first-pass testing queue that is ready for proxy capture in Module 05.

| Module | Position | Main output |
|---|---|---|
| Module 04 - Web Reconnaissance and Application Discovery | End-of-module lab | completed web recon worksheet, route map, prioritized proxy-capture queue |

| Prerequisites | Use while working |
|---|---|
| Lessons 4.1-4.4, Module 03 or equivalent service-triage context | [field reference](../references/module-04-reference-cheat-sheet.md), [web recon worksheet](../references/module-04-web-recon-worksheet.md), [route map template](../references/module-04-route-map-template.md) |

---

## Scenario

You have identified one or more in-scope web services during earlier enumeration.
Your job is not to exploit them yet.
Your job is to build a first-pass web surface map that answers:

- what names and entry points exist?
- what kind of application or applications appear to be present?
- which routes and functions look most important?
- what should be captured and inspected first in a web proxy next?

Use a legal lab target you control or a course-provided environment.

---

## Expected Learner Artifacts

- a completed recon worksheet
- a list of confirmed hostnames or URLs
- recorded redirect and certificate clues
- a route inventory with public, auth, admin, and API paths
- a prioritized first-pass proxy-capture queue
- short notes separating observation, inference, and validation needs

---

## Lab Workflow

### Checkpoint 1 - Prepare the target context

Record:

1. the approved scope
2. the original discovery source such as Nmap or prior notes
3. the primary hostname, IP, and port combination
4. any naming clues already visible from certificates or previous module output

### Checkpoint 2 - Perform passive recon

Use non-invasive sources first.
Capture:

- known names from scope notes or prior scans
- certificate names or wildcard patterns
- visible naming conventions like `app`, `api`, `admin`, `auth`, or `portal`
- any evidence that the target may really be several related web assets

Update the worksheet before sending many requests.

### Checkpoint 3 - Confirm live behavior

Validate the target with a small number of deliberate requests.
Capture:

- status code
- title
- redirect behavior
- HTTP versus HTTPS handling
- server or framework clues
- whether the target appears static, dynamic, API-first, or multi-role

### Checkpoint 4 - Map the visible surface

Identify and record:

- public routes
- authentication routes
- admin or operational routes
- API or documentation endpoints
- any forms, parameters, search functions, uploads, exports, or downloads

Focus on mapping what is visible.
Do not turn this lab into deep fuzzing or exploit testing.

### Checkpoint 5 - Build the route map

Use the route map template to classify each important route by:

- function
- auth expectation
- trust level
- interesting input or output
- priority
- next module owner

### Checkpoint 6 - Build the first testing queue

Create a short queue of the first five flows or requests you would capture in Module 05.

Good candidates often include:

- the main landing page and redirect chain
- the login flow
- an authenticated-looking or role-specific path
- an API request surfaced by visible links or JavaScript
- a state-changing route such as upload, export, search, or report generation

---

## Validation Questions

Use these questions to check whether your recon is strong enough:

1. Can you explain what kind of web system appears to be present?
2. Can you name the most important hostnames and why they matter?
3. Have you separated public, authenticated, administrative, and API routes?
4. Have you captured exact paths instead of vague descriptions?
5. Does your first testing queue clearly justify why those flows should be proxied first?

---

## Close-Out Reflection

Write a short close-out note that answers:

- What was directly observed?
- What is only inferred so far?
- What still needs traffic capture to validate?
- Which later module should own each important next step?

---

## Design Notes

This lab should feel like a guided web recon operation, not a generic checklist. The quality bar is a clean route map and a defensible handoff into Module 05.
