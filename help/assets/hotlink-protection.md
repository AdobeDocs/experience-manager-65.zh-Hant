---
title: 在Dynamic Media中啟用快速連結保護
description: 有關如何在Dynamic Media中啟用快速連結保護的資訊。
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
role: User, Admin
exl-id: 698e8bdb-9b31-49ab-8560-26b05109bb23
feature: Configuration
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# 在Dynamic Media中啟用快速連結保護 {#activating-hotlink-protection-in-dynamic-media}

熱連結是指第三方網站使用HTML程式碼顯示您網站中的影像時。 每次要求圖片時，他們都會使用您的頻寬，因為訪客的瀏覽器會直接從您的伺服器存取圖片。 直接連結&#x200B;*保護*&#x200B;是防止其他網站直接連結至您網頁上的圖片、CSS或JavaScript的方法。 這種遮蔽有助於減少Dynamic Media帳戶下不必要的頻寬使用量。

[Experience Manager客戶支援](https://experienceleague.adobe.com/zh-hant?support-solution=Experience+Manager#support)可以在CDN （內容傳遞網路）層級設定反向連結篩選器，以便Dynamic Media內容僅會提供給您網域所允許網站清單上的網站。

>[!NOTE]
>
>此功能需要您使用Adobe Experience Manager Dynamic Media隨附的現成可用CDN。 此功能不支援任何其他自訂CDN。 若要啟用快速連結保護，管理員必須建立Adobe客戶支援票證，以要求變更您Dynamic Media帳戶的設定。 啟用熱連結保護不需要額外付費。
