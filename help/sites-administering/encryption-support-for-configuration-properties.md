---
title: 設定屬性的加密支援
seo-title: Encryption Support for Configuration Properties
description: 瞭解AEM中提供的設定屬性加密支援。
seo-description: null
uuid: 26dc5e46-9332-4d9b-8874-895b90391e8c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: security
discoiquuid: 4e08c297-aa4b-44cf-84c8-1e11582d9ebb
exl-id: 3c3db1c8-5b22-45dd-aeaf-5cf830a9486b
source-git-commit: e54c1d422f2bf676e8a7b0f50a101e495c869c96
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# 設定屬性的加密支援{#encryption-support-for-configuration-properties}

## 概觀 {#overview}

此功能允許所有OSGi設定屬性以受保護的加密格式儲存，而非純文字。 Web主控台UI中的表單是用來使用全系統加密主金鑰，從純文字建立加密文字。

已新增OSGi設定外掛程式支援，以便在服務使用屬性之前將其解密。

>[!NOTE]
>
>預期加密值的服務必須使用IsProtected檢查，以檢視值是否已加密，然後再嘗試解密，因為值可能已經解密。

## 啟用加密支援 {#enabling-encryption-support}

這些步驟顯示如何加密Mail服務的SMTP密碼。 您可以針對要加密的OSGI屬性完成這些步驟。

1. 前往AEM Web主控台，位於 *https://&lt;serveraddress>：&lt;serverport>/system/console/configMgr*
1. 在左上角，前往 **主要 — 加密支援**

   ![chlimage_1-325](assets/chlimage_1-325.png)

1. 此 **Adobe Experience Manager Web主控台Crypto支援** 頁面隨即顯示。

   ![screen_shot_2018-08-01at113417am](assets/screen_shot_2018-08-01at113417am.png)

1. 在 **純文字** 欄位中，輸入要保護的敏感資料文字。
1. 選取 **Protect**. 受保護文字會顯示為加密文字。

   ![screen_shot_2018-08-01at113844am](assets/screen_shot_2018-08-01at113844am.png)

1. 從Step#5複製受保護的文字並貼到OSGI表單值中。 在此範例中，已解密的 **SMTP密碼** 新增至 *Day CQ郵件服務*.

   ![screen_shot_2016-12-18at105809pm](assets/screen_shot_2016-12-18at105809pm.png)

1. 儲存Day CQ Mail Service屬性。 SMTP密碼現在會以加密值的形式傳送。

## 解密支援 {#decryption-support}

AEM現在提供設定外掛程式，以解密設定屬性。 此AEM外掛程式會自動解密及擷取純文字屬性。
