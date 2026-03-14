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

2. **Navigate into the project**
   ```bash
   cd my-app/
   ```

3. **Install dependencies & start the dev server**
   ```bash
   npm install && npm run dev
   ```

4. **Set up Convex Cloud**
   - Choose `Create new project`
   - Name it (e.g. `my-app`)
   - Select **Cloud deployment**

5. **Activate your account**
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

## Section 2 — Understanding Convex Core Concepts

Convex keeps things **fast, scalable, and enterprise-ready** by enforcing clear boundaries between read, write, and external operations.

### The Three Building Blocks

| Concept      | Purpose                                      | Example Use                        |
|--------------|----------------------------------------------|------------------------------------|
| **Query**    | Read data from the database                  | Fetch a list of users or items     |
| **Mutation** | Write data to the database                   | Create, update, or delete a record |
| **Action**   | Send/fetch data from a third-party API       | Call an external service or webhook|

### Why This Matters

Convex **does not allow direct reads or writes** from the client. Everything goes through server functions first — this separation is what makes it secure by design.

---

## Section 3 — Codebase Documentation with Claude

Before building features, generate a full codebase overview so your AI tools understand your project.

### Prompt for Claude Code

```
Can you read my entire codebase and make an MD file for you?
I am using Next.js, Convex, and WorkOS.
```

> **Tip:** Study the generated MD file — it becomes the context your AI agent uses to work within your project accurately.

---

## Section 4 — Specialised AI Agents

Create focused agents that each own one domain. This avoids confusion and keeps output high-quality.

### Agent 1: Convex Specialist

> **Role:** Everything database and backend — strictly following Convex standards.

```
You are an agent fully specialised in Convex. You follow best practices
and the professional Convex way — no overcomplicating, no wrong approaches.

Your scope:
- Query  → read data from the database
- Mutation → write data to the database
- Action  → send or fetch data from third-party APIs

Everything you write or review must follow Convex standards exclusively.
```

### Agent 2: Next.js Specialist

> **Role:** Frontend framework logic — strictly following Next.js standards.

```
You are a Next.js agent. You produce high-standard, high-quality Next.js
code without overcomplicating things or adding unnecessary extras.

You build exclusively in the Next.js standard way, with quality and
adherence to Next.js best practices.
```

### Agent 3: UI/UX & Frontend Engineer

> **Role:** Design and component quality — pixel-perfect, minimal, consistent.

```
You are a UI/UX frontend engineer and designer. You ensure every
interface is perfect, using Shadcn components with a black-and-white
minimalistic theme design.
```

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
