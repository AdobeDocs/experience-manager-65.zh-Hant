---
title: Adobe Developer Console 中的 JWT 憑證已被取代
description: 了解 Adobe Developer Console 中已取代 JWT 憑證對 AEM 的影響
exl-id: f19a92de-ba6a-4f6d-9e12-60ad1bad2e74
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 58%

---

# Adobe Developer Console 中的 JWT 憑證已被取代 {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
> AEM as a Cloud Service應參考 [本文](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html) 以取得詳細資訊。

Adobe 客戶使用 [Adobe Developer Console](https://developer.adobe.com/console) 來產生可存取各種 API 的憑證。客戶可以選擇各種憑證類型，包括 OAuth 伺服器到伺服器和單頁應用程式。其中一種憑證類型 (服務帳戶 (JWT) 憑證) 已被已取代，取而代之的是 OAuth 伺服器到伺服器憑證。2024 年 6 月 3 日或之後無法建立新的服務帳戶 (JWT) 憑證，現有的 JWT 憑證自 2025 年 1 月 27 日起將無法再使用。您可以[閱讀已取代項目的資訊](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)。

本文提供一些關於AEM 6.5客戶應如何處理棄用的其他內容。

目前的主要要點是 AEM 功能尚未支援新的 OAuth 伺服器到伺服器憑證。即將提供支援 — 如果您執行的是最新的Service Pack 20或更低版本（Service Pack 21及更高版本會自動包含該版本），請在2024年4月底之前透過特別相容性套件安裝至AEM 6.5。 您可能已收到說明移轉 JWT 憑證的電子郵件，但請放心，您可以而且應該推遲憑證移轉，直到 AEM 支援新的 OAuth 伺服器到伺服器憑證類型。

以下各節列出客戶必須（或在某些情況下不得）在4月底獲得AEM支援後，使用OAuth伺服器對伺服器憑證取代其服務帳戶(JWT)憑證的案例。 [了解](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview)將來更換憑證的方法。

## 將 AEM 與其他 Adobe 解決方案整合 {#integrating-aem-with-other-adobe-solutions}

**動作**：等候移轉，直到2024年4月下旬AEM支援時為止。

**相關AEM版本**：AdobeManaged Services （Service Pack 20及以下版本）。


AEM 客戶使用 AEM Author UI 設定所有與其他 Adobe 解決方案的整合。例如，Adobe Target、Adobe Analytics、Adobe Launch、AFCS 等。

![將 AEM 與其他解決方案整合](/help/sites-administering/assets/jwt-deprecation.png)

例如，以下是設定與 Adobe Target 整合的[說明](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=zh-Hant)。中的API金鑰 [在AEM中完成IMS設定](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html#completing-the-ims-configuration-in-aem) 四月底的AEM支援這些認證後，區段應該移轉至OAuth伺服器對伺服器認證型別。 這些指示將會在4月下旬更新，以幫助您套用新的OAuth伺服器對伺服器認證。

## Cloud Manager API {#cloud-manager-apis}

**動作**：等候移轉，直到2024年4月下旬AEM支援時為止。

**相關AEM版本**：AdobeManaged Services （Service Pack 20及以下版本）。

客戶可建立 Adobe Developer Console 專案，以便叫用 [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/)。AEM 和 Cloud Manager 支援憑證後，Adobe Developer 專案中的憑證應移轉到 OAuth 伺服器到伺服器憑證類型。
