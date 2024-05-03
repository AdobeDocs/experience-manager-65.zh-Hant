---
title: 信件PDF預覽中的自訂浮水印
description: 瞭解如何在信件PDF預覽中建立自訂浮水印。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: 7d90fade-1ca4-41d8-bbf9-45490465784a
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 1%

---

# 信件PDF預覽中的自訂浮水印{#custom-watermark-in-letter-pdf-preview}

## 概觀 {#overview}

在「建立通訊」UI中，代理使用者會以最終形狀預覽通訊，並在最終形狀中將其傳送到後處理，例如電子郵件或列印。

為防止未經授權使用此資料，組織可以對預覽PDF加上浮水印。 預設浮水印為「PREVIEW」，會在PDF上顯示。

若要在預覽PDF中啟用浮水印，請選取 **[!UICONTROL 套用浮水印]** 中的預覽期間」選項 **[!UICONTROL 通訊管理設定]** 在https://&#39;[伺服器]：[連線埠]&#39;/system/console/configMgr.

![default-watermark](assets/default-watermark.png)

您可以使用下列步驟來自訂浮水印的文字和外觀：

## 在建立通訊UI中在PDF預覽中自訂浮水印 {#customizewatermark-}

1. 前往 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身分登入。
1. 在應用程式資料夾中，建立名為的資料夾 **[!UICONTROL 預覽浮水印]** 路徑/結構類似於libs資料夾中的previewwatermark資料夾：

   1. 用滑鼠右鍵按一下 **預覽浮水印** 資料夾並選取「 」 **覆蓋節點**：

      `/libs/fd/cm/configFiles/previewwatermark`

   1. 請確定「覆蓋節點」對話方塊是否具備下列值：

      **路徑：** /libs/fd/cm/configFiles/previewwatermark

      **覆蓋位置：** /apps/

      **符合節點型別：** 已核取

      >[!NOTE]
      >
      >請勿在/libs分支中進行變更。 您所做的任何變更都可能會遺失，因為每當您：
      >
      >    
      >    
      >    * 在您的執行個體上升級
      >    * 套用Hot Fix
      >    * 安裝Feature Pack
      >    
      >

   1. 按一下 **確定** 然後按一下 **全部儲存**. 此 **[!UICONTROL 預覽浮水印]** 資料夾會在指定的路徑中建立。

1. 將ddx檔案從「/libs/fd/cm/configFiles/previewwatermark」資料夾複製並貼到「/apps/fd/cm/configFiles/previewwatermark」資料夾，然後按一下 **[!UICONTROL 全部儲存]**.
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

   如需有關自訂浮水印外觀、文字和對齊的資訊，請參閱新增和移除浮水印和背景 [組合器服務和DDX參考](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf) 檔案。

   >[!NOTE]
   >
   >在ddx檔案中，對結果和來源的參照應保持未變更為output.pdf和input.pdf。 檔案ddx的名稱也不應變更。

1. 按一下&#x200B;**「儲存全部」**。
