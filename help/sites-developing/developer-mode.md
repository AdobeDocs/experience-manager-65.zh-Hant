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
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 0%

---


# 開發人員模式{#developer-mode}

在AEM中編輯頁面時，有數個[模式](/help/sites-authoring/author-environment-tools.md#modestouchoptimizedui)可用，包括「開發人員」模式。 這會開啟一個包含數個標籤的側面板，讓開發人員可瞭解目前頁面的相關資訊。 這三個標籤是：

* **[用於](#components)** 查看結構和效能資訊的元件。
* **[測試](#tests)** 以執行測試並分析結果。
* **[錯](#errors)** 誤，無法查看發生的任何問題。

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
   >   
   * 當寬度小於1024像素時就會發生此情況。
>* 僅適用於`administrators`群組成員的使用者。


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
>* 知識庫文章[疑難排解AEM TouchUI問題](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html)，以取得更多提示和工具。
>* AEM Gems階段作業關於[AEM 6.0 Developer Mode](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html)。

>



## 開啟開發人員模式{#opening-developer-mode}

開發人員模式是作為頁面編輯器的側面板實作。 若要開啟面板，請從頁面編輯器工具列的模式選擇器中選取&#x200B;**Developer**:

![chlimage_1-11](assets/chlimage_1-11.png)

此面板分為兩個標籤：

* **[Components](/help/sites-developing/developer-mode.md#components)**  —— 此處顯示與作者內容樹類似 [的](/help/sites-authoring/author-environment-tools.md#content-tree) 元件樹

* **[錯誤](/help/sites-developing/developer-mode.md#errors)** -發生問題時，會顯示每個元件的詳細資訊。

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
>某些連結指向`/libs`下的指令碼。 但是，這些僅供參考，您&#x200B;**不得**&#x200B;編輯`/libs`下的任何內容，因為您所做的任何變更都可能遺失。 這是由於當您升級或套用修補程式／功能套件時，此分支很容易發生變更。 您需要的任何變更都應在`/apps`下進行，請參閱[覆蓋與覆寫](/help/sites-developing/overlays.md)。

### 錯誤 {#errors}

![chlimage_1-16](assets/chlimage_1-16.png)

希望&#x200B;**Errors**&#x200B;標籤永遠為空（如上所示），但當出現問題時，會針對每個元件顯示以下詳細資料：

* 如果元件將項目寫入錯誤記錄，以及錯誤的詳細資訊，並直接連結至CRXDE Lite中的適當程式碼，則會發出警告。
* 當元件開啟管理工作階段時會發出警告。

例如，在呼叫未定義方法的情況下，產生的錯誤會顯示在&#x200B;**Errors**&#x200B;標籤中：

![chlimage_1-17](assets/chlimage_1-17.png)

出現錯誤時，「元件」頁籤樹中的元件條目也將用指示符標籤。

### 測試 {#tests}

>[!CAUTION]
>
>在AEM 6.2中，開發人員模式的測試功能已重新建置為獨立的「工具」應用程式。
>
>如需完整詳細資訊，請參閱[測試您的UI](/help/sites-developing/hobbes.md)。

