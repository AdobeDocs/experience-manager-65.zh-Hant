---
title: AEM商務- GDPR就緒性
seo-title: AEM商務- GDPR就緒性
description: 'null'
seo-description: 'null'
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---


# AEM Commerce - GDPR Readiness{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>GDPR在以下幾節中是以範例形式使用，但涵蓋的詳細資訊適用於所有資料保護和隱私權法規；例如GDPR、CCPA等。

歐盟的資料隱私權通用資料保護條例自2018年5月起生效。 如需詳細資訊，請參閱Adobe隱私權中心](https://www.adobe.com/privacy/general-data-protection-regulation.html)的[ GDPR頁面。

>[!NOTE]
>
>如需詳細資訊，請參閱[AEM GDPR Readiness](/help/managing/data-protection-and-privacy.md)。

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

在我們現成可用的「商務」整合中，AEM是體驗層，使用服務並將資料傳回以無頭模式執行的客戶商務平台。

對於某些商務平台，我們會在AEM中儲存設定檔資訊(`/home/users`)和商務Token（若要登入商務平台）。 如需這些使用案例，請閱讀[處理AEM平台的GDPR要求](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)。

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## 處理AEM Commerce的GDPR要求{#handling-gdpr-requests-for-aem-commerce}

對於Salesforces Commerce Cloud整合，AEM Commerce不會儲存任何GDPR相關資訊。 您應將請求轉送至[Salesforce Cloud](https://documentation.demandware.com/)。

對於hybris和IBM WebSphere整合，AEM中有一些資料。 您應使用[AEM Platform GDPR指示](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)並考慮以下問題：

1. **我的資料儲存／使用位置？** 快取的使用者設定檔資訊，例如名稱、商務使用者識別碼、Token、密碼、位址資料等，會從AEM中顯示。
1. **我要將涵蓋的GDPR資料分享給誰？** AEM Commerce中任何GDPR相關資料的更新都不會儲存（相關描述檔資訊除外，如上文所述），但是會轉送回商務平台。
1. **如何刪除我的使用者資料**?在AEM中刪除使用者設定檔，並在商務平台上叫用使用者刪除。

>[!NOTE]
>
>如有需要，請查看[hybris wiki](https://wiki.hybris.com/)或[Websphere商務檔案](https://www-01.ibm.com/support/docview.wss?uid=swg27036450)。

