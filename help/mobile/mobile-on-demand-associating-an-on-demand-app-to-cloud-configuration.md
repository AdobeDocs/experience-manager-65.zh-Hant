---
title: 雲端設定
seo-title: Cloud Configuration
description: 將按需應用與雲配置相關聯AEM允許Adobe Experience Manager()通過建立雙向連結直接與移動按需托管項目通信。 請按照此頁瞭解詳細資訊。
seo-description: Associating an On-Demand App to a Cloud Configuration allows Adobe Experience Manager (AEM) to communicate directly with a Mobile On-Demand hosted project by establishing a two way link. Follow this page to learn more.
uuid: f377f2af-864b-43df-9d42-4a5fd6cd70d5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: d0d29b99-53d4-4b0d-947b-39d91b381de7
exl-id: 37428543-c310-4712-a4ec-1f482579fb4b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 3%

---

# 雲端設定{#cloud-configuration}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

將按需應用與雲配置相關聯AEM允許Adobe Experience Manager()通過建立雙向連結直接與移動按需托管項目通信。 通過將應用連結到移動按需項目，您將能夠執行內容建立，如文章、橫幅和收藏，AEM但也可將該內容提供給移動按需。

從此，發佈、預覽和管理內容成為可能。 您還可以將現有的Mobile On-Demand內容導入AEM並執行內容編輯。

## 設定雲配置 {#setting-up-cloud-configuration}

>[!CAUTION]
>
>在開始為按需應用配置雲配置之前，您必須熟悉AEM Mobile設定和配置AEM Mobile On-demand Services客戶端。
>
>有關詳細資訊，請參閱 [設定AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md) 中。

要配置Mobile On-DemandCloud Services，請按一下右上角的頂齒輪 **管理連接** 從應用儀表板中平鋪。

您應熟悉應用儀表板和可用磁貼。 請參閱 [AEM Mobile應用程式儀表板](/help/mobile/mobile-apps-ondemand-application-dashboard.md) 的子菜單。

### 設定指向雲配置的連結 {#setting-up-link-to-cloud-configuration}

>[!CAUTION]
>
>確保您擁有現有的按需客戶端和雲配置。
>
>有關詳細資訊，請參閱 [設定AEM Mobile On-demand Services](/help/mobile/aem-mobile-setup.md) 中。

以下步驟介紹設定指向雲配置的連結：

1. 從 **移動**&#x200B;選項 **應用** 然後從目錄中獲取您的Mobile On-Demand應用。
1. 按一下 **管理連接** 平鋪。

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 輸入現有配置或通過輸入 **配置標題**。 **設備ID**, **設備令牌**。

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. 一旦 **設備ID** 和 **設備令牌** 驗證後，從清單中選擇您的按需項目。

   按一下 **提交**。

   ![chlimage_1-67](assets/chlimage_1-67.png)

   的 **管理連接** 磁貼顯示雲配置。

   ![chlimage_1-68](assets/chlimage_1-68.png)

   >[!CAUTION]
   >
   >如果您嘗試更改此應用與哪個項目關聯，則在儀表板中切換項目時，您將收到有關內容完整性問題的警告，如下圖所示：

   ![chlimage_1-69](assets/chlimage_1-69.png)

### 後續步驟 {#the-next-steps}

為應用配置雲配置後，請參閱以下管理內容的資源：

* [管理文章](/help/mobile/mobile-on-demand-managing-articles.md)
* [管理橫幅](/help/mobile/mobile-on-demand-managing-banners.md)
* [管理集合](/help/mobile/mobile-on-demand-managing-collections.md)
* [正在上載共用資源](/help/mobile/mobile-on-demand-shared-resources.md)
* [發佈/取消發佈內容](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [使用印前檢查預覽](/help/mobile/aem-mobile-manage-ondemand-services.md)
