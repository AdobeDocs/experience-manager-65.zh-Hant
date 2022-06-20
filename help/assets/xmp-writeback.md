---
title: XMP回寫到格式副本
description: 瞭解寫回XMP功能如何將資產的元資料更改傳播到資產的所有或特定格式副本。
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 82148ae5-37e9-4fc5-ada9-db3d91b29c33
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 5%

---

# XMP回寫到格式副本 {#xmp-writeback-to-renditions}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/xmp-metadata.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/xmp-writeback.html?lang=en) |

中XMP的此寫回功能 [!DNL Adobe Experience Manager Assets] 將元資料更改複製到原始資產的格式副本。 當您從資產內更改資產的元資料或在上載資產時，這些更改最初儲存在資產層次結構中的元資料節點中。

寫回XMP功能允許您將元資料更改傳播到資產的所有或特定格式副本。 該功能僅回寫那些使用 `jcr` 命名空間，即名為 `dc:title` 寫回，但名為 `mytitle` 不。

考慮修改 [!UICONTROL 標題] 標題為 `Classic Leather` 至 `Nylon`。

![中繼資料](assets/metadata.png)

在這個例子中， [!DNL Experience Manager Assets] 將更改保存到 **[!UICONTROL 標題]** 屬性 `dc:title` 資產層次結構中儲存的資產元資料的參數。

![元資料已儲存](assets/metadata_stored.png)

但是， [!DNL Experience Manager Assets] 不會自動將任何元資料更改傳播到資產的格式副本。 請參閱 [如何啟XMP用寫回](#enable-xmp-writeback)。

## 啟用寫XMP回 {#enable-xmp-writeback}

要在上載資產時允許元資料更改傳播到資產的格式副本，請修改 **[!UICONTROL Adobe CQDAM Rendition Maker]** 配置。

1. 要開啟Configuration Manager，請訪問 `https://[aem_server]:[port]/system/console/configMgr`。
1. 開啟 **[!UICONTROL Adobe CQDAM Rendition Maker]** 配置。
1. 選擇 **[!UICONTROL 傳播XMP]** ，然後保存更改。

   ![chlimage_1-135](assets/chlimage_1-346.png)

## 為特定XMP格式副本啟用寫回 {#enabling-xmp-writeback-for-specific-renditions}

要讓寫回功XMP能傳播元資料更改以選擇格式副本，請將這些格式副本指定XMP到的寫回流程工作流步驟 [!UICONTROL DAM元資料回寫] 工作流。 預設情況下，此步驟配置有原始格式副本。

對於「寫XMP回」功能將元資料傳播到格式副本縮略圖140.100.png和319.319.png，請執行這些步驟。

1. 在Experience Manager介面中，導航到 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
1. 從「模型」頁面，開啟 **[!UICONTROL DAM元資料寫回]** 工作流模型。
1. 在「 **[!UICONTROL DAM中繼資料回寫]** 」屬性頁面中，開啟 **[!UICONTROL 「XMP回寫程式」步驟]** 。
1. 在 [!UICONTROL 步驟屬性] 對話框，按一下 **[!UICONTROL 進程]** 頁籤。
1. 在 **參數** 框，添加 `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`，然後按一下 **[!UICONTROL 確定]**。

   ![步驟屬性](assets/step_properties.png)

1. 儲存變更。
1. 重新生成金字塔TIFF格式副本 [!DNL Dynamic Media] 影像，添加 **[!UICONTROL Dynamic Media處理映像資產]** 的 [!UICONTROL DAM元資料寫回] 工作流。

   PTIFF轉譯只會在Dynamic Media Hybrid實作中建立並儲存在本機。

1. 保存工作流。

元資料更改將傳播到資產的格式副本thumbnail.140.100.png和thumbnail.319.319.png，而不是其他格式副本。

>[!NOTE]
>
>有關XMP64位Linux中的寫回問題，請參見 [如何在XMP64位RedHat Linux上啟用回寫](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)。
>
>有關支援的平台，請參見 [元XMP資料回寫先決條件](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back)。

## 篩選元XMP資料 {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] 支援阻止清單和允許清單篩選從資產二進位檔案中讀取XMP的元資料的屬性/節點，並在接收資產時儲存在JCR中。

使用阻止清單進行篩選可導入除為XMP排除而指定的屬性之外的所有元資料屬性。 但是，對於具有大量元資料(例如XMP1000個節點，有10,000個屬性)的資產類型（如INDD檔案），要篩選的節點名稱並不總是預先知道的。 如果使用阻止清單進行篩選允許導入大量具有大量元資料XMP的資產，則 [!DNL Experience Manager] 部署可能會遇到穩定性問題，例如阻塞的觀察隊列。

通過允XMP許清單篩選元資料可通過定義要導入的XMP屬性來解決此問題。 這樣，將忽略任何其他或未XMP知屬性。 為了向後相容，可以將其中一些屬性添加到使用阻止清單的篩選器中。

>[!NOTE]
>
>篩選僅適用於資產二進位檔案中從XMP源派生的屬性。 對於從非源(如EXIF和IPTC格XMP式)派生的屬性，篩選不起作用。 例如，資產建立日期儲存在名為 `CreateDate` 的子菜單。 Experience Manager將此值儲存在名為 `exif:DateTimeOriginal`。 由於源是非源，XMP因此篩選對此屬性無效。

1. 要開啟Configuration Manager，請訪問 `https://[aem_server]:[port]/system/console/configMgr`。
1. 開啟 **[!UICONTROL Adobe CQDAM XmpFilter]** 配置。
1. 要通過允許的清單應用篩選，請選擇 **[!UICONTROL 將允許清單應用於屬XMP性]**，並指定要在 **[!UICONTROL 允許的XML名稱XMP篩選]** 框。

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. 要在通過允許的列XMP表應用篩選後篩選出被阻止的屬性，請在 **[!UICONTROL 已阻止的XML名稱XMP進行篩選]** 框。

   >[!NOTE]
   >
   >的 **[!UICONTROL 將塊清單應用於屬XMP性]** 選項。 換句話說，預設情況下啟用使用阻止清單的過濾。 要禁用此篩選，請取消選擇 **[!UICONTROL 將塊清單應用於屬XMP性]** 的雙曲餘切值。

1. 儲存變更。
