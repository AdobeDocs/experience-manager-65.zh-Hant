---
title: 管理您的數位資產
description: 了解資產管理工作，例如上傳、下載、編輯、搜尋、刪除、注釋，以及版本您的數位資產。
contentOwner: AG
mini-toc-levels: 1
role: User
feature: Asset Management,Search
exl-id: 158607e6-b4e9-4a3f-b023-4023d60c97d2
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: tm+mt
source-wordcount: '9846'
ht-degree: 3%

---

# 管理您的數位資產 {#manage-digital-assets}

在[!DNL Adobe Experience Manager Assets]中，您可以執行的不僅僅是儲存和管理資產。 [!DNL Experience Manager] 提供企業級資產管理功能。您可以編輯和共用資產、執行進階搜尋，以及建立數十種支援檔案格式的多種轉譯。 您也可以管理版本和數位權限、自動處理資產、管理和管理中繼資料、使用註解進行協作等。

本文主要介紹基本的資產管理任務，如建立或上傳；元資料更新；複製、移動和刪除；發佈、取消發佈和搜尋資產。 若要了解使用者介面，請參閱[開始使用資產使用者介面](/help/sites-authoring/basic-handling.md)。 若要管理內容片段，請參閱[管理內容片段](/help/assets/content-fragments/content-fragments-managing.md)資產。

## 建立資料夾 {#creating-folders}

組織資產集合時（例如所有`Nature`影像），您可以建立資料夾以將其保持在一起。 您可以使用資料夾來分類及組織資產。 [!DNL Experience Manager Assets] 不要求您組織資料夾中的資產，以提高運作效率。

>[!NOTE]
>
>* 共用至Experience Cloud時，不支援共用`sling:OrderedFolder`類型的[!DNL Assets]資料夾。 如果要共用資料夾，建立資料夾時不要選擇[!UICONTROL Ordered]。
>* [!DNL Experience Manager] 不允許使 `subassets` 用word作為資料夾的名稱。它是為包含複合資產子資產的節點保留的關鍵字。


1. 導覽至您要建立資料夾的數位資產資料夾中的位置。 在菜單中，按一下&#x200B;**[!UICONTROL Create]**。 選擇&#x200B;**[!UICONTROL 新建資料夾]**。
1. 在&#x200B;**[!UICONTROL Title]**&#x200B;欄位中，提供資料夾名稱。 依預設，DAM會使用您提供的標題作為資料夾名稱。 建立資料夾後，您可以覆寫預設值並指定其他資料夾名稱。
1. 按一下&#x200B;**[!UICONTROL 建立]**。您的資料夾會顯示在數位資產資料夾中。

不支援下列（以空格分隔的）字元清單：

* 資產檔案名稱不能包含下列任一字元：`* / : [ \\ ] | # % { } ? &`
* 資產資料夾名稱不能包含下列任一字元：`* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

請勿在資產檔案名稱的副檔名中加入特殊字元。

## 上傳資產 {#uploading-assets}

<!-- TBD the following:
Move this section into a new article. CQDOC-14874 ticket is created for this.
In this complete article, replace emphasis with UICONTROL where appropriate.
-->

您可以從本機資料夾或網路驅動器將各種類型的資產(包括影像、PDF檔案、RAW檔案等)上傳至[!DNL Experience Manager Assets]。

>[!NOTE]
>
>在Dynamic Media - Scene7模式中，預設資產上傳檔案大小為2 GB或更小。 若要設定大於2 GB且高達15 GB的資產上傳，請參閱[（選用）設定Dynamic Media - Scene7模式，以上傳大於2 GB](/help/assets/config-dms7.md#optional-config-dms7-assets-larger-than-2gb)的資產。

您可以選擇將資產上傳至資料夾，且無論資料夾是否已指派處理設定檔。

若資料夾已指派處理設定檔，設定檔名稱會顯示在卡片檢視的縮圖上。 在清單檢視中，設定檔名稱會顯示在&#x200B;**處理設定檔**&#x200B;欄中。 請參閱[處理設定檔](/help/assets/processing-profiles.md)。

上傳資產之前，請確定資產為[format](/help/assets/assets-formats.md)，且[!DNL Experience Manager Assets]支援。

1. 在[!DNL Assets]使用者介面中，導覽至您要新增數位資產的位置。
1. 若要上傳資產，請執行下列其中一項操作：

   * 在工具列上，按一下&#x200B;**[!UICONTROL Create]**。 然後，在菜單上，按一下&#x200B;**[!UICONTROL 檔案]**。 您可以視需要重新命名顯示對話方塊中的檔案。
   * 在支援HTML5的瀏覽器中，直接將資產拖曳至[!DNL Assets]使用者介面上。 不會顯示要更名檔案的對話框。

   ![建立上傳資產的選項](assets/create-options.png)

   若要選取多個檔案，請選取`Ctrl`或`Command`索引鍵，然後在檔案選取器對話方塊中選取資產。 使用iPad時，一次只能選取一個檔案。

   您可以暫停上傳大型資產（大於500 MB），稍後從同一頁繼續。 按一下上傳開始時顯示的進度列旁的&#x200B;**[!UICONTROL 暫停]**。

   ![上傳資產進度列](assets/upload-progress-bar.png)

資產視為大型資產的大小可設定。 例如，您可以將系統設為將大於1000 MB（而非500 MB）的資產視為大型資產。 在此情況下，上傳大於1000 MB的資產時，進度列上會出現&#x200B;**[!UICONTROL Pause]**。

如果上傳的檔案大於1000 MB且檔案小於1000 MB，則[!UICONTROL Pause]選項不會顯示。 不過，如果取消小於1000-MB的檔案上傳，則會顯示&#x200B;**[!UICONTROL Pause]**&#x200B;選項。

要修改大小限制，請配置CRX儲存庫中`fileupload`節點的`chunkUploadMinFileSize`屬性。

按一下&#x200B;**[!UICONTROL Pause]**&#x200B;時，它會切換至&#x200B;**[!UICONTROL Play]**&#x200B;選項。 若要繼續上傳，請按一下&#x200B;**[!UICONTROL Play]**。

若要取消持續上傳，請按一下進度列旁的關閉(`X`)。 取消上傳操作時，[!DNL Assets]會刪除資產的部分上傳部分。

能夠繼續上傳在低頻寬情況和網路故障中特別有用，因為上傳大型資產需要很長時間。 您可以暫停上傳操作，並在情況改善時稍後繼續。 繼續時，上傳會從您暫停的點開始。

在上傳作業期間，[!DNL Experience Manager]會將要上傳的資產部分儲存為CRX存放庫中的資料區塊。 When the upload completes, [!DNL Experience Manager] consolidates these chunks into a single block of data in the repository.

要配置未完成的區塊上載作業的清除任務，請轉到`https://[aem_server]:[port]/system/console/configMgr/org.apache.sling.servlets.post.impl.helper.ChunkCleanUpTask`。

>[!CAUTION]
>
>預設值為500 MB且區塊大小為50 MB時，就會觸發區塊上傳。 如果您編輯[Apache Jackrabbit Oak TokenConfiguration](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16464.html)，並將`timeout configuration`設為少於資產上傳所需的時間，則會在資產上傳期間發生工作階段逾時情況。 因此，請變更`chunkUploadMinFileSize`和`chunksize`，讓每個區塊要求都會重新整理工作階段。
>
>在憑證過期逾時、延遲、頻寬和預期的同時上傳的情況下，最高值可讓您確保已挑選下列項目：
>
>* 確保在上載過程中為可能導致憑據過期的檔案啟用區塊上載。
>
>* 確保每個區塊在憑據過期之前完成。


如果您上傳的資產名稱與資產相同，且在上傳資產的位置已可用，則會顯示警告對話方塊。

您可以選取重新命名已上傳的新資產，以取代現有資產、建立其他版本，或保留兩者。 If you replace an existing asset, the metadata for the asset and any prior modifications (for example annotate or crop) you made to the existing asset are deleted. 如果您選擇保留這兩個資產，新資產會重新命名，名稱后面會附加數字`1`。

![用於解決資產名稱衝突的名稱衝突對話框](assets/resolve-naming-conflict.png)

>[!NOTE]
>
>在[!UICONTROL 名稱衝突]對話方塊中選取&#x200B;**[!UICONTROL 取代]**&#x200B;時，會為新資產重新產生資產ID。 此ID與先前資產的ID不同。
>
>如果啟用「資產前瞻分析」以追蹤[!DNL Adobe Analytics]的曝光次數或點按次數，重新產生的資產ID會讓[!DNL Analytics]上為資產擷取的資料失效。

如果您上傳的資產存在於[!DNL Assets]中， **[!UICONTROL 偵測到的重複項目]**&#x200B;對話方塊會警告您嘗試上傳重複的資產。 只有當現有資產二進位的`SHA 1`檢查加總值符合所上傳資產的檢查加總值時，才會顯示對話方塊。 在這種情況下，資產名稱並不重要。

>[!NOTE]
>
>只有在啟用重複檢測功能時，才會顯示[!UICONTROL 重複檢測]對話框。 要啟用重複檢測功能，請參閱[啟用重複檢測](/help/assets/duplicate-detection.md)。

![偵測到重複資產對話方塊](assets/duplicate-asset-detected.png)

若要在[!DNL Assets]中保留重複資產，請按一下&#x200B;**[!UICONTROL Keep]**。 若要刪除您上傳的重複資產，請按一下「**[!UICONTROL 刪除]**」。

[!DNL Experience Manager Assets] 防止上傳檔案名稱中含有禁止字元的資產。如果您嘗試上傳檔案名稱包含不允許的字元或更多字元的資產， [!DNL Assets]會顯示警告訊息並停止上傳，直到您移除這些字元或上傳了允許的名稱為止。

為了符合貴組織的特定檔案命名慣例，「[!UICONTROL 上傳資產]」對話方塊可讓您為上傳的檔案指定長名稱。

不過，不支援下列（以空格分隔的）字元清單：

* 資產檔案名稱不得包含`* / : [ \\ ] | # % { } ? &`
* 資產資料夾名稱不得包含`* / : [ \\ ] | # % { } ? \" . ^ ; + & \t`

請勿在資產檔案名稱的副檔名中加入特殊字元。

![上傳進度對話方塊會顯示成功上傳之檔案和無法上傳之檔案的狀態](assets/bulk-upload-progress.png)

此外， [!DNL Assets]使用者介面會顯示您上傳的最新資產或您先建立的資料夾。

如果您在檔案上傳之前取消上傳操作，[!DNL Assets]會停止上傳目前的檔案並重新整理內容。 不過，不會刪除已上傳的檔案。

[!DNL Assets]中的上傳進度對話框顯示成功上傳檔案的計數以及無法上傳的檔案。

### 串列上傳 {#serialuploads}

大量上傳大量資產會耗用大量I/O資源，這可能對[!DNL Assets]部署的效能造成負面影響。 尤其是，如果您的網際網路連線速度緩慢，上傳時間會因磁碟I/O尖峰而大幅增加。此外，您的網頁瀏覽器可能會對同時上傳POST的[!DNL Assets]請求數量施加其他限制。 因此，上傳作業會失敗或過早終止。 換言之，[!DNL Experience Manager Assets]在擷取一堆檔案時可能會遺漏某些檔案，或完全無法擷取任何檔案。

為了克服此情況，在批量上載操作期間，[!DNL Assets]一次內嵌一個資產（串列上載），而不是同時內嵌所有資產。

資產的串列上傳預設為啟用。 若要停用功能並允許同時上傳，請在Crx-de中覆蓋`fileupload`節點，並將`parallelUploads`屬性的值設為`true`。

### 使用FTP上傳資產 {#uploading-assets-using-ftp}

Dynamic Media可透過FTP伺服器批次上傳資產。 如果您要上傳大型資產(>1 GB)或上傳整個資料夾和子資料夾，應使用FTP。 您甚至可以設定FTP上傳，以定期執行。

>[!NOTE]
>
>在Dynamic Media - Scene7模式中，預設資產上傳檔案大小為2 GB或更小。 若要設定大於2 GB且高達15 GB的資產上傳，請參閱[（選用）設定Dynamic Media - Scene7模式，以上傳大於2 GB](/help/assets/config-dms7.md#optional-config-dms7-assets-larger-than-2gb)的資產。

>[!NOTE]
>
>若要在Dynamic Media - Scene7模式中透過FTP上傳資產，請在[!DNL Experience Manager]製作執行個體上安裝Feature Pack 18912。 請聯絡[Adobe客戶支援](https://experienceleague.adobe.com/?support-solution=General#support)以存取FP-18912並完成FTP帳戶的設定。 如需詳細資訊，請參閱[安裝功能套件18912以取得大量資產移轉](/help/assets/bulk-ingest-migrate.md)。
>
>如果您使用FTP上傳資產，則會忽略[!DNL Experience Manager]中指定的上傳設定。 系統會改用Dynamic Media Classic中定義的檔案處理規則。

**使用FTP上傳資產**

1. 使用您選擇的FTP用戶端，使用您從布建電子郵件收到的FTP使用者名稱和密碼登入FTP伺服器。 在FTP用戶端中，將檔案或資料夾上傳至FTP伺服器。

1. 開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html#system-requirements-dmc-app)，然後登入您的帳戶。

   配置時，Adobe提供了您的憑據和登錄。 如果您沒有此資訊，請聯絡Adobe客戶支援。

1. 在全局導航欄上，按一下&#x200B;**[!UICONTROL Upload]**。
1. 在「上傳」頁面的左上角附近，按一下「透過FTP ]**」標籤。**[!UICONTROL 
1. 在頁面左側，選擇要上傳檔案的FTP資料夾；在頁面的右側，選擇目標資料夾。
1. 在頁面的右下角附近，按一下「**[!UICONTROL 作業選項]**」，然後根據您所選資料夾中的資產設定您想要的選項。

   請參閱[上傳作業選項](#upload-job-options)。

   >[!NOTE]
   >
   >透過FTP上傳資產時，您在Dynamic Media Classic中設定的上傳工作選項(S7)取代[!DNL Experience Manager]中設定的資產處理參數。

1. 在「上載作業選項」對話框的右下角，按一下「保存&#x200B;****」。
1. 在「上傳」頁面的右下角，按一下「**[!UICONTROL 提交上傳]**」。

   若要檢視上傳進度，請在全域導覽列上按一下&#x200B;**[!UICONTROL 工作]**。 「作業」頁面會顯示上傳的進度。 您可以繼續在[!DNL Experience Manager]中工作，並隨時返回Dynamic Media Classic的「工作」頁面，以檢閱進行中的工作。
要取消正在進行的上載作業，請按一下「持續時間」旁的「取消」****。

#### 上傳作業選項 {#upload-job-options}

| 上傳選項 | 子選項 | 說明 |
|---|---|---|
| 工作名稱 |  | 在文本欄位中預填的預設名稱包括用戶輸入的名稱部分和日期和時間戳。 您可以使用預設名稱，或輸入您為此上傳作業建立的名稱。 <br>作業以及其他上傳和發佈作業會記錄在「作業」頁面上，您可在此檢查作業的狀態。 |
| 上傳後發佈 |  | 自動發佈您上傳的資產。 |
| 任何檔案夾內若有基本資產名稱相同者 (無論副檔名為何)，將予以覆寫 |  | 如果您希望上傳的檔案以相同名稱取代現有檔案，請選取此選項。 此選項的名稱可能不同，具體取決於&#x200B;**[!UICONTROL Application Setup]** > **[!UICONTROL General Settings]** > **[!UICONTROL Upload to Application]** > **[!UICONTROL Overwrite Images]**&#x200B;中的設定。 |
| 上傳時解壓縮Zip或Tar檔案 |  |  |
| 作業選項 |  | 按一下&#x200B;**[!UICONTROL 作業選項]** ，以開啟[!UICONTROL 上載作業選項]對話框，並選擇影響整個上載作業的選項。 所有檔案類型的這些選項都相同。<br>您可以從「應用程式一般設定」頁面開始，選擇上傳檔案的預設選項。要開啟此頁，請選擇&#x200B;**[!UICONTROL Setup]** > **[!UICONTROL Application Setup]**。 選擇&#x200B;**[!UICONTROL 預設上載選項]**&#x200B;選項以開啟[!UICONTROL 上載作業選項]對話框。 |
|  | 時間 | 選取一次性或循環。 若要設定循環作業，請選擇「重複」選項（每日、每週、每月或自訂），以指定何時要重複執行FTP上傳作業。 然後視需要指定排程選項。 |
|  | 包含子資料夾 | 上傳要上傳之資料夾內的所有子資料夾。 在[!DNL Experience Manager Assets]中自動輸入上傳的資料夾及其子資料夾的名稱。 |
|  | 裁切選項 | 要從影像的側面手動裁切，請選擇「裁切」菜單，然後選擇「手動」。 然後輸入要從影像的任何一側或每一側裁切的像素數。 影像被裁切的程度取決於影像檔案中的ppi設定（每英吋像素）。 例如，如果影像顯示150 ppi，而您在「上」、「右」、「下」和「左」文字方塊中輸入75，則會從每側裁切半英吋。<br> 要自動從影像中裁切空白像素，請開啟「裁切」菜單，選擇「手動」，然後在「頂部」、「右」、「底部」和「左側」欄位中輸入像素測量，以便從側面裁切。您也可以在「裁切」菜單上選擇「修剪」，然後選擇以下選項：<br> **根據** <ul><li>**顏色**  — 選擇顏色選項。然後選取「角」菜單，選擇影像的角，該角的顏色最能代表要裁切的空白顏色。</li><li>**透明度**  — 選擇「透明度」選項。<br> **容差**  — 拖動滑桿以指定0到1的容差。對於基於顏色的修剪，請指定0以僅在像素與您在影像的角中選定的顏色完全匹配時裁剪像素。接近1的數字會產生更多的顏色差異。<br>要根據透明度進行修剪，請指定0隻在像素為透明時裁剪像素。接近1的數字使透明度更高。</li></ul><br>這些裁切選項不具破壞性。 |
|  | 色彩描述檔選項 | 建立用於傳送的最佳化檔案時，請選擇色彩轉換：<ul><li>預設顏色保留：當影像包含顏色空間資訊時，保持源影像的顏色；沒有顏色轉換。 目前幾乎所有的影像都已內嵌適當的色彩設定檔。 但是，如果CMYK源影像不包含嵌入的顏色配置檔案，則這些顏色將轉換為sRGB（標準紅綠藍）顏色空間。 sRGB是在網頁上顯示影像的建議色域。</li><li>保留原始顏色空間：保留原始顏色，點上不進行任何顏色轉換。 對於沒有內嵌顏色描述檔的影像，任何顏色轉換都使用在「發佈」設定中設定的預設顏色描述檔來完成。 顏色配置檔案可能與使用此選項建立的檔案中的顏色不一致。 因此，建議您使用「預設顏色保留」選項。</li><li>「自定義自」>「轉換為」<br>開啟菜單，以便選擇「轉換自」和「轉換為顏色空間」。 此高級選項將覆蓋嵌入源檔案中的任何顏色資訊。 當您提交的所有影像都包含不正確或遺失的色彩設定檔資料時，請選取此選項。</li></ul> |
|  | 影像編輯選項 | 可以保留影像中的剪裁蒙版，並選擇顏色輪廓。<br> 請參 [閱在上傳時設定影像編輯的選項](#setting-image-editing-options-at-upload)。 |
|  | Postscript選項 | 您可以柵格化PostScript®檔案、裁切檔案、維護透明背景、選擇解析度，以及選擇顏色空間。<br> 請參 [閱設定PostScript和Illustrator上傳選項](#setting-postscript-and-illustrator-upload-options)。 |
|  | Photoshop選項 | 您可以從Adobe® Photoshop®檔案建立範本、維護圖層、指定圖層的命名方式、擷取文字，以及指定如何將影像錨定到範本中。<br> 不支援范 [!DNL Experience Manager]本。<br> 請參 [閱設定Photoshop上傳選項](#setting-photoshop-upload-options)。 |
|  | PDF選項 | 您可以柵格化檔案、提取搜索詞和連結、自動生成eCatalog、設定解析度，以及選擇顏色空間。<br>中不支援eCatalog  [!DNL Experience Manager]。<br> 請參閱 [設定PDF上傳選項](#setting-pdf-upload-options)。 |
|  | Illustrator選項 | 您可以柵格化Adobe Illustrator®檔案、維護透明背景、選擇解析度，以及選擇顏色空間。<br> 請參 [閱設定PostScript和Illustrator上傳選項](#setting-postscript-and-illustrator-upload-options)。 |
|  | 視訊選項 | 您可以選擇「視訊預設集」來轉換視訊檔案的程式碼。<br> 請參 [閱設定eVideo上傳選項](#setting-evideo-upload-options)。 |
|  | 批次集預設集 | 若要從上傳的檔案建立影像集或回轉集，請按一下您要使用之預設集的「作用中」欄。 您可以選取多個預設集。 在Dynamic Media Classic的「應用程式設定/批集預設集」頁面中建立預設集。<br> See [Configuring Batch Set Presets to Auto-Generate Image Sets and Spin Sets](config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) to learn more about creating batch set presets.<br> 請參閱 [在上傳時設定批次集預設集](#setting-batch-set-presets-at-upload)。 |

#### 設定上傳時影像編輯的選項 {#setting-image-editing-options-at-upload}

上傳影像檔案(包括AI、EPS和PSD檔案)時，您可以在[!UICONTROL 上傳工作選項]對話方塊中執行下列編輯動作：

* 從影像邊緣裁切空白字元（請參閱上表說明）。
* 從影像的側面手動裁切（請參閱上表中的說明）。
* 選擇顏色配置檔案（請參閱上表中的選項說明）。
* 從剪裁路徑建立遮色片。
* 使用非銳利化遮色片選項銳利化影像
* Knockout Background

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

#### Set PostScript and Illustrator upload options {#setting-postscript-and-illustrator-upload-options}

上傳PostScript(EPS)或Illustrator(AI)影像檔案時，可以以多種方式格式化它們。 您可以柵格化檔案、維護透明背景、選擇解析度和選擇顏色空間。 在[!UICONTROL PostScript選項]和[!UICONTROL Illustrator選項]下的[!UICONTROL 上傳作業選項]對話方塊中，可使用格式化PostScript和Illustrator檔案的選項。

| 選項 | 子選項 | 說明 |
|---|---|---|
| 處理 |  | 選擇&#x200B;**[!UICONTROL 柵格化]**&#x200B;以將檔案中的向量圖形轉換為點陣圖格式。 |
| 在渲染的影像中保持透明背景 |  | 保持檔案的背景透明度。 |
| 解析度 |  | 確定解析度設定。 此設定決定檔案中每英吋顯示的像素數。 |
| 色彩空間 |  | 選擇「顏色空間」菜單，然後從以下顏色空間選項中選擇： |
|  | 自動檢測 | 保留檔案的顏色空間。 |
|  | 強制為RGB | 轉換為RGB顏色空間。 |
|  | 強制為CMYK | 轉換為CMYK顏色空間。 |
|  | 強制為灰度 | 轉換為灰度顏色空間。 |

#### 設定Photoshop上傳選項 {#setting-photoshop-upload-options}

Photoshop檔案(PSD)檔案最常用於建立影像範本。 上傳PSD檔案時，可以從檔案自動建立影像範本（在「上傳」畫面上選取[!UICONTROL 建立範本]選項）。

如果您使用檔案建立範本，Dynamic Media會從含圖層的PSD檔案建立多個影像；它會為每個圖層建立一個影像。

使用上述的[!UICONTROL 裁切選項]和[!UICONTROL 顏色設定檔選項]，搭配Photoshop上傳選項。

>[!NOTE]
>
>[!DNL Experience Manager]中不支援模板。

| 選項 | 子選項 | 說明 |
|---|---|---|
| 維護圖層 |  | 將PSD中的圖層（如果有的話）分割為個別資產。 資產層仍與PSD相關聯。 您可以在「詳細資訊」視圖中開啟PSD檔案並選取圖層面板來查看它們。 |
| 建立範本 |  | 從PSD檔案中的圖層建立模板。 |
| 擷取文字 |  | 擷取文字，讓使用者能在檢視器中搜尋文字。 |
| 延伸圖層以符合背景大小 |  | 將撕開的影像層的大小擴展到背景層的大小。 |
| 圖層命名 |  | PSD檔案中的圖層會上傳為個別影像。 |
|  | 圖層名稱 | 在影像的圖層名稱后面命名PSD檔案。 例如，原始PSD檔案中名為「價格標籤」的圖層會變成名為「價格標籤」的影像。 但是，如果PSD檔案中的圖層名稱是預設的Photoshop圖層名稱（背景、第1層、第2層等），則影像的名稱將以PSD檔案中的圖層號命名。 不會以其預設圖層名稱命名。 |
|  | Photoshop和圖層編號 | 在PSD檔案中的圖層編號後命名影像，忽略原始圖層名稱。 影像的名稱為Photoshop檔案名稱及附加的圖層編號。 例如，名為Spring Ad.psd的檔案的第二層名為Spring Ad_2，即使它在Photoshop中具有非預設名稱亦然。 |
|  | Photoshop和圖層名稱 | 在PSD檔案後面命名影像，後面跟圖層名稱或圖層編號。 如果PSD檔案中的圖層名稱是預設的Photoshop圖層名稱，則使用圖層號。 例如，在名為SpringAd的PSD檔案中，名為Price Tag的層名為Spring Ad_Price Tag。 預設名為Layer 2的層稱為Spring Ad_2。 |
| 錨點 |  | 指定如何將影像錨定在從PSD檔案生成的分層合成生成的模板中。 預設情況下，錨點為中心。 中心錨點允許替換影像最好地填充相同的空間，而不管替換影像的長寬比如何。 當參考範本並使用參數替代時，具有替代此影像的不同方面的影像會有效佔據相同的空間。 如果您的應用程式需要替換影像以填充模板中已分配的空間，請更改為其他設定。 |

#### 設定PDF上傳選項 {#setting-pdf-upload-options}

上傳PDF檔案時，可以以多種方式格式化該檔案。 您可以裁切其頁面、擷取搜尋字詞、輸入每英吋像素的解析度，然後選擇顏色空間。 PDF檔案通常包含修剪邊界、裁切標籤、註冊標籤和其他打印機標籤。 上傳PDF檔案時，您可以從頁面的兩側裁切這些標籤。

>[!NOTE]
>
>[!DNL Experience Manager]中不支援eCatalog。

從下列選項中選擇：

| 選項 | 子選項 | 說明 |
|---|---|---|
| 處理 | 光柵化 | （預設）拆分PDF檔案中的頁面，並將向量圖形轉換為點陣圖影像。 如果要建立eCatalog，請選擇此選項。 |
| 提取 | 搜尋字詞 | 從PDF檔案中擷取字詞，以便在eCatalog檢視器中依關鍵字搜尋檔案。 |
|  | 連結 | 從PDF檔案中擷取連結，並將其轉換為eCatalog檢視器中使用的影像地圖。 |
| 從多個頁面自動產生eCatalogPDF |  | 從PDF檔案自動建立eCatalog。 eCatalog會以您上傳的PDF檔案命名。 (只有在上傳PDF檔案時柵格化該檔案時，才可使用此選項。) |
| 解析度 |  | 確定解析度設定。 此設定決定每英吋顯示的PDF檔案像素數。 預設為150。 |
| 色彩空間 |  | 選擇「顏色空間」菜單，然後為PDF檔案選擇顏色空間。 大多數PDF檔案都有RGB和CMYK顏色影像。 線上檢視較偏好RGB色域。 |
|  | 自動偵測 | 保留PDF檔案的色域。 |
|  | 強制為 RGB | 轉換為RGB顏色空間。 |
|  | 強制為 CMYK | 轉換為CMYK顏色空間。 |
|  | 強制為灰階 | 轉換為灰度顏色空間。 |

#### 設定eVideo上傳選項 {#setting-evideo-upload-options}

若要透過從各種視訊預設集中選擇來轉換視訊檔案。

| 選項 | 子選項 | 說明 |
|---|---|---|
| 適應性影片 |  | 單一編碼預設集可搭配任何外觀比例來建立視訊，以傳送至行動裝置、平板電腦和桌上型電腦。 使用此預設集編碼的已上傳來源影片會以固定高度設定。 不過，寬度會自動縮放以保留視訊的外觀比例。 <br>最佳實務是使用最適化視訊編碼。 |
| 單一編碼預設集 | 排序編碼預設集 | 如果您想要依名稱或解析度大小排序「案頭」、「行動裝置」和「平板電腦」下列出的編碼預設集，請選取「**[!UICONTROL 名稱]**」或「**[!UICONTROL 大小]**」。 |
|  | 桌面 | 建立MP4檔案，將串流或漸進式視訊體驗提供至桌上型電腦。 選擇一個或多個縱橫比，其中包含所需的解析度大小和目標資料速率。 |
|  | 行動 | 建立MP4檔案以在iPhone或Android™行動裝置上傳送。 選擇一個或多個縱橫比，其中包含所需的解析度大小和目標資料速率。 |
|  | 平板電腦 | 建立MP4檔案以在iPad或Android™平板電腦裝置上傳送。 選擇一個或多個縱橫比，其中包含所需的解析度大小和目標資料速率。 |

#### 在上傳時設定批次集預設集 {#setting-batch-set-presets-at-upload}

如果您想從上傳的影像自動建立影像集或回轉集，請按一下您要使用之預設集的「作用中」欄。 您可以選取多個預設集。

請參閱[配置批集預設集以自動生成影像集和回轉集](/help/assets/config-dms7.md#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets)以了解有關建立批集預設集的詳細資訊。

### 串流上傳 {#streamed-uploads}

如果您將許多資產上傳至Adobe Experience Manager，對伺服器的I/O請求會大幅增加，進而降低上傳效率，甚至可能導致部分上傳任務逾時。 [!DNL Experience Manager Assets] 支援資產的串流上傳。串流上傳會先避免將資產儲存在伺服器上的臨時資料夾中，再複製到存放庫，借此在上傳作業期間減少磁碟I/O。 資料會直接傳輸至存放庫。 如此一來，上傳大型資產的時間和逾時的可能性就會降低。 預設會在[!DNL Assets]中啟用串流上傳。

>[!NOTE]
>
>若Adobe Experience Manager在JEE伺服器上執行，且servlet-api版本低於3.1，則會停用串流上傳。

### 解壓縮包含資產的ZIP封存 {#extractzip}

您可以像上傳任何其他支援的資產一樣上傳ZIP封存檔。 相同的檔案名規則適用於ZIP檔案。 [!DNL Experience Manager] 可讓您將ZIP封存解壓縮至DAM位置。如果封存檔未包含ZIP作為副檔名，請使用內容來啟用檔案類型偵測。

一次選擇一個ZIP存檔，按一下&#x200B;**[!UICONTROL 解壓縮存檔]**，然後選擇目標資料夾。 選擇要處理衝突的選項（如果有）。 如果ZIP檔案中的資產存在於目的地資料夾中，您可以選取下列其中一個選項：略過擷取、取代現有檔案、透過重新命名來保留兩個資產，或建立版本。

提取完成後，[!DNL Experience Manager]會在通知區域中通知您。 當[!DNL Experience Manager]提取郵遞區號時，您可以繼續工作而不中斷提取。

![ZIP檔案解壓縮通知](assets/Zip-extraction-notification.png)

功能的部分限制包括：

* 如果目的地存在同名的資料夾，系統會從ZIP檔案擷取現有資料夾中的資產。
* 如果您取消提取，系統不會刪除已提取的資產。
* 您無法同時選取兩個ZIP檔案並解壓縮。 一次只能解壓縮一個ZIP封存。
* 上傳ZIP封存時，如果上傳對話方塊顯示500伺服器錯誤，請在安裝[最新Service Pack](/help/release-notes/sp-release-notes.md)後重試。

## 預覽資產 {#previewing-assets}

若要預覽資產，請依照下列步驟操作。

1. 從[!DNL Assets]使用者介面，導覽至您要預覽的資產位置。
1. 按一下所需的資產，以便開啟它。

1. 在預覽模式中，[支援的影像類型](/help/assets/assets-formats.md#supported-raster-image-formats)（具有互動式編輯）可使用縮放選項。

   若要放大資產，請按一下`+`（或按一下資產上的放大鏡）。 要縮小，請按一下`-`。 放大時，可通過平移來密切查看影像的任何區域。 重設縮放箭頭會將您帶回原始檢視。 要將視圖重置為原始大小，請按一下「**[!UICONTROL 重置]** ![重置視圖](assets/do-not-localize/revert.png)」。

**僅使用鍵盤鍵預覽資產**

若要使用鍵盤預覽資產，請依照下列步驟操作：

1. 從[!DNL Assets]使用者介面，使用`Tab`和方向鍵導覽至所需的資產。

1. 在所需資產上按`Enter`鍵，以開啟它。 您可以在預覽模式中放大資產。

1. 若要放大資產：
   1. 使用`Tab`鍵將焦點移至放大選項。
   1. 使用`Enter`鍵縮放影像。

   要縮小，請使用`Tab`鍵將焦點置於縮小選項上，然後按`Enter`鍵。

1. 使用`Shift` + `Tab`鍵將焦點移回影像上。

1. 使用方向鍵在縮放的影像周圍移動。

>[!MORELIKETHIS]
>
>* [預覽Dynamic Media Assets](/help/assets/previewing-assets.md)。
>* [檢視子資產](managing-linked-subassets.md#viewing-subassets)。


## 編輯屬性和中繼資料 {#editing-properties}

1. 導覽至您要編輯其中繼資料的資產位置。

1. 選取資產，然後從工具列中選取「**[!UICONTROL 屬性]**」，以便您檢視資產的屬性。 或者，選擇資產卡上的&#x200B;**[!UICONTROL 屬性]**&#x200B;快速操作。

   ![資產卡片檢視的屬性快速動作](assets/properties_quickaction.png)

1. 在[!UICONTROL 屬性]頁中，編輯各個標籤下的元資料屬性。 例如，在&#x200B;**[!UICONTROL Basic]**&#x200B;標籤下，編輯標題和說明。

   >[!NOTE]
   >
   >[!UICONTROL 屬性]頁的佈局和可用的元資料屬性取決於基礎元資料架構。 若要了解如何修改[!UICONTROL 屬性]頁面的版面，請參閱[中繼資料結構](/help/assets/metadata-schemas.md)。

1. 若要排程啟動資產的特定日期/時間，請使用「準時」欄位旁的日 **[!UICONTROL 期選擇器]** 。

   ![日期時間選擇器或在「準時」欄位中使用鍵盤鍵來新增資產啟動的日期和時間](assets/datepicker.png)

   *圖：使用日期選擇器來排程資產啟動。*

1. 若要在特定持續時間後停用資產，請從&#x200B;**[!UICONTROL 關閉時間]**&#x200B;欄位旁的日期選取器選擇停用日期/時間。 停用日期應晚於資產的啟用日期。 在[!UICONTROL 關閉時間]之後，資產及其轉譯無法透過[!DNL Assets]網頁介面或HTTP API使用。

1. 在&#x200B;**[!UICONTROL 標籤]**&#x200B;欄位中，選取一或多個標籤。 若要新增自訂標籤，請在方塊中輸入標籤名稱並選取`Enter`。 新標籤儲存在[!DNL Experience Manager]中。 [!DNL YouTube] 需要標籤才能發佈。請參閱[將視訊發佈至YouTube](video.md#publishing-videos-to-youtube)。

   >[!NOTE]
   >
   >若要建立標籤，您需要CRX存放庫中`/content/cq:tags/default`的寫入權限。

1. 若要提供資產評等，請按一下「**[!UICONTROL 進階]**」標籤，然後按一下適當位置的星號，以指派所需評等。

   ![資產屬性中的進階索引標籤以指派評等](assets/ratings.png)

   您指派給資產的評等分數會顯示在&#x200B;**[!UICONTROL 您的評等]**&#x200B;下方。 從對資產進行評級的使用者收到的資產平均評級分數顯示在&#x200B;**[!UICONTROL Rating]**&#x200B;下。 此外，對平均評等分數有貢獻的評等分數的分割會顯示在&#x200B;**[!UICONTROL 評等劃分]**&#x200B;下。 您可以根據平均評等分數來搜尋資產。

1. 若要檢視資產的使用量統計資料，請按一下&#x200B;**[!UICONTROL Insights]**&#x200B;標籤。

   使用情況統計資料包括：

   * 檢視或下載資產的次數
   * 使用資產的管道/裝置
   * 最近使用資產的創意解決方案

   如需詳細資訊，請參閱[Assets Insights](/help/assets/asset-insights.md)。

1. 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。
1. 導覽至[!DNL Assets]使用者介面。 編輯的中繼資料屬性（包括標題、說明、評等等）會顯示在「卡片」檢視的資產卡片上，以及「清單」檢視的相關欄下。

## 複製資產 {#copying-assets}

複製資產或資料夾時，會複製整個資產或資料夾，及其內容結構。 複製的資產或資料夾會在目標位置複製。 來源位置的資產未變更。

資產特定復本的少數屬性不會結轉。 例如：

* 資產ID、建立日期和時間，以及版本和版本記錄。 其中有些屬性以屬性`jcr:uuid`、`jcr:created`和`cq:name`表示。

* 每個資產及其每個轉譯的建立時間和參考路徑都是唯一的。

保留其他屬性和中繼資料資訊。 複製資產時不會建立部分復本。

1. 在[!DNL Assets]介面中，選取一或多個資產，然後從工具列按一下&#x200B;**[!UICONTROL 複製]**。 或者，從資產介面的工具列中選取&#x200B;**[!UICONTROL 複製]** ![複製選項，並從資產卡片執行快速動作。](assets/do-not-localize/copy_icon.png)

   >[!NOTE]
   >
   >如果您使用[!UICONTROL Copy]快速動作，則一次只能複製一個資產。

1. 導覽至您要複製資產的位置。

   >[!NOTE]
   >
   >如果您複製相同位置的資產， [!DNL Experience Manager]會自動產生名稱的變異。 例如，如果您複製名為`Square`的資產， [!DNL Experience Manager]會自動產生其復本的標題，作為`Square1`。

1. 按一下工具列中資產工具列](assets/do-not-localize/paste.png)資產選項中的&#x200B;**[!UICONTROL 貼上]** ![貼上選項。 然後資產會複製到此位置。

   >[!NOTE]
   >
   >在貼上操作完成之前，工具列中會提供&#x200B;**[!UICONTROL 貼上]**&#x200B;選項。

## 移動和重新命名資產 {#moving-or-renaming-assets}

當您將資產（或資料夾）移至其他位置時，資產（或資料夾）不會重複，這與複製資產時不同。 資產（或資料夾）會放置在目標位置，並從來源位置移除。 您也可以在將資產移至新位置時重新命名資產。
如果您要將已發佈的資產移至其他位置，您可以選擇重新發佈資產。 依預設，已發佈資產的移動操作會自動取消發佈。 如果作者在移動資產時選取[!UICONTROL Republish]選項，則已移動的資產會重新發佈。

![您可以在移動資產時重新發佈已發佈的資產](assets/republish-on-move.png)

若要移動資產或資料夾：

1. 導覽至您要移動的資產位置。

1. 選取資產，然後從工具列按一下「**[!UICONTROL 移動]**」選項。
   ![「資產」工具列中的「移動」選項](assets/do-not-localize/move.png)

1. 在[!UICONTROL 移動資產]精靈中，執行下列其中一項作業：

   * 指定資產移動後的名稱。 然後按一下&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

   * 按一下&#x200B;**[!UICONTROL 取消]**&#x200B;以停止進程。
   >[!NOTE]
   >
   >* 如果新位置沒有具有該名稱的資產，您可以為資產指定相同的名稱。 不過，如果將資產移至資產名稱相同的位置，則應使用不同的名稱。 如果您使用相同的名稱，系統會自動產生名稱的變數。 例如，如果資產的名稱為Square，則系統會為其副本產生名稱Square1。
   >* 重新命名時，檔案名稱中不允許使用空格。


1. 在&#x200B;**[!UICONTROL 選擇目標]**&#x200B;對話框中，執行以下操作之一：

   * 導覽至資產的新位置，然後按一下&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

   * 按一下&#x200B;**[!UICONTROL Back]**&#x200B;返回&#x200B;**[!UICONTROL Rename]**&#x200B;螢幕。

1. 如果要移動的資產有任何參考頁面、資產或集合， **[!UICONTROL 調整參考]**&#x200B;標籤會顯示在&#x200B;**[!UICONTROL 選取目標]**&#x200B;標籤旁。

   在&#x200B;**[!UICONTROL Adjust References]**&#x200B;螢幕中執行以下操作之一：

   * 指定要根據新詳細資訊調整的參考，然後按一下&#x200B;**[!UICONTROL Move]**&#x200B;以繼續。

   * 從&#x200B;**[!UICONTROL Adjust]**&#x200B;欄中選取/取消選取資產的參考。
   * 按一下&#x200B;**[!UICONTROL Back]**&#x200B;返回&#x200B;**[!UICONTROL 選擇目標]**&#x200B;螢幕。

   * 按一下&#x200B;**[!UICONTROL 取消]**&#x200B;以停止移動操作。

   如果您未更新參考，它們會繼續指向資產的先前路徑。 如果調整參照，參照會更新為新資產路徑。

### 使用拖曳作業移動資產 {#move-using-drag}

您可以將資產（或資料夾）拖曳至目標位置，將資產（或資料夾）移至同層級資料夾，而非在使用者介面中使用[!UICONTROL Move]選項。 不過，只有在清單檢視中才能執行此操作。

拖曳資產來移動資產時不會開啟「移動資產」 [!UICONTROL 精靈，因此您在移動時找不到重新命名資產的選項。 ]此外，已發佈的資產會在拖曳後重新發佈，而無須尋求使用者的重新發佈核准。

![將資產拖曳至同層級資料夾中](assets/move-by-drag.gif)

## 管理轉譯 {#managing-renditions}

1. 您可以新增或移除資產的轉譯，但原始資產除外。 導覽至您要新增或移除轉譯的資產位置。

1. 按一下資產以開啟其頁面。
1. 在Experience Manager介面中，從清單中選擇&#x200B;**[!UICONTROL 轉譯]**。
1. 在&#x200B;**[!UICONTROL 轉譯]**&#x200B;面板中，檢視為資產產生的轉譯清單。

   ![「資產詳細資料」頁面上的轉譯面板](assets/renditions_panel.png)

   >[!NOTE]
   >
   >依預設，[!DNL Assets]不會以預覽模式顯示資產的原始轉譯。 如果您是管理員，則可以使用覆蓋來設定[!DNL Assets]以在預覽模式中顯示原始轉譯。

1. 選取轉譯以檢視或刪除轉譯。

   **刪除轉譯**

   從&#x200B;**[!UICONTROL Renditions]**&#x200B;面板中選擇格式副本，然後按一下&#x200B;**[!UICONTROL Delete Rendition]** ![Option以從工具欄刪除格式副本](assets/do-not-localize/deleteoutline.png)選項。 資產處理完成後，無法大量刪除轉譯。 對於個別資產，您可以從使用者介面手動移除轉譯。 對於多個資產，您可以自訂Experience Manager以刪除特定轉譯或刪除資產，然後重新上傳已刪除的資產。

   **上傳新的轉譯**

   導覽至資產的資產詳細資訊頁面，然後按一下&#x200B;**[!UICONTROL 新增轉譯]** ![新增轉譯選項，以在工具列中上傳新轉譯](assets/do-not-localize/add.png)選項，以上傳資產的新轉譯。

   >[!NOTE]
   >
   >如果您從「轉譯」面板選取轉譯 **** ，工具列會變更上下文，並僅顯示與轉譯相關的動作。未顯示[!UICONTROL Upload Rendition]選項。 若要在工具列中檢視這些選項，請導覽至資產的詳細資訊頁面。

   您可以為要顯示在影像或視訊資產詳細資訊頁面中的轉譯設定維度。 [!DNL Assets]會根據您指定的尺寸，顯示包含精確或最接近尺寸的轉譯。

   若要在資產詳細資料層級設定影像的轉譯尺寸，請覆蓋節 `renditionpicker` 點(`libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/renditionpicker`)並設定width屬性的值。設定屬性&#x200B;**[!UICONTROL 大小（長）(KB]**)以取代寬度，以便您可以根據影像大小自訂資產詳細資料頁面上的轉譯。 對於基於大小的定製，如果匹配的 `preferOriginal` 格式副本的大小大於原始格式副本的大小，則屬性會為原始格式副本指定首選項。

   同樣地，您可以通過覆蓋`libs/dam/gui/content/assets/annotate/jcr:content/body/content/content/items/content/renditionpicker`來自定義「注釋」頁影像。

   ![在CRXDE中覆蓋重新選取節點以自訂「註解」頁面影像](assets/renditionpicker-node.png)

   若要設定視訊資產的轉譯維度，請導覽至`/libs/dam/gui/content/assets/assetpage/jcr:content/body/content/content/items/assetdetail/items/col1/items/assetview/videopicker`位置之CRX存放庫的`videopicker`節點、覆蓋節點，然後編輯適當的屬性。

   >[!NOTE]
   >
   >只有具有HTML5相容視訊格式的瀏覽器才支援視訊註解。 此外，根據瀏覽器，支援不同的視訊格式。

如需有關產生和檢視子資產的詳細資訊，請參閱[管理子資產](managing-linked-subassets.md#generate-subassets)。

## 刪除資產 {#deleting-assets}

若要刪除資產，使用者需要`dam/asset`的刪除權限。 如果您只有修改權限，則只能編輯資產中繼資料和新增註解至資產。 不過，您無法刪除資產或其中繼資料。

若要解析或移除其他頁面中傳入的參照，請先更新相關的參照，再刪除資產。 若要禁止使用者刪除參考的資產並保留中斷的連結，請使用覆蓋圖停用強制刪除選項。

若要刪除資產或包含資產的資料夾：

1. 導覽至資產位置或您要刪除的資料夾。

1. 選取資產或資料夾，然後從工具列按一下「刪除&#x200B;**** ![刪除選項](assets/do-not-localize/deleteoutline.png)」。

   確認刪除後：

   * 如果資產沒有參考，則會刪除資產。

   * 如果資產有參考，則會出現錯誤訊息通知您&#x200B;**已參考一或多個資產**。 您可以選取&#x200B;**[!UICONTROL 強制刪除]**&#x200B;或&#x200B;**[!UICONTROL 取消]**。
   >[!NOTE]
   >
   >* 若要解析或移除其他頁面中傳入的參照，請先更新相關的參照，再刪除資產。 此外，使用覆蓋來停用強制刪除選項，以禁止使用者刪除參考的資產並留下中斷的連結。
   >* 可以刪除包含已簽出資產檔案的&#x200B;*資料夾*。 刪除資料夾前，請確定使用者未簽出任何數位資產。


>[!NOTE]
>
>如果您使用上述方法從使用者介面中刪除資料夾，則也會刪除相關的使用者群組。
>
>不過，在製作執行個體(`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`)的JMX中，可使用`clean`方法，從存放庫清理現有的備援、未使用和自動產生的使用者群組。

## 下載資產 {#downloading-assets}

請參閱[從Experience Manager下載資產](/help/assets/download-assets-from-aem.md)。

## 發佈或取消發佈資產 {#publish-assets}

在[!DNL Experience Manager]作者上傳、處理或編輯資產後，您會將資產發佈至發佈伺服器。 發佈可讓資產公開使用。 取消發佈動作會將資產從發佈伺服器中移除，但不會從編寫伺服器移除。

如需[!DNL Dynamic Media]的特定資訊，請參閱[publishing [!DNL Dynamic Media] assets](/help/assets/publishing-dynamicmedia-assets.md)。

1. 導覽至您要發佈或要從發佈環境中移除的資產或資產資料夾位置（取消發佈）。

1. 選取您要取消發佈的資產或資料夾，然後從工具列按一下「管理出版物&#x200B;]**![管理出版物選項](assets/do-not-localize/globe-publication.png)」選項。**[!UICONTROL &#x200B;或者，若要快速發佈，請從工具列選取&#x200B;**[!UICONTROL 快速發佈]**&#x200B;選項。 如果要發佈的資料夾包含空資料夾，則不會發佈空資料夾。

1. 視需要選取&#x200B;**[!UICONTROL Publish]**&#x200B;或&#x200B;**[!UICONTROL Unpublish]**&#x200B;選項。

   ![取消發佈動作](assets/unpublish_action.png)
   *圖：發佈和取消發佈選項及排程選項。*

1. 選取&#x200B;**[!UICONTROL Now]**&#x200B;立即對資產採取行動，或選取&#x200B;**[!UICONTROL Later]**&#x200B;以排程動作。 如果選擇&#x200B;**[!UICONTROL Later]**&#x200B;選項，請選擇日期和時間。 按一下&#x200B;**[!UICONTROL 下一步]**。

1. 發佈時，如果資產參考其他資產，其參考會列在精靈中。 系統只會顯示自上次發佈後取消發佈或修改的參照。 選擇要發佈的參照。

1. 取消發佈時，如果資產參考其他資產，請選擇您要取消發佈的參考。 按一下&#x200B;**[!UICONTROL 取消發佈]**。 在確認對話方塊中，按一下&#x200B;**[!UICONTROL 取消]**&#x200B;以停止動作，或按一下&#x200B;**[!UICONTROL 取消發佈]**&#x200B;以確認資產將在指定日期取消發佈。

了解發佈或取消發佈資產或資料夾的相關下列限制和秘訣：

* [!UICONTROL 管理出版物]選項僅適用於具有復寫權限的使用者帳戶。
* 取消發佈複雜資產時，僅取消發佈資產。 請避免取消發佈參考，因為其他已發佈的資產可能會參照這些參考。
* 未發佈空資料夾。
* 如果您發佈的資產經過處理，則只會發佈原始內容。 遺失轉譯。 等待處理完成，然後在處理完成後發佈或重新發佈資產。

## 已關閉的使用者群組 {#closed-user-group}

封閉的使用者群組(CUG)可用來限制對從[!DNL Experience Manager]發佈的特定資產資料夾的存取。 如果為資料夾建立CUG，則對資料夾（包括資料夾資產和子資料夾）的訪問權限僅限於分配的成員或組。 若要存取資料夾，使用者必須使用其安全憑證登入。

CUG是限制存取資產的額外方式。 您也可以為資料夾設定登入頁面。

1. 從[!DNL Assets]介面中選擇資料夾，然後按一下工具欄中的[!UICONTROL 屬性]選項以顯示屬性頁。
1. 從&#x200B;**[!UICONTROL Permissions]**&#x200B;頁簽，在&#x200B;**[!UICONTROL Closed User Group]**&#x200B;下添加成員或組。

   ![在封閉用戶組中添加用戶](assets/add_user.png)

1. 若要在使用者存取資料夾時顯示登入畫面，請選取&#x200B;**[!UICONTROL 啟用]**&#x200B;選項。 然後，選擇[!DNL Experience Manager]中登錄頁的路徑，並保存更改。

   ![啟用並選擇登錄頁以在用戶訪問資料夾時顯示](assets/login_page.png)

   >[!NOTE]
   >
   >如果您未指定登入頁面的路徑，[!DNL Experience Manager]會在發佈執行個體中顯示預設登入頁面。

1. 發佈資料夾，然後嘗試從發佈執行個體存取資料夾。 隨即顯示登入畫面。
1. 如果您是CUG成員，請輸入您的安全憑據。 資料夾會在[!DNL Experience Manager]驗證您後顯示。

## 搜尋資產 {#assetsearch}

搜尋資產是使用數位資產管理系統的核心。 此功能對於創意人員、業務使用者和行銷人員對資產的健全管理，或DAM管理員的管理，都很重要。

如需簡單、進階和自訂搜尋以探索及使用最適當的資產，請參閱Experience Manager](search-assets.md)中的[搜尋資產。

## 快速動作 {#quick-actions}

一次只有一個資產的快速動作圖示可用。視您的裝置而定，執行下列動作以顯示快速動作圖示：

* 觸摸設備：觸摸並按住。 例如，在iPad上，您可以點選並按住資產，以顯示快速動作。
* 非接觸裝置：暫留指針。 例如，在案頭裝置上，如果將指標暫留在資產縮圖上，則會顯示快速動作列。

### 導覽及選取資產 {#navigating-and-selecting-assets}

您可以使用&#x200B;**[!UICONTROL Select]**&#x200B;選項，檢視、導覽及選取具有任何可用檢視（卡片、欄及清單）的資產。

在清單檢視和欄檢視中，當您將指標暫留在資產縮圖上時，會顯示&#x200B;**[!UICONTROL Select]**&#x200B;選項。

在卡片檢視中，**[!UICONTROL Select]**&#x200B;選項會顯示為快速動作。

在瀏覽器的[!DNL Assets]使用者介面中瀏覽資料夾或集合時，您可以使用右上角的[!UICONTROL 全選]選項，選取所有顯示或載入的資產。 起初，卡片檢視中只會載入100個資產，清單檢視中只會載入200個資產。 當您捲動搜尋結果頁面時，檢視中會載入更多資產。 [!UICONTROL 全選]選項只會選取載入的資產。

如需詳細資訊，請參閱[檢視並選取您的資源](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)。

## 編輯影像 {#editing-images}

[!DNL Assets]介面中的編輯工具可讓您對影像資產執行小型編輯工作。 您可以裁切、旋轉、翻轉和對影像執行其他編輯工作。 您也可以將影像地圖新增至資產。

>[!NOTE]
>
>對於某些元件，全螢幕模式有其他可用選項。

1. 執行下列其中一項操作，以在編輯模式中開啟資產：

   * 選取資產，然後按一下工具列中的&#x200B;**[!UICONTROL 編輯]**。
   * 按一下顯示在卡片檢視中資產上的&#x200B;**[!UICONTROL 編輯]**&#x200B;選項。
   * 從工具欄![編輯選項](assets/do-not-localize/edit_icon.png)中，按一下&#x200B;**[!UICONTROL 編輯]**。

1. 若要裁切影像，請按一下「**[!UICONTROL 裁切]** ![選項」來裁切影像](assets/do-not-localize/crop.png)。

1. 從清單中選取所需的選項。裁切區域會根據您選擇的選項出現在影像上。「自 **由手形** 」選項可讓您裁切影像，而不受任何外觀比例限制。

1. 選取要裁切的區域，並在影像上調整大小或重新定位。

1. 使用&#x200B;**[!UICONTROL Undo]** ![Undo工具欄選項](assets/do-not-localize/undo.png)和&#x200B;**[!UICONTROL Redo]** ![重做工具欄選項](assets/do-not-localize/redo.png)選項分別恢復到未裁切的影像或保留已裁切的影像。
1. 按一下適當的&#x200B;**[!UICONTROL 旋轉]**&#x200B;選項，順時針或逆時針旋轉影像。

   ![順時針和逆時針旋轉選項](assets/do-not-localize/rotate-options.png)

1. 如果要水準翻轉影像![reflect horizontal選項](assets/do-not-localize/flip-horizontal.png)或垂直翻轉![reflect vertical選項](assets/do-not-localize/flip-vertical.png)，請按一下相應的&#x200B;**[!UICONTROL Flip]**&#x200B;選項。

1. 要完成影像編輯，請按一下&#x200B;**[!UICONTROL 完成]** ![完成選項](assets/do-not-localize/check-ok-done-icon.png)。 按一下&#x200B;**完成**&#x200B;也會開始重新產生轉譯。

>[!NOTE]
>
>BMP、GIF、PNG和JPEG檔案格式支援影像編輯。

您也可以使用影像編輯器新增影像地圖。 如需詳細資訊，請參閱[新增影像地圖](/help/assets/image-maps.md)。

>[!NOTE]
>
>要編輯TXT檔案，請從Configuration Manager設定&#x200B;**Day CQ Link Externalizer**。

## 時間軸 {#timeline}

時間軸可讓您檢視所選項目的各種事件，例如資產的作用中工作流程、註解/註解、活動記錄檔和版本。

![排序資產的時間軸項目](assets/sort_timeline.gif)

*圖：排序資產的時間軸項目。*

>[!NOTE]
>
>在[集合控制台](/help/assets/manage-collections.md#navigating-the-collections-console)中， **[!UICONTROL 全部顯示]**&#x200B;清單提供僅查看注釋和工作流的選項。 此外，時間軸只會針對控制台中列出的頂層集合顯示。 如果您導覽至任何系列內，畫面不會顯示。

>[!NOTE]
>
>時間軸包含多個內容片段專用的[選項](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments)。

## 為資產加上注釋 {#annotating}

註解是在影像或影片中新增的註解或說明性附註。 註解可讓行銷人員共同作業，並提供資產的相關意見。

只有HTML5相容視訊格式的瀏覽器才支援視訊註解。 [!DNL Assets]支援的視訊格式取決於瀏覽器。

>[!NOTE]
>
>對於內容片段，會在片段編輯器](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)中建立[註解。

1. 導覽至您要新增註解的資產位置。
1. 按一下以下其中一項中的&#x200B;**[!UICONTROL 注釋]**&#x200B;選項：

   * [快速動作](/help/assets/manage-assets.md#quick-actions)
   * 在選取資產或導覽至資產頁面後，從工具列中選取。

1. 在時間軸底部的 **[!UICONTROL 「注釋]** 」方塊中新增注釋。或者，在影像上標籤一個區域，並在「添加註釋」( **[!UICONTROL Add Annotation]** )對話框中添加註釋。

1. 要通知用戶注釋，請指定用戶的電子郵件地址並添加註釋。 例如，要通知Aaron MacDonald注釋，請輸入@aa。 清單中顯示所有匹配用戶的提示。 從清單中選擇Aaron的電子郵件地址，以便您可以用注釋標籤該人員。 同樣地，您可以在批注內或批注前後的任意位置標籤更多用戶。

   ![指定用戶的電子郵件地址並添加註釋以通知用戶](assets/annotate-gif.gif)

   >[!NOTE]
   >
   >對於非管理員使用者，只有當使用者具有CRXDE中`/home`路徑的讀取權限時，才會顯示建議。

1. 新增附註後，按一下「**[!UICONTROL 新增]**」加以儲存。 向Aaron發送注釋通知。

   >[!NOTE]
   >
   >您可以先新增多個註解，再儲存。

1. 按一下&#x200B;**[!UICONTROL 關閉]**&#x200B;退出「注釋」模式。
1. 若要檢視通知，請使用Aaron MacDonald的憑證登入[!DNL Assets]，然後按一下&#x200B;**[!UICONTROL Notifications]**&#x200B;選項以檢視通知。

   >[!NOTE]
   >
   >您也可以將註解新增至視訊資產。 為視訊加上註解時，播放器會暫停，讓您在影格上加上註解。 如需詳細資訊，請參閱[管理視訊資產](/help/assets/managing-video-assets.md)。

1. 要選擇不同的顏色以便區分用戶，請按一下「配置檔案」選項，然後按一下&#x200B;**[!UICONTROL 「我的首選項]**」。

   ![依次選擇用戶配置檔案選項和我的首選項以開啟用戶首選項](assets/User-profile-preferences.png)

   在「**[!UICONTROL 注釋顏色]**」框中指定所要的顏色，然後按一下「**[!UICONTROL 接受]**」。

   ![在「用戶首選項」中選擇注釋顏色以設定用戶角色顏色](assets/Annotation-color.png)

>[!NOTE]
>
>您也可以將註解新增至集合。 不過，如果集合包含子集合，則只能向父集合添加註釋/注釋。 「注釋」選項不適用於子集合。

### 查看保存的注釋 {#viewing-saved-annotations}

一次只能查看一個批注。

>[!NOTE]
>
>如果要選擇多個注釋，則用戶介面上會顯示最新的注釋。
>
>僅支援多選，以便將註解的資產列印為PDF。

**若要檢視資產的已儲存註解：**

1. 前往資產位置，然後開啟資產頁面。

1. 在Experience Manager介面中，選擇&#x200B;**[!UICONTROL 時間軸]**。
1. 從時間軸 **[!UICONTROL 的「顯示全部]** 」清單中，選取「注 **[!UICONTROL 釋]** 」以根據註解來篩選結果。

   如果要查看影像上的相應注釋，請按一下&#x200B;**[!UICONTROL 時間軸]**&#x200B;面板中的注釋。

   ![查看影像注釋的時間軸面板](assets/timeline-view-annotations.png)

   按一下&#x200B;**[!UICONTROL Delete]**&#x200B;以刪除特定注釋。

### 打印注釋 {#printing-annotations}

如果資產有註解，或已經受審核工作流，則您可以將資產連同注釋和審核狀態打印為PDF檔案，以便離線審核。

您也可以選擇僅打印注釋或查看狀態。

>[!NOTE]
>
>您可以在將已註解的資產列印為PDF時選取多個註解。

要打印注釋和查看狀態，請按一下&#x200B;**[!UICONTROL Print]**，然後按照嚮導中的說明操作。 只有當資產至少為其分配了一個批注或審閱狀態時，**[!UICONTROL 打印]**&#x200B;選項才會出現在工具欄中。

1. 從[!DNL Assets]介面，開啟資產的預覽頁面。
1. 執行下列任一操作：

   * 要打印所有注釋和審閱狀態，請跳過步驟3並直接轉到步驟4。
   * 要打印特定注釋和查看狀態，請開啟[時間軸](/help/assets/manage-assets.md#timeline)，然後轉到步驟3。

1. 要打印特定注釋，請從時間軸中選擇注釋。

   ![從時間軸中選擇注釋以打印它](assets/timeline-select-annotations.png)

   要僅打印審閱狀態，請從時間軸中選擇它。

1. 按一下工具欄上的&#x200B;**[!UICONTROL 打印]**。

1. 從「打印」對話框中，選擇要在PDF上顯示注釋/審閱狀態的位置。 例如，如果希望在包含打印影像的頁面的右上方打印注釋/狀態，請使用&#x200B;**左上**&#x200B;設定。 預設會選取。

   您可以根據要在打印的PDF中顯示注釋/狀態的位置選擇其他設定。如果您希望註解/狀態顯示在與印刷資產不同的頁面中，請選擇「下 **[!UICONTROL 一頁」]**。

1. 按一下&#x200B;**[!UICONTROL 打印]**。 根據您在步驟2中選擇的選項，產生的PDF會在指定位置顯示註解/狀態。例如，如果您選擇使用左上角設定打印注釋和審閱狀態 **** ，則生成的輸出類似於此處所示的PDF檔案。

   ![對生成的PDF進行注釋和審閱狀態](assets/annotation-status-pdf.png)

1. 下載PDF](assets/do-not-localize/download.png)的「下載」選項，或使用右上角的選項在PDF](assets/do-not-localize/print.png)上打印PDF![打印選項。![

   >[!NOTE]
   >
   >如果資產有子資產，您可以列印所有子資產及其特定的頁面註解。

   要編輯呈現的PDF檔案的外觀，例如字型顏色、大小和樣式，請從Configuration Manager中開啟&#x200B;**[!UICONTROL 注釋PDF配置]**，並修改所需的選項。 例如，若要變更已核准狀態的顯示顏色，請修改對應欄位中的顏色代碼。 有關更改批注的字型顏色的資訊，請參閱[批注](/help/assets/manage-assets.md#annotating)。

   ![在PDF文檔上打印資產批注的配置](assets/annotation-print-pdf-config.png)

   返回呈現的PDF檔案並重新整理。 重新整理的PDF會反映您所做的變更。

如果資產包含外文（尤其是非拉丁語）的註解，您必須先在[!DNL Experience Manager]伺服器上設定CQ-DAM-Handler-Gibson字型管理器服務，才能列印這些註解。 在配置CQ-DAM-Handler-Gibson字型管理器服務時，提供所需語言字型的位置路徑。

1. Open the CQ-DAM-Handler-Gibson Font Manager Service configuration page from the URL `https://[aem_server]:[port]/system/console/configMgr/com.day.cq.dam.handler.gibson.fontmanager.impl.FontManagerServiceImpl`.
1. To configure CQ-DAM-Handler-Gibson Font Manager Service, do one of the following:

   * 在「系統字型」目錄選項中，指定系統上字型目錄的完整路徑。 例如，如果您是Mac用戶，可以在「系統字型」目錄選項中將路徑指定為&#x200B;*/Library/Fonts*。 [!DNL Experience Manager] fetches the fonts from this directory.
   * 在`crx-quickstart`資料夾內建立名為`fonts`的目錄。 CQ-DAM-Handler-Gibson字型管理器服務自動在`crx-quickstart/fonts`位置提取字型。 您可以從Adobe伺服器字型目錄選項內覆寫此預設路徑。

   * 在系統中為字型建立資料夾，並將所需字型儲存在資料夾中。 然後，在「客戶字型」目錄選項中指定該資料夾的完整路徑。

1. 從URL `https://[aem_server]:[4502]/system/console/configMgr/com.day.cq.dam.core.impl.annotation.pdf.AnnotationPdfConfig`訪問「注釋PDF」配置。
1. 使用正確的字型系列集配置「注釋」PDF，如下所示：

   * 在font-family選項中包含字串`<font_family_name_of_custom_font, sans-serif>`。 例如，如果要以CJK（中文、日文和韓文）打印注釋，請在字型系列選項中包含字串`Arial Unicode MS, Noto Sans, Noto Sans CJK JP, sans-serif`。 如果要以印地語打印注釋，請下載相應的字型，並將字型系列配置為Arial® Unicode MS®、Noto Sans、Noto Sans CJK JP、Noto Sans Devalagari、sans-serif。

1. 重新啟動[!DNL Experience Manager]部署。

以下是如何配置[!DNL Experience Manager]以在CJK（中文、日文和韓文）中打印注釋的示例：

1. 從以下連結下載Google Noto CJK字型，並將其儲存在字型管理器服務中配置的字型目錄中。

   * 全部以一個超CJK字型顯示：[https://www.google.com/get/noto/help/cjk/](https://www.google.com/get/noto/help/cjk/)
   * Noto Sans（適用於歐洲語言）:[https://www.google.com/get/noto/](https://www.google.com/get/noto/)
   * 您所選擇的語言的無字型：[https://www.google.com/get/noto/](https://www.google.com/get/noto/)

1. 將font-family參數設定為`Arial Unicode MS, Noto Sans, Noto Sans CJK JP, sans-serif`以配置注釋PDF檔案。 此配置預設可用，適用於所有歐洲和中日韓語言。
1. 如果您選擇的語言與步驟2中提到的語言不同，請在預設字型系列中附加適當（以逗號分隔）的項。

## 建立、管理、預覽和回復資產版本 {#asset-versioning}

版本設定會建立數位資產在特定時間點的快照。版本設定有助於稍後將資產還原為先前狀態。 例如，如果您想要還原對資產所做的變更，請還原未編輯的資產版本。 在[!DNL Experience Manager]中，您可以建立版本、檢視目前修訂版本、檢視兩個影像版本之間並排的差異，以及將資產還原為其舊版。

在以下情況下，您可以在[!DNL Experience Manager]中建立版本：

* 上傳檔案名稱相同且位於相同位置的資產。 可以是新資產或相同資產的修改版本。
* 在[!DNL Experience Manager]中編輯影像並儲存變更。
* 編輯資產的中繼資料。
* 使用[!DNL Experience Manager]案頭應用程式來簽出現有資產、編輯資產，然後[上傳您的變更](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#edit-assets-upload-updated-assets)。

您也可以透過工作流程啟用自動版本設定。 當您建立資產的版本時，中繼資料和轉譯會與版本一併儲存。 轉譯是相同影像的替代項目，例如上傳之JPEG檔案的PNG轉譯。

1. 導覽至您要建立版本的資產位置，然後按一下以開啟預覽。 從頁面的左上角開啟功能表，然後選取&#x200B;**[!UICONTROL 時間軸]**。

   ![從左側導覽功能表中，選取時間軸選項](assets/timeline.png)

   *圖：從頁面的左上角開啟功能表，然後選取「時  間線」選項。*

1. 若要建立資產版本：

   * 按一下底部的&#x200B;**[!UICONTROL Actions]**。
   * 按一下「**[!UICONTROL 另存新檔]**」，即可建立資產的版本。 （可選）添加標籤和注釋。
   * 按一下&#x200B;**[!UICONTROL 建立]**&#x200B;以建立版本。

      ![從側欄建立資產版本](assets/create-new-version-from-timeline.png)

      *圖：從Timelineleft側欄建立資產  版本。*

1. 若要檢視資產版本：

   * 按一下[!UICONTROL 時間軸]中的「顯示全部」]**。**[!UICONTROL 
   * 按一下「**[!UICONTROL 版本]**」。 為資產建立的所有版本都會列在左側邊欄。

   * 選取資產的特定版本，然後按一下「**[!UICONTROL 預覽版本]**」。

1. 若要回復成舊版資產，請執行下列動作。 回復後，此版本會顯示在[!DNL Assets]介面中，並可供使用。

   * 按一下資產的版本。 （可選）添加標籤和注釋。
   * 按一下「**[!UICONTROL 還原為此版本]**」。

      ![選擇要還原的版本](assets/select_version.png)

      *圖：選取版本並回復至該版本。它會變成目前版本，然後可供DAM使用者使用。*

1. 若要比較兩個版本的影像，請遵循下列步驟：
   * 按一下要與目前版本比較的版本。
   * 將滑桿拖曳至左側，將此版本疊加在目前版本上並進行比較。

   ![使用滑桿來比較資產的選定版本與目前版本](assets/version-slider.gif)

   *圖：使用滑桿來輕鬆比較資產的選定版本與目前版本。*

### 啟動資產的工作流程 {#starting-a-workflow-on-an-asset}

若要套用工作流程以處理資產，請參閱[啟動資產](/help/assets/assets-workflow.md#apply-a-workflow-to-an-asset)上的工作流程。

## 集合 {#collections}

集合是一組已排序的資產。 使用集合在使用者之間共用相關資產，或將類似資產叢集在一起，以便輕鬆探索。

* A collection can include assets from different locations because they only contain references to these assets. 每個集合會維護資產的參考完整性。
* 您可以與具有不同權限層級的多個使用者共用集合，包括編輯、檢視等。

要了解集合管理的詳細資訊，請參閱[管理集合](/help/assets/manage-collections.md)。

## 在案頭應用程式或Adobe資產連結中檢視資產時，隱藏過期的資產 {#hide-expired-assets-via-acp-api}

[!DNL Experience Manager] 案頭應用程式可從Windows或Mac案頭存取DAM存放庫。Adobe資產連結可讓您從支援的[!DNL Creative Cloud]案頭應用程式存取資產。

從[!DNL Experience Manager]使用者介面內瀏覽資產時，不會顯示過期的資產。 若要防止從案頭應用程式和「資產連結」瀏覽資產時檢視、搜尋及擷取過期的資產，管理員可以執行下列設定。 此配置適用於所有用戶，而不考慮管理員權限。

執行以下CURL命令。 對於存取資產的使用者，請確保在`/conf/global/settings/dam/acpapi/`上有讀取存取權。 屬於`dam-user`群組的使用者依預設擁有權限。

```curl
curl -v -u admin:admin --location --request POST 'http://localhost:4502/conf/global/settings/dam/acpapi/configuration/_jcr_content' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'jcr:title=acpapiconfig' \
--data-urlencode 'hideExpiredAssets=true' \
--data-urlencode 'hideExpiredAssets@TypeHint=Boolean' \
--data-urlencode 'jcr:primaryType=nt:unstructured' \
--data-urlencode '../../jcr:primaryType=sling:Folder'
```

若要深入了解，請參閱如何使用案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets)和[如何使用Adobe資產連結](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html)來瀏覽DAM資產。[
