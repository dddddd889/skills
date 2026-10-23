# 方案与计划审查

审查已有方案和落地计划，分两步循环执行：

- **反复扫描对齐**：比较当前文档、上下文和上下游，解决冲突、矛盾、约定不一致。
- **Agent 对抗补漏**：A 推演设计并回应质疑，B 找反例并持续追问，发现设计遗漏。

主 Agent 组织审查、汇总问题和统一修订，不从零生成方案和计划。具体执行规则见 [SKILL.md](SKILL.md)。

## 安装与使用

在目标项目根目录执行：

```bash
npx skills add dddddd889/skills --skill design-plan-review --agent codex
```

安装后即可使用，无需手动复制 A、B 配置。给 Codex 以下请求，主 Agent 会先扫描，再主动创建并调用两个真实子 Agent：

```text
$design-plan-review
审查以下已有方案和落地计划：……
相关需求、上下文和上下游文档：……
```

## 流程图

```mermaid
graph TD;
    input["输入已有方案、计划、上下文及上下游文档"];
    scan["主 Agent 完整扫描当前文档、上下文和上下游"];
    conflict{"存在冲突、矛盾或约定未对齐？"};
    align["主 Agent 统一修正不一致"];
    call["主 Agent 主动创建或重新调用 A、B，提供同一最新版本"];
    debate["A、B 先独立审查，再相互质疑：B 提反例，A 回应，B 复核"];
    omission{"仍有有效遗漏或待确认问题？"};
    patch["主 Agent 补充文档；缺少依据时先补齐信息或确认决策"];
    finish["结束：已知问题已解决，完整扫描无冲突，随后对抗无新遗漏"];

    input --> scan;
    scan --> conflict;
    conflict -->|"有"| align;
    align -->|"再次完整扫描"| scan;
    conflict -->|"没有"| call;
    call --> debate;
    debate --> omission;
    omission -->|"有"| patch;
    patch -->|"补充后可能引入矛盾，重新扫描"| scan;
    omission -->|"没有"| finish;
```

每次补充后，都先重新完整扫描，再重新调用 A、B 对抗，不能只让发现问题的一方检查修复位置。可以复用原 Agent，但必须重新读取和审查最新材料。

结束前必须同时满足：已确认问题全部解决并复核；最新版本完整扫描无冲突；随后 A、B 实际完成质疑、回应和复核，未发现新有效遗漏。缺少材料、决策或真实 Agent 回执时，不能报告通过。

## A、B 的角色指令

- A：[推演业务闭环，回应质疑](agents/design-plan-proponent.toml)。
- B：[挑战假设，找反例和遗漏](agents/design-plan-challenger.toml)。

主 Agent 读取这两个文件的完整 `developer_instructions`，传给动态创建的通用子 Agent。不依赖已注册的原生角色，不修改 `.codex/agents/` 或全局配置。实际调用方式见 [SKILL.md](SKILL.md#主动创建并调用-ab)。
