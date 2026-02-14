---
name: plan-work-items
description: Activate when users ask to plan, prioritize, or structure existing work items. Orders backlog by priority and dependencies, validates parent-child hierarchy, and prepares run-ready next actions.
version: 10.2.14
author: "Karsten Samaschke"
contact-email: "karsten@vanillacore.net"
website: "https://vanillacore.net"
---

# Plan Work Items

Prioritize and structure work items so execution can proceed deterministically.

## When To Use

- User asks to prioritize or sequence work
- Parent/child hierarchy must be validated
- Dependencies/blockers need explicit management

## Planning Workflow

1. Load current backlog from active backend.
2. Normalize item types and priorities.
3. Build dependency graph (blocks/blocked-by).
4. Identify actionable next set (unblocked, highest priority).
5. Publish planning result back to backend.

## Parent/Child Rule (GitHub)

- `Parent: #123` in issue body is trace-only.
- Native GitHub parent-child relationship must exist for hierarchy to be valid.
- Verify native relationship before marking planning complete.

## Planning Output

Return:
- prioritized order
- blocked vs actionable items
- dependency risks
- hierarchy verification status
- recommended next item(s) for `run-work-items`
