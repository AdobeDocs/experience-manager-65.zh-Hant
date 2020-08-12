---
title: 透過動態媒體使CDN快取失效
description: 停用CDN（內容傳送網路）快取內容可讓您快速更新由動態媒體傳送的資產，而不需等待快取過期。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
translation-type: tm+mt
source-git-commit: 9e67e252348f471c052f6c3e88aea61d7a309241
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 4%

---


# 透過動態媒體使CDN快取失效 {#invalidating-cdn-cache-for-dm-assets}

動態媒體資產由CDN（內容傳送網路）快取，以便快速傳送給客戶。 不過，當您更新這些資產時，您可能會希望這些變更立即在您的網站上生效。 清除或停用CDN快取可讓您快速更新由動態媒體傳送的資產。 您不需等待快取使用TTL（存留時間）值（預設值為10小時）過期，而可從動態媒體內傳送要求，讓快取立即過期。

>[!IMPORTANT]
>
>這些步驟僅適用於AEM 6.5、Service Pack 6或更新版本中的Dynamic Media - Scene7模式。 <!-- If you are using Dynamic Media in AEM 6.5, Service Pack 5 or earlier [use the steps found here](/help/assets/invalidate-cdn-cache-dm-classic.md). -->

另請參閱 [動態媒體中的快取概觀](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)。

**若要使動態媒體資產的CDN快取內容無效：**

1. 在AEM 6.5.6或更新版本中，點選「工具> **[!UICONTROL 資產> CDN失效」。]**

   ![CDN驗證功能](/help/assets/assets-dm/cdn-invalidation-path.png)

1. 在「CDN失效」頁面上，設定您想要的選項：

   | 選項 | 說明 |
   | --- | --- |
   | **[!UICONTROL 使 CDN 中與影像預設集相關聯的資產失效]** | 勾選此選項時，您可以選取一或多個動態媒體資產（不論MIME類型），以及其相關的影像預設集，以便快取失效。<br>雖然您可以選取一或多個包含資產的檔案夾，但Adobe不建議使用此方法。 您應選擇個別資產檔案。<br>繼續下一步。 |
   | **[!UICONTROL 基於模板的失效]** | 勾選此選項時，您可以選取「動態媒體」資產和先前建立的「失效」範本。 使用此選項與 |
   | **[!UICONTROL 新增資產]** | BLA |
   | **[!UICONTROL 新增 URL]** | 手動將完整的URL路徑新增至您要使其快取無效的動態媒體資產。 |

1. 
1. 點選「下 **[!UICONTROL 一步」。]**
1. 
