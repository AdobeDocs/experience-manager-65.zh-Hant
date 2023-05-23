---
title: 門戶上發佈表單簡介
seo-title: Introduction to publishing forms on a portal
description: AEM Forms提供了可用於構建表單門戶的元件。 本文介紹了可用的表單門戶元件。
seo-description: AEM Forms provides with components that you can use to build your forms portal. This articles introduces you to the available forms portal components.
uuid: 658de12b-66e5-438b-ae8f-872ec11a9c3e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9f1beb89-8eb1-4e37-a5e8-19752b21374a
docset: aem65
exl-id: 240ed4d8-b21b-46eb-80a9-9e8093b77235
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 0%

---

# 門戶上發佈表單簡介{#introduction-to-publishing-forms-on-a-portal}

## AEM Forms門戶元件概述 {#aem-forms-portal-components-overview}

在典型的以表單為中心的門戶部署方案中，表單開發和門戶開發是兩個不相干的活動。 表單設計器在儲存庫中設計和儲存表單時，Web開發人員會建立一個Web應用程式來列出表單並處理表單提交。 Forms被複製到Web層，因為表單儲存庫和Web應用程式之間沒有通信。

這種情況往往導致管理問題和生產延遲。 例如，如果儲存庫中有一個較新版本的表單，則需要替換Web層上的表單，修改Web應用程式，然後在公共站點上重新部署該表單。 重新部署Web應用程式可能會導致伺服器停機。 通常，伺服器停機是計畫內活動，因此不能立即將更改推送到公共站點。

AEM Forms公司提供門戶元件，以減少管理費用和生產延遲。 這些元件使Web開發人員能夠在使用Adobe Experience Manager(AEM)創作的網站上建立和定制表單門戶。

![AEM Forms門戶](assets/aem-forms-portal.png)

表單門戶元件允許您添加以下功能：

* 在自定義佈局中列出表單。 現成版本中提供「清單」視圖、「卡」視圖和「面板」視圖佈局。 您可以建立自己的自定義佈局。
* 允許您在列出自定義元資料和自定義操作時顯示它們。
* 列出由AEM FormsUI在使用Forms門戶元件的發佈實例上發佈的表單。
* 允許最終用戶以HTML和PDF格式呈現表單。
* 使用自定義HTML配置檔案來呈現表單。
* 啟用基於各種條件（如表單屬性、元資料和標籤）的表單搜索。
* 將表單資料提交到Servlet。
* 使用自定義CSS自定義門戶的外觀。
* 建立到表單的連結。
* 列出與最終用戶建立的自適應表單相關的草稿和提交。

## 可用的AEM Forms門戶元件 {#available-aem-forms-portal-components}

AEM Forms提供以下開箱即用的門戶元件，分組在 **文檔服務** 和 **文檔服務謂語** 元件組：

### 搜索與李斯特 {#search-amp-lister}

Search &amp; Lister元件允許您將表單從表單儲存庫列到門戶頁面，並提供了根據指定條件列出表單的配置選項。 它還允許您指定搜索條件，以便您的門戶用戶能夠跨表單清單進行搜索。

### 草稿和提交 {#drafts-amp-submissions}

Search &amp; Lister元件顯示由Forms作者公開的表單，而Drafts &amp; Submissions元件則顯示保存為草稿的表單，以供日後完成和提交的表單。 此元件為任何登錄用戶提供個性化體驗。

### 連結 {#link}

「連結」元件允許您建立指向頁面上任意位置的表單的連結。 請考慮您正在提供培訓計畫，並且希望用戶提交表格以註冊培訓。 在你的網站上，你發佈了程式詳細資訊。 在詳細資訊下面，您要提供指向註冊表的連結。 「連結」元件可幫助您建立該連結。

## Forms門戶工作流 {#forms-portal-workflow}

Forms門戶使您能夠將表單從表單儲存庫列到門戶頁面。 它還允許您指定搜索條件，以便您的門戶用戶能夠跨表單清單進行搜索。 您還可以使用「草稿和提交」元件來顯示保存為草稿的表單，以供以後完成和提交的表單。 在「站點」頁面上提供這些功能之前，必須執行一組操作。 按列出順序執行步驟，使元件和各功能在站點頁面上可用：

1. **啟用Forms門戶元件**:現成，表單門戶元件不可用。 [從側腳啟用組AEM件](/help/forms/using/enabling-forms-portal-components.md) AEM Sites版。
1. **在頁面上列出表單（建立表單門戶頁面）:** 您可以在AEM Sites和非網站頁AEM面列出表單。 該清單包含發佈實例上可用的表單。 用戶可以開啟表單並開始填寫這些表單。 每當用戶開啟表單時，都會建立表單的新實例：

   1. **列出AEM Sites頁面上的表單**:添加 **[搜索與李斯特](../../forms/using/creating-form-portal-page.md)** 元件到頁面並配置 **[清單窗格](../../forms/using/creating-form-portal-page.md#p-list-pane-p)** 框中，選擇「預設值」。 添加和配置 **搜索窗格** 元件 **搜索與李斯特** 元件也可向頁面添加搜索功能。 帶有表單門戶元件的頁面稱為 [表單門戶頁](../../forms/using/creating-form-portal-page.md)。

   1. **在非AEM Sites頁面上列出表單：** 使用 [表單門戶搜索API](/help/forms/using/listing-forms-webpage-using-apis.md) 查詢、檢索和列出非AEM Sites頁面上的表單。

1. **在表單門戶頁面上列出草稿和提交的表單**:將「草稿和提交」元件添加並配置到表單門戶頁面。 該元件列出處於草稿狀態的所有表單以及已提交的表單。

   要使提交的自適應表單能夠顯示在提交頁籤中，請設定 **提交操作** 至 **[Forms門戶提交操作](configuring-submit-actions.md)。** 或者，啟用Forms門戶提交選項。 每當用戶提交表單時，表單都會添加到提交頁籤。

1. **配置草稿和已提交表單資料的儲存：** 預設情況下，草稿和提交資料儲存在儲存AEM庫中。 在生產環境中，建議不要將草稿或提交的表單資料儲存在儲存AEM庫中。 [配置表單門戶元件以將資料保存到安全位置](../../forms/using/draft-submission-component.md#customizing-the-storage)。
1. **（可選）自定義表單門戶元件：** [自定義表單門戶頁面模板](../../forms/using/customizing-templates-forms-portal-components.md) 為元件提供獨特的外觀。
1. **（可選）將自定義元資料添加到表單：** [將自定義元資料添加到表單](../../forms/using/customizing-templates-forms-portal-components.md) 以改進清單和搜索體驗。
1. **發佈表單門戶頁：** 您的表單門戶頁面現已就緒。 發佈頁面。

## 相關條目 {#related-articles}

* [啟用表單門戶元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立表單門戶頁](../../forms/using/creating-form-portal-page.md)
* [使用API在網頁上列出表單](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](../../forms/using/draft-submission-component.md)
* [自定義草稿和已提交表單的儲存](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [將草稿和提交元件與資料庫整合的示例](integrate-draft-submission-database.md)
* [自定義表單門戶元件的模板](../../forms/using/customizing-templates-forms-portal-components.md)
* [門戶上發佈表單簡介](../../forms/using/introduction-publishing-forms.md)
