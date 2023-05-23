---
title: 在Windows Vista上配置SSL
seo-title: Configuring SSL on Windows Vista
description: 瞭解如何在Windows Vista上配置SSL。
seo-description: Learn how to configure SSL on Windows Vista.
uuid: 20bfcefb-ec84-4c55-bceb-6af106d883d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 667645a0-53d0-4f9b-a0ba-cc7e366a23a1
exl-id: 36c4300d-7a44-41f4-b294-06f32bb01686
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# 在Windows Vista上配置SSL {#configuring-ssl-on-windows-vista}

要在Windows Vista™上配置SSL，您需要使用帶RSA密鑰的SSL證書進行身份驗證。 可以使用Java鍵工具建立證書。

>[!NOTE]
>
>Windows Vista無法使用DSA密鑰。

可以使用包含建立證書和密鑰庫所需的所有資訊的單個命令來運行keytool。

**建立SSL證書**

1. 在命令提示符下，導航到 *`[JAVA HOME]`*/bin並鍵入以下命令以建立證書和密鑰庫：

   `keytool -genkey -keyalg RSA -dname "CN=`*主機名* `, OU=`*組名稱* `, O=`*公司名稱* `,L=`*城市名稱* `, S=`*州* `, C=`*國家/地區代碼* `" -alias`*&quot;LC證書&quot;* `-keypass` `key`*_* *密碼* `-keystore`*鍵更名* `.keystore`

   >[!NOTE]
   >
   >替換 *`[JAVA_HOME]`將JDK安裝到的目錄中，並將斜體文本替換為與您的環境對應的值。*

1. 類型 `changeit` 的雙曲餘切值。 此密碼是Java安裝的預設密碼，系統管理員可能已更改了該密碼。
