---
title: 應用程式範本和元件
description: 請依照本頁面的說明了解應用程式範本和元件。 它提供有關範本結構的詳細資訊。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 58d95325-7cb1-4204-842d-17add70e1fbf
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 1%

---

# 應用程式範本和元件{#app-templates-and-components}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md)。

範本可用來建立頁面，並定義哪些元件可以在選取的範圍中使用。 範本是節點的階層，其結構與要建立的頁面相同，但沒有任何實際內容。

每個範本都會提供您一系列可供使用的元件。

* 範本的建置方式 [元件](/help/sites-developing/components.md)；
* 元件使用並允許存取Widget，這些用於呈現內容。

>[!NOTE]
>
>若要瞭解如何使用CRXDE Lite開發您的Adobe Experience Manager (AEM)應用程式，請參閱 [使用CRXDE Lite開發](/help/sites-developing/developing-with-crxde-lite.md).

範本是頁面的基礎。

若要建立頁面，必須複製範本（節點樹） **/apps/&lt;myapp>/templates/&lt;mytemplate>**)中的對應位置：如果頁面是使用 **網站** 標籤。

此複製動作也會提供頁面的初始內容（通常是僅限最上層內容）和屬性sling：resourceType，也就是用來呈現頁面的頁面元件路徑（子節點jcr：content中的所有專案）。

## 範本的結構 {#structure-of-a-template}

我們需要考慮兩個方面：

* 範本本身的結構
* 使用範本時產生的內容結構

範本建立於型別節點下 **cq：Template**.

您可以設定各種屬性，特別是：

* **jcr：title**  — 範本的標題；建立頁面時顯示在對話方塊中。
* **jcr：description**  — 範本的說明；建立頁面時顯示在對話方塊中。

此節點包含 *jcr：content (cq：PageContent)* 用作結果頁面內容節點基礎的節點。 此參考資料，使用 *sling：resourceType*，此元件用於轉譯新頁面的實際內容。

>[!NOTE]
>
>若要瞭解AEM範本和元件的基本知識，請參閱下列資源：
>
>* [範本](/help/sites-developing/templates.md)
>* [元件](/help/sites-developing/components.md)
>

在您已基本瞭解範本和元件後，請參閱下列資源：

* [建立和新增範本和元件](/help/mobile/mobile-ondemand-app-templates.md)
* [使用內容屬性匯出內容](/help/mobile/on-demand-content-properties-exporting.md)
* [最佳做法](/help/mobile/best-practices-aem-mobile.md)
* [開發AEM Mobile內容服務](/help/mobile/developing-content-services.md)

### 其他資源 {#additional-resources}

若要瞭解行動應用程式的其他主題，請參閱下列連結：

* [具有內容同步功能的行動裝置](/help/mobile/mobile-ondemand-contentsync.md)
* [測試行動應用程式](/help/mobile/develop-mobile-apps-testing.md)
