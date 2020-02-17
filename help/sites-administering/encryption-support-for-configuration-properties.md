---
title: 配置屬性的加密支援
seo-title: 配置屬性的加密支援
description: 'null'
seo-description: 'null'
uuid: 26dc5e46-9332-4d9b-8874-895b90391e8c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: security
discoiquuid: 4e08c297-aa4b-44cf-84c8-1e11582d9ebb
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# 配置屬性的加密支援{#encryption-support-for-configuration-properties}

## 概覽 {#overview}

此功能可讓所有OSGi組態屬性儲存在受保護的加密表單中，而非明文。 Web控制台UI中的表單用於使用系統寬加密主密鑰從明文建立加密文本。

已新增OSGi Configuration Plugin支援，以便在服務使用屬性之前先解密屬性。

>[!NOTE]
>
>預期加密值的服務需要使用IsProtected檢查，以在嘗試解密前查看該值是否已加密，因為可能已解密。

## 啟用加密支援 {#enabling-encryption-support}

這些步驟說明如何加密郵件服務的SMTP密碼。 您可以針對要加密的OSGI屬性完成這些步驟。

1. 前往AEM Web Console(網址 *為https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr)*
1. 在左上角，轉至「主——加 **密支援」**

   ![chlimage_1-325](assets/chlimage_1-325.png)

1. 此時 **會顯示「Adobe Experience Manager Web Console加密支援** 」頁面。

   ![screen_shot_2018-08-01at113417am](assets/screen_shot_2018-08-01at113417am.png)

1. 在「純 **文字** 」欄位中，輸入要保護的敏感資料文字。
1. 選擇 **保護**。 「受保護」文字會顯示為加密文字。

   ![screen_shot_2018-08-01at113844am](assets/screen_shot_2018-08-01at113844am.png)

1. 從步驟#5複製受保護的文字，並貼入OSGI表單值。 在此示例中，加密的 **SMTP密碼將添加到** Day CQ mail服務中 **。

   ![screen_shot_2016-12-18at105809pm](assets/screen_shot_2016-12-18at105809pm.png)

1. 保存Day CQ mail服務屬性。 SMTP密碼現在將作為加密值發送。

## 解密支援 {#decryption-support}

AEM現在提供Configuration Plugin以解密設定屬性。 此AEM外掛程式會自動解密並擷取清除文字屬性。
