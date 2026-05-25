# Andrew API Distributed Design

## 定位

此 skill 聚焦在 API 契約與 distributed workflow 的設計，不混進微服務平台治理、security policy、permission model、SLO 與整體營運治理等專屬領域內容。它的定位是把 domain lifecycle、message flow、retry 與 worker 協作收斂成一套可設計、可驗證、可衡量的 distributed contract 方法。

## 主流程

```text
+--------------------------------------+
| Problem Analysis                     |
+--------------------------------------+
                   |
                   v
+--------------------------------------+
| Domain And Interaction Modeling      |
+--------------------------------------+
                   |
                   v
+--------------------------------------+
| Contract Surfaces                    |
+--------------------------------------+
                   |
                   v
+--------------------------------------+
| State Machine And Delivery Semantics |
+--------------------------------------+
                   |
                   v
+--------------------------------------+
| Correctness And Coordination         |
+--------------------------------------+
                   |
                   v
+--------------------------------------+
| Worker And Runtime Topology          |
+--------------------------------------+
                   |
                   v
+--------------------------------------+
| Scenario Mapping                     |
+--------------------------------------+
                   |
                   v
+--------------------------------------+
| Metrics                              |
+--------------------------------------+
                   |
                   v
+--------------------------------------+
| POC                                  |
+--------------------------------------+
                   |
                   v
+--------------------------------------+
| Evaluation                           |
+--------------------------------------+
```

對應正式 skill 請見 [SKILL.md](SKILL.md)。

## 來源文章

這個 skill 的設計原則整理自 Andrew 過去發表的文章。若原文仍為草稿或尚未公開，會以未發佈文章標示。

- [架構師觀點 - API First 的開發策略](https://columns.chicken-house.net/2022/10/26/apifirst/), 2022-10-26
- [微服務架構 - 從狀態圖來驅動 API 的設計](https://columns.chicken-house.net/2022/03/25/microservices15-api-design/), 2022-03-25
- [微服務架構 - 從狀態圖來驅動 API 的實作範例](https://columns.chicken-house.net/2022/04/25/microservices16-api-implement/), 2022-04-25
- [架構師觀點 - API Design Workshop](https://columns.chicken-house.net/2023/01/01/api-design-workshop/), 2023-01-01
- [架構面試題 #1, 線上交易的正確性](https://columns.chicken-house.net/2018/03/25/interview01-transaction/), 2018-03-25
- [架構面試題 #2, 連續資料的統計方式](https://columns.chicken-house.net/2018/04/01/interview02-stream-statistic/), 2018-04-01
- [分散式系統 #1] Idempotency Key 的原理與實作 - 能安全 Retry 的 API 設計, 2021-03-15 (未發佈文章)
- [高可靠度的微服務通訊 - Message Queue](https://columns.chicken-house.net/2019/01/01/microservice12-mqrpc/), 2019-01-01
- [處理大型資料的技巧 – Async / Await](https://columns.chicken-house.net/2013/04/15/large-data-processing-techniques-async-await/), 2013-04-15
- [後端工程師必備: 平行任務處理的思考練習 (0916補完)](https://columns.chicken-house.net/2019/07/06/pipeline-practices/), 2019-07-06
- [後端工程師必備: 排程任務的處理機制練習 (12/01 補完)](https://columns.chicken-house.net/2019/08/30/scheduling-practices/), 2019-08-30
- [架構面試題 #5: Re-Order Messages](https://columns.chicken-house.net/2023/10/01/reorder/), 2023-10-01
- [微服務基礎建設: Process Pool 的設計與應用](https://columns.chicken-house.net/2020/02/09/process-pool/), 2020-02-09

## 參考資訊

- [api-first-strategy-principles.md](references/api-first-strategy-principles.md)
  這份參考聚焦 API First 的出發點：當介面本身是長期、共享、跨團隊的資產時，契約必須先於實作。它適合用來提醒設計者不要把 API 當成某個現有 UI flow 的包裝，而要把它視為 domain service 的外顯形式。當你要先做 contract review、mock、spec 驗證，或判斷最小 API surface 該長什麼樣子時，應優先看這份。
- [api-state-machine-principles.md](references/api-state-machine-principles.md)
  這份參考整理的是 Andrew 式 API 設計的核心骨架：先畫 primary subject 的 state machine，再從 transition 反推出 action、event 與 authorization。它特別適合處理 lifecycle-driven API、state/property 區分、contract extraction 與 thin controller 的分層設計。當你想驗證 API 命名、狀態轉移合法性與 scenario mapping 是否一致，這份就是主參考。
- [distributed-correctness-principles.md](references/distributed-correctness-principles.md)
  這份參考聚焦 distributed correctness 的底層判準：先定義 invariant，再決定 critical section 應由哪一層機制保護。它把 transaction correctness、idempotent retry、rolling statistic 與 late-arrival interpretation 收斂成同一套思考框架。當題目涉及 money-like operation、dedupe、retry、distributed lock 或 O(1) aggregation 設計時，應先看這份。
- [messaging-and-operation-principles.md](references/messaging-and-operation-principles.md)
  這份參考聚焦 message queue 不只用於 fire-and-forget，也可支撐 RPC、reply routing 與 cross-service context propagation。它很適合拿來規劃 message envelope、correlation id、worker abstraction 與 graceful shutdown 等 operability 細節。當你要把 broker complexity 從業務 handler 中切出去，或設計 DevOps-ready 的 messaging runtime 時，這份會很有幫助。
- [pipeline-scheduling-principles.md](references/pipeline-scheduling-principles.md)
  這份參考把 pipeline、scheduler、reorder 與 timing window 類問題收斂到同一套 metrics-driven evaluation 方法。它特別強調 first-result、last-completion、delay variance、polling cost、duplicate execution 與 theory limit 的量測。當你要比較不同 scheduling 參數、處理 reorder buffer、或驗證 multi-instance scheduler 的正確性時，應先讀這份。
- [worker-isolation-principles.md](references/worker-isolation-principles.md)
  這份參考聚焦 worker isolation 是一個成本與 blast radius 的架構選擇，而不是單純的 runtime 偏好。它會幫你比較 in-process、thread、process 與 infrastructure orchestration 的隔離能力與啟動成本。當你要決定任務單位該由哪一層執行、是否需要 custom runtime、或 process pool 是否比 thread pool 更合理時，這份最直接。
