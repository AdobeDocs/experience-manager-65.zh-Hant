---
title: 管理代理簽名映像
seo-title: 管理代理簽名映像
description: 在您建立信函範本之後，您可以使用它來管理資料、內容和附件，以建立AEM Forms中的對應。
seo-description: 在您建立信函範本之後，您可以使用它來管理資料、內容和附件，以建立AEM Forms中的對應。
uuid: 48b2697e-6065-4e23-9aa8-333e7b11ede1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: a81cdd53-f0fb-4ac5-b2ec-c19aeee7186e
docset: aem65
translation-type: tm+mt
source-git-commit: 06335b9a85414b6b1141dd19c863dfaad0812503

---


# 管理代理簽名映像{#manage-agent-signature-images}

## 概覽 {#overview}

在「對應管理」中，您可以使用影像以字母形式呈現代理簽名。 設定代理簽名映像後，在建立信件時，可以將信件中的代理簽名映像作為發送者代理的簽名呈現。

agentSignatureImage DDE是表示代理簽名映像的計算DDE。 此計算DDE的表達式使用「表達式管理器」構建塊公開的新自定義函式。 此自訂函式將agentID和agentFolder作為輸入參數，並根據這些參數讀取影像內容。 SystemContext系統資料字典為「通信管理」中的字母提供了對當前系統上下文中資訊的訪問。 系統上下文包括有關當前登錄用戶和活動配置參數的資訊。

您可以在cmuserroot資料夾下新增影像。 在 [Correponsent Management Configuration Properties](/help/forms/using/cm-configuration-properties.md)（對應管理配置屬性）中，使用CM User root屬性，可以更改從中獲取代理簽名映像的資料夾。

agentFolder DDE的值取自「對應管理」配置屬性的CMUserRoot配置參數。 預設情況下，此配置參數指向CRX儲存庫中的/content/cmUserRoot。 您可以在配置屬性中更改CMUserRoot配置的值。
您也可以覆寫預設自訂函式，以定義您自己用來擷取使用者簽名影像的邏輯。

## 添加代理簽名映像 {#adding-agent-signature-image}

1. 請確定代理簽名影像與使用者的AEM使用者名稱相同。 （影像檔案名稱不需要副檔名。）
1. 在CRX中，在內容檔案夾中 `cmUserRoot` 建立名稱的檔案夾。

   1. 前往 `https://[server]:[port]/crx/de`. 如有必要，請以管理員身份登錄。

   1. 在內容資料夾上按 **滑鼠右鍵** ，然後選 **取「建立** >建 **立資料夾**」。

      ![建立資料夾](assets/1_createnode_cmuserroot.png)

   1. 在「建立資料夾」對話框中，輸入資料夾的名稱 `cmUserRoot`。 按一下「 **全部儲存**」。

      >[!NOTE]
      >
      >cmUserRoot是AEM尋找代理簽名影像的預設位置。 但是，您可以通過編輯「通信管理」配置屬性中的「CM用戶根」屬 [性來更改它](/help/forms/using/cm-configuration-properties.md)。

1. 在「內容檔案總管」中，導覽至cmUserRoot資料夾，並在其中新增代理簽名影像。

   1. 前往 `https://[server]:[port]/crx/explorer/index.jsp`. 視需要以管理員身分登入。
   1. 按一 **下「內容總管**」。 「內容總管」會在新視窗中開啟。
   1. 在「內容檔案總管」中，導覽至cmUserRoot資料夾並選取它。 按一下右鍵 **cmUserRoot** 資料夾並選擇 **新建節點**。

      ![cmUserRoot中的新節點](assets/2_cmuserroot_newnode.png)

      在新節點的行中輸入以下條目，然後按一下綠色複選標籤。

      **** 名稱：JohnDoe（或您的代理簽名檔案的名稱）

      **** 類型：nt：檔案

      在該 `cmUserRoot` 資料夾下，將建立一個名為 `JohnDoe` （或您在上一步中指定的名稱）的新資料夾。

   1. 按一下您建立的新資料夾(此處 `JohnDoe`)。 「內容檔案總管」會將資料夾的內容顯示為暗灰色。

   1. 連按兩下 **jcr:content** 屬性，將其類型設為 **nt:resource**，然後按一下綠色核取標籤以儲存項目。

      如果屬性不存在，請先建立名為jcr:content的屬性。

      ![jcr:content屬性](assets/3_jcrcontentntresource.png)

      jcr:content的子屬性中包括jcr:data，此為暗灰色。 連按兩下jcr:data。 屬性變為可編輯狀態，「選擇檔案」按鈕將顯示在條目中。 按一 **下「選擇檔案** 」，然後選取您要當做標誌使用的影像檔案。 影像檔不需要副檔名。

      ![JCR資料](assets/5_jcrdata.png)
   按一下「 **全部儲存**」。

1. 請確定您在字母中使用的XDP\layout在左下方有影像欄位（或您要呈現簽名的版面中其他適當位置），以呈現簽名影像。
1. 建立對應時，在「資料」索引標籤中，使用下列步驟為簽名影像選取影像欄位：

   1. 從右窗格的「連結類型」彈出菜單中選擇「系統」。

   1. 從SystemContext DD的「資料元素」面板的清單中選取agentSignatureImage DDE。

   1. 保存信。

1. 在轉譯字母時，您可以根據版面在影像欄位的字母預覽中看到您的簽名。

   ![信中的代理簽名影像](assets/letterwithsignature.png)

