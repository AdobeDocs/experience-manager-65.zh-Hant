---
title: 初始沙盒應用程式
seo-title: 初始沙盒應用程式
description: 建立範本、元件和指令碼
seo-description: 建立範本、元件和指令碼
uuid: b0d03376-d8bc-4e98-aea2-a01744c64ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f74d225e-0245-4d5a-bb93-0ee3f31557aa
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 初始沙盒應用程式 {#initial-sandbox-application}

在本節中，您將建立以下內容：

* 用 **[於在](#createthepagetemplate)**範例網站中建立內容頁面的範本
* 用 **[於呈現網站頁面的元件](#create-the-template-s-rendering-component)**和指令碼

## 建立內容範本 {#create-the-content-template}

範本會定義新頁面的預設內容。 複雜的網站可能會使用數個範本來建立網站中不同類型的頁面。 此外，該組模板可以成為用於將更改推廣到伺服器群集的藍圖。

在本練習中，所有頁面都以單一簡單範本為基礎。

1. 在CRXDE Lite的瀏覽器窗格中

   * select `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL 「建立>建立範本」]**

1. 在「建立範本」對話方塊中，輸入下列值，然後按一下「下 **[!UICONTROL 一步]**:

   * 標籤: `playpage`
   * 標題: `An SCF Sandbox Play Template`
   * 說明: `An SCF Sandbox template for play pages`
   * 資源類型: `an-scf-sandbox/components/playpage`
   * 排名：&lt;leave as default>
   Label用於節點名稱。

   資源類型將作為屬 `playpage`性顯示在jcr:content節點上 `sling:resourceType`。 它可識別在瀏覽器要求時轉譯內容的元件（資源）。

   在這種情況下，使用模板建立的所 `playpage`有頁都由元件呈 `an-scf-sandbox/components/playpage` 現。 依慣例，元件的路徑是相對的，可讓Sling先在資料夾中搜尋資源，若找不到， `/apps` 則在資料夾中 `/libs` 搜尋。

   ![chlimage_1-75](assets/chlimage_1-75.png)

1. 如果使用複製／貼上，請確保「資源類型」值沒有前導或尾隨空格。

   按一 **[!UICONTROL 下「下一步]**」。

1. 「允許的路徑」是指使用此範本的頁面路徑，因此會列出「新頁面」對話 **[!UICONTROL 框的範本]** 。

   若要新增路徑，請按一下加號按 `+` 鈕並 `/content(/.&ast;)?` 在顯示的文字方塊中輸入。 如果使用複製／貼上，請確定沒有前導或尾隨空格。

   注意：允許的路徑屬性的值是規則運 *算式。* 路徑與運算式相符的內容頁面可以使用範本。 在這種情況下，規則運算式與 **/content資料夾的路徑** 及其所有子頁面相符。

   當作者在下面建立頁 `/content`面時，標 `playpage`題為「SCF沙盒頁面範本」的範本會出現在可用範本清單中。

   從範本建立根頁面後，修改屬性以將根路徑包含在規則運算式中，即可限制範本的存取權限至此網站。

   `/content/an-scf-sandbox(/.&ast;)?`

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. 按一 **[!UICONTROL 下「下一步]**」。

   在「允 **[!UICONTROL 許的父項]** 」面板中， **[!UICONTROL 按一下「下一步]** 」。

   在「允 **[!UICONTROL 許的子項]** 」面板中，按 **[!UICONTROL 一下「下一步]** 」。

   按一下 **[!UICONTROL 確定]**。

1. 按一下「確定」(OK)並完成模板的建立後，您將注意到新模板的「屬性」(Properties)頁籤值的拐角中顯示了紅色 `playpage`三角形。 這些紅色三角形表示未保存的編輯。

   按一下 **[!UICONTROL 全部保存]** ，將新模板保存到儲存庫。

   ![chlimage_1-77](assets/chlimage_1-77.png)

### 建立模板的渲染元件 {#create-the-template-s-rendering-component}

建立定 *義內容* ，並轉譯任何根據播放頁範本建立 [的頁面](#createthepagetemplate)。

1. 在CRXDE Lite中，以滑鼠右鍵按一下， **`/apps/an-scf-sandbox/components`** 然後按一 **[!UICONTROL 下「建立>元件」]**。
1. 將節點名稱（標籤）設為 *playpage*，則元件的路徑為

   `/apps/an-scf-sandbox/components/playpage`

   與播放頁範本的「資源類型」(可選減去路徑的 **`/apps/`** 初始部分)相對應。

   在「創 **[!UICONTROL 建元件]** 」對話框中，鍵入以下屬性值：

   * 標籤：播 **放頁**
   * 標題：SCF **沙盒播放元件**
   * 說明：這 **是轉換「SCF沙盒」頁面內容的元件。**
   * 超級類型： *&lt;留空>*
   * 群組:
   ![chlimage_1-78](assets/chlimage_1-78.png)

1. 按一下「 **[!UICONTROL 下一步]** 」，直到出現 **[!UICONTROL 對話框的「允許子項]** 」面板

   * 按一下「 **[!UICONTROL 確定」]**
   * 按一下「 **[!UICONTROL 全部儲存」]**

1. 驗證元件的路徑與模板的resourceType是否匹配。

   >[!CAUTION]
   >
   >playpage元件的路徑與playpage範本的sling:resourceType屬性之間的對應關係對網站的正確運作至關重要。

   ![chlimage_1-79](assets/chlimage_1-79.png)