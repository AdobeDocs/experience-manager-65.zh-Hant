---
title: 在動態媒體中啟用熱鏈路保護
description: 有關如何在動態媒體中啟用作用連結保護的資訊。
uuid: 5f93bc27-5edd-4143-8701-87896c52f0af
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: a70aa448-0f58-4ed2-9381-afcc76fa827f
translation-type: tm+mt
source-git-commit: 787f3b4cf5835b7e9b03e3f4e6f6597084adec8c
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# 在動態媒體中激活熱鏈路保護{#activating-hotlink-protection-in-dynamic-media}

作用連結是指協力廠商網站使用HTML程式碼來顯示您網站的影像時。 每次要求圖片時，他們都會使用您的頻寬，因為訪客的瀏覽器會直接從您的伺服器存取圖片。 Hotlink *protection*&#x200B;是一種方法，可防止其他網站直接連結至您網頁上的圖片、css或JavaScript。 這種防護罩有助於減少動態媒體帳戶下不必要的頻寬使用。

[Adobe ](https://helpx.adobe.com/support.html) Support可在CDN（內容傳送網路）層級設定反向連結篩選，如此，動態媒體內容僅會提供給您網域許可網站清單上的網站。

>[!NOTE]
>
>這項功能需要您使用Adobe Experience Manager Dynamic Media隨附的現成可用CDN。 此功能不支援任何其他自訂CDN。 若要啟用作用連結保護，管理員必須建立Adobe客戶服務支援票證，才能要求對您的動態媒體帳戶進行設定變更。 啟動熱鏈路保護不需要額外費用。
