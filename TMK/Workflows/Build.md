# TMK Build Workflow

Interactively construct a TMK structure for a new domain from scratch. Guides the user through domain analysis, layer-by-layer construction, and validation.

## Voice Notification

```bash
curl -s -X POST http://localhost:8888/notify \
  -H "Content-Type: application/json" \
  -d '{"message": "Running Build in TMK skill"}' \
  > /dev/null 2>&1 &
```

Running **Build** in **TMK**...

## Reference

Load before executing: `~/.claude/skills/TMK/TmkReference.md`

## Phase 1: Domain Elicitation

Ask the user these questions (can be combined into one prompt):

```
To build a TMK structure for your domain, I need to understand it:

1. What is the domain? (e.g., warehouse logistics, recipe cooking, CI/CD pipeline)
2. What are the key OBJECTS or entities? (things that exist and can change state)
3. What ACTIONS can be performed? List each one.
4. For each action:
   a. What must be true BEFORE you can do it? (preconditions)
   b. What becomes true AFTER it's done? (postconditions — what changes?)
5. Are there any relationships between objects that matter? (e.g., X is on Y, X holds Y)
```

## Phase 2: Build Knowledge Layer

From user's answers, extract:

**Concepts** = all object types + all state predicates (conditions that can be true/false)
**Relations** = all binary/n-ary relationships between objects

Output draft Knowledge and ask user to confirm or add:

```json
"Knowledge": {
  "Concepts": [
    {"name": "objectType", "description": "What it is."},
    {"name": "StatePredicate", "description": "A condition that can be true or false."}
  ],
  "Relations": [
    {"name": "RelationName", "description": "How objects relate."}
  ]
}
```

**Checkpoint:** "Does this capture all the concepts and relationships in your domain? Anything missing?"

## Phase 3: Build Goals Layer

For each action identified in Phase 1, construct a Goal.

Walk through each action one by one:

```
Action: [ActionName]
- Input parameters: What does this action operate on?
- Preconditions (given): What must be true? Use predicates from Knowledge.
- Postconditions (makes):
  * What NEW facts become true?
  * What OLD facts become false? (prefix with NOT)
- Which mechanism will execute this? (use: ActionNameMechanism)
```

Output Goals array and confirm with user.

**Common precondition patterns:**
- Possession: `Holds(agent, item)` / `NOT Holds(agent, item)`
- Location: `At(object, location)` / `NOT At(object, location)`
- State: `IsReady(resource)` / `IsLocked(resource)` / `IsEmpty(container)`
- Availability: `HandIsEmpty()` / `SlotAvailable(slot)`

## Phase 4: Build Mechanisms Layer

For each Goal, construct the corresponding Mechanism.

The Mechanism is the procedural "how" — it mirrors the Goal but adds:
- `type`: always `"operation"` for atomic actions
- `requires`: formal version of `given` (same predicates)
- `provides`: plain English outcomes (more readable than `makes`)
- `process`: explicit state delta — WHAT IS REMOVED and WHAT IS ADDED

```
Mechanism for: [ActionName]
- requires: [same as goal's given]
- provides: [plain English outcomes]
- process: "Remove [old facts], add [new facts], update [other state changes]"
```

**process field template:**
`"Remove [Predicate(params)], add [NewPredicate(params)], [update X state]"`

## Phase 5: Validate Structure

Run this checklist before finalizing:

### Completeness
- [ ] Every Goal has exactly one Mechanism (check name match: `Goal.mechanism == Mechanism.name`)
- [ ] Every predicate in `given`/`makes`/`requires` is defined in Knowledge
- [ ] All parameter names are consistent (same name = same thing everywhere)

### Correctness
- [ ] Every action that changes a relationship has `NOT OldRelation(...)` in `makes`
- [ ] Preconditions are sufficient (would a planner accept this action with only these conditions?)
- [ ] Postconditions are complete (does anything else change that isn't listed?)

### Coverage
- [ ] Are there any actions the user might need that aren't covered?
- [ ] Are there any states the domain can be in that aren't representable?

## Phase 6: Output

Provide the user:

1. **Complete TMK JSON** — the full structure, formatted and ready
2. **Usage instructions** — how to use it:

```
To use this TMK structure:

1. Copy the JSON below
2. Prepend this system prompt:
   "You must adhere strictly to the JSON below, paying attention to the rules,
    ensuring to use only legal moves to achieve the final plan."
3. Add your specific planning problem in this format:

[STATEMENT]
As initial conditions I have that, [describe your starting state].
My goal is to have that [describe your goal state].

My plan is as follows:

[PLAN]
```

3. **Extension notes** — if the domain needs deeper decomposition, note which Goals could be further broken down

## Iterative Refinement

If the user wants to improve the TMK after testing:

**Undertriggering (LLM ignores structure):**
- Add more explicit `CRITICAL:` annotations in the system prompt
- Make preconditions more specific

**Wrong plans (LLM violates preconditions):**
- Check that `given`/`requires` are complete — missing a precondition allows illegal moves
- Add a `verifyPlan` meta-goal that checks plan validity

**Incomplete plans (LLM stops early):**
- Verify all goal states are explicitly represented in postconditions
- Add a `checkGoalAchieved` goal with the target state as its `given`
