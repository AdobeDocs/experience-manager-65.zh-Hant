---
title: 信函PDF預覽中的自訂浮水印
seo-title: 信函PDF預覽中的自訂浮水印
description: 了解如何在信函PDF預覽中建立自訂浮水印。
seo-description: 了解如何在信函PDF預覽中建立自訂浮水印。
uuid: 5adfede3-9b38-4a12-bf14-6d80cfb0a05a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: adc7ec13-0675-4071-9c4c-e238202d9d85
docset: aem65
feature: 通信管理
exl-id: 7d90fade-1ca4-41d8-bbf9-45490465784a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---

# 信函PDF預覽中的自訂浮水印{#custom-watermark-in-letter-pdf-preview}

## 概覽 {#overview}

在「建立通信」UI中，代理用戶會以最終形式預覽通信，在該形式下，通信將被發送到後置處理，例如用於電子郵件或打印。

為防止未授權使用此資料，組織可以在預覽PDF上加上浮水印。 預設水印為「PREVIEW」，會出現在PDF中。

要在預覽PDF中啟用水印，請在&#x200B;**[!UICONTROL 通信管理配置]**&#x200B;中選擇&#x200B;**[!UICONTROL 在預覽期間應用水印]**&#x200B;選項(https://&#39;[server]:[port]&#39;/system/console/configMgr)。

![預設水印](assets/default-watermark.png)

您可以使用下列步驟來自訂浮水印的文字和外觀：

## 在建立通信UI {#customizewatermark-}中自訂PDF預覽中的浮水印

1. 前往`https://'[server]:[port]'/[ContextPath]/crx/de`並以管理員身分登入。
1. 在應用程式資料夾中，建立名為&#x200B;**[!UICONTROL previewwatermark]**&#x200B;的資料夾，其路徑/結構類似於libs資料夾中的previewwatermark資料夾：

   1. 按一下右鍵以下路徑的&#x200B;**previewwatermark**&#x200B;資料夾，然後選擇&#x200B;**覆蓋節點**:

      `/libs/fd/cm/configFiles/previewwatermark`

   1. 確定「覆蓋節點」對話方塊有下列值：

      **路徑：** /libs/fd/cm/configFiles/previewwatermark

      **覆蓋位置：** /apps/

      **匹配節點類型：已** 勾選

      >[!NOTE]
      >
      >請勿在/libs分支中進行變更。 您所做的任何變更都可能會遺失，因為只要您符合以下條件，此分支就會發生變更：
      >
      >    
      >    
      >    * 在您的執行個體上升級
      >    * 套用Hotfix
      >    * 安裝功能套件


   1. 按一下&#x200B;**OK**，然後按一下&#x200B;**Save All**。 **[!UICONTROL previewwatermark]**&#x200B;資料夾建立在指定路徑中。



1. 從「/libs/fd/cm/configFiles/previewwatermark」資料夾複製ddx檔案並貼到「/apps/fd/cm/configFiles/previewwatermark」資料夾，然後按一下「**[!UICONTROL 儲存全部]**」。
1. 在/apps/fd/cm/configFiles/previewwatermark/底下的ddx檔案中進行所需的變更。

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

   有關自定義水印外觀、文本和對齊方式的資訊，請參閱[組合器服務和DDX參考](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf)文檔中的添加和刪除水印和背景。

   >[!NOTE]
   >
   >在ddx檔案中，對結果和來源的參照應保持不變，為output.pdf和input.pdf。 也不應變更檔案ddx的名稱。

1. 按一下「**全部保存**」。
