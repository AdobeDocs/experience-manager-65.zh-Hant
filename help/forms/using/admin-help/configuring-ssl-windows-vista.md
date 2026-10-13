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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%
---
# 在Windows Vista上設定SSL {#configuring-ssl-on-windows-vista}

若要在Windows Vista™上設定SSL，您需要具有RSA金鑰的SSL憑證以進行驗證。 您可以使用Java keytool來建立憑證。

>[!NOTE]
>
>Windows Vista無法搭配DSA金鑰使用。

您可以使用單一命令執行keytool，該命令包含建立憑證和金鑰存放區所需的所有資訊。

**建立SSL憑證**

1. 在命令提示字元中，瀏覽至&#x200B;*`[JAVA HOME]`*/bin並輸入下列命令以建立憑證和金鑰存放區：

   `keytool -genkey -keyalg RSA -dname "CN=`*主機名稱* `, OU=`*群組名稱* `, O=`*公司名稱* `,L=`*城市名稱* `, S=`*州別* `, C=`*國碼* `" -alias`*&quot;LC憑證&quot;* `-keypass` `key`*_* *密碼* `-keystore`*金鑰重新命名* `.keystore`

   >[!NOTE]
   >
   >將&#x200B;*`[JAVA_HOME]`取代為安裝JDK的目錄，並將斜體文字取代為與您的環境相對應的值。*

1. 鍵入`changeit`作為密碼。 此密碼是Java安裝的預設密碼，系統管理員可能已變更此密碼。
