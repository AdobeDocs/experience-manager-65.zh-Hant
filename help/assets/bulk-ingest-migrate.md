---
title: 安裝Feature Pack 18912以進行大量資產移轉
description: Feature Pack 18912可讓您透過FTP大量擷取資產，或在Adobe Experience Manager上將資產從Dynamic Media Classic移轉至Dynamic Media。 Adobe支援提供此選用的Feature Pack。
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# 安裝Feature Pack 18912以進行大量資產移轉{#installing-feature-pack-for-bulk-asset-migration}

功能套件18912的安裝為 *可選*.

Feature Pack 18912可讓您透過FTP將資產直接大量擷取到Adobe Experience Manager上的Dynamic Media - Scene7模式。 它也可讓您在Experience Manager上將資產從Dynamic Media Classic移轉至Dynamic Media - Scene7模式。 此Feature Pack可從以下網址取得： [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

>[!IMPORTANT]
>
>您可以在Experience Manager中使用Feature Pack自行將資產從Dynamic Media Classic大量移轉至Dynamic Media - Scene7模式。 您也可以使用Dynamic Media Classic中的FTP功能來大量移轉資產。 不過，Adobe可以 *非* 由於其中涉及的複雜性，建議您使用其中一種方法。
>
>因此，此移轉Feature Pack *僅限* 透過完成時支援作為移轉專案的一部分 [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

在安裝Feature Pack之前，請先建立服務使用者，並提供該資訊以Adobe支援。

另請參閱 [設定Dynamic Media - Scene7模式](/help/assets/config-dms7.md).

**若要安裝Feature Pack 18912以進行大量資產移轉：**

1. 在您的Experience Manager例項中，導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]** 並選取 **[!UICONTROL 建立使用者]**. 此服務使用者必須具備 *讀取/寫入* 許可權： `/content/dam.`
1. 在 **[!UICONTROL ID]** 和 **[!UICONTROL 密碼]** 欄位，輸入使用者名稱和密碼；例如 **FTP使用者**. 此名稱會以建立資產之使用者的身分顯示在時間軸中。 從FTP上傳資產時，資產會在上傳至FTP伺服器並推送至Experience Manager時被視為已建立。
1. 連絡人 [Experience Manager的Adobe客戶支援](https://experienceleague.adobe.com/?support-solution=General#support) 請求存取功能套件18912以進行下載。 當您聯絡支援時，可能需要下列資訊：

   * 您的Author執行個體的伺服器IP位址，包括連線埠號碼（根據預設，連線埠號碼為4502）。
   * Experience Manager上一步驟中的服務使用者名稱與密碼。

1. Experience Manager的Adobe客戶支援為您提供FTP憑證和Feature Pack 18912的存取權。
1. 收到Feature Pack 18912時，請加以安裝。

   另請參閱 [如何使用套件](/help/sites-administering/package-manager.md) 以取得在Experience Manager中使用軟體發佈和套件的詳細資訊。
