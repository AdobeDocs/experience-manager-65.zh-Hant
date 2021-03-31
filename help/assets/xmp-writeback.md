---
title: XMP回寫轉譯
description: 瞭解回寫功XMP能如何將資產的中繼資料變更傳播至資產的所有或特定轉譯。
contentOwner: AG
role: 業務從業人員、管理員
feature: 中繼資料
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 4%

---


# XMP回寫至轉譯{#xmp-writeback-to-renditions}

&lt;a0/XMP>中的此回寫功能會將中繼資料變更複製到原始資產的轉譯。 [!DNL Adobe Experience Manager Assets]當您從「資產」中變更資產的中繼資料，或在上傳資產時，這些變更最初會儲存在資產階層的中繼資料節點中。

回寫功XMP能可讓您將中繼資料變更傳播至資產的所有或特定轉譯。 該功能僅回寫那些使用`jcr`命名空間的元資料屬性，即，將回寫名為`dc:title`的屬性，但不回寫名為`mytitle`的屬性。

考慮將`Classic Leather`資產[!UICONTROL Title]屬性修改為`Nylon`的藍本。

![中繼資料](assets/metadata.png)

在這種情況下，[!DNL Experience Manager Assets]會將對`dc:title`參數中&#x200B;**[!UICONTROL Title]**&#x200B;屬性的變更儲存在資產階層中儲存的資產中繼資料。

![metadata_stored](assets/metadata_stored.png)

不過，[!DNL Experience Manager Assets]不會自動將任何中繼資料變更傳播至資產的轉譯。 請參閱[如何啟XMP用回寫](#enable-xmp-writeback)。

## 啟XMP用回寫{#enable-xmp-writeback}

若要啟用上傳資產時中繼資料變更，將其傳播至資產的轉譯，請修改Configuration Manager中的&#x200B;**[!UICONTROL Adobe CQDAM Rendition Maker]**&#x200B;組態。

1. 要開啟配置管理器，請訪問`https://[aem_server]:[port]/system/console/configMgr`。
1. 開啟&#x200B;**[!UICONTROL Adobe CQDAM轉譯製作器]**&#x200B;組態。
1. 選擇&#x200B;**[!UICONTROL 傳播XMP]**&#x200B;選項，然後保存更改。

   ![chlimage_1-135](assets/chlimage_1-346.png)

## 啟用XMP特定轉譯的回寫{#enabling-xmp-writeback-for-specific-renditions}

若要讓回寫XMP功能將中繼資料變更傳播至選取的轉譯，請將這些轉譯指定至[!UICONTROL XMPDAM中繼資料回寫]工作流程的回寫程式工作流程步驟。 依預設，此步驟會以原始轉譯設定。

對於「XMP回寫」功能，將中繼資料傳播至轉譯縮圖140.100.png和319.319.png，請執行這些步驟。

1. 在Experience Manager介面中，導航至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 從「模型」頁面，開啟&#x200B;**[!UICONTROL DAM元資料回寫]**&#x200B;工作流模型。
1. 在「 **[!UICONTROL DAM中繼資料回寫]** 」屬性頁面中，開啟 **[!UICONTROL 「XMP回寫程式」步驟]** 。
1. 在[!UICONTROL 步驟屬性]對話框中，按一下&#x200B;**[!UICONTROL 進程]**&#x200B;頁籤。
1. 在&#x200B;**參數**&#x200B;框中，添加`rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png` ，然後按一下&#x200B;**[!UICONTROL 確定]**。

   ![step_properties](assets/step_properties.png)

1. 儲存變更。
1. 若要使用新屬性重新產生[!DNL Dynamic Media]影像的金字塔TIFF轉譯，請將&#x200B;**[!UICONTROL Dynamic Media處理影像資產]**&#x200B;步驟新增至[!UICONTROL DAM中繼資料回寫]工作流程。

   PTIFF轉譯只會在Dynamic Media Hybrid實作中建立並儲存在本機。

1. 儲存工作流程。

中繼資料變更會傳播至資產的轉譯縮圖140.100.png和thumbnail.319.319.png，而非其他。

>[!NOTE]
>
>有XMP關64位Linux的回寫問題，請參見[如何在64位XMP RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)上啟用回寫。
>
>如需支援的平台，請參閱[XMP中繼資料回寫必要條件](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back)。

## 篩選XMP中繼資料{#filtering-xmp-metadata}

[!DNL Experience Manager Assets] 支援從資產二進位檔案讀取並在收XMP集資產時儲存在JCR中之中繼資料的封鎖清單和允許的屬性／節點清單篩選。

使用封鎖清單進行篩選可讓您匯入除XMP為排除指定之屬性以外的所有中繼資料屬性。 但是，對於具有大量中繼資料的資產類型(例如1000個XMP節點，具有10,000個屬性)，篩選的節點名稱不一定會事先知道。 如果使用封鎖的清單進行篩選可匯入大量包含XMP許多中繼資料的資產，則[!DNL Experience Manager]部署可能會遇到穩定性問題，例如阻塞的觀察佇列。

透過允XMP許的清單篩選中繼資料，可讓您定義要匯入的XMP屬性，以解決此問題。 這樣，會忽略任何其他或未知XMP的屬性。 為了向後相容性，您可以將其中某些屬性新增至使用封鎖清單的篩選器。

>[!NOTE]
>
>篩選僅適用於資產二進位檔中衍生XMP自來源的屬性。 對於從非來源衍生的XMP屬性（如EXIF和IPTC格式），篩選無效。 例如，資產建立日期儲存在EXIF TIFF中名為`CreateDate`的屬性中。 Experience Manager將此值儲存在名為`exif:DateTimeOriginal`的中繼資料欄位中。 由於來源是非來源，XMP因此篩選不適用於此屬性。

1. 要開啟配置管理器，請訪問`https://[aem_server]:[port]/system/console/configMgr`。
1. 開啟&#x200B;**[!UICONTROL Adobe CQDAM XmpFilter]**&#x200B;組態。
1. 要通過允許的清單應用過濾，請選擇&#x200B;**[!UICONTROL 將允許清單應XMP用到屬性]**，並在&#x200B;**[!UICONTROL 允許的XML名稱中指定要導入的屬性，以XMP進行過濾]**。

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. 若要在透過允XMP許的清單套用篩選後篩選已封鎖的屬性，請在&#x200B;**[!UICONTROL 篩選]**&#x200B;的「封鎖的XML名稱」方XMP塊中指定這些屬性。

   >[!NOTE]
   >
   >預設情況下，**[!UICONTROL 將塊清單應XMP用到屬性]**&#x200B;選項處於選中狀態。 換言之，預設會啟用使用封鎖清單進行篩選。 要禁用此類過濾，請取消選擇&#x200B;**[!UICONTROL 將塊清單應XMP用到屬性]**&#x200B;選項。

1. 儲存變更。
