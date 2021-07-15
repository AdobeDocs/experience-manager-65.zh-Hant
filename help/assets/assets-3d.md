---
title: 在Dynamic Media中使用3D資產
seo-title: 在Dynamic Media中使用3D資產
description: 了解如何在Dynamic Media中使用3D資產
seo-description: 了解如何在Dynamic Media中使用3D資產
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
feature: 3D資產，資產管理
role: User, Admin
exl-id: 01c96f1e-c0e6-497d-bd7a-c0fd547a34da
source-git-commit: 471f9e99078a1e0af60024d439afd42ae77cba8c
workflow-type: tm+mt
source-wordcount: '2330'
ht-degree: 2%

---

# 在Dynamic Media中使用3D資產 {#working-with-three-d-assets-dm}

Dynamic Media可讓您上傳、管理、檢視及傳遞3D資產，盡享沈浸式體驗。

* 按一下發佈（使用工具列上的&#x200B;**[!UICONTROL 快速發佈]**）3D資產以產生URL。
* 使用Adobe Dimension提供的高品質互動式維度檢視器預設集，最佳化支援檢視3D資產。
* 3D Media WCM元件可讓您輕鬆將3D資產新增至Adobe Experience Manager Sites頁面。

在Dynamic Media中使用3D資產不需要額外設定。

![3d鞋](/help/assets/assets-dm/3d-dimensional-viewer-quickpublish-url-embed2.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Dynamic Media支援3D格式 {#supported-three-d-file-formats-in-dm}

Dynamic Media支援下列3D格式。

另請參閱[支援的3D格式](/help/assets/assets-formats.md)。

| 3D檔案副檔名 | 檔案格式 | MIME類型 | 附註 |
|---|---|---|---|
| GLB | 二進位GL傳輸 | 模型/gltf二進位 | 將材料和紋理作為單一資產包含。 |
| OBJ | WaveFront 3D對象檔案 | application/x-tgif |  |
| STL | 光固化成形 | application/vnd.ms-pki.stl |  |
| USDZ | 通用場景描述Zip封存 | model/vnd.usdz+zip | *僅支援擷取；沒有可用的檢視或互動。* USDZ是專屬的3D格式，可由Safari和iOS裝置原生檢視。 |

## 快速入門：Dynamic Media3D資產 {#quick-start-three-d}

下列逐步工作流程說明旨在協助您在Dynamic Media - Scene7模式中快速上手並執行3D資產。

>[!IMPORTANT]
>
>Dynamic Media — 混合模式不支援3D資產。

在Dynamic Media中處理3D資產之前，請確定您的Experience Manager管理員已在Dynamic Media - Scene7模式中啟用並設定Dynamic MediaCloud Services。

請參閱「設定Dynamic Media - Scene7模式」和「[疑難排解Dynamic Media - Scene7模式」中的「[設定Dynamic MediaCloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)」。](/help/assets/troubleshoot-dms7.md)

1. **上傳3D資產**

   * [上傳您的3D資產以用於Dynamic Media](/help/assets/manage-assets.md#uploading-assets)。
   * [支援的3D檔案格式，可在Dynamic Media中上傳](#supported-three-d-file-formats-in-dm)。

1. **管理3D資產**

   * 組織和搜尋3D資產

      * [組織數位資產](/help/assets/organize-assets.md#organize-digital-assets)。
      * [搜尋3D資產](/help/assets/search-assets.md)。
      * [使用自訂述詞來篩選搜尋結果](/help/assets/search-assets.md#custompredicates)。
   * 檢視3D資產

      * [檢視及與3D資產互動](#viewing-three-d-assets)。
      * [管理維度檢視器預設集](/help/assets/managing-viewer-presets.md)。
   * 使用3D資產中繼資料

      * [管理數位資產的中繼資料](/help/assets/metadata.md)。
      * [中繼資料結構](/help/assets/metadata-schemas.md)。



1. **發佈3D資產**

   * [發佈靜態Dynamic Media 3D資產](#publishing-three-d-assets)
   * [使用維度檢視器發佈Dynamic Media 3D資產的替代方法](#alternate-publish-methods)

## 關於檢視與與3D資產互動 {#viewing-three-d-assets}

本節說明如何以兩種不同的方式檢視及與3D資產互動：從資產詳細資訊頁面內和Sites的3D媒體元件內。

互動式3D檢視器除其他外，還包含一系列互動式相機控制項，可讓您環繞、縮放和平移3D資產。

在「資產詳細資料」頁面檢視中開啟3D資產所花的時間，取決於數個因素。 這些因素包括：

* 到伺服器的頻寬。
* 伺服器延遲
* 影像的複雜性。

此外，在交互操作攝像機時，客戶端電腦（如工作站、筆記型電腦或移動觸摸設備）的功能也很重要。 具有良好圖形功能的強大系統可讓互動式3D觀看體驗更流暢、更有利。

>[!TIP]
>
>您可以在檢視器預設集編輯器中開啟維度檢視器預設集，以練習導覽3D資產，而不需先上傳任何3D檔案。 「維度」檢視器預設集內建3D資產，供您互動。
>
>請參閱[管理檢視器預設集](/help/assets/managing-viewer-presets.md)。

## 從資產詳細資訊頁面檢視3D資產並與之互動 {#viewing-three-d-assets-from-asset-details-page}

另請參閱[使用軟體介面預覽資產](/help/assets/previewing-assets.md)。

**若要從資產詳細資訊頁面檢視3D資產並與之互動：**

1. 請確定您已將3D資產上傳至Experience Manager。

   請參閱[上傳您的3D資產以用於Dynamic Media](/help/assets/manage-assets.md#uploading-assets)。

1. 從Experience Manager，在&#x200B;**[!UICONTROL 導航]**&#x200B;頁上，轉至&#x200B;**[!UICONTROL 資產]** > **[!UICONTROL 檔案]**。
1. 在頁面的右上角附近，從&#x200B;**[!UICONTROL View]**&#x200B;下拉式清單中，選擇&#x200B;**[!UICONTROL Card View]**。
1. 導覽至您要檢視的3D資產。
1. 選取3D資產的卡片。
1. 在3D資產的詳細資訊檢視頁面上，執行下列任一操作：

   | 檢視 | 說明 | 滑鼠動作 | 觸控式螢幕動作 |
   | --- | --- | --- | --- |
   | **轉動你的相機** | 使檢視畫面在 3D 場景和物件周圍環繞 | 按一下左鍵+拖曳。 | 用單指按+拖動。 |
   | **平移您的相機** | 向左、向右、向上或向下平移視圖。 | 按一下右鍵+拖動。 | 用雙指按+拖。 |
   | **縮放您的相機** | 移入和移出3D場景中的區域。 | 滾輪。 | 雙指夾。 |
   | **重新輸入您的相機** | 將相機重新輸入到3D場景中某個對象上的某個點。 | 按兩下。 | 按兩下。 |
   | **重設** | 在頁面的右下角附近，選取「重設」圖示，將檢視目標點還原到3D資產的中央。 重置還使相機更近或更遠地移開，以便以合理的觀看大小顯示資產的整體。 |  |  |
   | **全螢幕模式** | 若要進入全螢幕模式，請在頁面的右下角，選取全螢幕圖示。 |  |  |

1. 在頁面的右上角，選取&#x200B;**[!UICONTROL Close]**&#x200B;以返回「資產」頁面。

## 在3D媒體元件內檢視3D資產並與之互動 {#interacting-with-asset-inside-three-d-media-component}

當網頁處於&#x200B;**[!UICONTROL Edit]**&#x200B;模式時，不能與3D資產進行互動。 若要讓資產互動式，您可以使用&#x200B;**[!UICONTROL 預覽]**&#x200B;功能，在頁面編輯器中檢視網頁，且可完整存取3D媒體元件的功能。

>[!IMPORTANT]
>
>只有在將3D媒體元件新增至網頁並將3D資產指派至元件後，才能完成此工作。 請參閱[將3D媒體元件添加到網頁](#adding-the-three-d-media-component-to-a-web-page)和[將3D資產分配給3D媒體元件](#assigning-a-three-d-asset-to-the-component)。

另請參閱[使用軟體介面預覽資產](/help/assets/previewing-assets.md)。

**若要在3D媒體元件內檢視3D資產並與之互動：**

1. 當網頁處於&#x200B;**[!UICONTROL Edit]**&#x200B;模式時，執行下列任一操作：

   * 在頁面的右上方附近，選擇&#x200B;**[!UICONTROL Preview]**&#x200B;以進入&#x200B;**[!UICONTROL Preview]**&#x200B;模式。
   * 從瀏覽器的頁面URL中刪除`/editor.html`。

完全互動的3D資產，如    ![顯示在3D媒體元件內的3D資](/help/assets/assets-dm/3d-asset-in-3d-media.png)
產：完全互動的3D資產，如預覽模 **** 式所示。

1. 在&#x200B;**[!UICONTROL 預覽]**&#x200B;模式中，執行下列任一操作：

   | 檢視 | 說明 | 滑鼠動作 | 觸控式螢幕動作 |
   | --- | --- | --- | --- |
   | **轉動你的相機** | 使檢視畫面在 3D 場景和物件周圍環繞 | 按一下左鍵+拖曳。 | 用單指按+拖動。 |
   | **平移您的相機** | 向左、向右、向上或向下平移視圖。 | 按一下右鍵+拖動。 | 用雙指按+拖。 |
   | **縮放您的相機** | 移入和移出3D場景中的區域。 | 滾輪。 | 雙指夾。 |
   | **重新輸入您的相機** | 將相機重新輸入到3D場景中某個對象上的某個點。 | 按兩下。 | 按兩下。 |
   | **重設** | 在頁面的右下角附近，選取「重設」圖示，將檢視目標點還原到3D資產的中央。 重置還使相機更近或更遠地移開，以便以合理的觀看大小顯示資產的整體。 |  |  |
   | **全螢幕模式** | 若要進入全螢幕模式，請在頁面的右下角，選取全螢幕圖示。 |  |  |

## 關於使用3D媒體元件 {#working-with-three-d-media-component}

Dynamic Media包含Dynamic Media 3D媒體元件，可在Adobe Experience Manager Sites中使用，以互動式檢視網頁上的3D模型。

* [將3D媒體元件新增至頁面範本](#adding-three-d-media-component-to-page-template)
* [將3D媒體元件新增至網頁](#adding-the-three-d-media-component-to-a-web-page)
   * [可選 — 配置3D介質元件](#configuring-the-three-d-component)
* [將3D資產分配給3D介質元件](#assigning-a-three-d-asset-to-the-component)

## 將3D媒體元件新增至頁面範本 {#adding-three-d-media-component-to-page-template}

1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 範本]**。
1. 導航到要在中啟用3D元件的頁面模板，然後選擇該模板。
1. 選擇&#x200B;**[!UICONTROL Edit]**&#x200B;以開啟模板。
1. 在頁面右上方附近，在下拉式選單中，選取&#x200B;**[!UICONTROL 結構]**&#x200B;模式（如果尚未啟用）。

   ![3d-media-component-structure](/help/assets/assets-dm/3d-media-component-structure.png)

1. 在&#x200B;**[!UICONTROL 佈局容器]**&#x200B;區域中選擇一個空區域，以便您選擇它並開啟它的關聯工具欄。
1. 在工具欄上，選擇&#x200B;**[!UICONTROL Policy]**&#x200B;表徵圖以開啟&#x200B;**[!UICONTROL Policy Editor]**。
1. 在&#x200B;**[!UICONTROL Properties]**&#x200B;區段中，在&#x200B;**[!UICONTROL Allowed Components]**&#x200B;標籤下，捲動至&#x200B;**[!UICONTROL Dynamic Media]**，然後展開清單並檢查&#x200B;**[!UICONTROL 3D Media]**。
1. 選擇&#x200B;**[!UICONTROL Done]**&#x200B;以保存更改並關閉&#x200B;**[!UICONTROL 策略編輯器]**。

   您現在可以將Dynamic Media 3D媒體元件放置在使用此範本的所有頁面上。

## 在網頁上新增3D媒體元件 {#adding-the-three-d-media-component-to-a-web-page}

如果您使用Experience Manager作為網頁內容管理系統，則可以通過3D媒體元件將3D資產添加到網頁。

另請參閱[在頁面上新增Dynamic Media資產](/help/assets/adding-dynamic-media-assets-to-pages.md)。

**要在網頁上添加3D介質元件：**

1. 開啟「Experience Manager網站」 ，然後選取您要新增Dynamic Media 3D媒體元件的網頁。
1. 選取&#x200B;**[!UICONTROL Edit]**（鉛筆）圖示，即可在頁面編輯器中開啟頁面。 請確定在頁面右上角附近選取了&#x200B;**[!UICONTROL Edit]**&#x200B;模式。

   ![3d-media-component-add](/help/assets/assets-dm/3d-media-component-edit.png)

1. 在工具欄上，選擇「側面板」表徵圖以切換或「開啟」面板的顯示。

1. 在側面板中，選擇加號表徵圖以開啟&#x200B;**[!UICONTROL 元件]**&#x200B;清單。

   ![3d-media-component-drag-drop](/help/assets/assets-dm/3d-assets-filter.png)

1. 將&#x200B;**[!UICONTROL 3D Media]**&#x200B;元件從&#x200B;**[!UICONTROL 元件]**&#x200B;清單拖曳至頁面上您希望3D檢視器顯示的位置。

您現在可以將3D資產指派給元件。

請參閱[將3D資產分配給3D媒體元件](#assigning-a-three-d-asset-to-the-component)。

### 可選 — 配置3D介質元件 {#configuring-the-three-d-component}

1. 在「Experience Manager網站」頁面編輯器中，選取您先前新增至頁面的&#x200B;**[!UICONTROL 3D媒體檢視器]**&#x200B;元件。
1. 選取「**[!UICONTROL 設定]**」圖示（扳手），以開啟元件設定對話方塊。

   ![3d-media-component-config](/help/assets/assets-dm/3d-media-component-config.png)

1. 在「3D媒體」對話框的「查看器預設」下拉清單中，選擇&#x200B;**[!UICONTROL Dimensional]**&#x200B;以將維查看器預設分配給元件。

   ![3d-media-component-edit-config](/help/assets/assets-dm/3d-media-component-edit-config.png)

1. 在右上角選取核取記號以儲存變更。

## 將3D資產分配給3D介質元件 {#assigning-a-three-d-asset-to-the-component}

將3D媒體元件新增至網頁後，您就可以指派3D資產給該頁面。

請參閱[將3D媒體元件新增至網頁](#adding-the-three-d-media-component-to-a-web-page)。

**要將3D資產分配給3D介質元件，請執行以下操作：**

1. 在「Experience Manager網站」頁面編輯器中，選取&#x200B;**[!UICONTROL Assets]**&#x200B;圖示，以在側面板中開啟&#x200B;**[!UICONTROL Assets]**。
1. 在下拉清單中，選擇&#x200B;**[!UICONTROL 3D]**&#x200B;以僅顯示3D資產檔案類型。
1. 在側面板中，搜索或滾動到要在正在編輯的頁面上查看的3D資產。
1. 從「資產」側面板拖曳3D資產，並將其拖曳至您先前新增至頁面的&#x200B;**[!UICONTROL 3D Media]**&#x200B;元件。

   ![將3D資產分配給3D介質元件](/help/assets/assets-dm/3d-asset-add.png)

>[!NOTE]
>
>當網頁處於「Experience Manager網站&#x200B;**[!UICONTROL 編輯]**」模式時，3D媒體元件會顯示3D資產，但無法與資產互動。 若要讓資產互動式，您可以使用&#x200B;**[!UICONTROL 預覽]**&#x200B;功能，在頁面編輯器中檢視網頁，且可完整存取3D媒體元件的功能。

## 發佈靜態Dynamic Media 3D資產 {#publishing-three-d-assets}

Dynamic Media接受Dynamic Media中支援作為&#x200B;*靜態內容*&#x200B;的各種3D檔案格式。 靜態內容表示您可以上傳和發佈3D資產，但不支援與3D資產相關聯的&#x200B;*變數影像*&#x200B;或影像重新整理。 原因在於Dynamic Media Imaging Server無法識別3D格式。 因此，在Dynamic Media中發佈3D資產後，您就可以複製即時URL。 3D資產的URL會遵循一般的Dynamic Media URL結構。 不過，您無法編輯資產URL中的任何參數，這與Dynamic Media中的傳統影像資產不同。

另請參閱[取得靜態資產的URL](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset)。

在&#x200B;**[!UICONTROL 卡片檢視]**&#x200B;中，資產名稱正下方及其日期與時間左側會顯示一個小型全球圖示，以指出資產已發佈。 在「清 **[!UICONTROL 單檢視]**」中，「已發佈」 **** 欄會指出已發佈或未發佈的資產。

如果您使用Experience Manager作為WCM，請使用此發佈方法直接在網頁上新增Dynamic Media 3D資產。

另請參閱[發佈Dynamic Media資產](publishing-dynamicmedia-assets.md)。

另請參閱[發佈頁面](/help/sites-authoring/publishing-pages.md)。

**若要發佈靜態Dynamic Media 3D資產：**

1. 開啟3D資產（GLB、OBJ或STL檔案格式），以便在資產詳細資訊頁面中查看。
1. 在工具欄上，選擇&#x200B;**[!UICONTROL 快速發佈]**。

   ![3d-asset-quick-publish](/help/assets/assets-dm/3d-asset-quick-publish.png)

1. 選擇&#x200B;**[!UICONTROL 關閉]**&#x200B;退出對話框並返回資產詳細資訊頁面。
1. 從3D資產檔案名稱左側的下拉式清單中，選擇&#x200B;**[!UICONTROL Renditions]**。

   ![3d-asset-renditions](/help/assets/assets-dm/3d-asset-renditions.png)

1. 選擇&#x200B;**[!UICONTROL original]**。 發佈3D資產（或「啟用」）時，如果符合下列所有3D資產條件，**[!UICONTROL URL]**&#x200B;按鈕就會出現在頁面左下角附近：
   * 3D資產是支援的格式（GLB、OBJ、STL和USDZ）。
   * 3D資產已擷取至Dynamic Media影像生產系統(IPS)。
   * 3D資產已發佈。

   ![3d-asset-url](/help/assets/assets-dm/3d-asset-url.png)

1. 選取&#x200B;**[!UICONTROL URL]** ，以便顯示3D資產的直接生產URL，您可以複製並在網頁上使用。

### 使用維度檢視器發佈Dynamic Media 3D資產的替代方法 {#alternate-publish-methods}

如果您&#x200B;*not*&#x200B;使用Experience Manager作為WCM，請使用下列兩種方法來發佈Dynamic Media 3D資產。

* **[!UICONTROL URL]**  — 如果您 **** 使用協力廠商網頁內容管理系統，而且您想要使用維度檢視器將Dynamic Media 3D資產連結至您的網頁，請使用URL。

   請參閱[將URL連結到您的Web應用程式](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset)。

* **[!UICONTROL 內嵌]**  — 當您 **** 想要使用維度檢視器檢視內嵌於網頁上的Dynamic Media 3D資產時，請使用內嵌。您可將內嵌代碼複製到剪貼簿，以便貼到網頁中。在&#x200B;**[!UICONTROL Embed]**&#x200B;對話方塊中不允許編輯代碼。

   請參閱將Dynamic Media視訊、影像檢視器或維度檢視器內嵌在網頁上](/help/assets/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page)。[
