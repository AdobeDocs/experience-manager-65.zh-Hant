---
title: Content Services
seo-title: 內容服務
description: 內容服務
seo-description: 'null'
uuid: 7bd09c91-3931-400b-bdfc-b064b9ca9668
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 6a7e5472-cb57-4c78-b183-7c6dcac11a4e
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 3%

---


# Content Services{#content-services}

>[!NOTE]
>
>Adobe建議針對需SPA要單頁應用程式架構用戶端轉換的專案使用編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>「內容服務」功能僅記錄在案，僅供預覽之用。
>
>它可能會隨6.3 GA Service Pack 1的發行而改變。

AEM Mobile內容服務是輕量型的功能，可用來要求由管理的內容AEM。 這為所有應用程式開發人員提供高效能的方式來擷取內容，而不需具備內容存放庫(JCR)AEM和Web架構(Sling)的深入知識。 它允許請求應用程式與內容儲存庫分離。

Content Services引入了幾種新AEM的結構，允許開發人員訪問受AEM管理的內容，而不需知道該內容的儲存庫結構。

這些結構是維持靈活性和未來擴充的必要條件，方法是在受管理的內容和使用內容的行動應用AEM程式之間提供抽象層。 這可讓AEMContent Services在原生應用程式的內容需求和內容儲存庫之間，以抽象層AEM的形式運作。

Content Services可將內容以資產、封裝的HTML(HTML/CSS/JS)或頻道無關的內容形式提供。

>[!CAUTION]
>
>**必備條件:**
>
>開始使用Content Services之前，請確定啟用Content Services標幟。 若要在您的應用程式中建立和管理模型，您必須在「設定瀏覽器」中啟用資料模型。
>
>如需詳細資訊，請參閱&#x200B;**[管理內容服務](/help/mobile/developing-content-services.md)**&#x200B;和[組態瀏覽器](/help/sites-administering/configurations.md)檔案。

![chlimage_1-143](assets/chlimage_1-143.png)

在設定Content Services標幟並啟用「設定瀏覽器」中的資料模型後，請參閱下列資源以開始使用AEM Mobile內容服務、熟悉內容服務概念，例如模型管理、實體管理，接著是AEM Mobile內容服務的內容傳送／轉譯。

* 儲存庫中的模型
* 演算和傳送
