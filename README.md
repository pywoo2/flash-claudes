# ⚡ Flash Claudes

An interactive quiz plugin for [Claude Code](https://docs.anthropic.com/en/docs/claude-code). Quiz yourself on any topic, learn from detailed explanations, and level up with XP, streaks, and trophies.

## Quick Start

```
/plugin marketplace add pywoo2/flash-claudes
/plugin install flash-claudes@flash-claudes
/reload-plugins
```

Then type `/quiz` and you're in.

## How It Works

1. **Pick a topic** — anything (Python, SQL, Rust, sleep science, whatever)
2. **Choose your style** — multiple choice, open-ended, or a mix
3. **Set your level** — tell it how familiar you are
4. **Answer questions** — get detailed explanations after every answer
5. **Ask follow-ups** — dig deeper before moving on (type `n` for next)
6. **Quit anytime** — type `q` to stop and see your session summary

## Commands

| Command | What it does |
|---------|-------------|
| `/quiz` | Start a quiz — pick from your topics or type a new one |
| `/quiz <topic>` | Jump straight into a specific topic |
| `/quiz random` | Random topic from your history (or starter set if new) |
| `/quiz stats` | Full stats dashboard |
| `/quiz-stats` | Standalone stats dashboard |

During a quiz: `s` for stats, `q` to quit.

## Features

### Adaptive Difficulty
Four tiers that adjust based on how you're doing:

| Tier | Question Types |
|------|---------------|
| Beginner | Multiple choice, true/false |
| Intermediate | Spot the bug, predict the output |
| Advanced | Fill-in-the-blank, multi-concept problems |
| Expert | Open-ended with partial credit, design tradeoffs |

### Learn as You Go
Every answer gets a thorough explanation — right or wrong. Ask as many follow-up questions as you want before moving on. This is a learning tool, not just a test.

### XP & Levels
Earn XP for every answer. Harder questions = more XP. Streak bonuses kick in at 3+ correct in a row.

### Trophies

Unlock ASCII art trophies as you level up:

```
🌱 Seedling (Lv 1) → Sprout (Lv 3) → Bronze (Lv 5)
→ Silver (Lv 10) → Gold (Lv 15) → Diamond (Lv 20)
→ ★ Legendary (Lv 25+)
```

### Achievements

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
| Polyglot | Intermediate or higher in 3+ topics |
| Deep Dive | Reach Expert in any topic |
| Comeback Kid | 3 right after 3 wrong |
| Renaissance | Play 10 different topics |

### Daily Streaks
Play every day to build your streak. Your longest streak is tracked too.

### Per-Topic Mastery
Each topic tracks your tier, correct/attempted count, and subtopic weak spots independently.

## Uninstalling

Open `/plugin` → **Installed** tab → remove flash-claudes.

To also delete your quiz data:
```bash
rm -rf ~/.local/share/flash-claudes
```

## Development

```bash
git clone git@github.com:pywoo2/flash-claudes.git
```
Then in Claude Code:
```
/plugin marketplace add ./flash-claudes
/plugin install flash-claudes@flash-claudes
```

## Data

Quiz state: `~/.local/share/flash-claudes/state.json` — see `quiz-state.example.json` for the schema.

## License

MIT
