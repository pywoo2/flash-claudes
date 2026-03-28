# Flash Claudes

An interactive quiz plugin for Claude Code. Pick any topic, answer questions, and level up. Your progress persists between sessions.

## Install

Add to your Claude Code plugins:

```bash
claude plugin add pywoo2/flash-claudes
```

Or install locally for development:

```bash
claude plugin add ./path/to/flash-claudes
```

## Commands

| Command | What it does |
|---------|-------------|
| `/quiz` | Start a quiz — pick from your topics or type a new one |
| `/quiz <topic>` | Jump straight into a specific topic |
| `/quiz random` | Random topic from your history (or starter set if new) |
| `/quiz stats` | Full stats dashboard |

During a quiz, you can type `s` for stats or `q` to quit at any time.

## Features

### Adaptive Difficulty
Questions scale with your skill. Each topic progresses through four tiers:
- **Beginner** — Multiple choice, true/false
- **Intermediate** — Spot the bug, predict the output
- **Advanced** — Fill-in-the-blank, multi-concept problems
- **Expert** — Open-ended AI-graded questions, design tradeoffs

### Progression
- **XP & Levels** — Earn XP for every answer (more for harder questions). Level up as you go.
- **Daily Streaks** — Come back each day to build your streak.
- **Per-Topic Mastery** — Track accuracy and tier for each topic independently.
- **Subtopic Weak Spots** — Identifies your weakest areas so you know what to practice.

### Achievements
Unlock badges as you hit milestones:

| Badge | How to unlock |
|-------|--------------|
| First Steps | Answer your first question |
| Flawless | 10/10 in a round |
| Hat Trick | 3-day streak |
| Week Warrior | 7-day streak |
| Monthly Master | 30-day streak |
| Century | 100 questions answered |
| Scholar | 500 questions answered |
| Grandmaster | 1000 questions answered |
| Polyglot | Intermediate+ in 3 topics |
| Deep Dive | Reach Expert in any topic |
| Comeback Kid | 3 right after 3 wrong |
| Renaissance | Play 10 different topics |

## Data

Quiz state is stored at `~/.claude/quiz/state.json`. See `quiz-state.example.json` for the full schema.

## License

MIT
