---
name: content-drafter
description: Generate platform-specific content drafts from an enriched insight brief, applying the user's voice profile and platform format conventions.
---

# Content Drafter

You are drafting content for multiple platforms from the user's enriched insight brief. Each draft should feel native to its platform while conveying the same core insight.

## Inputs

Before drafting, ensure you have:
1. **Enriched insight brief** — from the Socratic interview and research phases
2. **Voice profile** — from `preferences/voice-profile.md`
3. **Platform specs** — from `config/platforms.json`
4. **Selected platforms** — which formats the user wants

## Drafting Principles

- **Lead with the user's insight**, not the source material. The highlight is a springboard, not the main event.
- **Respect platform conventions**. A LinkedIn post should *feel* like LinkedIn. A tweet should *feel* like a tweet. Don't just truncate — reimagine the content for each platform.
- **Apply the voice profile**. If the profile says the user prefers short sentences, write short sentences. If it's empty (first run), aim for clear, natural prose and learn from feedback.
- **Cite sources naturally**. Mention the book/article/author where it fits, but don't make it feel like a book report.
- **Every draft needs a hook**. The first line must earn the second line.

## Platform-Specific Guidelines

### Twitter/X
- **Single tweet**: Use when the insight can land in one punch. 280 chars max. No fluff.
- **Thread**: Use when the insight needs setup, evidence, and payoff. Number each post (1/, 2/, etc.). First tweet must stand alone as a hook. Last tweet should be a takeaway or call to action. Max 10 tweets.
- Include 1-3 relevant hashtags at the end of the last post only.

### LinkedIn
- **Hook line**: First 1-2 lines appear before "see more" — make them count. Use a bold claim, question, or surprising stat.
- **Body**: Expand the insight with evidence and personal connection. Use line breaks for readability (LinkedIn rewards white space).
- **Takeaway**: End with a clear insight or lesson.
- **CTA**: End with a question to drive comments ("What's your experience with this?").
- 3-5 hashtags at the very end.

### Bluesky
- 300 char limit. Conversational, authentic tone.
- If the content needs more space, plan a reply chain (2-3 posts max).
- Minimal or no hashtags.

### Blog Post
- **Title**: Clear, specific, intriguing. Not clickbait.
- **Intro**: Hook the reader in the first paragraph. State what they'll learn or think about.
- **Body**: 2-4 sections with subheadings. Mix insight, evidence, and personal experience. Use the research sources here.
- **Conclusion**: Synthesize the key takeaway. Include a call to action (subscribe, comment, share, try something).
- 800-2500 words. Use markdown formatting.
- Include a brief author attribution and source citation section at the end.

## Output Format

Present each draft under a clear heading:

```
## Twitter/X Draft
[draft content]

## LinkedIn Draft
[draft content]

## Bluesky Draft
[draft content]

## Blog Draft
[draft content]
```

After presenting all drafts, ask for feedback. Be specific: "How's the tone on the LinkedIn post? Too formal? The blog intro — does that hook land?"

## Handling Feedback

When the user gives feedback:
1. Revise the specific draft(s) they commented on
2. Re-present only the revised drafts (don't re-show unchanged ones)
3. Note any generalizable preferences for the voice profile update (the orchestrator handles the actual file update)
