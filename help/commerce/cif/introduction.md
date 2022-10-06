---
title: 簡介和概述
description: 內容與商務的簡介和概述。 Experience Manager商務整合架構(CIF)是Adobe的建議模式，可將Adobe Commerce及其他第三方商務解決方案的商務服務與Experience Cloud整合及延伸。
thumbnail: introducing-aem-commerce.jpg
exl-id: 52dad8f9-1812-42a3-8106-92b23f8517cd
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 1%

---

# Content and Commerce {#content-commerce}

有了Adobe Experience Manager內容與商務，品牌可以更快速地擴展與創新，以區分商務體驗，並掌握加速的線上支出。 AEM內容與商務結合了Experience Manager中身臨其境、全通路及個人化的體驗與任何數量的商務解決方案，為購物歷程的所有階段帶來與眾不同的體驗，縮短實現價值的時間，並推動更高的轉換。

## 內容與商務如何協助客戶成功

隨著客戶對線上商務體驗的期望越來越高，品牌被迫更快提供與眾不同的體驗和更多內容。 但是，實施內容管理平台通常需要在開發基本要素（如定制元件和創作工具）方面投入大量時間和預算，並在維護和升級方面產生成本。 Experience Manager Sites提供內容與商務作為Experience Manager的附加模組，提供現成可用的商務核心元件、製作工具和參考店面，以加速上線、跨團隊順暢協作，並促進轉換。

品牌可將Experience Manager與Adobe Experience Cloud的一部分Adobe Commerce，以及任何您選擇的商務引擎整合。 有了Experience Manager內容與商務，品牌可以：

* 更快擴展和創新
* 個人化體驗以促進轉換
* 建立一次，然後隨處發佈
* 讓客戶的體驗更加豐富並與眾不同
* 使用商務資料存取簡化製作

## AEM Commerce Integration Framework(CIF)簡介 {#cif-intro}

因為這些項目必須處理整合商務解決方案的複雜性。 商務解決方案可以是商業解決方案(例如Adobe Commerce)和一組自訂商務服務等任何項目。 整合高度依賴使用案例和生態系統。 它通常接觸到不同的地方，有多種不同的口味：

* 整合複雜且動態的生態系統（範例產品目錄）
* 業務需要以高效、全通路的方式使用其自身的生命週期來管理產品內容
* 為不同的主管建立複雜且個人化的購物歷程
* 在後端和前端快速調整和創新的能力
* 運行可擴展且穩定的E2E基礎架構，該基礎架構旨在實現最佳效能(Flash銷售、黑色星期五……)。 這包括統一的搜尋和快取管理。

這種複雜性為潛在的故障點、增加的總體擁有成本、延遲和降低價值實現開啟了大門。 這些原因促使開發了商務整合架構(CIF)，此為本Experience Manager的附加元件。 CIF透過商務功能延伸Experience Manager，並標準化與商務引擎的整合。 結果是一個經得起未來考驗、穩定且可擴展的解決方案，TCO更低。 它通過靈活的工具和無縫整合的功能來釋放技術和業務創新，以構建引人入勝的商務體驗。

![CIF元素](./assets/CIF/CIF_Overview.png)

## CIF自2013年起成功支援客戶

CIF擁有200多家客戶，成為成功內容及商務項目的成功組成部分。 這為當今和未來的IT和業務提供了價值。 最近的客戶項目將CIF描述為「極大的加速器和巨大的省時措施，具有很大的價值」。

## CIF優勢 {#cif-benefits}

CIF提供現成可用的商務核心元件，可減少對自訂程式碼的需求，加速品牌的上市時間。 所有核心元件均可立即整合，並具備Adobe的用戶端資料層，以水合物化客戶設定檔，例如統一的設定檔。 此設定檔會詳細擷取訪客的行為，以便用來即時預測及個人化客戶歷程。

CIF附加元件將產品內容帶入Experience Manager，並提供製作工具，例如產品主控台和產品/類別選擇器，讓行銷人員能在Experience Manager中建立並提供可購買的體驗，而不需依賴開發人員。 優點包括：

### 體驗

AEM中功能強大的CIF工具，可讓內容建立者以可擴充且不受傳送限制的方式，快速建立豐富且個人化的商務體驗，以充份利用商機。

![CIF元素](./assets/CIF/CIF_Product_Experience_Management.png)

### 值時間(TTV)

透過 [AEM核心元件](https://www.aemcomponents.dev/), [AEM Venia參考店面](https://github.com/adobe/aem-cif-guides-venia), [AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，以及PWA（無頭內容與商務）的整合模式。

CIF的建置宗旨是持續創新，提供隨時更新的附加元件，讓客戶能存取新功能和改良功能。

### Integrations

使用將您的生態系統（例如商務解決方案）與Experience Cloud連結  [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html)、基於微服務的無伺服器PaaS，以及 [CIF的參考實作](https://github.com/adobe/commerce-cif-graphql-integration-reference).

## 經驗證的模式和最佳做法

CIF根據最佳實務，為客戶提供標準化的整合模式。 這可協助客戶在今天獲得成功，並具有隨客戶而增長的靈活性，並適應未來的需求：

* 消除了產品目錄整合可能發生的典型難題。 範例：
   * 目錄卷數增加或複雜性增加時的效能問題
   * 無權訪問暫存資料
   * 需要即時產品資料和體驗
* 數位成熟度日益提高，因此需要體驗管理。 CIF隨附產品體驗管理功能，可增量整合，無需額外IT投入。
* 全通路：CIF支援多種接觸點技術（伺服器端、混合式、用戶端），包括模式、加速器和核心元件。
