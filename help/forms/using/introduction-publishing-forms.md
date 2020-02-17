---
title: 在入口網站上發佈表格簡介
seo-title: 在入口網站上發佈表格簡介
description: AEM Forms提供可用來建立表單入口網站的元件。 本文將向您介紹可用的表單入口網站元件。
seo-description: AEM Forms提供可用來建立表單入口網站的元件。 本文將向您介紹可用的表單入口網站元件。
uuid: 658de12b-66e5-438b-ae8f-872ec11a9c3e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9f1beb89-8eb1-4e37-a5e8-19752b21374a
docset: aem65
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78

---


# 在入口網站上發佈表格簡介{#introduction-to-publishing-forms-on-a-portal}

## AEM Forms Portal元件概觀 {#aem-forms-portal-components-overview}

在典型的以表單為中心的入口網站部署場景中，表單開發和入口網站開發是兩個不相干的活動。 當表單設計人員在儲存庫中設計和儲存表單時，網頁開發人員會建立網頁應用程式來列出表單並處理表單的提交。 表單會複製到Web層，因為表單儲存庫和Web應用程式之間沒有通信。

這種情況通常會導致管理問題和生產延遲。 例如，如果儲存庫中有較新版本的表單，您需要替換Web層上的表單、修改Web應用程式，以及在公共站點上重新部署表單。 重新部署Web應用程式可能會造成伺服器停機。 通常，伺服器停機是計畫中的活動，因此不能立即將更改推送到公共站點。

AEM Forms提供入口元件，可減少管理開銷和生產延遲。 這些元件讓網頁開發人員能夠在使用Adobe Experience Manager(AEM)製作的網站上建立和自訂表單入口網站。

![AEM Forms入口網站](assets/aem-forms-portal.png)

表單入口元件可讓您新增下列功能：

* 在自訂版面中列出表格。 現成可用的功能包括清單檢視、卡片檢視和面板檢視版面。 您可以建立自己的自訂版面。
* 可讓您在列出自訂中繼資料和自訂動作時，顯示自訂中繼資料。
* 列出由AEM Forms UI在使用Forms Portal元件的發佈例項上發佈的表單。
* 允許使用者以HTML和PDF格式轉換表單。
* 使用自訂HTML描述檔來轉換表單。
* 可根據各種條件（例如表單屬性、中繼資料和標籤）來搜尋表單。
* 將表單資料提交至servlet。
* 使用自訂CSS來自訂入口網站的外觀和感覺。
* 建立表單連結。
* 列出與最終用戶建立的最適化表單相關的草稿和提交。

## 可用的AEM Forms入口網站元件 {#available-aem-forms-portal-components}

AEM Forms提供下列立即可用的入口網站元件，群組在「 **Document Services** 」和「 **** Document Services Predicates」元件群組下：

### Search &amp; Lister {#search-amp-lister}

Search &amp; Lister元件可讓您將表單儲存庫中的表單列在入口網頁上，並提供設定選項，以根據指定的准則來列出表單。 它也可讓您指定搜尋准則，讓您的入口網站使用者可以在表單清單中搜尋。

### 草稿和提交 {#drafts-amp-submissions}

當Search &amp; Lister元件顯示由Forms作者公開的表單時，Framts &amp; Submissions元件會顯示儲存為草稿的表單，以供日後填寫及提交的表單。 此元件可為任何登入的使用者提供個人化體驗。

### 連結 {#link}

Link元件允許您在頁面上任意位置建立表單的連結。 假設您提供培訓課程，而您希望使用者提交表單以註冊培訓。 在您的網站上，您已張貼了計畫詳細資訊。 在詳細資訊下方，您想要提供註冊表單的連結。 連結元件可協助您建立該連結。

## 表單入口網站工作流程 {#forms-portal-workflow}

Forms Portal可讓您將表單從表單儲存庫清單到您的入口網頁。 它也可讓您指定搜尋准則，讓您的入口網站使用者可以在表單清單中搜尋。 您也可以使用「草稿與提交」元件來顯示儲存為草稿的表單，以供日後完成和提交的表單。 您必須先執行特定的作業集，這些功能才能在「網站」頁面上使用。 執行所列順序中的步驟，讓網站頁面提供元件和各自的功能：

1. **啟用Forms Portal元件**:現成可用的表單入口元件無法使用。 [為AEM Sites頁面啟用AEM Sidekick](/help/forms/using/enabling-forms-portal-components.md) 的元件。
1. **** 列出頁面上的表單（建立表單入口網站頁面）:您可以在AEM Sites和非AEM Site頁面上列出表單。 清單包含發佈例項上可用的表格。 使用者可以開啟表格並開始填寫這些表格。 每當使用者開啟表格時，就會建立新的表格例項：

   1. **在AEM Sites頁面上列出表單**:將 **[Search &amp; Lister元件新增至頁面，並設定](../../forms/using/creating-form-portal-page.md)**「清單窗格」**[](../../forms/using/creating-form-portal-page.md#p-list-pane-p)** ，以列出頁面上的表單。 將「搜尋窗格 **」元件新增並設定至****** Search &amp; Lister元件，以新增搜尋功能至頁面。 含有表單入口元件的頁面稱為 [表單入口頁面](../../forms/using/creating-form-portal-page.md)。

   1. **** 列出非AEM網站頁面上的表單：使用表 [單入口網站搜尋API](/help/forms/using/listing-forms-webpage-using-apis.md) ，在非AEM網站頁面上查詢、擷取和列出表單。

1. **在表單入口網頁上列出草稿和提交的表單**:將「草稿與提交」元件新增及設定至表單入口網站頁面。 元件列出處於草稿狀態的所有表單以及已提交的表單。

   若要啟用已提交的最適化表單，使其顯示在提交標籤中，請將「 **提交」動作****[設為「表單入口網站提交動作」](configuring-submit-actions.md)。**或者，啟用「表單入口網站提交」選項。 每當使用者提交表格時，表格就會新增至提交標籤。

1. **** 為草稿和提交的表單資料設定儲存空間：依預設，草稿和提交資料會儲存在AEM儲存庫中。 在生產環境中，建議您不要將草稿或提交的表單資料儲存在AEM儲存庫中。 [設定表單入口元件，將資料儲存至安全位置](../../forms/using/draft-submission-component.md#customizing-the-storage)。
1. **** （可選）自訂表單入口元件：自 [訂表單入口網頁範本](../../forms/using/customizing-templates-forms-portal-components.md) ，為元件提供獨特的外觀。
1. **** （可選）將自訂中繼資料新增至表單：將自 [訂中繼資料新增至表單](../../forms/using/customizing-templates-forms-portal-components.md) ，以改善清單和搜尋體驗。
1. **** 發佈表單入口網頁：您的表單入口網頁現已準備就緒。 發佈頁面。

## 相關文章 {#related-articles}

* [啟用表單入口元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立表單入口網頁](../../forms/using/creating-form-portal-page.md)
* [使用API在網頁上列出表格](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](../../forms/using/draft-submission-component.md)
* [自訂草稿和提交表單的儲存](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [將草稿和提交元件與資料庫整合的示例](integrate-draft-submission-database.md)
* [自訂表單入口元件的範本](../../forms/using/customizing-templates-forms-portal-components.md)
* [在入口網站上發佈表格簡介](../../forms/using/introduction-publishing-forms.md)

