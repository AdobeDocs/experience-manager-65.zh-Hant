---
title: 在入口網站發佈表單簡介
seo-title: Introduction to publishing forms on a portal
description: AEM Forms提供可用來建置表單入口網站的元件。 本文會介紹可用的表單入口網站元件。
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

# 在入口網站發佈表單簡介{#introduction-to-publishing-forms-on-a-portal}

## AEM Forms portal元件概觀 {#aem-forms-portal-components-overview}

在典型的以表單為中心的門戶部署情形中，表單開發和門戶開發是兩個不相關的活動。 表單設計人員在存放庫中設計和儲存表單時，網頁開發人員會建立網頁應用程式來列出表單並處理表單提交作業。 Forms會複製到Web層，因為表單存放庫與Web應用程式之間沒有通訊。

這種情況往往導致管理問題和生產延遲。 例如，如果儲存庫中有較新版本的表單，則您需要替換Web層上的表單、修改Web應用程式，然後在公共站點上重新部署該表單。 重新部署Web應用程式可能會造成伺服器停機。 通常，伺服器停機是計畫中的活動，因此無法即時將變更推送至公開網站。

AEM Forms提供入口元件，可減少管理開銷和生產延遲。 這些元件讓網頁開發人員能在使用Adobe Experience Manager(AEM)製作的網站上建立和自訂表單入口網站。

![AEM Forms入口網站](assets/aem-forms-portal.png)

表單入口網站元件可讓您新增下列功能：

* 以自訂配置列出表單。 提供立即可用的清單視圖、卡片視圖和面板視圖佈局。 您可以建立自己的自訂配置。
* 可讓您在列出自訂中繼資料時顯示自訂動作。
* 列出由AEM Forms UI發佈的表單，位於使用Forms Portal元件的發佈執行個體上。
* 允許使用者以HTML和PDF格式呈現表單。
* 使用自訂HTML設定檔來轉譯表單。
* 根據各種條件（如表單屬性、中繼資料和標籤）啟用表單搜尋。
* 將表單資料提交至servlet。
* 使用自訂CSS來自訂入口網站的外觀和風格。
* 建立表單連結。
* 列出與使用者建立的最適化表單相關的草稿和提交。

## 可用的AEM Forms入口網站元件 {#available-aem-forms-portal-components}

AEM Forms提供下列立即可用的入口元件，分組於 **檔案服務** 和 **文檔服務謂詞** 元件組：

### Search &amp; Lister {#search-amp-lister}

Search &amp; Lister元件可讓您將表單從表單存放庫清單至入口網站頁面，並提供設定選項，讓您根據指定的條件列出表單。 它也可讓您指定搜尋條件，讓您的入口網站使用者能夠在表單清單中進行搜尋。

### 草稿和提交 {#drafts-amp-submissions}

Search &amp; Lister元件顯示由Forms作者公開的表單，而Drafts &amp; Submissions元件則顯示儲存為草稿的表單，以供稍後完成已提交的表單。 此元件可為任何登入的使用者提供個人化體驗。

### 連結 {#link}

「連結」元件可讓您建立表單的連結，該連結位於頁面上任何位置。 假設您提供培訓計畫，並且希望用戶提交表單以註冊培訓。 您已在您的網站上發佈了計畫詳細資訊。 在詳細資訊下方，您想要提供註冊表單的連結。 連結元件可協助您建立該連結。

## Forms Portal Workflow {#forms-portal-workflow}

Forms入口網站可讓您將表單從表單存放庫清單至入口網站頁面。 它也可讓您指定搜尋條件，讓您的入口網站使用者能夠在表單清單中進行搜尋。 您也可以使用「草稿與提交」元件來顯示儲存為草稿的表單，以便日後完成提交的表單。 您必須先執行一組特定操作，這些功能才能在Sites頁面上使用。 依照所列順序執行步驟，讓元件和各自功能可在網站頁面上使用：

1. **啟用Forms Portal元件**:現成可用的表單入口網站元件無法使用。 [從AEM sidekick啟用元件](/help/forms/using/enabling-forms-portal-components.md) ，取得AEM Sites頁面。
1. **在頁面上列出表單（建立表單入口網頁）:** 您可以列出AEM Sites和非AEM網站頁面上的表單。 清單包含發佈執行個體上可用的表單。 使用者可以開啟表單並開始填寫。 每當用戶開啟表單時，都會建立表單的新實例：

   1. **AEM Sites頁面上的表單清單**:新增 **[Search &amp; Lister](../../forms/using/creating-form-portal-page.md)** 元件並設定 **[清單窗格](../../forms/using/creating-form-portal-page.md#p-list-pane-p)** ，列出頁面上的表單。 新增及設定 **搜尋窗格** 元件 **Search &amp; Lister** 元件，也可將搜尋功能新增至頁面。 含有表單入口網站元件的頁面稱為 [表單入口網頁](../../forms/using/creating-form-portal-page.md).

   1. **非AEM Sites頁面上的表單清單：** 使用 [表單入口網站搜尋API](/help/forms/using/listing-forms-webpage-using-apis.md) 查詢、擷取和列出非AEM Sites頁面上的表單。

1. **在表單入口網站頁面上列出草稿和已提交的表單**:將「草稿與提交」元件新增及設定至表單入口網站頁面。 該元件列出處於草稿狀態的所有表單以及已提交的表單。

   若要讓已提交的最適化表單顯示在提交索引標籤中，請設定 **提交動作** to **[Forms Portal提交動作](configuring-submit-actions.md).** 或者，啟用Forms Portal Submit選項。 每當使用者提交表單時，表單就會新增至提交索引標籤。

1. **為草稿和提交的表單資料配置儲存空間：** 依預設，草稿和提交資料會儲存在AEM存放庫中。 在生產環境中，建議不要將草稿或已提交的表單資料儲存在AEM存放庫中。 [配置表單門戶元件以將資料保存到安全位置](../../forms/using/draft-submission-component.md#customizing-the-storage).
1. **（可選）自訂表單入口網站元件：** [自訂您的表單入口網站頁面範本](../../forms/using/customizing-templates-forms-portal-components.md) 為元件提供獨特的外觀。
1. **（可選）將自訂中繼資料新增至表單：** [將自訂中繼資料新增至表單](../../forms/using/customizing-templates-forms-portal-components.md) 以改善清單和搜尋體驗。
1. **發佈表單入口網站頁面：** 您的表單入口網站頁面現已準備就緒。 發佈頁面。

## 相關文章 {#related-articles}

* [啟用表單入口網站元件](/help/forms/using/enabling-forms-portal-components.md)
* [建立表單入口網站頁面](../../forms/using/creating-form-portal-page.md)
* [使用API列出網頁上的表單](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交元件](../../forms/using/draft-submission-component.md)
* [自訂草稿和已提交表單的儲存](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [將草稿和提交元件與資料庫整合的範例](integrate-draft-submission-database.md)
* [自訂表單入口網站元件的範本](../../forms/using/customizing-templates-forms-portal-components.md)
* [在入口網站發佈表單簡介](../../forms/using/introduction-publishing-forms.md)
