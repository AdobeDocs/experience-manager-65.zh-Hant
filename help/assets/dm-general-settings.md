---
title: 配置Dynamic Media常規設定
description: 瞭解如何在Dynamic Media管理常規設定。 您可以在此處設定發佈伺服器名稱和源伺服器名稱，並設定映像覆蓋選項。 還有預設的上載選項，用於對影像進行非銳化屏蔽，以及上載選項，用於處理PostScript、Adobe Photoshop、PDF和Adobe Illustrator檔案。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: 55cc7c57-87a0-4bfb-b226-36d01d36849a
source-git-commit: 9c548dbc0157607adda5ed76cab8ef970588e1e9
workflow-type: tm+mt
source-wordcount: '2498'
ht-degree: 4%

---

# 配置Dynamic Media常規設定

配置 **[!UICONTROL Dynamic Media常規設定]** 僅當：

* 您以Scene7模式運行Dynamic Media。 請參閱 [在Scene7模式下啟用Dynamic Media](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode)。
* 你有 *現有* **[!UICONTROL Dynamic Media配置]** (在 **[!UICONTROL Cloud Services]**)，在Adobe Experience Manager6.5.11或更高版本。 請參閱 [在Cloud Services中建立Dynamic Media配置](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)。
* 您是具有管理員權限的Experience Manager系統管理員。

Dynamic Media常規設定僅供經驗豐富的網站開發人員和程式設計師使用。 Adobe·Dynamic Media建議更改這些發佈設定的用戶熟悉Adobe Experience Manager的Dynamic Media和基本成像技術。

在建立帳戶時，AdobeDynamic Media會自動為您的公司提供指定的伺服器。 這些伺服器用於為網站和應用程式構建URL字串。 這些URL調用是特定於您的帳戶的。

「Dynamic Media發佈設定」頁建立預設設定，確定如何將資產從AdobeDynamic Media伺服器傳送到網站或應用程式。 如果未指定任何設定，AdobeDynamic Media伺服器將根據在Dynamic Media發佈設定頁面上配置的預設設定來傳遞資產。

另請參閱 [可選 — Dynamic Media-Scene7模式設定的設定和配置](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings) 的子菜單。

>[!NOTE]
>
>從Dynamic Media Classic升級到Adobe Experience ManagerDynamic Media? 「常規設定」頁和 [發佈設定](/help/assets/dm-publish-settings.md) 在Dynamic Media的頁面中預先填充了從您的Dynamic Media Classic帳戶獲取的值。 例外是列在 **[!UICONTROL 預設上載選項]** 的子菜單。 這些值已經處於Experience Manager。 因此，您在 **[!UICONTROL 預設上載選項]**，通過Experience Manager用戶介面，在五個頁籤中的任何一個頁籤上都反映在Dynamic Media，而不是Dynamic Media Classic。 「常規設定」頁和 [發佈設定](/help/assets/dm-publish-settings.md) 在Dynamic Media Classic和Dynamic Media之間保持Experience Manager。

**配置Dynamic Media常規設定：**

1. 在「Experience Manager作者」模式下，選擇Experience Manager徽標以訪問全局導航控制台。
1. 在左滑軌中，選擇「工具」表徵圖，然後轉到 **[!UICONTROL 資產]** > **[!UICONTROL Dynamic Media常規設定]**。
1. 在「伺服器」頁中，設定 **[!UICONTROL 已發佈伺服器名稱]** 和 **[!UICONTROL 源伺服器名稱]**，然後使用五個頁籤配置影像編輯和Postscript、Photoshop、PDF和Illustrator檔案的預設上載選項。

   * [伺服器](#server-general-setting)
   * [上傳至應用程式](#upload-to-application)
   * [影像編輯](#image-editing-tab) 頁籤
   * [PostScript](#postscript-tab) 頁籤
   * [Photoshop](#photoshop-tab) 頁籤
   * [PDF](#pdf-tab) 頁籤
   * [Illustrator](#illustrator-tab) 頁籤

   ![Dynamic Media常規設定頁](/help/assets/assets-dm/dm-general-settings.png)
   *Dynamic Media常規設定頁面，**[!UICONTROL 影像編輯]**的子菜單。*<br><br>

1. 完成後，在頁面右上角附近，選擇 **[!UICONTROL 保存]**。

## 伺服器 {#server-general-setting}

在建立帳戶時，AdobeDynamic Media會自動為您的公司提供指定的伺服器。 這些伺服器用於為網站和應用程式構建URL字串。 這些URL調用是特定於您的帳戶的。

| 選項 | 說明 |
| --- | --- |
| **[!UICONTROL 已發佈的伺服器名稱]** | 必要.<br>名稱必須使用 `https://` 在路上。<br>此伺服器是特定於您帳戶的所有系統生成URL調用中使用的即時CDN（內容分發網路）伺服器。 除非Adobe技術支援指示您更改此伺服器名稱，否則不要更改此名稱。 |
| **[!UICONTROL 原始伺服器名稱]** | 必要.<br>此伺服器僅用於質量保證測試。 除非Adobe技術支援部門指示更改此伺服器名稱，否則不要更改此名稱。 |

## 上傳至應用程式 {#upload-to-application}

* **[!UICONTROL 覆寫影像]**

   AdobeDynamic Media不允許兩個檔案具有相同的名稱。 每個項的AdobeDynamic MediaID（映像名稱減去檔案副檔名）必須唯一。 因為這個規則， **[!UICONTROL 上載到應用程式]** 已覆蓋。 此選項的確切效果取決於您選擇的指定「覆蓋影像」選項。 這些選項指定如何上載替換映像：是替換原始影像，還是變成重複影像。 使用 `-1`。 比如說， `chair.tif` 已更名 `chair-1.tif`。 這些選項會影響上載到與原始資料夾不同的資料夾的影像，或具有與原始檔案不同檔案副檔名的影像，如JPG、TIF或PNG。

   >[!NOTE]
   >
   >要保持與Experience Manager的一致性，請選擇「覆蓋影像」選項 **[!UICONTROL 在當前資料夾中覆蓋，基名/副檔名相同]**。

   | 「覆蓋影像」選項 | 說明 |
   | --- | --- |
   | **[!UICONTROL 在目前檔案夾中有基底名稱/副檔名相同者時予以覆寫]** | *預設* 只針對新Dynamic Media賬戶。<br>此選項是最嚴格的替換規則。 它要求您將替換映像上載到與原始映像相同的資料夾，並且替換映像的檔案副檔名與原始映像的副檔名相同。 如果未滿足這些要求，則會建立重複項。<br>*要保持與Experience Manager的一致性，請選擇此選項*。 |
   | **[!UICONTROL 在目前檔案夾中有基本名稱相同者 (無論副檔名為何) 時予以覆寫]** | 需要將替換映像上載到與原始映像相同的資料夾，但檔案副檔名可能與原始映像不同。 例如，chair.tif代替chair.jpg。 |
   | **[!UICONTROL 任何檔案夾內若有基本資產名稱/副檔名相同者，將予以覆寫]** | 要求替換影像與原始影像具有相同的檔案副檔名（例如，chair.jpg必須替換chair.jpg，而不是chair.tif）。 但是，您可以將替換影像上載到與原始資料夾不同的資料夾中。 更新後的影像駐留在新資料夾中；在檔案的原始位置中找不到該檔案。 |
   | **[!UICONTROL 任何檔案夾內若有基本資產名稱相同者 (無論副檔名為何)，將予以覆寫]** | 此選項是最包容的替換規則。 您可以將替換影像上載到與原始檔案不同的資料夾中，上載具有不同檔案副檔名的檔案，並替換原始檔案。 如果原始檔案位於其他資料夾中，則替換映像將駐留在上載到的新資料夾中。 |

* **[!UICONTROL 保留裁切]**

   控制現有手動裁剪定義的保留。

   另請參閱 `preserveCrop` 在 [上載後作業](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html) 和 [重新處理AssetsJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html)，都在《Dynamic Media觀眾參考指南》中。

## 預設上載選項 {#default-upload-options}

### 「影像編輯」頁籤 {#image-editing-tab}

通過此濾鏡，可以對最終的下採樣影像微調銳化濾鏡效果。 它有助於您控制效果的強度、效果半徑（以像素為單位）以及忽略的對比度閾值。

「非銳化蒙版」效果使用的選項與Photoshop的「非銳化蒙版」濾鏡相同。 與名稱相反，「非銳化蒙版」是銳化濾鏡。

| 「非銳化蒙版」選項 | 說明 |
| --- | --- |
| **[!UICONTROL 數量]** | 必要.<br>控制應用於邊緣像素的對比度量。<br>把它看成效果的強度。 在AdobeDynamic Media的Unsharp Mask值與在Adobe Photoshop的Amont值之間的主要區別是，Photoshop的金額範圍在1%至500%之間。 而在AdobeDynamic Media，價值範圍是 `0.0` 至 `5.0`。 Dynamic MediaAdobe的5.0大致相當於Photoshop的500%;0.9等於90%，依此類推。 |
| **[!UICONTROL 半徑]** | 必要.<br>控制效果的半徑。<br>值範圍是 `0` 至 `250`。 該效果在影像中的所有像素上運行，並從所有方向的所有像素輻射出來。 半徑以像素計量。 例如，要對2000 x 2000像素影像和500 x 500像素影像獲得類似的銳化效果，應在2000 x 2000像素影像上設定兩個像素的半徑。 然後在500 x 500像素影像上設定一個像素的半徑值。 對於具有更多像素的影像，使用較大的值。 |
| **[!UICONTROL 臨界值]** | 必要.<br>閾值是應用「非銳化蒙版」濾鏡時忽略的對比度範圍。 此效果非常重要，因此在使用此濾鏡時不會將「雜訊」引入影像。 值範圍是 `0` - `255`，即灰度影像中的亮度步數。 `0`=黑色， `128`=50%灰色和 `255`=white。<br>閾值 `12` 忽略膚色的細微變化是膚色亮度，以免加噪音，但仍會為眼睫毛與皮膚相遇的區域增加邊緣對比度。<br>如果您有某人的面部照片，「非銳化蒙版」會影響影像的禁忌部分。 例如，睫毛和皮膚會聚，形成明顯的對比區域，皮膚本身也是光滑的。 即使最光滑的皮膚也在亮度值上表現出微妙的變化。 如果不使用閾值，濾鏡會突出皮膚像素中的這些細微變化。 反之，在增加睫毛對比度的同時產生雜訊和不希望的效果，增強銳度。<br>為避免此問題，引入了閾值，該閾值指示濾波器忽略不會顯著改變對比度的像素，如平滑皮膚。<br>在前面顯示的拉鍊圖形中，注意拉鍊旁邊的紋理。 由於閾值過低，無法抑制雜訊，因此出現了影像雜訊。 |
| **[!UICONTROL 單色]** | 選擇以取消銳化蒙版影像亮度（強度）。<br>取消選擇以單獨取消對每個顏色分量進行銳化。 |

另請參閱 [銳化AdobeDynamic Media和影像伺服器上的影像](/help/assets/assets/sharpening_images.pdf)。

### PostScript頁籤 {#postscript-tab}

您可以柵格化Adobe PostScript®檔案、維護透明背景、選擇解析度和選擇顏色空間。

您可以在AdobeDynamic Media使用Adobe PostScript®(EPS)檔案。 Adobe·Dynamic Media提供了在上傳這些檔案時配置這些檔案的命令。

上載PostScript(EPS)映像檔案時，可以採用各種格式設定它們。 您可以柵格化檔案、維護透明背景、選擇解析度和選擇顏色空間。

| PostScript選項 | 說明 |
| --- | --- |
| **[!UICONTROL 處理]** | 選擇「柵格化」(Rasterize)，將檔案中的向量圖形轉換為點陣圖格式。 |
| **[!UICONTROL 在演算後的影像中保留透明背景]** | 保留檔案的背景透明度。 |
| **[!UICONTROL 解析度 (像素/英吋)]** | 確定解析度設定。 此設定確定檔案中每英吋顯示的像素數。 |
| **[!UICONTROL 顏色空間]** | · **[!UICONTROL 自動檢測]**  — 保留檔案的顏色空間。<br>· **[!UICONTROL 強制為RGB]**  — 轉換為RGB顏色空間。<br>· **[!UICONTROL 強制為CMYK]**  — 轉換為CMYK顏色空間。<br>· **[!UICONTROL 強制為灰度]**  — 轉換為灰度色空間。 |

### Photoshop頁籤 {#photoshop-tab}

您可以從Adobe®Photoshop®檔案建立模板，維護圖層，指定圖層的命名方式，提取文本，並指定如何將影像定位到模板中。

| Photoshop選項 | 說明 |
| --- | --- |
| **[!UICONTROL 保留圖層]** | 將PSD中的層（如果有）拆分為單個資產。 資產層仍與PSD關聯。 可通過在「詳細資訊視圖」中開啟PSD檔案並選擇層面板來查看它們。 請參閱查看和編輯PSD檔案中的圖層。 |
| **[!UICONTROL 建立範本]** | 從PSD檔案中的層建立模板。 |
| **[!UICONTROL 擷取文字]** | 提取文本，以便用戶可以在查看器中搜索文本。 |
| **[!UICONTROL 延伸圖層以符合背景大小]** | 將撕裂影像圖層的大小擴展到背景圖層的大小。 |
| **[!UICONTROL 圖層命名]** | 將撕裂影像圖層的大小擴展到背景圖層的大小。<br>· **[!UICONTROL 層名稱]**  — 在PSD檔案中將影像命名為圖層名稱。 例如，原始PSD檔案中名為「價格標籤」的圖層將變成名為「價格標籤」的影像。 但是，如果PSD檔案中的圖層名稱是預設的Photoshop圖層名稱（背景、第1層、第2層等），則這些影像將以其在PSD檔案中的圖層編號命名。 <br>· **[!UICONTROL Photoshop和層號]**  — 在PSD檔案中將影像命名為圖層編號，忽略原始圖層名稱。 影像以Photoshop檔案名和附加的圖層號命名。 例如，檔案的第二層 `Spring Ad.psd` 命名 `Spring Ad_2` 即使在Photoshop有個非預設名稱。<br>· **[!UICONTROL Photoshop和層名]**  — 將影像命名為PSD檔案後面的圖層名稱或圖層編號。 如果PSD檔案中的層名是預設的Photoshop層名，則使用層號。 例如，名為 `Price Tag` 在名為 `SpringAd` 命名 `Spring Ad_Price Tag`。 調用預設名為「層2」的層 `Spring Ad_2`。 |
| **[!UICONTROL 錨點]** | 指定如何將影像定位到從PSD檔案生成的分層合成生成的模板中。 預設情況下，錨點為中心。 中心錨點允許替換影像最好地填充相同的空間，而不管替換影像的長寬比。 當引用模板並使用參數替換時，具有不同方面的影像可替換此影像，有效地佔用了相同的空間。 如果應用程式需要替換影像來填充模板中分配的空間，請更改為其他設定。 |

### PDF頁籤 {#pdf-tab}

您可以選擇柵格化檔案、提取搜索詞和連結、設定解析度並選擇顏色空間。

| PDF選項 | 說明 |
| --- | --- |
| **[!UICONTROL 處理]** | · **[!UICONTROL 無]**  — 未處理PDF。<br>· **[!UICONTROL 縮略圖]**  — 將PDF檔案中的每頁翻頁，並將其轉換為縮略圖。<br> · **[!UICONTROL 光柵化]**  — 拆除PDF檔案中的頁面，並將向量圖形轉換為點陣圖影像。 要建立eCatalog，請選擇此選項。 |
| **[!UICONTROL 提取]** | · **[!UICONTROL 無]**  — 未從PDF中提取搜索詞或連結。<br>· **[!UICONTROL 搜索詞]**  — 從PDF檔案中提取搜索詞，以便在eCatalog Viewer中按關鍵字搜索檔案。<br>· **[!UICONTROL 連結]**  — 從PDF檔案中提取連結，並將其轉換為在eCatalog Viewer中使用的影像映射。<br>· **[!UICONTROL 搜索詞和連結]**  — 提取搜索詞和連結，以在eCatalog查看器中使用。 |
| **[!UICONTROL 解析度 (像素/英吋)]** | 確定解析度設定。 此設定確定PDF檔案中每英吋顯示的像素數。 預設值為150。 |
| **[!UICONTROL 顏色空間]** | · **[!UICONTROL 自動檢測]**  — 維護PDF檔案的顏色空間。<br>· **[!UICONTROL 強制為RGB]**  — 轉換為RGB顏色空間。<br>· **[!UICONTROL 強制為CMYK]**  — 轉換為CMYK顏色空間。<br>· **[!UICONTROL 強制為灰度]**  — 轉換為灰度色空間。 |

### Illustrator頁籤 {#illustrator-tab}

您可以柵格化Adobe Illustrator®檔案、維護透明背景、選擇解析度和選擇顏色空間。

您可以在AdobeDynamic Media使用Adobe®Illustrator®(AI)檔案。 Adobe·Dynamic Media提供了在上傳這些檔案時配置這些檔案的命令。

上載Illustrator(AI)影像檔案時，可以採用各種格式設定它們。 您可以柵格化檔案、維護透明背景、選擇解析度和選擇顏色空間。 在「上載作業選項」框的「上載」螢幕的「PostScript選項」和「Illustrator選項」下，可以使用PostScript和Illustrator檔案格式化選項。


| Illustrator選項 | 說明 |
| --- | --- |
| **[!UICONTROL 處理]** | 選擇「柵格化」(Rasterize)，將檔案中的向量圖形轉換為點陣圖格式。 |
| **[!UICONTROL 在演算後的影像中保留透明背景]** | 保留檔案的背景透明度。 |
| **[!UICONTROL 解析度 (像素/英吋)]** | 確定解析度設定。 此設定確定檔案中每英吋顯示的像素數。 |
| **[!UICONTROL 顏色空間]** | · **[!UICONTROL 自動檢測]**  — 保留檔案的顏色空間。<br>· **[!UICONTROL 強制為RGB]**  — 轉換為RGB顏色空間。<br>· **[!UICONTROL 強制為CMYK]**  — 轉換為CMYK顏色空間。<br>· **[!UICONTROL 強制為灰度]**  — 轉換為灰度色空間。 |
