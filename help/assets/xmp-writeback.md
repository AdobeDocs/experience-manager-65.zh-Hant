---
title: XMP回寫至轉譯
description: 瞭解XMP回寫功能如何將資產的中繼資料變更傳播至資產的所有或特定轉譯。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# XMP回寫至轉譯 {#xmp-writeback-to-renditions}

Adobe Experience Manager(AEM)Assets中的此XMP回寫功能會將資產中繼資料變更複製至資產的轉譯。

當您從AEM Assets中變更資產的中繼資料，或在上傳資產時，變更最初會儲存在Crx-De的資產節點中。

「XMP回寫」功能會將中繼資料變更傳播至資產的所有或特定轉譯。

請考慮您修改資產標題屬性的藍本 `Classic Leather` 為 `Nylon`。

![中繼資料](assets/metadata.png)

在此情況下，AEM Assets會將資產階層中儲存之資產中繼資料 **的參數中對Title**`dc:title` 屬性所做的變更儲存。

![metadata_stored](assets/metadata_stored.png)

不過，AEM Assets不會自動將任何中繼資料變更傳播至資產的轉譯。

XMP回寫功能可讓您將中繼資料變更傳播至資產的所有或特定轉譯。 不過，這些變更不會儲存在資產階層的中繼資料節點下。 此功能會在二進位檔案中內嵌轉譯的變更。

## 啟用XMP回寫 {#enabling-xmp-writeback}

若要啟用中繼資料變更在上傳資產時傳播至資產的轉譯，請在Configuration manager中修改 **Adobe CQ DAM Rendition Maker** configuration。

1. 要開啟配置管理器，請訪問 `https://[aem_server]:[port]/system/console/configMgr`。
1. 開啟 **Adobe CQ DAM Rendition Maker設定** 。
1. 選擇「 **傳播XMP** 」選項，然後保存更改。

   ![chlimage_1-135](assets/chlimage_1-346.png)

## 為特定轉譯啟用XMP回寫 {#enabling-xmp-writeback-for-specific-renditions}

若要讓「XMP回寫」功能將中繼資料變更傳播至選取的轉譯，請將這些轉譯指定至「DAM中繼資料回寫」工作流程的「XMP回寫程式」工作流程步驟。 依預設，此步驟會以原始轉譯設定。

對於「XMP回寫」功能，將中繼資料傳播至轉譯縮圖140.100.png和319.319.png，請執行這些步驟。

1. 點選／按一下AEM標誌，然後導覽至「工 **具** >工 **作流程** >模 **型**」。
1. 從「模型」頁面，開啟「 **DAM中繼資料回寫** 」工作流程模型。
1. 在「 **DAM中繼資料回寫** 」屬性頁面中，開啟 **「XMP回寫程式」步驟** 。
1. 在「步驟屬性」對話方塊中，點選／按一下「 **處理** 」標籤。
1. 在「參 **數** 」方塊中，新增 `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`，然後點選／按一下「 **確定」**。

   ![step_properties](assets/step_properties.png)

1. 儲存變更。
1. 若要使用新屬性重新產生動態媒體影像的金字塔TIF轉譯，請將 **** Dynamic Media Process Image Assets步驟新增至DAM中繼資料回寫工作流程。

   PTIFF轉譯只會在Dynamic Media Hybrid實作中建立並儲存在本機。

1. 儲存工作流程。

中繼資料變更會傳播至資產的轉譯縮圖140.100.png和thumbnail.319.319.png，而非其他。

>[!NOTE]
>
>有關64位元Linux中的XMP回寫問題，請參 [閱如何在64位元RedHat linux上啟用XMP回寫](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)。
>
>如需支援平台的詳細資訊，請參閱 [XMP中繼資料回寫的必要條件](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back)。

## 篩選XMP中繼資料 {#filtering-xmp-metadata}

AEM Assets支援黑名單和白名單篩選XMP中繼資料的屬性／節點，從資產二進位檔案讀取，並在收錄資產時儲存在JCR中。

黑名單篩選功能可讓您匯入除為排除而指定的屬性以外的所有XMP中繼資料屬性。 不過，對於資產類型（例如具有大量XMP中繼資料的INDD檔案）（例如1000個節點，具有10,000個屬性），篩選的節點名稱不一定都會事先知道。 如果黑名單篩選允許匯入大量包含大量XMP中繼資料的資產，AEM例項／叢集可能會遇到穩定性問題，例如阻塞的觀察佇列。

XMP中繼資料的白名單篩選可讓您定義要匯入的XMP屬性，以解決此問題。 這樣，將忽略其他／未知的XMP屬性。 您可以將這些屬性中的某些屬性添加到黑名單過濾器中，以便向後相容。

>[!NOTE]
>
>篩選只適用於資產二進位檔中衍生自XMP來源的屬性。 對於從非XMP來源衍生的屬性（例如EXIF和IPTC格式），篩選無法運作。 例如，資產建立日期會儲存在以EXIF TIFF命名的 `CreateDate` 屬性中。 AEM在名為的中繼資料欄位中提到此值 `exif:DateTimeOriginal`。 由於來源是非XMP來源，因此篩選不適用於此屬性。

1. 要開啟配置管理器，請訪問 `https://[aem_server]:[port]/system/console/configMgr`。
1. 開啟 **Adobe CQ DAM XmpFilter組態** 。
1. 若要套用白名單篩選，請選 **取「套用白名單至XMP屬性」**，並指定要在「白名單的XML名稱供XMP篩選」方 **塊中匯入的屬性** 。

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. 若要在套用白名單篩選後篩除黑名單XMP屬性，請在「XMP篩選的黑名單XML名 **稱」方塊中指定** 。

   >[!NOTE]
   >
   >預設 **情況下，「將黑名單應用於XMP屬性** 」選項處於選中狀態。 換言之，黑名單篩選預設為啟用。 要禁用黑名單過濾，請取消選 **擇將黑名單應用於XMP屬性** 。

1. 儲存變更。
