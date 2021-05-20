---
title: 初始沙箱應用程式
seo-title: 初始沙箱應用程式
description: 建立範本、元件和指令碼
seo-description: 建立範本、元件和指令碼
uuid: b0d03376-d8bc-4e98-aea2-a01744c64ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f74d225e-0245-4d5a-bb93-0ee3f31557aa
exl-id: cbf9ce36-53a2-4f4b-a96f-3b05743f6217
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 2%

---

# 初始沙箱應用程式{#initial-sandbox-application}

在本節中，您將建立下列項目：

* 將用於建立範例網站中內容頁面的&#x200B;**[範本](#createthepagetemplate)**。
* 將用於呈現網站頁面的&#x200B;**[元件和指令碼](#create-the-template-s-rendering-component)**。

## 建立內容範本{#create-the-content-template}

範本定義新頁面的預設內容。 複雜的網站可能會使用數個範本來建立網站中不同類型的頁面。 此外，該模板集可以成為用於將更改轉出到伺服器群集的藍圖。

在本練習中，所有頁面都以一個簡單範本為基礎。

1. 在CRXDE Lite的瀏覽器窗格中：

   * 選取 `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL 建立]**  >建 **[!UICONTROL 立範本]**

1. 在「建立模板」對話框中，鍵入以下值，然後按一下&#x200B;**[!UICONTROL Next]**:

   * 標籤: `playpage`
   * 標題: `An SCF Sandbox Play Template`
   * 說明: `An SCF Sandbox template for play pages`
   * 資源類型: `an-scf-sandbox/components/playpage`
   * 排名：&lt;保留為預設值>

   節點名稱使用標籤。

   資源類型作為屬性`sling:resourceType`顯示在`playpage`的jcr:content節點上。 它會識別在瀏覽器要求時轉譯內容的元件（資源）。

   在這種情況下，使用`playpage`範本建立的所有頁面都由`an-scf-sandbox/components/playpage`元件呈現。 根據慣例，元件的路徑是相對的，可讓Sling先在`/apps`資料夾中搜尋資源，若找不到，則在`/libs`資料夾中搜尋。

   ![create-content-template](assets/create-content-template-1.png)

1. 如果使用複製/貼上，請確定「資源類型」值沒有前導或尾隨空格。

   按一下&#x200B;**[!UICONTROL 下一步]**。

1. 「允許的路徑」是指使用此範本的頁面路徑，因此會為&#x200B;**[!UICONTROL 新頁面]**&#x200B;對話方塊列出範本。

   若要新增路徑，請按一下加號按鈕`+`，然後在出現的文字方塊中輸入`/content(/.&ast;)?`。 如果使用複製/貼上，請確定開頭或結尾沒有空格。

   注意：允許的路徑屬性的值是&#x200B;*規則運算式*。 具有符合運算式之路徑的內容頁面可使用範本。 在這種情況下，規則運算式會符合&#x200B;**/content**&#x200B;資料夾的路徑及其所有子頁面。

   當作者在`/content`下方建立頁面時，標題為「SCF沙箱頁面範本」的`playpage`範本會顯示在可使用範本清單中。

   從範本建立根頁面後，修改屬性以將根路徑包含在規則運算式中，即可限制對範本的存取，以存取此網站。

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. 按一下&#x200B;**[!UICONTROL 下一步]**。

   按一下&#x200B;**[!UICONTROL 允許的父項]**&#x200B;面板中的&#x200B;**[!UICONTROL Next]**。

   在&#x200B;**[!UICONTROL 允許的子項]**&#x200B;面板中，按一下&#x200B;**[!UICONTROL Next]**。

   按一下&#x200B;**[!UICONTROL 「確定」]**。

1. 按一下「確定」(OK)並完成模板的建立後，您將注意到新`playpage`模板的「屬性」(Properties)頁簽值的拐角中顯示了紅色三角形。 這些紅色三角形表示未保存的編輯。

   按一下「**[!UICONTROL 全部保存」，將新模板保存到儲存庫。]**

   ![verify-content-template](assets/verify-content-template.png)

### 建立模板的呈現元件{#create-the-template-s-rendering-component}

建立&#x200B;*元件*，定義內容並轉譯根據[playpage範本](#createthepagetemplate)建立的任何頁面。

1. 在CRXDE Lite中，按一下右鍵&#x200B;**`/apps/an-scf-sandbox/components`**，然後按一下&#x200B;**[!UICONTROL 建立>元件]**。
1. 將節點的名稱(Label)設定為&#x200B;*playpage*&#x200B;後，元件的路徑為

   `/apps/an-scf-sandbox/components/playpage`

   與播放頁面範本的「資源類型」對應（可選擇減去路徑的初始&#x200B;**`/apps/`**&#x200B;部分）。

   在&#x200B;**[!UICONTROL 建立元件]**&#x200B;對話方塊中，輸入下列屬性值：

   * 標籤：**playpage**
   * 標題：**SCF沙箱播放元件**
   * 說明：**這是為SCF沙箱頁面呈現內容的元件。**
   * 超類型：*&lt;leave blank>*
   * 組：*&lt;leave blank>*

   ![create-template-component](assets/create-template-component.png)

1. 按一下&#x200B;**[!UICONTROL Next]**，直到對話框的&#x200B;**[!UICONTROL 允許的子項]**&#x200B;面板出現：

   * 按一下&#x200B;**[!UICONTROL 「確定」]**。
   * 按一下「**[!UICONTROL 全部保存]**」。

1. 驗證元件的路徑與模板的resourceType是否匹配。

   >[!CAUTION]
   >
   >playpage元件路徑與playpage範本的sling:resourceType屬性之間的對應，對於網站的正確運作至關重要。

   ![verify-template-component](assets/verify-template-component.png)
