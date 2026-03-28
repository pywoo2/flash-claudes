---
name: quiz-stats
description: Display your Flash Claudes quiz stats dashboard — levels, streaks, per-topic accuracy, weak spots, and achievements.
allowed-tools: Bash(date *), Bash(cat *), Bash(mkdir *)
---

# Flash Claudes — Stats Dashboard

Read the quiz state using Bash (not the Read tool) and display a comprehensive stats dashboard:
```
mkdir -p ~/.flash-claudes && cat ~/.flash-claudes/state.json 2>/dev/null || echo "NO_STATE"
```

If the state file doesn't exist, say:
```
No quiz data yet! Run /flash-claudes:quiz to get started.
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
Topic           Tier          Correct   Attempted
------------------------------------------------------
{topic}         {tier}        {correct}✓   {answered}
...
------------------------------------------------------

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

**Achievements list:**
Show unlocked achievements first (with unlock date), then locked ones with their condition.

| ID | Name | Condition |
|----|------|-----------|
| `first_question` | First Steps | Answer your first question |
| `first_perfect` | Flawless | Get 10 in a row correct |
| `streak_3` | Hat Trick | 3-day streak |
| `streak_7` | Week Warrior | 7-day streak |
| `streak_30` | Monthly Master | 30-day streak |
| `century` | Century | 100 total questions |
| `five_hundred` | Scholar | 500 total questions |
| `thousand` | Grandmaster | 1000 total questions |
| `polyglot` | Polyglot | Intermediate+ in 3 topics |
| `deep_dive` | Deep Dive | Expert in any topic |
| `comeback` | Comeback Kid | 3 right after 3 wrong |
| `ten_topics` | Renaissance | Play 10 different topics |
