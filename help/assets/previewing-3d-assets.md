---
title: 預覽3D資產
description: 瞭解如何在Experience Manager中預覽3D資產。
contentOwner: Rick Brough
docset: aem65
feature: 3D Assets
role: User
exl-id: fdebbc2b-c04d-4cdd-b7c2-8e9a2a854e79
source-git-commit: aa45839c53cb2c0715c9163847351aa2391309e0
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 7%

---

# 在Adobe Experience Manager預覽3D資產 {#previewing-3d-assets-aem}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/previewing-3d-assets.html?lang=en) |
| AEM 6.5 | 本文 |

Experience Manager支援作為創作流程一部分的3D資產的上載、交付和互動式預覽。

互動式3D查看器可從Experience Manager中的資產詳細資訊頁面獲得。 這個檢視器還包含一系列互動式相機控制項，可用來環繞、縮放和平移 3D 資產。

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/assets-3d.md). -->

## 支援的3D預覽格式(在Experience Manager中) {#supported-3d-previewing-assets}

Interactive 3D預覽支援以下檔案格式：

| 3D檔案副檔名 | 檔案格式 | MIME類型 | 附註 |
|---|---|---|---|
| 格爾布 | 二進位GL傳輸 | 模型/gltf二進位 |  |
| GLTF | GL傳輸格式 | 模型/gltf+json | 請參閱 **注釋** 下。 |
| OBJ | WaveFront 3D對象檔案 | 應用程式/x-tgif |  |
| STL | 光固化成形 | application/vnd.ms-pki.stl |  |
| DN | Adobe Dimension | 模型/x adobe-dn | 僅支援攝入；預覽不可用。 |
| 烏茲 | 通用場景描述Zip存檔 | model/vnd.usdz | 僅支援攝入；預覽不可用。 |

>[!NOTE]
>
>如果材料未在gLTF模型的預覽中呈現，請確保它們的命名正確且位於 `textures` 與模型位於同一根資料夾中的資料夾，與以下內容類似：

    資產（資料夾）
    模型.gltf
    model.bin
    紋理（資料夾）
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## 在Experience Manager中預覽3D資產時的效能注意事項{#performance-3d-previewing-assets}

在資產詳細資訊視圖頁中開啟3D資產所花的時間取決於幾個因素，如頻寬、映像複雜性和伺服器延遲。

此外，當您以交互方式操作攝像頭時，客戶機的功能（如工作站、筆記本或移動觸摸設備）也很重要。 具有良好圖形功能的功能相當強大的系統可讓互動式3D觀看體驗更加流暢和有利。

**要在Experience Manager中預覽3D資產：**

1. 確保已將3D資產上載到Experience Manager。
請參閱 [支援的3D預覽格式](#supported-3d-previewing-assets) 和 [上載資產](/help/assets/manage-assets.md#uploading-assets)。
1. 從Experience Manager，在 **[!UICONTROL 導航]** ，選擇 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**。

   ![導航頁](/help/assets/assets-dm/navigation-assets.png)

1. 在頁面右上角的「視圖」(View)下拉清單中，選擇 **[!UICONTROL 卡視圖]**，然後導航到要預覽的3D資產。

   ![3D卡選擇](/help/assets/assets-dm/3d-card-select.png)
   _在「卡視圖」中，選擇要預覽的3D資產的卡。_

1. 選擇3D資產的卡。

   ![互動式3D預覽](/help/assets/assets-dm/3d-preview.png)
   _在資產詳細資訊視圖頁中互動式預覽3D資產。_
1. 在3D資產的資產詳細資訊視圖頁面上，執行下列任一操作：

   | 檢視 | 說明 | 滑鼠操作 | 觸摸屏操作 |
   | --- | --- | --- | --- |
   | **轉你的相機** | 使檢視畫面在 3D 場景和物件周圍環繞 | 左鍵按一下並拖動。 | 單指按+拖動。 |
   | **開啟你的相機** | 將視圖向左、向右、向上或向下平移。 | 按一下右鍵並拖動。 | 雙指按+拖動。 |
   | **縮放相機** | 進出3D場景中的區域。 | 滾輪。 | 兩指捏。 |
   | **重新輸入相機** | 將相機重新輸入到3D場景中某個對象上的點。 | 按兩下。 | 按兩下。 |
   | **重設** | 在頁面右下角附近，選擇「重置」表徵圖將視圖目標點還原到3D資產的中心。 重置還使相機更近或更遠地移動，以便以合理的觀看大小顯示整個資產。 |  |  |
   | **全屏模式** | 要進入全屏模式，請在頁面右下角選擇全屏表徵圖。 |  |  |

1. 完成後，在頁面右上角附近，選擇 **[!UICONTROL 關閉]**。
