---
name: gstack-qa
description: |
  Real browser QA testing with Playwright. Finds and fixes UI bugs systematically.
  Ported from gstack by Garry Tan. Requires /gstack-browse daemon running.

  Triggers: qa test, browser test, UI test, visual test, QA, 브라우저 테스트, UI 테스트,
  ブラウザテスト, UIテスト, 浏览器测试, UI测试,
  prueba de navegador, test de navigateur, Browser-Test, test del browser

  Do NOT use for: unit tests, API-only testing, or projects without a UI.
---

# Browser QA Testing

> Real Chromium browser testing with systematic bug detection and atomic fixes.
> Prerequisite: `/gstack-browse` daemon must be running.

## Modes

| Mode           | Description                               | When to Use                 |
| -------------- | ----------------------------------------- | --------------------------- |
| **Diff-aware** | Test pages affected by recent git changes | Default on feature branches |
| **Full**       | Test all pages comprehensively            | Before release              |
| **Quick**      | Critical + high severity only             | Fast feedback loop          |

## 11-Phase Workflow

### Phase 1: Setup

- Verify `/gstack-browse` daemon is running (check `/tmp/.gstack-browse.json`)
- If not running, start it: `/gstack-browse`
- Verify clean git working tree (offer to commit/stash if dirty)

### Phase 2: Scope Detection

- **Diff-aware**: `git diff --name-only main...HEAD` to find affected files
- Map changed files to affected pages/routes
- **Full**: Enumerate all routes from router config or sitemap

### Phase 3: Test Plan

- List pages to test with priority order
- Identify critical user flows (auth, checkout, forms)
- Note any authenticated routes requiring login

### Phase 4-6: Baseline QA

For each page:

1. Navigate: `goto {url}`
2. Screenshot: `screenshot {path}`
3. Check: visual layout, text content, interactive elements
4. Test: click buttons, fill forms, verify navigation
5. Record findings with severity

### Phase 7: Triage

Sort findings by severity:

- **Critical**: App crashes, data loss, security issues
- **High**: Broken functionality, major layout issues
- **Medium**: Minor visual issues, accessibility problems
- **Cosmetic**: Alignment, spacing, color inconsistencies

### Phase 8: Fix Loop

For each finding (highest severity first):

1. Locate the source file
2. Apply minimal fix
3. **Commit immediately** (one commit per fix)
4. Re-test the affected page
5. Verify fix, move to next

### Phase 9: Final QA

- Re-run affected pages
- Compute health score: (passing / total) \* 100

### Phase 10: Report

Generate structured report:

```markdown
## QA Report

**Date**: {date}
**Mode**: {mode}
**Pages tested**: {count}
**Issues found**: {count}
**Issues fixed**: {count}
**Health score**: {score}%

### Findings

| #   | Severity | Page   | Issue                 | Status |
| --- | -------- | ------ | --------------------- | ------ |
| 1   | Critical | /login | Form submit 500 error | Fixed  |
| ... |

### Screenshots

- Before: /tmp/qa-before-{page}.png
- After: /tmp/qa-after-{page}.png
```

### Phase 11: TODO Tracking

- Record deferred (unfixed) issues in project TODO or issue tracker

## Safety Rules

| Rule                 | Description                                  |
| -------------------- | -------------------------------------------- |
| Clean git first      | Must have clean working tree before starting |
| One commit per fix   | Never bundle multiple fixes                  |
| WTF risk limit       | Stop at 20% cumulative risk or 50 fixes max  |
| Verify every fix     | Re-test page after each fix                  |
| Revert on regression | Immediately revert if fix causes new issues  |

## Integration with bkit

- Use after `/pdca do {feature}` for UI verification
- Results feed into `/pdca analyze` gap analysis
- Complements bkit's Zero Script QA (log-based) with browser-based testing
