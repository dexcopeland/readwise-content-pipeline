# Readwise Content Pipeline

A Claude Code skill that transforms Readwise highlights into polished content for multiple platforms (blog posts, LinkedIn, Twitter/X, Bluesky).

## How It Works

Run `/content-pipeline` to start the pipeline. It will:
1. Connect to your Readwise library via MCP
2. Help you browse and select highlights
3. Run a Socratic interview to draw out your original insights
4. Find supporting research
5. Draft content for your chosen platforms
6. Iterate on feedback and learn your voice over time

## Key Files

- `skills/content-pipeline.md` — Main orchestrator skill (entry point)
- `skills/socratic-interview.md` — Interactive questioning to surface insights
- `skills/research-expander.md` — Finds supporting/contrasting sources
- `skills/content-drafter.md` — Multi-format content generation
- `config/platforms.json` — Platform format specs (char limits, tone, conventions)
- `preferences/voice-profile.md` — Learned tone/style preferences (grows over time)
- `output/` — Generated drafts

## Important Instructions

- **Always** read `preferences/voice-profile.md` before generating any draft content
- Use the Readwise MCP tools for highlight access (`readwise_search_highlights`, `reader_search_documents`, etc.)
- Save all final drafts to `output/<date>-<slug>/` with one file per platform
- After each feedback round, update `preferences/voice-profile.md` with new learnings

## Setup

The user must authenticate with Readwise. The MCP server is configured in `.claude/settings.json`.
