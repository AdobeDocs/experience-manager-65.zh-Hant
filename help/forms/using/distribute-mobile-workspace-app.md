---
title: 散發AEM Forms應用程式
seo-title: 散發AEM Forms應用程式
description: 使用行動裝置管理(MDM)，在行動裝置上大規模部署應用程式。
seo-description: 使用行動裝置管理(MDM)，在行動裝置上大規模部署應用程式。
uuid: 8a2ce42b-5e9b-42c1-a945-c069f6152f6e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 5756cb52-dd47-4277-981c-fd0af9a20638
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---


# 散發AEM Forms應用程式{#distribute-aem-forms-app}

行動裝置管理(MDM)可讓應用程式在行動裝置上大規模部署。

>[!NOTE]
>
>此散發僅適用於iOS和Android裝置。

## MDM解決方案通常提供的主要功能：{#main-features-generally-provided-by-mdm-solutions}

* 在企業環境中啟用裝置註冊
* 允許配置和更新設備設定
* 強制符合安全性。
* 安全地存取企業資源的行動裝置

MDM解決方案與移動應用管理相結合，可讓您管理企業內部、公開和購買的移動設備應用。

MDM管理員可以將ipa和apk檔案上傳到MDM伺服器，並控制可以訪問ipa或apk檔案的用戶。 管理員還可以控制對應於每個應用程式的配置檔案設定。

## 影響AEM Forms應用程式{#profile-settings-affecting-the-aem-forms-app-br}的設定檔設定

您裝置上的下列設定檔會影響裝置上AEM Forms應用程式的運作：

* **允許使用攝** 影機裝置 **功能** 區段

如果您停用「允許使用camera **」,[Photograph annotation](/help/forms/using/add-attachments.md)的相機功能將無法運作。**&#x200B;您必須啟用此選項，才能在應用程式中使用相機。

* **在「密碼策略」** 部分要求設備上的密碼

若要啟用應用程式資料的&#x200B;**加密**，建議您在裝置上啟用&#x200B;**密碼**。 如果未在裝置上設定密碼，儲存在裝置上的應用程式資料將不會加密。
