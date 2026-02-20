# Draft Email: Getting More Out of Claude Code

---

**Subject:** Tips for Using Claude Code More Efficiently

**To:** Team
**From:** [Your Name]

---

Hi team,

As we continue to use Claude Code day-to-day, I wanted to share some practical tips that will help you get better results, faster. Whether you're just getting started or have been using it for a while, these practices make a real difference.

---

## 1. The CLAUDE.md File

This is the single most impactful thing you can set up. Claude Code automatically reads `CLAUDE.md` at the start of every session, so it acts as a persistent brief that you never have to repeat.

**What to put in it:**

- **Project context** — what the project does, its tech stack, architecture overview
- **Coding conventions** — naming conventions, preferred patterns, what to avoid
- **Key commands** — how to run tests, linters, builds, and common scripts
- **Important constraints** — things Claude should never do (e.g. "never push to main directly", "always add tests for new functions")
- **Repo structure notes** — where key directories and files live

**Where to put it:**

- Root `CLAUDE.md` — applies to all Claude sessions in the repo
- Sub-directory `CLAUDE.md` — applies only when Claude is working in that folder (useful for monorepos or projects with distinct frontend/backend)

**Example snippet:**

```markdown
# Project: MyApp API

## Stack
Node.js 20, TypeScript, PostgreSQL, Prisma ORM, Jest for testing

## Key Commands
- `npm run dev` — start local server
- `npm test` — run test suite
- `npm run lint` — run ESLint

## Conventions
- All new functions must have corresponding unit tests
- Use `snake_case` for database fields, `camelCase` for TypeScript
- Never commit directly to `main`

## Do Not
- Add console.log statements to production code
- Skip error handling at API boundaries
```

Think of it as an onboarding doc that Claude reads every time — invest a bit of time upfront and every session starts with full context.

---

## 2. Prompting Best Practices

The quality of what Claude produces is directly tied to how clearly you describe the task. A few habits that consistently improve results:

**Be specific about what you want**
Instead of: *"Fix the login bug"*
Try: *"The login endpoint returns a 500 when the email contains a `+` character. The handler is in `src/auth/login.ts`. Fix the input validation to handle this correctly and add a test case."*

**Provide relevant context upfront**
Tell Claude which files are involved, what the expected behaviour is, and what you've already tried. It saves multiple back-and-forth turns.

**Specify the format of the output**
If you want a list of options, say so. If you want code only with no explanation, say that. If you want a plan before implementation, ask for it explicitly.

**Break large tasks into steps**
For complex features, ask Claude to first explain its approach, confirm it with you, then implement. This catches misunderstandings early.

**Use the `#` file reference shorthand**
In the terminal, typing `#filename.ts` lets you reference a file directly in your prompt without Claude having to search for it.

**Ask Claude to think before acting on ambiguous tasks**
Prefix with: *"Before making any changes, explain your understanding of what needs to be done and what approach you'll take."*

---

## 3. Session Management and Handover Documents

Claude Code does not retain memory between sessions — each new session starts fresh. Managing context well is key to avoiding repetition and maintaining momentum across long or multi-day pieces of work.

**The context window**
Within a session, Claude has a large but finite context window. On very long sessions, earlier context gets summarised automatically. For tasks that span many files or involve lots of back-and-forth, consider:

- Starting a new session for a new logical task
- Summarising progress at natural checkpoints

**Handover documents**
For work spanning multiple sessions, ask Claude to produce a handover note at the end of each session. Prompt it with:

*"Summarise what we've done in this session, what's been completed, what's still outstanding, and any important decisions or context the next session will need."*

Save this as a `HANDOVER.md` or paste it into CLAUDE.md temporarily. At the start of the next session, share it with Claude to restore context instantly.

**Structured progress tracking**
Ask Claude to maintain a `TODO.md` or task list as you work. Claude Code has a built-in todo tool it uses internally — you can also ask it to write tasks to a file so they persist across sessions.

**Named session notes**
If you work on multiple streams, keep a `sessions/` folder with dated notes (e.g. `sessions/2024-01-15-auth-refactor.md`) capturing decisions, open questions, and next steps.

---

## 4. Skills and Custom Tools

Claude Code supports custom **skills** (slash commands) and **tools** (MCP servers) that extend what it can do.

**Skills (slash commands)**
Skills are pre-written prompt templates you can invoke with `/skill-name`. They're great for repetitive workflows your team runs regularly.

Examples of useful skills to set up:
- `/commit` — generates a well-formatted commit message from staged changes
- `/review-pr` — reviews a pull request with a consistent checklist
- `/write-tests` — writes unit tests for a given function or module
- `/explain` — provides a plain-language explanation of a piece of code

Skills are defined in your Claude Code settings and can be shared across the team by committing them to the repo.

**MCP (Model Context Protocol) Tools**
MCP servers give Claude access to external tools and data sources. Useful integrations include:

- **Databases** — let Claude query your database schema and write/validate SQL
- **GitHub** — Claude can read issues, PRs, and repo metadata directly
- **Jira/Linear** — connect task management so Claude has ticket context
- **Slack** — surface relevant conversation threads as context
- **File systems and APIs** — connect internal tooling Claude can call

MCP servers can be configured in your `.claude/settings.json` file. Check the MCP directory for available servers or build your own.

---

## 5. Other Tips for Efficiency and Effectiveness

**Use `/clear` to reset context mid-session**
If a session has gone down an unhelpful path or the context is cluttered, `/clear` resets without closing the session. Useful when switching tasks.

**Leverage the plan mode**
For non-trivial tasks, start with `Shift+Tab` to enter plan mode. Claude will propose a plan and wait for your approval before making any changes. This prevents it from going off in the wrong direction on complex work.

**Iterative refinement over single big prompts**
It's often faster to start with a rough working version and iteratively refine than to try to specify every detail upfront. Ask Claude to "get it working first, then we'll clean it up."

**Use `--continue` or `/resume` for interrupted work**
If a session gets cut off, you can often resume with recent context rather than starting over. Keep handover notes (see above) as a backup.

**Read the output, don't just accept it**
Claude will produce confident-sounding code that can contain subtle bugs. Always review what it produces, especially around error handling, edge cases, and security-sensitive areas.

**Commit little and often**
Ask Claude to commit after each logical unit of work. This gives you clean checkpoints to roll back to if a later change goes wrong.

**Ask Claude to explain its changes**
After implementing something, ask: *"Briefly explain what you changed and why."* This helps you understand the code and catch any misunderstandings.

**Keep CLAUDE.md up to date**
As the project evolves, update CLAUDE.md. A 10-minute investment to document a new pattern or convention saves every future session from having to re-learn it.

---

Happy to walk through any of these in more detail or help set up CLAUDE.md and skills for our projects.

[Your Name]
