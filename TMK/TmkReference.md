# TMK Reference

Task-Method-Knowledge framework reference. Source: "Knowledge Model Prompting Increases LLM Performance on Planning Tasks" (Goh, Kos & Goel, 2026, arXiv:2602.03900).

---

## Core Concept

TMK is a **symbolic steering mechanism**. By imposing formal JSON structure on domain knowledge, it shifts LLM inference from linguistic approximation to symbolic manipulation — activating the model's code-execution reasoning pathways rather than its default linguistic ones.

**Key result:** o1 model on Random Blocksworld: 31.5% (plain text) → 97.3% (TMK). A 65.8% gain.

**Why it works:**
- TMK's nested JSON resembles code training data, activating formal reasoning pathways
- Explicit pre/post-conditions (given/makes, requires/provides) eliminate ambiguity
- Teleological structure (WHY → HOW → WHAT) mirrors how domain experts think about planning
- Performance inversion effect: hardest symbolic tasks (random/opaque tokens) benefit most

---

## Full JSON Schema

```json
{
  "Goals": [
    {
      "name": "ActionName",                    // PascalCase, matches a domain action
      "description": "Human-readable summary of what this goal achieves.",
      "inputParameters": [                     // What the goal consumes
        "param1",
        "param2"
      ],
      "outputParameters": [                    // What the goal produces
        "newState"
      ],
      "given": [                               // PRECONDITIONS — must be true to execute
        "Predicate(param1)",
        "Relation(param1, param2)"
      ],
      "makes": [                               // POSTCONDITIONS — true after execution
        "NewPredicate(param1)",
        "NOT OldPredicate(param1, param2)"
      ],
      "mechanism": "ActionNameMechanism"       // Links to the corresponding Mechanism
    }
  ],
  "Mechanisms": [
    {
      "name": "ActionNameMechanism",           // Matches the "mechanism" field in Goals
      "description": "Perform {param1} operation.",
      "inputParameters": [
        "param1",
        "param2"
      ],
      "outputParameters": [
        "newState"
      ],
      "type": "operation",                     // Always "operation" for atomic actions
      "requires": [                            // Logical prerequisites (mirrors given)
        "Predicate(param1)",
        "Relation(param1, param2)"
      ],
      "provides": [                            // Logical outcomes (plain English ok here)
        "NewPredicate(param1)",
        "param2 is now free"
      ],
      "process": "Remove OldPredicate(param1), add NewPredicate(param1), update states"
    }
  ],
  "Knowledge": {
    "Concepts": [
      {
        "name": "conceptName",                 // camelCase
        "description": "What this concept represents in the domain."
      }
    ],
    "Relations": [
      {
        "name": "RelationName",               // PascalCase
        "description": "What relationship this encodes between domain objects."
      }
    ]
  }
}
```

---

## Worked Example: Classic Blocksworld (from Appendix A.3)

This is the exact JSON used in the paper's experiments.

```json
{
  "Goals": [
    {
      "name": "PickUpBlock",
      "description": "Pick up a block from the table.",
      "inputParameters": ["block", "configuration"],
      "outputParameters": ["newConfiguration"],
      "given": ["On(block, table)", "IsClear(block)", "HandIsEmpty()"],
      "makes": ["Holding(block)", "NOT On(block, table)", "NOT HandIsEmpty()"],
      "mechanism": "PickUpBlockMechanism"
    },
    {
      "name": "PutDownBlock",
      "description": "Put down a held block onto the table.",
      "inputParameters": ["block", "configuration"],
      "outputParameters": ["newConfiguration"],
      "given": ["Holding(block)"],
      "makes": ["On(block, table)", "IsClear(block)", "HandIsEmpty()"],
      "mechanism": "PutDownBlockMechanism"
    },
    {
      "name": "StackBlock",
      "description": "Stack a held block onto another clear block.",
      "inputParameters": ["blockToStack", "blockTarget", "configuration"],
      "outputParameters": ["newConfiguration"],
      "given": ["Holding(blockToStack)", "IsClear(blockTarget)"],
      "makes": [
        "On(blockToStack, blockTarget)",
        "IsClear(blockToStack)",
        "NOT IsClear(blockTarget)",
        "HandIsEmpty()"
      ],
      "mechanism": "StackBlockMechanism"
    },
    {
      "name": "UnstackBlock",
      "description": "Unstack a block from on top of another block.",
      "inputParameters": ["blockToUnstack", "blockFrom", "configuration"],
      "outputParameters": ["newConfiguration"],
      "given": [
        "On(blockToUnstack, blockFrom)",
        "IsClear(blockToUnstack)",
        "HandIsEmpty()"
      ],
      "makes": [
        "Holding(blockToUnstack)",
        "IsClear(blockFrom)",
        "NOT On(blockToUnstack, blockFrom)"
      ],
      "mechanism": "UnstackBlockMechanism"
    }
  ],
  "Mechanisms": [
    {
      "name": "PickUpBlockMechanism",
      "description": "Pick up {block}.",
      "inputParameters": ["block", "configuration"],
      "outputParameters": ["newConfiguration"],
      "type": "operation",
      "requires": ["On(block, table)", "IsClear(block)", "HandIsEmpty()"],
      "provides": ["Holding(block)", "Hand not empty", "Block not on table"],
      "process": "Remove On(block, table), add Holding(block), set hand state"
    },
    {
      "name": "PutDownBlockMechanism",
      "description": "Put down {block}.",
      "inputParameters": ["block", "configuration"],
      "outputParameters": ["newConfiguration"],
      "type": "operation",
      "requires": ["Holding(block)"],
      "provides": ["On(block, table)", "HandIsEmpty()", "IsClear(block)"],
      "process": "Remove Holding(block), add On(block, table), clear hand state"
    },
    {
      "name": "StackBlockMechanism",
      "description": "Stack {blockToStack} on {blockTarget}.",
      "inputParameters": ["blockToStack", "blockTarget", "configuration"],
      "outputParameters": ["newConfiguration"],
      "type": "operation",
      "requires": ["Holding(blockToStack)", "IsClear(blockTarget)"],
      "provides": [
        "On(blockToStack, blockTarget)",
        "HandIsEmpty()",
        "IsClear(blockToStack)"
      ],
      "process": "Remove Holding(blockToStack), add On(blockToStack, blockTarget), update clear states"
    },
    {
      "name": "UnstackBlockMechanism",
      "description": "Unstack {blockToUnstack} from {blockFrom}.",
      "inputParameters": ["blockToUnstack", "blockFrom", "configuration"],
      "outputParameters": ["newConfiguration"],
      "type": "operation",
      "requires": [
        "On(blockToUnstack, blockFrom)",
        "IsClear(blockToUnstack)",
        "HandIsEmpty()"
      ],
      "provides": ["Holding(blockToUnstack)", "IsClear(blockFrom)"],
      "process": "Remove On(blockToUnstack, blockFrom), add Holding(blockToUnstack), update states"
    }
  ],
  "Knowledge": {
    "Concepts": [
      {
        "name": "block",
        "description": "A block in the blocks world that can be picked up, put down, stacked or unstacked"
      },
      {
        "name": "table",
        "description": "The surface where blocks can be picked up, put down or unstacked onto"
      },
      {
        "name": "hand",
        "description": "The manipulator that can pick up, put down, stack or unstack blocks"
      },
      {
        "name": "IsClear",
        "description": "A block is clear if no other block is on top of it"
      },
      {
        "name": "HandIsEmpty",
        "description": "The hand is not holding any block"
      }
    ],
    "Relations": [
      {
        "name": "On",
        "description": "Relates a block to what it's on top of (another block or table)"
      },
      {
        "name": "Holding",
        "description": "Relates the hand to the block it's holding"
      }
    ]
  }
}
```

---

## The System Prompt Wrapper

Always prepend this to any TMK-structured planning prompt:

```
You must adhere strictly to the JSON below, paying attention to the rules, ensuring to use only legal moves to achieve the final plan.
[TMK JSON here]

Below, within [Plan] and [Plan End], is the format you will use for the answer.

[STATEMENT]
As initial conditions I have that, [describe initial state].
My goal is to have that [describe goal state].

My plan is as follows:

[PLAN]
[PLAN END]
```

---

## Design Guidelines

### Hierarchy Depth
- **3 layers is recommended** for most domains (keeps context window manageable)
- No hard limit — decompose deeper for complex domains as context windows grow
- `verifyPlan` and `checkGoalAchieved` goals can be further decomposed into verification sub-steps

### When TMK Helps Most
- Tasks with **opaque or symbolic tokens** (random strings, unfamiliar names) — biggest gains
- **Multi-step sequential planning** with strict ordering constraints
- Domains where semantic cues are absent or misleading
- Any problem where the LLM defaults to linguistic approximation over formal reasoning

### When TMK May Not Help
- Highly optimized/distilled/quantized models (o1-mini showed regression in Mystery domain)
- Tasks where semantic associations are correct and helpful
- Very simple 1-2 step tasks where overhead outweighs gain

### Output Standardization

**Fixed field order** — always emit fields in this sequence:

| Object | Field order |
|--------|-------------|
| Goal | `name`, `description`, `inputParameters`, `outputParameters`, `given`, `makes`, `mechanism` |
| Mechanism | `name`, `description`, `inputParameters`, `outputParameters`, `type`, `requires`, `provides`, `process` |
| Concept | `name`, `description` |
| Relation | `name`, `description` |

**Naming conventions:**
- `Goals[].name` → PascalCase (e.g., `PickUpBlock`)
- `Mechanisms[].name` → PascalCase + "Mechanism" suffix (e.g., `PickUpBlockMechanism`)
- `Knowledge.Concepts[].name` → camelCase (e.g., `handIsEmpty`)
- `Knowledge.Relations[].name` → PascalCase (e.g., `On`, `Holding`)

**Length caps** (per field):
- `description` → ≤15 words
- `provides` → ≤15 words per entry
- `process` → ≤15 words total

**Provides/makes alignment:** Each `provides` entry must correspond to a `makes` entry in the paired Goal, normalized to plain English. One-to-one mapping required — same facts, different register.

| makes (formal) | provides (plain English) |
|----------------|--------------------------|
| `Holding(block)` | `block is now held` |
| `NOT On(block, table)` | `block no longer on table` |
| `HandIsEmpty()` | `hand is now empty` |

### Abstraction Level
- Goals describe WHAT to achieve (teleological — the why)
- Mechanisms describe HOW to achieve it (procedural — the process)
- Knowledge defines WHAT EXISTS in the domain (ontological — the concepts)
- Keep `given`/`makes` in Goals as formal predicates: `Predicate(param)`
- Keep `provides` in Mechanisms as human-readable (plain English acceptable)
- `process` field: describe state transitions explicitly (what's removed, what's added)
