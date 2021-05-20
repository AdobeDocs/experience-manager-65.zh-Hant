---
title: 為IBM Content Manager配置連接器
seo-title: 為IBM Content Manager配置連接器
description: 配置Connector for IBM Content Manager以啟用AEM表單與IBM Content Manager之間的通信。
seo-description: 配置Connector for IBM Content Manager以啟用AEM表單與IBM Content Manager之間的通信。
uuid: 3d55169d-93e3-4d4e-b18b-2a3394e1de3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3094b178-3b1a-46b3-8fbd-c20388afa3a7
exl-id: 50f0c963-8007-4e2a-aa73-d99b97d9a1aa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---

# 為IBM Content Manager配置連接器{#configuring-connector-for-ibm-content-manager}

Connector for IBM Content Manager允許AEM Forms和IBM Content Manager之間通信。 有關其他背景資訊，請參閱[服務參考](https://www.adobe.com/go/learn_aemforms_services_63)中的「ECM連接器」。

## 配置IBM Content Manager連接{#configure-the-ibm-content-manager-connection}

1. 在管理控制台中，按一下「服務」>「 IBM Content Manager的連接器」。
1. 在「資料儲存名稱」框中，輸入要連接的IBM Content Manager資料儲存的名稱。 如果資料庫是本地的，請輸入資料庫的名稱。 如果資料庫是遠程的，請輸入其別名。
1. 在「用戶名」框中，輸入將連接到IBM Content Manager資料儲存庫的用戶的用戶ID。
1. 在「密碼」框中，輸入用戶的密碼。
1. （可選）在「別名連接字串」框中，輸入其他連接參數。 在大多數情況下，此方塊應為空。 有關其他資訊，請參閱IBM文檔。
1. 按一下「儲存」。

## 驗證服務設定{#validation-of-service-settings}

如果您輸入了不正確的dataStore別名、用戶名或密碼，則將獲得以下結果，具體取決於IBM Content Manager服務當前是否正在運行Content Repository Connector :

* 如果服務停止，則保存服務配置資訊時，不會顯示錯誤。 但是，下次啟動服務時，將引發異常，且服務將不啟動。
* 如果啟動服務，則在保存服務配置資訊時，服務會嘗試立即驗證憑據資訊。 在此情況下，會發生錯誤且不會儲存設定資訊。
