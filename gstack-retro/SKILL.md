---
name: gstack-retro
description: |
  Engineering retrospective with quantitative metrics from git history.
  Ported from gstack by Garry Tan.

  Use after completing a sprint, PDCA cycle, or at regular intervals for team health analysis.

  Triggers: retro, retrospective, 회고, 스프린트 리뷰, 메트릭, 振り返り, レトロ, 回顾, 复盘,
  retrospectiva, revisión de sprint, rétrospective, revue de sprint,
  Retrospektive, Sprint-Review, retrospettiva, revisione sprint

  Do NOT use for: code review, debugging, or feature planning.
---

# Engineering Retrospective

> Quantitative analysis of development activity from git history.

## Arguments

| Argument  | Description                      | Example                 |
| --------- | -------------------------------- | ----------------------- |
| (none)    | Standard retro (last 7 days)     | `/gstack-retro`         |
| `{days}`  | Custom time window               | `/gstack-retro 14`      |
| `compare` | Compare two equal-length windows | `/gstack-retro compare` |

## Data Collection

Run these git commands to gather metrics:

```bash
# Commits in time window
git log --since="{start}" --until="{end}" --oneline --all

# Per-author breakdown
git shortlog --since="{start}" --until="{end}" -sne --all

# Files changed
git log --since="{start}" --until="{end}" --stat --all

# LOC changes
git log --since="{start}" --until="{end}" --numstat --all

# Conventional commit breakdown
git log --since="{start}" --until="{end}" --oneline --all | grep -cE "^[a-f0-9]+ (feat|fix|refactor|test|chore|docs|style|perf)(\(.*\))?:"
```

## Metrics to Compute

### Shipping Velocity

- Total commits
- Total PRs (if available via `gh pr list`)
- LOC added / removed / net
- Files touched

### Test Health

- Test file count: `find . -name "*.test.*" -o -name "*.spec.*" | wc -l`
- Test-to-code ratio: test files / total code files
- Test LOC changes vs production LOC changes

### Focus Score

- Primary directory: which directory had the most commits?
- Concentration: % of commits in top 3 directories
- Scatter score: how spread out was the work?

### Session Patterns

- Work sessions: group commits with >45min gap as session boundaries
- Deep work sessions: sessions with 3+ commits
- Micro sessions: sessions with 1 commit
- Active hours: histogram of commit times (hourly buckets)

### Hotspot Analysis

- Most frequently changed files (top 10)
- Files changed by multiple authors (collaboration points)
- Files with both feature and fix commits (potential quality issues)

### Shipping Streak

- Consecutive days with at least 1 commit
- Current streak vs best streak in window

## Output Format

```markdown
## Engineering Retrospective

**Period**: {start} — {end} ({days} days)

### Summary

| Metric          | Value                 | Trend         |
| --------------- | --------------------- | ------------- |
| Commits         | {n}                   | {vs previous} |
| LOC net         | +{added} / -{removed} |               |
| Test ratio      | {n}%                  |               |
| Focus score     | {n}%                  |               |
| Shipping streak | {n} days              |               |

### Activity Pattern

[Hourly histogram of commit times]

### Top Changed Files

1. `path/to/file.ts` — {n} commits
2. ...

### Hotspots (Potential Quality Risk)

Files with both `feat` and `fix` commits in the same period:

- `path/to/file.ts` — {feat_count} features, {fix_count} fixes

### Highlights

- [Notable achievements]
- [Patterns worth discussing]

### Growth Opportunities

- [Areas for improvement]
- [Process suggestions]
```

## Compare Mode

When using `compare`, analyze two equal windows and show deltas:

```
Period A: {date} — {date}
Period B: {date} — {date}

| Metric | Period A | Period B | Delta |
|--------|---------|---------|-------|
| Commits | 45 | 62 | +38% |
| ...
```

## Integration with bkit

- Run after `/pdca report {feature}` for quantitative supplement
- Use metrics to validate PDCA cycle efficiency
- Compare pre/post PDCA adoption metrics
