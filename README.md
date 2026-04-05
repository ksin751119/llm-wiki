# LLM Wiki

A pattern for building personal knowledge bases using LLMs. See [LLM_WIKI.md](LLM_WIKI.md) for the full idea.

## 完整使用教學（繁體中文）

**第一次使用？** 請看 [使用教學.md](使用教學.md) — 從安裝 Obsidian 到日常操作，一步一步帶你走完。

---

## llm-wiki-guide Skill

This repo includes a Claude Code skill (`llm-wiki-guide.skill`) that guides you through building and maintaining your own LLM Wiki step by step.

### Install

```bash
# Unzip the skill package into Claude Code's skills directory
unzip llm-wiki-guide.skill -d ~/.claude/skills/llm-wiki-guide
```

After installation, restart Claude Code. The skill will be automatically detected.

### Commands

| Command | Description |
|---------|-------------|
| `/llm-wiki-guide` | Show menu and guide you to the right step |
| `/llm-wiki-guide:setup` | Initialize a new wiki (create dirs, Schema, git init) |
| `/llm-wiki-guide:ingest` | Process a new source into the wiki |
| `/llm-wiki-guide:query` | Ask questions against the wiki, optionally file answers back |
| `/llm-wiki-guide:lint` | Health-check the wiki (contradictions, orphans, gaps) |
| `/llm-wiki-guide:status` | Check wiki state and get next-step suggestions |

### Typical Workflow

```
1. /llm-wiki-guide:setup       ← Run once to initialize
2. /llm-wiki-guide:ingest      ← Run for each new source
3. /llm-wiki-guide:query       ← Explore your wiki anytime
4. /llm-wiki-guide:lint        ← Every ~5 ingests (skill will remind you)
5. /llm-wiki-guide:status      ← Check progress anytime
```

### Smart Reminders

The skill automatically tracks your wiki state via `log.md` and provides timely suggestions:

- After every 5th ingest → reminds you to lint
- After your 1st ingest → suggests trying a query
- When a query produces a valuable answer → asks if you want to file it as a wiki page
- When contradictions are found during ingest → flags them and suggests lint

### What the Skill Does for You

**`setup`** asks your domain, creates the directory structure (`raw/`, `wiki/`, `CLAUDE.md`), generates a Schema tailored to your topic, and initializes git.

**`ingest`** reads a source file, discusses key takeaways with you, creates a summary page, cascade-updates all related entity/concept pages, and updates index + log.

**`query`** reads your wiki index, finds relevant pages, synthesizes an answer with citations, and offers to save valuable answers as permanent wiki pages.

**`lint`** runs 6 checks (contradictions, orphan pages, missing pages, stale claims, cross-reference gaps, data gaps), auto-fixes what it can, and suggests next actions.

**`status`** counts your sources and pages, shows recent operations, and recommends what to do next.
