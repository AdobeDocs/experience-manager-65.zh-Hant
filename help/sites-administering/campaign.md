---
title: 將AEM 6.5與Adobe Campaign整合
description: 瞭解AEM 6.5對與Adobe Campaign整合的支援。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: ab41e540-1d43-4fc2-99d4-621ff2290e77
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 243139ec-8e41-5296-a287-31343ab1bc0f
    internal-label: Integration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 2%
---

# 將AEM 6.5與Adobe Campaign整合{#integrating-with-adobe-campaign}

瞭解AEM 6.5對與Adobe Campaign整合的支援。

Adobe Campaign這一組解決方案可讓您跨所有線上及離線管道個人化並傳遞行銷活動。

>[!NOTE]
>
>本檔案說明如何將Adobe Campaign與AEM 6.5、內部部署或AMS託管的AEM解決方案整合。
>
>如需整合Adobe Campaign與雲端原生AEM解決方案AEM as a Cloud Service的詳細資訊，[請參閱此檔案。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/integrations/campaign.html?lang=zh-Hant)

## 與Adobe Campaign Classic整合 {#acc}

有數個Adobe Campaign Classic (ACC)版本。 是否支援與AEM整合，取決於您已實作的ACC版本，以及AEM是否安裝在Adobe管理服務(AMS)的內部部署中。

| ACC版本 | 與AEM 6.5 <br>內部部署整合 | 與AEM 6.5<br>AMS整合 |
|---|---|---|
| [v7](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=zh-Hant) | 支援 | 支援 |
| [v8使用者端主控台](https://experienceleague.adobe.com/docs/campaign-v8.html?lang=zh-Hant) | 支援 | 支援 |

以下檔案說明如何將AEM與Adobe Campaign Classic整合。

* [與Adobe Campaign Classic整合](/help/sites-administering/campaignonpremise.md) — 瞭解設定整合的逐步詳細資料。

下列其他檔案將說明如何使用整合。

* [電子郵件核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/email/introduction.html?lang=zh-Hant) — 瞭解在AEM中可用來編寫Campaign內容的標準電子郵件元件。
* [疑難排解您的Adobe Campaign Classic整合](/help/sites-administering/troubleshooting-campaignintegration.md) — 瞭解如何修正AEM-ACC整合最常見的問題。

## 與Adobe Campaign Standard整合 {#acs}

[Adobe Campaign Standard](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=zh-Hant) (ACS)與AEM的整合取決於AEM是否安裝在Adobe Manage Services (AMS)的內部部署。

| 與AEM 6.5 <br>內部部署整合 | 與AEM 6.5<br>AMS整合 |
|---|---|
| 支援 | 支援 |
| 支援 | 支援 |

以下檔案說明如何將AEM與Adobe Campaign Standard整合。

* [與Adobe Campaign Standard整合](/help/sites-administering/campaignstandard.md)

下列其他檔案將說明如何使用整合。

* [電子郵件核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/email/introduction.html?lang=zh-Hant)
