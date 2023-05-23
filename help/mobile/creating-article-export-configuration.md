---
title: 建立項目導出配置
seo-title: Creating Article Export Configuration
description: 關於從Adobe Experience Manager()導出內容以上載到AEMAEM Mobile，請訪問此頁。
seo-description: Follow this page to learn about exporting content from Adobe Experience Manager (AEM) for upload to AEM Mobile.
uuid: 089bc15b-669e-4623-bdbb-fd9abf46e098
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: bc681589-5d46-44cd-888d-b0722a2fd006
exl-id: 5295f383-3b46-4456-9177-65de68e39a85
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---

# 建立項目導出配置{#creating-article-export-configuration}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**必備條件**:
>
>在瞭解有關建立和修改共用資源之前，請參閱 [內容同步](/help/mobile/mobile-ondemand-contentsync.md) 瞭解基本概念。

AEM Mobile用戶使用內容同步將即時內容導出為靜態內容以用於移動應用，當內容從AEM Mobile上載到移動按需服務時，會出現此導出。

屬性 ***dps-exportTemplate*** 如上表所述，定義應用導出配置的路徑。 將此屬性設定為建立和修改共用資源。

以下資源介紹將內容從Adobe Experience Manager(AEM)導出以上載到AEM Mobile。

文章包含需要導出和上載的內容。 某些此內容可以在文章之間共用。

使用 [內容同步](/help/mobile/mobile-ondemand-contentsync.md) 將內容收集在一起並建立 ***共用資源*** 檔案。

在以下位置找到的ContentSync配置 **&lt;dps-exporttemplate>/dps-article>** 應配置為導出設備上屬性靜態呈現所需的所有內容和項目。

>[!CAUTION]
>
>只有在以下情況下，您才能執行以下步驟來查看示例共用資源：
>
>* 已安裝示例內容
>* 運行實AEM例
>* 未配置自定義上下文或其他埠
>


要查看共用資源示例，請參閱以下步驟：

1. 在伺服器上打AEM開CRXDE Lite。
1. 瀏覽到此路徑 [/etc/contentsync/templates/dps-we-unlimited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article)，以查看共用資源示例。

   您可以查看建立共用資源所需的所有屬性，如下圖所示：

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>當文章內容更改時，應將文章上載或導出到AEM Mobile On-demand Services。
