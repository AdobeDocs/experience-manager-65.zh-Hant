---
title: XMP回寫至轉譯
description: 瞭解XMP回寫功能如何將資產的中繼資料變更傳播至資產的所有或特定轉譯。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 711cd438cc8962d310bb2bfbb14f079161aacce0
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 4%

---


# XMP回寫至轉譯 {#xmp-writeback-to-renditions}

中的XMP回寫功能 [!DNL Adobe Experience Manager Assets] 會將資產中繼資料變更複製至資產的轉譯。 當您從資產內部或上傳資產時變更資 [!DNL Experience Manager Assets] 產的中繼資料時，變更最初會儲存在CRXDe的資產節點中。 XMP回寫功能會將中繼資料變更傳播至資產的所有或特定轉譯。

請考慮您修改資產 [!UICONTROL 標題] (Title)屬性的 `Classic Leather` 藍本 `Nylon`。

![中繼資料](assets/metadata.png)

在此情況下，會 [!DNL Experience Manager Assets] 將資產階層中儲存的資產中繼資 ****`dc:title` 料的參數中，儲存對Title屬性的變更。

![metadata_stored](assets/metadata_stored.png)

不過， [!DNL Experience Manager Assets] 不會自動將任何中繼資料變更傳播至資產的轉譯。

XMP回寫功能可讓您將中繼資料變更傳播至資產的所有或特定轉譯。 不過，這些變更不會儲存在資產階層的中繼資料節點下。 此功能會在二進位檔案中內嵌轉譯的變更。

## 啟用XMP回寫 {#enabling-xmp-writeback}

若要啟用中繼資料變更在上傳資產時傳播至資產的轉譯，請在Configuration Manager中修改 **[!UICONTROL Adobe CQ DAM Rendition Maker]** configuration。

1. 要開啟配置管理器，請訪問 `https://[aem_server]:[port]/system/console/configMgr`。
1. 開啟 **[!UICONTROL Adobe CQ DAM Rendition Maker設定]** 。
1. 選擇**[!UICONTROL傳播XMP[!UICONTROL **選項，然後保存更改。

   ![chlimage_1-135](assets/chlimage_1-346.png)

## 為特定轉譯啟用XMP回寫 {#enabling-xmp-writeback-for-specific-renditions}

若要讓「XMP回寫」功能將中繼資料變更傳播至選取的轉譯，請將這些轉譯指定至「 [!UICONTROL DAM中繼資料回寫」工作流程的「XMP回寫程式」工作流程步驟] 。 依預設，此步驟會以原始轉譯設定。

對於「XMP回寫」功能，將中繼資料傳播至轉譯縮圖140.100.png和319.319.png，請執行這些步驟。

1. 在Experience Manager介面中，導覽至「工 **[!UICONTROL 具]** >工 **[!UICONTROL 作流程]** > **[!UICONTROL 模型]**」。
1. 從「模型」頁面，開啟「 **[!UICONTROL DAM中繼資料回寫]** 」工作流程模型。
1. 在「 **[!UICONTROL DAM中繼資料回寫]** 」屬性頁面中，開啟 **[!UICONTROL 「XMP回寫程式」步驟]** 。
1. In the [!UICONTROL Step Properties] dialog box, click the **[!UICONTROL Process]** tab.
1. 在「參 **數** 」框中，添加 `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`，然後按一下「 **確定」**。

   ![step_properties](assets/step_properties.png)

1. 儲存變更。
1. To regenerate the pyramid TIFF renditions for [!DNL Dynamic Media] images with the new attributes, add the **[!UICONTROL Dynamic Media Process Image Assets]** step to the [!UICONTROL DAM Metadata Writeback] workflow.

   PTIFF轉譯只會在Dynamic Media Hybrid實作中建立並儲存在本機。

1. 儲存工作流程。

中繼資料變更會傳播至資產的轉譯縮圖140.100.png和thumbnail.319.319.png，而非其他。

>[!NOTE]
>
>有關64位元Linux中的XMP回寫問題，請參 [閱如何在64位元RedHat Linux上啟用XMP回寫](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)。
>
>如需支援平台的詳細資訊，請參閱 [XMP中繼資料回寫的必要條件](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back)。

## 篩選XMP中繼資料 {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] 支援從資產二進位檔案讀取並在收錄資產時儲存在JCR中的XMP中繼資料的封鎖清單和允許的屬性／節點清單篩選。

使用封鎖清單進行篩選可讓您匯入所有XMP中繼資料屬性，但為排除指定的屬性除外。 不過，對於資產類型（例如具有大量XMP中繼資料的INDD檔案）（例如1000個節點，具有10,000個屬性），篩選的節點名稱不一定都會事先知道。 如果使用封鎖清單進行篩選可讓大量包含大量XMP中繼資料的資產匯入，AEM例項／叢集可能會遇到穩定性問題，例如阻塞的觀察佇列。

透過允許的清單篩選XMP中繼資料可讓您定義要匯入的XMP屬性，以解決此問題。 如此，就會忽略任何其他或未知的XMP屬性。 為了向後相容性，您可以將其中某些屬性新增至使用封鎖清單的篩選器。

>[!NOTE]
>
>篩選只適用於資產二進位檔中衍生自XMP來源的屬性。 對於從非XMP來源衍生的屬性（例如EXIF和IPTC格式），篩選無法運作。 例如，資產建立日期會儲存在以EXIF TIFF命名的 `CreateDate` 屬性中。 Experience Manager將此值儲存在名為的中繼資料欄位中 `exif:DateTimeOriginal`。 由於來源是非XMP來源，因此篩選不適用於此屬性。

<!-- TBD: The instructions don't seem to match the UI. I see com.day.cq.dam.commons.metadata.XmpFilterBlackWhite.description
in Config Manager. And the settings are,
com.day.cq.dam.commons.metadata.XmpFilterBlackWhite.xmp.filter.apply_whitelist.name
com.day.cq.dam.commons.metadata.XmpFilterBlackWhite.xmp.filter.whitelist.name
com.day.cq.dam.commons.metadata.XmpFilterBlackWhite.xmp.filter.apply_blacklist.name
com.day.cq.dam.commons.metadata.XmpFilterBlackWhite.xmp.filter.blacklist.name
 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

1. 要開啟配置管理器，請訪問 `https://[aem_server]:[port]/system/console/configMgr`。
1. 開啟 **[!UICONTROL Adobe CQ DAM XmpFilter組態]** 。
1. To apply filtering via an allowed list, select **[!UICONTROL Apply Allowlist to XMP Properties]**, and specify the properties to be imported in the **[!UICONTROL Allowed XML Names for XMP filtering]** box.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. 若要在透過允許的清單套用篩選後篩選已封鎖的XMP屬性，請在「XMP篩選的封鎖的XML **[!UICONTROL 名稱」方塊中指定]** 。

   >[!NOTE]
   >
   >預設 **[!UICONTROL 情況下，「將塊清單應用到XMP屬性]** 」選項處於選中狀態。 換言之，預設會啟用使用封鎖清單進行篩選。 要禁用此類過濾，請取消選 **[!UICONTROL 擇「將塊清單應用到XMP屬性]** 」選項。

1. 儲存變更。
