---
title: 定義Test案例
seo-title: Defining your Test Cases
description: 您的test案例應基於使用案例和詳細的要求規格
seo-description: Your test cases should be based upon the use cases and the detailed requirements specification
uuid: daaa5370-bcd3-45a6-9974-f9b5af6a1529
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: f01eb2aa-6891-4f5d-8a4a-43fc1534c222
docset: aem65
exl-id: c09cde0d-401c-437f-9ec8-a0530c1312d5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# 定義Test案例{#defining-your-test-cases}

您的test案例應基於：

**使用案例**

* 這些功能根據參與者（啟動某些操作的角色）與系統之間的交互定義所需的功能。
* 使用案例應由客戶定義。

**詳細需求規格**

* 應測試所有功能和效能要求。

test應明確界定：

* 先決條件；這些可能涵蓋特定的系統、配置或測試程式體驗。
* 要採取的步驟；以適當的細節。
* 預期結果。
* 清除通過或失敗的條件。

自動化test案例的前景顯然非常誘人，因為它可以消除重複性任務。

## 手動與自動Test {#manual-versus-automated-tests}

但是，自動化test案例是一項重大投資，因此應考慮以下某些方面：

* 設定和配置需要時間、精力和經驗。
* 如果基於瀏覽器，則安裝瀏覽器更新時出現問題的風險增加；需要更多時間來糾正。
* 只對大項目真正可行。
* 當為測試或在長期發佈計畫中生成多個版本時是好的。

## 測試特定方面 {#testing-specific-aspects}

在測試AEM某些特定細節時，特別感興趣：

**作者和發佈環境**

不過， [環境](/help/sites-developing/the-basics.md#environments) 值得強調的是測AEM試的決定性因素。

您必須考慮AEM為兩個應用程式：

* 這樣 *作者* 環境此實例允許作者輸入和發佈內容。
這有一小組（呃）可預測的用戶，對於這些用戶來說，特定的功能和效能至關重要。

* 這樣 *發佈* 環境此實例以其發佈的表單顯示網站，供訪問者訪問。
這通常會有更多的用戶群，其流量並不總是100%可預測。 在響應請求時，效能仍然至關重要。 快取和負載平衡也必須考慮。

儘管軟體與此相同，但它們：

* 服務於不同的目的
* 在功能和效能方面有不同的要求
* 配置不同
* 單獨調諧
* 將各自擁有一套接受test

換句話說，它們必須單獨進行測試，並使用不同的test案例。

**個人化**

在測試個性化時，應使用多個用戶帳戶重複每個單獨的使用案例以證明行為。

還必須檢查快取是否正確。

**調度員**

大多數項目都將安裝Dispatcher用於快取和負載平衡。

測試很困難（快取在不同級別和不同位置），必須在黑盒基礎上進行。 test的關鍵方面包括：

* **精度**
確保網站訪問者看到內容更新。

* **連續性**
確保當一台伺服器關閉時網站仍然可用。

* **群集**
群集用於提供：

   * **故障轉移**
如果一台伺服器發生故障，群集中的其他伺服器將接管處理。

   * **效能**
使用完全故障轉移的負載平衡提高了群集的效能。
當用於客戶項目時，必須測試群集以確認配置的正確操作。

## 測試第三方軟體 {#testing-third-party-software}

接入的任何第三方軟體AEM將在詳細要求規範中參考。

必須分析所需的任何test（取決於定義的範圍）並獲得乾淨的test。
