---
title: AEM Forms簡介
seo-title: Introduction to AEM Forms
description: 透過Adobe Experience Manager Forms，商務使用者可將吸引人、回應式和最適化的表單整合至網頁和行動網站，簡化數位註冊程式，並提高客戶轉換率。
seo-description: With Adobe Experience Manager Forms, business users can integrate engaging, responsive, and adaptive forms into web and mobile sites, simplifying the digital enrollment process and increasing customer conversion rates.
uuid: a6564997-4227-4d5d-b27d-47a55a386238
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
discoiquuid: a20383f2-f86a-45bf-a39e-725ee764503b
docset: aem65
feature: Adaptive Forms
exl-id: e5533b4f-93b7-4ea9-a01d-fdf9528652c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 0%

---

# AEM Forms簡介{#introduction-to-aem-forms}

如需AEM Forms最新功能和增強功能的相關資訊，請參閱 [AEM Forms的新功能](../../forms/using/whats-new.md).

## 關於AEM Forms {#about-aem-forms}

Adobe Experience Manager(AEM)提供簡單易用的解決方案，可建立、管理、發佈和更新複雜的數位表單，同時與後端流程、業務規則和資料整合。

AEM Forms將表單製作、管理和發佈與通信管理功能、檔案安全性及整合式分析結合，打造吸引人的端對端體驗。 AEM Forms旨在跨網頁和行動通道運作，可有效地整合至您的業務流程中，減少紙面流程和錯誤，同時提高效率。

在大型企業中，表單通常只需建立一次，然後通過複製到內容管理系統來重複使用。 保持大型表單資料庫的最新狀態並使其可被發現，這是一個相當大的挑戰。 AEM提供可自訂的Forms入口網站，確保客戶在網頁和行動裝置頻道間都能找到並存取所需表單。

AEM Forms提供的表單管理工具不僅可讓您管理最適化表單，還可管理XFA表單、PDF forms和相關資產。 如需詳細資訊，請參閱 [管理表單簡介](../../forms/using/introduction-managing-forms.md).

![](do-not-localize/4th-draft.gif)

### 關鍵功能 {#key-capabilities}

總而言之，AEM Forms提供了功能強大的表單管理功能，如以下功能，可減少手動流程並提高客戶滿意度。

* 集中式Forms入口網站，用於設計和部署動態表單，包括PDF、HTML5和最適化表單
* 簡單易用的圖形用戶介面，可讓商務用戶輕鬆導入、管理、預覽和發佈表單
* 回應式表單目錄，具有使用關鍵字、標籤和中繼資料的強大搜尋功能
* 動態偵測使用者的裝置和位置，以在網路和行動頻道上適當地呈現表單
* 與Adobe Analytics整合，以有效衡量表單使用量度
* 與Adobe Document Cloud eSign Services或Scribble整合，以電子方式簽署包含機密資訊的檔案
* 自動化表單發佈功能，以及透過多個管道提供及時、個人化且一致的通訊的能力

## AEM表單類型 {#aem-form-types}

AEM Forms可讓您擴充新表單和現有表單以建立：

* 像素完美、編頁的HTML和PDF forms，看起來幾乎像紙張，或
* 自動為使用者裝置和瀏覽器轉譯的最適化表單。

**PDF forms**

PDF forms可離線填寫、儲存於本機，並可在您下次上線時傳送表單資料。 您可以使用2D條碼來擷取表單資料，並使用數位簽名來驗證使用者的真實性。

**HTML表單**

HTML5瀏覽器型表單可在行動裝置和案頭瀏覽器上檢視。 您可以使用手寫或eSign服務以電子方式簽署HTML表單。

**調適型表單**

視需要新增或移除欄位或區段，最適化表單可動態適應使用者回應。 AEM可讓您重複使用AdobeXML表單範本，以建立最適化表單。

### 支援的功能 {#supported-features}

所有表單類型都支援下列功能：

* 動態版面
* 表單欄位驗證
* 內容相關說明
* 指令碼和XML資料處理
* 協助工具設計和檢查
* 可在伺服器端儲存表單
* 支援檔案附件
* 與HTML工作區整合以進行資料擷取

## 離線資料收集 {#offline-data-collection}

提交表單資料後，Adobe Experience Manager會將表單資料與現有系統、業務規則及必要人員連結。

AEM Forms提供Forms Workspace，此行動應用程式可將您的數位業務流程擴充至行動裝置。 使用Forms Workspace，即使離線，您也可以收集和記錄資料。 Forms工作區運用行動裝置的功能，並可讓您擷取像片、影片，以及收集時間戳記和其他資訊等資料。 下次連接到網路時，可以同步收集的資料。

離線擷取資料並在您下次再上線時進行同步，對現場人員特別有幫助。 它可提高生產力並減少錯誤。

**使用Forms Workspace進行離線資料收集的優點**

* 簡單易用的HTML工作區應用程式，用於任務分配和跟蹤
* 拖放式工作流程設計環境
* 企業內容管理連接器(ECM)
* 開放標準支援，包括XML和SOAP，以連接表單資料與企業系統
* 現成可用的HTML報表可監控積壓、工作佇列和關鍵績效指標(KPI)
* 可自訂的控制面板，以即時深入分析業務運作
* 用於連線協力廠商報表工具的API

![](do-not-localize/3rd-draft.gif)

## 個人化通訊 {#personalized-communication}

高效自助式數位體驗的重要元件，是及時傳達個人化資訊，供使用者從任何位置和裝置存取。 個人化和及時的通訊可改善轉換率和使用者滿意度。

使用AEM Forms，業務使用者可以透過自訂檔案範本、納入後端程式的資訊，以及包括互動式元件，建立引人入勝的個人化使用者體驗。 直觀的用戶介面幫助非技術用戶開發業務規則，這些規則根據查詢決定何時生成通信，或啟動用戶生成的響應。

個人化文檔（如收據、歡迎工具包和對帳單）可以輕鬆地跨多個渠道傳送。 組織可以推動流向個性化的Web門戶，從而導致註冊或購買其他服務。

**重要功能**

* 支援範本、內容區塊、業務規則等的通信製作環境
* 文檔轉換和匯編
* 支援透過多個管道（包括網頁、電子郵件和紙張）的隨選或批次檔案傳送
* 具有更改歷史記錄的審核跟蹤
* 支援數位簽名，以驗證內容完整性和簽名者的身份
* AEM Forms的檔案安全附加元件，包括加密、使用原則、追蹤和稽核

![](do-not-localize/layout-02.png)

簡化的個人化通訊工作流程
