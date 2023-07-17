---
title: 建立共用資源匯出設定
description: 請依照本頁所述操作，瞭解如何從Adobe Experience Manager (AEM)匯出共用資源，以便上傳至AEM Mobile。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 576b4567-c7b6-4196-84e7-47e980637540
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---

# 建立共用資源匯出設定{#creating-shared-resources-export-configuration}

>[!NOTE]
>
>Adobe建議對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案使用SPA編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**必備條件**:
>
>在瞭解如何建立和修改共用資源之前，請參閱 [內容同步](/help/mobile/mobile-ondemand-contentsync.md) 以瞭解基本概念。

Adobe Experience Manager (AEM) Mobile使用者會使用Content Sync將即時內容匯出至靜態內容，以便在行動應用程式中使用，此匯出會在內容從AEM Mobile上傳至Mobile On-Demand Services時發生。

屬性 ***dps-exportTemplate*** 以上表格所述，會定義應用程式匯出設定的路徑。 設定此屬性以建立和修改共用資源。

下列資源說明如何從AEM匯出共用資源以上傳至AEM Mobile。

共用HTML資源可讓文章共用原本會針對所有文章複製的HTML資源，並可包含圖示、字型、JavaScript和css。

內容同步設定位於 **&lt;dps-exporttemplate>/dps-HTMLResources>** 應設定為匯出內容以及裝置上靜態呈現屬性所需的文章。

>[!CAUTION]
>
>只有具備下列條件時，您才可以執行下列步驟來檢視範例共用資源：
>
>* 已安裝範例內容
>* 執行AEM執行個體
>* 沒有已設定的自訂內容或其他連線埠
>

若要檢視範例共用資源，請參閱下列步驟：

1. 在您的AEM伺服器上開啟CRXDE Lite。
1. 瀏覽至此路徑 *[/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)*，以檢視範例共用資源。

   您可以檢視建立共用資源所需的所有屬性，如下圖所示：

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>共用資源發生變更時，應將共用資源上傳或匯出至AEM Mobile On-demand Services。
