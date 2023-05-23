---
title: 在Dynamic Media激活熱鏈路保護
description: 有關如何激活Dynamic Media熱鏈路保護的資訊。
uuid: 5f93bc27-5edd-4143-8701-87896c52f0af
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: a70aa448-0f58-4ed2-9381-afcc76fa827f
role: User, Admin
exl-id: 698e8bdb-9b31-49ab-8560-26b05109bb23
feature: Configuration
source-git-commit: 65af6e33ae3897519491952f4d3a6832700f77b2
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 2%

---

# 在Dynamic Media激活熱鏈路保護 {#activating-hotlink-protection-in-dynamic-media}

熱連結是指第三方網站使用HTML代碼顯示您網站中的影像。 每次請求圖片時，他們都會使用您的頻寬，因為訪問者的瀏覽器直接從您的伺服器訪問圖片。 熱連結 *保護* 是一種防止其他網站直接連結到網頁上的圖片、CSS或JavaScript的方法。 這種防護有助於減少您的Dynamic Media帳戶下不必要的頻寬使用。

[Experience Manager客戶支援](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) 可以在CDN（內容分發網路）級別配置引用者篩選器，以便僅將Dynamic Media內容提供給域允許網站清單上的網站。

>[!NOTE]
>
>此功能要求您使用與Adobe Experience ManagerDynamic Media捆綁的現成CDN。 此功能不支援任何其他自定義CDN。 要激活熱連結保護，管理員必須建立Adobe客戶支援支援票證，以請求對Dynamic Media帳戶進行配置更改。 激活熱鏈路保護無需額外成本。
