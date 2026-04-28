# Senior Product Manager — PRD Generator Prompt

A system prompt that turns an LLM into a Senior Product Manager who walks you through creating a complete, agent-ready Product Requirements Document via chat.

Designed for vibe-coding workflows — the output PRD is meant to feed directly into an AI coding agent (Claude Code, Cursor, Codex, Gemini Code Assist, etc.). It deliberately skips engineering-team concerns like time estimates, effort points, and team size and focuses on what an agent actually needs to build the product: clear goals, personas, user stories, functional requirements, UX, and a priority-ordered build sequence.

## What's in this repo

- **`Senior Product Manager.md`** — the system prompt
- **`README.md`** — this file

## What you get

A complete PRD in clean Markdown, structured as:

1. **Product Overview** — concise summary
2. **Goals** — business goals, user goals, non-goals
3. **User Personas** — user types, persona details, role-based access (auto-inferred)
4. **User Stories** — `US-1`, `US-2`, … in *"As a [persona], I want to [action] so that [outcome]"* format
5. **Functional Requirements** — `FR-1`, `FR-2`, … cross-referenced to user stories where applicable
6. **User Experience** — entry points, core flow, edge cases, UI/UX highlights
7. **Narrative** — concrete user-facing scenario
8. **Success Metrics** — table with baseline, target, timeframe across user / business / technical types
9. **Technical Considerations** — integrations, data, scale, risks
10. **Build Phases** — priority-ordered (scaffolding → core → polish), not time-boxed

Plus a separate **Review Notes** section flagging weak spots and suggested validations so you know what to pressure-test before sharing the doc.

## How to use it (Gemini Gem)

1. Open [Gemini](https://gemini.google.com/) and go to **Gems → New Gem**.
2. Name it (e.g., "Senior Product Manager") and add an optional description.
3. Open `Senior Product Manager.md`, copy the entire contents, and paste them into the **Instructions** field.
4. Save.
5. Start chatting — the Gem opens with *"What do you want to build?"* and takes it from there.

## How to use it elsewhere

Works the same way with any LLM that supports custom system prompts:

- **ChatGPT** — paste into a Custom GPT's instructions
- **Claude** — paste into a Project's custom instructions
- **API / playground** — use as the `system` prompt

## How a session flows

1. **Kickoff.** The assistant greets you and asks what you want to build. Your first reply is mined aggressively — title, summary, goals, personas, integrations, even early user stories are seeded if mentioned.
2. **Slot-filling.** Targeted follow-up questions, walking section by section. At any point you can:
   - Say *"skip"* or *"suggest a default"* to move on without blocking
   - Revise any earlier answer
   - Ask *"show me what we have so far"* for a live draft with `{{placeholders}}` still visible
3. **Consistency check.** Before finalizing, the assistant verifies that every user story has an implementing FR, every goal has a success metric, and personas/goals/stories don't contradict each other. Issues are surfaced for you to resolve.
4. **Summary + confirmation.** One-line summary per section. You confirm or request edits.
5. **Final PRD.** Clean Markdown, ready to paste into Notion, GitHub, Confluence, or directly into your AI coding agent.

## Key behaviors

- **Opinionated.** Pushes back on vague answers (*"improve engagement"* → *"which metric, baseline, target, by when?"*).
- **Helpful when stuck.** Proposes sensible defaults with brief rationale instead of blocking on slots you can't answer cold.
- **No filler.** Skips pleasantries and recapping. Moves directly to the next question.
- **Captures specifics verbatim.** Numbers, dates, proper nouns, and exact metric phrasing are preserved.
- **Multi-slot detection.** If one of your answers covers several fields, all of them are filled — no re-asking.
- **Auto-fills.** `Version Number` = `v1`. `Role-Based Access` is inferred from your personas and goals — multi-role when distinct permission tiers exist (admin / editor / viewer, owner / member / guest, etc.), single-role otherwise.
- **Mid-flow revision.** Change any earlier answer at any time without restarting.

## License

Free to use, modify, and share.
