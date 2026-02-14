---
name: create-work-items
description: Activate when users ask to create or capture work items. Classifies and creates typed items (epic, story, feature, bug, finding, work-item), resolves missing fields with focused clarification, and publishes to the configured tracking backend.
version: 10.2.14
author: "Karsten Samaschke"
contact-email: "karsten@vanillacore.net"
website: "https://vanillacore.net"
---

# Create Work Items

Create typed work items and publish them to the active tracking backend.

## When To Use

- User asks to create tickets/issues/work items
- New work is discovered during implementation or review
- Requirements must be captured before planning/execution

## Item Types

Supported item types:
- `epic`
- `story`
- `feature`
- `bug`
- `finding`
- `work-item`

## Backend Selection

Use config-first backend routing from `work-queue`:
1. `.agent/tracking.config.json`
2. `${ICA_HOME}/tracking.config.json`
3. `$HOME/.codex/tracking.config.json` or `$HOME/.claude/tracking.config.json`
4. Auto-detect GitHub
5. Fallback to `.agent/queue/`

## Required Fields

Each created item should include:
- title
- type
- priority (`p0` to `p3` or local equivalent)
- description / acceptance notes
- optional parent

If fields are missing, ask focused clarification (short, bounded), then proceed.

## Creation Rules

- GitHub backend:
  - Use `github-issues-planning` conventions for labels/types/priorities.
  - If parent is requested, include `Parent: #<id>` in body for traceability.
  - Create native GitHub parent-child relationship separately and verify it.
- File-based backend:
  - Create `.agent/queue/NNN-pending-<slug>.md` with structured fields.

## Output

Return a concise creation summary:
- backend used
- items created (ids/urls or filenames)
- type/priority
- parent + native-link verification status (if applicable)
