---
name: run-work-items
description: Activate when users ask to execute queued work. Selects next actionable item from the configured backend, runs implementation with process quality gates, and continuously updates item state until completion.
version: 10.2.14
author: "Karsten Samaschke"
contact-email: "karsten@vanillacore.net"
website: "https://vanillacore.net"
---

# Run Work Items

Execute the next actionable work item and maintain continuous state tracking.

## When To Use

- User asks to run/execute work items
- Backlog has actionable items and execution should continue
- Autonomy loop needs next-step dispatch

## Execution Workflow

1. Load prioritized plan from active backend.
2. Select next actionable unblocked item.
3. Execute with `process` quality gates (`tdd`, test loop, review loop).
4. Update state continuously (`in_progress`, `blocked`, `completed`).
5. On completion, re-evaluate next actionable item.

## Backend State Updates

- GitHub backend: update labels/state/closure on issue.
- File-based backend: rename `.agent/queue/` status prefix.

## Continuation Rules

- If actionable items remain, continue automatically per autonomy level.
- If only blocked items remain, report blockers and stop.
- If no items remain, report completion.

## Output

Return:
- item executed
- result/status change
- test/review gate summary
- next action (continue/blocked/done)
