---
title: 管理代理簽名映像
seo-title: Manage agent signature images
description: 建立信函範本後，您就可以透過管理資料、內容及附件，使用該範本在AEM Forms中建立通信。
seo-description: After you have created a letter template, you can use it to create correspondence in AEM Forms by managing data, content, and attachments.
uuid: 48b2697e-6065-4e23-9aa8-333e7b11ede1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: a81cdd53-f0fb-4ac5-b2ec-c19aeee7186e
docset: aem65
feature: Correspondence Management
exl-id: f044ed75-bb72-4be1-aef6-2fb3b2a2697b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---

# 管理代理簽名映像{#manage-agent-signature-images}

## 總覽 {#overview}

在通信管理中，您可以使用影像在信函中呈現代理簽名。 設定代理簽名影像後，在建立信函時，可以將信函中的代理簽名影像呈現為發件人代理的簽名。

agentSignatureImage DDE是表示代理簽名映像的計算DDE。 此計算DDE的表達式使用由「表達式管理器」構建塊公開的新自定義函式。 此自定義函式將agentID和agentFolder作為輸入參數，並根據這些參數讀取影像內容。 SystemContext系統資料字典為通信管理中的字母提供對當前系統上下文中資訊的訪問。 系統上下文包括有關當前登錄的用戶和活動配置參數的資訊。

您可以在cmuserroot資料夾下新增影像。 在 [通信管理配置屬性](/help/forms/using/cm-configuration-properties.md)，可以使用CM用戶根屬性更改從中提取代理簽名影像的資料夾。

代理資料夾DDE的值取自通信管理配置屬性的CMUserRoot配置參數。 依預設，此設定參數會指向CRX存放庫中的/content/cmUserRoot。 您可以在「配置屬性」中更改CMUserRoot配置的值。
您也可以覆寫預設的自訂函式，以定義您用來擷取使用者簽名影像的自訂邏輯。

## 添加代理簽名映像 {#adding-agent-signature-image}

1. 請確定代理簽名映像與用戶的AEM用戶名具有相同的名稱。 （影像檔案名稱不需要副檔名。）
1. 在CRX中，建立名為 `cmUserRoot` （在內容資料夾中）。

   1. 前往 `https://'[server]:[port]'/crx/de`. 如有必要，請以管理員身分登入。

   1. 以滑鼠右鍵按一下 **內容** 資料夾和選取 **建立** > **建立資料夾**.

      ![建立資料夾](assets/1_createnode_cmuserroot.png)

   1. 在「建立資料夾」對話框中，將資料夾的名稱輸入為 `cmUserRoot`. 按一下 **全部儲存**.

      >[!NOTE]
      >
      >cmUserRoot是AEM在其中查找代理簽名映像的預設位置。 但是，您可以通過編輯 [通信管理配置屬性](/help/forms/using/cm-configuration-properties.md).

1. 在「內容總管」中，導覽至cmUserRoot資料夾，並在其中新增代理簽名影像。

   1. 前往 `https://'[server]:[port]'/crx/explorer/index.jsp`. 視需要以管理員身分登入。
   1. 按一下 **內容總管**. 「內容總管」(Content Explorer)將在新窗口中開啟。
   1. 在「內容總管」中，導覽至cmUserRoot資料夾並選取它。 以滑鼠右鍵按一下 **cmUserRoot** 資料夾和選取 **新節點**.

      ![cmUserRoot中的新節點](assets/2_cmuserroot_newnode.png)

      在新節點的行中輸入以下條目，然後按一下綠色複選標籤。

      **名稱：** JohnDoe（或代理簽名檔案的名稱）

      **類型：** nt:file

      在 `cmUserRoot` 資料夾，新資料夾稱為 `JohnDoe` （或您在上一步驟中指定的名稱）已建立。

   1. 按一下您建立的新資料夾（此處） `JohnDoe`)。 「內容總管」會以灰色顯示資料夾的內容。

   1. 按兩下 **jcr:content** 屬性，將其類型設定為 **nt:resource**，然後按一下綠色複選記號以儲存項目。

      如果屬性不存在，請先建立名為jcr:content的屬性。

      ![jcr:content屬性](assets/3_jcrcontentntresource.png)

      jcr:content的子屬性中有jcr:data，其為灰色。 按兩下jcr:data。 該屬性變為可編輯狀態，Choose File（選擇檔案）按鈕將出現在條目中。 按一下 **選擇檔案** 並選擇要用作徽標的影像檔案。 影像檔案的副檔名不需要。

      ![JCR資料](assets/5_jcrdata.png)
   按一下 **全部儲存**.

1. 確保在信函中使用的XDP\layout左下角有一個影像欄位（或要呈現簽名的佈局中的其他適當位置），以呈現簽名影像。
1. 建立通信時，在「資料」頁簽中，使用下列步驟為簽名影像選擇一個影像欄位：

   1. 從右窗格的「連結類型」彈出菜單中選擇「系統」。

   1. 從「資料元素」面板的清單中為SystemContext DD選擇agentSignatureImage DDE。

   1. 保存信。

1. 轉譯信函時，您可以根據版面，在影像欄位的信函預覽中看到您的簽名。

   ![信函中的代理簽名影像](assets/letterwithsignature.png)
