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
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---


# 適用於社群的FFmpeg {#ffmpeg-for-communities}

## 概覽 {#overview}

FFmpeg是轉換和串流音訊和視訊的解決方案，在安裝時，會用於適當轉碼[視訊資產](../../help/sites-authoring/default-components-foundation.md#video)以及AEM Communities的啟用功能。

在作者環境中使用FFmpeg來獲取上傳的啟用資源的元資料，並在列出啟用資源時生成要顯示的縮略圖。

## 安裝FFmpeg {#installing-ffmpeg}

FFmpeg應安裝在代管AEM *author*&#x200B;實例的伺服器上。

1. 前往[https://www.ffmpeg.org](https://www.ffmpeg.org/)。
1. 下載適用於您特定環境（Macintosh、Windows或Linux）的最新版FFmpeg。

   * 由於舊版軟體中的安全性弱點，因此請務必保持FFmpeg的最新狀態。

1. 依照作業系統的指示安裝Fmpeg。

1. 請確定FFmpeg可執行檔已設定在您的系統路徑中。

   您應該能夠從系統中的任何目錄運行FFmpeg。

   * 例如，`ffmpeg -version`。

## 配置FFmpeg轉碼服務{#configure-ffmpeg-transcoding-service}

依預設，當安裝FFmpeg時，會根據[!UICONTROL DAM更新資產]工作流程定義設定多個轉譯（轉碼）。

由於轉碼需要CPU資源，因此建議修改目標轉譯的清單。 在大多數情況下，不需要轉碼。

要修改[!UICONTROL DAM更新資產]工作流，在此示例中，要關閉轉碼：

* 以管理權限登入作者例項。
* 從全域導覽，導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**。
* 找到&#x200B;**[!UICONTROL DAM Update Asset]**。
* 連按兩下以開啟Classic UI中要編輯的工作流程。

   結果位置：[http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* 連按兩下&#x200B;**[!UICONTROL FFmpeg codecing]**&#x200B;步驟，以存取「步驟屬性」對話方塊。
* 在&#x200B;**[!UICONTROL Process]**&#x200B;頁籤下：

   * **[!UICONTROL 圖]**:清除所有條目以禁用轉碼預設值：  `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

   ![configure-ffmpeg](assets/configure-ffmpeg.png)

* 選擇&#x200B;**[!UICONTROL 確定]**&#x200B;以關閉`Step Properties`對話框。

* 選擇&#x200B;**[!UICONTROL 保存]**&#x200B;以保存`DAM Update Asset`工作流。



