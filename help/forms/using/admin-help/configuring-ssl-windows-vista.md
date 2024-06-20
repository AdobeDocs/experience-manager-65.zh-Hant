---
title: 在Windows Vista上設定SSL
description: 瞭解如何在Windows Vista上設定SSL。 使用並執行Java Keytool來產生包含RSA金鑰的SSL憑證以進行驗證。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 36c4300d-7a44-41f4-b294-06f32bb01686
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# 在Windows Vista上設定SSL {#configuring-ssl-on-windows-vista}

若要在Windows Vista™上設定SSL，您需要具有RSA金鑰的SSL憑證以進行驗證。 您可以使用Java keytool來建立憑證。

>[!NOTE]
>
>Windows Vista無法搭配DSA金鑰使用。

您可以使用單一命令執行keytool，該命令包含建立憑證和金鑰存放區所需的所有資訊。

**建立SSL憑證**

1. 在命令提示字元中，瀏覽至 *`[JAVA HOME]`*/bin ，然後輸入以下命令來建立憑證和金鑰存放區：

   `keytool -genkey -keyalg RSA -dname "CN=`*主機名稱* `, OU=`*群組名稱* `, O=`*公司名稱* `,L=`*城市名稱* `, S=`*狀態* `, C=`*國家/地區代碼* `" -alias`*「LC憑證」* `-keypass` `key`*_* *密碼* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >取代 *`[JAVA_HOME]`使用安裝JDK的目錄，並將斜體文字取代為與您的環境相對應的值。*

1. 型別 `changeit` 作為密碼。 此密碼是Java安裝的預設密碼，系統管理員可能已變更此密碼。
