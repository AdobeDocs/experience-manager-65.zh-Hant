---
title: AEM Commerce - GDPR整備
description: 瞭解在AEM Commerce中處理GDPR請求的程式以及如何使用它們。
contentOwner: carlino
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# AEM Commerce - GDPR整備{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>以下各節以GDPR為例，但說明的詳細資料適用於所有資料保護和隱私權法規，例如GDPR和CCPA。

歐盟資料隱私權的一般資料保護規範於2018年5月起生效。 請參閱 [Adobe隱私權中心的GDPR頁面](https://business.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>另請參閱 [AEM GDPR整備](/help/managing/data-protection-and-privacy.md) 以取得更多詳細資料。

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

透過Adobe的開箱即用的Commerce整合，AEM成為體驗層，使用服務並傳送資料回以Headless模式執行的客戶商務平台。

對於某些商務平台，Adobe會儲存設定檔資訊( `/home/users`)和AEM中的商務權杖（以登入commerce平台）。 針對這些使用案例，請閱讀 [處理AEM平台的GDPR請求](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## 處理AEM Commerce的GDPR請求 {#handling-gdpr-requests-for-aem-commerce}

針對SalesforceCommerce Cloud整合，AEM Commerce不會儲存任何GDPR相關資訊。 將請求轉寄至 [Salesforce Cloud](https://documentation.b2c.commercecloud.salesforce.com/DOC1/index.jsp).

對於hybris和HCL WebSphere® Commerce整合，AEM中有些資料。 使用 [AEM平台GDPR指示](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) 並考量下列問題：

1. **我的資料儲存/使用於何處？** 快取的使用者設定檔資訊，例如，名稱、商務使用者識別碼、權杖、密碼和位址資料，如AEM中所示。
1. **我應該與誰共用涵蓋的GDPR資料？** AEM Commerce中GDPR相關資料的任何更新都不會儲存（上述相關設定檔資訊除外），而是透過代理傳回至Commerce平台。
1. **如何刪除我的使用者資料**？ 在AEM中刪除使用者設定檔，並在商務平台上叫用使用者刪除。

>[!NOTE]
>
>請檢視 [hybris wiki](https://wiki.hybris.com/) 或 [HCL WebSphere® Commerce檔案](https://help.hcltechsw.com/commerce/index.html)，如有必要。
