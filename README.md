# Andrew Architect Skills

這個 repo 收錄 Andrew 的架構設計 skills，讓 repo 本身就是可閱讀、可安裝、可持續維護的 skills package。

這些 skills 的內容，整理自 Andrew 過去公開發表的文章與案例，原始文章可見：

- [https://columns.chicken-house.net](https://columns.chicken-house.net)

目前 repo 以 `Codex` 與 `Claude Code` 的技能格式為主，保留標準的 `skills/<skill>/SKILL.md` 結構，同時補上面向人類讀者的 `README.md` 與 `agents/overview.yaml`，方便快速挑選合適的 skill。

## 安裝

### Claude Code

將本 repo 的內容放到專案根目錄下的 `.claude/`，使 skill 路徑成為：

```text
.claude/
  skills/
    andrew-architecture-core/
    andrew-api-distributed-design/
    ...
```

### Codex

將本 repo 的 `skills/` 目錄複製到 `~/.codex/skills/`，使 skill 路徑成為：

```text
~/.codex/skills/
  andrew-architecture-core/
  andrew-api-distributed-design/
  ...
```

## Skills

| Skill | 說明 |
|-------|------|
| [andrew-architecture-core](skills/andrew-architecture-core/README.md) | 保留跨領域架構題的核心方法，先處理問題定義、建模、資料與邊界設計，再進入可量測的 POC 與評估。 |
| [andrew-api-distributed-design](skills/andrew-api-distributed-design/README.md) | 從 domain lifecycle 與 state machine 出發，設計 API、message、worker 與 scheduler 的契約、correctness 與驗證流程。 |
| [andrew-security-permission-design](skills/andrew-security-permission-design/README.md) | 從 trust boundary、identity、authorization 到 token、enforcement 與 permission management，建立完整安全模型。 |
| [andrew-service-reliability-design](skills/andrew-service-reliability-design/README.md) | 從 service promise、SLO/SLI、bottleneck 與 admission control 出發，設計可靠度、queue、公平性與 observability。 |
| [andrew-microservice-architecture](skills/andrew-microservice-architecture/README.md) | 判斷 microservices 是否適合、如何切 boundary、如何分階段遷移，以及平台、runtime 與 delivery baseline 應如何規劃。 |

## Repo 結構

```text
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
