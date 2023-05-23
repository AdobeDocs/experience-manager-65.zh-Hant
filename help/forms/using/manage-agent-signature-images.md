---
title: 管理代理簽名映像
seo-title: Manage agent signature images
description: 建立信件模板後，可以使用它通過管理資料、內容和附件在AEM Forms建立信件。
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
ht-degree: 1%

---

# 管理代理簽名映像{#manage-agent-signature-images}

## 概觀 {#overview}

在「通信管理」中，可以使用影像以字母形式呈現代理簽名。 在設定代理簽名映像後，在建立信件時，可以將信件中的代理簽名映像作為發件人代理的簽名呈現。

agentSignatureImage DDE是代表代理簽名映像的計算DDE。 此計算DDE的表達式使用表達式管理器構建塊公開的新自定義函式。 此自定義函式將agentID和agentFolder作為輸入參數，並根據這些參數提取影像內容。 SystemContext系統資料字典在Oracle Tergement中提供對當前系統上下文中資訊的訪問。 系統上下文包括有關當前登錄的用戶和活動配置參數的資訊。

可以在cmuserroot資料夾下添加影像。 在 [通信管理配置屬性](/help/forms/using/cm-configuration-properties.md)，使用CM用戶根屬性可更改從中獲取代理簽名影像的資料夾。

agentFolder DDE的值是從Tergement Management配置屬性的CMUserRoot配置參數中獲取的。 預設情況下，此配置參數指向CRX儲存庫中的/content/cmUserRoot。 可以在「配置屬性」中更改CMUserRoot配置的值。
您還可以覆蓋預設自定義函式以定義您自己的邏輯來獲取用戶簽名影像。

## 添加代理簽名映像 {#adding-agent-signature-image}

1. 確保代理簽名映像與用戶的用戶名AEM同名。 （映像檔案名不需要副檔名。）
1. 在CRX中，建立名為 `cmUserRoot` 的子菜單。

   1. 前往 `https://'[server]:[port]'/crx/de`. 如有必要，請以管理員身份登錄。

   1. 按一下右鍵 **內容** 資料夾和 **建立** > **建立資料夾**。

      ![建立資料夾](assets/1_createnode_cmuserroot.png)

   1. 在「建立資料夾」對話框中，輸入資料夾的名稱 `cmUserRoot`。 按一下 **全部保存**。

      >[!NOTE]
      >
      >cmUserRoot是查找代理簽AEM名映像的預設位置。 但是，可以通過編輯CM用戶根屬性來更改 [通信管理配置屬性](/help/forms/using/cm-configuration-properties.md)。

1. 在內容資源管理器中，導航到cmUserRoot資料夾並在其中添加代理簽名映像。

   1. 前往 `https://'[server]:[port]'/crx/explorer/index.jsp`. 如有必要，請以管理員身份登錄。
   1. 按一下 **內容瀏覽器**。 「內容瀏覽器」(Content Explorer)將在新窗口中開啟。
   1. 在內容資源管理器中，導航到cmUserRoot資料夾並選擇它。 按一下右鍵 **cmUserRoot** 資料夾和 **新建節點**。

      ![cmUserRoot中的新節點](assets/2_cmuserroot_newnode.png)

      在新節點的行中輸入以下條目，然後按一下綠色複選標籤。

      **名稱：** JohnDoe（或代理簽名檔案的名稱）

      **類型：** nt：檔案

      在 `cmUserRoot` 資料夾，名為 `JohnDoe` （或上一步中指定的名稱）。

   1. 按一下您建立的新資料夾（此處） `JohnDoe`)。 內容資源管理器將資料夾的內容顯示為灰色。

   1. 按兩下 **jcr：內容** 屬性，將其類型設定為 **nt：資源**，然後按一下綠色複選標籤以保存該條目。

      如果屬性不存在，請首先建立名為jcr:content的屬性。

      ![jcr：內容屬性](assets/3_jcrcontentntresource.png)

      jcr:content的子屬性中包括jcr:data，該屬性為灰色。 按兩下jcr:data。 該屬性將變為可編輯狀態，「選擇檔案」(Choose File)按鈕將出現在條目中。 按一下 **選擇檔案** 並選擇要用作徽標的影像檔案。 映像檔案不需要副檔名。

      ![JCR資料](assets/5_jcrdata.png)
   按一下 **全部保存**。

1. 確保在字母中使用的XDP\layout在左下角（或要呈現簽名的佈局中的其他適當位置）有一個影像欄位來呈現簽名影像。
1. 建立對應時，在「資料」頁籤中，使用以下步驟為簽名影像選擇一個影像欄位：

   1. 從右窗格的「連結類型」彈出菜單中選擇「系統」。

   1. 從SystemContext DD的「資料元素」面板的清單中選擇agentSignatureImage DDE。

   1. 保存信件。

1. 在呈現字母時，您可以根據佈局在影像欄位中的字母預覽中看到您簽名。

   ![字母中的代理簽名影像](assets/letterwithsignature.png)
