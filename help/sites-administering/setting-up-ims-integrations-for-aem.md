---
title: 設定AEM的IMS整合
description: 瞭解如何設定AEM的IMS整合
source-git-commit: bca98907b79f12572879273ece41ec8d82fed1b8
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 79%

---


# 設定AEM的IMS整合 {#setting-up-ims-integrations-for-aem}


>[!NOTE]
>
>Adobe 客戶使用 [Adobe Developer Console](https://developer.adobe.com/console) 來產生可存取各種 API 的憑證。客戶可以選擇各種憑證類型，包括 OAuth 伺服器到伺服器和單頁應用程式。其中一種認證型別，服務帳戶(JWT)認證已遭取代，傾向使用Service Pack 20的OAuth伺服器對伺服器認證。 此變更可重新移植到舊版Service Pack，從Service Pack 11到Service Pack 20，並使用您可下載的Hotfix [此處](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/ims-jwt-compatibility-package-6.5-1.0.zip).

Adobe Experience Manager (AEM)可與許多其他Adobe解決方案整合。 例如 Adobe Target、Adobe Analytics 等。

整合會使用 IMS 整合，並設定 S2S OAuth。

* 您建立以下項目後：

   * [Developer Console 中的認證](#credentials-in-the-developer-console)

* 就可以：

   * 建立 (新的) [OAuth 設定](#creating-oauth-configuration)

   * [將現有 JWT 設定移轉到 OAuth 設定](#migrating-existing-JWT-configuration-to-oauth)

>[!CAUTION]
>
>先前是使用 [JWT 認證進行設定，現在 Adobe Developer Console 將淘汰這些認證](/help/sites-administering/jwt-credentials-deprecation-in-adobe-developer-console.md)。
>
>此類設定無法再建立或更新，但可以移轉至 OAuth 設定。

## Developer Console 中的認證 {#credentials-in-the-developer-console}

作為第一步，您必須在 Adobe Developer Console 中設定 OAuth 認證。

如需有關如何執行此操作的詳細資訊，請根據您的要求參閱 Developer Console 文件：

* 概觀：

   * [伺服器對伺服器驗證](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/)

* 建立新的 OAuth 認證：

   * [OAuth 伺服器對伺服器認證實作指南](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/)

* 將現有 JWT 認證移轉到 OAuth 認證：

   * [從服務帳戶 (JWT) 認證移轉至 OAuth 伺服器對伺服器認證](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)

例如：

![Developer Console 的 OAuth 認證](assets/ims-configuration-developer-console.png)

## 建立 OAuth 設定 {#creating-oauth-configuration}

若要使用 OAuth 建立新的 Adobe IMS 整合：

1. 在 AEM 中，導覽至「**工具**」、「**安全性**」、「**Adobe IMS 整合**」。

1. 選取「**建立**」。

1. 根據 [Developer Console](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/) 中的詳細資訊完成設定。例如：

   ![建立 OAuth 設定](assets/ims-create-oauth-configuration.png)

1. **儲存**&#x200B;您的變更。

## 將現有 JWT 設定移轉到 OAuth 設定 {#migrating-existing-JWT-configuration-to-oauth}

若要移轉基於 JWT 認證的現有 Adobe IMS 整合：

>[!NOTE]
>
>此範例顯示的是 Launch IMS 設定。

1. 在 AEM 中，導覽至「**工具**」、「**安全性**」、「**Adobe IMS 整合**」。

1. 選取需要移轉的 JWT 設定。JWT 設定以「**JWT 認證 (已淘汰)**」警告標示。

1. 選取「**屬性**」：

   ![選取 JWT 設定](assets/ims-migrate-jwt-select-configuration.png)

1. 該設定將以唯讀方式開啟：

   ![設定屬性 - 唯讀](assets/ims-migrate-jwt-properties-read-only.png)

1. 從「**驗證類型**」下拉選單中選取「**OAuth**」：

   ![選取驗證類型](assets/ims-migrate-jwt-authentication-type.png)

1. 系統將更新可用的屬性。使用 Developer Console 中的詳細資訊來填寫以下內容：

   ![完整的 OAuth 詳細資訊](assets/ims-migrate-jwt-complete-oauth-details.png)

1. 使用「**儲存並關閉**」保留您的更新。
您返回控制台時，「**JWT 認證 (已淘汰)**」警告就會消失。