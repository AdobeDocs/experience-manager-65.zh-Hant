---
title: 預覽 3D 資產
description: 瞭解如何在Experience Manager中預覽3D資產。
contentOwner: Rick Brough
docset: aem65
feature: 3D Assets
role: User
exl-id: fdebbc2b-c04d-4cdd-b7c2-8e9a2a854e79
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: bca6156727dca11b2e09be549f3def6130827193
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 8%

---

# 在Adobe Experience Manager中預覽3D資產 {#previewing-3d-assets-aem}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/previewing-3d-assets.html?lang=en) |
| AEM 6.5 | 本文章 |

Experience Manager支援3D資產的製作程式功能，包括上傳、傳送和互動式預覽。

您可從Experience Manager的資產詳細資訊頁面取得互動式3D檢視器。 這個檢視器還包含一系列互動式相機控制項，可用來環繞、縮放和平移 3D 資產。

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/assets-3d.md). -->

## Experience Manager中支援的3D預覽格式 {#supported-3d-previewing-assets}

互動式3D預覽支援下列檔案格式：

| 3D副檔名 | 檔案格式 | MIME型別 | 備註 |
|---|---|---|---|
| GLB | 二進位GL傳輸 | model/gltf-binary | |
| GLTF | 總帳傳輸格式 | model/gltf+json | 請參閱下方的&#x200B;**附註**。 |
| 物件 | WaveFront 3D物件檔案 | application/x-tgif | |
| STL | 立體成型 | application/vnd.ms-pki.stl | |
| DN | Adobe Dimension | model/x-adobe-dn | Support for ingestion only; preview not available. |
| USDZ | Universal Scene Description Zip archive | model/vnd.usdz+zip | Support for ingestion only; preview not available. |

>[!NOTE]
>
>If materials do not render in preview of a gLTF model, make sure they are named properly and in a `textures` folder in the same root folder as the model, similar to the following:

    Asset (folder)
    model.gltf
    model.bin
    textures (folder)
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## Performance considerations when you preview 3D assets in Experience Manager{#performance-3d-previewing-assets}

The time it takes to open a 3D asset in the asset details view page depends on several factors such things as bandwidth, image complexity, and latencies to the server.

In addition, the capabilities of the client computer – such as a workstation, notebook, or mobile touch device – are also important to consider when you manipulate the camera interactively. A reasonably powerful system with good graphics capabilities can make the interactive 3D viewing experience smoother and more favorable.

**To preview 3D assets in Experience Manager:**

1. Make sure you have uploaded 3D assets into Experience Manager.
See [Supported formats for 3D preview](#supported-3d-previewing-assets) and [Upload Assets](/help/assets/manage-assets.md#uploading-assets).
1. From Experience Manager, on the **[!UICONTROL Navigation]** page, select **[!UICONTROL Assets]** > **[!UICONTROL Files]**.

   ![Navigation page](/help/assets/assets-dm/navigation-assets.png)

1. Near the upper-right corner of the page, from the View drop-down list, select **[!UICONTROL Card View]**, then navigate to a 3D asset that you want to preview.

   ![3D card select](/help/assets/assets-dm/3d-card-select.png)
   _In Card View, select the card of the 3D asset you want to preview._

1. Select the card of the 3D asset.

   ![Interactive 3D preview](/help/assets/assets-dm/3d-preview.png)
   _Interactive preview of a 3D asset in the asset details view page._
1. On the asset details view page for the 3D asset, do any of the following:

   | 檢視 | 說明 | Mouse action | Touch screen action |
   | --- | --- | --- | --- |
   | **轉動相機** | 使檢視畫面在 3D 場景和物件周圍環繞 | 按一下左鍵+拖曳。 | 單指按下+拖曳。 |
   | **平移相機** | 向左、向右、向上或向下平移檢視。 | 按一下滑鼠右鍵+拖曳。 | 雙指按下+拖曳。 |
   | **縮放相機** | 在3D場景中移入和移出區域。 | 滾輪。 | 兩指捏合。 |
   | **重新將相機置中** | 將相機重新置中至3D場景中物件上的某個點。 | 按兩下。 | 連按兩下。 |
   | **重設** | 在頁面的右下角附近，選取「重設」圖示，將檢視目標點恢復到3D資產的中心。 重設也會將相機移到更近或更遠的位置，以合理的檢視大小完整顯示資產。 |   |   |
   | **全熒幕模式** | 若要進入全熒幕模式，請在頁面的右下角選取「全熒幕」圖示。 |   |   |

1. 完成後，在頁面的右上角附近，選取&#x200B;**[!UICONTROL 關閉]**。
