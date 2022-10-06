---
title: 適用於社群的FFmpeg
seo-title: FFmpeg for Communities
description: 如何安裝和配置FFmpeg for Communities
seo-description: How to install and configure FFmpeg for Communities
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
role: Admin
exl-id: dbe28334-3b38-4362-b4f8-e0630e634503
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# 適用於社群的FFmpeg {#ffmpeg-for-communities}

## 總覽 {#overview}

FFmpeg是轉換和串流音訊和視訊的解決方案，安裝後用於適當轉碼 [影片資產](../../help/sites-authoring/default-components-foundation.md#video) 以及AEM Communities啟用功能。

FFmpeg用於製作環境，以取得上傳的啟用資源的中繼資料，並產生縮圖以在列出啟用資源時顯示。

## 安裝FFmpeg {#installing-ffmpeg}

FFmpeg應安裝在托管AEM的伺服器上 *作者* 例項。

1. 前往 [https://www.ffmpeg.org](https://www.ffmpeg.org/).
1. 下載適用於您特定環境（Macintosh、Windows或Linux）的最新版FFmpeg。

   * 由於舊版中的安全漏洞，請務必保持FFmpeg最新。

1. 按照作業系統的說明安裝FFmpeg。

1. 請確保在系統路徑中設定了FFmpeg執行檔。

   您應該可以從系統中的任何目錄運行FFmpeg。

   * 例如， `ffmpeg -version`.

## 配置FFmpeg轉碼服務 {#configure-ffmpeg-transcoding-service}

依預設，安裝FFmpeg時，會根據 [!UICONTROL DAM更新資產] 工作流程定義。

由於轉譯需要CPU資源，因此建議修改目標轉譯清單。 在大多數情況下，不需要轉碼。

若要修改 [!UICONTROL DAM更新資產] 工作流程和此範例中，關閉轉碼：

* 以管理權限登入製作例項。
* 從全域導覽導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 工作流程]** > **[!UICONTROL 模型]**.
* 找出 **[!UICONTROL DAM更新資產]**.
* 按兩下以開啟傳統UI中編輯的工作流程。

   產生的位置： [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* 按兩下 **[!UICONTROL FFmpeg轉碼]** 訪問「步驟屬性」對話框的步驟。
* 在 **[!UICONTROL 程式]** 標籤：

   * **[!UICONTROL 區段]**:清除所有條目以禁用轉碼預設值： `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

   ![configure-ffmpeg](assets/configure-ffmpeg.png)

* 選擇 **[!UICONTROL 確定]** 關閉 `Step Properties` 對話框。

* 選擇 **[!UICONTROL 儲存]** 來儲存 `DAM Update Asset` 工作流程。
