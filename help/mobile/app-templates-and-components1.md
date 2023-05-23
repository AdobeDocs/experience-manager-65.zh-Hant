---
title: 應用程式模板和元件
seo-title: App Templates and Components
description: 按照此頁瞭解應用程式模板和元件。 它提供了有關模板結構的詳細資訊。
seo-description: Follow this page to learn about App Templates and Components. It provides detailed information on the structure of templates.
uuid: ba2fd91b-de5a-4f39-a976-5455f9983669
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 7f31c6a7-92d5-4a87-a9f0-68a82b834d5a
exl-id: 58d95325-7cb1-4204-842d-17add70e1fbf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 1%

---

# 應用程式模板和元件{#app-templates-and-components}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

「模板」用於建立頁面，並定義可在選定範圍內使用的元件。 模板是節點的層次結構，其結構與要建立的頁面相同，但沒有任何實際內容。

每個模板都將為您提供可供使用的元件選擇。

* 模板由 [元件](/help/sites-developing/components.md);
* 元件使用和允許訪問小部件，這些部件用於呈現內容。

>[!NOTE]
>
>要瞭解如何使用CRXDE Lite開AEM發應用程式，請參見 [用CRXDE Lite開發](/help/sites-developing/developing-with-crxde-lite.md)。

模板是頁面的基礎。

要建立頁面，必須複製模板（節點 — 樹） **/apps/&lt;myapp>/templates/&lt;mytemplate>**)到站點樹中的相應位置：如果使用 **網站** 頁籤。

此複製操作還為頁面提供其初始內容（通常僅限頂級內容）和屬性sling:resourceType，用於呈現頁面的頁面元件的路徑（子節點jcr:content中的所有內容）。

## 模板的結構 {#structure-of-a-template}

需要考慮兩個方面：

* 模板本身的結構
* 使用模板時生成的內容的結構

在類型的節點下建立模板 **cq：模板**。

可以設定各種屬性，特別是：

* **jcr：標題**  — 模板的標題；建立頁面時顯示。
* **jcr：說明**  — 模板說明；建立頁面時顯示。

此節點包含 *jcr:content(cq:PageContent)* 節點，作為生成頁面的內容節點的基礎；此引用，使用 *sling:resourceType*，用於呈現新頁面的實際內容的元件。

>[!NOTE]
>
>要瞭解中模板和元件的基AEM本資訊，請參閱以下資源：
>
>* [範本](/help/sites-developing/templates.md)
>* [元件](/help/sites-developing/components.md)
>


對「模板」和「元件」有基本瞭解後，請參閱以下資源：

* [建立和添加模板和元件](/help/mobile/mobile-ondemand-app-templates.md)
* [使用內容屬性導出內容](/help/mobile/on-demand-content-properties-exporting.md)
* [最佳做法](/help/mobile/best-practices-aem-mobile.md)
* [開發AEM Mobile內容服務](/help/mobile/developing-content-services.md)

### 其他資源 {#additional-resources}

要瞭解有關移動應用的其他主題，請參閱以下連結：

* [帶內容同步的移動](/help/mobile/mobile-ondemand-contentsync.md)
* [測試移動應用](/help/mobile/develop-mobile-apps-testing.md)
