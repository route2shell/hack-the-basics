# Module 04 Route Map Template

---

> **📝 Template Purpose**
>
> Use this route map to turn first-pass web discovery into a structured testing queue. Keep route purpose, auth context, and later-module ownership visible.

## Route Inventory Table

| Route / Endpoint | Method or interaction | Seen where | Likely role | Auth required | Interesting input or output | Priority | Next module owner |
|---|---|---|---|---|---|---|---|
| `/login` | GET, form submit | nav bar | authentication entry point | no | username, password, reset link | high | Module 05 / Module 06 |
| `/api/v1/users` | GET | JavaScript clue | authenticated API | likely yes | user IDs, JSON response | high | Module 05 / Module 08 |
| `/admin` | redirect | footer link | admin portal | likely yes | role boundary, redirect chain | high | Module 05 |

Replace the sample rows with your own route inventory.

---

## Minimal Route Record

```text
Route:
How discovered:
Host / virtual host:
Method or interaction:
Observed response:
Likely role:
Observation:
Inference:
Needs proxy capture next:
Deferred to later module:
```

---

## Suggested Priority Legend

| Priority | Meaning |
|---|---|
| High | likely to affect auth, trust, admin function, or sensitive application logic |
| Medium | useful for context, mapping, or later validation |
| Low | informational or low-value surface with no strong next-step signal yet |

---

## Handoff Questions

- Which routes should be captured first with a proxy?
- Which routes likely involve authentication state or session handling?
- Which endpoints look better suited for later content discovery?
- Which functions suggest state changes, uploads, exports, or administrative value?

---

## Design Notes

This template should help the learner move from route collection into an explicit first testing queue rather than a loose page list.
