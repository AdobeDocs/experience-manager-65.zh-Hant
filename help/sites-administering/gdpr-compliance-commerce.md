---
title: AEM商務 — GDPR整備
seo-title: AEM Commerce - GDPR Readiness
description: 「AEM商務 — GDPR整備」
seo-description: null
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
source-git-commit: 71842228dd3cb1ce3b79728912e8333d25fccefc
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---

# AEM商務 — GDPR整備{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>GDPR是以下各節中的範例，但涵蓋的詳細資訊適用於所有資料保護和隱私權法規；例如GDPR和CCPA。

歐盟資料隱私權一般資料保護規範自2018年5月起生效。 請參閱 [Adobe隱私權中心的GDPR頁面](https://business.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>請參閱 [AEM GDPR整備](/help/managing/data-protection-and-privacy.md) 以取得詳細資訊。

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

透過Adobe的現成可用商務整合，AEM成為體驗層，耗用服務並將資料傳回以無頭模式執行的客戶商務平台。

對於某些商務平台，Adobe會儲存設定檔資訊( `/home/users`)和AEM中的商務代號（登入商務平台）。 針對這些使用案例，請參閱 [處理AEM平台的GDPR請求](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## 處理AEM Commerce的GDPR請求 {#handling-gdpr-requests-for-aem-commerce}

針對SalesforceCommerce Cloud整合，AEM Commerce不會儲存任何GDPR相關資訊。 將請求轉送至 [Salesforce Cloud](https://documentation.b2c.commercecloud.salesforce.com/DOC1/index.jsp).

針對hybris和HCL WebSphere®商務整合，AEM中有些資料。 使用 [AEM Platform GDPR指示](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) 並考慮以下問題：

1. **我的資料儲存/使用位置為何？** 快取的使用者設定檔資訊，例如名稱、商務使用者識別碼、代號、密碼和位址資料，如AEM所示。
1. **我該將涵蓋的GDPR資料分享給誰？** AEM Commerce中任何GDPR相關資料的更新皆不會儲存（如上所述的相關設定檔資訊除外），但會保存回商務平台。
1. **如何刪除我的使用者資料**? 刪除AEM中的使用者設定檔，並在商務平台上叫用使用者刪除。

>[!NOTE]
>
>查看 [hybris wiki](https://wiki.hybris.com/) 或 [HCL WebSphere®商務文檔](https://help.hcltechsw.com/commerce/index.html)，如有必要。
