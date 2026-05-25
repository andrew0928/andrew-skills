# Andrew Service Reliability Design

## 定位

此 skill 聚焦在 service reliability 與 quality control 的設計，不混進 API lifecycle、security policy、permission model 與微服務平台治理等其他專屬領域內容。它的定位是從 service promise、SLO/SLI、bottleneck 與 workload control 出發，建立一套可設計、可監控、可營運的服務品質保證方法。

## 主流程

```text
+-----------------------------------+
| Problem Analysis                  |
+-----------------------------------+
                 |
                 v
+-----------------------------------+
| Service Objective Model           |
+-----------------------------------+
                 |
                 v
+-----------------------------------+
| Bottleneck And Workload Model     |
+-----------------------------------+
                 |
                 v
+-----------------------------------+
| Capacity Control And Admission    |
+-----------------------------------+
                 |
                 v
+-----------------------------------+
| Queue And Lineup Design           |
+-----------------------------------+
                 |
                 v
+-----------------------------------+
| Observability And Metrics         |
+-----------------------------------+
                 |
                 v
+-----------------------------------+
| Operational Controls And Response |
+-----------------------------------+
                 |
                 v
+-----------------------------------+
| POC                               |
+-----------------------------------+
                 |
                 v
+-----------------------------------+
| Evaluation                        |
+-----------------------------------+
```

對應正式 skill 請見 [SKILL.md](SKILL.md)。

## 來源文章

這個 skill 的設計原則整理自 Andrew 過去發表的文章。若原文仍為草稿或尚未公開，會以未發佈文章標示。

- [微服務基礎建設 - 線上購物排隊機制設計](https://columns.chicken-house.net/2018/12/12/microservice11-lineup/), 2018-12-12
- [[架構師的修練] #2, SLO - 如何確保服務水準? ](https://columns.chicken-house.net/2021/06/04/slo/), 2021-06-04
- [微服務基礎建設: 斷路器 #1, 服務負載的控制](https://columns.chicken-house.net/2018/06/10/microservice10-throttle/), 2018-06-10

## 參考資訊

- [slo-and-toc-principles.md](references/slo-and-toc-principles.md)
  這份參考聚焦 service promise、SLO、SLI 與 TOC 之間的整體設計關係，是 reliability domain 的理論主幹。它特別適合處理目標拆解、bottleneck diagnosis、workload separation 與 upstream control 的策略判斷。當你要定義何謂達標、如何量測、何時該保護瓶頸、以及何時要拒絕註定失敗的流量時，這份最重要。
- [throttle-and-qos-principles.md](references/throttle-and-qos-principles.md)
  這份參考聚焦 throttling 與 QoS，不只問 how to limit，而是先問 service amount 該怎麼定義與量測。它會幫你拆清楚 admission control 的兩個核心問題：怎麼量化負載，以及超限後該採取什麼動作。當設計涉及 rate limit、reject/defer/queue、capacity reservation 或 burst control 時，應優先看這份。
- [lineup-and-queue-fairness-principles.md](references/lineup-and-queue-fairness-principles.md)
  這份參考聚焦 queue/lineup 不只保護系統，也要維持可解釋的公平性與使用者體驗。它強調 queue semantics、user feedback、operator control、abandonment handling 與 O(1)-style status query。當題目涉及 waiting room、position/ETA、公平性、manual removal 或 queue state metrics 時，這份最直接。
