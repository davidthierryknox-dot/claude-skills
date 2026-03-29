---
name: TMK
description: Increases LLM performance on planning tasks using the Task-Method-Knowledge (TMK) framework (Murdock 2001; Goh, Kos & Goel 2026). USE WHEN user says "use TMK", "apply TMK", "TMK framework", "TMK prompt", "structure this planning problem", "improve planning accuracy", or wants to convert domain knowledge into TMK JSON for better LLM planning. Proven up to 65.8% accuracy gain on symbolic planning tasks.
---

# TMK

The Task-Method-Knowledge (TMK) framework structures planning prompts as formal JSON, steering LLMs away from linguistic pattern-matching toward symbolic reasoning. Research shows up to 65.8% accuracy gain (o1 on Random Blocksworld, from 31.5% → 97.3%).

## Voice Notification

**When executing a workflow, do BOTH:**

1. **Send voice notification**:
   ```bash
   curl -s -X POST http://localhost:8888/notify \
     -H "Content-Type: application/json" \
     -d '{"message": "Running WORKFLOWNAME in TMK skill"}' \
     > /dev/null 2>&1 &
   ```

2. **Output text notification**:
   ```
   Running **WorkflowName** in **TMK**...
   ```

## Workflow Routing

| Workflow | Trigger | File |
|----------|---------|------|
| **Apply** | "use TMK", "apply TMK", "TMK prompt", wrap existing problem | `Workflows/Apply.md` |
| **Build** | "build TMK", "create TMK", "new TMK domain", construct from scratch | `Workflows/Build.md` |

## Quick Reference

**TMK JSON top-level structure:**
```json
{
  "Goals": [...],       // Tasks: WHY — goals with given/makes (pre/post-conditions)
  "Mechanisms": [...],  // Methods: HOW — operations with requires/provides/process
  "Knowledge": {        // Domain: WHAT — concepts and relations
    "Concepts": [...],
    "Relations": [...]
  }
}
```

**System prompt wrapper (prepend to any TMK-structured prompt):**
> "You must adhere strictly to the JSON below, paying attention to the rules, ensuring to use only legal moves to achieve the final plan."

**Full schema + worked example:** `TmkReference.md`

## Examples

**Example 1: Apply TMK to an existing planning problem**
```
User: "Use TMK to help me plan a software deployment sequence"
→ Invokes Apply workflow
→ Extracts domain actions (deploy, rollback, test, notify)
→ Builds Goals with given/makes, Mechanisms with requires/provides
→ Constructs Knowledge (concepts: service, environment, version)
→ Outputs TMK JSON + system prompt ready to use
```

**Example 2: Build TMK for a new domain from scratch**
```
User: "Build a TMK structure for a recipe cooking domain"
→ Invokes Build workflow
→ Guides: What objects exist? What actions? What are pre/post conditions?
→ Constructs layer by layer: Knowledge → Goals → Mechanisms
→ Produces validated TMK JSON structure
```

**Example 3: Direct invocation**
```
User: "Use TMK — I need to plan warehouse restocking"
→ Invokes Apply workflow
→ Identifies domain: shelves, items, forklifts, zones
→ Builds complete TMK JSON
→ Provides final prompt ready to paste into any LLM
```
