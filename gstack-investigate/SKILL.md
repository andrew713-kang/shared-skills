---
name: gstack-investigate
description: |
  5-phase systematic debugging framework. Enforces root cause investigation before any fix.
  Ported from gstack by Garry Tan.

  Use when debugging complex bugs, intermittent failures, or mysterious behavior.

  Triggers: investigate, debug, root cause, 디버깅, 근본 원인, 버그 추적, 調査, デバッグ, 调查, 调试,
  investigar, depurar, causa raíz, enquêter, déboguer, untersuchen, debuggen, indagare, debug

  Do NOT use for: simple typo fixes, known issues with clear solutions, or feature implementation.
---

# Systematic Investigation Framework

> **Iron Law**: No fixes without investigation first. Understand before you change.

## When to Use

- Bug with unclear root cause
- Intermittent or hard-to-reproduce failures
- Regression after seemingly unrelated change
- "It works on my machine" scenarios
- Performance degradation without obvious cause

## Phase 1: Symptom Collection (NO CODE CHANGES)

**Goal**: Gather all observable evidence before forming any hypothesis.

1. **Reproduce**: Attempt to reproduce the issue. Document exact steps.
2. **Read logs**: Check all relevant log outputs, error messages, stack traces.
3. **Trace code path**: Follow the execution flow from entry point to failure.
4. **Check history**: `git log --oneline -20` and `git log --all --oneline -- <affected-files>` to find recent changes.
5. **Environment diff**: Compare working vs broken environments if applicable.

**Output**: Structured symptom report:

```
Symptom: [What happens]
Expected: [What should happen]
Frequency: [Always / Intermittent / Under specific conditions]
First observed: [When]
Recent changes: [What changed around that time]
```

**Rule**: Do NOT modify any code during this phase. Read-only investigation.

## Phase 2: Pattern Analysis

**Goal**: Identify which category of bug this is.

Common patterns to check:

- **Race condition**: Timing-dependent behavior, works sometimes
- **Null propagation**: Undefined/null passed through multiple layers
- **State corruption**: Shared mutable state modified unexpectedly
- **Resource leak**: Memory, connections, file handles not released
- **Type mismatch**: Wrong type passes silently (especially in JS/TS)
- **Dependency version**: Package update broke implicit contract
- **Environment**: Missing env vars, wrong config, path issues
- **Off-by-one / boundary**: Edge cases at limits

**Output**: Pattern hypothesis (max 3 candidates ranked by likelihood)

## Phase 3: Hypothesis Testing (3-Strike Rule)

**Goal**: Validate or eliminate each hypothesis with evidence.

For each hypothesis:

1. **Predict**: "If this hypothesis is correct, then X should be true"
2. **Test**: Write a minimal test or add logging to verify prediction
3. **Evaluate**: Does evidence support or contradict?

**3-Strike Escalation**:

- Strike 1: First hypothesis fails → try next candidate
- Strike 2: Second hypothesis fails → try last candidate
- Strike 3: All hypotheses fail → **STOP and ask the user for guidance**

Use AskUserQuestion after 3 failed hypotheses:

- "3가지 가설이 모두 반증되었습니다. 추가 컨텍스트가 있으신가요?"
- Present findings so far
- Suggest next investigation directions

## Phase 4: Minimal Fix

**Goal**: Apply the smallest possible fix targeting root cause.

**Scope Lock**: After identifying root cause, restrict edits to the affected module only.

**Blast Radius Check**: If fix requires changes to more than 5 files:

- STOP and use AskUserQuestion to confirm with user
- Explain why the fix is wider than expected
- Propose a phased approach if possible

**Fix Principles**:

- Fix the root cause, not the symptom
- Prefer the smallest change that solves the problem
- Do not refactor surrounding code
- Do not add "while I'm here" improvements
- One logical change per edit

## Phase 5: Verification & Report

**Goal**: Confirm the fix works and document findings.

1. **Verify**: Reproduce the original steps — confirm bug is resolved
2. **Regression check**: Verify nothing else broke
3. **Document**: Generate structured debug report

**Debug Report Format**:

```
## Investigation Report

### Symptom
[What was observed]

### Root Cause
[What was actually wrong and why]

### Fix Applied
[What was changed and why this is the correct fix]

### Evidence
[Logs, traces, or tests that confirm the fix]

### Prevention
[How to prevent similar issues: better types, validation, tests, etc.]
```

## Safety Rules

| Rule           | Description                             |
| -------------- | --------------------------------------- |
| No blind fixes | Never change code hoping it might help  |
| Evidence first | Every fix must have supporting evidence |
| Scope lock     | Stay within the affected module         |
| Blast radius   | >5 files = user confirmation required   |
| 3-strike       | 3 failed hypotheses = ask for help      |
| No side quests | Don't improve unrelated code            |
