---
title: 定義測試案例
seo-title: Defining your Test Cases
description: 您的測試案例應根據使用案例和詳細的需求規格
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

# 定義測試案例{#defining-your-test-cases}

您的測試案例應以下列項目為基礎：

**使用案例**

* 這些功能在行為者（啟動某些動作的角色）與系統之間的互動中定義了所需的功能。
* 使用案例應由客戶定義。

**詳細需求規格**

* 應測試所有功能和效能要求。

測試應明確界定：

* 先決條件；這些內容可能涵蓋特定系統、配置或測試體驗。
* 應採取的步驟；詳細程度。
* 預期結果。
* 清除通過或失敗的標準。

自動化測試用例的前景顯然很有吸引力，因為它可以消除重複性任務。

## 手動測試與自動測試 {#manual-versus-automated-tests}

不過，自動化測試案例是一項重大投資，因此應考慮某些方面：

* 設定和設定需要時間、精力和體驗。
* 如果以瀏覽器為基礎，則安裝瀏覽器更新時，問題的風險會增加；需要更多時間來修正。
* 只有大項目才真正可行。
* 當為測試或長期發行計畫產生多個發行時即適用。

## 測試特定方面 {#testing-specific-aspects}

在測試AEM時，需特別注意一些特定詳細資訊：

**製作和發佈環境**

不過， [環境](/help/sites-developing/the-basics.md#environments) 有必要強調AEM在測試方面的決定性因素。

您必須將AEM視為兩個應用程式：

* the *作者* 環境此例項可讓作者輸入和發佈內容。
這有一小組(er)可預測的用戶，對於這些用戶，特定功能和效能至關重要。

* the *發佈* 環境此例項以發佈的表單呈現網站，供訪客存取。
這通常會有較大的使用者集，其中的流量並不總是100%可預測。 效能仍至關重要 — 在回應請求時。 還必須考慮快取和負載平衡。

雖然軟體與此相同，但它們：

* 不同用途
* 對功能和效能有不同的要求
* 設定不同
* 單獨調諧
* 每人都有自己的一套驗收測試

換句話說，它們必須分別測試，並搭配不同的測試案例。

**個人化**

測試個人化時，應使用多個使用者帳戶重複每個個別使用案例，以證明行為。

還必須檢查快取以檢查正確行為。

**Dispatcher**

大部分的專案都會安裝Dispatcher以進行快取和負載平衡。

測試很困難（快取會發生在不同層級和不同位置），且必須使用黑盒機制。 要測試的關鍵方面包括：

* **準確度**
確保網站訪客看到內容更新。

* **連續性**
確保當一台伺服器關閉時該網站仍可用。

* **叢集**
群集用於提供：

   * **故障轉移**
如果一台伺服器出現故障，群集中的其他伺服器將接管處理。

   * **效能**
通過完全故障轉移實現負載平衡可提高群集的效能。
當用於客戶項目時，必須測試群集以確認配置的正確操作。

## 測試第三方軟體 {#testing-third-party-software}

任何與AEM介面的第三方軟體都將在詳細需求規格中參考。

必須分析所需的任何測試（取決於定義的範圍）並獲得乾淨的測試。
