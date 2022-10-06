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

## 總覽 {#overview}

此功能可讓所有OSGi設定屬性以受保護的加密形式儲存，而非透明文字。 Web控制台UI中的表單用於使用系統寬加密主密鑰從明文建立加密文本。

已新增OSGi設定外掛程式支援，以便在服務使用屬性之前先解密屬性。

>[!NOTE]
>
>期望加密值的服務需要使用IsProtected檢查，以在嘗試解密值之前查看值是否已加密，因為可能已解密。

## 啟用加密支援 {#enabling-encryption-support}

這些步驟說明如何為Mail服務加密SMTP密碼。 您可以針對要加密的OSGI屬性完成這些步驟。

1. 前往AEM Web Console，網址為 *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. 在左上角，前往 **主 — 加密支援**

   ![chlimage_1-325](assets/chlimage_1-325.png)

1. 此 **Adobe Experience Manager Web控制台加密支援** 頁面。

   ![screen_shot_2018-08-01at113417am](assets/screen_shot_2018-08-01at113417am.png)

1. 在 **純文字** 欄位，輸入要保護的敏感資料的文本。
1. 選擇 **Protect**. 「受保護」文本將顯示為加密文本。

   ![screen_shot_2018-08-01at113844am](assets/screen_shot_2018-08-01at113844am.png)

1. 從步驟5複製受保護的文字，並貼到OSGI表單值中。 在此範例中，加密 **SMTP密碼** 已新增至 *Day CQ Mail Service*.

   ![screen_shot_2016-12-18at105809pm](assets/screen_shot_2016-12-18at105809pm.png)

1. 儲存Day CQ Mail Service屬性。 SMTP密碼現在會以加密值的形式傳送。

## 解密支援 {#decryption-support}

AEM現在提供設定外掛程式來解密設定屬性。 此AEM外掛程式會自動解密並擷取清除文字屬性。
