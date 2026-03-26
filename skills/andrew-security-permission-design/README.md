# Andrew Security Permission Design

## 定位

此 skill 聚焦在 security 與 permission 的設計，不混進 API lifecycle、distributed workflow、SLO、微服務平台治理等其他專屬領域內容。它的定位是先釐清 trust boundary，再把 authentication、authorization、credential、enforcement 與 permission management 收斂成一套可設計、可驗證、可營運的安全模型。

## 主流程

```text
+------------------------------------+
| Problem Analysis                   |
+------------------------------------+
                |
                v
+------------------------------------+
| Trust Boundary And Threat Model    |
+------------------------------------+
                |
                v
+------------------------------------+
| Identity And Authentication        |
+------------------------------------+
                |
                v
+------------------------------------+
| Authorization Model                |
+------------------------------------+
                |
                v
+------------------------------------+
| Token, Key, And Credential Design  |
+------------------------------------+
                |
                v
+------------------------------------+
| Enforcement Boundaries             |
+------------------------------------+
                |
                v
+------------------------------------+
| Permission Management And Scaling  |
+------------------------------------+
                |
                v
+------------------------------------+
| Operational Controls And Audit     |
+------------------------------------+
                |
                v
+------------------------------------+
| POC                                |
+------------------------------------+
                |
                v
+------------------------------------+
| Evaluation                         |
+------------------------------------+
```

對應正式 skill 請見 [SKILL.md](SKILL.md)。

## 來源文章

這個 skill 的設計原則整理自 Andrew 過去發表的文章。若原文仍為草稿或尚未公開，會以未發佈文章標示。

- 微服務架構 - API 的安全管控模型, 2022-07-15 (未發佈文章)
- [[設計案例] \"授權碼\" 如何實作? #1, 需求與問題](https://columns.chicken-house.net/2016/02/17/casestudy_license_01_requirement/), 2016-02-17
- [[設計案例] 授權碼 如何實作?  #2, 序列化](https://columns.chicken-house.net/2016/02/24/casestudy_license_02_serialization/), 2016-02-24
- [[設計案例]  授權碼 如何實作?  #3, 數位簽章](https://columns.chicken-house.net/2016/02/24/casestudy_license_03_digital_signature/), 2016-02-24
- [[設計案例] 授權碼 如何實作? #3 (補) - 金鑰的保護](https://columns.chicken-house.net/2016/03/19/casestudy_license_03_appendix_key_management/), 2016-03-19
- [微服務架構 #4, 如何強化微服務的安全性? API Token / JWT 的應用](https://columns.chicken-house.net/2016/12/01/microservice7-apitoken/), 2016-12-01
- xxxxx 架構面試題 #6: 權限管理機制的設計, 2024-05-01 (未發佈文章)
- [[架構師觀點] 資安沒有捷徑，請從根本做起!](https://columns.chicken-house.net/2020/11/23/security-talk/), 2020-11-23

## 參考資訊

- [credential-and-signature-principles.md](references/credential-and-signature-principles.md)
  這份參考聚焦 token、license、digital signature 與 key management 的核心設計原則。它會幫你區分 readable payload 與 authenticity proof、offline verification、replay defense 與 trust-anchor 保護。當題目涉及 signed token、API token、client binding、private key 保護或 public key 發佈時，這份是主參考。
- [security-by-design-principles.md](references/security-by-design-principles.md)
  這份參考把 security 視為 quality requirement，而不是功能列表中的附加選項。它的重點是標準機制優先、集中 enforcement、縮小 exposed surface，以及不要把 UI visibility 當成 authorization。當你需要建立安全設計的基本立場，或要說明為何某些問題不能留到事後 patch 時，這份很適合先看。
- [api-security-model-principles.md](references/api-security-model-principles.md)
  這份參考聚焦 public API 與 multi-service API ecosystem 的 security model，而不是傳統 UI 時代的權限假設。它適合處理 caller type、scope、delegation、multi-tenant exposure 與 enforcement layer 轉移等問題。當你要設計 partner API、third-party integration 或考慮未來把控制下放到 gateway/proxy 時，這份最有幫助。
- [permission-model-principles.md](references/permission-model-principles.md)
  這份參考聚焦 permission management 是業務問題先於技術問題，核心取捨在 precision 與 management complexity 之間。它整理了 subject、role、permission、session、operation 與 data scope 的基本模型，以及 cache/precompute 的策略。當你要設計 RBAC、policy model、permission matrix、admin-side definition 或 application-side check interface 時，這份最直接。
