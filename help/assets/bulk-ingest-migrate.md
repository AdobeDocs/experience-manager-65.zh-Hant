---
title: 安裝功能套件18912以進行大量資產移轉
description: 功能套件18912可讓您透過FTP大量內嵌資產，或將資產從Dynamic Media經典移轉至Dynamic MediaAEM。 此可選功能套件可從Adobe支援取得。
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
feature: Asset Management
role: Business Practitioner, Administrator
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# 安裝功能套件18912以進行大量資產移轉{#installing-feature-pack-for-bulk-asset-migration}

功能包18912的安裝是&#x200B;*可選*。

功能套件18912可讓您透過FTP將大量資產直接內嵌至Dynamic Media-Scene7模式，或AEM是將資產從Dynamic Media經典移轉至Dynamic Media-Scene7模式AEM。 功能包可從[Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html)取得。

>[!NOTE]
>
>雖然您可以使用功能套件自行將資產從Dynamic Media經典大量移轉至Dynamic Media-使用Dynamic Media經典的FTP功能在Scene 7模式中AEM，或大量移轉資產，但Adobe不建議使用&#x200B;*not*，因為涉及的複雜性。
>
>因此，遷移功能包（如此）在通過[Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html)完成遷移項目時，僅&#x200B;**&#x200B;受支援。

在安裝功能套件之前，您必須先建立服務使用者，並提供該資訊給Adobe支援。

另請參閱[配置Dynamic Media-Scene7模式](/help/assets/config-dms7.md)。

**若要安裝功能套件18912以進行大量資產移轉**

1. 在您的AEM實例中，導航至&#x200B;**[!UICONTROL 工具>安全性>用戶]**&#x200B;並選擇&#x200B;**[!UICONTROL 建立用戶]**。 此服務用戶必須具有&#x200B;*`/content/dam.`的讀／寫*&#x200B;權限
1. 在&#x200B;**[!UICONTROL ID]**&#x200B;和&#x200B;**[!UICONTROL Password]**&#x200B;欄位中，輸入用戶名和密碼；例如，**FTP使用者**。 此名稱會以建立資產的使用者身分出現在時間軸中。 當資產從FTP上傳時，當資產上傳至FTP伺服器並推送至時，即視為已建立AEM資產。
1. 請聯絡[Adobe企業客戶服務以取得Experience Manager](https://experienceleague.adobe.com/?support-solution=General#support)，要求存取功能套件18912以進行下載。 當您聯絡支援人員時，可能需要下列資訊：

   * 您「作者」實例的伺服器IP地址，包括埠號（預設情況下，埠號為4502）。
   * 服AEM務用戶用戶名和密碼。

1. Adobe企業客戶服AEM務提供FTP憑證和功能套件18912的存取權。
1. 收到功能套件18912時，請安裝它。

   有關在中使用軟體分發和軟體包的詳細資訊，請參見[如何使用軟體包](/help/sites-administering/package-manager.md)AEM。
