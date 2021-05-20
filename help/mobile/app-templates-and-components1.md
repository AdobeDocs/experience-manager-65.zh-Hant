---
title: 應用程式範本和元件
seo-title: 應用程式範本和元件
description: 請依照本頁面了解應用程式範本和元件。 它提供了有關模板結構的詳細資訊。
seo-description: 請依照本頁面了解應用程式範本和元件。 它提供了有關模板結構的詳細資訊。
uuid: ba2fd91b-de5a-4f39-a976-5455f9983669
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 7f31c6a7-92d5-4a87-a9f0-68a82b834d5a
exl-id: 58d95325-7cb1-4204-842d-17add70e1fbf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 1%

---

# 應用程式範本和元件{#app-templates-and-components}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

模板用於建立頁面，並定義哪些元件可在選定範圍內使用。 範本是節點的階層，其結構與要建立的頁面相同，但沒有任何實際內容。

每個範本都會提供一系列可供使用的元件。

* 範本由[元件](/help/sites-developing/components.md)組成；
* 元件使用和允許訪問介面工具集，這些元件用於呈現內容。

>[!NOTE]
>
>若要了解如何使用CRXDE Lite開發您的AEM應用程式，請參閱[使用CRXDE Lite開發](/help/sites-developing/developing-with-crxde-lite.md)。

範本是頁面的基礎。

若要建立頁面，必須將範本複製(node-tree **/apps/&lt;myapp>/templates/&lt;mytemplate>**)到站點樹中的對應位置：如果使用&#x200B;**Websites**&#x200B;標籤建立頁面，就會發生此情況。

此複製動作也會提供頁面的初始內容（通常僅限頂層內容）和屬性sling:resourceType，用於轉譯頁面的頁面元件路徑（子節點jcr:content中的所有內容）。

## 模板{#structure-of-a-template}的結構

需要考慮兩個方面：

* 模板本身的結構
* 使用範本時產生的內容結構

在&#x200B;**cq:Template**&#x200B;類型的節點下建立模板。

可以設定各種屬性，特別是：

* **jcr:title**  — 範本的title;建立頁面時顯示在對話方塊中。
* **jcr:description**  — 範本的說明；建立頁面時顯示在對話方塊中。

此節點包含&#x200B;*a jcr:content(cq:PageContent)*&#x200B;節點，這些節點用作生成頁面的內容節點的基礎；這會參考，使用&#x200B;*sling:resourceType*，用來轉譯新頁面實際內容的元件。

>[!NOTE]
>
>若要了解AEM中範本和元件的基本知識，請參閱下列資源：
>
>* [範本](/help/sites-developing/templates.md)
* [元件](/help/sites-developing/components.md)



在您基本了解範本和元件後，請參閱下列資源：

* [建立和新增範本和元件](/help/mobile/mobile-ondemand-app-templates.md)
* [使用內容屬性來匯出內容](/help/mobile/on-demand-content-properties-exporting.md)
* [最佳作法](/help/mobile/best-practices-aem-mobile.md)
* [開發AEM Mobile內容服務](/help/mobile/developing-content-services.md)

### 其他資源 {#additional-resources}

若要了解行動應用程式上的其他主題，請參閱下列連結：

* [具有內容同步的行動裝置](/help/mobile/mobile-ondemand-contentsync.md)
* [測試行動應用程式](/help/mobile/develop-mobile-apps-testing.md)
