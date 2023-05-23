---
title: 視頻呈現
description: 視頻呈現
uuid: a02f9ec1-30d9-4cbb-8746-8391ac614f0a
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: 1601b473-7227-4a56-bb7c-289de2987e4b
exl-id: a644558e-5be9-4ba2-b560-fc300497fbdf
source-git-commit: 77687a0674b939460bd34011ee1b94bd4db50ba4
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# 視頻呈現 {#video-renditions}

Adobe Experience Manager資產為各種格式的視頻資產生成視頻格式副本，包括OGG、FLV等。

Experience Manager Assets支援媒體資產的靜態和動態格式副本（DM編碼格式副本）。

靜態格式副本是使用FFMPEG（在系統路徑上安裝並可用）以本機方式生成的，並儲存在內容儲存庫中。

DM編碼的格式副本儲存在代理伺服器中，並在運行時提供服務。

Experience Manager Assets在客戶端為這些格式副本提供播放支援。

要查看特定視頻資產的格式副本，請開啟其資產頁面，然後選擇「全局導航」表徵圖。 然後，選擇 **[!UICONTROL 格式副本]** 清單中。

![chlimage_1-478](assets/chlimage_1-478.png)

視頻格式副本清單顯示在 **[!UICONTROL 格式副本]** 的子菜單。

![chlimage_1-479](assets/chlimage_1-479.png)

要為DM編碼的格式副本配置代理伺服器， [配置Dynamic Media雲服務](config-dynamic.md)。

要使用所需參數生成視頻呈現， [建立相應的視頻配置檔案](video-profiles.md)。

配置代理伺服器並建立視頻配置檔案後，可以將此視頻預設包含在處理配置檔案中，並將處理配置檔案應用到資料夾。

>[!NOTE]
>
>在Microsoft® Internet Explorer 11上播放OGG和WAV檔案時，音頻播放不起作用。 錯誤 `Invalid Source` 顯示在分機為OGG或WAV的資產的資產詳細資訊頁面上。
>
>在MS® Edge和iPad上，OGG檔案不播放並引發不支援的格式錯誤。
