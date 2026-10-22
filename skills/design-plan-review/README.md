# 方案与计划审查

审查已有方案和落地计划，分两步循环执行：

- **反复扫描对齐**：比较当前文档、上下文和上下游，解决冲突、矛盾、约定不一致。
- **Agent 对抗补漏**：A 推演设计并回应质疑，B 找反例并持续追问，发现设计遗漏。

主 Agent 组织审查、汇总问题和统一修订，不从零生成方案和计划。具体执行规则见 [SKILL.md](SKILL.md)。

## 流程图

```mermaid
graph TD;
    input["输入已有方案、计划、上下文及上下游文档"];
    scan["主 Agent 完整扫描当前文档、上下文和上下游"];
    conflict{"存在冲突、矛盾或约定未对齐？"};
    align["主 Agent 统一修正不一致"];
    call["主 Agent 每轮重新调用 A、B，提供同一最新版本"];
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

## A、B 的配置

- A：[`design_plan_proponent`](agents/design-plan-proponent.toml)，推演业务闭环，回应质疑。
- B：[`design_plan_challenger`](agents/design-plan-challenger.toml)，挑战假设，找反例和遗漏。

这两个 TOML 文件是原生 Codex Agent 定义。`agents/openai.yaml` 是技能展示配置。项目安装和实际调用方式见 [SKILL.md 的子 Agent 说明](SKILL.md#codex-子-agent-定义与调用)。
