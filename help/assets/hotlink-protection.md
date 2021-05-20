---
title: 在Dynamic Media中啟用熱連結保護
description: 有關如何在Dynamic Media中啟用熱連結保護的資訊。
uuid: 5f93bc27-5edd-4143-8701-87896c52f0af
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: a70aa448-0f58-4ed2-9381-afcc76fa827f
role: Business Practitioner, Administrator
exl-id: 698e8bdb-9b31-49ab-8560-26b05109bb23
feature: 設定
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# 在Dynamic Media中啟用熱連結保護{#activating-hotlink-protection-in-dynamic-media}

熱連結是指第三方網站使用HTML程式碼來顯示您網站的影像時。 每次請求圖片時，他們都會使用您的頻寬，因為訪客的瀏覽器會直接從您的伺服器存取圖片。 Hotlink *protection*&#x200B;是一種方法，可防止其他網站直接連結至您網頁上的圖片、CSS或JavaScript。 這種防護有助於減少您Dynamic Media帳戶下不必要的頻寬使用。

[Adobe](https://helpx.adobe.com/support.html) 支援可在CDN（內容傳遞網路）層級設定反向連結篩選，使Dynamic Media內容僅供網域允許之網站清單上的網站使用。

>[!NOTE]
>
>若要使用此功能，您必須使用隨Adobe Experience Manager Dynamic Media提供的現成可用CDN。 此功能不支援任何其他自訂CDN。 若要啟用熱連結保護，管理員必須建立Adobe客戶服務支援票證，以向您的Dynamic Media帳戶要求設定變更。 激活熱鏈路保護無需額外費用。
