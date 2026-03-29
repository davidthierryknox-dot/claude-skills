# TMK Apply Workflow

Apply the TMK framework to an existing planning problem. Takes a user's domain description and constructs a complete TMK JSON prompt.

## Voice Notification

```bash
curl -s -X POST http://localhost:8888/notify \
  -H "Content-Type: application/json" \
  -d '{"message": "Running Apply in TMK skill"}' \
  > /dev/null 2>&1 &
```

Running **Apply** in **TMK**...

## Reference

Load before executing: `~/.claude/skills/TMK/TmkReference.md`

## Step 1: Extract Domain Elements

From the user's description, identify:

**Objects (→ Knowledge Concepts):**
- What physical or logical entities exist in this domain?
- What states can those entities be in? (→ state predicates)

**Actions (→ Goals + Mechanisms):**
- What discrete operations can be performed?
- For each action: What must be true BEFORE? (preconditions → `given`)
- For each action: What becomes true AFTER? (postconditions → `makes`)

**Relationships (→ Knowledge Relations):**
- How do objects relate to each other or to locations?

## Step 2: Build Knowledge Layer First

Always build Knowledge before Goals — it defines the vocabulary everything else uses.

```json
"Knowledge": {
  "Concepts": [
    {"name": "conceptName", "description": "What it is in this domain."},
    // One entry per domain object type and state predicate
  ],
  "Relations": [
    {"name": "RelationName", "description": "What relationship this encodes."},
    // One entry per relationship between domain objects
  ]
}
```

**Tips:**
- Include both physical objects AND state predicates as Concepts (e.g., `IsClear`, `HandIsEmpty`)
- Relations are binary/n-ary predicates: `On(block, table)`, `Holds(agent, item)`

## Step 3: Build Goals Layer

One Goal entry per available action in the domain.

```json
{
  "name": "ActionName",                        // PascalCase
  "description": "Plain English summary.",
  "inputParameters": ["param1", "param2"],     // What the action operates on
  "outputParameters": ["newState"],
  "given": [                                   // PRECONDITIONS — use Knowledge predicates
    "Predicate(param1)",
    "Relation(param1, param2)"
  ],
  "makes": [                                   // POSTCONDITIONS — what changes
    "NewPredicate(param1)",
    "NOT OldPredicate(param1)"                 // Negation with NOT prefix
  ],
  "mechanism": "ActionNameMechanism"           // MUST match a Mechanism name exactly
}
```

**Precondition/postcondition checklist for each goal:**
- [ ] What must be true for this action to be legal?
- [ ] What new facts become true after execution?
- [ ] What old facts become false after execution? (add `"NOT Predicate(...)"`)
- [ ] Does this action change any relationship between objects?

## Step 4: Build Mechanisms Layer

One Mechanism entry per Goal. The mechanism is the "how" — the procedural execution detail.

```json
{
  "name": "ActionNameMechanism",               // Must match Goal's "mechanism" field
  "description": "Perform {param1} operation.",
  "inputParameters": ["param1", "param2"],
  "outputParameters": ["newState"],
  "type": "operation",
  "requires": [                                // Mirror of goal's "given" (formal predicates)
    "Predicate(param1)"
  ],
  "provides": [                                // Plain English ok — outcomes of execution
    "param1 is now held",
    "previous location is now free"
  ],
  "process": "Remove OldPredicate(param1), add NewPredicate(param1), update states"
}
```

**process field:** Always write as explicit state delta: what's removed, what's added.

## Step 5: Assemble Final Prompt

Combine with the system prompt wrapper:

```
You must adhere strictly to the JSON below, paying attention to the rules, ensuring to use only legal moves to achieve the final plan.
{
  "Goals": [...],
  "Mechanisms": [...],
  "Knowledge": {...}
}

Below, within [Plan] and [Plan End], is the format you will use for the answer. The first one is an example. Focus on only the second plan.

[STATEMENT]
As initial conditions I have that, [describe example initial state].
My goal is to have that [describe example goal state].

My plan is as follows:

[PLAN]
[example plan steps]
[PLAN END]

[STATEMENT]
As initial conditions I have that, [describe ACTUAL initial state].
My goal is to have that [describe ACTUAL goal state].

My plan is as follows:

[PLAN]
```

## Step 6: Output

Provide the user:
1. **The complete TMK JSON** — ready to use
2. **The assembled prompt** — with system wrapper and their specific planning problem
3. **Domain summary** — brief table of Goals identified and their preconditions

## Validation Checklist

- [ ] Every Goal has a corresponding Mechanism (name match)
- [ ] All predicates in `given`/`makes` reference concepts defined in Knowledge
- [ ] All `NOT` postconditions are explicitly listed in `makes`
- [ ] `process` field describes exact state delta (remove X, add Y)
- [ ] System prompt wrapper is prepended
- [ ] Parameter names are consistent across Goals and Mechanisms
