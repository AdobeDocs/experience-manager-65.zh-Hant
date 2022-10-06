---
title: 安裝Feature Pack 18912以大量移轉資產
description: Feature Pack 18912可讓您透過FTP大量內嵌資產，或將資產從Dynamic Media Classic移轉至Adobe Experience Manager上的Dynamic Media。 此選用功能套件提供Adobe支援。
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 2%

---

# 安裝Feature Pack 18912以大量移轉資產{#installing-feature-pack-for-bulk-asset-migration}

安裝Feature Pack 18912為 *可選*.

Feature Pack 18912可讓您透過FTP，將資產直接大量內嵌至Adobe Experience Manager上的Dynamic Media - Scene7模式。 也可讓您將資產從Dynamic Media Classic移轉至Dynamic Media - Scene7模式(Experience Manager)。 此功能包可從 [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

>[!IMPORTANT]
>
>您可以使用Feature Pack以Experience Manager方式，自行將資產從Dynamic Media Classic(Dynamic Media)- Scene7模式大量移轉至。 您也可以使用Dynamic Media Classic中的FTP功能大量移轉資產。 不過，Adobe確實 *not* 由於所涉的複雜性，建議您使用上述任一方法。
>
>因此，此移轉功能套件為 *僅限* 支援作為移轉專案的一部分，若完成 [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

安裝Feature Pack之前，請建立Service使用者，並提供該資訊給Adobe支援。

另請參閱[設定 Dynamic Media - Scene7 模式](/help/assets/config-dms7.md).

**若要安裝Feature Pack 18912以大量移轉資產：**

1. 在您的Experience Manager例項中，導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]** 選取 **[!UICONTROL 建立使用者]**. 此服務用戶必須 *讀/寫* 權限 `/content/dam.`
1. 在 **[!UICONTROL ID]** 和 **[!UICONTROL 密碼]** 欄位，輸入用戶名和密碼；例如， **FTP使用者**. 此名稱會以建立資產的使用者身分顯示在時間軸中。 從FTP上傳資產時，會將資產上傳至FTP伺服器並推送至Experience Manager時，視為已建立資產。
1. 連絡人 [AdobeExperience Manager支援](https://experienceleague.adobe.com/?support-solution=General#support) 請求存取feature pack 18912以供下載。 聯絡支援人員時，您可能需要下列資訊：

   * 您Author例項的伺服器IP位址，包括連接埠號（依預設，連接埠號為4502）。
   * Experience Manager服務用戶的用戶名和密碼。

1. AdobeExperience Manager客戶支援提供FTP憑證，以及Feature Pack 18912的存取權。
1. 收到Feature Pack 18912時，請安裝它。

   請參閱 [如何使用套件](/help/sites-administering/package-manager.md) 有關在Experience Manager中使用軟體分發和軟體包的詳細資訊。
