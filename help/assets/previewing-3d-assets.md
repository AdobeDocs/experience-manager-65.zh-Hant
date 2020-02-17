---
title: 預覽3D資產
description: 瞭解如何預覽3D資產
contentOwner: Rick Brough
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# 預覽3D資產{#previewing-3d-assets}

Experience manager支援3D資產的上傳、傳送和互動式預覽，做為製作程式的一部分。

您可從AEM的資產詳細資訊頁面取得互動式3D檢視器。 檢視器除了其他功能外，還包含一系列互動式相機控制項，可讓您環繞、縮放和平移3D資產。

## 支援的3D預覽格式{#supported-3d-previewing-assets}

互動式3D預覽支援下列檔案格式：

| 3D副檔名 | 檔案格式 | MIME類型 | 附註 |
|---|---|---|---|
| GLB | 二進位GL傳輸 | 模型/gltf-binary |  |
| GLTF | GL傳輸格式 | model/gltf+json | 請參 **閱下** 「附註」。 |
| OBJ | WaveFront 3D物件檔案 | application/x-tgif |  |
| STL | 立體成形 | application/vnd.ms-pki.stl |  |
| DN | Adobe Dimension | model/x-adobe-dn | 僅支援擷取；預覽無法使用。 |
| USDZ | 通用場景描述Zip封存 | model/vnd.usdz+zip | 僅支援擷取；預覽無法使用。 |

**注意**:如果材料未在gLTF模型的預覽中渲染，請確保它們的命名正確，並且位於與模型相同的根資料夾中，類似 `textures` 於以下內容：

    Asset(folder)
    model.
    gltfmodel.
    bintextures(folder)
    material_0_baseColor.
    jpegmaterial_0_normal.jpeg

## 預覽3D資產時的效能考量{#performance-3d-previewing-assets}

在資產詳細資訊檢視頁面中開啟3D資產所花的時間，視頻寬、影像複雜性和伺服器延遲等因素而定。

此外，在您以互動方式操作相機時，用戶端電腦的功能（例如工作站、筆記型電腦或行動觸控裝置）也很重要。 功能相當強大的系統，具備良好的圖形功能，可讓互動式3D檢視體驗更順暢更有利。

**若要預覽3D資產**

1. 請確定您已將3D資產上傳至AEM。
請參 [閱3D預覽和上傳資產的](#supported-3d-previewing-assets)[支援格式](/help/assets/managing-assets-touch-ui.md#uploading-assets)。
1. 在AEM的「導覽」頁面 **[!UICONTROL 上]** ，點選「 **[!UICONTROL 資產>檔案」]**。

   ![導覽頁面](/help/assets/assets-dm/navigation-assets.png)

1. 在頁面的右上角，從「檢視」下拉式清單中，點選「卡片檢視」 ****，然後導覽至您要預覽的3D資產。

   ![3D卡片選擇](/help/assets/assets-dm/3d-card-select.png)
   _在「卡片檢視」中，點選您要預覽的3D資產卡片。_

1. 點選3D資產的資訊卡，以在資產詳細資訊檢視頁面中開啟它。

   ![互動式3D預覽](/help/assets/assets-dm/3d-preview.png)
   _在資產詳細資訊檢視頁面中互動式預覽3D資產。_
1. 在3D資產的資產詳細資料檢視頁面上，執行下列任一項作業：
   * **旋轉相機**-圍繞3D場景和物件環繞視圖。
      * _滑鼠_:左鍵按一下+拖曳。
      * _觸控螢幕_:單指按+拖曳。
   * **平移您的相機**—向左、向右、向上或向下平移您的檢視。
      * _滑鼠_:按一下滑鼠右鍵並拖曳。
      * _觸控螢幕_:雙指按住+拖曳。
   * **縮放相機**-縮放相機以移入和移出3D場景的區域。
      * _滑鼠_:滾輪。
      * _觸控螢幕_:雙指夾捏。
   * **重新輸入相機**-將相機重新輸入到3D場景中某個物件的某個點。
      * _滑鼠_:按兩下。
      * _觸控螢幕_:點兩下。
   * **重設**-靠近頁面的右下角，點選「重設」圖示，將檢視目標點還原至3D資產的中心。 Reset也會使攝影機更靠近或更遠，以便以合理的檢視大小顯示整個資產。
   * **全螢幕模式**-若要進入全螢幕模式，請在頁面的右下角點選全螢幕圖示。

1. 完成後，在頁面右上角附近點選「關 **[!UICONTROL 閉」]**。
