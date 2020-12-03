---
title: 安裝功能套件18912以進行大量資產移轉
description: 功能套件18912可讓您透過FTP大量收錄資產，或從Dynamic Media Classic將資產移轉至AEM上的Dynamic Media。 Adobe支援提供此選購的功能套件。
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
translation-type: tm+mt
source-git-commit: d6ae8bffa2d9d59f5656b9344d8826128f12885c
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 1%

---


# 安裝功能套件18912以進行大量資產移轉{#installing-feature-pack-for-bulk-asset-migration}

功能包18912的安裝是&#x200B;*可選*。

功能套件18912可讓您透過FTP將大量資產直接收錄至AEM的Dynamic Media - Scene7模式，或從Dynamic Media Classic將資產移轉至AEM的Dynamic Media - Scene7模式。 您可從[Adobe專業服務](https://www.adobe.com/experience-cloud/consulting-services.html)取得功能套件。

>[!NOTE]
>
>雖然您可以使用功能套件將資產自行從Dynamic Media Classic大量移轉至Dynamic Media - AEM中的Scene 7模式，或使用Dynamic Media Classic的FTP功能大量移轉資產，但Adobe會&#x200B;*not*&#x200B;建議使用此方法，因為涉及的複雜性。
>
>因此，當透過[Adobe專業服務](https://www.adobe.com/experience-cloud/consulting-services.html)進行移轉時，僅&#x200B;**&#x200B;支援移轉功能套件。

在安裝功能套件之前，您必須先建立服務使用者，並將該資訊提供給Adobe支援。

另請參閱[設定動態媒體- Scene7模式](/help/assets/config-dms7.md)。

**若要安裝功能套件18912以進行大量資產移轉**

1. 在您的AEM例項中，導覽至「**[!UICONTROL 工具>安全性>使用者]**」，然後選取「建立使用者&#x200B;]**」。**[!UICONTROL &#x200B;此服務用戶必須具有&#x200B;*`/content/dam.`的讀／寫*&#x200B;權限
1. 在&#x200B;**[!UICONTROL ID]**&#x200B;和&#x200B;**[!UICONTROL Password]**&#x200B;欄位中，輸入用戶名和密碼；例如，**FTP使用者**。 此名稱會以建立資產的使用者身分出現在時間軸中。 當資產從FTP上傳時，當資產上傳至FTP伺服器並推送至AEM時，即視為已建立資產。
1. 請聯絡[Adobe Enterprise Customer Care for Experience Manager](https://helpx.adobe.com/tw/contact/enterprise-support.ec.html)以要求存取功能套件18912以進行下載。 當您聯絡支援人員時，可能需要下列資訊：

   * 您「作者」實例的伺服器IP地址，包括埠號（預設情況下，埠號為4502）。
   * AEM服務使用者使用者使用者名稱和密碼。

1. Adobe Enterprise Customer Care for AEM提供您FTP認證和功能套件18912的存取權。
1. 收到功能套件18912時，請安裝它。

   如需在AEM中使用「軟體散發」和「封裝」的詳細資訊，請參閱[如何使用套件](/help/sites-administering/package-manager.md)。
