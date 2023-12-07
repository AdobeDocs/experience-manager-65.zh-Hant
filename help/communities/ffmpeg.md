---
title: 適用於社群的FFmpeg
description: 如何為社群安裝和設定FFmpeg
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: dbe28334-3b38-4362-b4f8-e0630e634503
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 1%

---

# 適用於社群的FFmpeg {#ffmpeg-for-communities}

## 概觀 {#overview}

FFmpeg是一種轉換和串流音訊與視訊的解決方案，安裝後可用於正確轉碼 [視訊資產](../../help/sites-authoring/default-components-foundation.md#video).

## 安裝FFmpeg {#installing-ffmpeg}

FFmpeg應安裝在託管AEM的伺服器上 *作者* 執行個體。

1. 前往 [https://www.ffmpeg.org](https://www.ffmpeg.org/).
1. 針對您的特定環境（Macintosh、Windows或Linux）下載最新版的FFmpeg。

   * 由於FFmpeg較舊版本的安全性弱點，因此務必保持最新狀態。

1. 依照作業系統的指示安裝FFmpeg。

1. 請確定已在您的系統路徑中設定FFmpeg可執行檔。

   您應該可以從系統中的任何目錄執行FFmpeg。

   * 例如，`ffmpeg -version`。

## 設定FFmpeg轉碼服務 {#configure-ffmpeg-transcoding-service}

依預設，安裝FFmpeg時，會根據 [!UICONTROL DAM更新資產] 工作流程定義。

由於轉碼耗用CPU，因此建議修改目標轉譯清單。 在大多數情況下，不需要轉碼。

若要修改 [!UICONTROL DAM更新資產] 工作流程，在此範例中，若要關閉轉碼：

* 使用管理許可權登入作者執行個體。
* 從全域導覽，導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.
* 尋找 **[!UICONTROL DAM更新資產]**.
* 按兩下以在傳統UI中開啟要編輯的工作流程。

  產生的位置： [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* 按兩下 **[!UICONTROL FFmpeg轉碼]** 步驟以存取「步驟屬性」對話方塊。
* 在 **[!UICONTROL 程式]** 標籤：

   * **[!UICONTROL 引數]**：清除所有專案以停用轉碼預設值： `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

  ![configure-ffmpeg](assets/configure-ffmpeg.png)

* 選取 **[!UICONTROL 確定]** 以關閉 `Step Properties` 對話方塊。

* 選取 **[!UICONTROL 儲存]** 儲存 `DAM Update Asset` 工作流程。
