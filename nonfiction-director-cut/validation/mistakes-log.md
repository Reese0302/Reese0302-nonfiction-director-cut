# Mistakes Log

## Status

```text
Status: Runtime observation log
Authority: Evidence source only
Primary use: Future maintenance review and Phase 4 candidate evaluation
Created: 2026-05-09
```

## Purpose

This file records observed mistakes, weak outputs, ambiguous triggers, policy drift, and repeated runtime failures in the Director's Cut Skill system.

It is inspired by the Blue Book's iteration-loop idea (Ch5, MISTAKES.md pattern), but it does **not** redefine the current Skill architecture and does **not** override any existing policy module.

Its role in the maintenance loop:

```text
记录错误 → 归因模块 → 判断是否重复出现 → 决定是否进入 Phase 4 修改
```

## Non-Authority Statement

This file does **not**:

- define new rules
- override `SKILL.md`
- override files under `specs/`
- replace `validation/validation-checklist.md`
- replace `validation/blue-book-checklist.md`
- require immediate modification after a single observed issue
- change the frozen migration baseline

A mistake entry becomes actionable only after review and approval.

## When to Add an Entry

Add an entry when one of the following occurs:

- the Skill produces an output that violates an existing rule
- the Skill follows the wrong mode or source policy
- the Skill exposes internal module paths unnecessarily
- the Skill uses inconsistent terminology
- the Skill misclassifies a case level
- the Skill over-dramatizes a real-world example
- the Skill fails to mark Chinese-context adaptation as contextual supplementation
- the Skill treats fragmentary material as a full Standard instead of a partial Standard
- the same ambiguity appears in multiple real usage scenarios
- a user correction reveals a gap in the current rule structure

Do **not** add an entry for ordinary preference changes unless the issue exposes a repeatable system-level problem.

## Entry Format

Each entry must use the following structure.

```markdown
## YYYY-MM-DD — Short Issue Title

### 1. Context
Describe the user task, input type, and relevant usage scenario.

### 2. Observed Problem
Describe what went wrong in the actual output or behavior.

### 3. Expected Behavior
Describe what should have happened according to the current Skill rules.

### 4. Likely Cause
Identify the most likely cause. Possible causes include:
- unclear trigger condition
- missing negative example
- module boundary ambiguity
- terminology drift
- insufficient validation coverage
- over-broad rule in `SKILL.md`
- missing rule in a `specs/` module
- output policy conflict
- case policy conflict
- source/mode policy conflict

### 5. Affected Area
Mark the primary affected area:
- [ ] `SKILL.md`
- [ ] `specs/source-and-mode-policy.md`
- [ ] `specs/memory-rag-spec.md`
- [ ] `specs/writing-policy.md`
- [ ] `specs/case-policy.md`
- [ ] `specs/output-policy.md`
- [ ] `templates/trigger-response.md`
- [ ] `templates/skeleton-template.md`
- [ ] `validation/validation-checklist.md`
- [ ] `validation/blue-book-checklist.md`
- [ ] unclear / cross-module

### 6. Severity
Choose one:
- [ ] Low — minor expression issue
- [ ] Medium — repeated quality issue or ambiguous behavior
- [ ] High — violates an explicit rule or causes incorrect mode selection
- [ ] Critical — breaks core architecture, source handling, or user trust

### 7. Recurrence
Choose one:
- [ ] First occurrence
- [ ] Repeated occurrence
- [ ] Pattern confirmed across multiple scenarios

### 8. Proposed Treatment
Choose one:
- [ ] No change; record only
- [ ] Add example to future documentation
- [ ] Clarify checklist item
- [ ] Clarify module trigger
- [ ] Adjust module wording in a future approved phase
- [ ] Consider new rule only after more evidence
- [ ] Requires immediate review before further use

### 9. Decision
- Decision:
- Reviewer:
- Date:
- Follow-up required:
```

## Control Principles

To keep this log lightweight and actionable:

- **Record only when**: the issue violates a rule, exposes a rule gap, repeats across scenarios, is explicitly flagged by a user, affects output credibility, or affects module routing judgment.
- **Do not record**: style preferences, one-off phrasing adjustments, or issues that cannot be reproduced.
- **Review cadence**: entries are reviewed during Phase 4 candidate evaluation, not during normal Skill execution.
- **Maximum entries before review**: if this log exceeds 15 unreviewed entries, schedule a maintenance review.

## Current Entries

*No entries yet.*
