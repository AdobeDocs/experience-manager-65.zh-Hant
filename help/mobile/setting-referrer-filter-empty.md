---
title: 將反向連結篩選設定為允許空白
description: 瞭解反向連結篩選。 若要允許Adobe Experience Manager (AEM) Mobile Application Viewer在您的Author例項上檢視應用程式，您必須將HTML反向連結篩選設定為「允許空白」。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
source-git-commit: 6799f1d371734b69c547f3c0c68e1e633aa63229
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 1%

---

# 將反向連結篩選設定為允許空白{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [深入了解](/help/sites-developing/spa-overview.md)。

若要允許Adobe Experience Manager (AEM) Mobile Application Viewer在您的Author例項上檢視應用程式，您必須將HTML反向連結篩選設定為「允許空白」。

如果您不打算使用「應用程式檢視器」來檢閱處於開發和測試狀態的應用程式，則不需要變更反向連結篩選器的預設設定。

在您執行中的AEM作者例項中，導覽至： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) 和搜尋「Apache Sling反向連結篩選器」。 按一下以編輯反向連結篩選條件，並勾選「允許空白」核取方塊（請參閱下圖）。 接著，按一下儲存按鈕，並關閉瀏覽器頁面。

![反向連結篩選設定](assets/chlimage_1-106.png)
