---
title: 開發人員模式
description: 開發人員模式會開啟一個側面板，其中包含數個標籤，為開發人員提供目前頁面的相關資訊。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
exl-id: aef0350f-4d3d-47f4-9c7e-5675efef65d9
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 3%

---

# 開發人員模式{#developer-mode}

在Adobe Experience Manager (AEM)中編輯頁面時，有數種[模式](/help/sites-authoring/author-environment-tools.md#modestouchoptimizedui)可供使用，包括開發人員模式。 這會開啟一個側面板，內含數個標籤，為開發人員提供目前頁面的相關資訊。 這三個索引標籤為：

* **[元件](#components)**&#x200B;以檢視結構和效能資訊。
* **[測試](#tests)**&#x200B;以執行測試並分析結果。
* **[錯誤](#errors)**，檢視發生的任何問題。

這些功能可協助開發人員：

* 探索：組成頁面的專案。
* 偵錯：隨時隨地發生的狀況，進而協助解決問題。
* 測試：應用程式行為是否符合預期。

>[!CAUTION]
>
>開發人員模式：
>
>* 僅適用於觸控式UI （編輯頁面時）。
>* 在行動裝置或桌上型電腦的小型視窗上無法使用（由於空間限制）。
>
>   * 當寬度小於1024畫素時，就會發生這種情況。
>* 僅適用於`administrators`群組成員的使用者。

>[!CAUTION]
>
>開發人員模式僅適用於未使用nosamplecontent執行模式的標準制作執行個體。
>
>如有必要，可將其設定以供使用：
>
>* 在使用nosamplecontent執行模式的作者執行個體上
>* 發佈執行個體
>
>使用後應再次停用。

>[!NOTE]
>
>請參閱：
>
>* 知識庫文章，[疑難排解AEM TouchUI問題](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html)，以取得進一步的提示和工具。
>* 關於[AEM 6.0 Developer Mode](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2014/aem-developer-mode.html?lang=zh-Hant)的AEM Gems工作階段。
>

## 開啟開發人員模式 {#opening-developer-mode}

開發人員模式會實作為頁面編輯器的側面板。 若要開啟面板，請從頁面編輯器工具列的模式選取器中選取&#x200B;**開發人員**：

![chlimage_1-11](assets/chlimage_1-11.png)

面板分為兩個標籤：

* **[元件](/help/sites-developing/developer-mode.md#components)** — 這會顯示元件樹狀結構，類似於作者的[內容樹狀結構](/help/sites-authoring/author-environment-tools.md#content-tree)

* **[錯誤](/help/sites-developing/developer-mode.md#errors)** — 發生問題時，會顯示每個元件的詳細資料。

### 元件 {#components}

![chlimage_1-12](assets/chlimage_1-12.png)

這會顯示符合下列條件的元件樹狀結構：

* 概述元件鏈和在頁面上呈現的範本（SLY、JSP等）。 可展開樹狀結構以顯示階層內的前後關聯。
* 顯示呈現元件的伺服器端運算時間。
* 可讓您展開樹狀結構並選取樹狀結構中的特定元件。 選取範圍提供元件詳細資料的存取權，例如：

   * 存放庫路徑
   * 指令碼連結(在CRXDE Lite中存取)

* 選取的元件（在內容流程中，以藍色邊框表示）將在內容樹狀結構中反白顯示（反之亦然）。

這有助於：

* 決定並比較每個元件的演算時間。
* 檢視並瞭解階層。
* 找出緩慢的元件，瞭解並改善頁面載入時間。

每個元件專案都可顯示（例如）：

![chlimage_1-13](assets/chlimage_1-13.png)

* **檢視詳細資料**：顯示下列專案的清單連結：

   * 用於呈現元件的所有元件指令碼。
   * 此特定元件的存放庫內容路徑。

  ![chlimage_1-14](assets/chlimage_1-14.png)

* **編輯指令碼**：連結：

   * 以CRXDE Lite開啟元件指令碼。

* 展開元件專案（箭頭標頭）也可顯示：

   * 所選元件內的階層。
   * 所選元件的單獨呈現時間、巢狀內嵌的任何個別元件，以及合併總數。

  ![chlimage_1-15](assets/chlimage_1-15.png)

>[!CAUTION]
>
>部分連結指向`/libs`下的指令碼。 不過，這些僅供參考，您&#x200B;**不得**&#x200B;編輯`/libs`下的任何專案，因為您所做的任何變更可能會遺失。 這是因為每當您升級或套用Hotfix或Feature Pack時，此分支很容易發生變更。 進行您在`/apps`下所需的任何變更。 請參閱[覆蓋和覆寫](/help/sites-developing/overlays.md)。

### 錯誤次數 {#errors}

![chlimage_1-16](assets/chlimage_1-16.png)

希望&#x200B;**錯誤**&#x200B;索引標籤永遠是空的（如上所述），但是當問題發生時，會顯示每個元件的下列詳細資料：

* 如果元件將專案寫入錯誤記錄檔，連同錯誤的詳細資訊以及指向CRXDE Lite內適當程式碼的直接連結，會出現警告。
* 如果元件開啟管理員工作階段，會出現警告。

例如，在呼叫未定義的方法的情況下，產生的錯誤會顯示在&#x200B;**錯誤**&#x200B;索引標籤中：

![chlimage_1-17](assets/chlimage_1-17.png)

當發生錯誤時，「元件」標籤樹狀結構中的元件專案也會標示一個指示器。

### 測試 {#tests}

>[!CAUTION]
>
>在AEM 6.2中，開發人員模式的測試功能已重新實作為獨立的工具應用程式。
>
>如需完整詳細資訊，請參閱[測試您的UI](/help/sites-developing/hobbes.md)。
