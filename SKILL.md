---
name: surgical-development
description: Use for clearly scoped code or configuration changes, focused bug fixes, implementation summaries, or complex flow/configuration explanations. Prefer the smallest complete change, proportionate verification, concise diagrams, and immediate stopping. Do not use its fixed small-change workflow for open-ended architecture, broad exploration, or requirements that still need business clarification.
metadata:
  version: "1.0.0"
---

# Surgical development

Complete the requested change without expanding it. Optimize for the shortest reliable path from the stated target to verified behavior, not for the largest possible investigation.

## Scope

Use this skill when:

- The target file, configuration, method, behavior, or acceptance result is already identified.
- The task is a small code change, configuration adjustment, boolean/value change, narrow bug fix, or focused refactor explicitly requested by the user.
- A completed code change needs a concise implementation summary.
- The task is to explain a complex business flow, state transition, cross-system interaction, data-consistency concern, or configuration/cache propagation.

Do not apply the fixed workflow below to open-ended design, broad investigation, complex cross-system diagnosis, or work whose business meaning is still unclear. Use a normal investigation/design process there.

## Before editing

1. Identify the narrowest layer that owns the incorrect or requested behavior. Prefer the responsible shared implementation over a caller-side workaround.
2. Read only the relevant code path, callers, configuration, and existing analogous implementation. Batch independent read-only checks when they are all needed.
3. Reuse an existing project helper, component, service, pattern, or platform capability before introducing new code.
4. Follow the surrounding module's existing architecture and style.
5. Define the smallest sufficient completion proof before editing. Use the strongest evidence already available; reproduce a failure first only when the cause is uncertain and reproduction is cheaper than broader inspection.

State assumptions only when they materially affect behavior. If a remaining ambiguity can change business meaning, database structure, interface contract, historical data, permission scope, or cross-module behavior, stop and ask for a decision instead of silently choosing.

## Choose the smallest complete implementation

Take the first option that fully solves the requested behavior:

1. No code change, such as an existing setting or configuration value.
2. An existing project helper, component, service, or pattern.
3. A standard-library or platform capability already compatible with project conventions.
4. An already installed dependency.
5. The smallest direct patch that completely implements the request.

Do not add:

- Features, options, flags, abstractions, wrappers, adapters, or flexibility not requested.
- New dependencies, tests, project configuration, build scripts, or engineering structure unless explicitly requested.
- Unrelated cleanup, renaming, formatting, refactoring, or comment normalization.
- Unrequested fallback, degradation, compatibility, backup implementation, default value, silent error handling, or automatic recovery behavior.

Never omit validation at trust boundaries, data-loss prevention, security handling, accessibility, concurrency protection, or behavior the user explicitly requested. A smaller change is not complete if it silently moves the risk elsewhere.

## Editing rules

- Every changed line should trace directly to the request.
- Match the existing language, structure, naming, and test/build conventions of the surrounding code.
- Preserve unrelated changes and user modifications.
- For bug fixes, fix the root cause once at the owning layer; do not duplicate the same guard across callers unless the caller-specific context genuinely requires it.
- Keep comments in Chinese and consistent with the code. Explain important rules and non-obvious reasons with accurate domain terms; distinguish business behavior from display, response, and export formatting.
- If a deliberate shortcut has a known limit, note the limit and upgrade condition in one concise comment only when that limitation is not obvious from the code.

Git operations that alter history or remote state require explicit user authorization. Unless the user explicitly asks, do not commit, merge, push, create tags, or create merge requests; leave worktree changes for review.

## Execution and stopping

- Once the target and constraints are known, edit directly. Avoid re-planning after every partial read.
- Run verification proportionate to risk:
  - Literal or configuration-only change: inspect the diff and run a syntax or loading check when needed.
  - Local code change: run the focused test, compile, lint, or nearest affected check.
  - Risky branch, data, security, concurrency, or contract-adjacent logic: use an existing targeted regression proof. Creating or changing tests requires explicit user authorization.
- Do not run full repository scans, broad test suites, builds, database queries, or cross-repository investigations merely because they might help. They must be required by project rules, requested by the user, or justified by a concrete risk.
- Reuse a still-current verification result only when the repository state and relevant inputs have not changed.
- If a command or tool fails, read the error and correct the invocation once. If the same failure continues, stop that path and report the exact blocker.
- If an out-of-scope dependency, environment, or business issue appears, report its impact and continue only with the part of the original task that remains independently completable.
- Stop as soon as the acceptance proof is complete. Do not add polish, extra checks, or unrelated tests after passing.

## Completion report

Scale the report to the change. For small edits, briefly state:

- Changed files/modules and relevant entry point or method.
- What changed and the key condition or parameter.
- How the new behavior differs from the old behavior.
- Verification performed and its result.
- Remaining risk, skipped work, or unverified compatibility point, if any.

For substantial work, add a concise main flow using `来源 → 处理 → 状态 → 结果`, and mention database, cache, queue, timer, third-party system, and deployment responsibilities when they participate. Include a separate change-propagation flow only when configuration, state, or data propagation is material. Explain only relevant exceptions and concurrency behavior.

When the user asks primarily for a complex flow, state, data-consistency, or configuration/cache explanation, read [references/flow-output.md](references/flow-output.md) and apply that reference instead of improvising a diagram structure.
