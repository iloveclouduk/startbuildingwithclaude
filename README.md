# Full-Stack Web App Workshop Guide

> **Stack:** Next.js · Convex (Backend) · WorkOS AuthKit (Authentication)

---

## Section 1 — Project Setup & Authentication

Get a fully functional, secured web app running in minutes — no manual coding required.

### Steps

1. **Scaffold the project**
   ```bash
   npm create convex@latest
   ```
   - Select **Next.js** as the framework
   - Select **AuthKit (WorkOS)** for authentication

2. **Navigate into the project** (default is `my-app`, or whatever name you chose)
   ```bash
   cd my-app/
   ```

3. **Install dependencies & start the dev server**
   ```bash
   npm install && npm run dev
   ```

4. **Set up Convex Cloud**
   - Choose `Create new project`
   - Name it (e.g. `my-app`, or any name you want)
   - Select **Cloud deployment**

5. **Activate your account**
   - **Important:** Make sure you use the **same email** for both Convex and WorkOS.
   - Confirm email, create a strong password, verify — done.

6. **Open the app**
   - Visit [http://localhost:3000](http://localhost:3000/)
   - You now have a running app with **Next.js frontend**, **Convex backend**, and **enterprise-grade auth**.

### Convex Dashboard

Once running, you can monitor everything live at your Convex dashboard:

```
https://dashboard.convex.dev/t/<your-username>/<your-project>/<deployment-slug>
```

You'll see real-time logs like sign-in redirects, callback handling, and database mutations — all streaming automatically because **Convex syncs in real time**.

---

---

> **You're done with the setup — happy coding!** You now have a fully working app with a **frontend** (Next.js), **authentication** (WorkOS), and **backend** (Convex). That's a real application, running and ready to build on.
>
> Your **landing page**, **authentication page**, and **main application page** are already built and ready. You can redesign the frontend and authentication page to match your brand, then focus on the **main application functionality** — where you'll work closely with **Convex** and **Next.js** to customise it for your core business. Below, we'll showcase tips and best practices for Claude Code to help you make it even better.

---

## Section 2 — Understanding Convex Core Concepts

Convex keeps things **fast, scalable, and enterprise-ready** by enforcing clear boundaries between read, write, and external operations.

### The Three Building Blocks

| Concept      | Purpose                                      | Example Use                        |
|--------------|----------------------------------------------|------------------------------------|
| **Query**    | Read data from the database                  | Fetch a list of users or items     |
| **Mutation** | Write data to the database                   | Create, update, or delete a record |
| **Action**   | Send/fetch data from a third-party API       | Call an external service or webhook|


---

## Section 3 — Codebase Documentation with Claude Code

Before building features, let Claude Code understand your entire project. It has a **built-in command** for this — no custom prompt needed.

### Generate Your CLAUDE.md

Inside your project directory, open Claude Code and run:

```
/init
```

That's it. Claude Code will automatically:
- Scan your entire project (package files, configs, code structure, README, etc.)
- Generate a `CLAUDE.md` file tailored to your project
- Include build commands, test instructions, key directories, and coding conventions it detected

### What is CLAUDE.md?

It's your **project's memory**. Every time you start a new Claude Code session, this file is loaded automatically as context — so Claude already knows your project without you re-explaining anything.

### Keep It Updated

As your project grows, run `/init` again — Claude Code will review the existing `CLAUDE.md` and suggest improvements.

### Add Convex Rules to CLAUDE.md

After `/init` generates your `CLAUDE.md`, open it and add this at the bottom:

```markdown
## Convex Rules
When working with Convex, always read `.cursor/rules/convex.mdc` or 
`.cursor/rules/anthropic_convex_rules.mdc` for official best practices, 
function syntax, schema patterns, and code examples before writing code.
```

This ensures Claude knows about the rules files in **every session** — not just when the skill or agent is active.

> **You now have Convex rules referenced in three places:**
> - **CLAUDE.md** — loaded every session, always available
> - **Convex Skill** — loaded when Claude works on Convex code
> - **Convex Builder Agent** — loaded when the subagent builds backend features
>
> No matter how Claude enters your Convex code, it will find the rules.

> **Pro tip:** Use `#` in Claude Code to quickly add something to memory mid-session. For example, type `# we use Shadcn with black-and-white theme` and it gets saved for future sessions.

---

## Section 4 — Specialised AI Skills

Claude Code has a built-in **Skills** system — instead of pasting prompts every session, you create `SKILL.md` files that Claude automatically discovers and loads when relevant. Each skill makes Claude a specialist in one domain.

### How Skills Work

- A Skill is just a folder with a `SKILL.md` file inside it
- Place them in your project at `.claude/skills/`
- Claude **automatically** uses the right skill based on your task — no manual selection needed
- Skills load on-demand, so they only use context when relevant

### Step 1: Install Official Pre-Built Skills

For Next.js and UI/UX, **don't write your own** — install the official ones from the teams who build these tools. Run these in your terminal:

```bash
# ──────────────────────────────────────────────
# FROM ANTHROPIC (official)
# ──────────────────────────────────────────────

# Frontend design — distinctive UI, avoids generic "AI slop" (277K+ installs)
npx skills add anthropics/claude-code --skill frontend-design -g -y

# ──────────────────────────────────────────────
# FROM VERCEL (official — the team behind Next.js)
# ──────────────────────────────────────────────

# React & Next.js performance — 40+ rules across 8 categories
npx skills add vercel-labs/agent-skills@react-best-practices -g -y

# Web design & accessibility — 100+ rules for UI quality
npx skills add vercel-labs/agent-skills@web-design-guidelines -g -y

# React composition patterns — clean component architecture
npx skills add vercel-labs/agent-skills@react-composition-patterns -g -y

# ──────────────────────────────────────────────
# FROM SENTRY (official — the error tracking company)
# ──────────────────────────────────────────────

# Security review — 17 vulnerability types, structured reports
npx skills install getsentry/skills@security-review -g -y

# ──────────────────────────────────────────────
# FROM COMMUNITY (verified)
# ──────────────────────────────────────────────

# Shadcn UI component patterns
npx skills add giuseppe-trisciuoglio/developer-kit@shadcn-ui -g -y
```

> **Why official skills?** They're maintained by the teams who build these tools — Anthropic for design, Vercel for React/Next.js, Sentry for security. They get updated when the frameworks change. Writing your own risks being wrong or outdated.
>
> **What each one does:**
>
> | Skill | Provider | What it covers |
> |---|---|---|
> | `frontend-design` | **Anthropic** | Bold typography, colour palettes, animations, layout — breaks out of generic AI design |
> | `react-best-practices` | **Vercel** | Server Components, bundle optimisation, memoisation, data fetching — 40+ rules |
> | `web-design-guidelines` | **Vercel** | Accessibility, ARIA, focus states, touch targets, dark mode, forms — 100+ rules |
> | `react-composition-patterns` | **Vercel** | Compound components, state lifting, clean prop patterns |
> | `security-review` | **Sentry** | Injection, XSS, SSRF, CSRF, auth, crypto — structured vulnerability reports |
> | `shadcn-ui` | **Community** | Shadcn component patterns, CLI usage, theming |

### Step 2: Create Your Custom Convex Skill

The official skills above cover Next.js, UI/UX, Shadcn, and security. But **Convex doesn't have an official Claude Code skill yet** — they provide `.mdc` rule files for Cursor, not a `SKILL.md`. So this custom skill is the bridge that tells Claude to read those official Convex rules.

| What | How | Custom skill needed? |
|---|---|---|
| **Next.js** | Official `react-best-practices` from Vercel | No |
| **UI/UX** | Official `frontend-design` from Anthropic + `web-design-guidelines` from Vercel | No |
| **Shadcn** | Official `shadcn-ui` community skill | No |
| **Security** | Official `security-review` from Sentry | No |
| **Convex** | Custom skill that references official `.mdc` rule files | **Yes** |

#### Convex Specialist (Custom — references official rules)

Create `.claude/skills/convex-specialist/SKILL.md`:

```markdown
---
name: convex-specialist
description: Use when working with Convex — database queries, mutations, actions, schema, or any backend logic.
---
## Reference files
When working on Convex code, FIRST read these files for detailed patterns and examples:
- `.cursor/rules/convex.mdc` (if it exists)
- `.cursor/rules/anthropic_convex_rules.mdc` (if it exists)
These contain comprehensive official Convex best practices maintained by the Convex team.
Always follow patterns in these reference files over general knowledge.

When writing Convex code:

## Core functions
- Query → read data (use `query()` constructor from `"./_generated/server"`)
- Mutation → write data (use `mutation()` constructor)
- Action → call third-party APIs (use `action()` constructor)

## Argument validation (critical)
- ALWAYS define args with validators: `args: { id: v.id("users"), name: v.string() }`
- Never use unvalidated handler arguments — a client could pass any value
- Import validators from `import { v } from "convex/values"`

## Code structure
- Keep query/mutation/action handlers as thin wrappers
- Put business logic in plain TypeScript helper functions in `convex/model/`
- All functions live in the `convex/` directory

## Database best practices
- Use indexes (`.withIndex()`) instead of `.filter()` on `.collect()` — filtered results still count towards bandwidth
- Use Convex schema validation for all tables
- Mutations are full transactions automatically — no begin/end needed
- Use Convex built-in reactivity — no manual polling or refresh

## Actions rules
- Actions CANNOT read/write the database directly
- Actions must use `ctx.runQuery()` and `ctx.runMutation()` to interact with the database
- Keep actions as small as possible — only the external API call should be in the action
- Prefer scheduling actions from mutations (`ctx.scheduler.runAfter()`) over calling actions directly from client
- Never mix database writes with external API calls in the same function
```

### Optional: Download Convex's Official Rules Files

If you're using Claude Code or Cursor, Convex provides comprehensive `.mdc` rule files with detailed best practices, code examples, and common mistakes. The Convex skill above already references these files — you just need to download them once.

Run this in your project root:

```bash
mkdir -p .cursor/rules && npx -y convex@latest cursor-rules
```

The Convex skill already tells Claude to read these files when working on Convex code.

> **Tip:** This also works if you use Cursor — same files, both tools benefit.

### Verify Your Skills

After creating the custom files and installing the official skills, start Claude Code and type:

```
/skills
```

You should see:
- **Official (installed globally):** `frontend-design`, `react-best-practices`, `web-design-guidelines`, `react-composition-patterns`, `security-review`, `shadcn-ui`
- **Custom (your project):** `convex-specialist`

---

## Section 5 — Subagents (The Workers)

Skills teach Claude *how* to do things correctly. But subagents are **separate Claude instances** that go off, do the work independently, and come back with results — keeping your main conversation clean.

### Skills vs Subagents — When to Use Each

| | Skills | Subagents |
|---|---|---|
| **What it does** | Teaches Claude rules and standards | Sends a separate worker to do a task |
| **Runs where** | Inside your current conversation | In its own isolated context window |
| **Best for** | Standards, conventions, patterns | Building features, security reviews |
| **Can restrict tools?** | No | Yes — you control what it can/can't do |
| **Analogy** | A rulebook on the desk | A specialist in another room doing the job |

### Why Only 2 Agents

Now that official skills auto-load for Next.js, UI/UX, and Shadcn, most agents would just duplicate what skills already do. We only keep agents that **add value skills can't provide**:

| Agent | Why it exists (what skills can't do) |
|---|---|
| **Convex Builder** | Preloads your custom Convex skill + reads `.mdc` rules + works in **isolated context** so big backend tasks don't pollute your main conversation |
| **Security Reviewer** | **Read-only by design** — has `Read`, `Grep`, `Glob`, `Bash` but NO `Write` or `Edit`. It literally cannot modify your code, only report issues. Skills can't restrict tools like this |

### Create Your Subagents

For each agent below, follow this flow in Claude Code:

1. Run `/agents`
2. Select **Create new agent**
3. Choose **Project-level** (shared with your team via version control)
4. Select **Generate with Claude**
5. Paste the description below when prompted
6. Choose a **model** (Sonnet recommended for balance of speed and quality)
7. Pick a **background colour** (helps identify which agent is running)
8. Review the generated file — press `e` to edit if needed
9. Save — available immediately, no restart needed

#### Subagent 1: Convex Builder

Paste this when Claude asks you to describe the agent:

```
A Convex backend builder specialised in building and modifying schema, 
queries, mutations, actions, and server functions. It should preload 
the convex-specialist skill and always read .cursor/rules/convex.mdc 
before writing any code. It returns a summary of what was built and 
which files were created or modified.
```

After Claude generates the agent, review it (`e` to edit), then:
- **Tools:** keep all selected (needs Read, Write, Edit, Bash, Glob, Grep)
- **Skills:** make sure `convex-specialist` is listed
- **Model:** Sonnet (good balance of speed and quality)

#### Subagent 2: Security Reviewer

Repeat the same flow (`/agents` → Create → Project-level → Generate with Claude), then paste:

```
A read-only security reviewer that scans code for vulnerabilities 
but never modifies any files. It should preload the security-review 
skill. It checks for OWASP Top 10, hardcoded secrets, input validation, 
auth issues, and dependency vulnerabilities. It reports each issue 
with severity, file location, and a recommended fix.
```

After Claude generates the agent, review it (`e` to edit), then:
- **Tools:** deselect Write and Edit — keep only Read, Grep, Glob, Bash
- **Skills:** make sure `security-review` is listed
- **Model:** Sonnet

> **Note:** The Security Reviewer has **no** `Write` or `Edit` tools — it can only review and report, never modify your code. This is a deliberate safety feature that skills alone cannot provide.

### Verify Your Subagents

```
/agents
```

You should see `convex-builder` and `security-reviewer` alongside the built-in ones (Explore, Plan, etc.).

### How It All Works Together

When you ask Claude Code to build something like "add a task list feature":

1. **Claude Code** works in your main conversation with official skills auto-loaded (`react-best-practices`, `frontend-design`, `shadcn-ui`, `web-design-guidelines`)
2. For backend work, the **Convex Builder** subagent spins up → builds the database schema, queries, and mutations in its own context (with custom Convex skill + official `.mdc` rules loaded)
3. After building, you ask the **Security Reviewer** to check the code → it scans for vulnerabilities in its own context and reports back findings without touching your code
4. Your main conversation stays clean and focused throughout

---

## Section 6 — Plugins (Ready-Made Power-Ups)

Claude Code has a **plugin system** — ready-made extensions you can install in seconds to give Claude extra capabilities. Think of them as power-ups for your codebase.

### How to Install Plugins

The official Anthropic marketplace is already available. To browse and install:

```
/plugin
```

This opens an interactive menu. Go to the **Discover** tab to see available plugins. To install directly from the command line:

```
/plugin install <plugin-name>@claude-plugins-official
```

### Recommended Plugins for This Stack

The official Anthropic marketplace is already available in Claude Code. Browse with `/plugin` → Discover tab, or install directly.

> **Less is more.** Every plugin loads into Claude's context, uses tokens, and adds decisions Claude has to make. Start with 3 essentials. Add more only when you hit a real problem.

#### Essential — Install These 4

```bash
# 1. TypeScript LSP — real-time type checking and error detection
/plugin install typescript-lsp

# 2. Code Simplifier — refines code for clarity after building features
/plugin install code-simplifier

# 3. Security Guidance — catches vulnerabilities as you write code
/plugin install security-guidance

# 4. Feature Dev — structured building: explore → architect → implement → review
/plugin install feature-dev
```

| Plugin | Why it's essential |
|---|---|
| `typescript-lsp` | You're building in Next.js/TypeScript — catches type errors instantly instead of grepping. Needs `npm install -g typescript-language-server` |
| `code-simplifier` | Keeps your codebase clean as you build fast — run it after finishing a feature |
| `security-guidance` | Catches injection, XSS, unsafe patterns in real time — critical since you handle auth with WorkOS |
| `feature-dev` | Guides every feature through a structured workflow — explore the codebase first, design the architecture, implement with quality gates, then review. Uses 3 specialised agents (explorer, architect, reviewer) so features are built properly from the start |

#### Optional — Add When You Need Them

```bash
# Ready to commit? Clean git workflow commands
/plugin install commit-commands

# Reviewing a PR? 6 specialised review agents
/plugin install pr-review-toolkit

# Automated code review with confidence scoring
/plugin install code-review

# Structured feature building: explore → architect → implement → review
/plugin install feature-dev

# Building Agent SDK apps
/plugin install agent-sdk-dev

# Frontend design (also available as a skill)
/plugin install frontend-design
```

> **Tip:** All of these are from the official Anthropic marketplace — no third-party trust needed. Browse everything available with `/plugin` → Discover tab.

---

## Section 7 — Security (Skills, Agents & Built-in Tools)

Security shouldn't be an afterthought. Claude Code has built-in security features plus community skills and agents to keep your codebase safe.

### Built-in: `/security-review`

Claude Code ships with a security review command out of the box. Run it anytime to scan your pending changes:

```
/security-review
```

This checks for SQL injection risks, cross-site scripting (XSS), authentication flaws, insecure data handling, and dependency vulnerabilities — all without installing anything extra.

### Security Skill: OWASP Standards

Install the OWASP security skill to give Claude knowledge of current security standards when writing or reviewing code:

```bash
curl -sL https://raw.githubusercontent.com/agam/claude-code-owasp/main/.claude/skills/owasp-security/SKILL.md \
  -o .claude/skills/owasp-security/SKILL.md --create-dirs
```

Once installed, Claude automatically activates this skill when you say things like "review this code for security issues" or "is this authentication implementation secure?". It covers OWASP Top 10, input validation, auth patterns, and secure coding across multiple languages.

### Security Skill: Sentry's Security Review

Already installed in Section 4 (Step 1). Built by Sentry's team — provides structured vulnerability reports with file locations, confidence levels, and fix recommendations. Covers 17 vulnerability types including injection, XSS, SSRF, CSRF, auth, and crypto.

### Security Agent: Security Reviewer

Already created in Section 5. This subagent has **no** `Write` or `Edit` tools — it can only review and report, never modify your code. Use it after building features:

```
Use the security-reviewer agent to check my latest changes
```

### Claude for Enterprise Security

For teams that need enterprise-grade security features, compliance, and advanced controls, Anthropic offers a dedicated security programme:

> **Join the waiting list:** [claude.com/contact-sales/security](https://claude.com/contact-sales/security)

---

---

## Quick Reference

```
npm create convex@latest     # scaffold
cd my-app && npm install      # install
npm run dev                   # start dev server
```

**Stack at a glance:**
- **Frontend:** Next.js
- **Backend:** Convex (real-time, serverless)
- **Auth:** WorkOS AuthKit
- **UI Library:** Shadcn (black & white minimal theme)
