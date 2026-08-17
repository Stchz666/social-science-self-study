# Political Science Resource Backlog Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create a discoverable `TODO.md` that preserves the selected political science and computational social science repositories for later review without changing the active Stata learning path.

**Architecture:** `TODO.md` is a non-active candidate pool, grouped by intended use and readiness. `README.md` exposes one navigation link; `LEARNING_PLAN.md`, `PROGRESS.md`, and `SOURCES.md` remain unchanged until a candidate is actually used.

**Tech Stack:** Markdown, Git, GitHub CLI

## Global Constraints

- Keep Stata Fundamentals as the current learning path and leave `PROGRESS.md` unchanged.
- Do not clone any candidate repository or create exercise directories for it.
- Treat Star counts as a snapshot dated 2026-08-17.
- Do not stage `exercises/stata-fundamentals/part-01/01_introduction_my.do`.
- Add a candidate to `SOURCES.md` only after it is read, cloned, or cited in later work.

---

### Task 1: Create the Resource Backlog and Navigation Entry

**Files:**
- Create: `TODO.md`
- Modify: `README.md`

**Interfaces:**
- Consumes: the approved resource list and repository metadata snapshot
- Produces: a stable backlog entry point linked from the repository README

- [ ] **Step 1: Refresh the GitHub metadata snapshot**

Run:

```bash
for repo in kosukeimai/qss apachecn/stanford-game-theory-notes-zh gesiscss/awesome-computational-social-science elder-frog/OpenCourseCatalog briatte/awesome-network-analysis tsinghua-fib-lab/AgentSociety HarborLibrary/Political-Science; do
  gh api "repos/$repo" --jq '[.full_name,.stargazers_count,.pushed_at,(.license.spdx_id // "NOASSERTION"),.html_url] | @tsv'
done
```

Expected: seven rows with accessible GitHub URLs. Preserve the refreshed Star values in the document and keep the snapshot date at 2026-08-17.

- [ ] **Step 2: Create `TODO.md` with the approved categories**

Create the following sections and entries:

```markdown
# 待办与资源候选

本文件保存值得日后查看的课程、资源地图和研究工具。它们尚未进入正式学习主线；当前唯一主线仍是 Stata Fundamentals。

## 使用规则

- Star 数是 2026-08-17 的检索快照，会随时间变化。
- Star 用于判断社区关注度，课程结构、许可和实际练习价值拥有更高优先级。
- 开始阅读、克隆或引用某个项目时，将其登记到 `SOURCES.md`，并在 `PROGRESS.md` 中安排一个明确的下一步。
- 每次只激活一个后续主项目，避免同时铺开多条路线。

## 优先查看

| 项目 | Star 快照 | 中文适配 | 主要用途 | 建议时机 |
| --- | ---: | --- | --- | --- |
| [QSS](https://github.com/kosukeimai/qss) | 278 | 中等：英文教材，代码和数据清晰 | 定量社会科学与政治学方法主课 | 完成 Stata Fundamentals 后评估 |
| [斯坦福博弈论中文笔记](https://github.com/apachecn/stanford-game-theory-notes-zh) | 215 | 高：中文笔记 | 博弈论、政治经济学与策略互动 | 掌握基础概率后选读 |

## 资源地图

| 项目 | Star 快照 | 中文适配 | 主要用途 | 注意事项 |
| --- | ---: | --- | --- | --- |
| [Awesome Computational Social Science](https://github.com/gesiscss/awesome-computational-social-science) | 929 | 较低：以英文资源为主 | 寻找计算社会科学课程、书籍和工具 | 作为导航使用，不要求从头读完 |
| [OpenCourseCatalog](https://github.com/elder-frog/OpenCourseCatalog) | 8,982 | 高：中文目录和 B 站入口 | 寻找国内易访问的公开课视频 | 政治学条目较少，维护时间较早 |

## 进阶实验

| 项目 | Star 快照 | 中文适配 | 主要用途 | 建议时机 |
| --- | ---: | --- | --- | --- |
| [Awesome Network Analysis](https://github.com/briatte/awesome-network-analysis) | 4,093 | 较低：英文资源为主 | 政治传播、组织和关系网络分析 | 掌握 R 或 Python 后选择专题 |
| [AgentSociety](https://github.com/tsinghua-fib-lab/AgentSociety) | 1,200 | 高：提供中文文档 | 智能体模拟与计算社会科学实验 | 具备 Python 与研究设计基础后 |

## 谨慎参考

| 项目 | Star 快照 | 价值 | 风险与决定 |
| --- | ---: | --- | --- |
| [HarborLibrary/Political-Science](https://github.com/HarborLibrary/Political-Science) | 2,447 | 中文政治学书目线索 | 缺少清晰课程结构与仓库许可证，并含大量可能仍受版权保护的全文文件；不整体 Fork、克隆或再分发 |
```

If Step 1 returns a different Star value, use the refreshed value in `TODO.md` while retaining the snapshot date 2026-08-17.

- [ ] **Step 3: Add `TODO.md` to README navigation**

Insert this row immediately after the `PROGRESS.md` row:

```markdown
| [TODO.md](TODO.md) | 尚未激活的课程、资源地图和进阶项目候选 |
```

- [ ] **Step 4: Validate the Markdown change**

Run:

```bash
test -f TODO.md
rg -n 'QSS|AgentSociety|HarborLibrary' TODO.md
rg -n '\[TODO.md\]\(TODO.md\)' README.md
git diff --check -- TODO.md README.md
```

Expected: all commands exit with status 0 and `git diff --check` prints no output.

- [ ] **Step 5: Commit only the backlog and navigation**

```bash
git add TODO.md README.md
git diff --cached --check
git commit -m "docs: add political science resource backlog"
```

Expected: the untracked Stata do-file remains absent from the commit.

### Task 2: Publish the Existing Branch and Refresh the Draft PR

**Files:**
- Modify remotely: Draft PR `#1`

**Interfaces:**
- Consumes: committed `TODO.md` and README navigation from Task 1
- Produces: an updated remote branch and a Draft PR that accurately describes the full documentation change

- [ ] **Step 1: Verify branch scope before pushing**

Run:

```bash
git status --short --branch
git show --check --stat --oneline HEAD
```

Expected: `01_introduction_my.do` remains untracked, and the new commit contains only `TODO.md` and `README.md`.

- [ ] **Step 2: Push the existing feature branch**

```bash
git push
```

Expected: `origin/agent/record-csdiy-wiki-option` advances to the local HEAD.

- [ ] **Step 3: Update Draft PR #1 title and description**

Create `/tmp/social-science-roadmap-pr-body.md` with this exact content using `apply_patch`:

```markdown
## What changed

- add CSDIY as an auxiliary reference for computing tools and self-study organization
- record explicit conditions for reconsidering a Wiki or knowledge site later
- add a political science and computational social science resource backlog with dated Star snapshots
- link the backlog from the repository README

## Why

The learning hub should remember promising future resources without expanding the active Stata Fundamentals path or downloading third-party materials prematurely.

## Validation

- refreshed repository metadata through the GitHub API on 2026-08-17
- checked Markdown with `git diff --check`
- verified the candidate links and README navigation entry
- confirmed the learner's untracked Stata exercise remains excluded from every commit
```

Run:

```bash
gh pr edit 1 \
  --repo Stchz666/social-science-self-study \
  --title "docs: expand the self-study resource roadmap" \
  --body-file /tmp/social-science-roadmap-pr-body.md
```

Expected: the command prints the PR URL and exits with status 0.

- [ ] **Step 4: Verify the published PR**

Run:

```bash
gh pr view 1 --repo Stchz666/social-science-self-study --json title,isDraft,state,headRefName,baseRefName,url
git status --short --branch
```

Expected: PR #1 is open and draft, targets `main`, uses `agent/record-csdiy-wiki-option`, and the only remaining local change is the untracked Stata do-file.
