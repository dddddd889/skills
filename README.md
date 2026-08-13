# skills

个人 / 团队的 AI Agent 技能（Skill）仓库，遵循 [Agent Skills 开放规范](https://github.com/vercel-labs/skills)，可以通过 `npx skills add` 安装到 Claude Code、Codex 等支持该规范的 agent 中，也可以直接把 `skills/<name>` 目录复制或软链到对应 agent 的技能目录里使用。

## 目录结构

```
skills/
  business-application-modeling/ # 业务应用程序的活动图、用例图、类图与数据模式建模
    SKILL.md
  concept-explainer/    # 文档写作中讲解名词/概念
    SKILL.md
  deep-dive-learning/   # 技术深度调研 / 系统学习模板
    SKILL.md
```

## 已有技能

| 技能 | 说明 |
| --- | --- |
| `business-application-modeling` | 从现实业务活动出发，依次用活动图、用例图、系统活动图和类图定义系统职责、信息结构及关系型数据库模式 |
| `concept-explainer` | 写文档遇到名词/概念时，优先用时序图、架构图、穷尽场景路径讲清楚定位，其次才用文字 + 具体场景补充 |
| `deep-dive-learning` | 系统调研一项技术时，按"背景与目的 → 优劣权衡 → 使用场景 → 组成与关键点 → 底层原理 → 对比"六步展开，并做联想 / 抽象 / 自省与归纳总结 |

## 安装方式

```bash
# 安装整个仓库的所有技能
npx skills add <你的github>/skills --all

# 只安装某一个技能
npx skills add <你的github>/skills --skill concept-explainer

# 指定目标 agent（可多选）
npx skills add <你的github>/skills --skill deep-dive-learning -a claude-code -a codex
```

## 新增技能

1. 在 `skills/` 下新建一个目录，目录名即技能名（小写 + 连字符）。
2. 目录下创建 `SKILL.md`，文件头部必须包含 `name` 和 `description` 两个 YAML frontmatter 字段。
3. 正文用清晰的步骤 / 模板描述 agent 该怎么做。
