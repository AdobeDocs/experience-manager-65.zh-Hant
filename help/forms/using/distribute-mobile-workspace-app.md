---
title: 發佈AEM Forms應用程式
seo-title: 發佈AEM Forms應用程式
description: 使用移動設備管理(MDM)在移動設備上大規模部署應用。
seo-description: 使用移動設備管理(MDM)在移動設備上大規模部署應用。
uuid: 8a2ce42b-5e9b-42c1-a945-c069f6152f6e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 5756cb52-dd47-4277-981c-fd0af9a20638
exl-id: 375cfa95-ac6f-44c4-a736-f5dd55d24195
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# 分發AEM Forms應用程式{#distribute-aem-forms-app}

移動設備管理(MDM)支援在移動設備上大規模部署應用。

>[!NOTE]
>
>此分送僅適用於iOS和Android裝置。

## MDM解決方案通常提供的主要功能：{#main-features-generally-provided-by-mdm-solutions}

* 在企業環境中啟用設備註冊
* 允許配置和更新設備設定
* 強制遵守安全性。
* 對公司資源的安全移動訪問

MDM解決方案與移動應用管理一起，允許您管理企業內的移動設備上的內部、公共和購買的應用。

MDM管理員可將ipa和apk檔案上載到MDM伺服器，並控制可訪問ipa或apk檔案的用戶。 管理員也可以控制與每個應用程式對應的設定檔設定。

## 影響AEM Forms應用程式的設定檔設定{#profile-settings-affecting-the-aem-forms-app-br}

裝置上的下列設定檔設定將影響裝置上AEM Forms應用程式的運作：

* **允許在「設備** 功能」部分 **使用** 攝像頭

如果禁用&#x200B;**允許使用相機**，則[照片批注](/help/forms/using/add-attachments.md)的相機功能將無法工作。 您必須啟用此選項，才能在應用程式中使用相機。

* **在「密碼策** 略」部分要求設備上的密碼

若要啟用應用程式資料&#x200B;**加密**，建議您在裝置上啟用&#x200B;**密碼**。 如果未在設備上設定密碼，則儲存在設備上的應用程式資料不會加密。
