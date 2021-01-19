---
title: 應用程式範本和元件
seo-title: 應用程式範本和元件
description: 請依照本頁來瞭解應用程式範本和元件。 它提供了有關模板結構的詳細資訊。
seo-description: 請依照本頁來瞭解應用程式範本和元件。 它提供了有關模板結構的詳細資訊。
uuid: ba2fd91b-de5a-4f39-a976-5455f9983669
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 7f31c6a7-92d5-4a87-a9f0-68a82b834d5a
translation-type: tm+mt
source-git-commit: a876a1a8d4aeb9e9a94c93a16742a4058307b0a8
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 1%

---


# 應用程式範本和元件{#app-templates-and-components}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

「範本」可用來建立「頁面」，並定義哪些元件可在選取範圍內使用。 範本是節點的階層，其結構與要建立的頁面相同，但沒有任何實際內容。

每個範本都會提供可供使用的元件選擇。

* 範本由[Components](/help/sites-developing/components.md)建立；
* 元件使用並允許存取Widget，而這些元件則用來轉換內容。

>[!NOTE]
>
>若要瞭解如何使用CRXDE Lite來開發AEM應用程式，請參閱「使用CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)開發」。[

範本是頁面的基礎。

若要建立頁面，必須將範本複製(node-tree **/apps/&lt;myapp>/templates/&lt;mytemplate>**)至site-tree中的對應位置：如果使用&#x200B;**Websites**&#x200B;標籤建立頁面，就會發生這種情況。

此複製動作也會提供頁面的初始內容（通常為僅限Top-Level Content）和屬性sling:resourceType，用於呈現頁面的頁面元件路徑（子節點jcr:content中的所有項目）。

## 範本結構{#structure-of-a-template}

需要考慮兩個方面：

* 範本本身的結構
* 使用範本時產生的內容結構

在類型&#x200B;**cq:Template**&#x200B;的節點下建立模板。

可以設定各種屬性，特別是：

* **jcr:title** - title for the template;顯示在對話框中。
* **jcr:description** - the template的description;顯示在對話框中。

此節點包含&#x200B;*a jcr:content(cq:PageContent)*&#x200B;節點，用作產生頁面的內容節點；此參照會使用&#x200B;*sling:resourceType*，來呈現新頁面的實際內容。

>[!NOTE]
>
>若要瞭解AEM中範本和元件的基本資訊，請參閱下列資源：
>
>* [範本](/help/sites-developing/templates.md)
>* [元件](/help/sites-developing/components.md)

>



對範本和元件有基本瞭解後，請參閱下列資源：

* [建立和添加模板和元件](/help/mobile/mobile-ondemand-app-templates.md)
* [使用內容屬性匯出內容](/help/mobile/on-demand-content-properties-exporting.md)
* [最佳作法](/help/mobile/best-practices-aem-mobile.md)
* [開發AEM Mobile內容服務](/help/mobile/developing-content-services.md)

### 其他資源 {#additional-resources}

若要瞭解行動應用程式的其他主題，請參閱下列連結：

* [具備內容同步功能的行動裝置](/help/mobile/mobile-ondemand-contentsync.md)
* [測試行動應用程式](/help/mobile/develop-mobile-apps-testing.md)

