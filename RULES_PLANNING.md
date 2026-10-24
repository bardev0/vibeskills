# Planning rules

## Rule 1: Small, ordered tasks with test gates

Every plan created by an agent must consist of small code or DevOps tasks in a clear, numbered execution order.

Each task must include a test gate: a specific verification step with clear pass criteria. A task may be marked complete only after its test gate passes.

## Rule 2: Track completion and version

Each task must have one of these statuses:

- `not started`
- `complete` — include the specific project version in which the task was completed, using `MAJOR.MINOR.PATCH` format.

## Rule 3: Preserve the original plan

Never delete the original plan file or text, or remove, rewrite, or reorder its original tasks and test gates. When updating progress, change only the task's completion status and record its completion version.
