---
title: 適用於社群的FFmpeg
seo-title: 適用於社群的FFmpeg
description: 如何安裝和設定適用於社群的FFmpeg
seo-description: 如何安裝和設定適用於社群的FFmpeg
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 適用於社群的FFmpeg {#ffmpeg-for-communities}

## 概覽 {#overview}

FFmpeg是轉換和串流音訊和視訊的解決方案，在安裝時，會用來正確轉碼視訊資 [產](../../help/sites-authoring/default-components-foundation.md#video) ，以及AEM Communities的啟用功能。

在作者環境中使用FFmpeg來獲取上傳的啟用資源的元資料，並在列出啟用資源時生成要顯示的縮略圖。

## 安裝FFmpeg {#installing-ffmpeg}

FFmpeg應安裝在代管AEM作者例 *項* 的伺服器上。

1. 前往 [https://www.ffmpeg.org](https://www.ffmpeg.org/)
1. 下載適用於您特定環境（Macintosh、Windows或Linux）的最新版FFmpeg

   * 由於舊版軟體中的安全性弱點，請務必保持FFmpeg最新狀態

1. 依照作業系統的指示安裝Fmpeg。

1. 請確定FFmpeg可執行檔已設定在您的系統路徑中。

   您應該能夠從系統中的任何目錄運行FFmpeg。

   * 例如， `ffmpeg -version`

## 設定FFmpeg轉碼服務 {#configure-ffmpeg-transcoding-service}

依預設，當安裝FFmpeg時，會根據DAM更新資產工作流程定義設定多個轉譯（轉碼）。

由於轉碼需要CPU資源，因此建議修改目標轉譯的清單。 在大多數情況下，不需要轉碼。

若要修改DAM更新資產工作流程，以及在此範例中，若要關閉轉碼：

* 以管理權限登入作者例項
* 從全域導覽：「工 **[!UICONTROL 具>工作流>模型」]**
* 尋找 **[!UICONTROL DAM更新資產]**
* 連按兩下以開啟Classic UI中要編輯的工作流程

   結果位置： [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* 連按兩下 **[!UICONTROL FFmpeg轉碼步驟]** ，以存取「步驟屬性」對話方塊
* 在「流程 **[!UICONTROL 」(Process]** )頁籤下：

   * **[!UICONTROL 圖]**:清除所有條目以禁用轉碼預設值： `profile:firefoxhq,profile:hq,profile:flv,profile:iehq`

![chlimage_1-372](assets/chlimage_1-372.png)

* 選擇「 **[!UICONTROL 確定]** 」以關閉對 `Step Properties` 話框

* 選擇「 **[!UICONTROL 保存]** 」以保存工作 `DAM Update Asset` 流

   （左上角）

