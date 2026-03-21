# Tech-to-PM Translator

A Claude Code skill that converts technical developer documentation into PM/designer-friendly knowledge base documents.

## The Problem

Engineers write docs for engineers. PMs read them and miss 60% of the meaning. Architecture decisions, failure modes, and system constraints are buried in code references, file paths, and implementation jargon that non-engineers can't parse.

The result: PMs file worse bug reports, write vague specs, and can't have informed conversations with engineers about system behavior.

## The Solution

This skill reads your engineering docs and produces structured, **code-free** knowledge base files that non-engineers can actually use.

**Input:** Technical markdown files (architecture refs, API docs, runbooks, ADRs, READMEs)

**Output:** Up to 4 document types, depending on source material:

| Document | Purpose |
|----------|---------|
| **Platform Guide** | How the system works end-to-end: user flows, data pipelines, integrations |
| **Bug Anatomy** | Bug families with symptom/cause/severity tables, filing guide, prioritization framework |
| **Migration Landscape** | What's changing, dependency maps, decision framework for fix depth |
| **Architecture Overview** | Infrastructure and system design in PM-friendly terms |

## Key Principle: Translation, Not Summarization

- **Summarization** loses detail. A PM reading a summary still can't answer questions.
- **Translation** reframes the same information for a different audience. A PM reading a translated doc can understand what breaks, why, and who to talk to.

## The Five Transformations

| Technical Pattern | PM Translation |
|------------------|----------------|
| Code snippet or config | Table or plain English description |
| Implementation detail | "What it does" + "When it matters" |
| File paths and function names | "Who owns it" + "What area" |
| Error handling code | "What breaks and why" symptom table |
| Architecture decisions | Decision + impact + "What it means for you" |

## Audience Modes

| Audience | Focus |
|----------|-------|
| **PM** (default) | Bug filing, prioritization, spec writing, stakeholder communication |
| **Designer** | Component library, breakpoints, styling systems, i18n/RTL rules, text expansion |
| **Stakeholder** | Business impact only: what it does, what's changing, risk areas |
| **New-hire** | Onboarding depth: everything + glossary + "where to find more" |

## Installation

### Option 1: Copy the skill file

Copy `SKILL.md` into your Claude Code skills directory:

```bash
# Project-level (recommended)
mkdir -p .claude/skills/tech-to-pm-translator
cp SKILL.md .claude/skills/tech-to-pm-translator/SKILL.md

# Or user-level (available across all projects)
mkdir -p ~/.claude/skills/tech-to-pm-translator
cp SKILL.md ~/.claude/skills/tech-to-pm-translator/SKILL.md
```

### Option 2: Reference from CLAUDE.md

Add to your project's `CLAUDE.md`:

```markdown
## Skills
- Tech-to-PM Translator: `path/to/tech-to-pm-translator/SKILL.md`
```

## Usage

In Claude Code, say any of:

- `translate docs for PMs`
- `make this PM-friendly`
- `convert tech docs`
- `create PM context from docs/architecture/`
- `/tech-to-pm`

### With options:

```
Translate the docs in .claude/ref/ for designers, output to docs/design-context/
```

```
Create PM context from docs/architecture/ for new-hires
```

## Example: Real-World Output

This skill was built by doing the translation manually first, then encoding the process.

**Input:** 18 developer reference files for a Next.js education platform covering routing, middleware, CMS, search, auth, forms, i18n, tracking, testing, CI/CD, tech debt, and three simultaneous migrations.

**Output:**
- **Platform Guide** (280 lines): Page rendering pipeline, search mechanics, lead forms, translation systems (with +30% text expansion rules and silent failure warnings), tracking, auth, CMS
- **Bug Anatomy** (250 lines): Six bug families with symptom/cause/severity tables. Why bugs become non-reproducible. How to write a great bug report. PM-engineer communication phrase guide.
- **Migration Landscape** (220 lines): Three migrations explained with before/after tables. Decision framework (invest properly vs. minimal fix). ASCII dependency diagram. PM checklist.
- **Architecture Overview**: Refreshed from outdated v12 docs to current v16 reality.

## Hard Rules

The skill enforces these in every output:

1. **Zero code.** No code blocks, no file paths, no function names.
2. **Every section gets a "PM Takeaway".** The translation anchor.
3. **Symptom-first.** Organize by "what you'll encounter" not "how it's built."
4. **Failure modes included.** Engineers document happy paths. PMs need to know what breaks.
5. **Ownership mapped.** Every area links to a team or person.
6. **Warnings preserved.** "NEVER cache X" in source becomes "X must never be cached. Here's why." in output.

## Quality Checks

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

## Part of the PM Toolkit Family

Open-source tools for PMs who ship with AI:

| Tool | What it does |
|------|-------------|
| [PM Pilot](https://github.com/mshadmanrahman/pm-pilot) | 20 skills, 5 agents for product managers using Claude Code |
| [Bug Shepherd](https://github.com/mshadmanrahman/bug-shepherd) | Zero-code bug triage with parallel AI agents |
| **Tech-to-PM Translator** | **You are here** |
| [Morning Digest](https://github.com/mshadmanrahman/morning-digest) | AI-powered daily briefing from calendar, email, and Slack |

## Contributing

Issues and PRs welcome. If you use this skill on your codebase and find gaps in the templates or translation rules, please share what you learned.

## License

MIT. See [LICENSE](LICENSE).

## Author

[Shadman Rahman](https://github.com/mshadmanrahman)

Built with Claude Code. Inspired by the gap between what engineers write and what PMs need to read.
