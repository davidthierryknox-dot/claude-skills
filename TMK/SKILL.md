---
name: TMK
description: Increases LLM performance on planning tasks using the Task-Method-Knowledge (TMK) framework (Murdock 2001; Goh, Kos & Goel 2026). USE WHEN user says "use TMK", "apply TMK", "TMK framework", "TMK prompt", "formalize this multi-step planning domain", "convert this domain into TMK JSON", or "strict preconditions/postconditions for a planning task". Proven up to 65.8% accuracy gain on symbolic planning tasks.
---

# TMK

TMK (Task-Method-Knowledge) structures planning prompts as formal JSON — Goals (WHY, pre/postconditions), Mechanisms (HOW, procedural steps), Knowledge (WHAT, domain concepts/relations) — steering LLMs from linguistic pattern-matching to symbolic reasoning. Research shows up to 65.8% accuracy gain (o1 on Random Blocksworld: 31.5% → 97.3%).

## Routing

| Workflow | Trigger | File |
|----------|---------|------|
| **Apply** | "use TMK", "apply TMK", "TMK prompt", wrap existing problem | `Workflows/Apply.md` |
| **Build** | "build TMK", "create TMK", "new TMK domain", construct from scratch | `Workflows/Build.md` |

## Schema Summary

```json
{
  "Goals": [{ "name": "PascalCase", "description": "≤15 words", "inputParameters": [], "outputParameters": [], "given": ["Predicate(param)"], "makes": ["NewPredicate(param)", "NOT OldPredicate(param)"], "mechanism": "ActionNameMechanism" }],
  "Mechanisms": [{ "name": "ActionNameMechanism", "description": "≤15 words", "inputParameters": [], "outputParameters": [], "type": "operation", "requires": ["Predicate(param)"], "provides": ["≤15 words, plain English"], "process": "Remove X, add Y — ≤15 words" }],
  "Knowledge": { "Concepts": [{ "name": "camelCase", "description": "≤15 words" }], "Relations": [{ "name": "PascalCase", "description": "≤15 words" }] }
}
```

**System prompt wrapper:** `"You must adhere strictly to the JSON below, paying attention to the rules, ensuring to use only legal moves to achieve the final plan."`

**Full schema + worked example:** `TmkReference.md`

## Apply Checklist

- [ ] Every Goal has a corresponding Mechanism (name match)
- [ ] All predicates in `given`/`makes` reference Knowledge concepts
- [ ] All `NOT` postconditions listed in `makes`
- [ ] `process` field is explicit state delta (remove X, add Y)
- [ ] System prompt wrapper prepended
- [ ] Parameter names consistent across Goals and Mechanisms

## Build Checklist

- [ ] Every Goal has exactly one Mechanism
- [ ] Every predicate defined in Knowledge
- [ ] All parameter names consistent
- [ ] Every relationship change has `NOT OldRelation(...)` in `makes`
- [ ] All inferred/assumed fields marked `// assumed`
