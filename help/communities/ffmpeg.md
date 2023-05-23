---
title: 社區FMPEG
seo-title: FFmpeg for Communities
description: 如何為社區安裝和配置FFmpeg
seo-description: How to install and configure FFmpeg for Communities
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
role: Admin
exl-id: dbe28334-3b38-4362-b4f8-e0630e634503
source-git-commit: 942db8fe3dad16be53dc6abe0e519d97a659e480
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 社區FMPEG {#ffmpeg-for-communities}

## 概觀 {#overview}

FFmpeg是一種用於轉換和流式傳輸音頻和視頻的解決方案，當安裝時，用於適當的音頻和視頻轉碼 [視頻資產](../../help/sites-authoring/default-components-foundation.md#video)。

## 安裝FFmpeg {#installing-ffmpeg}

FFmpeg應安裝在承載FF MP的服AEM務器 *作者* 實例。

1. 轉到 [https://www.ffmpeg.org](https://www.ffmpeg.org/)。
1. 下載適用於您特定環境（Macintosh、Windows或Linux）的最新版本的FFmpeg。

   * 由於舊版本中存在安全漏洞，因此保持FFmpeg最新非常重要。

1. 按照作業系統的說明安裝FFmpeg。

1. 確保在系統路徑中設定了FFmpeg執行檔。

   您應該能夠從系統中的任何目錄運行FFmpeg。

   * 比如說， `ffmpeg -version`。

## 配置FFmpeg轉碼服務 {#configure-ffmpeg-transcoding-service}

預設情況下，當安裝FFmpeg時，將按照 [!UICONTROL DAM更新資產] 工作流定義。

由於轉換佔用CPU，建議修改目標格式副本清單。 在大多數情況下，不需要轉碼。

修改 [!UICONTROL DAM更新資產] 工作流，在本示例中，要關閉轉碼：

* 以管理權限登錄作者實例。
* 從全局導航，導航到 **[!UICONTROL 工具]** > **[!UICONTROL 工作流]** > **[!UICONTROL 模型]**。
* 定位 **[!UICONTROL DAM更新資產]**。
* 按兩下以開啟要在「傳統用戶介面」中編輯的工作流。

   結果位置： [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* 按兩下 **[!UICONTROL FFmpeg轉碼]** 步驟以訪問「步驟屬性」對話框。
* 在 **[!UICONTROL 進程]** 頁籤：

   * **[!UICONTROL 阿爾甘]**:清除所有條目以禁用轉碼預設值： `profile:format_ogg,profile:format_aac,profile:format_flv,profile:format_aac_ie`

   ![配置ffmpeg](assets/configure-ffmpeg.png)

* 選擇 **[!UICONTROL 確定]** 關閉 `Step Properties` 對話框。

* 選擇 **[!UICONTROL 保存]** 來保存 `DAM Update Asset` 工作流。
