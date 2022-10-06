---
title: 初始沙箱應用程式
seo-title: Initial Sandbox Application
description: 建立範本、元件和指令碼
seo-description: Create template, component, and script
uuid: b0d03376-d8bc-4e98-aea2-a01744c64ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f74d225e-0245-4d5a-bb93-0ee3f31557aa
exl-id: cbf9ce36-53a2-4f4b-a96f-3b05743f6217
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 2%

---

# 初始沙箱應用程式 {#initial-sandbox-application}

在本節中，您將建立下列項目：

* 此 **[範本](#createthepagetemplate)** 將用來建立範例網站中的內容頁面。
* 此 **[元件和指令碼](#create-the-template-s-rendering-component)** 來呈現網站頁面。

## 建立內容範本 {#create-the-content-template}

範本定義新頁面的預設內容。 複雜的網站可能會使用數個範本來建立網站中不同類型的頁面。 此外，該模板集可以成為用於將更改轉出到伺服器群集的藍圖。

在本練習中，所有頁面都以一個簡單範本為基礎。

1. 在CRXDE Lite的瀏覽器窗格中：

   * 選取 `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL 建立]** > **[!UICONTROL 建立範本]**

1. 在「建立範本」對話方塊中，輸入下列值，然後按一下 **[!UICONTROL 下一個]**:

   * 標籤: `playpage`
   * 標題: `An SCF Sandbox Play Template`
   * 說明: `An SCF Sandbox template for play pages`
   * 資源類型: `an-scf-sandbox/components/playpage`
   * 排名： &lt;leave as=&quot;&quot; default=&quot;&quot;>

   節點名稱使用標籤。

   資源類型將出現在 `playpage`作為屬性的s jcr:content節點 `sling:resourceType`. 它會識別在瀏覽器要求時轉譯內容的元件（資源）。

   在此案例中，使用 `playpage` 範本由 `an-scf-sandbox/components/playpage` 元件。 根據慣例，元件的路徑是相對的，可讓Sling先在 `/apps` 資料夾中，若找不到，則位於 `/libs` 檔案夾。

   ![create-content-template](assets/create-content-template-1.png)

1. 如果使用複製/貼上，請確定「資源類型」值沒有前導或尾隨空格。

   按一下&#x200B;**[!UICONTROL 下一步]**。

1. 「允許的路徑」是指使用此範本的頁面路徑，因此會為 **[!UICONTROL 新頁面]** 對話框。

   若要新增路徑，請按一下加號按鈕 `+` 和類型 `/content(/.&ast;)?` 框中。 如果使用複製/貼上，請確定開頭或結尾沒有空格。

   注意：允許的路徑屬性的值為 *規則運算式*. 具有符合運算式之路徑的內容頁面可使用範本。 在此情況下，規則運算式會比對 **/content** 資料夾及其所有子頁面。

   作者在下方建立頁面時 `/content`, `playpage` 標題為「SCF沙箱頁面範本」的範本會顯示在可使用範本清單中。

   從範本建立根頁面後，修改屬性以將根路徑包含在規則運算式中，即可限制對範本的存取，以存取此網站。

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. 按一下&#x200B;**[!UICONTROL 下一步]**。

   按一下 **[!UICONTROL 下一個]** 在 **[!UICONTROL 允許的父項]** 中。

   按一下 **[!UICONTROL 下一個]** 在 **[!UICONTROL 允許的子項]** 面板。

   按一下&#x200B;**[!UICONTROL 「確定」]**。

1. 按一下「確定」(OK)並完成模板的建立後，您會注意到新模板的「屬性」(Properties)頁簽值的拐角中顯示了紅色三角形 `playpage` 範本。 這些紅色三角形表示未保存的編輯。

   按一下 **[!UICONTROL 全部儲存]** 將新模板保存到儲存庫。

   ![verify-content-template](assets/verify-content-template.png)

### 建立範本的呈現元件 {#create-the-template-s-rendering-component}

建立 *元件* 定義內容並轉譯任何根據 [播放頁面範本](#createthepagetemplate).

1. 在CRXDE Lite中，按一下右鍵 **`/apps/an-scf-sandbox/components`** 按一下 **[!UICONTROL 建立>元件]**.
1. 將節點名稱（標籤）設定為 *播放頁面*，元件的路徑為

   `/apps/an-scf-sandbox/components/playpage`

   與播放頁面範本的「資源類型」對應(選擇性減去初始 **`/apps/`** 路徑的一部分)。

   在 **[!UICONTROL 建立元件]** 對話框，鍵入以下屬性值：

   * 標籤： **播放頁面**
   * 標題： **SCF沙箱播放元件**
   * 說明： **這是可為SCF沙箱頁面轉譯內容的元件。**
   * 超類型： *&lt;leave blank=&quot;&quot;>*
   * 組： *&lt;leave blank=&quot;&quot;>*

   ![create-template-component](assets/create-template-component.png)

1. 按一下 **[!UICONTROL 下一個]** 直到 **[!UICONTROL 允許的子項]** 對話框的面板出現：

   * 按一下&#x200B;**[!UICONTROL 「確定」]**。
   * 按一下 **[!UICONTROL 全部儲存]**.

1. 驗證元件的路徑與模板的resourceType是否匹配。

   >[!CAUTION]
   >
   >playpage元件路徑與playpage範本的sling:resourceType屬性之間的對應，對於網站的正確運作至關重要。

   ![verify-template-component](assets/verify-template-component.png)
