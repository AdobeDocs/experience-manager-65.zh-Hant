---
title: 為IBM Content Manager設定連接器
seo-title: Configuring Connector for IBM Content Manager
description: 設定IBM Content Manager的連接器，以啟用AEM Forms與IBM Content Manager之間的通訊。
seo-description: Configure the Connector for IBM Content Manager to enable communication between AEM forms and IBM Content Manager.
uuid: 3d55169d-93e3-4d4e-b18b-2a3394e1de3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3094b178-3b1a-46b3-8fbd-c20388afa3a7
exl-id: 50f0c963-8007-4e2a-aa73-d99b97d9a1aa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# 為IBM Content Manager設定連接器{#configuring-connector-for-ibm-content-manager}

IBM Content Manager的連接器可啟用AEM Forms與IBM Content Manager之間的通訊。 如需其他背景資訊，請參閱 [服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 設定IBM Content Manager連線 {#configure-the-ibm-content-manager-connection}

1. 在管理主控台中，按一下「服務>IBM Content Manager的連接器」 。
1. 在「資料存放區名稱」方塊中，輸入您要連線的IBM Content Manager資料存放區名稱。 如果資料庫是本地的，請輸入資料庫的名稱。 如果資料庫是遠程的，請輸入其別名。
1. 在「使用者名稱」方塊中，輸入要連線至IBM Content Manager資料存放區之使用者的使用者ID。
1. 在「密碼」框中，輸入用戶的密碼。
1. （可選）在「別名連接字串」框中，輸入其他連接參數。 在大多數情況下，此方塊應為空。 如需詳細資訊，請參閱您的IBM檔案。
1. 按一下「儲存」。

## 服務設定驗證 {#validation-of-service-settings}

如果您輸入了不正確的dataStore別名、用戶名或密碼，則將獲得以下結果，具體取決於IBM Content Manager服務的Content Repository Connector當前是否正在運行：

* 如果服務停止，則保存服務配置資訊時，不會顯示錯誤。 但是，下次啟動服務時，將引發異常，且服務將不啟動。
* 如果啟動服務，則在保存服務配置資訊時，服務會嘗試立即驗證憑據資訊。 在此情況下，會發生錯誤且不會儲存設定資訊。
