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

> **Pro tip:** Use `#` in Claude Code to quickly add something to memory mid-session. For example, type `# we use Shadcn with black-and-white theme` and it gets saved for future sessions.

---

## Section 4 — Specialised AI Skills

Claude Code has a built-in **Skills** system — instead of pasting prompts every session, you create `SKILL.md` files that Claude automatically discovers and loads when relevant. Each skill makes Claude a specialist in one domain.

### How Skills Work

- A Skill is just a folder with a `SKILL.md` file inside it
- Place them in your project at `.claude/skills/`
- Claude **automatically** uses the right skill based on your task — no manual selection needed
- Skills load on-demand, so they only use context when relevant

### Create Your Skills

#### Skill 1: Convex Specialist

Create `.claude/skills/convex-specialist/SKILL.md`:

```markdown
---
name: convex-specialist
description: Use when working with Convex — database queries, mutations, actions, schema, or any backend logic.
---
When writing Convex code:
- Query → read data from the database (use `query()`)
- Mutation → write data to the database (use `mutation()`)
- Action → send or fetch data from third-party APIs (use `action()`)
- All reads/writes go through server functions — never bypass them
- Use Convex schema validation for all tables
- All functions live in the `convex/` directory
- Use Convex built-in reactivity — no manual polling or refresh
- Keep actions separate from mutations — never mix database writes with API calls
```

#### Skill 2: Next.js Specialist

Create `.claude/skills/nextjs-specialist/SKILL.md`:

```markdown
---
name: nextjs-specialist
description: Use when working with Next.js — pages, routing, components, server/client logic, or any frontend framework code.
---
When writing Next.js code:
- Use the App Router (not Pages Router)
- Default to Server Components — only add 'use client' when genuinely needed
- Follow file-based routing conventions
- Use loading.tsx and error.tsx patterns
- Keep server and client logic cleanly separated
```

#### Skill 3: UI/UX & Frontend Engineer

Create `.claude/skills/ui-engineer/SKILL.md`:

```markdown
---
name: ui-engineer
description: Use when building UI, designing interfaces, or styling components with Shadcn.
---
When building UI:
- Use Shadcn components exclusively
- Black-and-white minimalistic theme
- Clean spacing and typography
- Mobile-responsive by default
- No unnecessary visual clutter — every element earns its place
```

### Verify Your Skills

After creating the files, start Claude Code and type:

```
/skills
```

You should see all three skills listed.

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
  - nextjs-specialist
  - ui-engineer
---
You are a Next.js frontend builder with UI design skills.

Workflow:
1. Read existing pages and components to understand the structure
2. Implement the requested feature using App Router conventions
3. Use Shadcn components with black-and-white minimalistic theme
4. Return a summary of what you built and where the files are
```

### How It All Works Together

When you ask Claude Code to build something like "add a task list feature":

1. **Claude Code** decides which subagent(s) to use based on the task
2. The **Convex Builder** subagent spins up → builds the database schema, queries, and mutations (with Convex skill loaded)
3. The **Next.js Builder** subagent spins up → builds the page and components (with Next.js + UI skills loaded)
4. Each subagent works in its **own context** and returns a clean summary
5. Your main conversation stays clean and focused

### Verify Your Subagents

```
/agents
```

You should see both subagents listed alongside the built-in ones (Explore, Plan, etc.).

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
