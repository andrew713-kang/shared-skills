---
name: gstack-codex
description: |
  Multi-AI code review using OpenAI for independent cross-verification.
  Ported from gstack by Garry Tan. Requires OPENAI_API_KEY.

  Triggers: codex review, multi-AI review, cross-verify, second opinion, 멀티AI 리뷰, 크로스 검증,
  マルチAIレビュー, クロス検証, 多AI审查, 交叉验证,
  revisión multi-AI, verificación cruzada, revue multi-IA, vérification croisée,
  Multi-AI-Review, Kreuzverifizierung, revisione multi-AI, verifica incrociata

  Do NOT use for: simple code questions, when OPENAI_API_KEY is not available.
---

# Multi-AI Code Review (Codex)

> Independent code review from a different AI model for cross-verification.
> Requires: `OPENAI_API_KEY` environment variable.

## Three Modes

### 1. Review Mode (`/gstack-codex review`)

Independent diff analysis against base branch.

**Process**:

1. Get diff: `git diff main...HEAD`
2. Send to OpenAI API with review prompt
3. Parse response for priority markers:
   - **P1** (Critical): Security, data loss, crash → **FAIL**
   - **P2** (Important): Performance, logic errors → **PASS with notes**
   - **Clean**: No issues found → **PASS**
4. Report verdict with reasoning

### 2. Challenge Mode (`/gstack-codex challenge`)

Adversarial testing — try to break the code.

**Process**:

1. Send code with adversarial prompt
2. Ask for: failure modes, race conditions, security holes, edge cases
3. Report each finding with severity
4. Cross-reference with Claude's own analysis

### 3. Consult Mode (`/gstack-codex {question}`)

General technical consultation for a second opinion.

**Process**:

1. Send question with relevant code context
2. Get independent analysis
3. Compare with Claude's perspective
4. Present both viewpoints

## API Integration

```bash
# Review mode example
DIFF=$(git diff main...HEAD)
curl -s https://api.openai.com/v1/chat/completions \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d "{
    \"model\": \"gpt-4o\",
    \"messages\": [
      {\"role\": \"system\", \"content\": \"You are a senior code reviewer. Analyze this diff for bugs, security issues, and quality problems. Mark critical issues as P1, important as P2.\"},
      {\"role\": \"user\", \"content\": $(echo "$DIFF" | jq -Rs .)}
    ],
    \"temperature\": 0.1
  }"
```

## Prerequisites

1. `OPENAI_API_KEY` must be set in environment or `secrets/global.env`
2. To check: `test -n "$OPENAI_API_KEY" && echo "OK" || echo "Missing"`
3. If missing, inform user and skip

## Output Format

```markdown
## Multi-AI Review Report

### Verdict: PASS / FAIL

**Model**: gpt-4o
**Files reviewed**: {count}

### Findings

| #   | Priority | File    | Issue              | Claude Agrees? |
| --- | -------- | ------- | ------------------ | -------------- |
| 1   | P1       | auth.ts | Missing CSRF check | Yes            |
| 2   | P2       | api.ts  | N+1 query          | Already fixed  |

### Cross-Model Comparison

- **Agreed**: [Issues both models flagged]
- **OpenAI only**: [Issues Claude missed]
- **Claude only**: [Issues OpenAI missed]
- **Conflicting**: [Different opinions — needs human decision]
```

## Integration with bkit

- Use during PDCA Check phase alongside `gap-detector`
- Provides independent verification from a different AI perspective
- Cross-model comparison increases confidence in code quality
- Pairs with `/security-review` for comprehensive security analysis
