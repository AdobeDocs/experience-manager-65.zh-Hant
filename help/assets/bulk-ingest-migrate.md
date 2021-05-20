---
title: 安裝Feature Pack 18912以大量移轉資產
description: Feature Pack 18912可讓您透過FTP大量內嵌資產，或將資產從Dynamic Media Classic移轉至AEM上的Dynamic Media。 此選用功能套件提供Adobe支援。
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
feature: 資產管理
role: Business Practitioner, Administrator
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---

# 安裝Feature Pack 18912以進行大量資產移轉{#installing-feature-pack-for-bulk-asset-migration}

Feature Pack 18912的安裝為&#x200B;*optional*。

Feature Pack 18912可讓您透過FTP將資產直接大量內嵌至AEM的Dynamic Media - Scene7模式，或將資產從Dynamic Media Classic移轉至AEM的Dynamic Media - Scene7模式。 此功能包可從[Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html)取得。

>[!NOTE]
>
>雖然您可以使用Feature Pack自行將資產從Dynamic Media Classic大量移轉至Dynamic Media — 在AEM中使用Scene 7模式，或使用Dynamic Media Classic的FTP功能大量移轉資產，但由於相關複雜性，Adobe不建議使用&#x200B;*not*&#x200B;此方法。
>
>因此，透過[Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html)完成移轉專案時，僅支援&#x200B;**&#x200B;等移轉功能套件。

您必須先建立Service使用者，並提供該資訊給Adobe支援，才能安裝Feature Pack。

另請參閱[設定Dynamic Media - Scene7模式](/help/assets/config-dms7.md)。

**若要安裝Feature Pack 18912以大量移轉資產**

1. 在您的AEM例項中，導覽至&#x200B;**[!UICONTROL 工具>安全性>使用者]**&#x200B;並選取&#x200B;**[!UICONTROL 建立使用者]**。 此服務用戶必須具有&#x200B;*讀/寫*`/content/dam.`權限
1. 在&#x200B;**[!UICONTROL ID]**&#x200B;和&#x200B;**[!UICONTROL 密碼]**&#x200B;欄位中，輸入用戶名和密碼；例如， **FTP使用者**。 此名稱會以建立資產的使用者身分顯示在時間軸中。 從FTP上傳資產時，會將資產上傳至FTP伺服器並推送至AEM時，視為已建立資產。
1. 如需Experience Manager](https://experienceleague.adobe.com/?support-solution=General#support)，請聯絡[Adobe企業客戶服務，以要求存取Feature Pack 18912以供下載。 聯絡支援人員時，您可能需要下列資訊：

   * 您Author例項的伺服器IP位址，包括連接埠號（依預設，連接埠號為4502）。
   * AEM服務使用者使用者名稱和密碼。

1. AdobeAEM企業客戶服務提供FTP憑證和Feature Pack 18912的存取權。
1. 收到Feature Pack 18912時，請安裝它。

   有關在AEM中使用軟體分發和軟體包的詳細資訊，請參閱[如何使用軟體包](/help/sites-administering/package-manager.md)。
