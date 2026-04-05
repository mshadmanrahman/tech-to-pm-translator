# Tech-to-PM Translator

<p align="center">
  <img src="assets/hero.png" alt="Tech-to-PM Translator" width="720" />
</p>

A Claude Code skill that reads your engineering docs and turns them into something you can actually use.

New to Claude Code? Start at [claudecodeguide.dev](https://claudecodeguide.dev) — zero jargon, from first install to daily use.

---

## The problem

Engineers write docs for engineers. PMs read them and miss 60% of the meaning.

Architecture decisions, failure modes, and system constraints are buried in code references, file paths, and implementation jargon that non-engineers cannot parse. You end up reading the same paragraph three times, nodding along, and still not knowing what to ask in your next engineering sync.

The result: worse bug reports. Vague specs. Conversations where you can tell the engineer thinks you don't understand the system — because you don't.

---

## Translation, not summarization

This is the thing that makes this skill different from just asking Claude to "summarize these docs."

**Summarization** loses detail. A PM reading a summary still cannot answer follow-up questions. They just know slightly less than before, with more confidence.

**Translation** reframes the same information for a different audience. Every fact stays. Every failure mode stays. What changes is the framing — from "here is how we built it" to "here is what it means for you."

A PM reading a translated doc can understand what breaks, why it breaks, who owns it, and how to talk about it with engineers.

---

## What you get

**Before — what the engineering doc says:**

> `AuthMiddleware` throws a `401` when the JWT signature validation fails against the RS256 public key stored in `config/keys/auth.pem`. Token expiry is checked via `exp` claim against server UTC. Silent failure occurs when `NEXT_PUBLIC_AUTH_BYPASS=true` in non-prod envs.

**After — what the translator produces:**

> **When users get logged out unexpectedly**
>
> This happens when the login token is invalid, expired, or was issued in a different environment. Tokens expire based on server time — if a user's device clock is significantly off, they may see this more often.
>
> **PM Takeaway:** If QA reports "always logged in" on staging but users are getting logged out in production, this is the likely cause. File the bug with the environment name and whether it's intermittent or consistent.
>
> **Who to talk to:** Auth team owns this area.

Same information. Different audience.

---

## What it produces

Run the skill against your engineering docs and you get up to four document types, depending on what the source material covers:

| Document | Purpose |
|----------|---------|
| **Platform Guide** | How the system works end-to-end: user flows, data pipelines, integrations |
| **Bug Anatomy** | Bug families with symptom/cause/severity tables, filing guide, prioritization framework |
| **Migration Landscape** | What's changing, dependency maps, decision framework for fix depth |
| **Architecture Overview** | Infrastructure and system design in PM-friendly terms |

---

## The Five Transformations

Every technical pattern gets converted the same way:

| Technical Pattern | PM Translation |
|------------------|----------------|
| Code snippet or config | Table or plain English description |
| Implementation detail | "What it does" + "When it matters" |
| File paths and function names | "Who owns it" + "What area" |
| Error handling code | "What breaks and why" symptom table |
| Architecture decisions | Decision + impact + "What it means for you" |

---

## Audience modes

The default output is written for PMs. But you can ask for a different audience:

| Audience | Focus |
|----------|-------|
| **PM** (default) | Bug filing, prioritization, spec writing, stakeholder communication |
| **Designer** | Component library, breakpoints, styling systems, i18n/RTL rules, text expansion |
| **Stakeholder** | Business impact only: what it does, what's changing, risk areas |
| **New-hire** | Onboarding depth: everything + glossary + "where to find more" |

---

## Installation

You need Claude Code installed first. If you haven't done that yet, [claudecodeguide.dev](https://claudecodeguide.dev) walks you through it in plain English.

Once Claude Code is running, there are two ways to add this skill.

### Option 1: Copy the skill file (recommended)

Open your terminal and run:

```bash
# Project-level — only available in this project
mkdir -p .claude/skills/tech-to-pm-translator
cp SKILL.md .claude/skills/tech-to-pm-translator/SKILL.md

# Or user-level — available across all your projects
mkdir -p ~/.claude/skills/tech-to-pm-translator
cp SKILL.md ~/.claude/skills/tech-to-pm-translator/SKILL.md
```

### Option 2: Reference it from your CLAUDE.md

If your project already has a `CLAUDE.md` file, add this:

```markdown
## Skills
- Tech-to-PM Translator: `path/to/tech-to-pm-translator/SKILL.md`
```

---

## How to use it

Open Claude Code and say any of these:

- `translate docs for PMs`
- `make this PM-friendly`
- `convert tech docs`
- `create PM context from docs/architecture/`
- `/tech-to-pm`

With options:

```
Translate the docs in .claude/ref/ for designers, output to docs/design-context/
```

```
Create PM context from docs/architecture/ for new-hires
```

---

## A real-world example

This skill was built by doing the translation manually on a live codebase first, then encoding that process so it could run automatically.

**Input:** 18 developer reference files for a Next.js education platform — routing, middleware, CMS, search, auth, forms, internationalization, tracking, testing, CI/CD, tech debt, and three simultaneous migrations running at once.

**Output:**

- **Platform Guide** (280 lines): Page rendering pipeline, search mechanics, lead forms, translation systems — including a +30% text expansion rule that causes silent layout failures, which no PM on the team knew about
- **Bug Anatomy** (250 lines): Six bug families with symptom/cause/severity tables. Why bugs become non-reproducible. How to write a great bug report. PM-to-engineer communication phrase guide.
- **Migration Landscape** (220 lines): Three migrations explained with before/after tables. Decision framework for when to invest properly vs. apply a minimal fix. ASCII dependency diagram. PM checklist.
- **Architecture Overview**: Refreshed from outdated v12 docs to current v16 reality — the team had been working from documentation that no longer described the system they were running.

---

## Hard rules

The skill enforces these in every output. No exceptions.

1. **Zero code.** No code blocks, no file paths, no function names.
2. **Every section gets a "PM Takeaway".** The translation anchor.
3. **Symptom-first.** Organized by "what you'll encounter" not "how it's built."
4. **Failure modes included.** Engineers document happy paths. PMs need to know what breaks.
5. **Ownership mapped.** Every area links to a team or person.
6. **Warnings preserved.** "NEVER cache X" in source becomes "X must never be cached. Here's why." in output.

---

## Quality checks

Before finalizing, the skill verifies:

- [ ] Zero code in output
- [ ] Every section has a PM Takeaway
- [ ] All ownership mapped
- [ ] Failure modes included
- [ ] Warnings preserved from source docs
- [ ] Cross-references link documents
- [ ] Glossary covers all domain terms
- [ ] Tables over paragraphs wherever possible
- [ ] No file paths or function names leaked

---

## Part of the PM Toolkit Family

Open-source tools for PMs who use Claude Code:

| Tool | What it does |
|------|-------------|
| [pm-pilot](https://github.com/mshadmanrahman/pm-pilot) | Claude Code configured for PMs. Meeting prep, PRDs, market sizing — 25 skills, ready to install. |
| [bug-shepherd](https://github.com/mshadmanrahman/bug-shepherd) | Zero-code bug triage for PMs. Reproduce and sync bugs without reading a line of code. |
| [morning-digest](https://github.com/mshadmanrahman/morning-digest) | Your morning briefed in 30 seconds. Calendar, email, Slack, and action items in one digest. |
| [claudecode-guide](https://github.com/mshadmanrahman/claudecode-guide) | The friendly guide to Claude Code. Zero jargon — from first install to daily operating system. |
| [root-kg](https://github.com/mshadmanrahman/root-kg) | Your knowledge graph. Ask questions across all your notes, meetings, and emails — cited answers in plain English. |
| **tech-to-pm-translator** | **You are here** |

---

## Contributing

Issues and PRs welcome. If you run this on your codebase and find gaps in the templates or translation rules, please share what you learned. The best improvements have come from real engineering docs hitting edge cases the templates didn't expect.

## License

MIT. See [LICENSE](LICENSE).

## Author

[Shadman Rahman](https://github.com/mshadmanrahman)

Built with Claude Code. Inspired by the gap between what engineers write and what PMs need to read.
