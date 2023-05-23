---
title: Content Services
seo-title: Content Services
description: Content Services
seo-description: null
uuid: 7bd09c91-3931-400b-bdfc-b064b9ca9668
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 6a7e5472-cb57-4c78-b183-7c6dcac11a4e
exl-id: 955ffb1c-4fa9-43bb-8e5b-2df7f2d17951
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 3%

---

# Content Services{#content-services}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>Content Services功能僅用於預覽。
>
>隨著6.3 GA Service Pack 1的發佈，它可能會發生更改。

AEM Mobile內容服務是一種輕量級的功能，用於請求由管理的內AEM容。 這為所有應用程式開發人員提供了一種檢索內容的高效能方法，而不必對內容儲存庫(AEMJCR)和Web框架(Sling)有深入的瞭解。 它允許請求應用程式與內容儲存庫分離。

Content Services引入了幾種新構AEM造，使開發人員能夠訪問受管AEM理的內容，而不需要知道該內容的儲存庫結構。

這些結構對於保持靈活性和通過在托管內容和使用內容的移動應用之間提供抽象層AEM來實現未來擴展是必不可少的。 這允AEM許Content Services在本機應用程式的內容要求和內容儲存庫之間作為抽AEM像層工作。

Content Services可以將內容作為資產、打包HTML(HTML/CSS/JS)或渠道獨立內容提供。

>[!CAUTION]
>
>**必備條件:**
>
>在開始使用Content Services之前，請確保啟用Content Services標誌。 若要在應用中啟用模型的建立和管理，您需要在配置瀏覽器中啟用資料模型。
>
>請參閱 **[管理Content Services](/help/mobile/developing-content-services.md)** 和 [配置瀏覽器](/help/sites-administering/configurations.md) 的子菜單。

![chlimage_1-143](assets/chlimage_1-143.png)

在配置瀏覽器中設定Content Services標誌並啟用資料模型後，請參閱以下資源以開始使用AEM MobileContent Services，瞭解Content Services概念，如模型管理、實體管理，然後是AEM MobileContent Services的內容交付/呈現。

* 儲存庫中的模型
* 呈現和交付
