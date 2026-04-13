---
name: content-pipeline
description: Transform Readwise highlights into polished content for multiple platforms (blog, LinkedIn, Twitter/X, Bluesky). Orchestrates the full pipeline from highlight selection through Socratic interview, research expansion, and multi-format drafting with iterative feedback.
---

# Content Pipeline Orchestrator

You are running the content generation pipeline. Follow these phases in order.

**Important:** This pipeline assumes the working directory is the repository root (`readwise-content-pipeline/`). All file paths below are relative to that root.

## Phase 1: Readwise Highlight Selection

Help the user find and select highlights to work with.

1. Ask the user how they want to find highlights. Offer these options:
   - **Search by topic** — use `readwise_search_highlights` with a search term
   - **Browse recent highlights** — use `readwise_list_highlights` to show recent items
   - **Search Reader documents** — use `reader_search_documents` to find saved articles/books
   - **Specific document** — use `reader_get_document_highlights` if they have a specific source

   **Fallback (if MCP tools are unavailable):** If the Readwise MCP server is not connected, fall back to the Readwise CLI. Use `readwise readwise-search-highlights --query "<term>"` for search, or `readwise readwise-list-highlights` to browse. If neither MCP nor CLI is available, ask the user to paste their highlights directly.

2. If a search returns no results, suggest broader search terms or alternative search modes. If the library appears empty, ask the user to paste highlights manually so the pipeline can continue.

3. Present results in a clean list format. For each highlight show:
   - The highlight text (truncated if very long)
   - The source title and author
   - Any existing tags or notes

4. Let the user select one or more highlights. They can also ask you to search again with different terms.

5. Once highlights are selected, summarize what you're working with and confirm before proceeding.

## Phase 2: Load Voice Profile

Read `preferences/voice-profile.md` to understand the user's existing style preferences. If the profile is mostly empty (first run), note that you'll be learning their preferences through this session.

## Phase 3: Socratic Interview

Read and follow the instructions in `skills/socratic-interview.md`.

Pass the selected highlights to the interview phase. The output of this phase is a structured **insight brief**.

## Phase 4: Research Expansion

Read and follow the instructions in `skills/research-expander.md`.

Pass the insight brief from Phase 3. The output is an **enriched insight brief** with supporting evidence.

## Phase 5: Platform Selection

Ask the user which platforms they want content for. Present the options from `config/platforms.json`:
- Twitter/X (tweet or thread)
- LinkedIn
- Bluesky
- Blog post

Default: all platforms. The user can select any subset.

## Phase 6: Content Drafting

Read and follow the instructions in `skills/content-drafter.md`.

Pass the enriched insight brief, voice profile, and selected platforms.

## Phase 7: Feedback Loop

After presenting drafts:

1. Ask the user for feedback on each draft. Be specific: "How's the tone? Structure? Any phrases you'd change?"

2. Revise drafts based on feedback. You may need multiple rounds.

3. **Extract voice preferences**: After each feedback round, identify any generalizable style preferences revealed by the feedback. Examples:
   - "User shortened all my compound sentences" → preference for shorter sentences
   - "User removed all hashtags from LinkedIn" → no hashtags on LinkedIn
   - "User rewrote the opening to start with a question" → prefers question hooks

4. **Update voice profile**: Append new learnings to `preferences/voice-profile.md` under the appropriate section. Include the date and a concrete before/after example.

5. When the user approves the drafts, proceed to Phase 8.

## Phase 8: Save Output

1. Generate a slug from the content topic (lowercase, hyphens, max 50 chars).
2. Create directory: `output/<YYYY-MM-DD>-<slug>/`
3. Save each approved draft as a separate file:
   - `twitter.md`
   - `linkedin.md`
   - `bluesky.md`
   - `blog.md`
4. Include a `metadata.md` file with:
   - Source highlights (with Readwise URLs if available)
   - Date generated
   - Platforms drafted
   - Key insight summary

5. Tell the user where the files are saved and confirm the pipeline is complete.

## Run Counter

After saving, check `preferences/voice-profile.md` for a `## Run Count` section. If it exists, increment the count. If not, add it at the bottom with `Count: 1`. Every 5 runs, suggest to the user that you consolidate and deduplicate the voice profile.
