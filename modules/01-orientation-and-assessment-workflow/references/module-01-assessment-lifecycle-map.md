# Module 01 Assessment Lifecycle Map

---

> **📝 Map Purpose**
>
> Use this page as the course-wide operating map for understanding where a task belongs in the larger assessment flow.

## Lifecycle Diagram

```mermaid
%%{init: {"theme":"base","flowchart":{"curve":"basis","htmlLabels":true},"themeVariables":{"primaryTextColor":"#e8f0ff","lineColor":"#7dd3fc","fontSize":"14px"}}}%%
flowchart LR
    O["Orientation<br/>Environment, scope, constraints"] --> S["Surface Mapping<br/>Visibility and reachability"]
    S --> U["Service and App Understanding<br/>Role, meaning, and triage"]
    U --> V["Validation and Access<br/>Controlled testing and footholds"]
    V --> P["Post-Access and Expansion<br/>Privilege, movement, and new visibility"]
    P --> R["Reporting and Close-Out<br/>Evidence, findings, and delivery"]

    classDef orientation fill:#0f3a52,stroke:#5eead4,color:#ecfeff,stroke-width:3px;
    classDef mapping fill:#1e3a8a,stroke:#60a5fa,color:#eff6ff,stroke-width:2.5px;
    classDef understanding fill:#312e81,stroke:#a78bfa,color:#f5f3ff,stroke-width:2.5px;
    classDef validation fill:#78350f,stroke:#fbbf24,color:#fffbeb,stroke-width:2.5px;
    classDef postaccess fill:#4c0519,stroke:#fb7185,color:#fff1f2,stroke-width:2.5px;
    classDef reporting fill:#334155,stroke:#cbd5e1,color:#f8fafc,stroke-width:2.5px;

    class O orientation;
    class S mapping;
    class U understanding;
    class V validation;
    class P postaccess;
    class R reporting;
```

---

## Phase Questions

| Phase | Main question | Typical outputs |
|---|---|---|
| Orientation | what are we doing, in what environment, and under what limits? | scope note, VM inventory, workspace setup |
| Surface Mapping | what is reachable and visible from here? | host lists, scan artifacts, route maps |
| Service and App Understanding | what do those visible things probably mean? | host-role notes, app maps, triage queues |
| Validation and Access | what deserves direct testing or controlled validation next? | test queues, auth checks, footholds |
| Post-Access and Expansion | what changed after access and what can we now see? | local enum notes, pivot maps, privilege paths |
| Reporting and Close-Out | what evidence, findings, and workflow history must be preserved? | final notes, findings, report material |

---

## Mini Phase-Mapping Exercise

Use this prompt during Module 01:

```text
Current task:
Which lifecycle phase does it belong to?
What evidence should it produce?
What later phase will depend on it?
```

---

## Design Notes

This map is intended to stay useful across the entire course, not only inside Module 01.
