---
title: 建立文章匯出設定
seo-title: 建立文章匯出設定
description: 請依照本頁瞭解如何從Adobe Experience Manager(AEM)匯出內容以上傳至AEM Mobile。
seo-description: 請依照本頁瞭解如何從Adobe Experience Manager(AEM)匯出內容以上傳至AEM Mobile。
uuid: 089bc15b-669e-4623-bdbb-fd9abf46e098
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: bc681589-5d46-44cd-888d-b0722a2fd006
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 建立文章匯出設定{#creating-article-export-configuration}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**先決條件**:
>
>在瞭解如何建立和修改共用資源之前，請參 [閱內容同步](/help/mobile/mobile-ondemand-contentsync.md) ，以瞭解基本概念。

AEM mobile使用者使用「內容同步」將即時內容匯出為靜態內容，以便用於「行動應用程式」，當內容從AEM mobile上傳至Mobile隨選服務時，就會發生此匯出。

上表 ***中提及的屬性dps-exportTemplate*** ，會定義應用程式匯出設定的路徑。 設定此屬性可建立和修改共用資源。

下列資源說明從Adobe Experience Manager(AEM)匯出內容以上傳至AEM Mobile。

文章有需要匯出和上傳的內容。 部分內容可在文章之間共用。

使用 [ContentSync](/help/mobile/mobile-ondemand-contentsync.md) 來收集內容並建立共 ***用資源套件*** 。

位於&lt;dps-exportTemplate>/ **dps-article>的ContentSync設定** ，應該設定為匯出裝置上屬性靜態演算所需的所有內容和文章。

>[!CAUTION]
>
>您只有在具備下列條件時，才能執行下列步驟來檢視範例共用資源：
>
>* 已安裝範例內容
>* 執行AEM例項
>* 未配置自定義上下文或不同埠
>



要查看共用資源示例，請參閱以下步驟：

1. 在AEM伺服器上開啟CRXDE Lite。
1. 瀏覽至此路 [徑/etc/contentsync/templates/dps-we-unlimited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article)，以檢視範例共用資源。

   您可以檢視建立共用資源所需的所有屬性，如下圖所示：

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>當文章內容變更時，應上傳或匯出至AEM Mobile On-Demand Services。

