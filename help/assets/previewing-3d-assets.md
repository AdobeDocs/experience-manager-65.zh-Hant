---
title: 預覽3D資產
description: 了解如何以Experience Manager預覽3D資產。
contentOwner: Rick Brough
docset: aem65
feature: 3D Assets
role: User
exl-id: fdebbc2b-c04d-4cdd-b7c2-8e9a2a854e79
source-git-commit: 32e637463a2f68a48b39c5dea9cc3cc4d1596d9b
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 6%

---

# 在Adobe Experience Manager中預覽3D資產 {#previewing-3d-assets-aem}

Experience Manager在製作程式中支援3D資產的上傳、傳送和互動式預覽。

互動式3D檢視器可從Experience Manager中的資產詳細資訊頁面取得。 這個檢視器還包含一系列互動式相機控制項，可用來環繞、縮放和平移 3D 資產。

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/assets-3d.md). -->

## 支援的格式，可在Experience Manager中預覽3D {#supported-3d-previewing-assets}

互動式3D預覽支援下列檔案格式：

| 3D檔案副檔名 | 檔案格式 | MIME類型 | 附註 |
|---|---|---|---|
| GLB | 二進位GL傳輸 | 模型/gltf二進位 |  |
| GLTF | GL傳輸格式 | model/gltf+json | 請參閱 **附註** 下方。 |
| OBJ | WaveFront 3D對象檔案 | application/x-tgif |  |
| STL | 光固化成形 | application/vnd.ms-pki.stl |  |
| DN | Adobe Dimension | model/x-adobe-dn | 僅支援擷取；預覽不可用。 |
| USDZ | 通用場景描述Zip封存 | model/vnd.usdz+zip | 僅支援擷取；預覽不可用。 |

>[!NOTE]
>
>如果材料未在gLTF模型的預覽中呈現，請確保它們的名稱正確且在 `textures` 與模型相同的根資料夾中的資料夾，類似於以下內容：

    資產（資料夾）
    model.gltf
    model.bin
    紋理（資料夾）
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## 以Experience Manager預覽3D資產時的效能考量{#performance-3d-previewing-assets}

在資產詳細資訊檢視頁面中開啟3D資產所花的時間，取決於頻寬、影像複雜度和伺服器延遲等數項因素。

此外，當您以交互方式操作攝像機時，還需要考慮客戶端電腦的功能，如工作站、筆記型電腦或移動觸摸設備。 具有良好圖形功能的強大系統可讓互動式3D觀看體驗更流暢、更有利。

**若要預覽3D資產的Experience Manager:**

1. 請確定您已將3D資產上傳至Experience Manager。
請參閱 [支援的3D預覽格式](#supported-3d-previewing-assets) 和 [上傳資產](/help/assets/manage-assets.md#uploading-assets).
1. 從Experience Manager，在 **[!UICONTROL 導覽]** 頁面，選取 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.

   ![導覽頁面](/help/assets/assets-dm/navigation-assets.png)

1. 在頁面的右上角附近，從「檢視」下拉式清單中，選取 **[!UICONTROL 卡片檢視]**，然後導覽至您要預覽的3D資產。

   ![3D卡選擇](/help/assets/assets-dm/3d-card-select.png)
   _在「卡片檢視」中，選取您要預覽之3D資產的卡片。_

1. 選取3D資產的卡片。

   ![互動式3D預覽](/help/assets/assets-dm/3d-preview.png)
   _在資產詳細資訊檢視頁面中互動式預覽3D資產。_
1. 在3D資產的資產詳細資訊檢視頁面上，執行下列任一操作：

   | 檢視 | 說明 | 滑鼠動作 | 觸控式螢幕動作 |
   | --- | --- | --- | --- |
   | **轉動你的相機** | 使檢視畫面在 3D 場景和物件周圍環繞 | 按一下左鍵+拖曳。 | 用單指按+拖動。 |
   | **平移您的相機** | 向左、向右、向上或向下平移視圖。 | 按一下右鍵+拖動。 | 用雙指按+拖。 |
   | **縮放您的相機** | 移入和移出3D場景中的區域。 | 滾輪。 | 雙指夾。 |
   | **重新輸入您的相機** | 將相機重新輸入到3D場景中某個對象上的某個點。 | 按兩下。 | 按兩下。 |
   | **重設** | 在頁面的右下角附近，選取「重設」圖示，將檢視目標點還原到3D資產的中央。 重置還使相機更近或更遠地移開，以便以合理的觀看大小顯示資產的整體。 |  |  |
   | **全螢幕模式** | 若要進入全螢幕模式，請在頁面的右下角，選取全螢幕圖示。 |  |  |

1. 完成後，在頁面右上角附近選取 **[!UICONTROL 關閉]**.
