# Flash Claudes

An interactive quiz plugin for Claude Code. Pick any topic, answer questions, and level up. Your progress persists between sessions.

## Prerequisites

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed and working

## Install

```bash
claude plugin add pywoo2/flash-claudes
```

That's it. No other dependencies or configuration needed.

To verify it installed correctly, open Claude Code and type:

```
/quiz
```

You should see surprised Pikachu and a welcome screen.

### Updating

To pull the latest version:

```bash
claude plugin update pywoo2/flash-claudes
```

### Uninstalling

```bash
claude plugin remove flash-claudes
```

This removes the plugin but keeps your quiz data at `~/.flash-claudes/state.json`. To remove that too:

```bash
rm -rf ~/.flash-claudes
```

### Local development

Clone and install from a local path:

```bash
git clone git@github.com:pywoo2/flash-claudes.git
claude plugin add ./flash-claudes
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
When you start a new topic, you'll be asked how familiar you are — just describe your experience in plain language. The quiz calibrates to your level from there and adapts as you answer.

Four tiers of difficulty:
- **Beginner** — Multiple choice, true/false
- **Intermediate** — Spot the bug, predict the output
- **Advanced** — Fill-in-the-blank, multi-concept problems
- **Expert** — Open-ended AI-graded questions, design tradeoffs

At the start of each session, pick your question style: **multiple choice** (click your answer), **open-ended** (type freely), or a **mix** of both.

### Learn as You Go
Every answer comes with a detailed explanation. After each question, you can ask follow-up questions to dig deeper before moving on. The quiz waits for you — type `n` or `next` when you're ready to continue.

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
| Flawless | 10 in a row correct |
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

Quiz state is stored at `~/.flash-claudes/state.json`. See `quiz-state.example.json` for the full schema.

## License

MIT
