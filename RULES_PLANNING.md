# Planning rules

## Rule 1: Small, ordered tasks with test gates

Every plan created by an agent must consist of small code or DevOps tasks in a clear, numbered execution order.

Each task must include a test gate: a specific verification step with clear pass criteria. A task may be marked `GREEN` only after its test gate passes.

## Rule 2: Track completion and version

Each task must have exactly one of these statuses, saved in the plan file:

- `PENDING` — work has not started.
- `RUNNING` — work or verification is in progress.
- `GREEN` — work is complete and its test gate has passed. Include the specific project version in which the task was completed, using `MAJOR.MINOR.PATCH` format.
- `RED` — work or its test gate failed, including an unexpected error. Record the failure and the next recovery step.
- `BLOCKED` — work cannot proceed because of a missing prerequisite, unavailable dependency, required input, or unresolved interruption. Record the blocker and what is needed to resume.

Initialize every task as `PENDING`. Immediately before starting or resuming a task, persist `RUNNING` and a start timestamp in the plan file, before performing any task actions. If the status cannot be saved, do not start the task.

Persist each outcome as soon as it is known, with an updated timestamp and relevant progress or recovery notes. Use `GREEN` only after verification passes; skipped or unrun verification does not qualify. On a handled failure or unexpected error, save `RED`. If a prerequisite prevents further work, save `BLOCKED`. Before a controlled session stop, save unfinished `RUNNING` tasks as `BLOCKED` with a checkpoint describing completed work and remaining actions.

A crash or abrupt session termination may prevent a final status update. Leave the persisted `RUNNING` status as evidence of unfinished work; never infer completion from it. On resuming a plan, inspect every task left `RUNNING`, reconcile its recorded progress with actual work and verification results, and save the appropriate status before continuing. If the state cannot be established, mark it `BLOCKED` and explain what must be checked. Persist `RUNNING` again before retrying or resuming work from `RED` or `BLOCKED`.

## Rule 3: Preserve the original plan

Never delete the original plan file or text, or remove, rewrite, or reorder its original tasks and test gates. When updating progress, change only task tracking metadata: status, timestamps, progress or recovery notes, and completion version. Preserve prior failure and interruption notes when recording a retry or recovery.
