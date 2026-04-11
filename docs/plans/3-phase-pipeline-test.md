# Plan: 3-Phase Pipeline Test

## Goal Summary

Implement a simple utility function in an otherwise empty repository. This is a
pipeline probe (`planner-3phase-ctx-probe-2025-v1`) designed to exercise the
three-phase plan-then-implement workflow against a trivially scoped goal.

## Approach

The repository has no language, framework, or tooling established. A minimal
TypeScript utility module will be created (a single file exporting a pure helper
function), along with a lightweight test using Node's built-in `node:assert`
module so no test runner installation is required.

Because `commit.gpgsign=true` is set globally (1Password SSH signing), every
commit in this environment must override signing with
`git config --local commit.gpgsign false` before committing, or use
`git -c commit.gpgsign=false commit ...` per invocation.

---

## Tasks

### Task 1: Implement the utility function

**Agent type:** coder

**Description:**
Create a `src/utils.ts` file that exports one well-named pure utility function
(e.g., `clamp(value, min, max)` — constrains a number to an inclusive range),
add a `tsconfig.json` enabling `moduleResolution: node`, and a minimal test
file `src/utils.test.ts` that exercises the function with `node:assert`. No
package manager or external dependencies are required.

**Subtasks (ordered):**
1. Create `src/utils.ts` with the exported `clamp` function (pure, typed).
2. Create `tsconfig.json` with `"module": "commonjs"`, `"target": "es2020"`,
   `"strict": true`, and `"outDir": "dist"`.
3. Create `src/utils.test.ts` using `import assert from 'node:assert'` and
   `import { clamp } from './utils'` with at least three assertions covering
   below-min, above-max, and within-range cases.
4. Verify the TypeScript compiles cleanly: `npx tsc --noEmit`.
5. Verify tests pass: `npx ts-node src/utils.test.ts` (or equivalent).
6. Disable commit signing locally:
   `git config --local commit.gpgsign false`
7. Stage all new files and commit with a descriptive message.
8. Push the feature branch and create a PR:
   ```
   gh pr create --fill --base dev
   ```

**Acceptance criteria:**
- `src/utils.ts` exists and exports at least one typed utility function.
- `src/utils.test.ts` exists and all assertions pass without error.
- `npx tsc --noEmit` exits with code 0 (no type errors).
- A GitHub PR is open targeting the `dev` branch.

**Dependencies:** none

**Note:** Changes must be on a feature branch with a GitHub PR created via
`gh pr create`.
