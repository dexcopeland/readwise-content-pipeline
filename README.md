# Readwise Content Pipeline

A Claude Code skill that transforms your Readwise highlights into polished content for multiple platforms — blog posts, LinkedIn, Twitter/X, and Bluesky.

The pipeline draws out your original thinking through Socratic questioning, finds supporting research, then drafts platform-native content. Over time it learns your voice and tone from feedback.

## How It Works

1. **Select highlights** — Browse or search your Readwise library
2. **Socratic interview** — Answer questions designed to surface your unique perspective (not just summarize what you read)
3. **Research expansion** — Find supporting data, studies, or counterpoints to strengthen your content
4. **Draft content** — Get platform-specific drafts tailored to each format's conventions
5. **Iterate** — Give feedback, get revisions, and the pipeline learns your style for next time

## Prerequisites

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed and authenticated
- A [Readwise](https://readwise.io) account with highlights

## Setup

### 1. Clone and enter the repo

```bash
git clone <your-repo-url>
cd readwise-content-pipeline
```

### 2. Connect Readwise

The pipeline accesses your Readwise library through an MCP (Model Context Protocol) server. The server is already configured in `.claude/settings.json` — you just need to authenticate.

**Option A: MCP server (recommended)**

The MCP server is pre-configured to use `mcp-remote` with the Readwise MCP endpoint. When you first start Claude Code in this repo, it will connect to `https://mcp2.readwise.io/mcp` and prompt you to authenticate via your browser.

No additional setup is needed — just start Claude Code and follow the auth prompt.

**Option B: Access token (manual)**

If you prefer to authenticate with an access token:

1. Get your token from [readwise.io/access_token](https://readwise.io/access_token)
2. Set it as an environment variable before starting Claude Code:

```bash
export READWISE_ACCESS_TOKEN=your_token_here
```

**Option C: Readwise CLI**

If you have the Readwise CLI installed separately, the pipeline can fall back to CLI commands like `readwise readwise-search-highlights`. Install it with:

```bash
npm install -g readwise-cli
readwise login
```

### 3. Run the pipeline

Start Claude Code in the repo directory and invoke the skill:

```
/content-pipeline
```

Follow the interactive prompts to select highlights, answer interview questions, review research, and refine your drafts.

## Output

Finished drafts are saved to `output/<date>-<slug>/` with one file per platform:

```
output/2026-04-13-deep-work-myth/
├── twitter.md
├── linkedin.md
├── bluesky.md
├── blog.md
└── metadata.md
```

## Voice Profile

The file `preferences/voice-profile.md` stores your writing preferences, learned from feedback you give during each run. It starts empty and grows over time. After a few runs, the pipeline's first drafts should closely match your natural voice.

You can also edit this file directly if you want to seed it with known preferences.

## Project Structure

```
├── CLAUDE.md                        # Project instructions for Claude Code
├── .claude/
│   ├── settings.json                # MCP server configuration
│   └── skills/
│       └── content-pipeline.md      # Skill entry point
├── skills/
│   ├── content-pipeline.md          # Main orchestrator
│   ├── socratic-interview.md        # Insight extraction through questioning
│   ├── research-expander.md         # Supporting source discovery
│   └── content-drafter.md           # Platform-specific draft generation
├── config/
│   └── platforms.json               # Platform format specs
├── preferences/
│   └── voice-profile.md             # Learned tone/style (grows with use)
└── output/                          # Generated drafts
```

## Supported Platforms

| Platform   | Format                        | Limits         |
|------------|-------------------------------|----------------|
| Twitter/X  | Single tweet or thread        | 280 chars/post |
| LinkedIn   | Hook + insight + CTA          | 3000 chars     |
| Bluesky    | Post or reply chain           | 300 chars/post |
| Blog       | Full article with subheadings | 800-2500 words |

Platform specs are configurable in `config/platforms.json`.
