---
title: AEM商務 — GDPR整備
seo-title: AEM商務 — GDPR整備
description: 「AEM商務 — GDPR整備」
seo-description: 'null'
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# AEM商務 — GDPR整備{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>GDPR是以下各節中的範例，但涵蓋的詳細資訊適用於所有資料保護和隱私權法規；例如GDPR、CCPA等

歐盟資料隱私權一般資料保護規範自2018年5月起生效。 如需詳細資訊，請參閱Adobe隱私權中心](https://www.adobe.com/privacy/general-data-protection-regulation.html)的[GDPR頁面。

>[!NOTE]
>
>如需詳細資訊，請參閱[AEM GDPR整備](/help/managing/data-protection-and-privacy.md) 。

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

在現成可用的商務整合中，AEM是體驗層，耗用服務，並將資料傳回以無頭模式執行的客戶商務平台。

對於某些商務平台，我們會在AEM中儲存設定檔資訊(`/home/users`)和商務代號（若要在商務平台中登入）。 若為這些使用案例，請參閱[處理AEM平台的GDPR請求](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)。

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## 處理AEM Commerce的GDPR請求{#handling-gdpr-requests-for-aem-commerce}

針對SalesforcesCommerce Cloud整合，AEM Commerce不會儲存任何GDPR相關資訊。 您應將要求轉送至[Salesforce Cloud](https://documentation.demandware.com/)。

對於hybris和IBM WebSphere整合，AEM中有些資料。 您應使用[AEM Platform GDPR指示](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)並考量下列問題：

1. **我的資料儲存/使用位置為何？** 快取的使用者設定檔資訊（例如名稱、商務使用者識別碼、代號、密碼、位址資料等）會從AEM中顯示。
1. **我該將涵蓋的GDPR資料分享給誰？** AEM Commerce中任何GDPR相關資料的更新皆不會儲存（除了如上所述的相關設定檔資訊外），但會保存回商務平台。
1. **如何刪除我的使用者資料**?刪除AEM中的使用者設定檔，並在商務平台上叫用使用者刪除。

>[!NOTE]
>
>如有需要，請查看[hybris wiki](https://wiki.hybris.com/)或[Websphere商務檔案](https://www-01.ibm.com/support/docview.wss?uid=swg27036450)。
