# skills

个人 / 团队的 AI Agent 技能（Skill）仓库，遵循 [Agent Skills 开放规范](https://github.com/vercel-labs/skills)，可以通过 `npx skills add` 安装到 Claude Code、Codex 等支持该规范的 agent 中，也可以直接把 `skills/<name>` 目录复制或软链到对应 agent 的技能目录里使用。

## 目录结构

```
skills/
  business-application-modeling/ # 业务应用程序的分析、需求定义与面向对象设计
    SKILL.md
  concept-explainer/    # 文档写作中讲解名词/概念
    SKILL.md
  deep-dive-learning/   # 技术深度调研 / 系统学习模板
    SKILL.md
  design-plan-review/   # 反复扫描对齐文档，Agent 对抗查找设计遗漏
    README.md          # 流程图、结束条件及 Agent 配置入口
    SKILL.md
    agents/            # 技能展示信息，以及主动调用 A、B 时传入的角色指令
  progressive-learning-coach/ # 从陌生破冰到能够独立使用一项技能
    SKILL.md
  work-with-understanding/ # 边做边理解、任务记录与主动复盘
    SKILL.md
```

## 已有技能

| 技能 | 说明 |
| --- | --- |
| `business-application-modeling` | 从现实业务活动出发，完成需求与信息建模，再定义运行环境、软件整体结构、构件接口和数据库模式 |
| `concept-explainer` | 写文档遇到名词/概念时，优先用时序图、架构图、穷尽场景路径讲清楚定位，其次才用文字 + 具体场景补充 |
| `deep-dive-learning` | 系统调研一项技术时，按"背景与目的 → 优劣权衡 → 使用场景 → 组成与关键点 → 底层原理 → 对比"六步展开，并做联想 / 抽象 / 自省与归纳总结 |
| [design-plan-review](skills/design-plan-review/README.md) | 审查已有方案和落地计划：先反复扫描当前文档、上下文和上下游以解决矛盾，再由两个 Agent 对抗补漏；修订后重复，直到对齐且无新遗漏 |
| `progressive-learning-coach` | 通过破冰讲解、示范模仿、刻意练习和迁移验证，把一项陌生技能逐步学到能够独立使用 |
| `work-with-understanding` | 从任务开始按情况澄清、比较方案、执行和检查理解，沉淀任务记录，并复盘用户指定的 1～2 件事 |

## 安装方式

```bash
# 安装整个仓库的所有技能
npx skills add <你的github>/skills --all

# 只安装某一个技能
npx skills add <你的github>/skills --skill concept-explainer

# 指定目标 agent（可多选）
npx skills add <你的github>/skills --skill deep-dive-learning -a claude-code -a codex
```

`design-plan-review` 安装后，由主 Agent 读取技能附带的 A、B 完整角色指令并主动创建两个真实子 Agent，不需要另行注册或复制配置：

```bash
npx skills add dddddd889/skills --skill design-plan-review --agent codex
```

## 新增技能

1. 在 `skills/` 下新建一个目录，目录名即技能名（小写 + 连字符）。
2. 目录下创建 `SKILL.md`，文件头部必须包含 `name` 和 `description` 两个 YAML frontmatter 字段。
3. 正文用清晰的步骤 / 模板描述 agent 该怎么做。
