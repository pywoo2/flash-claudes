---
name: quiz-stats
description: Display your Flash Claudes quiz stats dashboard — levels, streaks, per-topic accuracy, weak spots, and achievements.
allowed-tools: Read, Bash(date *), Bash(cat *)
---

# Flash Claudes — Stats Dashboard

Read the quiz state from `~/.claude/quiz/state.json` and display a comprehensive stats dashboard.

If the state file doesn't exist, say:
```
No quiz data yet! Run /flash-claudes:quiz to get started.
```

## Dashboard Format

Display the following:

```
========================================
        FLASH CLAUDES STATS
========================================

Level {level} — {xp}/{xpToNext} XP
[{progressBar}] {pct}% to next level

Streak: {currentStreak} days (best: {longestStreak})
Total: {totalAnswered} questions | {totalCorrect} correct ({overallAccuracy}%)

TOPICS
--------------------------------------------------------------
Topic           Tier          Accuracy   Answered   Trend
--------------------------------------------------------------
{topic}         {tier}        {pct}%     {count}    {arrow} {delta}%
...
--------------------------------------------------------------

WEAK SPOTS
- {subtopic} in {topic}: {accuracy}% ({correct}/{total})
- {subtopic} in {topic}: {accuracy}% ({correct}/{total})
- {subtopic} in {topic}: {accuracy}% ({correct}/{total})

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

**Trend:** Compare accuracy of `recentResults` (last 20 answers) to lifetime accuracy for each topic.
- If recent > lifetime by 3%+: up arrow + green delta
- If recent < lifetime by 3%+: down arrow + red delta
- Otherwise: flat arrow

**Weak spots:** Find the 3 subtopics with the lowest accuracy (minimum 5 questions answered in that subtopic to qualify). If fewer than 3 qualify, show however many do.

**Achievements list:**
Show unlocked achievements first (with unlock date), then locked ones with their condition.

| ID | Name | Condition |
|----|------|-----------|
| `first_question` | First Steps | Answer your first question |
| `first_perfect` | Flawless | Get 10/10 in a round |
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
