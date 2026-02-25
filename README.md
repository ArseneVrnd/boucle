# Boucle

Context checkpoint plugin for Claude Code. Creates concise snapshots of your progress between work phases so you can safely clear context and resume later.

## What it does

When working on multi-phase projects, Claude's context window fills up. Boucle creates a structured checkpoint that captures:

- What's been completed
- Current build/test status
- What's next (with key files and blockers)
- A summary for the next agent to pick up seamlessly

## Install

```bash
claude plugin add ArseneVrnd/Boucle
```

## Usage

```
/boucle
```

Run this between phases of any multi-step implementation. The checkpoint is saved to your project's memory directory as `boucle-checkpoint.md`.

## License

MIT
