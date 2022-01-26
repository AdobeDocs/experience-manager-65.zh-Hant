---
title: 在Dynamic Media處理3D資產
description: 瞭解如何在Dynamic Media使用3D資產
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
feature: 3D Assets,Asset Management
role: User, Admin
exl-id: 01c96f1e-c0e6-497d-bd7a-c0fd547a34da
source-git-commit: a13d6d10dd10605d2cb83a8622fae3a7e2590c93
workflow-type: tm+mt
source-wordcount: '2317'
ht-degree: 2%

---

# 在Dynamic Media處理3D資產 {#working-with-three-d-assets-dm}

Dynamic Media讓您將3D資產作為沈浸式體驗進行上傳、管理、查看和交付。

* 按一下發佈(使用 **[!UICONTROL 快速發佈]** 的子菜單。
* 優化支援，使用由Adobe Dimension提供支援的高質量互動式Dimension查看器來查看3D資產。
* 3D Media WCM元件使您能夠輕鬆地將3D資產添加到您的Adobe Experience Manager Sites頁面。

在Dynamic Media，使用3D資產不需要額外配置。

![三維鞋](/help/assets/assets-dm/3d-dimensional-viewer-quickpublish-url-embed2.png) *三維鞋的詳細資訊頁面。*

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## 3D格式在Dynamic Media支援 {#supported-three-d-file-formats-in-dm}

Dynamic Media支援以下3D格式。

另請參閱 [支援的3D格式](/help/assets/assets-formats.md)。

| 3D檔案副檔名 | 檔案格式 | MIME類型 | 附註 |
|---|---|---|---|
| 格爾布 | 二進位GL傳輸 | 模型/gltf二進位 | 將材料和紋理作為單個資源包括在內。 |
| OBJ | WaveFront 3D對象檔案 | 應用程式/x-tgif |  |
| STL | 光固化成形 | application/vnd.ms-pki.stl |  |
| 烏茲 | 通用場景描述Zip存檔 | model/vnd.usdz | *僅支援攝入；沒有可用的查看或交互。* USDZ是一種專有的3D格式，Safari和iOS設備可以本機查看。 |

<!-- >[!NOTE]
>
>The 3D Media WCM component and 3D preview on an asset's Details page is not compatible with the latest version of Chrome (97.x). Instead, to work with 3D assets, use Firefox or Safari, or use an earlier version of Chrome (96.x). -->

## 快速啟動：Dynamic Media3D資產 {#quick-start-three-d}

以下逐步工作流說明旨在幫助您在Dynamic Media-Scene7模式下快速啟動和運行3D資產。

>[!IMPORTANT]
>
>3D資產在Dynamic Media — 混合模式中不受支援。

在您處理Dynamic Media的3D資產之前，請確保您的Experience Manager管理員已在Dynamic Media-Scene7模式下啟用並配置了Dynamic MediaCloud Services。

請參閱 [配置EDynamic MediaCloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) 配置Dynamic Media-Scene7模式和 [診斷Dynamic Media-Scene7模式](/help/assets/troubleshoot-dms7.md)。

1. **上載3D資產**

   * [上傳3D資產供Dynamic Media使用](/help/assets/manage-assets.md#uploading-assets)。
   * [支援的3D檔案格式，可在Dynamic Media上傳](#supported-three-d-file-formats-in-dm)。

1. **管理3D資產**

   * 組織和搜索3D資產

      * [組織數字資產](/help/assets/organize-assets.md#organize-digital-assets)。
      * [搜索3D資產](/help/assets/search-assets.md)。
      * [使用自定義謂語篩選搜索結果](/help/assets/search-assets.md#custompredicates)。
   * 查看3D資產

      * [查看3D資產並與其交互](#viewing-three-d-assets)。
      * [管理維查看器預設](/help/assets/managing-viewer-presets.md)。
   * 使用3D資產元資料

      * [管理數字資產的元資料](/help/assets/metadata.md)。
      * [元資料架構](/help/assets/metadata-schemas.md)。



1. **發佈3D資產**

   * [發佈靜態Dynamic Media3D資產](#publishing-three-d-assets)
   * [使用Dimensional查看器發佈Dynamic Media3D資產的替代方法](#alternate-publish-methods)

## 關於查看和與3D資產交互 {#viewing-three-d-assets}

本節介紹如何查看和與3D資產交互的兩種不同方式：從資產詳細資訊頁面和Experience Manager Sites的3D介質元件中。

互動式3D查看器除其它外還包括一組互動式攝像機控制項，它使您能夠對3D資產進行軌道、縮放和平移。

在「資產詳細資訊」頁視圖中開啟3D資產所花的時間取決於幾個因素。 這些因素包括：

* 伺服器頻寬。
* 伺服器延遲
* 影像的複雜性。

此外，當您以交互方式操作攝像頭時，客戶機（如工作站、筆記本或移動觸摸設備）的功能也很重要。 具有良好圖形功能的功能相當強大的系統可讓互動式3D觀看體驗更加流暢和有利。

>[!TIP]
>
>您可以在查看器預設編輯器中開啟維查看器預設，以練習在3D資產中導航，而無需先上載任何3D檔案。 「維」查看器預設有一個內置的3D資源，供您與其交互。
>
>請參閱 [管理查看器預設](/help/assets/managing-viewer-presets.md)。

## 從資產詳細資訊頁面查看3D資產並與其交互 {#viewing-three-d-assets-from-asset-details-page}

另請參閱 [使用軟體介面預覽資產](/help/assets/previewing-assets.md)。

**要從資產詳細資訊頁面查看3D資產並與其交互，請執行以下操作：**

1. 確保已將3D資產上載到Experience Manager。

   請參閱 [上傳3D資產供Dynamic Media使用](/help/assets/manage-assets.md#uploading-assets)。

1. 從Experience Manager，在 **[!UICONTROL 導航]** 頁面，轉到 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**。
1. 在頁面右上角，從 **[!UICONTROL 視圖]** 下拉清單，選擇 **[!UICONTROL 卡視圖]**。
1. 定位至要查看的3D資產。
1. 選擇3D資產的卡。
1. 在3D資產的詳細資訊視圖頁面上，執行下列任一操作：

   | 檢視 | 說明 | 滑鼠操作 | 觸摸屏操作 |
   | --- | --- | --- | --- |
   | **轉你的相機** | 使檢視畫面在 3D 場景和物件周圍環繞 | 左鍵按一下並拖動。 | 單指按+拖動。 |
   | **開啟你的相機** | 將視圖向左、向右、向上或向下平移。 | 按一下右鍵並拖動。 | 雙指按+拖動。 |
   | **縮放相機** | 進出3D場景中的區域。 | 滾輪。 | 兩指捏。 |
   | **重新輸入相機** | 將相機重新輸入到3D場景中某個對象上的點。 | 按兩下。 | 按兩下。 |
   | **重設** | 在頁面右下角附近，選擇「重置」表徵圖將視圖目標點還原到3D資產的中心。 重置還使相機更近或更遠地移動，以便以合理的觀看大小顯示整個資產。 |  |  |
   | **全屏模式** | 要進入全屏模式，請在頁面右下角選擇全屏表徵圖。 |  |  |

1. 在頁面的右上角，選擇 **[!UICONTROL 關閉]** 頁面。

## 查看3D介質元件內的3D資產並與其交互 {#interacting-with-asset-inside-three-d-media-component}

當網頁在 **[!UICONTROL 編輯]** 模式，不能與3D資產進行交互。 要使資產具有交互性，可以使用 **[!UICONTROL 預覽]** 功能，可在頁面編輯器中查看完全訪問3D媒體元件功能的網頁。

>[!IMPORTANT]
>
>只有在將3D媒體元件添加到網頁並將3D資產分配給該元件後，才能完成此任務。 請參閱 [將3D媒體元件添加到網頁](#adding-the-three-d-media-component-to-a-web-page) 和 [將3D資產分配給3D介質元件](#assigning-a-three-d-asset-to-the-component)。

另請參閱 [使用軟體介面預覽資產](/help/assets/previewing-assets.md)。

**要查看3D介質元件內的3D資產並與其交互：**

1. 當網頁在 **[!UICONTROL 編輯]** 模式，執行以下任一操作：

   * 在頁面右上角，選擇 **[!UICONTROL 預覽]** 輸入 **[!UICONTROL 預覽]** 的子菜單。
   * 刪除 `/editor.html` 的子菜單。

全互動式3D資產，如所示    ![3D介質元件內顯示的3D資產](/help/assets/assets-dm/3d-asset-in-3d-media.png)
全互動式3D資產，如所示 **[!UICONTROL 預覽]** 的子菜單。

1. 在 **[!UICONTROL 預覽]** 模式，執行下列任一操作：

   | 檢視 | 說明 | 滑鼠操作 | 觸摸屏操作 |
   | --- | --- | --- | --- |
   | **轉你的相機** | 使檢視畫面在 3D 場景和物件周圍環繞 | 左鍵按一下並拖動。 | 單指按+拖動。 |
   | **開啟你的相機** | 將視圖向左、向右、向上或向下平移。 | 按一下右鍵並拖動。 | 雙指按+拖動。 |
   | **縮放相機** | 進出3D場景中的區域。 | 滾輪。 | 兩指捏。 |
   | **重新輸入相機** | 將相機重新輸入到3D場景中某個對象上的點。 | 按兩下。 | 按兩下。 |
   | **重設** | 在頁面右下角附近，選擇「重置」表徵圖將視圖目標點還原到3D資產的中心。 重置還使相機更近或更遠地移動，以便以合理的觀看大小顯示整個資產。 |  |  |
   | **全屏模式** | 要進入全屏模式，請在頁面右下角選擇全屏表徵圖。 |  |  |

## 關於使用3D介質元件 {#working-with-three-d-media-component}

Dynamic Media包含Dynamic Media3D媒體元件，您可以在Adobe Experience Manager Sites使用該元件，以在網頁上互動式查看3D模型。

* [將3D介質元件添加到頁面模板](#adding-three-d-media-component-to-page-template)
* [將3D媒體元件添加到網頁](#adding-the-three-d-media-component-to-a-web-page)
   * [可選 — 配置3D介質元件](#configuring-the-three-d-component)
* [將3D資產分配給3D介質元件](#assigning-a-three-d-asset-to-the-component)

## 將3D介質元件添加到頁面模板 {#adding-three-d-media-component-to-page-template}

1. 導航到 **[!UICONTROL 工具]** > **[!UICONTROL 常規]** > **[!UICONTROL 模板]**。
1. 導航到要在中啟用3D元件的頁面模板並選擇該模板。
1. 選擇 **[!UICONTROL 編輯]** 以便開啟模板。
1. 在頁面右上角的下拉菜單中，選擇 **[!UICONTROL 結構]** 的子菜單。

   ![三維介質構件結構](/help/assets/assets-dm/3d-media-component-structure.png)

1. 在 **[!UICONTROL 佈局容器]** 的子菜單。
1. 在工具欄上，選擇 **[!UICONTROL 策略]** 表徵圖以開啟 **[!UICONTROL 策略編輯器]**。
1. 在 **[!UICONTROL 屬性]** 的 **[!UICONTROL 允許的元件]** 頁籤，滾動到 **[!UICONTROL Dynamic Media]**，然後展開清單並檢查 **[!UICONTROL 3D介質]**。
1. 選擇 **[!UICONTROL 完成]** 保存更改並關閉 **[!UICONTROL 策略編輯器]**。

   現在，您可以將Dynamic Media3D媒體元件放置在使用此模板的所有頁面上。

## 在網頁上添加3D媒體元件 {#adding-the-three-d-media-component-to-a-web-page}

如果將Experience Manager用作Web內容管理系統，則可以通過3D媒體元件將3D資產添加到網頁。

另請參閱 [將Dynamic Media資產添加到頁面](/help/assets/adding-dynamic-media-assets-to-pages.md)。

**要在網頁上添加3D媒體元件：**

1. 開啟Experience Manager Sites並選擇要向其中添加Dynamic Media3D媒體元件的網頁。
1. 選擇 **[!UICONTROL 編輯]** （鉛筆）表徵圖，以便您可以將頁面開啟到頁面編輯器中。 確保 **[!UICONTROL 編輯]** 在頁面的右上角處選擇模式。

   ![3d-media-component-add](/help/assets/assets-dm/3d-media-component-edit.png)

1. 在工具欄上，選擇「側面板」表徵圖以切換或「開啟」面板的顯示。

1. 在側面板中，選擇加號表徵圖以開啟 **[!UICONTROL 元件]** 清單框。

   ![三維介質元件 — 拖放](/help/assets/assets-dm/3d-assets-filter.png)

1. 拖動 **[!UICONTROL 3D介質]** 元件 **[!UICONTROL 元件]** 清單到要顯示3D查看器的頁面上的位置。

現在，您已準備好將3D資產分配給元件。

請參閱 [將3D資產分配給3D介質元件](#assigning-a-three-d-asset-to-the-component)。

### 可選 — 配置3D介質元件 {#configuring-the-three-d-component}

1. 在Experience Manager Sites頁面編輯器中，選擇 **[!UICONTROL 3D媒體查看器]** 添加到頁面的元件。
1. 選擇 **[!UICONTROL 配置]** 表徵圖（扳手），以便開啟「元件配置」(component configuration)對話框。

   ![3d-media-component-config](/help/assets/assets-dm/3d-media-component-config.png)

1. 在「3D媒體」對話框中，從「查看器預設」下拉清單中，選擇 **[!UICONTROL 維]** 將「維」查看器預設指定給元件。

   ![3d-media-component-edit-config](/help/assets/assets-dm/3d-media-component-edit-config.png)

1. 在右上角，選擇複選標籤以保存更改。

## 將3D資產分配給3D介質元件 {#assigning-a-three-d-asset-to-the-component}

在將3D媒體元件添加到網頁後，可以為其分配3D資源。

請參閱 [將3D媒體元件添加到網頁](#adding-the-three-d-media-component-to-a-web-page)。

**要將3D資產分配給3D介質元件：**

1. 在Experience Manager Sites頁面編輯器中，選擇 **[!UICONTROL 資產]** 開啟 **[!UICONTROL 資產]** 的下界。
1. 在下拉清單中，選擇 **[!UICONTROL 3D]** 只顯示3D資產檔案類型。
1. 在側面板中，搜索或滾動到要在編輯的頁面上查看的3D資產。
1. 將3D資產從「資產」側面板拖放到 **[!UICONTROL 3D介質]** 添加到頁面的元件。

   ![將3D資產分配給3D介質元件](/help/assets/assets-dm/3d-asset-add.png)

>[!NOTE]
>
>網頁在Experience Manager Sites **[!UICONTROL 編輯]** 模式下，3D介質元件將顯示3D資產，但不可能與資產進行交互。 要使資產具有交互性，可以使用 **[!UICONTROL 預覽]** 功能，可在頁面編輯器中查看完全訪問3D媒體元件功能的網頁。

## 發佈靜態Dynamic Media3D資產 {#publishing-three-d-assets}

Dynamic Media接受支援的各種3D檔案格式 *靜態內容* 在Dynamic Media。 靜態內容意味著您可以上傳和發佈3D資產，但不支援 *可變成像* 或與3D資產關聯的影像重新編寫。 原因是Dynamic Media映像伺服器無法識別3D格式。 因此，在Dynamic Media發佈3D資產後，您可以複製一個即時URL。 3D資產的URL遵循通常的Dynamic MediaURL結構。 但是，與Dynamic Media的傳統影像資產不同，您無法編輯資產URL中的任何參數。

另請參閱 [獲取靜態資產的URL](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset)。

在 **[!UICONTROL 卡視圖]**，一個小型全球表徵圖將出現在資產名稱的正下方，並顯示在其日期和時間的左側，以指示資產已發佈。 在「清 **[!UICONTROL 單檢視]**」中，「已發佈」 **** 欄會指出已發佈或未發佈的資產。

如果您使用Experience Manager作為WCM，請使用此發佈方法將Dynamic Media3D資產直接添加到您的網頁上。

另請參閱 [發佈Dynamic Media資產](publishing-dynamicmedia-assets.md)。

另請參閱 [發佈頁面](/help/sites-authoring/publishing-pages.md)。

**要發佈靜態Dynamic Media3D資產，請執行以下操作：**

1. 開啟3D資產（GLB、OBJ或STL檔案格式），以便可以在資產詳細資訊頁面中查看它。
1. 在工具欄上，選擇 **[!UICONTROL 快速發佈]**。

   ![3d資產快速發佈](/help/assets/assets-dm/3d-asset-quick-publish.png)

1. 選擇 **[!UICONTROL 關閉]** 對話框並返回資產詳細資訊頁面。
1. 從3D資產檔案名左側的下拉清單中，選擇 **[!UICONTROL 格式副本]**。

   ![3d資產格式副本](/help/assets/assets-dm/3d-asset-renditions.png)

1. 選擇 **[!UICONTROL 原始]**。 當3D資產發佈（或「激活」）時， **[!UICONTROL URL]** 頁籤頁面的下方。
   * 3D資產是支援的格式（GLB、OBJ、STL和USDZ）。
   * 3D資產已被攝入Dynamic Media影像製作系統(IPS)。
   * 3D資產已發佈。

   ![3d資產URL](/help/assets/assets-dm/3d-asset-url.png)

1. 選擇 **[!UICONTROL URL]** 因此，您可以顯示3D資產的直接生產URL，您可以在網頁上複製和使用該URL。

### 使用Dimensional查看器發佈Dynamic Media3D資產的替代方法 {#alternate-publish-methods}

如果執行以下操作，請使用以下兩種方法發佈Dynamic Media3D資產 *不* 使用Experience Manager作為WCM。

* **[!UICONTROL URL]**  — 使用 **[!UICONTROL URL]** 如果您使用的是第三方Web內容管理系統，並且希望使用Dimensional查看器將Dynamic Media3D資產連結到您的網頁。

   請參閱 [將URL連結到Web應用程式](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset)。

* **[!UICONTROL 嵌入]**  — 使用 **[!UICONTROL 嵌入]** 當您希望使用Dimensional查看器查看嵌入在網頁上的Dynamic Media3D資產時。 您可將內嵌代碼複製到剪貼簿，以便貼到網頁中。不允許在 **[!UICONTROL 嵌入]** 對話框。

   請參閱 [將Dynamic Media視頻、影像查看器或維查看器嵌入網頁](/help/assets/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page)。
