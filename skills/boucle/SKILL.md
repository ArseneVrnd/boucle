---
name: boucle
description: Use when completing a phase of a multi-step plan, before clearing context, when resuming after a break, or when handing off between sessions
---

# Boucle (Context Loop Checkpoint)

Use this skill between phases of a multi-phase implementation plan. It creates a concise context snapshot that survives context clearing, and ensures all project documentation stays in sync.

## When to Use

- After completing a phase of a multi-step plan
- Before clearing context to free up space
- When resuming work after a break
- When handing off between sessions

## Process

### Step 1: Read the implementation plan

Read the plan file (check `docs/plans/` for the most recent plan). Identify all phases and their status.

### Step 2: Check git log for completed work

```bash
git log --oneline -20
```

Cross-reference commits with plan tasks to determine what's done.

### Step 3: Check for issues

```bash
cd apps/web && npx tsc --noEmit 2>&1 | tail -10
```

Note any build errors or failing tests that need addressing.

### Step 4: Update MEMORY.md

Read the project auto-memory file (`MEMORY.md` in the memory directory). Update it with:

- **New tips/lessons** discovered this session (patterns that broke, things that worked)
- **Status changes** (e.g. blog went from "pending" to "3 articles live")
- **New infrastructure** added (new tools, plugins, services installed)
- Remove or correct any entries that are now outdated

Keep it concise — MEMORY.md is loaded into every conversation.

### Step 5: Update CLAUDE.md

Read the project `CLAUDE.md`. Update:

- **Learned Mistakes table** — add any new mistakes discovered this session with date, description, and rule. Format: `| YYYY-MM-DD | What went wrong | Rule to prevent it |`
- **Relevant sections** that changed (e.g. Design System, Blog entry, Architecture) — keep them accurate
- **Gotchas & Tips** — add any new gotchas discovered

Do NOT rewrite sections that haven't changed. Only touch what's stale.

### Step 6: Write the checkpoint summary

Write a concise checkpoint to your memory file at the project memory directory as `boucle-checkpoint.md` with this exact format:

```markdown
# Boucle Checkpoint — [Date]

## Plan
- **Plan file:** docs/plans/[filename].md
- **Total phases:** N
- **Current phase:** N (name)

## Completed
- Phase 1: [name] — [1-line summary of what was done]
- Phase 2: [name] — [1-line summary]
- ...

## Current State
- **Build status:** passing/failing (details if failing)
- **Test status:** passing/failing
- **Git branch:** [branch]
- **Last commit:** [hash] [message]
- **Files created/modified this session:** [count]

## Next Up
- Phase N: [name] — [1-line description of what needs to happen]
- **Key files to touch:** [list]
- **Dependencies/blockers:** [any]
- **Parallel opportunities:** [which tasks can run simultaneously]

## Context for Next Agent
[2-3 sentences explaining the project state so a fresh agent can pick up without reading the full plan]
```

### Step 7: Announce readiness

Tell the user:
- What phase just completed
- What's next
- Whether context can be safely cleared
- Any issues that need attention before continuing
- What was updated in MEMORY.md and CLAUDE.md
