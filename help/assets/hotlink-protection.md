---
title: 激活Dynamic Media熱鏈路保護
description: 有關如何在Dynamic Media啟用熱鏈路保護的資訊。
uuid: 5f93bc27-5edd-4143-8701-87896c52f0af
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: a70aa448-0f58-4ed2-9381-afcc76fa827f
role: 業務從業人員、管理員
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---


# 在Dynamic Media激活熱鏈路保護{#activating-hotlink-protection-in-dynamic-media}

作用連結是指協力廠商網站使用HTML程式碼來顯示您網站的影像時。 每次要求圖片時，他們都會使用您的頻寬，因為訪客的瀏覽器會直接從您的伺服器存取圖片。 Hotlink *protection*&#x200B;是一種方法，可防止其他網站直接連結至您網頁上的圖片、css或JavaScript。 這種防護罩有助於減少您Dynamic Media帳戶下不必要的頻寬使用。

[Adobe支](https://helpx.adobe.com/support.html) 援可在CDN（內容傳送網路）層級設定反向連結篩選器，讓Dynamic Media內容僅提供給您網域許可網站清單上的網站。

>[!NOTE]
>
>此功能需要您使用隨附於Adobe Experience Manager·Dynamic Media的現成可用CDN。 此功能不支援任何其他自訂CDN。 要激活熱連結保護，管理員必須建立Adobe客戶服務支援票證，以請求對Dynamic Media帳戶進行配置更改。 啟動熱鏈路保護不需要額外費用。
