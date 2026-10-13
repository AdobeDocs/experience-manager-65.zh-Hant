---
title: 為IBM&reg； Content Manager設定聯結器
description: 設定IBM&reg；內容管理員的聯結器，以啟用AEM表單與IBM&reg；內容管理員之間的通訊。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 50f0c963-8007-4e2a-aa73-d99b97d9a1aa
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%
---
# 設定® Content Manager的聯結器{#configuring-connector-for-ibm-content-manager}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

® Content Manager聯結器可啟用AEM表單與IBM® Content Manager之間的通訊。 如需其他背景資訊，請參閱[服務參考](https://www.adobe.com/go/learn_aemforms_services_63)中的「Connectors for ECM」。

## 設定®內容管理員連線 {#configure-the-ibm-content-manager-connection}

1. 在管理控制檯中，按一下「服務>IBM聯結器®內容管理員」。
1. 在「資料存放區名稱」方塊中，輸入您要連線的® Content Manager資料存放區名稱。 如果資料庫是本機資料庫，請輸入資料庫的名稱。 如果資料庫是遠端資料庫，請輸入其別名。
1. 在「使用者名稱」方塊中，輸入即將連線至® Content Manager資料存放區之使用者的使用者ID。
1. 在密碼方塊中，輸入使用者的密碼。
1. （選擇性）在「別名連線字串」方塊中，輸入其他連線引數。 通常，此方塊應該是空的。 如需詳細資訊，請參閱您的®檔案。
1. 按一下「儲存」。

## 驗證服務設定 {#validation-of-service-settings}

如果您輸入不正確的dataStore別名、使用者名稱或密碼，則會獲得以下結果，具體取決於® Content Manager服務的Content Repository Connector是否正在執行：

* 如果服務已停止，當您儲存服務組態資訊時，不會出現任何錯誤。 但是，下次啟動服務時，會擲回例外狀況，而且服務不會啟動。
* 如果服務已啟動，當您儲存服務組態資訊時，服務會立即嘗試驗證認證資訊。 在這種情況下，會發生錯誤且未儲存設定資訊。
