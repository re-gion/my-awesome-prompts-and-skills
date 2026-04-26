---
name: tutorial-writer
description: |
  Create, expand, audit, and polish practical Chinese tutorials from user-provided WeChat article links, blog links, official docs, or existing tutorial drafts. Use when Codex needs to: (1) write a tutorial from source articles, (2) enrich or update an existing tutorial with new links, (3) independently search official/current sources to check whether a tutorial is outdated, incorrect, or incomplete, or (4) turn technical material such as Claude Code, Codex, WSL2, Linux, Ubuntu, developer tools, or learning guides into a progressive tutorial for undergraduates, graduate students, and programmers.
---

# Tutorial Writer

## Overview

Turn source articles and current references into tutorials that are accurate, teachable, and readable. Always follow the four-stage loop: read source material, write the tutorial, verify freshness and correctness, then polish for a human, pragmatic Chinese voice.

## Mode Selection

Choose the workflow from the user's intent:

- **From 0 to 1**: Write a new tutorial from article/blog/doc links.
- **From 1 to n**: Expand, reorganize, or update an existing tutorial with newly provided links.
- **Audit/update only**: Review an existing tutorial without user-provided new links; search official docs, release notes, changelogs, and reputable recent blogs to find stale or wrong content.

If the user does not specify audience or output format, assume a Chinese tutorial for learners with basic technical literacy: senior undergraduates, graduate students, or working programmers.

## Completion Standard

A finished tutorial must:

- Be based on actually read source content, not only titles or summaries.
- Progress from low difficulty to higher difficulty.
- Explain key concepts plainly; use analogies only for important abstractions, not for every tip.
- Include practical steps, examples, caveats, and common mistakes when relevant.
- Cite or name the main sources used, while paraphrasing rather than copying long passages.
- Verify time-sensitive claims against official/current sources before presenting them as current.
- End with a concise note on what was verified, what changed, and what remains uncertain.

## Workflow

### 1. Read

Open every user-provided link and read the original text. For WeChat or other pages that cannot be fetched because of login, anti-bot checks, removed content, paywalls, or scripts, ask the user for pasted text, exported Markdown/HTML/PDF, screenshots, or another accessible copy. Do not infer article content from a title, snippet, or URL alone.

While reading, extract:

- Main claims, steps, commands, screenshots, examples, and assumptions.
- Target environment, version numbers, dates, platform constraints, and prerequisites.
- Useful teaching order: beginner concepts first, then setup, then common workflow, then advanced usage, then troubleshooting.
- Parts that are opinion, anecdote, or local experience rather than stable facts.

Preserve source intent, but do not keep the original article's structure if a tutorial needs a clearer learning path.

### 2. Write

Build the tutorial as a teaching sequence:

1. Start with what the learner will be able to do after finishing.
2. State prerequisites and environment assumptions.
3. Explain the minimum mental model before commands or procedures.
4. Move through practical steps from simple to complex.
5. Add exercises, checkpoints, or "try this" sections when they help learning.
6. Add troubleshooting and common mistakes after the main path works.
7. Add advanced topics only after the learner has a working baseline.

Prefer this tutorial shape unless the user asks for another format:

- Title
- Who this is for
- What you will learn
- Prerequisites
- Fast path / first working result
- Core concepts
- Step-by-step guide
- Practical examples
- Common mistakes and troubleshooting
- Advanced usage or next steps
- Source and freshness notes

For "from 1 to n" updates, read the existing tutorial first, identify what the new sources add, then patch the tutorial instead of rewriting everything by default. Preserve useful voice, examples, headings, and learner progression unless they block correctness.

### 3. Verify

After drafting, check whether the tutorial is current and correct.

Verification order:

- Official documentation, release notes, changelogs, manuals, standards, or vendor pages.
- Maintainer repositories, package pages, or issue trackers.
- Recent reputable technical blogs only when official sources are missing, vague, or insufficient.

For fast-moving topics such as Codex, Claude Code, WSL2, Ubuntu, package managers, APIs, CLI tools, installation commands, model capabilities, pricing, version support, or deprecations, browse/search the web unless the user explicitly forbids it. Record exact dates or version numbers for claims likely to drift.

During verification:

- Replace stale commands, flags, UI labels, install paths, and version guidance.
- Mark claims that could not be verified instead of smoothing them over.
- Separate "officially documented behavior" from "blogger's experience" or "local workaround".
- If a source conflict exists, prefer official docs and explain the conflict briefly.
- If the task involves runnable commands and a local environment is available, run the smallest safe verification command; otherwise say it was not run.

### 4. Polish

Before finalizing, read the whole tutorial as a learner. Load `references/style-checklist.md` and apply it.

Polishing priorities:

- Keep the tone efficient, practical, and clear.
- Remove inflated claims, vague authority, filler transitions, and formulaic AI phrasing.
- Vary sentence length without making the writing chatty.
- Use concrete examples in place of abstract encouragement.
- Keep analogies short and only for concepts that learners commonly struggle with.
- Trust the reader: explain enough to unblock them, but do not over-explain obvious operations.

## Source Discipline

Do not reproduce long copyrighted passages from articles. Summarize, restructure, and cite. Short quotes are acceptable only when the wording itself matters.

When sources are unavailable, say exactly what is missing and ask for the original content. A tutorial based on inaccessible links is not complete.

## Final Response Pattern

When handing the result back to the user, include:

- What was created or updated.
- Whether it is ready to use.
- What sources were read and what current sources were checked.
- Any stale, uncertain, or unverified areas.
