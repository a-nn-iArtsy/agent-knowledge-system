# Review-Me — Template Evolution Queue

This folder is the **human review gate** for template evolution.

When an agent building a persona adds fields beyond the canonical templates,
it reverse-engineers a generalized version and submits it here. A human
decides whether the generalized pattern is worth promoting into the system.

---

## The Flow

```
Agent builds a persona
    ↓
Agent adds field X (domain-specific, justified by expertise)
    ↓
Agent asks: "What is the underlying pattern here?"
    ↓
Agent submits generalized version → this folder
    ↓
Human reviews: PROMOTE / VARIANT / REJECT / DEFER
    ↓
If PROMOTE → field added to canonical template (version bump)
If VARIANT → field added as a typed delta (e.g., game-dev only)
If REJECT  → stays in role file only; not generalized
If DEFER   → needs more examples from other domains first
```

---

## Real Example: How This Works

**Domain-specific field added to a Roblox developer persona:**
```yaml
exploit_surface_awareness:
  # Roblox's client-server model creates specific exploit vectors.
  # This field captures what attack patterns this developer must
  # recognize and design against.
  remoteevents_validation: "Never trust client-fired RemoteEvents..."
  replication_hygiene: "Server-side state is authoritative..."
```

**Reverse-engineered generalized pattern:**
- Field name: `adversarial_input_surface_awareness`
- Underlying pattern: *"Recognizing and pre-empting known attack vectors
  specific to the untrusted-input operating environment of this role"*
- Applies to: game-dev agents, security engineers, smart contract developers,
  content moderation roles, any role where external/user inputs are adversarial

**Decision:** VARIANT — add to a `game-dev` and `security` agent template delta,
not to the master agent-profile template (too specific for general use).

---

## Submission File Naming

```
[role-slug]--[field-slug]--[YYYY-MM-DD].yaml
```

Examples:
- `roblox-developer--exploit-surface-awareness--2026-05-12.yaml`
- `pe-partner--vintage-year-risk-adjustment--2026-05-20.yaml`
- `surgeon--sterile-field-discipline--2026-06-01.yaml`

---

## Reviewer Notes

Files in this folder are not urgent — review them in batches, not one-by-one.
The goal is to catch patterns that appear in 3+ domains and are worth standardizing.

A single domain-specific addition is almost never worth promoting.
Two domains is interesting. Three domains is a pattern worth generalizing.

Check this folder:
- After every 5–10 new personas are built
- Before starting a new domain (review what prior agents added)
- When you notice a gap in the canonical templates from using the system
