---
name: "implementation"
description: "Implement only explicitly approved feature task IDs after validating the merged specification, plan, tasks, and repository guidance."
compatibility: "Requires a repository feature directory containing spec.md, plan.md, and tasks.md."
metadata:
  author: "mostafamos/cobol-buggy-sample"
---

# Implementation Skill

Use this skill to implement an approved feature task list. A task appearing in
`tasks.md`, being unchecked, or being described as necessary is not approval.

## Required Inputs

Before editing files or running implementation commands, establish:

- The exact feature directory and its `spec.md`, `plan.md`, and `tasks.md`.
- The GitHub issue and linked Azure DevOps work item, when applicable.
- The exact task IDs the user authorized, as recorded on the GitHub issue.
- The approval's applicable artifact revision or commit and any explicitly
  authorized rework.

If the approved artifact revision cannot be matched to the current default
branch, the task IDs are missing or ambiguous, or authorization does not cover
the current artifacts, stop and ask for current approval. Do not infer
authorization from a prior session message or a task checklist.

## Pre-Implementation Review

Read the approved spec, plan, and tasks in full, plus `.specify/memory/constitution.md`,
applicable repository guidance, referenced artifacts, and any applicable NFRs.
Review relevant source and tests. Before changing files, summarize:

- Approved task IDs and their dependency order.
- Applicable principles and NFRs, or explicitly note unresolved/missing guidance.
- Acceptance criteria that each task addresses.
- Planned verification commands and any known tool limitations.

Treat missing artifacts, unresolved required policy placeholders, conflicting
requirements, missing or ambiguous NFR criteria, stale approval, or incomplete
unapproved dependencies as blockers. Ask the user rather than inventing
requirements, policy, thresholds, expected results, or approvals.

## Implementation Rules

- Follow task phases and dependencies in order.
- Implement only the exact approved task IDs. Skip tasks already marked
  complete unless explicit rework authorization covers them.
- If a required dependency is incomplete and not approved, stop. Continue other
  approved work only if the task plan explicitly permits it independently.
- Keep changes focused on authorized tasks, including necessary tests and
  directly related documentation. Do not perform unrelated refactoring or add
  dependencies/configuration without authorization.
- Do not rewrite the spec, plan, constitution, or NFRs to make an implementation
  pass. If those artifacts need to change, stop and request revised artifacts
  and approval.
- Do not create or modify skills as part of feature implementation.

## Verification and Task Status

Run applicable repository tests, lint, builds, and NFR checks. Report exact
commands and actual outcomes. Never claim an unavailable or unrun check passed.

If a task or required check fails, leave it incomplete and stop dependent work.
If a required compiler, runtime, or test harness is unavailable, state the
specific limitation; do not substitute an unrelated calculation or source
inspection for execution of the target program.

Mark a task complete in `tasks.md` only when that authorized task has been
implemented and its required verification has succeeded. Preserve task IDs,
descriptions, dependencies, and unrelated entries. Leave unverified, blocked,
failed, skipped, and unauthorized tasks unchecked.

## Pull Request and Handoff

Open an implementation pull request linked to the GitHub issue and Azure DevOps
work item. Describe the authorized task IDs, changed files, acceptance-criteria
traceability, exact validation commands and results, and any remaining risks
or gaps. Do not merge, enable auto-merge, or claim release or deployment.

Stop after opening the pull request and report completed, incomplete, blocked,
and skipped tasks with the exact evidence for each.
