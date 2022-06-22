---
title: 管理您的數位資產
description: 瞭解資產管理任務，如上載、下載、編輯、搜索、刪除、注釋和版本數字資產。
contentOwner: AG
role: User
feature: Asset Management,Search
mini-toc-levels: 4
exl-id: 158607e6-b4e9-4a3f-b023-4023d60c97d2
source-git-commit: dabd27389c9fc5f30589d554ba4da8fce041dd4b
workflow-type: tm+mt
source-wordcount: '9974'
ht-degree: 4%

---

# 管理您的數位資產 {#manage-digital-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-digital-assets.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/managing-assets-touch-ui.html?lang=en) |

在 [!DNL Adobe Experience Manager Assets]你可以做的不止是儲存和管理資產。 [!DNL Experience Manager] 提供企業級資產管理功能。 您可以編輯和共用資產、運行高級搜索，以及建立數十種受支援檔案格式的多個格式副本。 您還可以管理版本和數字權限、自動處理資產、管理和管理元資料、使用注釋進行協作等。

本文介紹了建立或上載等基本資產管理任務；元資料更新；複製、移動和刪除；發佈、取消發佈和搜索資產。 要瞭解用戶介面，請參見 [開始使用assets用戶介面](/help/sites-authoring/basic-handling.md)。 要管理內容片段，請參見 [管理內容片段](/help/assets/content-fragments/content-fragments-managing.md) 資產。

## 建立檔案夾 {#creating-folders}

組織資產集合時，例如， `Nature` 影像，您可以建立資料夾以將它們保持在一起。 您可以使用資料夾對資產進行分類和組織。 [!DNL Experience Manager Assets] 不要求您組織資料夾中的資產以更好地工作。

>[!NOTE]
>
>* 共用 [!DNL Assets] 類型的資料夾 `sling:OrderedFolder` 共用到Experience Cloud時不受支援。 如果要共用資料夾，不要選擇 [!UICONTROL 已訂購] 建立資料夾時。
>* [!DNL Experience Manager] 不允許使用 `subassets` word作為資料夾的名稱。 它是為包含複合資產子集的節點保留的關鍵字。


1. 導航到要建立資料夾的數字資產資料夾中的位置。 在菜單中，按一下 **[!UICONTROL 建立]**。 選擇 **[!UICONTROL 新建資料夾]**。
1. 在 **[!UICONTROL 標題]** 欄位，提供資料夾名稱。 預設情況下，DAM使用您提供的標題作為資料夾名稱。 建立資料夾後，可以覆蓋預設資料夾並指定另一個資料夾名稱。
1. 按一下&#x200B;**[!UICONTROL 建立]**。您的資料夾顯示在數字資產資料夾中。

不支援以下（以空格分隔的）字元清單：

* 資產檔案名不能包含以下任何字元： `* / : [ \\ ] | # % { } ? &`
* 資產資料夾名稱不能包含以下任何字元： `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

不要在資產檔案名的副檔名中包含特殊字元。

## 上傳資產 {#uploading-assets}

<!-- TBD the following:
Move this section into a new article. CQDOC-14874 ticket is created for this.
In this complete article, replace emphasis with UICONTROL where appropriate.
-->

您可以從本地資料夾或網路驅動器上載各種類型的資產(包括影像、PDF檔案、RAW檔案等)到 [!DNL Experience Manager Assets]。

>[!NOTE]
>
>在Dynamic Media-Scene7模式下，預設資產上載檔案大小為2 GB或更小。 要配置大於2 GB的上載資產，請參見 [（可選）配置Dynamic Media-Scene7模式以上載大於2 GB的資產](/help/assets/config-dms7.md#optional-config-dms7-assets-larger-than-2gb)。

您可以選擇將資產上載到具有或不具有分配給它們的處理配置檔案的資料夾。

對於已分配了處理配置檔案的資料夾，配置檔案名稱將顯示在卡視圖中的縮略圖上。 在清單視圖中，配置檔案名稱將出現在 **處理配置檔案** 的雙曲餘切值。 請參閱 [處理配置檔案](/help/assets/processing-profiles.md)。

在上載資產之前，請確保它位於 [格式](/help/assets/assets-formats.md) 那 [!DNL Experience Manager Assets] 支援。

1. 在 [!DNL Assets] 用戶介面，導航到要添加數字資產的位置。
1. 要上載資產，請執行以下操作之一：

   * 在工具欄上，按一下 **[!UICONTROL 建立]**。 然後，在菜單上，按一下 **[!UICONTROL 檔案]**。 如果需要，可在顯示的對話框中更名檔案。
   * 在支援HTML5的瀏覽器中，將資產直接拖到 [!DNL Assets] 用戶介面。 不顯示要更名檔案的對話框。

   ![建立選項以上載資產](assets/create-options.png)

   要選擇多個檔案，請選擇 `Ctrl` 或 `Command` 鍵，然後在檔案選取器對話框中選擇資產。 使用iPad時，一次只能選擇一個檔案。

   您可以暫停上載大型資產（大於500 MB），稍後從同一頁恢復。 按一下 **[!UICONTROL 暫停]** 位於上載開始時顯示的進度欄旁邊。

   ![上載資產進度欄](assets/upload-progress-bar.png)

資產被視為大型資產的大小可以配置。 例如，可以將系統配置為將1000 MB以上（而不是500 MB）的資產視為大資產。 在這個例子中， **[!UICONTROL 暫停]** 當上載大於1000 MB的資產時，將顯示在進度欄上。

的 [!UICONTROL 暫停] 選項不顯示是否上載的檔案大於1000 MB且檔案小於1000 MB。 但是，如果取消少於1000-MB的檔案上載， **[!UICONTROL 暫停]** 的子菜單。

要修改大小限制，請配置 `chunkUploadMinFileSize` 屬性 `fileupload` 的子目錄。

按一下 **[!UICONTROL 暫停]**，則切換到 **[!UICONTROL 播放]** 的雙曲餘切值。 要繼續上載，請按一下 **[!UICONTROL 播放]**。

要取消正在進行的上載，請按一下「關閉」(`X`)。 取消上載操作後， [!DNL Assets] 刪除資產的部分上載部分。

在低頻寬情況和網路故障中，恢復上載功能尤其有用，在這些情況下，上載大型資產需要很長時間。 您可以暫停上載操作，並在情況好轉後繼續。 恢復時，上載從暫停時開始。

在上載操作期間， [!DNL Experience Manager] 將上載的資產部分作為資料塊保存在CRX儲存庫中。 上載完成後， [!DNL Experience Manager] 將這些塊合併到儲存庫中的單個資料塊中。

要為未完成的區塊上載作業配置清除任務，請轉到 `https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`。

>[!CAUTION]
>
>當預設值為500 MB且區塊大小為50 MB時，將觸發區塊上載。 如果編輯 [Apache Jackrabbit Oak TokenConfiguration](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16464.html) 並設定 `timeout configuration` 如果要上載資產所花的時間少於，則在資產上載過程中會遇到會話超時情況。 因此，更改 `chunkUploadMinFileSize` 和 `chunksize` 以便每個區塊請求刷新會話。
>
>給定憑據到期超時、延遲、頻寬和預期的併發上載，可確保選擇以下項的最高值：
>
>* 確保在上載過程中為可能導致憑據過期的大小的檔案啟用區塊上載。
>
>* 確保每個區塊在憑據過期之前完成。


如果上載的資產名稱與上載資產的位置已可用的資產名稱相同，則會顯示警告對話框。

您可以選擇替換現有資產、建立其他版本或通過更名已上載的新資產來保留兩者。 如果替換現有資產，則資產的元資料以及您對現有資產所做的任何先前修改（例如注釋或裁剪）都將被刪除。 如果選擇保留兩個資產，則新資產將更名為數字 `1` 附加到其名稱。

![「名稱衝突」對話框以解決資產名稱衝突](assets/resolve-naming-conflict.png)

>[!NOTE]
>
>選擇時 **[!UICONTROL 替換]** 的 [!UICONTROL 名稱衝突] 對話框，將為新資產重新生成資產ID。 此ID與上一個資產的ID不同。
>
>如果啟用了Assets Insights以跟蹤觀點或按一下 [!DNL Adobe Analytics]，重新生成的資產ID將使為上的資產捕獲的資料失效 [!DNL Analytics]。

如果上載的資產存在於 [!DNL Assets]，也請參見Wiki頁。 **[!UICONTROL 檢測到重複項]** 對話框警告您嘗試上載重複的資產。 僅當 `SHA 1` 現有資產的二進位校驗和值與您上載的資產的校驗和值匹配。 在這種情況下，資產名稱無關緊要。

>[!NOTE]
>
>的 [!UICONTROL 檢測到重複項] 對話框僅在啟用重複檢測功能時顯示。 要啟用重複檢測功能，請參見 [啟用重複檢測](/help/assets/duplicate-detection.md)。

![「檢測到重複的資產」對話框](assets/duplicate-asset-detected.png)

將重複資產保留在 [!DNL Assets]按一下 **[!UICONTROL 保留]**。 要刪除上載的重複資產，請按一下 **[!UICONTROL 刪除]**。

[!DNL Experience Manager Assets] 阻止您使用其檔案名中的禁止字元上載資產。 如果嘗試上載包含不允許的字元或更多字元的檔案名的資產， [!DNL Assets] 顯示警告消息並停止上載，直到您刪除這些字元或使用允許的名稱上載。

要適合組織的特定檔案命名約定， [!UICONTROL 上載資產] 對話框用於為上載的檔案指定長名稱。

但是，不支援以下（以空格分隔的）字元清單：

* 資產檔案名不能包含 `* / : [ \\ ] | # % { } ? &`
* 資產資料夾名稱不包含 `* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

不要在資產檔案名的副檔名中包含特殊字元。

![「上載進度」對話框顯示成功上載的檔案和無法上載的檔案的狀態](assets/bulk-upload-progress.png)

另外， [!DNL Assets] 用戶介面顯示您上載的最新資產或您首先建立的資料夾。

如果在上載檔案之前取消上載操作， [!DNL Assets] 停止上載當前檔案並刷新內容。 但是，不會刪除已上載的檔案。

上載進度對話框 [!DNL Assets] 顯示成功上載的檔案和無法上載的檔案的計數。

### 串列上載 {#serialuploads}

批量上載大量資產會佔用大量I/O資源，這可能會對您的效能產生負面影響 [!DNL Assets] 部署。 特別是，如果您的Internet連接速度較慢，則由於磁碟I/O激增，上載的時間會顯著增加。此外，您的Web瀏覽器可能會對POST請求數施加其他限制 [!DNL Assets] 可以處理併發資產上載。 因此，上載操作將失敗或提前終止。 換句話說， [!DNL Experience Manager Assets] 可能會在接收大量檔案時丟失某些檔案，或完全無法接收任何檔案。

為了克服這種局面， [!DNL Assets] 在批量上載操作期間一次接收一個資產（串列上載），而不是同時接收所有資產。

預設情況下啟用資產的串列上載。 要禁用功能並允許併發上載，請覆蓋 `fileupload` 節點，並設定 `parallelUploads` 屬性 `true`。

### 使用FTP上載資產 {#uploading-assets-using-ftp}

Dynamic Media支援通過FTP伺服器批量上載資產。 如果要上載大資產(>1 GB)或上載整個資料夾和子資料夾，則應使用FTP。 您甚至可以設定FTP上載，以定期執行。

>[!NOTE]
>
>在Dynamic Media-Scene7模式下，預設資產上載檔案大小為2 GB或更小。 要配置大於2 GB的上載資產，請參見 [（可選）配置Dynamic Media-Scene7模式以上載大於2 GB的資產](/help/assets/config-dms7.md#optional-config-dms7-assets-larger-than-2gb)。

>[!NOTE]
>
>要在Dynamic Media-Scene7模式下通過FTP上傳資產，請在 [!DNL Experience Manager] 作者實例。 聯繫人 [Adobe客戶支援](https://experienceleague.adobe.com/?support-solution=General#support) 訪問FP-18912並完成FTP帳戶的設定。 有關詳細資訊，請參見 [安裝功能包18912以進行批量資產遷移](/help/assets/bulk-ingest-migrate.md)。
>
>如果使用FTP上載資產，請在 [!DNL Experience Manager] 忽略。 而是使用在Dynamic Media Classic中定義的檔案處理規則。

**使用FTP上載資產**

1. 使用您選擇的FTP客戶端，使用您從預配電子郵件收到的FTP用戶名和密碼登錄到FTP伺服器。 在FTP客戶端中，將檔案或資料夾上載到FTP伺服器。

1. 開啟 [Dynamic Media Classic台式機應用](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html#system-requirements-dmc-app)，然後登錄到您的帳戶。

   您的憑據和登錄是在設定時由Adobe提供的。 如果您沒有此資訊，請與Adobe客戶支援聯繫。

1. 在全局導航欄上，按一下 **[!UICONTROL 上載]**。
1. 在「上載」(Upload)頁面的左上角附近，按一下 **[!UICONTROL 通過FTP]** 頁籤。
1. 在頁面左側，選擇要上載檔案的FTP資料夾；在頁面的右側，選擇目標資料夾。
1. 在頁面右下角附近，按一下 **[!UICONTROL 作業選項]** 然後根據所選資料夾中的資產設定所需選項。

   請參閱 [上載作業選項](#upload-job-options)。

   >[!NOTE]
   >
   >通過FTP上載資產時，您在Dynamic Media Classic(S7)中設定的上載作業選項將優先於在 [!DNL Experience Manager]。

1. 在「上載作業選項」對話框的右下角，按一下 **[!UICONTROL 保存]**。
1. 在上載頁面的右下角，按一下 **[!UICONTROL 提交上載]**。

   要查看上載進度，請在全局導航欄上按一下 **[!UICONTROL 作業]**。 「作業」頁顯示上載的進度。 您可以繼續工作 [!DNL Experience Manager] 並隨時返回Dynamic Media Classic的「工作」頁面，以查看正在執行的工作。
要取消正在執行的上載作業，請按一下 **[!UICONTROL 取消]** 在工期時間旁邊。

#### 上載作業選項 {#upload-job-options}

| 上載選項 | 子選項 | 說明 |
|---|---|---|
| 工作名稱 |  | 預填充在文本欄位中的預設名稱包括用戶輸入的名稱部分和日期和時間戳。 您可以使用預設名稱，或為此上載作業輸入自己建立的名稱。 <br>作業以及其他上載和發佈作業將記錄在「作業」頁面中，您可以在該頁面中檢查作業的狀態。 |
| 上載後發佈 |  | 自動發佈您上傳的資產。 |
| 任何檔案夾內若有基本資產名稱相同者 (無論副檔名為何)，將予以覆寫 |  | 如果希望上載的檔案替換具有相同名稱的現有檔案，請選擇此選項。 此選項的名稱可能不同，具體取決於 **[!UICONTROL 應用程式設定]** > **[!UICONTROL 常規設定]** > **[!UICONTROL 上載到應用程式]** > **[!UICONTROL 覆蓋影像]**。 |
| 上傳時解壓縮ZIP或Tar檔案 |  |  |
| 作業選項 |  | 按一下 **[!UICONTROL 作業選項]** 這樣你就能開啟 [!UICONTROL 上載作業選項] 對話框，然後選擇影響整個上載作業的選項。 這些選項對於所有檔案類型都相同。<br>您可以選擇從「應用程式一般設定」頁開始上載檔案的預設選項。 要開啟此頁，請選擇 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]**。 選擇 **[!UICONTROL 預設上載選項]** 選項 [!UICONTROL 上載作業選項] 對話框。 |
|  | 時間 | 選擇一次性或循環。 要設定循環作業，請選擇「重複」選項（每日、每週、每月或自定義），以指定FTP上載作業重複的時間。 然後根據需要指定計畫選項。 |
|  | 包括子資料夾 | 上載要上載的資料夾中的所有子資料夾。 您上載的資料夾及其子資料夾的名稱將自動輸入到 [!DNL Experience Manager Assets]。 |
|  | 裁切選項 | 要從影像的側面手動裁剪，請選擇「裁剪」菜單，然後選擇「手動」。 然後輸入要從影像的任何一側或每一側裁剪的像素數。 剪切的影像量取決於影像檔案中的ppi（像素/英吋）設定。 例如，如果影像顯示150 ppi，而您在「頂部」、「右側」、「底部」和「左側」文本框中輸入75，則從每側裁剪半英吋。<br> 要自動從影像中裁剪空白像素，請開啟「裁剪」菜單，選擇「手動」，然後在「頂部」、「右部」、「底部」和「左部」欄位中輸入像素測量值以從側面裁剪。 您也可以在「裁剪」菜單上選擇「裁切」，然後選擇以下選項：<br> **基於** <ul><li>**顏色**  — 選擇「顏色」選項。 然後選擇「角」菜單，然後選擇影像的角，該角的顏色最能代表要裁剪的白色空間顏色。</li><li>**透明度**  — 選擇「透明度」選項。<br> **容差**  — 拖動滑塊以指定0到1的公差。對於基於顏色的修剪，僅當像素與在影像角部選擇的顏色完全匹配時，才指定0來裁剪像素。 接近1的數字允許更多顏色差異。<br>對於基於透明度的修剪，請指定0以僅在像素為透明時裁剪像素。 接近1的數字允許更透明。</li></ul><br>這些裁剪選項是無損的。 |
|  | 顏色配置檔案選項 | 在建立用於傳遞的優化檔案時選擇顏色轉換：<ul><li>預設顏色保留：當影像包含顏色空間資訊時，維護源影像顏色；沒有顏色轉換。 目前幾乎所有影像都已嵌入適當的顏色配置檔案。 但是，如果CMYK源影像不包含嵌入的顏色配置檔案，這些顏色將轉換為sRGB（標準紅綠藍）顏色空間。 sRGB是建議的用於在網頁上顯示影像的顏色空間。</li><li>保留原始顏色空間：保留原始顏色，點處不進行任何顏色轉換。 對於沒有嵌入顏色配置檔案的影像，任何顏色轉換都使用在「發佈」設定中配置的預設顏色配置檔案完成。 顏色配置檔案可能與使用此選項建立的檔案中的顏色不對齊。 因此，建議您使用「預設顏色保留」選項。</li><li>自定義自>自<br> 開啟菜單，以便選擇「轉換自」和「轉換至」顏色空間。 此高級選項將覆蓋源檔案中嵌入的任何顏色資訊。 當您提交的所有影像包含不正確或缺少顏色配置檔案資料時，選擇此選項。</li></ul> |
|  | 影像編輯選項 | 可以保留影像中的剪貼蒙版，並選擇顏色配置檔案。<br> 請參閱 [在上載時設定影像編輯選項](#setting-image-editing-options-at-upload)。 |
|  | Postscript選項 | 您可以柵格化PostScript®檔案、裁剪檔案、維護透明背景、選擇解析度和選擇顏色空間。<br> 請參閱 [設定PostScript和Illustrator上載選項](#setting-postscript-and-illustrator-upload-options)。 |
|  | Photoshop選項 | 您可以從Adobe®Photoshop®檔案建立模板，維護圖層，指定圖層的命名方式，提取文本，並指定如何將影像定位到模板中。<br> 中不支援模板 [!DNL Experience Manager]。<br> 請參閱 [設定Photoshop上載選項](#setting-photoshop-upload-options)。 |
|  | PDF選項 | 您可以柵格化檔案、提取搜索詞和連結、自動生成eCatalog、設定解析度並選擇顏色空間。<br>中不支援eCatalog [!DNL Experience Manager]。 <br> 請參閱 [設定PDF上載選項](#setting-pdf-upload-options)。<br>**注釋**:要考慮提取的PDF的最大頁數為5000，用於新上載。 到2022年12月31日，此限制將改為100頁。 另請參閱 [Dynamic Media限制](/help/assets/limitations.md)。 |
|  | Illustrator選項 | 您可以柵格化Adobe Illustrator®檔案、維護透明背景、選擇解析度和選擇顏色空間。<br> 請參閱 [設定PostScript和Illustrator上載選項](#setting-postscript-and-illustrator-upload-options)。 |
|  | EVideo選項 | 通過選擇「視頻預設」，可以對視頻檔案進行代碼轉換。<br> 請參閱 [設定eVideo上載選項](#setting-evideo-upload-options)。 |
|  | 批次集預設集 | 要從上載的檔案建立「影像集」或「旋轉集」，請按一下要使用的預設的「活動」列。 可以選擇多個預設。 您可以在Dynamic Media Classic的「應用程式設定/批集預設」頁中建立預設。<br> 請參閱 [將批集預設配置為自動生成影像集和旋轉集](config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) 以瞭解有關建立批集預設的詳細資訊。<br> 請參閱 [在上載時設定批集預設](#setting-batch-set-presets-at-upload)。 |

#### 在上載時設定影像編輯選項 {#setting-image-editing-options-at-upload}

上載影像檔案(包括AI、EPS和PSD檔案)時，可在 [!UICONTROL 上載作業選項] 對話框：

* 從影像邊緣裁剪空白（請參閱上表中的說明）。
* 從影像的側面手動裁剪（請參閱上表中的說明）。
* 選擇顏色配置檔案（請參閱上表中的選項說明）。
* 從剪切路徑建立蒙版。
* 使用反銳化掩碼選項銳化影像
* 挖空背景

<!--
| Option | Sub-option | Description |
|---|---|---|
| Create Mask From Clipping Path | | Create a mask for the image based on its clipping path information. This option applies to images created with image-editing applications in which a clipping path was created. |
| Unsharp Masking | | Lets you fine-tune a sharpening filter effect on the final downsampled image, controlling the intensity of the effect, the radius of the effect (as measured in pixels), and a threshold of contrast that is ignored.<br> This effect uses the same options as Photoshop’s Unsharp Mask filter. Contrary to what the name suggests, Unsharp Mask is a sharpening filter. Under Unsharp Masking, set the options you want. Setting options are described in the following: |
| | Amount | Controls the amount of contrast that is applied to edge pixels.<br> Think of it as the intensity of the effect. The main difference between the amount values of Unsharp Mask in Dynamic Media and the amount values in Adobe Photoshop, is that Photoshop has an amount range of 1% to 500%. Whereas, in Dynamic Media, the value range is 0.0 to 5.0. A value of 5.0 is the rough equivalent of 500% in Photoshop; a value of 0.9 is the equivalent of 90%, and so on. |
| | Radius | Controls the radius of the effect. The value range is 0-250.<br> The effect is run on all pixels in an image and radiates out from all pixels in all directions. The radius is measured in pixels. For example, to get a similar sharpening effect for a 2000 x 2000 pixel image and 500 x 500 pixel image, you would set a radius of two pixels on the 2000 x 2000 pixel image and a radius value of one pixel on the 500 x 500 pixel image. A larger value is used for an image that has more pixels. |
| | Threshold | Threshold is a range of contrast that is ignored when the Unsharp Mask filter is applied. It is important so that no "noise" is introduced to an image when this filter is used. The value range is 0-255, which is the number of brightness steps in a grayscale image. 0=black, 128=50% gray and 255=white.<br> For example, a threshold value of 12 ignores slight variations is skin tone brightness to avoid adding noise, but still add edge contrast to areas such as where eyelashes meet skin.<br> For example, if you have a photo of someone’s face, the Unsharp Mask affects the parts of the image, such as where eyelashes and skin meet to create an obvious area of contrast, and the smooth skin itself. Even the smoothest skin exhibits subtle changes in brightness values. If you do not use a threshold value, the filter accentuates these subtle changes in skin pixels. In turn, a noisy and undesirable effect is created while contrast on the eyelashes is increased, enhancing sharpness.<br> To avoid this issue, a threshold value is introduced that tells the filter to ignore pixels that do not change contrast dramatically, like smooth skin.<br> In the zipper graphic shown earlier, notice the texture next to the zippers. Image noise is exhibited because the threshold values were too low to suppress the noise. |
| | Monochrome | Select to unsharp-mask image brightness (intensity).<br> Deselect to unsharp-mask each color component separately. |
| Knockout Background | | Automatically removes the background of an image when you upload it. This technique is useful to draw attention to a particular object and make it stand out from a busy background. Select to enable or “turn on” the Knockout Background feature and the following sub-options: |
| | Corner | Required.<br> The corner of the image that is used to define the background color to knockout.<br> You can choose from **Upper Left**, **Bottom Left**, **Upper Right**, or **Bottom Right**. |
| | Fill Method | Required.<br> Controls pixel transparency from the Corner location that you set.<br> You can choose from the following fill methods: <ul><li>**Flood Fill** - turns all pixels transparent that match the Corner that you have specified and are connected to it.</li><li>**Match Pixel** - turns all matching pixels transparent, regardless of their location on the image.</li></ul> |
| | Tolerance | Optional.<br> Controls the allowable amount of variation in pixel color matching based on the Corner location that you set.<br> Use a value of 0.0 to match pixel colors exactly or, use a value of 1.0 to allow for the greatest variation. |
-->

#### 設定PostScript和Illustrator上載選項 {#setting-postscript-and-illustrator-upload-options}

上載PostScript(EPS)或Illustrator(AI)映像檔案時，可以採用各種格式設定它們。 您可以柵格化檔案、維護透明背景、選擇解析度和選擇顏色空間。 PostScript和Illustrator檔案的格式設定選項在 [!UICONTROL 上載作業選項] 對話框 [!UICONTROL PostScript選項] 和 [!UICONTROL Illustrator選項]。

| 選項 | 子選項 | 說明 |
|---|---|---|
| 處理 |  | 選擇 **[!UICONTROL 光柵化]** 將檔案中的向量圖形轉換為點陣圖格式。 |
| 在渲染的影像中維護透明背景 |  | 維護檔案的背景透明度。 |
| 解析度 |  | 確定解析度設定。 此設定確定檔案中每英吋顯示的像素數。 |
| 色彩空間 |  | 選擇「顏色空間」菜單，然後從以下顏色空間選項中進行選擇： |
|  | 自動檢測 | 保留檔案的顏色空間。 |
|  | 強制為RGB | 轉換為RGB顏色空間。 |
|  | 強制為CMYK | 轉換為CMYK顏色空間。 |
|  | 強制為灰度 | 轉換為灰度色空間。 |

#### 設定Photoshop上載選項 {#setting-photoshop-upload-options}

Photoshop文檔(PSD)檔案最常用於建立影像模板。 上載PSD檔案時，可以自動從檔案建立影像模板(選擇 [!UICONTROL 建立模板] 選項)。

Dynamic Media會使用檔案建立模板，從包含圖層的PSD檔案建立多個影像；它為每個圖層建立一個影像。

使用 [!UICONTROL 裁剪選項] 和 [!UICONTROL 顏色配置檔案選項]，上述，帶有Photoshop上載選項。

>[!NOTE]
>
>中不支援模板 [!DNL Experience Manager]。

| 選項 | 子選項 | 說明 |
|---|---|---|
| 維護層 |  | 將PSD中的層（如果有）拆分為單個資產。 資產層仍與PSD關聯。 可通過在「詳細資訊」視圖中開啟PSD檔案並選擇層面板來查看它們。 |
| 建立範本 |  | 從PSD檔案中的層建立模板。 |
| 提取文本 |  | 提取文本，以便用戶可以在查看器中搜索文本。 |
| 延伸圖層以符合背景大小 |  | 將撕裂影像圖層的大小擴展到背景圖層的大小。 |
| 層命名 |  | PSD檔案中的圖層將作為單獨的影像上載。 |
|  | 層名稱 | 在PSD檔案中將影像命名為其圖層名稱。 例如，原始PSD檔案中名為「價格標籤」的圖層將變成名為「價格標籤」的影像。 但是，如果PSD檔案中的圖層名稱是預設的Photoshop圖層名稱（背景、第1層、第2層等），則這些影像將以其在PSD檔案中的圖層編號命名。 它們不以預設層名稱命名。 |
|  | Photoshop和層號 | 在PSD檔案中將影像命名為其圖層編號，而忽略原始圖層名稱。 影像以Photoshop檔案名和附加的圖層號命名。 例如，名為Spring Ad.psd的檔案的第二層命名為Spring Ad_2，即使它在Photoshop具有非預設名稱。 |
|  | Photoshop和層名稱 | 將影像命名為PSD檔案後面的圖層名稱或圖層編號。 如果PSD檔案中的層名是預設的Photoshop層名，則使用層號。 例如，在名為SpringAd的PSD檔案中，名為Price Tag的層名為Spring Ad_Price Tag。 預設名稱為「層2」的層稱為「彈簧Ad_2」。 |
| 錨點 |  | 指定如何將影像定位到從PSD檔案生成的分層合成生成的模板中。 預設情況下，錨點為中心。 中心錨點允許替換影像最好地填充相同的空間，而不管替換影像的長寬比。 當引用模板並使用參數替換時，具有不同方面的影像可替換此影像，有效地佔用了相同的空間。 如果應用程式需要替換影像來填充模板中分配的空間，請更改為其他設定。 |

#### 設定PDF上載選項 {#setting-pdf-upload-options}

上載PDF檔案時，可以採用各種格式設定該檔案。 您可以裁剪其頁面、提取搜索詞、輸入每英吋像素的解析度並選擇顏色空間。 PDF檔案通常包含裁切邊距、裁切標籤、註冊標籤和其他打印機標籤。 在上載PDF檔案時，可以從頁面的側面裁剪這些標籤。

要考慮提取的PDF的最大頁數為5000，用於新上載。 到2022年12月31日，此限制將改為100頁。 另請參閱 [Dynamic Media限制](/help/assets/limitations.md)。

>[!NOTE]
>
>中不支援eCatalog [!DNL Experience Manager]。

從以下選項中選擇：

| 選項 | 子選項 | 說明 |
|---|---|---|
| 處理 | 點陣化 | （預設）拆除PDF檔案中的頁面，並將向量圖形轉換為點陣圖影像。 如果要建立eCatalog，請選擇此選項。 |
| 提取 | 搜尋字詞 | 從PDF檔案中提取單詞，以便在eCatalog Viewer中按關鍵字搜索檔案。 |
|  | 連結 | 從PDF檔案中提取連結，並將其轉換為在eCatalog Viewer中使用的影像映射。 |
| 自動從多頁生成eCatalogPDF |  | 自動從PDF檔案建立eCatalog。 eCatalog以您上載的PDF檔案命名。 (此選項僅在上載PDF檔案時柵格化時才可用。) |
| 解析度 |  | 確定解析度設定。 此設定確定PDF檔案中每英吋顯示的像素數。 預設值為150。 |
| 色彩空間 |  | 選擇「顏色空間」菜單，然後為PDF檔案選擇顏色空間。 大多數PDF檔案都有RGB和CMYK彩色影像。 RGB色空間優選用於線上觀看。 |
|  | 自動偵測 | 保留PDF檔案的顏色空間。 |
|  | 強制為 RGB | 轉換為RGB顏色空間。 |
|  | 強制為 CMYK | 轉換為CMYK顏色空間。 |
|  | 強制為灰階 | 轉換為灰度色空間。 |

#### 設定eVideo上載選項 {#setting-evideo-upload-options}

通過從各種視頻預設中進行選擇來對視頻檔案進行代碼轉換。

| 選項 | 子選項 | 說明 |
|---|---|---|
| 適應性影片 |  | 單個編碼預設，可與任意縱橫比配合工作，用於建立視頻，以交付到移動、平板和案頭。 使用此預設編碼的上載源視頻設定為固定高度。 但是，寬度會自動縮放以保留視頻的寬高比。 <br>最佳做法是使用自適應視頻編碼。 |
| 單個編碼預設 | 對編碼預設進行排序 | 選擇 **[!UICONTROL 名稱]** 或 **[!UICONTROL 大小]** 按名稱或解析度大小對「案頭」、「移動」和「平板電腦」下列出的編碼預設進行排序。 |
|  | 桌面 | 建立MP4檔案，以便向台式電腦提供流式或漸進視頻體驗。 選擇具有所需解析度大小和目標資料速率的一個或多個縱橫比。 |
|  | 行動 | 建立MP4檔案，以便在iPhone或Android™移動設備上交付。 選擇具有所需解析度大小和目標資料速率的一個或多個縱橫比。 |
|  | 平板電腦 | 建立MP4檔案，以便在iPad或Android™平板電腦設備上交付。 選擇具有所需解析度大小和目標資料速率的一個或多個縱橫比。 |

#### 在上載時設定批集預設 {#setting-batch-set-presets-at-upload}

如果要從上載的影像自動建立影像集或旋轉集，請按一下要使用的預設的「活動」列。 可以選擇多個預設。

請參閱 [將批集預設配置為自動生成影像集和旋轉集](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) 以瞭解有關建立批集預設的詳細資訊。

### 流式上傳 {#streamed-uploads}

如果您將許多資產上傳到Adobe Experience Manager，則對伺服器的I/O請求會急劇增加，這會降低上傳效率，甚至會導致某些上載任務超時。 [!DNL Experience Manager Assets] 支援流式上傳資產。 流式上載通過在將磁碟複製到儲存庫之前避免在伺服器上的臨時資料夾中儲存資產，減少了上載操作期間的磁碟I/O。 相反，資料會直接傳輸到儲存庫。 這樣，上載大型資產的時間和超時的可能性就會減少。 預設情況下，在 [!DNL Assets]。

>[!NOTE]
>
>對於JEE伺服器上運行的Servlet-api版本低於3.1的Adobe Experience Manager，禁用流上載。

### 提取包含資產的ZIP存檔 {#extractzip}

您可以像其他任何受支援的資產一樣上載ZIP存檔。 同一檔案名規則適用於ZIP檔案。 [!DNL Experience Manager] 允許您將ZIP存檔解壓到DAM位置。 如果存檔檔案不包含ZIP作為副檔名，請啟用使用內容的檔案類型檢測。

一次選擇一個ZIP存檔，按一下 **[!UICONTROL 提取存檔]**，然後選擇目標資料夾。 選擇要處理衝突的選項（如果有）。 如果ZIP檔案中的資產存在於目標資料夾中，則可以選擇以下選項之一：跳過提取、替換現有檔案、通過更名保留兩個資產或建立版本。

提取完成後， [!DNL Experience Manager] 通知您。 同時 [!DNL Experience Manager] 提取ZIP，你可以回到你的工作，而不中斷提取。

![ZIP檔案提取通知](assets/Zip-extraction-notification.png)

該功能的一些限制是：

* 如果目標上存在同名的資料夾，則ZIP檔案中的資產將提取到現有資料夾中。
* 如果取消提取，則不會刪除已提取的資產。
* 不能同時選擇兩個ZIP檔案並解壓它們。 一次只能提取一個ZIP存檔。
* 上載ZIP存檔檔案時，如果上載對話框顯示500伺服器錯誤，請在安裝後重試 [最新的Service Pack](/help/release-notes/release-notes.md)。

## 預覽資產 {#previewing-assets}

要預覽資產，請執行以下步驟。

1. 從 [!DNL Assets] 用戶介面，導航至要預覽的資產的位置。
1. 按一下所需的資源，以便開啟它。

1. 在預覽模式下，縮放選項可用於 [支援的映像類型](/help/assets/assets-formats.md#supported-raster-image-formats) （使用互動式編輯）。

   要放大資產，請按一下 `+` （或按一下資產上的放大鏡）。 要縮小，請按一下 `-`。 放大時，可以通過平移來仔細查看影像的任何區域。 重置縮放箭頭將您返回到原始視圖。 要將視圖重置為原始大小，請按一下 **[!UICONTROL 重置]** ![重置視圖](assets/do-not-localize/revert.png)。

**僅使用鍵盤鍵預覽資產**

要使用鍵盤預覽資產，請執行以下步驟：

1. 從 [!DNL Assets] 用戶介面，使用 `Tab` 和箭頭鍵。

1. 按 `Enter` 鍵，以便您可以開啟它。 可以在預覽模式中放大資產。

1. 要放大資產，請執行以下操作：
   1. 使用 `Tab` 鍵，將焦點移到放大選項。
   1. 使用 `Enter` 鍵以放大影像。

   要縮小，請使用 `Tab` 鍵，將焦點放在縮小選項上，然後按 `Enter`。

1. 使用 `Shift` + `Tab` 鍵將焦點移回影像。

1. 使用箭頭鍵在縮放影像周圍移動。

>[!MORELIKETHIS]
>
>* [預覽Dynamic Media資產](/help/assets/previewing-assets.md)。
>* [查看子組](managing-linked-subassets.md#viewing-subassets)。


## 編輯屬性和元資料 {#editing-properties}

1. 導航到要編輯其元資料的資產的位置。

1. 選擇資產，然後從工具欄中選擇 **[!UICONTROL 屬性]** 以便您查看資產的屬性。 或者，選擇 **[!UICONTROL 屬性]** 對資產卡執行快速操作。

   ![資產卡視圖的屬性快速操作](assets/properties_quickaction.png)

1. 在 [!UICONTROL 屬性] 頁，編輯各個頁籤下的元資料屬性。 例如，在 **[!UICONTROL 基本]** 頁籤。

   >[!NOTE]
   >
   >佈局 [!UICONTROL 屬性] 頁和可用的元資料屬性取決於基礎元資料架構。 瞭解如何修改佈局 [!UICONTROL 屬性] 頁面，請參閱 [元資料架構](/help/assets/metadata-schemas.md)。

1. 若要排程啟動資產的特定日期/時間，請使用「準時」欄位旁的日 **[!UICONTROL 期選擇器]** 。

   ![日期時間選取器或使用「按時」欄位中的鍵盤鍵添加資產激活的日期和時間](assets/datepicker.png)

   *圖：使用日期選取器來安排資產激活。*

1. 要在特定持續時間後停用資產，請從位於 **[!UICONTROL 關機時間]** 的子菜單。 停用日期應晚於資產的激活日期。 在 [!UICONTROL 關機時間]，資產及其格式副本也無法通過 [!DNL Assets] Web介面或通過HTTP API。

1. 在 **[!UICONTROL 標籤]** 的子菜單。 要添加自定義標籤，請在框中鍵入標籤名稱，然後選擇 `Enter`。 新標籤保存在 [!DNL Experience Manager]。 [!DNL YouTube] 需要要發佈的標籤。 請參閱 [發佈視頻給YouTube](video.md#publishing-videos-to-youtube)。

   >[!NOTE]
   >
   >要建立標籤，您需要在 `/content/cq:tags/default` 的下界。

1. 要為資產提供評級，請按一下 **[!UICONTROL 高級]** 頁籤，然後按一下適當位置的星號以指定所需的評級。

   ![資產屬性中的「高級」頁籤，以分配評級](assets/ratings.png)

   您分配給資產的評級分數顯示在 **[!UICONTROL 您的評級]**。 從對資產進行評級的用戶接收的資產的平均評級分數顯示在 **[!UICONTROL 評級]**。 此外，在下面顯示有助於平均評級得分的評級得分的分解 **[!UICONTROL 評級細分]**。 您可以根據平均評級得分搜索資產。

1. 要查看資產的使用情況統計資訊，請按一下 **[!UICONTROL 洞察力]** 頁籤。

   使用情況統計資訊包括：

   * 查看或下載資產的次數
   * 使用資產的渠道/設備
   * 最近使用資產的創造性解決方案

   有關詳細資訊，請參閱 [資產透視](/help/assets/asset-insights.md)。

1. 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。
1. 導航到 [!DNL Assets] 用戶介面。 已編輯的元資料屬性（包括標題、說明、評級等）顯示在「卡」視圖的資產卡上以及「清單」視圖中相關列下。

## 複製資產 {#copying-assets}

複製資產或資料夾時，將複製整個資產或資料夾及其內容結構。 複製的資產或資料夾在目標位置重複。 源位置的資產不會更改。

不會結轉資產特定副本所特有的幾個屬性。 有些示例包括：

* 資產ID、建立日期和時間以及版本和版本歷史記錄。 這些屬性中的某些屬性由 `jcr:uuid`。 `jcr:created`, `cq:name`。

* 建立時間和引用的路徑對於每個資產及其每個格式副本都是唯一的。

保留其他屬性和元資料資訊。 複製資產時不建立部分副本。

1. 在 [!DNL Assets] 介面，選擇一個或多個資產，然後按一下 **[!UICONTROL 複製]** 的子菜單。 或者，選擇 **[!UICONTROL 複製]** ![「資產」介面工具欄中的「複製」選項](assets/do-not-localize/copy_icon.png) 資產卡中的快速操作。

   >[!NOTE]
   >
   >如果使用 [!UICONTROL 複製] 快速操作，一次只能複製一個資產。

1. 定位至要複製資產的位置。

   >[!NOTE]
   >
   >如果複製同一地點的資產， [!DNL Experience Manager] 自動生成名稱的變體。 例如，如果複製標題為 `Square`。 [!DNL Experience Manager] 自動為其副本生成標題 `Square1`。

1. 按一下 **[!UICONTROL 貼上]** ![「資產」工具欄中的「貼上」選項](assets/do-not-localize/paste.png) 的子菜單。 然後，資產被複製到此位置。

   >[!NOTE]
   >
   >的 **[!UICONTROL 貼上]** 選項。

## 移動和更名資產 {#moving-or-renaming-assets}

將資產（或資料夾）移到另一個位置時，與複製資產時不會複製資產（或資料夾）。 資產（或資料夾）被放置在目標位置，並從源位置刪除。 也可以在將資產移動到新位置時更名該資產。
如果要將已發佈的資產移到其他位置，則您可以根據需要重新發佈該資產。 預設情況下，已發佈資產的移動操作會自動取消發佈該資產。 如果作者選擇 [!UICONTROL 重新發佈] 選項。

![移動已發佈的資產時，可以重新發佈它](assets/republish-on-move.png)

移動資產或資料夾：

1. 定位至要移動的資產的位置。

1. 選擇資產，然後按一下 **[!UICONTROL 移動]** 的子菜單。
   ![「資產」工具欄中的「移動」選項](assets/do-not-localize/move.png)

1. 在 [!UICONTROL 移動資產] 嚮導，執行下列操作之一：

   * 指定移動資產後的資產名稱。 然後按一下 **[!UICONTROL 下一個]** 繼續。

   * 按一下 **[!UICONTROL 取消]** 來停止進程。
   >[!NOTE]
   >
   >* 如果在新位置沒有具有該名稱的資產，則可以為該資產指定相同的名稱。 但是，如果將資產移動到存在同名資產的位置，則應使用其他名稱。 如果使用相同的名稱，系統將自動生成名稱的變體。 例如，如果資產的名稱為Square，則系統會為其副本生成名稱Square1。
   >* 更名時，檔案名中不允許有空格。


1. 在 **[!UICONTROL 選擇目標]** 對話框，執行下列操作之一：

   * 導航到資產的新位置，然後按一下 **[!UICONTROL 下一個]** 繼續。

   * 按一下 **[!UICONTROL 後退]** 返回 **[!UICONTROL 更名]** 的上界。

1. 如果要移動的資產具有任何引用頁、資產或集合，則 **[!UICONTROL 調整參照]** 頁籤 **[!UICONTROL 選擇目標]** 頁籤。

   在 **[!UICONTROL 調整參照]** 螢幕：

   * 指定要根據新詳細資訊調整的參照，然後按一下 **[!UICONTROL 移動]** 繼續。

   * 從 **[!UICONTROL 調整]** 列，選擇/取消選擇對資產的引用。
   * 按一下 **[!UICONTROL 後退]** 返回 **[!UICONTROL 選擇目標]** 的上界。

   * 按一下 **[!UICONTROL 取消]** 來停止移動操作。

   如果不更新引用，則它們會繼續指向資產的上一路徑。 如果調整參照，則參照將更新為新資產路徑。

### 使用拖動操作移動資產 {#move-using-drag}

通過將資產（或資料夾）拖動到目標位置，而不是使用 [!UICONTROL 移動] 的子菜單。 但是，此操作只能在清單視圖中執行。

通過拖動來移動資產不會開啟 [!UICONTROL 移動資產] 嚮導，因此您在移動時無法獲得更名資產的選項。 此外，已發佈的資產在移動時通過拖動重新發佈，而不需要獲得用戶的重新發佈批准。

![通過拖動資產將資產移入同級資料夾](assets/move-by-drag.gif)

## 管理格式副本 {#managing-renditions}

1. 您可以添加或刪除資產的格式副本，但原始格式副本除外。 導航到要為其添加或刪除格式副本的資產的位置。

1. 按一下資產，開啟其頁面。
1. 在Experience Manager介面中，選擇 **[!UICONTROL 格式副本]** 清單中。
1. 在 **[!UICONTROL 格式副本]** 面板，查看為資產生成的格式副本清單。

   ![「資產詳細資訊」頁面上的格式副本面板](assets/renditions_panel.png)

   >[!NOTE]
   >
   >預設情況下， [!DNL Assets] 不在預覽模式下顯示資產的原始格式副本。 如果您是管理員，則可以使用疊加來配置 [!DNL Assets] 在預覽模式下顯示原始格式副本。

1. 選擇要查看或刪除格式副本的格式副本。

   **刪除格式副本**

   從 **[!UICONTROL 格式副本]** ，然後按一下 **[!UICONTROL 刪除格式副本]** ![刪除格式副本的選項](assets/do-not-localize/deleteoutline.png) 的子菜單。 資產處理完成後，無法批量刪除格式副本。 對於單個資產，您可以從用戶介面手動刪除格式副本。 對於多個資產，您可以自定義Experience Manager以刪除特定格式副本或刪除資產並重新上載已刪除的資產。

   **上載新格式副本**

   定位至資產的資產詳細資訊頁，然後按一下 **[!UICONTROL 添加格式副本]** ![添加格式副本選項以上載新格式副本](assets/do-not-localize/add.png) 的子菜單。

   >[!NOTE]
   >
   >如果您從「轉譯」面板選取轉譯 **** ，工具列會變更上下文，並僅顯示與轉譯相關的動作。選項，如 [!UICONTROL 上載格式副本] 頁籤 若要在工具列中檢視這些選項，請導覽至資產的詳細資訊頁面。

   您可以配置要顯示在影像或視頻資產詳細資訊頁面中的格式副本的尺寸。 根據您指定的尺寸， [!DNL Assets] 顯示具有精確尺寸或最接近尺寸的格式副本。

   若要在資產詳細資料層級設定影像的轉譯尺寸，請覆蓋節 `renditionpicker` 點(`libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/renditionpicker`)並設定width屬性的值。配置屬性 **[!UICONTROL 大小（長）(KB)]** 替換寬度，以便您可以根據影像大小在資產詳細資訊頁面上自定義格式副本。 對於基於大小的定製，如果匹配的 `preferOriginal` 格式副本的大小大於原始格式副本的大小，則屬性會為原始格式副本指定首選項。

   同樣，可以通過疊加來定制「注釋」頁面影像 `libs/dam/gui/content/assets/annotate/jcr:content/body/content/content/items/content/renditionpicker`。

   ![在CRXDE中覆蓋RenditionPicker節點以自定義「注釋」頁影像](assets/renditionpicker-node.png)

   要為視頻資產配置格式副本維，請導航到 `videopicker` CRX儲存庫中的節點 `/libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/videopicker`，覆蓋節點，然後編輯相應的屬性。

   >[!NOTE]
   >
   >只有HTML5相容視頻格式的瀏覽器才支援視頻批注。 此外，根據瀏覽器的不同，支援不同的視頻格式。 但是，MXF視頻格式尚不支援視頻批注。

有關生成和查看子集的詳細資訊，請參見 [管理子集](managing-linked-subassets.md#generate-subassets)。

## 刪除資產 {#deleting-assets}

要刪除資產，用戶需要在 `dam/asset`。 如果您僅具有修改權限，則只能編輯資產元資料並向資產添加註釋。 但是，不能刪除資產或其元資料。

要解析或刪除來自其他頁面的傳入引用，請在刪除資產之前更新相關引用。 要禁止用戶刪除引用的資產和保留斷開的連結，請使用覆蓋禁用強制刪除選項。

要刪除資產或包含資產的資料夾，請執行以下操作：

1. 導航到資產或要刪除的資料夾的位置。

1. 選擇資產或資料夾，然後按一下 **[!UICONTROL 刪除]** ![刪除選項](assets/do-not-localize/deleteoutline.png) 的子菜單。

   確認刪除後：

   * 如果資產沒有參考，則資產將被刪除。

   * 如果資產有引用，則會出現一條錯誤消息通知您 **引用一個或多個資產**。 您可以選取&#x200B;**[!UICONTROL 強制刪除]**&#x200B;或&#x200B;**[!UICONTROL 取消]**。
   >[!NOTE]
   >
   >* 要解析或刪除來自其他頁面的傳入引用，請在刪除資產之前更新相關引用。 另外，使用覆蓋禁用強制刪除選項，以禁止用戶刪除引用的資產和保留斷開的連結。
   >* 可以刪除 *資料夾* 包含已簽出資產檔案。 在刪除資料夾之前，請確保用戶未簽出任何數字資產。


>[!NOTE]
>
>如果使用上述方法從用戶介面中刪除資料夾，則還會刪除關聯的用戶組。
>
>但是，現有的冗餘、未使用和自動生成的用戶組可以使用 `clean` JMX中的方法(`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`)。

## 下載資產 {#downloading-assets}

請參閱 [從Experience Manager下載資產](/help/assets/download-assets-from-aem.md)。

## 發佈或取消發佈資產 {#publish-assets}

在上載、處理或編輯您的資產後 [!DNL Experience Manager] 作者，將資產發佈到發佈伺服器。 發佈使資產公開可用。 取消發佈操作已從發佈伺服器中刪除資產，但未從創作伺服器中刪除資產。

有關特定於 [!DNL Dynamic Media]，請參閱 [發佈 [!DNL Dynamic Media] 資產](/help/assets/publishing-dynamicmedia-assets.md)。

1. 導航到要發佈或要從發佈環境中刪除的資產或資產資料夾的位置（取消發佈）。

1. 選擇要取消發佈的資產或資料夾，然後按一下 **[!UICONTROL 管理發布]** ![管理發布選項](assets/do-not-localize/globe-publication.png) 的子菜單。 或者，要快速發佈，請選擇 **[!UICONTROL 快速發佈]** 的子菜單。 如果要發佈的資料夾包含空資料夾，則不會發佈空資料夾。

1. 選擇 **[!UICONTROL 發佈]** 或 **[!UICONTROL 取消發佈]** 按鈕。

   ![取消發佈操作](assets/unpublish_action.png)
   *圖：發佈和取消發佈選項以及計畫選項。*

1. 選擇 **[!UICONTROL 現在]** 立即對資產採取行動或選擇 **[!UICONTROL 稍後]** 以安排操作。 如果選擇 **[!UICONTROL 稍後]** 的雙曲餘切值。 按一下&#x200B;**[!UICONTROL 下一步]**。

1. 發佈時，如果資產引用了其他資產，則其引用將在嚮導中列出。 只顯示自上次發佈後未發佈或修改的那些引用。 選擇要發佈的引用。

1. 取消發佈時，如果資產引用了其他資產，請選擇要取消發佈的引用。 按一下 **[!UICONTROL 取消發佈]**。 在確認對話框中，按一下 **[!UICONTROL 取消]** 停止操作或按一下 **[!UICONTROL 取消發佈]** 確認在指定日期將取消發佈資產。

瞭解與發佈或取消發佈資產或資料夾相關的以下限制和提示：

* 選擇 [!UICONTROL 管理發布] 僅對具有複製權限的用戶帳戶可用。
* 取消發佈複雜資產時，僅取消發佈該資產。 避免取消發佈引用，因為其他發佈的資產可能會引用這些引用。
* 未發佈空資料夾。
* 如果發佈正在處理的資產，則只發佈原始內容。 缺少格式副本。 等待處理完成，然後在處理完成後發佈或重新發佈資產。

## 已關閉的使用者群組 {#closed-user-group}

關閉的用戶組(CUG)用於限制對發佈自的特定資產資料夾的訪問權限 [!DNL Experience Manager]。 如果為資料夾建立CUG，則對資料夾（包括資料夾資產和子資料夾）的訪問將僅限於分配的成員或組。 要訪問資料夾，他們必須使用其安全憑據登錄。

CUG是限制訪問您資產的額外方法。 您還可以為資料夾配置登錄頁。

1. 從 [!DNL Assets] ，然後按一下 [!UICONTROL 屬性] 的子菜單。
1. 從 **[!UICONTROL 權限]** 頁籤，在 **[!UICONTROL 已關閉用戶組]**。

   ![在關閉的用戶組中添加用戶](assets/add_user.png)

1. 要在用戶訪問資料夾時顯示登錄螢幕，請選擇 **[!UICONTROL 啟用]** 的雙曲餘切值。 然後，選擇登錄頁的路徑 [!DNL Experience Manager]，並保存更改。

   ![啟用並選擇在用戶訪問資料夾時顯示的登錄頁](assets/login_page.png)

   >[!NOTE]
   >
   >如果未指定登錄頁的路徑， [!DNL Experience Manager] 顯示發佈實例中的預設登錄頁。

1. 發佈資料夾，然後嘗試從發佈實例訪問該資料夾。 將顯示登錄螢幕。
1. 如果您是CUG成員，請輸入您的安全憑據。 資料夾顯示在 [!DNL Experience Manager] 驗證你的身份。

## 搜尋資產 {#assetsearch}

搜索資產是數字資產管理系統使用的核心。 此功能對於創意、業務用戶和營銷人員對資產的穩健管理或DAM管理員的管理非常重要。

有關簡單、高級和自定義搜索以發現和使用最合適的資產，請參見 [在Experience Manager中搜索資產](search-assets.md)。

## 快速操作 {#quick-actions}

一次只有一個資產的快速動作圖示可用。根據您的設備，執行以下操作以顯示快速操作表徵圖：

* 觸摸設備：摸摸摸。 例如，在iPad上，您可以點擊並保留一個資產，以便顯示快速操作。
* 非接觸設備：懸停指針。 例如，在案頭設備上，如果將指針懸停在資產縮略圖上，則會顯示快速操作欄。

### 導航並選擇資產 {#navigating-and-selecting-assets}

您可以使用以下任何可用視圖（卡、列和清單）查看、瀏覽和選擇資產： **[!UICONTROL 選擇]** 的雙曲餘切值。

在清單視圖和列視圖中， **[!UICONTROL 選擇]** 選項。

在卡視圖中， **[!UICONTROL 選擇]** 選項。

瀏覽資料夾或集合時 [!DNL Assets] 在瀏覽器中的用戶介面中，您可以使用 [!UICONTROL 全選] 的上界。 最初，只有100個資產在卡視圖中載入，200個資產在清單視圖中載入。 在滾動搜索結果頁面時，將在視圖中載入更多資產。 的 [!UICONTROL 全選] 選項只選擇已載入的資產。

有關詳細資訊，請參見 [查看和選擇資源](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)。

## 編輯影像 {#editing-images}

中的編輯工具 [!DNL Assets] 介面，您可以對影像資產執行小型編輯作業。 您可以裁剪、旋轉、翻轉和對影像執行其他編輯作業。 您還可以將影像映射添加到資產中。

>[!NOTE]
>
>對於某些元件，「全屏」模式有其他可用選項。

1. 執行下列操作之一以在編輯模式下開啟資產：

   * 選擇資產，然後按一下 **[!UICONTROL 編輯]** 的子菜單。
   * 按一下 **[!UICONTROL 編輯]** 的子菜單。
   * 按一下 **[!UICONTROL 編輯]** 的子菜單。 ![工具欄中的編輯選項](assets/do-not-localize/edit_icon.png)。

1. 要裁剪影像，請按一下 **[!UICONTROL 裁剪]** ![裁剪影像的選項](assets/do-not-localize/crop.png)。

1. 從清單中選取所需的選項。裁切區域會根據您選擇的選項出現在影像上。「自 **由手形** 」選項可讓您裁切影像，而不受任何外觀比例限制。

1. 選擇要裁切的區域，並在影像上調整其大小或重定位。

1. 使用 **[!UICONTROL 撤消]** ![撤消工具欄選項](assets/do-not-localize/undo.png) 和 **[!UICONTROL 重做]** ![重做工具欄選項](assets/do-not-localize/redo.png) 選項，分別恢復為未裁切的影像或保留已裁切的影像。
1. 按一下相應的 **[!UICONTROL 旋轉]** 按鈕，將選定控制項在Tab鍵次序中下移一個位置。

   ![順時針和逆時針旋轉選項](assets/do-not-localize/rotate-options.png)

1. 按一下相應的 **[!UICONTROL 翻轉]** 選項 ![反射水準選項](assets/do-not-localize/flip-horizontal.png) 垂直 ![反射垂直選項](assets/do-not-localize/flip-vertical.png)。

1. 要完成影像編輯，請按一下 **[!UICONTROL 完成]** ![完成選項](assets/do-not-localize/check-ok-done-icon.png)。 按一下 **完成** 也會啟動格式副本的再生。

>[!NOTE]
>
>BMP、GIF、PNG和JPEG檔案格式支援影像編輯。

也可以使用影像編輯器添加影像映射。 有關詳細資訊，請參閱 [添加影像映射](/help/assets/image-maps.md)。

>[!NOTE]
>
>要編輯TXT檔案，請設定 **第CQ天連結外部化程式** 從Configuration Manager中。

## 時間軸 {#timeline}

時間軸允許您查看選定項的各種事件，如資產的活動工作流、注釋/注釋、活動日誌和版本。

![對資產的時間表條目排序](assets/sort_timeline.gif)

*圖：對資產的時間線條目排序。*

>[!NOTE]
>
>在 [集合控制台](/help/assets/manage-collections.md#navigating-the-collections-console)，也請參見Wiki頁。 **[!UICONTROL 全部顯示]** 清單提供了僅查看注釋和工作流的選項。 此外，時間線僅顯示在控制台中列出的頂級集合。 如果在任何集合內部導航，則不顯示它。

>[!NOTE]
>
>時間軸包含若干 [特定於內容片段的選項](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)。

## 注釋資產 {#annotating}

注釋是添加到影像或視頻中的注釋或解釋性注釋。 注釋使營銷人員能夠協作並保留有關資產的反饋。

只有相容HTML5的視頻格式的瀏覽器才支援視頻注釋。 視頻格式 [!DNL Assets] 支援取決於瀏覽器。 但是，MXF視頻格式尚不支援視頻批注。

>[!NOTE]
>
>對於內容片段， [注釋在片段編輯器中建立](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)。

1. 導航到要添加註釋的資產的位置。
1. 按一下 **[!UICONTROL 注釋]** 選項：

   * [快速操作](/help/assets/manage-assets.md#quick-actions)
   * 在選擇資產或導航到資產頁面後從工具欄中。

1. 在時間軸底部的 **[!UICONTROL 「注釋]** 」方塊中新增注釋。或者，在影像上標籤一個區域，並在「添加註釋」( **[!UICONTROL Add Annotation]** )對話框中添加註釋。

1. 要通知用戶注釋，請指定用戶的電子郵件地址並添加註釋。 例如，要通知Aaron MacDonald有關批注，請輸入@aa。 所有匹配用戶的提示都顯示在清單中。 從清單中選擇Aaron的電子郵件地址，以便您可以用注釋標籤該人。 同樣，可以在注釋內的任何位置或注釋之前或之後為更多用戶添加標籤。

   ![指定用戶的電子郵件地址並添加註釋以通知用戶](assets/annotate-gif.gif)

   >[!NOTE]
   >
   >對於非管理員用戶，僅當用戶具有以下位置的讀取權限時，才會顯示建議 `/home` 路徑。

1. 添加註釋後，按一下 **[!UICONTROL 添加]** 來拯救它。 注釋的通知將發送給Aaron。

   >[!NOTE]
   >
   >在保存多個注釋之前，可以添加它們。

1. 按一下 **[!UICONTROL 關閉]** 的子菜單。
1. 要查看通知，請登錄至 [!DNL Assets] 使用Aaron MacDonald的憑據，然後按一下 **[!UICONTROL 通知]** 的子菜單。

   >[!NOTE]
   >
   >注釋也可以添加到視頻資產中。 在注釋視頻時，播放器會暫停以允許您在框架上進行注釋。 有關詳細資訊，請參閱 [管理視頻資產](/help/assets/managing-video-assets.md)。 視頻批注尚不支援MXF視頻格式。

1. 要選擇不同的顏色以便能夠區分用戶，請按一下「配置檔案」選項，然後按一下 **[!UICONTROL 我的首選項]**。

   ![選擇用戶配置檔案選項，然後選擇「我的首選項」以開啟用戶首選項](assets/User-profile-preferences.png)

   在 **[!UICONTROL 注釋顏色]** 框，然後按一下 **[!UICONTROL 接受]**。

   ![在「用戶首選項」中選擇注釋顏色以設定「用戶個人」顏色](assets/Annotation-color.png)

>[!NOTE]
>
>也可向集合添加註釋。 但是，如果集合包含子集合，則只能向父集合添加註釋/注釋。 「注釋」(Annotate)選項不可用於子集合。

### 查看保存的注釋 {#viewing-saved-annotations}

一次只能查看一個批注。

>[!NOTE]
>
>如果要選擇多個注釋，則最新注釋在用戶介面上可見。
>
>只支援將注釋的資產打印為PDF。

**要查看資產的已保存注釋，請執行以下操作：**

1. 轉至資產的位置並開啟資產頁。

1. 在Experience Manager介面中，選擇 **[!UICONTROL 時間軸]**。
1. 從時間軸 **[!UICONTROL 的「顯示全部]** 」清單中，選取「注 **[!UICONTROL 釋]** 」以根據註解來篩選結果。

   按一下 **[!UICONTROL 時間軸]** 的子菜單。

   ![查看影像注釋的時間軸面板](assets/timeline-view-annotations.png)

   按一下 **[!UICONTROL 刪除]**，刪除特定注釋。

### 打印注釋 {#printing-annotations}

如果資產具有批注或已經受到審閱工作流的影響，則可以將資產連同批注和審閱狀態打印為PDF檔案，以便離線審閱。

也可以選擇僅打印注釋或審閱狀態。

>[!NOTE]
>
>在將注釋的資產打印為PDF時，可以選擇多個注釋。

要打印注釋和審閱狀態，請按一下 **[!UICONTROL 打印]** 並按照嚮導中的說明進行操作。 的 **[!UICONTROL 打印]** 選項僅在資產至少分配了一個注釋或審閱狀態時才顯示。

1. 從 [!DNL Assets] 介面，開啟資產的預覽頁面。
1. 執行下列任一項作業：

   * 要打印所有注釋和審閱狀態，請跳過步驟3並直接轉到步驟4。
   * 要打印特定注釋和審閱狀態，請開啟 [時間](/help/assets/manage-assets.md#timeline) 然後轉到步驟3。

1. 要打印特定注釋，請從時間軸中選擇注釋。

   ![從時間軸中選擇注釋以打印它](assets/timeline-select-annotations.png)

   要僅打印審閱狀態，請從時間軸中選擇它。

1. 按一下 **[!UICONTROL 打印]** 的子菜單。

1. 從「打印」對話框中，選擇要在PDF上顯示注釋/審閱狀態的位置。 例如，如果希望在包含打印影像的頁面的右上角打印注釋/狀態，請使用 **左上** 的子菜單。 預設情況下，它處於選中狀態。

   您可以根據要在打印的PDF中顯示注釋/狀態的位置選擇其他設定。如果您希望註解/狀態顯示在與印刷資產不同的頁面中，請選擇「下 **[!UICONTROL 一頁」]**。

1. 按一下 **[!UICONTROL 打印]**。 根據您在步驟2中選擇的選項，產生的PDF會在指定位置顯示註解/狀態。例如，如果您選擇使用左上角設定打印注釋和審閱狀態 **** ，則生成的輸出類似於此處所示的PDF檔案。

   ![生成的PDF的注釋和審閱狀態](assets/annotation-status-pdf.png)

1. 下載 ![下載選項，用於PDF](assets/do-not-localize/download.png) 打印 ![打印PDF](assets/do-not-localize/print.png) PDF使用右上角的選項。

   >[!NOTE]
   >
   >如果資產具有子組，則可以打印所有子組及其特定頁面注釋。

   要編輯呈現的PDF檔案的外觀，例如字型顏色、大小和樣式，請開啟 **[!UICONTROL 注釋PDF配置]** 從Configuration Manager中，修改所需選項。 例如，要更改批准狀態的顯示顏色，請修改相應欄位中的顏色代碼。 有關更改批注字型顏色的資訊，請參見 [注釋](/help/assets/manage-assets.md#annotating)。

   ![在PDF文檔上打印資產注釋的配置](assets/annotation-print-pdf-config.png)

   返回到呈現的PDF檔案並刷新它。 刷新PDF反映您所做的更改。

如果資產包含外語（尤其是非拉丁語）的注釋，則必須首先在 [!DNL Experience Manager] 打印這些注釋。 配置CQ-DAM-Handler-Gibson字型管理器服務時，請提供所需語言的字型所在的路徑。

1. 從URL開啟「CQ-DAM-Handler-Gibson字型管理器服務」配置頁 `https://[aem_server]:[port]/system/console/configMgr/com.day.cq.dam.handler.gibson.fontmanager.impl.FontManagerServiceImpl`。
1. 要配置CQ-DAM-Handler-Gibson字型管理器服務，請執行以下操作之一：

   * 在「系統字型」目錄選項中，指定系統上字型目錄的完整路徑。 例如，如果您是Mac用戶，則可以將路徑指定為 */庫/字型* 的下界。 [!DNL Experience Manager] 從此目錄讀取字型。
   * 建立名為 `fonts` 內 `crx-quickstart` 的子菜單。 CQ-DAM-Handler-Gibson字型管理器服務自動獲取位置的字型 `crx-quickstart/fonts`。 可以從「Adobe伺服器字型」目錄選項中覆蓋此預設路徑。

   * 為系統中的字型建立資料夾，並將所需的字型儲存在資料夾中。 然後，在「客戶字型」目錄選項中指定該資料夾的完整路徑。

1. 從URL訪問注釋PDF配置 `https://[aem_server]:[4502]/system/console/configMgr/com.day.cq.dam.core.impl.annotation.pdf.AnnotationPdfConfig`。
1. 按如下方式使用正確的font-family集配置「注釋」PDF:

   * 包括字串 `<font_family_name_of_custom_font, sans-serif>` 的子菜單。 例如，如果要在CJK（中文、日文和韓文）中打印注釋，請包括字串 `Arial Unicode MS, Noto Sans, Noto Sans CJK JP, sans-serif` 的子菜單。 如果要用印地語打印注釋，請下載相應的字型，並將字型系列配置為Arial® Unicode MS®、Noto Sans、Noto Sans CJK JP、Noto Sans Devanagari、sans-serif。

1. 重新啟動 [!DNL Experience Manager] 部署。

下面是如何配置的示例 [!DNL Experience Manager] 要在CJK（中文、日文和韓文）中打印注釋：

1. 從以下連結下載GoogleNoto CJK字型，並將其儲存在Font Manager服務中配置的字型目錄中。

   * 全部以一個超級CJK字型顯示： [https://www.google.com/get/noto/help/cjk/](https://www.google.com/get/noto/help/cjk/)
   * Noto Sans（歐洲語言）: [https://www.google.com/get/noto/](https://www.google.com/get/noto/)
   * 所選語言的Noto字型： [https://www.google.com/get/noto/](https://www.google.com/get/noto/)

1. 通過將font-family參數設定為 `Arial Unicode MS, Noto Sans, Noto Sans CJK JP, sans-serif`。 預設情況下，此配置可用，適用於所有歐洲語言和CJK語言。
1. 如果您選擇的語言與步驟2中提到的語言不同，請在預設font-family中添加一個適當的（逗號分隔）條目。

## 建立、管理、預覽和還原資產版本 {#asset-versioning}

版本設定會建立數位資產在特定時間點的快照。版本控制有助於以後將資產還原到以前的狀態。 例如，如果要撤消對資產所做的更改，請恢復資產的未編輯版本。 在 [!DNL Experience Manager]，您可以建立版本、查看當前修訂版本、查看兩個映像版本之間的並排差異，以及將資產還原到其早期版本。

您可以在 [!DNL Experience Manager] 在以下情形中：

* 上載具有相同檔案名且位於同一位置的資產。 它可以是新資產或同一資產的修改版本。
* 在中編輯影像 [!DNL Experience Manager] 並保存更改。
* 編輯資產的元資料。
* 使用 [!DNL Experience Manager] 案頭應用程式，用於簽出現有資產、編輯它，以及 [上載您的更改](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#edit-assets-upload-updated-assets)。

您還可以通過工作流啟用自動版本控制。 為資產建立版本時，元資料和格式副本會隨版本一起保存。 格式副本是相同影像的替代選項，例如，上載的JPEG檔案的PNG格式副本。

1. 導航到要為其建立版本的資產的位置，然後按一下以開啟其預覽。 從頁面左上角開啟菜單，然後選擇 **[!UICONTROL 時間軸]**。

   ![從左側導航菜單中，選擇時間軸選項](assets/timeline.png)

   *圖：從頁面左上角區域開啟菜單並選擇 [!UICONTROL 時間軸] 的雙曲餘切值。*

1. 要建立資產版本，請執行以下操作：

   * 按一下 **[!UICONTROL 操作]** 在底部。
   * 按一下 **[!UICONTROL 另存為版本]** 這樣您就可以為資產建立版本。 （可選）添加標籤和注釋。
   * 按一下 **[!UICONTROL 建立]** 的子菜單。

      ![從邊欄建立資產版本](assets/create-new-version-from-timeline.png)

      *圖：從 [!UICONTROL 時間軸] 左側欄。*

1. 要查看資產版本，請執行以下操作：

   * 按一下 **[!UICONTROL 全部顯示]** 在 [!UICONTROL 時間軸]。
   * 按一下 **[!UICONTROL 版本]**。 為資產建立的所有版本都列在左側提要欄中。

   * 選擇資產的特定版本，然後按一下 **[!UICONTROL 預覽版本]**。

1. 要還原為資產的較舊版本，請執行以下操作。 恢復後，此版本將顯示在 [!DNL Assets] 可供使用。

   * 按一下資產的版本。 （可選）添加標籤和注釋。
   * 按一下 **[!UICONTROL 還原到此版本]**。

      ![選擇要還原到的版本](assets/select_version.png)

      *圖：選擇一個版本並恢復到它。 它成為當前版本，然後可供DAM用戶使用。*

1. 要比較映像的兩個版本，請執行以下步驟：
   * 按一下要與當前版本進行比較的版本。
   * 將滑塊向左拖動，將此版本疊加到當前版本上並進行比較。

   ![使用滑塊將資產的選定版本與當前版本進行比較](assets/version-slider.gif)

   *圖：使用滑塊可輕鬆比較資產的選定版本與當前版本。*

### 啟動資產的工作流 {#starting-a-workflow-on-an-asset}

要應用工作流來處理資產，請參閱 [啟動資產工作流](/help/assets/assets-workflow.md#apply-a-workflow-to-an-asset)。

## 集合 {#collections}

集合是一組已訂購的資產。 使用集合在用戶之間共用相關資產或將類似資產聚集在一起，以便於發現。

* 集合可以包括來自不同位置的資產，因為它們只包含對這些資產的引用。 每個集合都維護資產的參照完整性。
* 您可以與具有不同權限級別的多個用戶共用集合，包括編輯、查看等。

要瞭解集合管理的詳細資訊，請參閱 [管理集合](/help/assets/manage-collections.md)。

## 在案頭應用或Adobe資產連結中查看資產時隱藏過期資產 {#hide-expired-assets-via-acp-api}

[!DNL Experience Manager] 案頭應用允許從Windows或Mac案頭訪問DAM儲存庫。 Adobe資產連結允許從受支援的 [!DNL Creative Cloud] 案頭應用程式。

從內部瀏覽資產時 [!DNL Experience Manager] 用戶介面，不顯示過期資產。 為防止在從案頭應用程式和資產連結瀏覽資產時查看、搜索和獲取過期資產，管理員可以執行以下配置。 該配置適用於所有用戶，而與管理員權限無關。

執行以下CURL命令。 確保讀取訪問 `/conf/global/settings/dam/acpapi/` 訪問資產的用戶。 屬於 `dam-user` 預設情況下，組具有權限。

```curl
curl -v -u admin:admin --location --request POST 'http://localhost:4502/conf/global/settings/dam/acpapi/configuration/_jcr_content' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'jcr:title=acpapiconfig' \
--data-urlencode 'hideExpiredAssets=true' \
--data-urlencode 'hideExpiredAssets@TypeHint=Boolean' \
--data-urlencode 'jcr:primaryType=nt:unstructured' \
--data-urlencode '../../jcr:primaryType=sling:Folder'
```

要瞭解更多資訊，請瞭解如何 [使用案頭應用瀏覽DAM資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) 和 [如何使用Adobe資產連結](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html)。
