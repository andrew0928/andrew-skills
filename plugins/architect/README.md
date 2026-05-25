# architect

Claude Code plugin：架構設計 skills。內容整理自 Andrew 過去公開發表的文章與案例，原始文章可見 [https://columns.chicken-house.net](https://columns.chicken-house.net)。

## 安裝

```bash
/plugin marketplace add andrew0928/andrew-skills
/plugin install architect@andrew-skills
```

## Skills

| Skill | 說明 |
|-------|------|
| [architecture-core](skills/architecture-core/README.md) | 保留跨領域架構題的核心方法，先處理問題定義、建模、資料與邊界設計，再進入可量測的 POC 與評估。 |
| [api-distributed-design](skills/api-distributed-design/README.md) | 從 domain lifecycle 與 state machine 出發，設計 API、message、worker 與 scheduler 的契約、correctness 與驗證流程。 |
| [security-permission-design](skills/security-permission-design/README.md) | 從 trust boundary、identity、authorization 到 token、enforcement 與 permission management，建立完整安全模型。 |
| [service-reliability-design](skills/service-reliability-design/README.md) | 從 service promise、SLO/SLI、bottleneck 與 admission control 出發，設計可靠度、queue、公平性與 observability。 |
| [microservice-architecture](skills/microservice-architecture/README.md) | 判斷 microservices 是否適合、如何切 boundary、如何分階段遷移，以及平台、runtime 與 delivery baseline 應如何規劃。 |

## 結構

```text
plugins/architect/
  .claude-plugin/
    plugin.json
  skills/
    <skill-name>/
      README.md
      SKILL.md
      agents/
        openai.yaml
        overview.yaml
      references/
```

## 設計原則

- `SKILL.md` 保留會影響 agent 執行的正式內容。
- `agents/overview.yaml` 保留給人類讀者與其他工具的摘要資訊。
- `README.md` 負責快速導覽，不影響 skill 執行。
- `references/` 保留文章脈絡與補充原則，避免把所有細節塞回主 skill。
