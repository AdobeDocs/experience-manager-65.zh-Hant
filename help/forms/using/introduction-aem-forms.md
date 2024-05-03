---
title: AEM Forms簡介
description: 使用此 AEM 6.5 指南建立、管理、發佈和更新數位表單。尋找有關如何進行安裝、升級和設定的說明，並了解如何編寫最適化表單。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
docset: aem65
feature: Adaptive Forms
exl-id: e5533b4f-93b7-4ea9-a01d-fdf9528652c8
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 15%

---

# AEM Forms簡介{#introduction-to-aem-forms}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html) |
| AEM 6.5 | 本文章 |

如需AEM Forms最新功能和增強功能的相關資訊，請參閱 [AEM Forms的新增功能](../../forms/using/whats-new.md).

## 關於AEM Forms {#about-aem-forms}

Adobe Experience Manager (AEM)提供易用的解決方案，用於建立、管理、發佈和更新複雜的數位表格，同時與後端流程、商業規則和資料整合。

AEM Forms結合表單製作、管理和發佈，以及通訊管理功能、檔案安全性和整合式分析，以建立吸引人的端對端體驗。 AEM Forms可在網路和行動裝置通路間運作，因此可有效整合至您的業務流程，減少紙張流程和錯誤，同時提升效率。

在大型企業中，表單通常是建立一次並透過複製到內容管理系統來重複使用。讓大型的表單資料庫保持最新狀態，並讓這些表單可供探索，是一項相當艱鉅的挑戰。 AEM提供可自訂的Forms入口網站，確保客戶可透過網頁和行動裝置管道找到並存取所需的表單。

AEM Forms提供的表單管理工具不僅可讓您管理最適化表單，還可管理XFA表單、PDF forms和相關資產。 如需詳細資訊，請參閱 [管理表單簡介](../../forms/using/introduction-managing-forms.md).

>[!NOTE]
>
>調適型表單功能 (適用於 [AEM 6.5 QuickStart](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html)) 僅用於探索和評估目的。若要供生產使用，必須獲得 AEM Forms 的有效許可；調適型表單的功能需要適當許可才可使用。

![AEM forms功能](do-not-localize/4th-draft.gif)

### 主要功能 {#key-capabilities}

總而言之，AEM Forms提供強大的表單管理功能（如下列功能），可減少手動程式並提高客戶滿意度。

* 集中式Forms入口網站，用於設計和部署動態表單，包括PDF、HTML5和調適型表單
* 簡單易用的圖形使用者介面，可讓業務使用者輕鬆匯入、管理、預覽和發佈表單
* 回應式表單目錄，具有使用關鍵字、標籤和中繼資料的強大搜尋功能
* 動態偵測使用者的裝置和位置，以適當地跨網頁和行動裝置頻道呈現表單
* 與Adobe Analytics整合，以有效測量表單使用量度
* 與Adobe Document Cloud eSign服務整合，或以手寫方式以電子方式簽署包含機密資訊的檔案
* 自動化表單發佈功能，以及透過多個管道提供及時、個人化且一致的通訊能力

## AEM表單型別 {#aem-form-types}

AEM Forms可讓您擴充新的和現有的表單，以建立：

* 完美的畫素、分頁HTML和看起來幾乎像紙張的PDF forms，或
* 自動針對使用者裝置和瀏覽器轉譯的最適化表單。

**PDF forms**

PDF forms可以離線填寫、儲存在本機，以及下次線上上時傳送的表單資料。 您可以使用2D條碼來擷取表單資料，並使用數位簽名來驗證使用者的真實性。

**HTML表單**

HTML5瀏覽器表單可在行動裝置和桌上型瀏覽器上檢視。 您可以使用Scribble或eSign服務，以電子方式簽署HTML表單。

**調適型表單**

調適型表單可以視需要新增或移除欄位或區段，動態調整以符合使用者回應。 AEM可讓您重複使用AdobeXML表單範本來建立調適型表單。

### 支援的功能 {#supported-features}

所有表單型別都支援下列功能：

* 動態配置
* 表單欄位驗證
* 內容感應式說明
* 指令碼和XML資料處理
* 協助工具設計與檢查
* 可在伺服器端儲存表單
* 支援檔案附件
* 與資料擷取的HTML Workspace整合

## 離線資料收集 {#offline-data-collection}

在提交表單資料後，Adobe Experience Manager會將表單資料與現有系統、商業規則和所需人員連結。

AEM Forms提供Forms Workspace，此行動應用程式可將您的數位業務流程延伸到行動裝置。 使用Forms工作區，您甚至可以在離線時收集及記錄資料。 Forms工作區使用行動裝置的功能，可讓您擷取像片、視訊，以及收集時間戳記和其他資訊等資料。 下次連線到網路時，您可以同步收集的資料。

離線擷取資料並在下次您重新連線時加以同步處理，對現場人員來說特別實用。 它可以提升生產力並減少錯誤。

**使用Forms Workspace進行離線資料收集的優點**

* 易於使用的HTML工作區應用程式，用於任務指派和追蹤
* 拖放式工作流程設計環境
* 企業內容管理聯結器(ECM)
* 開放式標準支援，包括連線表單資料與企業系統的XML和SOAP
* 現成的HTML報告可監控積壓、工作佇列和關鍵績效指標(KPI)
* 可自訂儀表板，以即時洞察業務營運
* 用於連線協力廠商報告工具的API

![第三份草稿](do-not-localize/3rd-draft.gif)

## 個人化通訊 {#personalized-communication}

高效率自助服務數位體驗的一個重要組成元件是及時通訊，使用者可以從任何地方在任何裝置上存取個人化的資訊。個人化和及時的通訊可以提高轉換率和使用者滿意度。

商業使用者可以使用AEM Forms自訂檔案範本、合併後端程式的資訊，並包含互動式元件，藉此建立引人入勝的個人化使用者體驗。 直覺式使用者介面可協助非技術使用者開發商業規則，以根據查詢來決定何時產生通訊，或起始使用者產生的回應。

個人化檔案，例如，收據、歡迎套件和陳述式，可以輕鬆地跨多個管道傳送。 組織可以將流量吸引到個人化的 Web 入口網站，進而讓使用者註冊或購買額外的服務。

**主要功能**

* 通訊製作環境，支援範本、內容區塊、商業規則等
* 檔案轉換與組裝
* 支援透過多個管道（包括網頁、電子郵件和紙張）隨選或批次檔案傳送
* 具有變更記錄的稽核軌跡
* 支援數位簽章，以驗證內容完整性和簽署者的身分
* AEM Forms的Document Security附加元件，包括加密、使用原則、追蹤和稽核

![版面配置二](do-not-localize/layout-02.png)

簡化個人化通訊工作流程

