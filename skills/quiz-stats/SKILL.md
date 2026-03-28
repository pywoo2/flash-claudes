---
name: quiz-stats
description: Display your Flash Claudes quiz stats dashboard — levels, streaks, per-topic progress, weak spots, and achievements.
allowed-tools: Bash(date *), Bash(cat *), Bash(mkdir *)
---

# Flash Claudes — Stats Dashboard

Read the quiz state using Bash (not the Read tool) and display a comprehensive stats dashboard:
```
mkdir -p ~/.local/share/flash-claudes && cat ~/.local/share/flash-claudes/state.json 2>/dev/null || echo "NO_STATE"
```

If the state file doesn't exist, say:
```
No quiz data yet! Run /flash-claudes:quiz to get started.
```

## State Schema

```json
{
  "version": 1,
  "user": {
    "xp": 0,
    "level": 1,
    "currentStreak": 0,
    "longestStreak": 0,
    "lastActiveDate": null,
    "totalAnswered": 0,
    "totalCorrect": 0
  },
  "topics": {},
  "achievements": [],
  "sessionState": {
    "currentTopic": null,
    "questionNumber": 0,
    "correctThisSession": 0,
    "currentSessionStreak": 0,
    "xpEarnedThisSession": 0,
    "questionStyle": null
  }
}
```

**Topic entry schema** (created when user first plays a topic):
```json
{
  "displayName": "Rust",
  "difficultyScore": 0,
  "tier": "beginner",
  "totalAnswered": 0,
  "totalCorrect": 0,
  "recentResults": [],
  "subtopicAccuracy": {}
}
```

**`recentResults`** is a rolling array of the last 20 results (true/false) used for trend calculation.

**`subtopicAccuracy`** maps subtopic names to `{ "correct": N, "total": N }`.

**Achievement entry:**
```json
{
  "id": "first_question",
  "name": "First Steps",
  "unlockedAt": "2026-03-27T14:30:00Z"
}
```

## Dashboard Format

Display the following:

```
    ⚡ FLASH CLAUDES ⚡
    ╭─────────────────╮
    │  (◕‿◕) Stats!   │
    ╰─────────────────╯

{current trophy art}

Level {level} — {xp}/{xpToNext} XP
[{progressBar}] {pct}% to next level
Next trophy: Level {nextTrophyLevel} ({trophyName})

Streak: {currentStreak} days (best: {longestStreak})
Total: {totalCorrect}✓ / {totalAnswered} attempted

TOPICS
------------------------------------------------------
Topic           Tier          Correct   Attempted   Trend
--------------------------------------------------------------
{topic}         {tier}        {correct}✓   {answered}   {trend}
...
--------------------------------------------------------------

WEAK SPOTS
- {subtopic} in {topic}: {correct}✓ / {total} attempted
- {subtopic} in {topic}: {correct}✓ / {total} attempted
- {subtopic} in {topic}: {correct}✓ / {total} attempted

ACHIEVEMENTS ({unlocked}/{total})
{achieved} {name} — {description}
...
{locked} {name} — {description}
...
========================================
```

## Calculations

**XP to next level:**
- Level 2: 100 XP
- Level 3: 250 XP
- Level 4: 500 XP
- Level 5: 800 XP
- Level N (N >= 6): 800 + (N - 5) * 400 XP

**Progress bar:** 20-character bar using filled/empty blocks, e.g., `[============--------]`

**Weak spots:** Find the 3 subtopics with the lowest accuracy (minimum 5 questions answered in that subtopic to qualify). If fewer than 3 qualify, show however many do.

**Trend calculation (per topic):** Compare accuracy of `recentResults` (last 20) to lifetime accuracy (`totalCorrect / totalAnswered`). If recent accuracy > lifetime accuracy by 3%+: show `↑`. If recent accuracy < lifetime accuracy by 3%+: show `↓`. Otherwise: show `→`. If there are no `recentResults`, omit the trend indicator.

**Achievements list:**
Show unlocked achievements first (with unlock date), then locked ones with their condition.

| ID | Name | Condition |
|----|------|-----------|
| `first_question` | First Steps | Answer your first question |
| `first_perfect` | Flawless | Get 10 in a row correct in a session |
| `streak_3` | Hat Trick | 3-day streak |
| `streak_7` | Week Warrior | 7-day streak |
| `streak_30` | Monthly Master | 30-day streak |
| `century` | Century | 100 total questions |
| `five_hundred` | Scholar | 500 total questions |
| `thousand` | Grandmaster | 1000 total questions |
| `polyglot` | Polyglot | Reach Intermediate or higher in 3+ topics |
| `deep_dive` | Deep Dive | Expert in any topic |
| `comeback` | Comeback Kid | 3 right after 3 wrong |
| `ten_topics` | Renaissance | Play 10 different topics |

## Level Trophies

Display the trophy matching the user's current level. These are referenced by `{current trophy art}` and `Next trophy: Level {nextTrophyLevel} ({trophyName})` in the dashboard.

**Level 1** — Seedling
```
  🌱
```

**Level 3** — Sprout
```
   \|/
    |
   /|\
```

**Level 5** — Bronze Trophy
```
     ___
    '   '
    |   |
    |   |
   .'___'.
```

**Level 10** — Silver Trophy
```
    \   /
     )_(
    |   |
    |   |
    )   (
   /     \
  '-------'
```

**Level 15** — Gold Trophy
```
   ☆ \   / ☆
      )_(
  ---|   |---
     |   |
     )   (
    / ☆ ☆ \
   '-------'
```

**Level 20** — Diamond Trophy
```
      ◇
    ◇/ \◇
   / ◇ ◇ \
  ◇ MASTER ◇
   \ ◇ ◇ /
    ◇\ /◇
      ◇
```

**Level 25+** — Legendary (with stars)
```
   ★  ·  ★
  · ╔═══╗ ·
  ★ ║ ∞ ║ ★
  · ║   ║ ·
  ★ ╚═╦═╝ ★
   ·  ║  ·
   ★  ╨  ★
  LEGENDARY
```

Show the user's current trophy (the highest tier they've reached). For `Next trophy`, show the next tier's level threshold and name. If the user is Level 25+, they have the maximum trophy — omit the "Next trophy" line.
