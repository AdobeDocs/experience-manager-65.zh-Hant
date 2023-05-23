---
title: 初始沙盒應用程式
seo-title: Initial Sandbox Application
description: 建立模板、元件和指令碼
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

# 初始沙盒應用程式 {#initial-sandbox-application}

在本節中，將建立以下內容：

* 的 **[模板](#createthepagetemplate)** 將用於在示例網站中建立內容頁面。
* 的 **[元件和指令碼](#create-the-template-s-rendering-component)** 將用於呈現網站頁面。

## 建立內容模板 {#create-the-content-template}

模板定義新頁面的預設內容。 複雜網站可能使用多個模板在網站中建立不同類型的頁面。 此外，該模板集可以成為用於對伺服器群集進行部署的更改的藍圖。

在本練習中，所有頁面都基於一個簡單模板。

1. 在CRXDE Lite的瀏覽器窗格中：

   * 選取 `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL 建立]** > **[!UICONTROL 建立模板]**

1. 在「建立模板」對話框中，鍵入以下值，然後按一下 **[!UICONTROL 下一個]**:

   * 標籤: `playpage`
   * 標題: `An SCF Sandbox Play Template`
   * 說明: `An SCF Sandbox template for play pages`
   * 資源類型: `an-scf-sandbox/components/playpage`
   * 排名： &lt;leave as=&quot;&quot; default=&quot;&quot;>

   「標籤」用於節點名稱。

   「Resource Type（資源類型）」出現在 `playpage`s jcr:content節點作為屬性 `sling:resourceType`。 它標識當瀏覽器請求時呈現內容的元件（資源）。

   在本例中，使用 `playpage` 模板由 `an-scf-sandbox/components/playpage` 元件。 按照慣例，到元件的路徑是相對的，允許Sling首先在 `/apps` 資料夾和（如果找不到） `/libs` 的子菜單。

   ![建立內容模板](assets/create-content-template-1.png)

1. 如果使用複製/貼上，請確保「資源類型」值沒有前導空格或尾隨空格。

   按一下&#x200B;**[!UICONTROL 下一步]**。

1. 「允許的路徑」是指使用此模板的頁的路徑，以便為 **[!UICONTROL 新建頁面]** 對話框。

   要添加路徑，請按一下加號按鈕 `+` 和類型 `/content(/.&ast;)?` 的上界。 如果使用複製/貼上，請確保沒有前導空格或尾隨空格。

   注：允許的路徑屬性的值是 *規則運算式*。 具有與表達式匹配的路徑的內容頁可以使用模板。 在這種情況下，規則運算式與 **/內容** 資料夾及其所有子頁。

   當作者在下面建立頁面時 `/content`，也請參見Wiki頁。 `playpage` 標題為「SCF沙盒頁面模板」的模板將出現在可用模板清單中。

   從模板建立根頁後，可以通過修改屬性將根路徑包括在規則運算式中，即，對模板的訪問限制到此網站。

   `/content/an-scf-sandbox(/.&ast;)?`

   ![配置模板路徑](assets/configure-template-path.png)

1. 按一下&#x200B;**[!UICONTROL 下一步]**。

   按一下 **[!UICONTROL 下一個]** 的 **[!UICONTROL 允許的父項]** 的子菜單。

   按一下 **[!UICONTROL 下一個]** 的 **[!UICONTROL 允許的子項]** 的下界。

   按一下&#x200B;**[!UICONTROL 「確定」]**。

1. 按一下「確定」(OK)並完成模板的建立後，您會注意到新模板的「屬性」(Properties)頁籤值拐角中顯示的紅色三角形 `playpage` 的下界。 這些紅色三角形表示尚未保存的編輯。

   按一下 **[!UICONTROL 全部保存]** 將新模板保存到儲存庫。

   ![驗證內容模板](assets/verify-content-template.png)

### 建立模板的渲染元件 {#create-the-template-s-rendering-component}

建立 *元件* 定義內容並呈現基於 [playpage template（播放頁模板）](#createthepagetemplate)。

1. 在CRXDE Lite中，按一下右鍵 **`/apps/an-scf-sandbox/components`** 按一下 **[!UICONTROL 建立>元件]**。
1. 通過將節點的名稱（標籤）設定為 *播放頁*，到元件的路徑為

   `/apps/an-scf-sandbox/components/playpage`

   與播放頁模板的「資源類型」(可選地減去初始 **`/apps/`** 部分路徑)。

   在 **[!UICONTROL 建立元件]** 對話框，鍵入以下屬性值：

   * 標籤： **播放頁**
   * 標題： **SCF沙盒播放元件**
   * 描述： **這是為SCF沙盒頁呈現內容的元件。**
   * 超級類型： *&lt;leave blank=&quot;&quot;>*
   * 組： *&lt;leave blank=&quot;&quot;>*

   ![建立模板元件](assets/create-template-component.png)

1. 按一下 **[!UICONTROL 下一個]** 直到 **[!UICONTROL 允許的子項]** 對話框的面板：

   * 按一下&#x200B;**[!UICONTROL 「確定」]**。
   * 按一下 **[!UICONTROL 全部保存]**。

1. 驗證元件的路徑與模板的resourceType是否匹配。

   >[!CAUTION]
   >
   >播放頁元件的路徑與播放頁模板的sling:resourceType屬性之間的對應關係對網站的正確運行至關重要。

   ![驗證模板元件](assets/verify-template-component.png)
