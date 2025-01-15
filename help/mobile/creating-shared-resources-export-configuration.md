---
title: 建立共用資源匯出設定
description: 請依照本頁面的說明了解如何從Adobe Experience Manager (AEM)匯出共用資源，以便上傳至AEM Mobile。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 576b4567-c7b6-4196-84e7-47e980637540
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# 建立共用資源匯出設定{#creating-shared-resources-export-configuration}

{{ue-over-mobile}}

>[!CAUTION]
>
>**先決條件**：
>
>在瞭解如何建立和修改共用資源之前，請參閱[Content Sync](/help/mobile/mobile-ondemand-contentsync.md)瞭解基本概念。

Adobe Experience Manager (AEM) Mobile使用者會使用Content Sync將即時內容匯出至靜態內容，以供行動應用程式使用，此匯出作業會在內容從AEM Mobile上傳至Mobile On-Demand Services時發生。

上表提及的屬性&#x200B;***dps-exportTemplate***&#x200B;定義應用程式匯出設定的路徑。 設定此屬性以建立和修改共用資源。

下列資源說明如何從AEM匯出共用資源以上傳至AEM Mobile。

共用HTML資源可讓文章共用原本會針對所有文章複製的HTML資源，並可包含圖示、字型、JavaScript和css。

在&#x200B;**&lt;dps-exportTemplate>/dps-HTMLResources>**&#x200B;找到的內容同步設定應該設定為匯出內容與裝置上的內容靜態轉譯所需的所有文章。

>[!CAUTION]
>
>只有具備下列條件時，您才可以執行以下步驟來檢視範例共用資源：
>
>* 已安裝範例內容
>* 執行AEM執行個體
>* 沒有已設定的自訂內容或其他連線埠
>

若要檢視範例共用資源，請參閱下列步驟：

1. 在您的AEM伺服器上開啟CRXDE Lite。
1. 瀏覽至此路徑&#x200B;*[/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)*，以檢視範例共用資源。

   您可以檢視建立共用資源所需的所有屬性，如下圖所示：

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>共用資源發生變更時，應將共用資源上傳或匯出至AEM Mobile On-demand Services。
