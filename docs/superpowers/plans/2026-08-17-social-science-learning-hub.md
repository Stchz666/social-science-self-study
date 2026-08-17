# Social Science Learning Hub Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build and publish a durable social-science self-study hub that Codex can use to plan sessions and recover learning progress.

**Architecture:** The root Git repository tracks plans, progress, logs, exercises, projects, and source metadata. Third-party course repositories live under ignored `upstream/` as independent Git clones, allowing Codex to read them without copying their histories into the learning hub.

**Tech Stack:** Git, GitHub CLI, Markdown, Stata course materials

## Global Constraints

- Publish the root repository as `Stchz666/social-science-self-study` with public visibility.
- Treat `upstream/` as read-only reference material and exclude it from the root Git history.
- Use `PROGRESS.md` as the durable source of current learning status.
- Preserve source URLs and exact upstream revisions in `SOURCES.md`.
- Do not commit credentials, Stata license files, restricted data, or redistributed textbook files.

---

### Task 1: Create the learning-management layer

**Files:**
- Create: `README.md`
- Create: `AGENTS.md`
- Create: `LEARNING_PLAN.md`
- Create: `PROGRESS.md`
- Create: `SOURCES.md`
- Create: `.gitignore`
- Create: `learning-logs/README.md`
- Create: `exercises/README.md`
- Create: `projects/README.md`

**Interfaces:**
- Consumes: The approved design in `docs/superpowers/specs/2026-08-17-social-science-learning-hub-design.md`.
- Produces: A project entry point and durable state files used by future Codex sessions.

- [ ] **Step 1: Create the hub documents and directory guides**

Use focused Markdown files: repository overview in `README.md`, agent behavior in `AGENTS.md`, curriculum in `LEARNING_PLAN.md`, state in `PROGRESS.md`, and provenance in `SOURCES.md`.

- [ ] **Step 2: Verify the management files**

Run:

```bash
test -f README.md && test -f AGENTS.md && test -f LEARNING_PLAN.md && test -f PROGRESS.md && test -f SOURCES.md
```

Expected: exit code 0.

### Task 2: Add the first upstream course

**Files:**
- Create locally but ignore from root Git: `upstream/Stata-Fundamentals/`
- Modify: `SOURCES.md`
- Modify: `PROGRESS.md`

**Interfaces:**
- Consumes: The `upstream/` policy from `.gitignore` and `AGENTS.md`.
- Produces: A readable local course repository and a recorded source revision.

- [ ] **Step 1: Clone the official course repository**

Run:

```bash
git clone https://github.com/dlab-berkeley/Stata-Fundamentals.git upstream/Stata-Fundamentals
```

Expected: an independent Git checkout containing `lessons/` and `README.md`.

- [ ] **Step 2: Record the exact revision and initialize progress**

Write the output of the following command into `SOURCES.md`:

```bash
git -C upstream/Stata-Fundamentals rev-parse HEAD
```

Set the active track in `PROGRESS.md` to Stata Fundamentals Part 1.

- [ ] **Step 3: Verify isolation**

Run:

```bash
git check-ignore -v upstream/Stata-Fundamentals/README.md
```

Expected: `.gitignore` reports the `upstream/` rule.

### Task 3: Validate and publish the initial hub

**Files:**
- Track: all root documents and directory guides created by Tasks 1 and 2
- Exclude: `upstream/`

**Interfaces:**
- Consumes: The complete local hub and authenticated GitHub CLI session.
- Produces: Public repository `Stchz666/social-science-self-study` with local `main` tracking `origin/main`.

- [ ] **Step 1: Run structural and content checks**

Run:

```bash
git status --short
git check-ignore -v upstream/Stata-Fundamentals/README.md
rg -n 'LEARNING_PLAN.md|PROGRESS.md|SOURCES.md|upstream/' README.md AGENTS.md
```

Expected: only intended hub files are untracked; the upstream README is ignored; README and AGENTS contain the required durable-context references.

- [ ] **Step 2: Commit the initial hub**

Run:

```bash
git add .gitignore AGENTS.md LEARNING_PLAN.md PROGRESS.md README.md SOURCES.md docs exercises learning-logs projects
git commit -m "chore: initialize social science learning hub"
```

Expected: one root commit on `main`; no `upstream/` content in the commit.

- [ ] **Step 3: Create and push the public GitHub repository**

Run:

```bash
gh repo create Stchz666/social-science-self-study --public --source=. --remote=origin --push
```

Expected: the public repository is created and local `main` tracks `origin/main`.

- [ ] **Step 4: Verify local and remote state**

Run:

```bash
git status --short --branch
git remote -v
gh repo view Stchz666/social-science-self-study --json nameWithOwner,visibility,defaultBranchRef,url
git ls-tree -r --name-only HEAD
```

Expected: clean `main...origin/main`, public visibility, default branch `main`, and no tracked paths under `upstream/`.
