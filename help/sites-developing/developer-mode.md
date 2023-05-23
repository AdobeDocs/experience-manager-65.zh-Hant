---
title: 開發人員模式
seo-title: Developer Mode
description: 開發者模式開啟帶有多個頁籤的側面板，這些頁籤為開發者提供有關當前頁面的資訊
seo-description: Developer mode opens a side panel with several tabs that provide a developer with infomation about the current page
uuid: 8301ab51-93d6-44f9-a813-ba7f03f54485
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 589e3a83-7d1a-43fd-98b7-3b947122829d
docset: aem65
exl-id: aef0350f-4d3d-47f4-9c7e-5675efef65d9
source-git-commit: 30327950779337ce869b6ca376120bc09826be21
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 2%

---

# 開發人員模式{#developer-mode}

在中編輯頁AEM面時 [模式](/help/sites-authoring/author-environment-tools.md#modestouchoptimizedui) 可用，包括開發人員模式。 這將開啟一個帶有多個頁籤的側面板，這些頁籤為開發人員提供了有關當前頁面的資訊。 這三個頁籤是：

* **[元件](#components)** 查看結構和效能資訊。
* **[Test](#tests)** 運行test並分析結果。
* **[錯誤](#errors)** 看到發生的任何問題。

這些幫助開發人員：

* 發現：由哪些頁面組成。
* 調試：在何處何時發生什麼，這反過來又有助於解決問題。
* Test:應用程式是否按預期運行。

>[!CAUTION]
>
>開發人員模式:
>
>* 僅在啟用觸摸的UI（編輯頁面時）中可用。
>* 移動設備或案頭上的小窗口上不可用（由於空間限制）。
   >
   >   * 當寬度小於1024px時出現此情況。
>* 僅適用於 `administrators` 組。


>[!CAUTION]
>
>開發者模式僅在不使用nosamplecontent運行模式的標準作者實例上可用。
>
>如果需要，可將其配置為使用：
>
>* 關於使用nosamplecontent運行模式的作者實例
>* 發佈實例
>
>使用後應再次禁用。

>[!NOTE]
>
>請參閱：
>
>* 知識庫文章， [TouchUI問題AEM疑難解答](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html)，以獲取更多提示和工具。
>* Gems會AEM話關於 [AEM 6.0開發模式](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2014/aem-developer-mode.html?lang=en)。
>


## 開啟開發人員模式 {#opening-developer-mode}

開發者模式被實現為頁面編輯器的側面板。 要開啟面板，請選擇 **開發人員** 從頁面編輯器工具欄中的模式選擇器：

![chlimage_1-11](assets/chlimage_1-11.png)

該面板分為兩個頁籤：

* **[元件](/help/sites-developing/developer-mode.md#components)**  — 顯示與 [內容樹](/help/sites-authoring/author-environment-tools.md#content-tree) 作者

* **[錯誤](/help/sites-developing/developer-mode.md#errors)**  — 出現問題時，將顯示每個元件的詳細資訊。

### 元件 {#components}

![chlimage_1-12](assets/chlimage_1-12.png)

這顯示一個元件樹，它：

* 概述在頁面上呈現的元件和模板鏈（SLY、JSP等）。 樹可以展開，以在層次中顯示上下文。
* 顯示呈現元件所需的伺服器端計算時間。
* 允許您展開樹並在樹中選取特定元件。 選擇提供對元件詳細資訊的訪問；例如：

   * 儲存庫路徑
   * 指向指令碼的連結(在CRXDE Lite中訪問)

* 所選元件（在內容流中，用藍色邊框指示）將在內容樹中加亮（反之亦然）。

這有助於：

* 確定並比較每個元件的渲染時間。
* 查看並瞭解層次結構。
* 通過查找慢速元件瞭解並改進頁面載入時間。

每個元件條目都可以顯示（例如）:

![chlimage_1-13](assets/chlimage_1-13.png)

* **查看詳細資訊**:指向清單的連結，其中顯示：

   * 用於呈現該元件的所有元件指令碼。
   * 此特定元件的儲存庫內容路徑。

   ![chlimage_1-14](assets/chlimage_1-14.png)

* **編輯指令碼**:連結：

   * 在CRXDE Lite中開啟元件指令碼。

* 展開元件條目（箭頭）還可顯示：

   * 所選元件中的層次。
   * 獨立呈現選定元件的時間、嵌套在其中的任何單個元件以及組合總數。

   ![chlimage_1-15](assets/chlimage_1-15.png)

>[!CAUTION]
>
>某些連結指向以下指令碼 `/libs`。 但是，這些僅供參考，您 **不能** 編輯 `/libs`，因為您所做的任何更改都可能丟失。 這是由於以下事實：無論您何時升級或應用修補程式/功能包，此分支都可能發生更改。 您需要的任何更改都應在 `/apps`，請參閱 [覆蓋和覆蓋](/help/sites-developing/overlays.md)。

### 錯誤 {#errors}

![chlimage_1-16](assets/chlimage_1-16.png)

但願 **錯誤** 頁籤將始終為空（如上所示），但當出現問題時，將為每個元件顯示以下詳細資訊：

* 如果元件將條目寫入錯誤日誌，以及錯誤的詳細資訊，並直接連結到CRXDE Lite中的相應代碼，則會出現警告。
* 如果元件開啟管理會話，則出現警告。

例如，在調用未定義方法的情況下，將在 **錯誤** 頁籤：

![chlimage_1-17](assets/chlimage_1-17.png)

出現錯誤時，「元件」頁籤樹中的元件條目也將用指示符標籤。

### 測試 {#tests}

>[!CAUTION]
>
>在AEM6.2中，開發人員模式的測試功能作為獨立工具應用程式重新實施。
>
>有關完整詳細資訊，請參閱 [測試您的UI](/help/sites-developing/hobbes.md)。
