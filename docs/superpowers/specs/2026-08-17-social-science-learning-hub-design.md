# 社会科学自学中枢设计

## 目标

把当前目录建设为经济学、政治学和 Stata 自学的长期中枢。成熟课程仓库作为本地只读参考材料；学习规划、进度、日志、练习和独立成果由本仓库持续记录并发布到 GitHub。

## 仓库边界

- 根仓库：保存学习管理文件和学习者原创成果。
- `upstream/`：保存从 GitHub 下载的成熟课程仓库，每个课程保留自身的 Git 历史；根仓库通过 `.gitignore` 忽略该目录。
- `exercises/`：保存学习者完成的练习、解释和重写代码。
- `projects/`：保存能够逐渐独立发布的研究或复现项目。
- `learning-logs/`：按日期记录每次学习的内容、证据、困难和下一步。

## 持续协作

`AGENTS.md` 规定 Codex 每次开始前读取 `LEARNING_PLAN.md` 和 `PROGRESS.md`，把 `upstream/` 视为只读材料，并在学习会话结束时维护进度和日志。`PROGRESS.md` 是跨会话的当前状态来源，聊天上下文仅作辅助。

## GitHub 工作流

根仓库发布为 `Stchz666/social-science-self-study`。首次提交直接建立 `main`；后续重要修改使用主题分支。学习过程以小而明确的提交保存，例如完成一课、补充一份概念说明或完成一次复现。

## 第一阶段材料

第一份课程材料为 `dlab-berkeley/Stata-Fundamentals`。初期直接 clone 原仓库到 `upstream/Stata-Fundamentals`，先运行和学习；确认需要在个人 GitHub 上长期修改时再 fork。`SOURCES.md` 记录仓库 URL、本地位置、用途、许可证提示和本地所基于的 commit。

## 验收标准

- 根仓库包含清晰的入口、计划、进度、来源登记和协作规则。
- `upstream/` 不进入根仓库的提交历史。
- Stata Fundamentals 已下载且 commit 可追溯。
- 所有 Markdown 内部链接和关键路径可验证。
- 本地 `main` 与 GitHub 远程仓库建立跟踪关系。
