# Andrew Architecture Core

## 定位

此 skill 保留所有 cross-domain 的 core 方法，不混進 API lifecycle、security policy、SLO 與運維治理等專屬領域內容。它適合在問題還太早、太廣、或還不適合直接套用 domain-specific skill 時，先把架構題收斂成穩定模型、資料與邊界設計，以及可驗證的 POC 與評估方式。

## 主流程

```text
+---------------------------+
| Problem Analysis          |
+---------------------------+
              |
              v
+---------------------------+
| Modeling                  |
+---------------------------+
              |
              v
+---------------------------+
| Data And Storage Design   |
+---------------------------+
              |
              v
+---------------------------+
| Class And Boundary Design |
+---------------------------+
              |
              v
+---------------------------+
| Scenario And Flow Mapping |
+---------------------------+
              |
              v
+---------------------------+
| Metrics And Theory Limits |
+---------------------------+
              |
              v
+---------------------------+
| POC                       |
+---------------------------+
              |
              v
+---------------------------+
| Evaluation                |
+---------------------------+
```

對應正式 skill 請見 [SKILL.md](SKILL.md)。

## 來源文章

這個 skill 的設計原則整理自 Andrew 過去發表的文章。若原文仍為草稿或尚未公開，會以未發佈文章標示。

- [[Azure] Multi-Tenancy Application #1, 設計概念](https://columns.chicken-house.net/2013/03/12/azure-multi-tenancy-application-1-design-concepts/), 2013-03-12
- [[Azure] Multi-Tenancy Application #2, 資料層的選擇](https://columns.chicken-house.net/2013/03/17/azure-multi-tenancy-application-2-data-layer-choices/), 2013-03-17
- [[Azure] Multi-Tenancy Application #3, (資料層)實作案例](https://columns.chicken-house.net/2013/03/21/azure-multi-tenancy-application-3-data-layer-implementation/), 2013-03-21
- [架構面試題 #3, RDBMS 處理樹狀結構的技巧](https://columns.chicken-house.net/2019/06/01/nested-query/), 2019-06-01
- 微服務架構設計 - 資料庫的選擇, RDBMS or NOSQL?, 2020-07-01 (未發佈文章)
- [[架構師的修練] #1, 刻意練習 - 打好基礎](https://columns.chicken-house.net/2021/03/01/practice-01/), 2021-03-01
- [架構師的修練] #3, 刻意練習 - 如何鍛鍊你的抽象化能力, 2023-04-01 (未發佈文章)
- 微服務架構設計 - Event Sourcing, 2020-01-01 (未發佈文章)
- [架構面試題 #4 - 抽象化設計；折扣規則的設計機制 (06/25 補完)](https://columns.chicken-house.net/2020/03/10/interview-abstraction/), 2020-03-10
- [處理大型資料的技巧 – Async / Await](https://columns.chicken-house.net/2013/04/15/large-data-processing-techniques-async-await/), 2013-04-15
- [後端工程師必備: CLI + PIPELINE 開發技巧](https://columns.chicken-house.net/2019/06/15/netcli-pipeline/), 2019-06-15
- [後端工程師必備: CLI 傳遞物件的處理技巧](https://columns.chicken-house.net/2019/06/20/netcli-tips/), 2019-06-20
- [[架構師的修練] - 從 DateTime 的 Mock 技巧談 PoC 的應用](https://columns.chicken-house.net/2022/05/29/datetime-mock/), 2022-05-29

## 參考資訊

- [interview-abstraction-principles.md](references/interview-abstraction-principles.md)
  這份參考整理的是抽象化設計最核心的判準：先抽出穩定關注點，再把變動細節藏到實作之後。它特別適合拿來檢查 contract、main flow 與 extension point 是否切在真正的痛點上。當你懷疑目前設計只是把案例硬分類，而不是形成穩定抽象時，應優先回頭看這份參考。
- [deliberate-practice-principles.md](references/deliberate-practice-principles.md)
  這份參考把能力培養本身也當成一個設計題，強調用可重跑的練習取代模糊的成長目標。它的重點是先定義 correctness、measurements 與 baseline，再逐步迭代設計能力。當任務焦點是如何練習架構思考、如何設計演練題、或如何找出知識缺口時，這份最有用。
- [time-mock-poc-principles.md](references/time-mock-poc-principles.md)
  這份參考說明只要時間會影響 correctness，時間就必須成為可控制的依賴，而不是隱藏背景條件。它強調 POC 要用 low-friction 的 controllable time，而不是靠 realtime waiting 或改系統時間。當設計涉及 schedule、expiry、timeout、delay 或 deterministic replay，應直接套用這份原則。
- [data-shape-and-storage-principles.md](references/data-shape-and-storage-principles.md)
  這份參考聚焦資料形狀、存取模式、tenant boundary 與 storage choice 之間的架構取捨。它提醒你不要抽象地問 RDBMS or NoSQL，而要從 dominant operations 與 hardest constraint 出發。當問題核心落在 schema、index、projection、materialization 或 multi-tenancy 設計時，這份是主參考。
- [pipeline-and-object-stream-principles.md](references/pipeline-and-object-stream-principles.md)
  這份參考整理 batch、stream、pipeline 三種思考模式的差異，特別適合 staged processing 類題目。它強調 stage contract、restartability、structured stream 與 first-result latency 等設計重點。當設計涉及多階段處理、CLI composition、物件流傳遞或 throughput/latency 取捨時，應先看這份。
- [event-sourcing-materialization-principles.md](references/event-sourcing-materialization-principles.md)
  這份參考聚焦 event history、projection、materialization 與 late/corrected data 的整體設計觀。它的核心不是把 event sourcing 當成流行名詞，而是界定何時需要以 change history 作為 source of truth。當題目涉及 replay、audit、correction、projection lag 或 event time 與 process time 的區分時，這份能補足判準。
