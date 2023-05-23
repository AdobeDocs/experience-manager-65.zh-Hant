---
title: 配置屬性的加密支援
seo-title: Encryption Support for Configuration Properties
description: 配置屬性的加密支援
seo-description: null
uuid: 26dc5e46-9332-4d9b-8874-895b90391e8c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: security
discoiquuid: 4e08c297-aa4b-44cf-84c8-1e11582d9ebb
exl-id: 3c3db1c8-5b22-45dd-aeaf-5cf830a9486b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# 配置屬性的加密支援{#encryption-support-for-configuration-properties}

## 概觀 {#overview}

此功能允許所有OSGi配置屬性以受保護的加密形式而不是明文形式儲存。 Web控制台UI中的表單用於使用系統範圍的加密主密鑰從明文建立加密文本。

添加了OSGi配置插件支援，以便在服務使用屬性之前對其進行解密。

>[!NOTE]
>
>需要加密值的服務需要使用IsProtected檢查，以在嘗試解密值之前查看該值是否已加密，因為可能已解密。

## 啟用加密支援 {#enabling-encryption-support}

這些步驟說明如何加密郵件服務的SMTP密碼。 您可以完成要加密的OSGI屬性的這些步驟。

1. 轉到AEMWeb控制台 *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. 在左上角，轉到 **主 — 加密支援**

   ![chlimage_1-325](assets/chlimage_1-325.png)

1. 的 **Adobe Experience ManagerWeb控制台加密支援** 的上界。

   ![screen_shot_2018-08-01at113417am](assets/screen_shot_2018-08-01at113417am.png)

1. 在 **純文字檔案** 欄位中，輸入要保護的敏感資料的文本。
1. 選擇 **Protect**。 「受保護」文本顯示為加密文本。

   ![screen_shot_2018-08-01at113844am](assets/screen_shot_2018-08-01at113844am.png)

1. 從步驟5複製受保護文本，並將其貼上到OSGI窗體值中。 在此示例中，加密 **SMTP密碼** 添加到 *第CQ天郵件服務*。

   ![screen_shot_2016-12-18at105809pm](assets/screen_shot_2016-12-18at105809pm.png)

1. 保存第CQ天郵件服務屬性。 SMTP密碼現在將作為加密值發送。

## 解密支援 {#decryption-support}

現在AEM提供一個配置插件來解密配置屬性。 此插AEM件將自動解密和檢索明文屬性。
