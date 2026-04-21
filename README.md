# shared-skills

CC(Claude Code) + AG(AntiGravity/Gemini) + Codex 공용 스킬 레포.

## 구조

각 스킬은 `{skill-name}/SKILL.md` 폴더 구조로 관리됩니다.

```
shared-skills/
├── government-funding/SKILL.md   ← AG 기원
├── gstack-investigate/SKILL.md   ← CC 기원
├── pdca/SKILL.md                 ← CC 기원
└── ...                           (총 63개)
```

## 사용 환경

| 환경             | 연결 방식                                  |
| ---------------- | ------------------------------------------ |
| Claude Code (CC) | `~/.claude/skills/` → Junction             |
| AntiGravity (AG) | `~/.gemini/antigravity/skills/` → Junction |
| Codex            | `oh-my-opencode.json` sources              |

## 동기화

- `warp-start-v2.ps1` — 세션 시작 시 `git pull`
- `clean-sync-v2.ps1` — 세션 종료 시 `git push`
