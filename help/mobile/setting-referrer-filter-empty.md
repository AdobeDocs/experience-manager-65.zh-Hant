---
title: 將您的反向連結篩選設定為允許空白
seo-title: 將您的反向連結篩選設定為允許空白
description: 請依此頁面瞭解反向連結篩選。 若要允許AEM Mobile應用程式檢視器在您的「作者」例項上檢視應用程式，您必須將HTML反向連結篩選器設為「允許空白」。
seo-description: 請依此頁面瞭解反向連結篩選。 若要允許AEM Mobile應用程式檢視器在您的「作者」例項上檢視應用程式，您必須將HTML反向連結篩選器設為「允許空白」。
uuid: 4fb0f95c-ac8f-4a14-8c46-6616d9d4f380
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 8fb7d088-94bf-4799-98b3-8fa58eef83df
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 將您的反向連結篩選設定為允許空白{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

若要允許AEM Mobile應用程式檢視器在您的「作者」例項上檢視應用程式，您必須將HTML反向連結篩選器設為「允許空白」。

如果您不想使用Application Viewer來檢視處於開發和測試狀態的應用程式，則不需要變更反向連結篩選器的預設設定。

在您執行中的AEM「作者」例項中，導覽至： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) ，並搜尋&#39;Apache Sling Referrer Filter&#39;。 按一下以編輯反向連結篩選並勾選「允許空白」核取方塊（請參閱下圖）。 接著按一下儲存按鈕並關閉瀏覽器頁面。

![反向連結篩選設定](assets/chlimage_1-106.png)
