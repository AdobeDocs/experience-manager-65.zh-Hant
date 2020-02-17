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
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# 安裝功能套件18912以進行大量資產移轉{#installing-feature-pack-for-bulk-asset-migration}

安裝功能套件18912是可選 *的*。

功能套件18912可讓您透過FTP將大量資產直接收錄至AEM的Dynamic Media - Scene7模式，或從Dynamic Media Classic將資產移轉至AEM的Dynamic Media - Scene7模式。 您可從 [Adobe專業服務取得功能套件](https://www.adobe.com/experience-cloud/consulting-services.html)。

>[!NOTE]
>
>雖然您可以使用功能套件將資產自行從Dynamic Media Classic大量移轉至Dynamic Media - AEM中的Scene 7模式，或使用Dynamic Media Classic的FTP功能大量移轉資產，但Adobe不建議使用此方 ** 法，因為涉及的複雜性。
>
>因此，移轉功能套件（例如此套件）只 *能在* 透過 [Adobe專業服務完成移轉專案時受支援](https://www.adobe.com/experience-cloud/consulting-services.html)。

在安裝功能套件之前，您必須先建立服務使用者，並將該資訊提供給Adobe支援。

另請參 [閱設定動態媒體- Scene7模式](/help/assets/config-dms7.md)。

**若要安裝功能套件18912以進行大量資產移轉**

1. 在您的AEM例項中，導覽至「工具> **[!UICONTROL 保全>使用者」]** ，然後選 **[!UICONTROL 取「建立使用者」]**。 此服務使用者必 *須具有讀／寫權限* ，才能 `/content/dam.`
1. 在「 **[!UICONTROL ID]** 」和「 **[!UICONTROL Password]** 」欄位中輸入用戶名和密碼；例如， **FTP使用者**。 此名稱會以建立資產的使用者身分出現在時間軸中。 當資產從FTP上傳時，當資產上傳至FTP伺服器並推送至AEM時，即視為已建立資產。
1. 請聯 [絡Adobe Enterprise Support for Experience Manager](https://helpx.adobe.com/contact/enterprise-support.ec.html) ，要求存取功能套件18912以進行下載。 當您聯絡支援人員時，可能需要下列資訊：

   * 您「作者」實例的伺服器IP地址，包括埠號（預設情況下，埠號為4502）。
   * AEM服務使用者使用者使用者名稱和密碼。

1. Adobe Enterprise Support for AEM提供您FTP認證和功能套件18912的存取權。
1. 收到功能套件18912時，請安裝它。

   如需 [在AEM中使用Package Share和Packages的詳細資訊，請參閱How to Work with Packages](/help/sites-administering/package-manager.md) 。

