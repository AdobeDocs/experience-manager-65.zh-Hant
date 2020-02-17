---
title: 字母PDF預覽中的自訂浮水印
seo-title: 字母PDF預覽中的自訂浮水印
description: 瞭解如何在字母PDF預覽中建立自訂浮水印。
seo-description: 瞭解如何在字母PDF預覽中建立自訂浮水印。
uuid: 5adfede3-9b38-4a12-bf14-6d80cfb0a05a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: adc7ec13-0675-4071-9c4c-e238202d9d85
docset: aem65
translation-type: tm+mt
source-git-commit: 5a586758da84f467e075adcc33cdcede2fbf09c7

---


# 字母PDF預覽中的自訂浮水印{#custom-watermark-in-letter-pdf-preview}

## 概覽 {#overview}

在「建立對應」UI中，工程師使用者會以最終形式預覽對應，並將其傳送至後置處理，例如以電子郵件傳送或列印。

為防止未授權使用此資料，組織可在預覽PDF上加上浮水印。 預設浮水印為「PREVIEW」，會顯示在PDF中。

要在預覽PDF中啟用水印，請在 **[!UICONTROL Correponsement Management Configurations]** https:// **[!UICONTROL server]** :[portSystem/console/configMgr中選擇Apply Watermark][]During Preview選項。

![default-watermark](assets/default-watermark.png)

您可以使用下列步驟來自訂浮水印的文字和外觀：

## 在「建立對應UI」中自訂PDF預覽中的浮水印 {#customizewatermark-}

1. 前往並 `https://[server]:[port]/[ContextPath]/crx/de` 以管理員身分登入。
1. 在應用程式檔案夾中，建立名為 **[!UICONTROL previewwatermark的檔案夾]** ，其路徑／結構類似於libs檔案夾中的previewwatermark檔案夾：

   1. 以滑鼠右鍵按一 **下下列路徑** ，並選取「覆蓋節點 **」**:

      `/libs/fd/cm/configFiles/previewwatermark`

   1. 請確定「覆蓋節點」對話框具有下列值：

      **** 路徑：/libs/fd/cm/configFiles/previewwatermark

      **** 覆蓋位置：/apps/

      **** 匹配節點類型：已勾選

      >[!NOTE]
      >
      >請勿在/libs分支中進行更改。 您所做的任何變更都可能會遺失，因為此分支在您執行下列動作時都會面臨變更：
      >
      >    
      >    
      >    * 在您的實例上升級
      >    * 套用Hot Fix
      >    * 安裝功能套件


   1. 按一 **下「確定** 」，然後按一 **下「全部儲存」**。 預 **[!UICONTROL 檢浮水印]** 資料夾會建立在指定的路徑中。



1. 將「/libs/fd/cm/configFiles/previewwatermark」檔案夾中的ddx檔案複製並貼至「/apps/fd/cm/configFiles/previewwatermark」檔案夾，然後按一下「全 **[!UICONTROL 部儲存]**」。
1. 在/apps/fd/cm/configFiles/previewwatermark/下的dx檔案中進行所需的變更。

   ```
   <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
    <PDF result="output.pdf">
     <PDF source="input.pdf"/>
           <Watermark opacity="15%" rotation="45">
            <StyledText>
                     <p font-family="Georgia" font-size="70pt" color="black" font-weight="bold">
                         PREVIEW
                    </p>
            </StyledText>
           </Watermark>
    </PDF>
   </DDX>
   ```

   如需自訂浮水印外觀、文字和對齊方式的詳細資訊，請參閱 [Assembler Service和DDX Reference檔案中的新增和移除浮水印和背景](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf) 。

   >[!NOTE]
   >
   >在ddx檔案中，結果和來源的參照應保持未變更為output.pdf和input.pdf。 也不應更改檔案ddx的名稱。

1. 按一下「 **全部儲存**」。

