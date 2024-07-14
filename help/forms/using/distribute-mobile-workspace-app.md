---
title: 發佈AEM Forms應用程式
description: 使用行動裝置管理(MDM)在行動裝置上大規模部署應用程式。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 375cfa95-ac6f-44c4-a736-f5dd55d24195
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# 發佈AEM Forms應用程式 {#distribute-aem-forms-app}

行動裝置管理(MDM)可讓您在行動裝置上大規模部署應用程式。

>[!NOTE]
>
>此發佈僅適用於iOS和Android™裝置。

## MDM解決方案提供的主要功能： {#main-features-generally-provided-by-mdm-solutions}

* 在您的企業環境中啟用裝置註冊
* 允許設定和更新裝置設定
* 強制執行安全性法規遵循。
* 以行動裝置安全地存取公司資源

MDM解決方案搭配行動應用程式管理，可讓您透過企業內的行動裝置，管理內部、公開及已購買的應用程式。

MDM管理員可以將ipa和apk檔案上傳到MDM伺服器，並控制可以存取ipa或apk檔案的使用者。 管理員也可以控制對應到每個應用程式的設定檔設定。

## 影響AEM Forms應用程式的設定檔設定 {#profile-settings-affecting-the-aem-forms-app-br}

您裝置上的下列設定檔設定會影響裝置上AEM Forms應用程式的運作：

* **允許在**&#x200B;裝置功能&#x200B;**區段中使用攝影機**

如果停用&#x200B;**允許使用相機**，則[像片註解](/help/forms/using/add-attachments.md)的相機功能無法運作。 啟用此選項以使用應用程式中的攝影機。

* **需要裝置**&#x200B;上的密碼原則區段

若要啟用&#x200B;**應用程式資料**&#x200B;的加密，建議您在裝置上啟用&#x200B;**密碼**。 如果裝置上未設定密碼，則儲存在裝置上的應用程式資料不會加密。
