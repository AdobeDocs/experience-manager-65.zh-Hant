---
title: 字母PDF預覽中的自定義水印
seo-title: Custom watermark in letter PDF preview
description: 瞭解如何在字母PDF預覽中建立自定義水印。
seo-description: Learn how to create custom watermark in letter PDF preview.
uuid: 5adfede3-9b38-4a12-bf14-6d80cfb0a05a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: adc7ec13-0675-4071-9c4c-e238202d9d85
docset: aem65
feature: Correspondence Management
exl-id: 7d90fade-1ca4-41d8-bbf9-45490465784a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# 字母PDF預覽中的自定義水印{#custom-watermark-in-letter-pdf-preview}

## 概觀 {#overview}

在「建立通信」UI中，座席用戶以最終形式預覽通信，在最終形式中，通信被發送到後處理，例如用於電子郵件或打印。

為防止未經授權使用此資料，組織可以在預覽PDF上加上水印。 預設水印為「PREVIEW」，該水印出現在PDF中。

要在預覽PDF中啟用水印，請選擇 **[!UICONTROL 應用水印]** 「預覽期間」選項 **[!UICONTROL 通信管理配置]** https://&#39;[伺服器]:[埠]「/system/console/configMgr。

![預設水印](assets/default-watermark.png)

可以使用以下步驟來自定義水印的文本和外觀：

## 在「建立對應UI」中的PDF預覽中自定義水印 {#customizewatermark-}

1. 轉到 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身份登錄。
1. 在應用資料夾中，建立名為 **[!UICONTROL 預覽水印]** 路徑/結構與libs資料夾中的previewwatermark資料夾類似：

   1. 按一下右鍵 **預覽水印** 資料夾，然後選擇 **覆蓋節點**:

      `/libs/fd/cm/configFiles/previewwatermark`

   1. 確保「覆蓋節點」對話框具有以下值：

      **路徑：** /libs/fd/cm/configFiles/previewwatermark

      **覆蓋位置：** /apps/

      **匹配節點類型：** 已選中

      >[!NOTE]
      >
      >不要在/libs分支中進行更改。 您所做的任何更改都可能丟失，因為在以下情況下，此分支可能會發生更改：
      >
      >    
      >    
      >    * 在實例上升級
      >    * 應用熱修復
      >    * 安裝功能包


   1. 按一下 **確定** 然後按一下 **全部保存**。 的 **[!UICONTROL 預覽水印]** 資料夾是在指定路徑中建立的。

1. 將ddx檔案從&quot;/libs/fd/cm/configFiles/previewwatermark&quot;資料夾複製並貼上到&quot;/apps/fd/cm/configFiles/previewwatermark&quot;資料夾，然後按一下 **[!UICONTROL 全部保存]**。
1. 在/apps/fd/cm/configFiles/previewwatermark/下對ddx檔案進行所需更改。

   ```xml
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

   有關自定義水印外觀、文本和對齊方式的資訊，請參閱中的添加和刪除水印和背景 [匯編程式服務和DDX參考](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf) 的子菜單。

   >[!NOTE]
   >
   >在ddx檔案中，對結果和源的引用應保持未更改為output.pdf和input.pdf。 也不應更改檔案ddx的名稱。

1. 按一下 **全部保存**。
