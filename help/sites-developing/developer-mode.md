---
title: 開發人員模式
seo-title: Developer Mode
description: 開發人員模式會開啟側面板，其中包含數個標籤，為開發人員提供目前頁面的相關資訊
seo-description: Developer mode opens a side panel with several tabs that provide a developer with infomation about the current page
uuid: 8301ab51-93d6-44f9-a813-ba7f03f54485
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 589e3a83-7d1a-43fd-98b7-3b947122829d
docset: aem65
exl-id: aef0350f-4d3d-47f4-9c7e-5675efef65d9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 0%

---

# 開發人員模式{#developer-mode}

在AEM中編輯頁面時， [模式](/help/sites-authoring/author-environment-tools.md#modestouchoptimizedui) 可用，包括開發人員模式。 這會開啟一個側面板，其中包含數個標籤，為開發人員提供目前頁面的相關資訊。 這三個標籤是：

* **[元件](#components)** 查看結構和效能資訊。
* **[測試](#tests)** 用於運行測試和分析結果。
* **[錯誤](#errors)** 看到發生的任何問題。

這些功能可協助開發人員：

* Discover:頁面的組成。
* 調試：何時何地發生，進而有助於解決問題。
* 測試：應用程式是否如預期般運作。

>[!CAUTION]
>
>開發人員模式：
>
>* 僅適用於觸控式UI（編輯頁面時）。
>* 在行動裝置上或案頭上的小視窗上皆無法使用（因空間限制）。
   >
   >   * 當寬度小於1024px時即會發生此情況。
>* 僅適用於 `administrators` 群組。


>[!CAUTION]
>
>開發人員模式僅適用於未使用nosamplecontent執行模式的標準製作例項。
>
>如有需要，可將其設定為使用：
>
>* 在使用nosamplecontent執行模式的製作例項上
>* 發佈例項
>
>使用後應再次停用。

>[!NOTE]
>
>請參閱：
>
>* 知識庫文章， [疑難排解AEM TouchUI問題](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html)，以取得更多秘訣和工具。
>* AEM Gem課程關於 [AEM 6.0開發人員模式](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html).
>


## 開啟開發人員模式 {#opening-developer-mode}

開發人員模式是作為側面板實作到頁面編輯器。 若要開啟面板，請選取 **開發人員** 從頁面編輯器工具列中的模式選取器：

![chlimage_1-11](assets/chlimage_1-11.png)

面板分為兩個標籤：

* **[元件](/help/sites-developing/developer-mode.md#components)**  — 這會顯示類似於 [內容樹](/help/sites-authoring/author-environment-tools.md#content-tree) 供作者使用

* **[錯誤](/help/sites-developing/developer-mode.md#errors)**  — 發生問題時，會顯示每個元件的詳細資訊。

### 元件 {#components}

![chlimage_1-12](assets/chlimage_1-12.png)

這會顯示元件樹，其中包含：

* 概述在頁面上呈現的元件和範本鏈（SLY、JSP等）。 樹可以展開，以顯示階層內的內容。
* 顯示轉譯元件所需的伺服器端計算時間。
* 允許您展開樹並在樹中選擇特定元件。 「選擇」提供對元件詳細資訊的訪問；例如：

   * 儲存庫路徑
   * 指令碼連結(以CRXDE Lite存取)

* 選取的元件（在內容流程中，以藍色邊框表示）會在內容樹狀結構中反白顯示（反之亦然）。

這有助於：

* 決定並比較每個元件的轉譯時間。
* 請參閱並了解階層。
* 了解並改善頁面載入時間，方法是尋找緩慢的元件。

每個元件項目都可顯示（例如）:

![chlimage_1-13](assets/chlimage_1-13.png)

* **檢視詳細資料**:一個清單連結，其中顯示：

   * 用於呈現元件的所有元件指令碼。
   * 此特定元件的儲存庫內容路徑。

   ![chlimage_1-14](assets/chlimage_1-14.png)

* **編輯指令碼**:連結：

   * 以CRXDE Lite開啟元件指令碼。

* 展開元件輸入項（箭頭頭）也可以顯示：

   * 所選元件內的階層。
   * 單獨呈現所選元件、內嵌的任何個別元件以及合併總計的呈現時間。

   ![chlimage_1-15](assets/chlimage_1-15.png)

>[!CAUTION]
>
>有些連結指向下的指令碼 `/libs`. 不過，這些僅供參考，您 **不能** 在下面編輯任何內容 `/libs`，因為您所做的任何變更可能會遺失。 這是因為當您升級或套用Hotfix/Feature Pack時，此分支很可能會發生變更。 您需要的任何變更都應在 `/apps`，請參閱 [覆蓋和覆寫](/help/sites-developing/overlays.md).

### 錯誤 {#errors}

![chlimage_1-16](assets/chlimage_1-16.png)

希望 **錯誤** 標籤將一律為空白（如上所示），但當發生問題時，會針對每個元件顯示下列詳細資料：

* 如果元件將項目寫入錯誤記錄，以及錯誤的詳細資訊，並將連結導向CRXDE Lite內的適當程式碼，則會發出警告。
* 元件開啟管理工作階段時出現警告。

例如，在呼叫未定義方法的情況下，產生的錯誤會顯示在 **錯誤** 標籤：

![chlimage_1-17](assets/chlimage_1-17.png)

「元件」頁簽的樹中的元件條目在發生錯誤時也將用指示器標籤。

### 測試 {#tests}

>[!CAUTION]
>
>在AEM 6.2中，開發人員模式的測試功能已重新實作為獨立工具應用程式。
>
>如需完整詳細資訊，請參閱 [測試您的UI](/help/sites-developing/hobbes.md).
