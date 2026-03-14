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

4. **Download Convex AI rules** (gives Claude Code and Cursor the best Convex knowledge)
   ```bash
   mkdir -p .cursor/rules && npx -y convex@latest cursor-rules
   ```

5. **Set up Convex Cloud**
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

### Step 2: Create Your Custom Project Skills

The official skills handle general best practices. Your custom skills handle **your project's specific rules** — things only you know about your app.

#### Skill 1: Convex Specialist (Custom — references official rules)

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

#### Skill 2: Project Design Rules (Custom — your app's specific look)

The official `frontend-design` and `shadcn-ui` skills handle general design best practices. This skill adds **your project's specific theme**:

Create `.claude/skills/project-theme/SKILL.md`:

```markdown
---
name: project-theme
description: Use when building UI for this project. Defines our specific design theme and conventions.
---
This project uses a specific design theme on top of Shadcn UI:

## Theme
- Black-and-white minimalistic design — no colours unless explicitly requested
- Clean spacing and generous whitespace
- Use CSS variables defined in `globals.css` for all theming

## Component conventions
- Shadcn components live in `components/ui/` — do not modify these directly
- Custom shared components go in `components/shared/`
- Use the `cn()` helper from `@/lib/utils` for conditional Tailwind classes
- Use `lucide-react` for all icons

## Key rule
- Shadcn UI components use React hooks internally — they ALWAYS need `'use client'`
- Keep client boundaries as small as possible
```

### Bonus: Convex's Official Rules Files

Convex provides comprehensive `.mdc` rule files with detailed best practices, code examples, and common mistakes. The Convex skill above already references these files automatically — you just need to download them once.

Run this in your project root:

```bash
mkdir -p .cursor/rules && npx -y convex@latest cursor-rules
```

That's it. The Convex skill already tells Claude to read these files when working on Convex code.

> **Tip:** This also works if you use Cursor — same files, both tools benefit.

### Verify Your Skills

After creating the custom files and installing the official skills, start Claude Code and type:

```
/skills
```

You should see:
- **Official (installed globally):** `frontend-design`, `react-best-practices`, `web-design-guidelines`, `react-composition-patterns`, `security-review`, `shadcn-ui`
- **Custom (your project):** `convex-specialist`, `project-theme`

---

## Section 5 — Subagents (The Workers)

Skills teach Claude *how* to do things correctly. But subagents are **separate Claude instances** that go off, do the work independently, and come back with results — keeping your main conversation clean.

### Skills vs Subagents — When to Use Each

| | Skills | Subagents |
|---|---|---|
| **What it does** | Teaches Claude rules and standards | Sends a separate worker to do a task |
| **Runs where** | Inside your current conversation | In its own isolated context window |
| **Best for** | Standards, conventions, patterns | Building features, research, reviews |
| **Analogy** | A rulebook on the desk | A specialist in another room doing the job |

**The power move:** Subagents can **preload skills**, so your Convex subagent follows Convex standards automatically while it builds.

### Create Your Subagents

You can create subagents interactively by running `/agents` in Claude Code, or create them manually:

#### Subagent 1: Convex Builder

Create `.claude/agents/convex-builder.md`:

```markdown
---
name: convex-builder
description: Build or modify Convex backend — schema, queries, mutations, actions, server functions.
tools: Read, Write, Edit, Bash, Glob, Grep
skills:
  - convex-specialist
---
You are a Convex backend builder.

Before writing any code, read `.cursor/rules/convex.mdc` or `.cursor/rules/anthropic_convex_rules.mdc` if they exist.

Workflow:
1. Read existing schema and functions in `convex/`
2. Implement the requested feature using the correct pattern (query, mutation, or action)
3. Follow Convex standards from your preloaded skill
4. Return a summary of what you built and where the files are
```

#### Subagent 2: Next.js Builder

Create `.claude/agents/nextjs-builder.md`:

```markdown
---
name: nextjs-builder
description: Build or modify Next.js pages, components, routes, layouts, or frontend logic.
tools: Read, Write, Edit, Bash, Glob, Grep
skills:
  - project-theme
---
You are a Next.js frontend builder with UI design skills.

The official frontend-design, react-best-practices, shadcn-ui, and web-design-guidelines 
skills are installed globally and will load automatically when relevant.
Your preloaded project-theme skill defines this project's specific design rules.

Workflow:
1. Read existing pages and components to understand the structure
2. Implement the requested feature using App Router conventions
3. Use Shadcn components with the project's black-and-white minimalistic theme
4. Return a summary of what you built and where the files are
```

### How It All Works Together

When you ask Claude Code to build something like "add a task list feature":

1. **Claude Code** decides which subagent(s) to use based on the task
2. The **Convex Builder** subagent spins up → builds the database schema, queries, and mutations (with custom Convex skill + official `.mdc` rules loaded)
3. The **Next.js Builder** subagent spins up → builds the page and components (with official `frontend-design`, `react-best-practices`, `shadcn-ui` skills auto-loaded + custom `project-theme` preloaded)
4. Each subagent works in its **own context** and returns a clean summary
5. Your main conversation stays clean and focused

### Verify Your Subagents

```
/agents
```

You should see both subagents listed alongside the built-in ones (Explore, Plan, etc.).

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

#### TypeScript LSP — Real-Time Error Checking

Gives Claude the same code intelligence as VS Code — go-to-definition, find references, and **real-time type error checking** after every edit.

```
/plugin install typescript-lsp@claude-plugins-official
```

Once installed, Claude can catch type errors instantly instead of grepping through your entire codebase. Since you're building with Next.js and TypeScript, this is essential.

> **Setup:** You need `typescript-language-server` installed globally:
> ```bash
> npm install -g typescript-language-server
> ```

#### Context7 — Up-to-Date Library Docs

Gives Claude access to **real, current documentation** for libraries instead of relying on training data. This means fewer hallucinations and correct API usage for Convex, Next.js, and Shadcn.

#### Superpowers — Structured Development Workflow

Adds brainstorming, test-driven development (TDD), debugging, and code review skills. Includes code simplification and security auditing — great for keeping your codebase clean as it grows.

#### Local-Review — AI Code Review Before You Commit

Runs **5 agents in parallel** to review your uncommitted changes and flag issues before they hit version control. Catches bugs, security issues, and code quality problems you'd otherwise miss.

### Exploring More Plugins

There are hundreds of community plugins available. To add more marketplaces:

```
/plugin marketplace add <marketplace-name>
```

> **Tip:** Start small — install the **TypeScript LSP** first since you're building with Next.js/TypeScript. Add more plugins as you need them. Too many plugins at once can slow things down.

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

Create a dedicated security subagent that reviews your code after every feature. Create `.claude/agents/security-reviewer.md`:

```markdown
---
name: security-reviewer
description: Review code for security vulnerabilities. Use after writing code that handles user input, authentication, API endpoints, or sensitive data.
tools: Read, Grep, Glob, Bash
skills:
  - owasp-security
---
You are a security specialist focused on identifying and remediating vulnerabilities.

Check for:
1. OWASP Top 10 vulnerabilities (injection, XSS, SSRF, CSRF)
2. Hardcoded secrets, API keys, passwords, tokens
3. Input validation — ensure all user inputs are sanitised
4. Authentication and authorisation — verify proper access controls
5. Dependency security — check for vulnerable packages

Flag each issue with severity level, file location, and a recommended fix.
Do not modify code — only report findings.
```

> **Note:** This agent has `Read`, `Grep`, `Glob`, and `Bash` but **no** `Write` or `Edit` — it can only review and report, never modify your code. This is a safety feature.

### Claude for Enterprise Security

For teams that need enterprise-grade security features, compliance, and advanced controls, Anthropic offers a dedicated security programme:

> **Join the waiting list:** [claude.com/contact-sales/security](https://claude.com/contact-sales/security)

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
