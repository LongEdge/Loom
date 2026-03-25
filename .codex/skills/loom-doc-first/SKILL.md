---
name: loom-doc-first
description: Enforce Loom's documentation-first workflow for any task that changes code, config, interfaces, architecture, data flow, or runtime behavior. Use when working in the Loom repo to resolve repo root dynamically, detect current version from README (README-first), and require synchronized updates under DOCUMENTS/<version>/ before completion for core changes.
---

# Loom Documentation-First Guardrail

Apply this workflow before finishing any Loom task that may change project behavior or semantics.

## Workflow

### 1) Resolve repository root dynamically (no hardcoded paths)

Resolve `repo_root` in this exact order:

1. Run `git rev-parse --show-toplevel`.
2. If that fails, walk upward from current working directory until finding a directory that contains both:
   - `README.md`
   - `DOCUMENTS/`
3. If still unresolved, stop and report: cannot determine repository root.

Derived paths:

- `docs_root = <repo_root>/DOCUMENTS`
- `readme_path = <repo_root>/README.md`

### 2) Detect current version from README (README-first)

Parse `README.md` status/version text. Prefer explicit status lines like:

- `Early development (v0.1)`
- any `(...vX.Y...)` pattern

If no parseable version exists, stop and report: current version cannot be determined from README.

Set:

- `current_version = parsed value` (for example `v0.1`)
- `target_docs_dir = <repo_root>/DOCUMENTS/<current_version>`

If `target_docs_dir` does not exist, stop and report: missing versioned docs directory.

### 3) Classify change level

Classify the requested or implemented change before completion.

Core changes (mandatory docs update):

- Interface or CLI behavior change
- Architecture or module responsibility change
- Data flow or protocol change
- Config semantic or default behavior change
- Runtime behavior change visible to users/operators

Minor changes (reminder only):

- Comment-only updates
- Typo or wording fixes
- Formatting or layout-only edits
- Non-semantic refactor with no behavior change

When uncertain, treat as core.

### 4) Enforce documentation sync

For core changes:

- Require at least one updated file under `target_docs_dir`.
- Ensure docs include:
  - what changed
  - impact scope
  - code/command/config touchpoints
- If docs are not updated, block completion and request doc sync first.

For minor changes:

- Allow completion without doc edits.
- Explicitly state that change is minor and did not trigger mandatory documentation sync.

### 5) Use completion checklist

Before final response, confirm all applicable checks:

- `repo_root` resolved dynamically
- `current_version` parsed from README
- `target_docs_dir` resolved and exists
- core change: documentation updated in versioned docs path
- response includes `doc path + summary + impact points` when docs changed

## Output Contract

When this skill is active, report these fields in the final summary:

1. `Version`: detected version from README
2. `Docs Directory`: resolved versioned docs path
3. `Change Level`: `core` or `minor` with one-line rationale
4. `Doc Sync`: done/blocked/waived (with reason)

If blocked, do not present the task as completed.
