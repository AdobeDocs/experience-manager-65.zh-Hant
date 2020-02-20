---
title: 開發人員模式
seo-title: 開發人員模式
description: 開發人員模式會開啟一個側面板，其中包含數個標籤，可讓開發人員取得目前頁面的相關資訊
seo-description: 開發人員模式會開啟一個側面板，其中包含數個標籤，可讓開發人員取得目前頁面的相關資訊
uuid: 8301ab51-93d6-44f9-a813-ba7f03f54485
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 589e3a83-7d1a-43fd-98b7-3b947122829d
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 開發人員模式{#developer-mode}

在AEM中編輯頁面時，有數種 [模式](/help/sites-authoring/author-environment-tools.md#modestouchoptimizedui) ，包括「開發人員」模式。 這會開啟一個包含數個標籤的側面板，讓開發人員可瞭解目前頁面的相關資訊。 這三個標籤是：

* **[用於查看結構](#components)**和效能資訊的元件。
* **[測試](#tests)**，以執行測試並分析結果。
* **[錯誤](#errors)**，以查看發生的任何問題。

這些功能可協助開發人員：

* Discover:由哪些頁面組成。
* 除錯：發生在何處和何時的情況，這反過來有助於解決問題。
* 測試：應用程式是否如預期般運作。

>[!CAUTION]
>
>開發人員模式：
>
>* 僅在啟用觸控的UI中可用（在編輯頁面時）。
>* 在行動裝置或桌上型電腦的小視窗上無法使用（因為空間限制）。
>
>    * 當寬度小於1024像素時就會發生此情況。
>
>* 需要適當的權限／權限：
>
>    * 對「開發人員模式」的存取權會授予對具有寫入存取權的使用者 `/apps`。
>

>[!CAUTION]
>
>開發人員模式僅適用於未使用nosamplecontent執行模式的標準作者例項。
>
>如果需要，可將其配置為使用：
>
>* 在使用nosamplecontent run-mode的作者實例上
>* 發佈實例
>
>
使用後應再次停用。

>[!NOTE]
>
>請參閱：
>
>* 知識庫文章「疑難 [排解AEM TouchUI問題](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html)」，以取得更多提示和工具。
>* AEM Gems工作階段關於 [AEM 6.0 Developer Mode](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html)。
>



## 開啟開發人員模式 {#opening-developer-mode}

開發人員模式是作為頁面編輯器的側面板實作。 若要開啟面板，請從頁面編輯器工具列 **的模式選取器** ，選取「開發人員」:

![chlimage_1-11](assets/chlimage_1-11.png)

此面板分為兩個標籤：

* **[元件](/help/sites-developing/developer-mode.md#components)**-這會顯示元件樹，類似於作者的[內容樹](/help/sites-authoring/author-environment-tools.md#content-tree)。

* **[錯誤](/help/sites-developing/developer-mode.md#errors)**-發生問題時，會顯示每個元件的詳細資料。

### 元件 {#components}

![chlimage_1-12](assets/chlimage_1-12.png)

這顯示了一個元件樹，其中：

* 概述在頁面上呈現的元件和範本鏈（SLY、JSP等）。 樹可以展開，以顯示層次中的上下文。
* 顯示轉換元件所需的伺服器端計算時間。
* 允許您展開樹並在樹中選擇特定元件。 Selection提供對元件詳細資訊的訪問；例如：

   * 儲存庫路徑
   * 指令碼的連結（在CRXDE Lite中存取）

* 選取的元件（在內容流中，以藍色邊框表示）會在內容樹狀結構中反白顯示（反之亦然）。

這有助於：

* 確定並比較每個元件的轉換時間。
* 瞭解並瞭解階層。
* 透過尋找緩慢的元件，瞭解並改善頁面載入時間。

每個元件項目都可顯示（例如）:

![chlimage_1-13](assets/chlimage_1-13.png)

* **檢視詳細資訊**:一個指向清單的連結，其中顯示：

   * 用於呈現元件的所有元件指令碼。
   * 此特定元件的儲存庫內容路徑。
   ![chlimage_1-14](assets/chlimage_1-14.png)

* **編輯指令碼**:連結：

   * 在CRXDE Lite中開啟元件指令碼。

* 展開元件項目（箭頭標題）也可顯示：

   * 所選元件內的層次。
   * 單獨呈現所選元件的時間、其中巢狀內嵌的任何個別元件，以及總和。
   ![chlimage_1-15](assets/chlimage_1-15.png)

>[!CAUTION]
>
>有些連結指向下方的指令碼 `/libs`。 但是，這些僅供參考，您不 **得編輯** ，因 `/libs`為您所做的任何變更都可能遺失。 這是由於當您升級或套用修補程式／功能套件時，此分支很容易發生變更。 您需要的任何變更都應在下方進行，請 `/apps`參閱覆 [蓋和覆寫](/help/sites-developing/overlays.md)。

### 錯誤 {#errors}

![chlimage_1-16](assets/chlimage_1-16.png)

希望「錯 **誤** 」頁籤始終為空（如上所示），但當出現問題時，會為每個元件顯示以下詳細資訊：

* 如果元件將項目寫入錯誤記錄，以及錯誤的詳細資訊，並直接連結至CRXDE Lite中的適當程式碼，則會發出警告。
* 當元件開啟管理工作階段時會發出警告。

例如，在呼叫未定義方法的情況下，產生的錯誤會顯示在「錯誤」標 **簽中** :

![chlimage_1-17](assets/chlimage_1-17.png)

發生錯誤時，「元件」頁籤樹中的元件條目也將用指示符標籤。

### 測試 {#tests}

>[!CAUTION]
>
>在AEM 6.2中，開發人員模式的測試功能已重新建置為獨立的「工具」應用程式。
>
>如需完整詳細資訊，請 [參閱測試您的UI](/help/sites-developing/hobbes.md)。

