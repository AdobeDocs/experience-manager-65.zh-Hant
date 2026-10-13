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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 3f00fc92-85ee-583e-abd1-3bc3d96de3a0
    internal-label: Correspondence Management
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 1%
---
# 信件PDF預覽中的自訂浮水印{#custom-watermark-in-letter-pdf-preview}

## 概觀 {#overview}

在「建立通訊」UI中，代理使用者會以最終形狀預覽通訊，並在最終形狀中將其傳送到後處理，例如電子郵件或列印。

為避免未經授權使用此資料，組織可以對預覽PDF加上浮水印。 預設浮水印為「預覽」，會在整個PDF中顯示。

若要在預覽PDF中啟用浮水印，請在&#x200B;**[!UICONTROL 通訊管理設定]** （位於https://&#39;[伺服器]：[連線埠]&#39;/system/console/configMgr）中選取&#x200B;**[!UICONTROL 預覽期間套用浮水印]**。

![預設浮水印](assets/default-watermark.png)

您可以使用下列步驟來自訂浮水印的文字和外觀：

## 在建立通訊UI中在PDF預覽中自訂浮水印 {#customizewatermark-}

1. 前往`https://'[server]:[port]'/[ContextPath]/crx/de`並以管理員身分登入。
1. 在apps資料夾中，建立名為&#x200B;**[!UICONTROL previewwatermark]**&#x200B;的資料夾，其路徑/結構類似於libs資料夾中的previewwatermark資料夾：

   1. 在下列路徑的&#x200B;**previewwatermark**&#x200B;資料夾上按一下滑鼠右鍵，然後選取&#x200B;**覆蓋節點**：

      `/libs/fd/cm/configFiles/previewwatermark`

   1. 請確定「覆蓋節點」對話方塊是否具備下列值：

      **路徑：** /libs/fd/cm/configFiles/previewwatermark

      **覆蓋位置：** /apps/

      **符合節點型別：**&#x200B;已核取

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

   1. 按一下[確定]&#x200B;**&#x200B;**，然後按一下[儲存全部]&#x200B;**&#x200B;**。 **[!UICONTROL previewwatermark]**&#x200B;資料夾是在指定的路徑中建立的。

1. 將ddx檔案從「/libs/fd/cm/configFiles/previewwatermark」資料夾複製並貼到「/apps/fd/cm/configFiles/previewwatermark」資料夾，然後按一下&#x200B;**[!UICONTROL 全部儲存]**。
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

   如需自訂浮水印外觀、文字和對齊方式的資訊，請參閱[組合器服務和DDX參考](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf)檔案中的新增和移除浮水印和背景。

   >[!NOTE]
   >
   >在ddx檔案中，對結果和來源的參照應保持未變更為output.pdf和input.pdf。 檔案ddx的名稱也不應變更。

1. 按一下&#x200B;**「儲存全部」**。
