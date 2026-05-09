# Blue Book Reference Map

## Purpose

This document records how selected ideas from *Skil 蓝皮书 2026* (Jason Zhu, v1.1, based on 67,196 Skill data points from AgentSkillsHub) are referenced by the current Director's Cut Skill system.

This document does **not** redefine the Skill format, does **not** override the existing modular migration result, and does **not** require retroactive restructuring.

The current system remains frozen as:

- `SKILL.md` — lightweight control entry
- `specs/` — policy modules (5 files)
- `templates/` — reusable output structures (2 files)
- `validation/` — verification assets (1 file)
- `migration/monolith-baseline-map.md` — migration baseline

## Non-Goals

This phase does **not**:

- convert the project to the Blue Book's standard Skill folder format
- replace the current modular architecture
- introduce AgentSkillsHub distribution logic
- introduce Verified Creator logic
- use market data to determine file structure
- modify frozen migration results without a separate change request

---

## Reference Area 1: Progressive Loading

### Blue Book Idea

The Blue Book (Ch2) describes three-layer progressive loading as the core mechanism that allows unlimited Skill expansion without context explosion:

- **L1 · description (~50 tokens)**: loaded at every session start. A single sentence—"what this Skill does + when to activate." It determines the Skill's fate—poorly written, the Skill is never opened.
- **L2 · instructions (~500-3,000 tokens)**: loaded only after Agent decides to activate based on L1.
- **L3 · resources (not counted in prompt)**: code templates, sample data, large files. Agent fetches on demand at execution time.

Hub data confirms: 86% of Top 500 SKILL.md files are 5-30KB—the format pressure of 3-layer loading has filtered authors into this range.

Key design insight: description must be rewritten, not copied from instructions. Its function is "directory entry," not "body summary." The most economical formula: "what problem this solves + when to activate + output form preview"—within 50 tokens.

### Current System Mapping

The current Director's Cut system uses a comparable but different layered structure:

| Blue Book Layer | Director's Cut Equivalent |
|---|---|
| L1 · description (~50 tokens) | `SKILL.md` YAML frontmatter `description` + `triggers` — determines activation |
| L2 · instructions | `specs/` (5 policy modules) — loaded when Agent enters a specific Step |
| L3 · resources | `templates/` (2 files) — reusable output structures, fetched when needed |

Key differences:
- Blue Book's L2 is a single flat file; Director's Cut uses 5 module files indexed by a routing `SKILL.md`.
- Blue Book's L3 is file-based resources; Director's Cut's templates are markdown instructions, not code/data.
- Director's Cut's `validation/` layer has no direct Blue Book equivalent (quality checks are after output, not loaded progressively).

### Adoption Decision

**Adopt as a design principle, not as a file-format requirement.**

The existing architecture already follows the spirit of progressive loading—SKILL.md is a light index, specs are loaded per-step, templates are fetched on demand. No restructuring needed.

### Practical Rule

1. The main `SKILL.md` must remain lightweight. New rules should NOT be added to the entry file unless required for routing, priority resolution, or mandatory global behavior.
2. Each `specs/` module must answer its "when to load" clearly in its header (already done via "模块职责" section).
3. Any new reference data (case pools, memory cards, run-time logs) should go into `templates/` or a new `resources/` directory, NOT into `SKILL.md` or `specs/`.

### Non-Adoption Scope

- Blue Book's L1 50-token hard limit: Director's Cut's `description` is longer because it serves a different function (human-triggered rather than Agent-auto-discovered).
- Blue Book's L3 fetch mechanics: Director's Cut does not have code templates or data files that need runtime fetching.

---

## Reference Area 2: Agent-Centric Design

### Blue Book Idea

The Blue Book (Ch4, 宝玉 four philosophies) establishes that Skills should be designed from the Agent's perspective, not the human's:

1. **Agent Perspective (+7.7 quality points)**: Use explicit triggers ("Use when user shares code and says look at this"), explicit output formats ("MUST output a markdown table"), explicit pre-steps ("Run git diff first"). Agent cannot infer from vague instructions like "use when needed."
2. **Script-First (+7.7 points)**: Use code/constants over natural language. "animation: 200ms cubic-bezier(0.23, 1, 0.32, 1)" beats "animation should feel natural." Push decisions from runtime to edit-time.
3. **Atomicity (+15 points)**: One Skill, one purpose. Optimal file size 10-20KB (51.4 quality score). <2KB is too thin (36.3). >40KB degrades (45.2).
4. **Self-Iteration (+8.6 points)**: MISTAKES.md records error → root cause → fix → lesson. Only 1.2% of authors do this.

The four philosophies compound: Skills with 3-4 of them average 63.4 quality score vs. Top 500 average of 47.2.

Critical design rule from L2 instructions: the first 200 words must answer 5 questions (what it does exactly, input, output, prerequisites, failure handling). Use decision trees, not prose. Explicitly ban anti-patterns with "DO NOT" sections.

### Current System Mapping

The Director's Cut system was designed with Agent-centric principles independently, not derived from the Blue Book:

| Blue Book Principle | Director's Cut Equivalent |
|---|---|
| Agent Perspective (explicit triggers) | YAML `triggers` field with 15+ Chinese/English trigger phrases; `MUST` rules in "最高优先级规则" |
| Script-First | Not directly applicable—Director's Cut is a writing Skill, not a code Skill. Closest equivalent: skeleton template with explicit structure requirements |
| Atomicity | Modular architecture: 8 files with clear single responsibilities, each module states its scope in "模块职责" |
| Self-Iteration | v1.1/v1.2 changelog in SKILL.md; `monolith-baseline-map.md` migration status tracking |

Key differences:
- Director's Cut is a **writing/editing** Skill, not a **code/engineering** Skill. "Script-first" (hardcoded constants, lookup tables) has no direct equivalent in prose generation.
- Director's Cut's atomicity is file-level (spec per concern), not content-level (10-20KB sweet spot).

### Adoption Decision

**Adopt Agent Perspective and Atomicity as maintenance principles. Script-First is not applicable to this Skill type. Self-Iteration should be strengthened.**

### Practical Rules

1. **Agent Perspective already strong**: `description` uses explicit triggers; "最高优先级规则" uses `MUST`/`不得` language. Keep this standard.
2. **Decision tree adoption**: When adding new rules to `specs/`, prefer decision-tree format over prose. Example: "If 素材类型 = 长文章 → skip 机制提炼 → go to Step 2 directly" over "对于长文章类型，通常不需要提炼机制。"
3. **Anti-pattern bans**: Each `specs/` module should have an explicit "DO NOT" or "禁止" section listing what the module does NOT handle. Currently some modules have this (e.g., "本模块只负责入口判断，不负责正文写作") but it could be more systematic.
4. **Atomicity check**: Total SKILL.md is 442 lines (~15KB). Combined specs+templates+validation ~100KB. Each module is 3-8KB. This aligns with Blue Book's sweet spot findings.

### Non-Adoption Scope

- Script-first: Not applicable to writing Skills.
- 50-token description formula: Director's Cut's `description` field serves a different discovery model (human slash-command vs. Agent auto-detection).

---

## Reference Area 3: Atomic Module Boundaries

### Blue Book Idea

The Blue Book (Ch4.2, Ch6) establishes atomicity as the single biggest quality lever (+15 points):

- One Skill = one purpose. Not "the shorter the better"—optimal is 10-20KB.
- <2KB Skills are under-documented (36.3 quality score).
- >40KB Skills suffer from scope creep—Agent doesn't know when to activate them (45.2).
- The 9 functional types (Reference, Data Acquisition, Scaffolding, CI/CD, Code Quality, Documentation, Workflow, Persona, Communication) emerged from Hub data, not from a top-down spec.
- Only 3 types recommended for new authors: Reference, CI/CD, Code Quality.

### Current System Mapping

Director's Cut's modular architecture independently converged on similar principles:

| Blue Book Concept | Director's Cut Equivalent |
|---|---|
| One Skill, one purpose | Each `specs/` file has one clear responsibility declared in its header "模块职责" |
| 10-20KB sweet spot | SKILL.md ~15KB (442 lines); spec files 3-8KB each |
| Scope creep prevention | "本模块只负责 X，不负责 Y" pattern in every module header |
| 9 functional types | 5 policy domains: source-and-mode, writing, case, memory-rag, output |
| Skill type selection advice | Only 3 recommended types—Director's Cut is naturally a "Reference/Workflow" hybrid |

Key structural difference: Blue Book envisions one Skill = one SKILL.md file. Director's Cut uses one SKILL.md + multiple spec modules. The Blue Book does not discuss multi-file Skill architectures. However, the *intent* of atomicity (clear boundaries, no scope creep) is preserved.

### Adoption Decision

**Adopt the 10-20KB sweet spot as a maintenance guardrail for individual modules. Formalize module boundary declarations.**

### Practical Rules

1. **Module size guardrail**: Any new `specs/` module should be 3-12KB. Existing modules are within range. If a module exceeds 15KB, split it.
2. **Boundary enforcement**: Each module's "模块职责" section must explicitly answer: (a) what this module decides, (b) what it does NOT decide, (c) which other module handles the excluded concerns.
3. **No scope creep**: When adding new rules, first check which module owns that concern. If no module owns it, create a new module rather than appending to an existing one.
4. **DO NOT section**: Add an explicit "本模块不负责" (anti-scope) section to every module that currently lacks one.

### Non-Adoption Scope

- Blue Book's 9-type classification: Not applicable. Director's Cut is a single-purpose writing Skill, not a multi-type ecosystem.
- Blue Book's 4-level sharing path (Personal→Project→Team→Global): Director's Cut is project-level by design. Distribution is not a design concern at this stage.

---

## Reference Area 4: Iteration Loop

### Blue Book Idea

The Blue Book (Ch5) establishes iteration as the difference between life and death:

- **15× star growth rate difference**: continuously-committed Skills 58.8% still gaining stars; frozen ones 3.8%.
- **Death inflection point**: Month 10—survival drops from 77-83% (months 6-9) to 69%.
- **Three iteration mechanisms**:
  1. MISTAKES.md (manual + honest): 4-field format—error scene → root cause → fix → lesson. Only 6 Skills in Top 500 do this. Their average quality score is 55.8 vs. 47.2 overall.
  2. Regular commits (manual + disciplined): at least 1 commit every 90 days. System only checks "is it breathing."
  3. Autoreason 3-way tournament (automated + memoryless): 3 independent agents (critic, author, synthesizer) + 7 judges via Borda voting. "Change nothing" is always a valid option.
- **Iteration can also kill**: over-iteration without deletion leads to SKILL.md growing 5KB→50KB and quality_score dropping 60→45. Good iteration = targeted fix + removal of redundancy. Bad iteration = unlimited addition.

### Current System Mapping

Director's Cut has iteration infrastructure but not a formal iteration discipline:

| Blue Book Practice | Director's Cut Equivalent | Status |
|---|---|---|
| MISTAKES.md | No equivalent | **Missing** |
| 90-day commit rule | v1.1/v1.2 version changelog in SKILL.md | Partial |
| Targeted fix + deletion | Migration map with "done/deferred" status tracking | Partial |
| Autoreason | Not applicable (writing Skill, not code Skill) | N/A |

The migration map's "第三阶段第三轮：修复记录与最终冻结" records 5 optimization items as "recorded, not fixed." This is functionally similar to a MISTAKES.md but stored in the migration baseline rather than a dedicated file.

### Adoption Decision

**Adopt the MISTAKES.md pattern and 90-day review rule. Create a lightweight iteration log.**

### Practical Rules

1. **Create `validation/mistakes-log.md`**: A dedicated file for recording errors encountered during actual use. 4-field format: 错误现场 → 根本原因 → 修复方案 → 预防教训. Each entry ≤ 200 words. Target: 3-5 entries before first review.
2. **90-day review trigger**: Every 90 days, review `mistakes-log.md` and fold fixes back into relevant `specs/` modules. Delete obsolete or redundant rules during the same pass.
3. **Commit discipline**: Each modification to a spec/template file should remove at least 1 line of obsolete content OR fix 1 specific bug. Never "add only."
4. **Do NOT iterate on**: Claude/Cursor version bumps, other people's interesting rules, "it's been a while so let me change something."

### Non-Adoption Scope

- Autoreason: Writing quality cannot be judged by a 3-way tournament. Human review is the final arbiter.
- Exact commit frequency targets: Director's Cut is a project-internal Skill, not a public GitHub repo. Star growth metrics are irrelevant.

---

## Reference Area 5: Validation-First Maintenance

### Blue Book Idea

The Blue Book embeds validation at multiple levels but does not have a standalone "validation" chapter. Key validation ideas are scattered:

- **L1 validation**: description with "Use when / MUST / Output format" phrases scores +7.7 quality points. "Do NOT use when" is as important as "Use when."
- **L2 validation**: instructions must answer 5 questions in the first 200 words. Decision trees beat prose.
- **Quality score dimensions**: completeness, clarity, specificity, examples, readme_structure, agent_readiness (6 dimensions in Hub's scoring algorithm).
- **Self-check habit**: before publishing, verify: does this Skill still do what it claims? Are triggers unambiguous? Are anti-patterns explicit?

The Blue Book's own quality score algorithm has acknowledged flaws (Ch3.7): 76.8% of Skills cluster at 20-39, none score above 80. Top 20 Skills average only 46.8.

### Current System Mapping

Director's Cut has a formal validation system that is more structured than the Blue Book's:

| Blue Book Validation | Director's Cut Equivalent |
|---|---|
| Description quality check | `SKILL.md` frontmatter with explicit `triggers` and `description` |
| Instructions quality check | Each `specs/` module has "模块职责" answering scope questions |
| Output quality check | `validation/validation-checklist.md` with 22 check items covering 主问题/问题链/机制/案例/成稿连续性/语气/版权 |
| Mode-specific validation | Quick/Standard/Deep verification rules in validation checklist |
| No formal quality score | Migration map's 9-scenario stress test serves as quality benchmark |

Director's Cut's validation is more rigorous than the Blue Book's in several ways:
- 22 explicit pass/fail check items (vs. Blue Book's 6-dimension continuous score)
- Mode-specific checks (Quick 1500-2500 words, Standard 3500-5000, Deep 6000-8000)
- Style verification (4 subjective checks: "我被解释了" not "我又被教育了")

### Adoption Decision

**Strengthen the validation layer with Blue Book-inspired additions. Current system is already ahead of Blue Book in validation rigor—do not degrade it.**

### Practical Rules

1. **Add "激活边界检查" to validation checklist**: Before producing output, verify the Skill should have been activated. Check against "do NOT use when" conditions. This mirrors Blue Book's L1 anti-pattern rule.
2. **Add "指令清晰度检查"**: Verify that any new spec rules use decision-tree format rather than prose where applicable. Check that the first 200 words of each spec answers the 5 questions.
3. **Maintain the 22-item checklist**: It is more comprehensive than the Blue Book's quality dimensions. Do not reduce it.
4. **Keep the 9-scenario stress test as a regression suite**: When modifying any spec, mentally run through the 9 scenarios to verify no breakage.

### Non-Adoption Scope

- Blue Book's quality_score algorithm: Director's Cut does not need a numerical quality score. Pass/fail checklists are more appropriate for a writing Skill.
- Hub's 6-dimension scoring model: Designed for code/engineering Skills, not applicable to writing Skills.

---

## Reference Area 6: Obsolescence and Maintenance Risk

### Blue Book Idea

The Blue Book (Ch3.5, Ch5) documents severe maintenance risks in the Skill ecosystem:

- **Skill half-life: 6-12 months**. Most star Skills die within 1 year of last commit.
- **"Zombie King" phenomenon**: Skills with 1,000+ stars but 180+ days without updates. 20,816-star Skills sitting dead with no announcement, no fork takeover, no explanation.
- **Skills are more dangerous than regular packages when abandoned**: regular packages warn users on deprecation; abandoned Skills silently produce outdated/incorrect results.
- **54% one-and-done authors**: 17,833 authors published exactly 1 Skill then never again.
- **Death inflection point at month 10**: survival drops from 77-83% to 69%.
- **Over-iteration risk**: authors who commit weekly but only add rules, never delete, see quality_score drop from 60 to 45.

### Current System Mapping

Director's Cut has explicit anti-obsolescence measures built into its architecture:

| Blue Book Risk | Director's Cut Mitigation | Status |
|---|---|---|
| Half-life decay | Migration map records complete history of all changes; each module has a traceable origin in the monolith | Strong |
| Zombie King | "冻结" state declaration prevents silent drift; migration map serves as a "last known good" reference | Strong |
| Author abandonment | Modular architecture allows partial updates without full rewrite | Medium |
| Over-iteration | Each module has explicit scope boundaries preventing unlimited growth | Medium |

Key structural advantage: Director's Cut's modular architecture with a migration baseline is inherently more maintainable than a monolith. If one spec file becomes outdated, it can be updated independently. The migration map prevents "why was this rule put here?" confusion.

### Adoption Decision

**Formalize the anti-obsolescence measures. The modular architecture is already a strong defense—document it as such.**

### Practical Rules

1. **6-month module review**: Every 6 months, review each `specs/` module. Check: (a) is this rule still correct? (b) has any external dependency (Claude behavior, tool capability) changed? (c) is there accumulated cruft to delete?
2. **Breathing signal**: At minimum, update `validation/mistakes-log.md` once every 90 days. This serves the same function as Blue Book's "commit to prove you're alive" rule but adapted to a project-internal Skill.
3. **Anti-zombie declaration**: If this Skill is ever deprecated, add a prominent notice at the top of `SKILL.md` and in each `specs/` header. Never let it silently rot.
4. **Deletion discipline**: When adding a rule, consider deleting an obsolete one. The migration map's "deferred" items are candidates for future deletion review.

### Non-Adoption Scope

- Public GitHub metrics (stars, forks, watchers): Not applicable to a project-internal Skill.
- AgentSkillsHub indexing: Not applicable.
- Verified Creator maintenance requirements: Not applicable.

---

## Summary: What to Actually Do

Based on the six reference areas above, the following concrete actions are recommended for a future optimization phase (NOT this phase):

### Immediate (this phase — documentation only)

- [x] Create `migration/blue-book-reference-map.md` (this file)

### Phase 4 Candidates (future, requires separate approval)

1. **Create `validation/mistakes-log.md`** — 4-field error log template (Ref Area 4)
2. **Add "DO NOT" sections to specs lacking them** — `source-and-mode-policy.md` already has scope boundaries; others may need explicit anti-scope declarations (Ref Area 2, 3)
3. **Add 2 check items to `validation/validation-checklist.md`** — 激活边界检查 + 指令清晰度检查 (Ref Area 5)
4. **Define 90-day review cadence** — breathing signal for maintenance (Ref Area 4, 6)
5. **Define 6-month module review** — anti-obsolescence measure (Ref Area 6)

### Never (explicitly excluded)

- Restructuring to Blue Book's single-file SKILL.md format
- Adding quality_score or numerical scoring
- Introducing distribution/marketing concerns
- Adding AgentSkillsHub integration
- Adding Verified Creator logic
- Changing the existing directory structure
- Rewriting any existing SKILL.md or spec file for Blue Book compliance

---

## Document Metadata

- **Created**: 2026-05-09
- **Based on**: *Skil 蓝皮书 2026* v1.1, Jason Zhu (@GoSailGlobal), 2026-04-28
- **Original data**: AgentSkillsHub Supabase, 67,196 Skills, snapshot 2026-04-22 to 2026-04-28
- **License**: CC BY-NC-SA 4.0 (original Blue Book)
- **This document**: Part of the Director's Cut Skill system, MIT license
