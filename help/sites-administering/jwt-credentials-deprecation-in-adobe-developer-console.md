---
title: Adobe Developer Console 中的 JWT 憑證已被取代
description: 了解 Adobe Developer Console 中已取代 JWT 憑證對 AEM 的影響
exl-id: f19a92de-ba6a-4f6d-9e12-60ad1bad2e74
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 72%

---

# Adobe Developer Console 中的 JWT 憑證已被取代 {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
> 如需詳細資訊，AEM as a Cloud Service應該參考[AEMaaCS版本](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html?lang=zh-Hant)的可比文章。

Adobe 客戶使用 [Adobe Developer Console](https://developer.adobe.com/console) 來產生可存取各種 API 的認證。客戶可以選擇各種認證類型，包括 OAuth 伺服器到伺服器和單頁應用程式。其中一種認證類型 (服務帳戶 (JWT) 認證) 已被已取代，取而代之的是 OAuth 伺服器到伺服器認證。2024 年 6 月 3 日或之後無法建立新的服務帳戶 (JWT) 認證，現有的 JWT 認證自 2025 年 1 月 27 日起將無法再使用。您可以[閱讀已取代項目的資訊](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration)。

本文提供一些關於Adobe Experience Manager (AEM) 6.5客戶應如何處理棄用的其他內容。

主要成果是AEM現在支援AEM的全新OAuth伺服器對伺服器認證。 您可能已收到一封電子郵件，其中包含移轉 JWT 認證的指示，現在可以完成此移轉。

以下區段列出客戶必須 (或在某些情況下不得) 將其服務帳戶 (JWT) 認證取代為 OAuth 伺服器對伺服器認證的情境，目前 AEM 支援這些情境。[了解如何](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration#migration-overview)移轉認證。

## 將 AEM 與其他 Adobe 解決方案整合 {#integrating-aem-with-other-adobe-solutions}

**動作**：移轉您的設定，因為 AEM 現在支援 OAuth 認證。

**相關的AEM版本**： Adobe Managed Services （Service Pack 21及更新版本）。

AEM客戶可使用AEM來設定與所有其他Adobe解決方案的整合。 例如 Adobe Target、Adobe Analytics 等。

![將 AEM 與其他解決方案整合](/help/sites-administering/assets/jwt-deprecation.png)

請參閱[設定AEM的IMS整合](/help/sites-administering/setting-up-ims-integrations-for-aem.md)，以取得以下操作的詳細資訊：

* 使用 OAuth 認證建立設定
* 將之前使用 JWT 認證建立的設定，移轉成使用 OAuth 認證

## Cloud Manager API {#cloud-manager-apis}

**動作**：確認何時可以將這些設定從 JWT 移轉到 OAuth 憑證。

**相關的AEM版本**： Adobe Managed Services （Service Pack 21及更新版本）。

客戶可建立 Adobe Developer Console 專案，以便叫用 [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/)。在已棄用的 JWT 認證於 2025 年 1 月到期之前，應將 Adobe Developer 專案中的認證移轉到 OAuth 伺服器對伺服器認證類型。
