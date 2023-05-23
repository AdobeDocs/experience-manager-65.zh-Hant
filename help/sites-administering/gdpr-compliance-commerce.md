---
title: 商AEM業 — GDPR就緒性
seo-title: AEM Commerce - GDPR Readiness
description: "商AEM業 — GDPR就緒性"
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

# 商AEM業 — GDPR就緒性{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>GDPR在以下各節中用作示例，但所涵蓋的詳細資訊適用於所有資料保護和隱私法規；如GDPR和CCPA。

歐盟關於資料隱私權的一般資料保護條例自2018年5月起生效。 查看 [Adobe隱私中心的GDPR頁](https://business.adobe.com/privacy/general-data-protection-regulation.html)。

>[!NOTE]
>
>請參閱 [GDPR就緒AEM性](/help/managing/data-protection-and-privacy.md) 的上界。

![screen_shot_2018-03-22at11606](assets/screen_shot_2018-03-22at111606.jpg)

通過Adobe的現成Commerce整合，AEM體驗層、消費服務以及將資料發回以無頭模式運行的客戶商務平台。

對於某些商務平台，Adobe儲存配置檔案資訊( `/home/users`)和商業令牌（要在商業平台中登錄）AEM。 對於這些使用案例，請閱讀 [處理平台的GDPR請AEM求](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)。

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## 處理商務的GDPR請AEM求 {#handling-gdpr-requests-for-aem-commerce}

對於SalesforceCommerce Cloud整合，AEM Commerce不儲存任何GDPR相關資訊。 將請求轉發到 [Salesforce雲](https://documentation.b2c.commercecloud.salesforce.com/DOC1/index.jsp)。

對於hybris和HCL WebSphere® Commerce整合，中包含一些數AEM據。 使用 [平AEM台GDPR說明](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) 並考慮以下問題：

1. **我的資料儲存/使用在哪裡？** 快取的用戶配置檔案資訊，如名稱、商業用戶標識符、令牌、密碼和地址資料，如中所AEM示。
1. **與誰共用所涵蓋的GDPR資料？** Commerce中任何GDPR相關資料的更新都不會被儲存（除上面提到的相關配置檔案資訊外），而是被代理回商務平台。
1. **如何刪除我的用戶資料**? 刪除中的用戶配置AEM檔案，並調用商務平台上的用戶刪除。

>[!NOTE]
>
>看看 [碎片維基](https://wiki.hybris.com/) 或 [HCL WebSphere® Commerce文檔](https://help.hcltechsw.com/commerce/index.html)的雙曲餘切值。
