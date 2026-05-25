# Andrew Skills

這個 repo 是 Andrew 的 Claude Code skills marketplace，收錄一系列以 Andrew 過去公開發表的文章與案例整理而成的 skills。

目前已收錄的 plugin：

- **architect** — 5 個架構設計 skills（架構核心、API 與分散式、安全與權限、服務可靠度、微服務）。

未來會在同一個 marketplace 下持續加入其他主題的 plugins。

原始文章可見：[https://columns.chicken-house.net](https://columns.chicken-house.net)

## 安裝

### Claude Code

```bash
/plugin marketplace add andrew0928/andrew-skills
/plugin install architect@andrew-skills
```

### Codex

將 `plugins/architect/skills/` 底下的 skill 目錄複製到 `~/.codex/skills/`，使 skill 路徑成為：

```text
~/.codex/skills/
  andrew-architecture-core/
  andrew-api-distributed-design/
  ...
```

## Plugins

| Plugin | 說明 |
|--------|------|
| [architect](plugins/architect/README.md) | 5 個架構設計 skills，涵蓋架構核心、API 與分散式、安全與權限、服務可靠度、微服務。 |

## Repo 結構

```text
.claude-plugin/
  marketplace.json          # marketplace 中繼資料
plugins/
  architect/
    .claude-plugin/
      plugin.json           # plugin 中繼資料
    skills/
      <skill-name>/
        README.md
        SKILL.md
        agents/
        references/
```

## 設計原則

- `SKILL.md` 保留會影響 agent 執行的正式內容。
- `agents/overview.yaml` 保留給人類讀者與其他工具的摘要資訊。
- `README.md` 負責快速導覽，不影響 skill 執行。
- `references/` 保留文章脈絡與補充原則，避免把所有細節塞回主 skill。

## 授權

除非另有註明，本 repo 內容採用 [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/) 授權條款釋出。

- 使用者可重製、散布、改作，並可商業使用
- 使用時需保留出處、附上授權連結，並標示是否有修改
- 詳細條款請見 [LICENSE.md](LICENSE.md)
