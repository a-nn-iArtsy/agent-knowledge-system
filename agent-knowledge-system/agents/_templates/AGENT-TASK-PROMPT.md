# AGENT TASK PROMPT — Building a Specialized Persona
## Copy-paste this as the instruction to any agent building a new persona or role.
## Fill in the [BRACKETED] fields before sending.

---

You are building a specialized professional persona for the agent knowledge system.

**Your assignment:** `[ROLE TITLE]`
**Domain:** `[DOMAIN e.g. finance / game-dev / legal / operations]`
**Persona variant (if named individual):** `[NAME or "none — build base archetype"]`

---

## STEP 1 — Pull the templates

Fetch the canonical template scaffolds from the repository:
`https://github.com/a-nn-iArtsy/agent-knowledge-system`

You need these files:
- `agents/_templates/agent-profile.template.yaml` — for the role profile
- `agents/_templates/persona-variant.template.yaml` — if building a named individual
- `skills/_templates/skill-master.template.yaml` — for each skill file
- `knowledge-trees/_templates/knowledge-tree.template.yaml` — for the knowledge tree
- `relationships/_templates/relationship.template.yaml` — for relationship files

Read every field in every template before you begin filling anything in.

---

## STEP 2 — Fill every field

Complete every field in the template. Do not skip fields.

**If a field genuinely does not apply** to this role: write `null` with a one-line
explanation of why it doesn't apply. Never leave a field blank.

**Quality bar** (from the template validation checklists):
- `expert_insight` must differ from `summary` — not a restatement
- `common_errors` must include at least one mistake that an experienced practitioner makes, not just a novice
- Skill entries must capture HOW and WHEN NOT, not just WHAT
- Knowledge tree nodes must reach L5 (variance_points, judgment_calls, specific facts) in at least 30% of branches
- Persona variant entries must be behavioral delta maps with sourced evidence — not biographies

Use web search extensively. Surface:
- Primary sources (publications, interviews, documented decisions, legal filings)
- Practitioner communities and forums for insider vocabulary
- Case studies, post-mortems, and retrospectives for failure modes
- Named individuals whose approach diverges from the standard archetype

---

## STEP 3 — Extend if justified

You are **permitted and encouraged** to add fields beyond the canonical template
if the expertise of this role genuinely requires it.

**Rules for extensions:**
- Add the field directly to the file with an inline comment explaining:
  - What it captures
  - Why the canonical template doesn't cover it
  - What a shallow fill looks like vs. an expert-grade fill
- Do not invent fields just to appear thorough. Only add a field if:
  - Omitting it would leave a meaningful gap in the role's expert representation
  - It would change how an AI agent reasons or communicates for this role

**Example of a justified extension:**
A Roblox developer persona might add:
```yaml
exploit_surface_awareness:
  # Roblox's client-server architecture creates exploit vectors that
  # standard "software engineer" templates don't capture. This field
  # documents the specific attack patterns this developer must recognize
  # and design against — a core competency distinguishing Roblox dev
  # from general game dev.
```

---

## STEP 4 — Reverse-engineer your extensions

After completing the persona, for **every field you added beyond the canonical template**:

1. Write a reverse-engineered, generalized version of the field
2. Ask: "What is the underlying pattern here that could apply beyond this specific domain?"
3. Submit it as a review-me entry

**The Roblox example generalized:**
`exploit_surface_awareness` → `adversarial_input_surface_awareness`
Applies to: any role in a domain where user-generated content, external inputs,
or untrusted actors are part of the operating environment
(game dev, security, smart contract dev, content moderation, etc.)

Submit each generalized field using the review-me template at:
`templates/review-me/SUBMISSION.template.yaml`

Save your submission to:
`templates/review-me/[ROLE-SLUG]--[FIELD-SLUG]--[YYYY-MM-DD].yaml`

---

## STEP 5 — Version the templates you touched

If you added fields to the canonical template structure (even informally, via inline
additions), update the version comment at the top of the affected template file:

```yaml
# schema_version: 1.1  (was 1.0)
# changed_by: [agent task: ROLE-TITLE, DATE]
# change_summary: Added [field_name] — see review-me/[submission file]
```

Do NOT modify the canonical `_templates/` files directly.
Your extensions live in the completed role file, not the template.
The versioning comment is your signal to the human reviewer that something new was tried.

---

## DELIVERABLES

When complete, you should have created:
- [ ] `agents/[domain]/[role-slug]/profile.yaml`
- [ ] `agents/[domain]/[role-slug]/knowledge-tree.yaml`
- [ ] `agents/[domain]/[role-slug]/skills.yaml` (list of skill IDs)
- [ ] `agents/[domain]/[role-slug]/relationships.yaml`
- [ ] `skills/[domain]/[skill-slug].skill.yaml` — one per skill (if new skills needed)
- [ ] `agents/[domain]/[role-slug]/variants/[name].yaml` — if building a named individual
- [ ] `templates/review-me/[role-slug]--[field]--[date].yaml` — one per extension added
- [ ] Updated `registry/role-registry.yaml` entry for the new role
- [ ] Updated `registry/skill-registry.yaml` entries for any new skills

---

## QUALITY GATE

Before declaring the persona complete, run the validation checklist embedded
in each template file. A persona that fails more than 20% of its checklist
items should NOT be marked complete — fix the gaps first.

The hardest checklist items to pass (and therefore the most important):
- `impostor_tells` in the profile (what does an AI sound like when it has
  the credential but not the expertise?)
- `variance_points` in the knowledge tree (which named experts diverge and how?)
- `failure_modes` targeting proficient practitioners, not just novices
- `when_this_matters` being a real concrete scenario, not a generic statement
