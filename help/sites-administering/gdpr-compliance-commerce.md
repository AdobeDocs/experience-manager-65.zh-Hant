---
title: 商AEM務- GDPR就緒性
seo-title: 商AEM務- GDPR就緒性
description: 「商AEM務- GDPR就緒性」
seo-description: 'null'
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# 商AEM務- GDPR就緒{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>GDPR在以下幾節中是以範例形式使用，但涵蓋的詳細資訊適用於所有資料保護和隱私權法規；例如GDPR、CCPA等。

歐盟的資料隱私權通用資料保護條例自2018年5月起生效。 如需詳細資訊，請參閱Adobe隱私中心](https://www.adobe.com/privacy/general-data-protection-regulation.html)的[ GDPR頁面。

>[!NOTE]
>
>如需詳細資訊，請參AEM閱[ GDPR Readiness](/help/managing/data-protection-and-privacy.md)。

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

在我們現成可用的商務整合中，AEM是體驗層、消費服務並將資料傳回以無頭模式執行的客戶商務平台。

對於某些商務平台，我們會將描述檔資訊(`/home/users`)和商務Token（若要登入商務平台）儲存在AEM中。 有關這些使用案例，請閱讀[處理平台的GDPR請AEM求](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)。

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## 處理商務的AEMGDPR請求{#handling-gdpr-requests-for-aem-commerce}

對於SalesforcesCommerce Cloud整合，AEM Commerce不會儲存任何GDPR相關資訊。 您應將請求轉送至[Salesforce Cloud](https://documentation.demandware.com/)。

對於hybris和IBM WebSphere的整合，中有一些資料AEM。 您應使用[AEM平台GDPR說明](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)並考慮以下問題：

1. **我的資料儲存／使用位置？** 快取的使用者設定檔資訊，例如名稱、商務使用者識別碼、Token、密碼、位址資料等，如AEM中。
1. **我要將涵蓋的GDPR資料分享給誰？** 商務中任何GDPR相關資料的更新都不會AEM儲存（相關個人資料資訊除外，如上文所述），但是會傳回商務平台。
1. **如何刪除我的使用者資料**?刪除中的用戶配置AEM檔案，並在商務平台上調用用戶刪除。

>[!NOTE]
>
>如有需要，請查看[hybris wiki](https://wiki.hybris.com/)或[Websphere商務檔案](https://www-01.ibm.com/support/docview.wss?uid=swg27036450)。

