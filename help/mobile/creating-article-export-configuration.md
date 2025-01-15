---
title: 建立文章匯出設定
description: 請依照本頁面的說明了解如何從Adobe Experience Manager (AEM)匯出內容以上傳至AEM Mobile。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 5295f383-3b46-4456-9177-65de68e39a85
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# 建立文章匯出設定{#creating-article-export-configuration}

{{ue-over-mobile}}

>[!CAUTION]
>
>**先決條件**：
>
>在瞭解如何建立和修改共用資源之前，請參閱[Content Sync](/help/mobile/mobile-ondemand-contentsync.md)瞭解基本概念。

AEM Mobile使用者會使用Content Sync將即時內容匯出至靜態內容，以供行動應用程式使用，此匯出作業會在內容從AEM Mobile上傳至Mobile On-Demand Services時發生。

上表提及的屬性&#x200B;***dps-exportTemplate***&#x200B;定義應用程式匯出設定的路徑。 設定此屬性以建立和修改共用資源。

下列資源說明如何從Adobe Experience Manager (AEM)匯出內容以上傳至AEM Mobile。

文章包含需要匯出和上傳的內容。 部分內容可在文章之間共用。

使用[ContentSync](/help/mobile/mobile-ondemand-contentsync.md)將內容收集在一起，並建立&#x200B;***共用資源***&#x200B;套件。

在&#x200B;**&lt;dps-exportTemplate>/dps-article>**&#x200B;找到的ContentSync設定應設定為匯出內容與裝置上靜態呈現內容所需的文章。

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
1. 瀏覽至此路徑[/etc/contentsync/templates/dps-we-unlimited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article)，以檢視範例共用資源。

   您可以檢視建立共用資源所需的所有屬性，如下圖所示：

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>當文章內容變更時，應將文章上傳或匯出至AEM Mobile On-demand Services。
