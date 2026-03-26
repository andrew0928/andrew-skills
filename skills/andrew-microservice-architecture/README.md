# Andrew Microservice Architecture

## 定位

此 skill 聚焦在整體 microservice architecture 與 migration 的規劃，不混進單一 API 契約、security policy、permission model 或 SLO 控制細節。它的定位是回答「是否該做微服務」、「要怎麼切」、「要怎麼分階段遷移」，以及「平台、runtime、交付流程要準備到什麼程度」。

## 主流程

```text
+----------------------------------+
| Problem Analysis                 |
+----------------------------------+
                |
                v
+----------------------------------+
| Microservice Fit                 |
+----------------------------------+
                |
                v
+----------------------------------+
| Service Boundaries               |
+----------------------------------+
                |
                v
+----------------------------------+
| Migration Strategy               |
+----------------------------------+
                |
                v
+----------------------------------+
| Platform Capabilities            |
+----------------------------------+
                |
                v
+----------------------------------+
| Runtime And Hosting Model        |
+----------------------------------+
                |
                v
+----------------------------------+
| Delivery And Operability Model   |
+----------------------------------+
                |
                v
+----------------------------------+
| POC                              |
+----------------------------------+
                |
                v
+----------------------------------+
| Evaluation                       |
+----------------------------------+
```

對應正式 skill 請見 [SKILL.md](SKILL.md)。

## 來源文章

這個 skill 的設計原則整理自 Andrew 過去發表的文章。若原文仍為草稿或尚未公開，會以未發佈文章標示。

- [容器化的微服務開發 #1, IP查詢架構與開發範例](https://columns.chicken-house.net/2017/05/28/aspnet-msa-labs1/), 2017-05-28
- [容器化的微服務開發 #2, IIS or Self Host ?](https://columns.chicken-house.net/2018/05/12/msa-labs2-selfhost/), 2018-05-12
- [Blogging as code !!](https://columns.chicken-house.net/2016/09/16/blog-as-code/), 2016-09-16
- [架構師觀點: 你需要什麼樣的 CI / CD ?](https://columns.chicken-house.net/2017/08/05/what-cicd-do-you-need/), 2017-08-05
- [微服務架構 #2, 按照架構，重構系統](https://columns.chicken-house.net/2016/10/03/microservice2/), 2016-10-03
- [架構師觀點 - 轉移到微服務架構的經驗分享 (Part 2)](https://columns.chicken-house.net/2017/05/20/microservice8-case-study-p2/), 2017-05-20
- [微服務架構 #1, WHY Microservices?](https://columns.chicken-house.net/2016/09/15/microservice-case-study-01/), 2016-09-15
- [架構師觀點 - 轉移到微服務架構的經驗分享 (Part 1)](https://columns.chicken-house.net/2017/04/15/microservice8-case-study/), 2017-04-15
- [架構師觀點 - 轉移到微服務架構的經驗分享 (Part 3)](https://columns.chicken-house.net/2017/07/11/microservice8-case-study-p3/), 2017-07-11
- [微服務基礎建設 - Service Discovery](https://columns.chicken-house.net/2017/12/31/microservice9-servicediscovery/), 2017-12-31
- DevOpsDays 專刊: Service Discovery, 微服務架構的基礎建設, 2018-10-10 (未發佈文章)

## 參考資訊

- [microservice-fit-and-boundary-principles.md](references/microservice-fit-and-boundary-principles.md)
  這份參考聚焦最根本的問題：微服務是不是當下真的適合，以及 boundary 應該沿著什麼脈絡來切。它會幫你從 business flow、organizational ownership、technical heterogeneity 與 over-splitting risk 來看整體架構。當你還在判斷是否該拆、該怎麼切、以及團隊是否已具備門票時，這份最值得先讀。
- [microservice-evolution-and-build-vs-buy-principles.md](references/microservice-evolution-and-build-vs-buy-principles.md)
  這份參考聚焦 staged evolution：先重構、再模組化、再服務化，而不是直接 rewrite-from-scratch。它同時整理了 transitional glue code、incremental extraction 與 build-vs-buy 的判準。當題目涉及 monolith 漸進拆分、取代舊系統、引進成熟外部服務或評估 custom build 是否值得時，應優先看這份。
- [microservice-platform-and-discovery-principles.md](references/microservice-platform-and-discovery-principles.md)
  這份參考聚焦微服務不是只靠 service code 就能成立，還必須有 API gateway、service discovery、messaging 與 config management 等共享能力。它會幫你區分 registry、query、health signal、metadata/tag 與 client-side/server-side discovery 的設計差異。當你要規劃平台 baseline、internal routing、service metadata 或選擇 discovery pattern 時，這份最有幫助。
- [container-driven-runtime-principles.md](references/container-driven-runtime-principles.md)
  這份參考聚焦 container-driven runtime design，提醒你 service 往往不只一個 web endpoint，而是包含 worker、scheduler、proxy、SDK 等角色。它很適合處理 one-process-per-container、self-host vs IIS-style host、lifecycle control 與 runtime composition 這些題目。當你在決定 container 內部的執行模型、啟停方式與 health/deregistration 邏輯時，應先看這份。
- [delivery-and-system-as-code-principles.md](references/delivery-and-system-as-code-principles.md)
  這份參考聚焦 delivery model 與 system-as-code，強調 source control、CI、artifact、release management 應先形成最小可靠基線。它也把 blog-as-code 這類經驗收斂成更通用的判準：能在 build time 決定的東西，就不要硬留成 runtime system。當題目涉及 CI/CD baseline、artifact trust chain、registry/package feed、static generation 或 deployment definition as code 時，這份最直接。
