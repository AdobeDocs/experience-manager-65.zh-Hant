---
title: 將引用者篩選器設定為允許空
seo-title: Setting Your Referrer Filter to Allow Empty
description: 按照此頁瞭解「引用過濾器」。 為了允許AEM Mobile應用程式查看器查看您的「作者」實例上的應用，您需要將HTML引用篩選器設定為「允許空」。
seo-description: Follow this page to learn about Referrer Filter. In order to allow the AEM Mobile Application Viewer to view apps on your Author instance, you'll need to set your HTML referrer filter to 'allow empty'.
uuid: 4fb0f95c-ac8f-4a14-8c46-6616d9d4f380
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 8fb7d088-94bf-4799-98b3-8fa58eef83df
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 1%

---

# 將引用者篩選器設定為允許空{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

為了允許AEM Mobile應用程式查看器查看您的「作者」實例上的應用，您需要將HTML引用篩選器設定為「允許空」。

如果您不打算使用應用程式查看器來查看處於開發和轉移狀態的應用程式，則無需更改引用過濾器的預設設定。

在您運行的「作者」實AEM例中，導航到： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) 並搜索「Apache Sling引用過濾器」。 按一下以編輯引用過濾器並選中「允許空」複選框（請參閱下圖）。 然後按一下「保存」按鈕並關閉瀏覽器頁面。

![引用者篩選器設定](assets/chlimage_1-106.png)
