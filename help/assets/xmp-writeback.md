---
title: XMP回寫至轉譯
description: 瞭解XMP回寫功能如何將資產的中繼資料變更傳播至資產的所有或特定轉譯。
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 82148ae5-37e9-4fc5-ada9-db3d91b29c33
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 0b90fdd13efc5408ef94ee1966f04a80810b515e
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 6%

---

# XMP回寫至轉譯 {#xmp-writeback-to-renditions}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [按一下這裡](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/admin/xmp-metadata) |
| AEM 6.5 | 本文章 |

[!DNL Adobe Experience Manager Assets]中的這個XMP回寫功能會將中繼資料變更復寫至原始資產的轉譯。 當您從Assets內變更資產的中繼資料或上傳資產時，變更最初會儲存在資產階層中的中繼資料節點中。

XMP回寫功能可讓您將中繼資料變更傳播至資產的所有或特定轉譯。 功能只會回寫使用已登入名稱空間的中繼資料屬性，也就是說，會回寫名為`dc:title`的屬性，但不回寫名為`mytitle`的屬性。

假設您將[!UICONTROL Title]屬性（標題為`Classic Leather`至`Nylon`）修改為的情況。

![中繼資料](assets/metadata.png)

在此案例中，[!DNL Experience Manager Assets]會針對儲存在資產階層中的資產中繼資料，將變更儲存在`dc:title`引數中的&#x200B;**[!UICONTROL Title]**&#x200B;屬性。

![metadata_stored](assets/metadata_stored.png)

但是，[!DNL Experience Manager Assets]不會自動將任何中繼資料變更傳播到資產的轉譯。 請參閱如何啟用XMP回寫[&#128279;](#enable-xmp-writeback)。

## 啟用XMP回寫 {#enable-xmp-writeback}

若要讓中繼資料變更在上傳資產時傳播至資產的轉譯，請在Configuration Manager中修改&#x200B;**[!UICONTROL Adobe CQ DAM Rendition Maker]**&#x200B;設定。

1. 若要開啟[組態管理員]，請存取`https://[aem_server]:[port]/system/console/configMgr`。
1. 開啟&#x200B;**[!UICONTROL Adobe CQ DAM Rendition Maker]**&#x200B;設定。
1. 選取&#x200B;**[!UICONTROL 傳播XMP]**&#x200B;選項，然後儲存變更。

   ![chlimage_1-135](assets/chlimage_1-346.png)

## 為特定轉譯啟用XMP回寫 {#enabling-xmp-writeback-for-specific-renditions}

若要讓XMP回寫功能傳播中繼資料變更以選取轉譯，請將這些轉譯指定至[!UICONTROL DAM中繼資料回寫]工作流程的XMP回寫程式工作流程步驟。 依預設，此步驟會使用原始轉譯進行設定。

若要XMP回寫功能將中繼資料傳播至轉譯縮圖140.100.png和319.319.png，請執行這些步驟。

1. 在Experience Manager介面中，導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**。
1. 從「模型」頁面，開啟&#x200B;**[!UICONTROL DAM中繼資料回寫]**&#x200B;工作流程模型。
1. 在「 **[!UICONTROL DAM中繼資料回寫]** 」屬性頁面中，開啟 **[!UICONTROL 「XMP回寫程式」步驟]** 。
1. 在[!UICONTROL 步驟屬性]對話方塊中，按一下&#x200B;**[!UICONTROL 處理序]**&#x200B;索引標籤。
1. 在&#x200B;**引數**&#x200B;方塊中，新增`rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`並按一下&#x200B;**[!UICONTROL 確定]**。

   ![step_properties](assets/step_properties.png)

1. 儲存變更。
1. 若要使用新屬性重新產生[!DNL Dynamic Media]影像的金字塔TIFF轉譯，請將&#x200B;**[!UICONTROL 動態媒體處理影像Assets]**&#x200B;步驟新增至[!UICONTROL DAM中繼資料回寫]工作流程。

   PTIFF轉譯只會在Dynamic Media Hybrid實作中建立並儲存在本機。

1. 儲存工作流程。

中繼資料變更會傳播至資產的轉譯thumbnail.140.100.png和thumbnail.319.319.png ，而不是其他專案。

>[!NOTE]
>
>如需支援的平台，請參閱[XMP中繼資料回寫先決條件](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back)。

## 篩選XMP中繼資料 {#filtering-xmp-metadata}

[!DNL Experience Manager Assets]支援針對從資產二進位檔讀取並在擷取資產時儲存在JCR中的XMP中繼資料，篩選屬性/節點的封鎖清單和允許清單。

使用封鎖清單進行篩選時，可讓您匯入所有XMP中繼資料屬性，但為排除專案指定的屬性除外。 然而，對於具有大量XMP中繼資料的資產型別（例如，有1000個節點，具有10,000個屬性），要篩選的節點名稱並不一定是事先知道的。 如果使用封鎖清單進行篩選，可匯入大量含有許多XMP中繼資料的資產，則[!DNL Experience Manager]部署可能會遇到穩定性問題，例如觀測佇列阻塞。

透過允許清單篩選XMP中繼資料可讓您定義要匯入的XMP屬性，以解決此問題。 如此一來，任何其他或未知的XMP屬性都會被忽略。 為了回溯相容性，您可以將其中一些屬性新增至使用封鎖清單的篩選器。

>[!NOTE]
>
>篩選僅適用於資產二進位檔中衍生自XMP來源的屬性。 對於衍生自非XMP來源(例如EXIF和IPTC格式)的屬性，篩選無法運作。 例如，建立資產的日期儲存在EXIF TIFF中名為`CreateDate`的屬性中。 Experience Manager將此值儲存在名為`exif:DateTimeOriginal`的中繼資料欄位中。 由於來源是非XMP來源，因此篩選在此屬性上無法運作。

1. 若要開啟[組態管理員]，請存取`https://[aem_server]:[port]/system/console/configMgr`。
1. 開啟&#x200B;**[!UICONTROL Adobe CQ DAM XmpFilter]**&#x200B;設定。
1. 若要透過允許清單套用篩選，請選取&#x200B;**[!UICONTROL 套用允許清單至XMP屬性]**，並指定要在&#x200B;**[!UICONTROL XMP篩選的允許XML名稱]**&#x200B;方塊中匯入的屬性。

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. 若要透過允許清單套用篩選後，篩選掉封鎖的XMP屬性，請在&#x200B;**[!UICONTROL XMP篩選的封鎖XML名稱]**&#x200B;方塊中指定這些屬性。

   >[!NOTE]
   >
   >預設會選取&#x200B;**[!UICONTROL 套用封鎖清單至XMP屬性]**&#x200B;選項。 換言之，使用封鎖清單的篩選功能預設為啟用。 若要停用這類篩選，請取消選取&#x200B;**[!UICONTROL 套用封鎖清單至XMP屬性]**&#x200B;選項。

1. 儲存變更。
