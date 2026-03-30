# Module 04 Gap Analysis

---

## Review Scope

Reviewed against:

- `README.md`
- `hack-the-basics-implementation-blueprint.md`
- Module 03 contract and handoff
- Module 05 contract
- Module 04 README
- all Module 04 lessons
- Module 04 reference artifacts
- Module 04 lab
- shared Markdown and authoring standards

---

## Role Check

Module 04 is correctly positioned as the first module in the contiguous web arc.
It builds on service triage from Module 03 and hands directly into Module 05 proxy workflows, while leaving deeper authentication, fuzzing, and vulnerability work to Modules 06-08.

---

## Findings

### Critical gaps

None identified in the implemented module contract.

### Strengths

- The README clearly states module role, artifacts, lesson path, and handoff.
- Lesson progression follows the blueprint cleanly: mental model, passive recon, active mapping, then test-plan construction.
- Observation, inference, and validation boundaries are explicit throughout.
- Artifact system is present and practical: worksheet, route map, cheat sheet, and lab all reinforce the same workflow.
- Module 04 hands off cleanly into Module 05 without collapsing into proxy or fuzzing content too early.

### Residual risks

- The module currently relies on Mermaid and prose examples rather than screenshots; that is acceptable now, but future screenshots could strengthen self-paced usability further.
- Real lab environments vary widely, so instructors or future authors may eventually want additional scenario packs with different app shapes such as CMS, API-first, and SSO-heavy targets.

---

## Recommendation

Keep the module as implemented.

No structural revisions are justified at this stage.
Future improvements should be additive and bounded:

- optional screenshots for especially abstract sections
- optional extra labs for distinct web target types

Those are enrichments, not blockers.
