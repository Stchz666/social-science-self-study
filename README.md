# 社会科学自学中枢

这是我的经济学、政治学、计量方法和 Stata 自学中枢。仓库保存学习计划、进度、日志、练习和逐渐成熟的独立项目；成熟课程仓库保留为本地参考材料，并通过来源清单追踪版本。

## 当前主线

- 课程：[UC Berkeley D-Lab Stata Fundamentals](https://github.com/dlab-berkeley/Stata-Fundamentals)
- 当前阶段：Part 1 — Introduction
- 当前状态：材料准备完成，等待首次正式学习会话
- 进度详情：[PROGRESS.md](PROGRESS.md)

## 仓库导航

| 路径 | 用途 |
| --- | --- |
| [LEARNING_PLAN.md](LEARNING_PLAN.md) | 学习目标、阶段安排和验收标准 |
| [PROGRESS.md](PROGRESS.md) | 当前状态、已完成内容、困难和下一步 |
| [SOURCES.md](SOURCES.md) | 外部课程、数据、许可证和版本来源 |
| [learning-logs/](learning-logs/) | 每次学习会话的日期化记录 |
| [exercises/](exercises/) | 自己完成的练习、解释和重写代码 |
| [projects/](projects/) | 可以逐步发展为独立仓库的成果 |
| `upstream/` | 本地课程仓库；根仓库忽略，不公开复制 |

## 每次学习的基本循环

1. 阅读 `PROGRESS.md` 的“下一步”。
2. 从 `upstream/` 中选择本次课程材料。
3. 在 `exercises/` 中独立完成练习，保留运行证据。
4. 用自己的话解释概念、命令和结果。
5. 更新 `PROGRESS.md`，并在 `learning-logs/` 新建当日记录。
6. 将一个明确的学习成果提交到 Git。

推荐的提交信息：

```text
learn(stata): complete fundamentals lesson 01
notes(qss): summarize causality chapter
reproduce(did): regenerate figure 2
plan: update September learning schedule
```

## 在新电脑上恢复材料

根仓库不重新发布第三方课程文件。按照 [SOURCES.md](SOURCES.md) 中的地址，把课程仓库重新 clone 到 `upstream/`：

```bash
git clone https://github.com/dlab-berkeley/Stata-Fundamentals.git upstream/Stata-Fundamentals
```

完成后可用 `git -C upstream/Stata-Fundamentals rev-parse HEAD` 核对版本。

## 公开原则

- 只公开有权传播的数据和材料。
- 引用外部代码、数据或文字时记录来源和许可证。
- 不提交密码、令牌、Stata 许可证、受限数据或未经授权的教材文件。
- `upstream/` 主要用于阅读与运行；原创练习和扩展放入本仓库。
