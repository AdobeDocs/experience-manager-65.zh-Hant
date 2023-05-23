---
title: 分發AEM Forms應用
seo-title: Distribute AEM Forms app
description: 使用移動設備管理(MDM)在移動設備上大規模部署應用。
seo-description: Use Mobile Device Management (MDM) for the large-scale deployment of apps on mobile devices.
uuid: 8a2ce42b-5e9b-42c1-a945-c069f6152f6e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 5756cb52-dd47-4277-981c-fd0af9a20638
exl-id: 375cfa95-ac6f-44c4-a736-f5dd55d24195
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# 分發AEM Forms應用 {#distribute-aem-forms-app}

移動設備管理(MDM)支援在移動設備上大規模部署應用。

>[!NOTE]
>
>此分發僅適用於iOS和Android設備。

## MDM解決方案通常提供的主要功能： {#main-features-generally-provided-by-mdm-solutions}

* 在企業環境中啟用設備註冊
* 允許配置和更新設備設定
* 強制遵守安全法規。
* 保護對公司資源的移動訪問

MDM解決方案與移動應用程式管理相結合，允許您跨企業中的移動設備管理內部、公共和購買的應用。

MDM管理員可以將ipa和apk檔案上載到MDM伺服器，並控制可以訪問ipa或apk檔案的用戶。 管理員還可以控制與每個應用程式對應的配置檔案設定。

## 影響AEM Forms應用的配置檔案設定 {#profile-settings-affecting-the-aem-forms-app-br}

您設備上的以下配置檔案設定將影響您設備上的AEM Forms應用的功能：

* **允許使用相機** 的 **設備功能** 節

如果禁用 **允許使用相機**，相機的特徵 [照片批注](/help/forms/using/add-attachments.md) 不起作用。 你需要啟用此選項才能在應用中使用相機。

* **需要設備上的密碼** 在「密碼策略」部分

啟用 **應用程式資料加密**，建議您啟用 **密碼** 在你的設備上。 如果未在設備上設定密碼，則不加密儲存在設備上的應用程式資料。
