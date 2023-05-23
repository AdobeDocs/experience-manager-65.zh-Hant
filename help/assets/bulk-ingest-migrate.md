---
title: 安裝功能包18912以進行批量資產遷移
description: 功能包18912允許您通過FTP批量接收資產，或將資產從Dynamic Media Classic遷移到Adobe Experience Manager的Dynamic Media。 此可選功能包可從Adobe支援獲得。
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

# 安裝功能包18912以進行批量資產遷移{#installing-feature-pack-for-bulk-asset-migration}

安裝功能包18912 *可選*。

功能包18912允許您通過FTP將資產直接大量接收到Adobe Experience Manager的Dynamic Media-Scene7模式。 它還允許您將資產從Dynamic Media Classic遷移到Dynamic Media-Scene7Experience Manager模式。 功能包可從 [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html)。

>[!IMPORTANT]
>
>您可以使用功能包將資產從Dynamic Media Classic批量遷移到Dynamic Media — 在Experience Manager中使用Scene7模式。 您還可以使用Dynamic Media Classic的FTP功能批量遷移資產。 但是，Adobe *不* 建議您使用其中一種方法，因為涉及的複雜性。
>
>因此，此遷移功能包 *僅* 作為遷移項目的一部分支援 [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html)。

在安裝功能包之前，請建立服務用戶並提供該資訊以Adobe支援。

另請參閱[設定 Dynamic Media - Scene7 模式](/help/assets/config-dms7.md).

**要安裝功能包18912以進行批量資產遷移，請執行以下操作：**

1. 在Experience Manager實例中，導航至 **[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 用戶]** 選擇 **[!UICONTROL 建立用戶]**。 此服務用戶必須 *讀/寫* 權限 `/content/dam.`
1. 在 **[!UICONTROL ID]** 和 **[!UICONTROL 密碼]** 輸入用戶名和密碼；比如說， **FTP用戶**。 此名稱作為建立資產的用戶出現在時間軸中。 當從FTP上載資產時，當資產上載到FTP伺服器並被推入Experience Manager時，會考慮建立該資產。
1. 聯繫人 [Adobe客戶支援以Experience Manager](https://experienceleague.adobe.com/?support-solution=General#support) 請求訪問功能包18912以進行下載。 在與支援人員聯繫時，您可能需要以下資訊：

   * 作者實例的伺服器IP地址，包括埠號（預設情況下，埠號為4502）。
   * Experience Manager服務用戶的用戶名和密碼。

1. Adobe客戶Experience Manager支援為您提供FTP憑據和功能包18912的訪問權限。
1. 收到功能包18912後，請安裝它。

   請參閱 [如何使用包](/help/sites-administering/package-manager.md) 有關在Experience Manager中使用軟體分發和軟體包的詳細資訊。
