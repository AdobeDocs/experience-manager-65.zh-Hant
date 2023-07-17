---
title: 在入口網站上發佈表單的簡介
description: Adobe Experience Manager Forms提供可用來建置Forms入口網站的元件。 本文會向您介紹可用的Forms Portal元件。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: 240ed4d8-b21b-46eb-80a9-9e8093b77235
source-git-commit: 60924e7ee204e43a2ff833fbc394beca8db9c9d9
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 0%

---

# 在入口網站上發佈表單的簡介{#introduction-to-publishing-forms-on-a-portal}

## AEM Forms Portal元件概觀 {#aem-forms-portal-components-overview}

在典型的以表單為中心的入口網站部署情境中，表單開發和入口網站開發是兩個分離的活動。 當表單設計人員將表單設計和儲存在存放庫時，網頁開發人員會建立網站應用程式以列出表單並處理表單提交。 Forms會複製到Web層，因為Forms存放庫和Web應用程式之間沒有通訊。

這類情況通常會導致管理問題和生產延遲。 例如，如果儲存庫中有較新版本的表單，您必須取代Web層上的表單、修改Web應用程式，並在公用網站上重新部署表單。 重新部署Web應用程式可能會導致伺服器停機。 伺服器停機通常是計畫的活動，因此變更無法即時推送至公用網站。

AEM Forms提供入口網站元件，可減少管理費用和生產延遲。 這些元件讓網頁開發人員能夠在使用Forms (AEM)編寫的網站上建立和自訂Adobe Experience Manager入口網站。

![AEM Forms入口網站](assets/aem-forms-portal.png)

表單入口網站元件可讓您新增下列功能：

* 以自訂版面配置列出表單。 隨附現成可用的清單檢視、卡片檢視和面板檢視版面配置。 您可以建立自己的自訂版面配置。
* 可讓您在列出自訂中繼資料和自訂動作時顯示它們。
* 列出使用AEM Forms Portal元件的發佈執行個體上Forms UI發佈的表單。
* 允許一般使用者以HTML和PDF格式轉譯表單。
* 使用自訂HTML設定檔來轉譯表單。
* 啟用根據各種條件搜尋表單，例如表單屬性、中繼資料和標籤。
* 將表單資料提交至servlet。
* 使用自訂CSS來自訂入口網站的外觀。
* 建立表單連結。
* 列出一般使用者建立的最適化表單相關的草稿和提交內容。

## 可用的AEM Forms Portal元件 {#available-aem-forms-portal-components}

AEM Forms提供下列立即可用的入口網站元件，分組在 **檔案服務** 和 **檔案服務述詞** 元件群組：

### 搜尋和製表人 {#search-amp-lister}

Search &amp; Lister元件可讓您從表單存放庫將表單列示到入口網站頁面，並提供根據指定條件列示表單的設定選項。 它也可讓您指定搜尋條件，讓入口網站使用者在表單清單中進行搜尋。

### 草稿和提交 {#drafts-amp-submissions}

雖然「搜尋和清單程式」元件會顯示由Forms作者公開的表單，但「草稿和提交」元件會顯示儲存為草稿的表單，以供稍後完成和提交的表單。 此元件可為任何登入使用者提供個人化體驗。

### 連結 {#link}

連結元件可讓您在頁面上的任何位置建立表單的連結。 假設您提供訓練計畫，並且希望使用者提交表格以註冊訓練。 您已在您的網站上公佈此計畫的詳細資料。 在詳細資訊下方，您想要提供登錄檔單的連結。 連結元件可協助您建立該連結。

## Forms入口網站工作流程 {#forms-portal-workflow}

Forms入口網站可讓您將表單從表單存放庫清單至入口網站頁面。 它也可讓您指定搜尋條件，讓入口網站使用者在表單清單中進行搜尋。 您也可以使用草稿和提交元件來顯示儲存為草稿的表單，以便稍後完成和提交表單。 您可以在Sites頁面上提供這些功能之前，執行特定的一組作業。 依照列出的順序執行步驟，讓元件和個別功能可在網站頁面上使用：

1. **啟用Forms Portal元件**：Forms Portal元件為現成可用元件。 [啟用來自AEM sidekick的元件](/help/forms/using/enabling-forms-portal-components.md) 適用於AEM Sites頁面。
1. **在頁面上列出表單(建立Forms入口網站頁面)：** 您可以在AEM Sites和非AEM網站頁面上列出表單。 此清單包含發佈執行個體上可用的表單。 使用者可以開啟表單並開始填寫表單。 每當使用者開啟表單時，就會建立表單的新例項：

   1. **在AEM Sites頁面上列出表單**：新增 **[搜尋和製表人](../../forms/using/creating-form-portal-page.md)** 元件至頁面並設定 **[清單窗格](../../forms/using/creating-form-portal-page.md#p-list-pane-p)** 在其中，列出頁面上的表單。 新增並設定 **搜尋窗格** 元件至 **搜尋和製表人** 元件以新增搜尋功能至頁面。 具有Forms Portal元件的頁面稱為 [Forms入口網站頁面](../../forms/using/creating-form-portal-page.md).

   1. **在非AEM Sites頁面上列出表單：** 使用 [Forms入口網站搜尋API](/help/forms/using/listing-forms-webpage-using-apis.md) 在非AEM Sites頁面上查詢、擷取及列出表單。

1. **在Forms入口網站頁面上列出草稿和已提交的表單**：將草稿和提交元件新增並設定至Forms Portal頁面。 元件會列出處於草稿狀態的所有表單以及已提交的表單。

   若要讓提交的最適化表單出現在提交索引標籤中，請設定 **提交動作** 至 **[Forms入口網站提交動作](configuring-submit-actions.md).** 或者，啟用Forms入口網站提交選項。 每當使用者提交表單時，該表單都會新增到提交索引標籤。

1. **設定草稿和已提交表單資料的儲存空間：** 依預設，草稿和提交資料會儲存在AEM存放庫中。 在生產環境中，建議不要將草稿或已提交的表單資料儲存在AEM存放庫中。 [設定Forms Portal元件，將資料儲存至安全位置](../../forms/using/draft-submission-component.md#customizing-the-storage).
1. **（選用）自訂Forms Portal元件：** [自訂Forms Portal頁面範本](../../forms/using/customizing-templates-forms-portal-components.md) 為元件提供獨特的外觀。
1. **（選用）新增自訂中繼資料至表單：** [新增自訂中繼資料至表單](../../forms/using/customizing-templates-forms-portal-components.md) 以改善清單和搜尋體驗。
1. **發佈Forms入口網站頁面：** 您的Forms入口網站頁面現已準備就緒。 發佈頁面。

## 相關文章 {#related-articles}

* [啟用Forms Portal元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立Forms入口網站頁面](../../forms/using/creating-form-portal-page.md)
* [使用API的網頁上列出表單](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](../../forms/using/draft-submission-component.md)
* [自訂草稿和已提交表單的儲存](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [將草稿和提交元件與資料庫整合的範例](integrate-draft-submission-database.md)
* [自訂Forms Portal元件的範本](../../forms/using/customizing-templates-forms-portal-components.md)
* [在入口網站上發佈表單的簡介](../../forms/using/introduction-publishing-forms.md)
