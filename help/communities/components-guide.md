---
title: 社群元件指南
description: 開始使用社交元件架構(SCF)的互動式開發工具
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 12c0eae5-fd76-4480-a012-25d3312f3570
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 0%

---

# 社群元件指南  {#community-components-guide}

社群元件指南是互動式開發工具，適用於 [社交元件架構(SCF)](scf.md). 它提供可用的Adobe Experience Manager (AEM) Communities元件清單，或由多個元件建置的更複雜功能。

除了每個元件的基本資訊外，本指南還允許實驗SCF元件/功能的工作方式，以及如何對其進行設定或自訂。

如需與每個元件相關的開發要件的相關資訊，請參閱 [功能和元件要點](essentials.md).

## 快速入門 {#getting-started}

本指南適用於製作執行個體(localhost：4502)和發佈執行個體(localhost：4503)的開發安裝。

社群元件網站可透過瀏覽存取：

* [https://&lt;server>：&lt;port>/content/community-components/en.html](http://localhost:4502/content/community-components/en.html)

與Communities元件的互動會依據以下因素而有所不同：

* 伺服器（製作或發佈）。
* 網站訪客是否已登入。
* 如果登入，則為成員指派許可權。
* 預設SRP、 [JSRP](jsrp.md)，正在使用中。

在作者上，若要進入編輯模式，請插入 `editor.html` 或 `cf#` 做為伺服器名稱之後的第一個路徑區段：

* 標準UI：

  [https://&lt;server>：&lt;port>/editor.html/content/community-components/en.html](http://localhost:4502/editor.html/content/community-components/en.html)

* 傳統UI：

  [https://&lt;server>：&lt;port>/cf#/content/community-components/en.html](http://localhost:4502/cf#/content/community-components/en.html)

>[!NOTE]
>
>在編輯模式下的作者上，頁面上的連結非作用中。
>
>若要導覽至元件頁面，請先選取預覽模式以啟動連結。
>
>在瀏覽器中顯示元件頁面後，返回「編輯」模式以開啟元件的編輯對話方塊。
>
>如需一般撰寫資訊，請檢視 [製作頁面的快速指南](../../help/sites-authoring/qg-page-authoring.md).
>
>若不熟悉AEM，請檢視相關的檔案： [基本處理](../../help/sites-authoring/basic-handling.md).

### 首頁 {#home-page}

本指南提供可在頁面左側預覽及建立原型的SCF元件清單。

在編輯模式中的作者執行個體所檢視的元件指南：

![community-component1](assets/community-component1.png)

## 元件頁面 {#component-pages}

從頁面左側的清單中選取元件。

![社群 — 元件 — 頁面](assets/community-component2.png)

指南的主體隨即顯示：

1. 標題：所選元件的名稱
1. [使用者端資料庫](#client-side-libraries)：一或多個必要類別的清單
1. [包含](scf.md#add-or-include-a-communities-component)：如果可動態包含元件，則可在作者編輯模式中切換狀態：

   * 如果新增，顯示的文字為：「此元件透過其par節點包含。」
   * 如果包含，顯示的文字會是：「此元件是以動態方式包含。」
   * 如果不可包含，則不會顯示任何文字

1. 範例元件或特徵：元件或特徵的活動例證。 如果元件，可能會隨著對索引標籤區段中提供的範本、CSS和資料所做的變更而變更。

>[!NOTE]
>
>從左側進行選取後，當瀏覽器視窗太窄時，元件會顯示在元件清單的下方，而不是旁邊。

### 作者互動 {#author-interactions}

在製作例項上使用指南時，可以透過開啟對話方塊來體驗設定元件的方式。 有關開發人員的資訊，請參閱 [元件和功能要點](essentials.md) 區段，對話方塊設定則在中說明 [Communities元件](author-communities.md) 區段供作者使用。

在社群元件指南中，有些元件對話方塊設定會以 [包含](scf.md#add-or-include-a-communities-component) 切換狀態。 若要在使用現有資源或動態包含的資源之間切換，請在編輯模式中選取元件和可包含的文字，然後按兩下以開啟編輯對話方塊：

![community-component3](assets/community-component3.png)

在 **範本** 標籤：

![community-component4](assets/community-component4.png)

* **使用sling：include包含子元件**

  如果取消勾選，「元件指南」會使用存放庫中的現有資源（jcr節點，是par節點的子節點）。

   * 文字顯示為：「透過其par節點包含此元件」。

  如果勾選，「元件指南」會使用Sling來動態包含子節點的resourceType （非現有資源）的元件。

   * 文字顯示為：「此元件為動態包含。」

  預設為未勾選。

### 發佈互動 {#publish-interactions}

在發佈執行個體上使用指南時，元件和功能可能會以網站訪客（未登入）及具有各種許可權的成員身分在登入時體驗。

>[!NOTE]
>
>請注意，如果SRP預設為 [JSRP](jsrp.md)，則在發佈執行個體上輸入的UGC將只會顯示在發佈上，而且 *非* 可從以下位置看到： [稽核](moderate-ugc.md) 作者執行個體上的主控台。

## 用戶端資源庫 {#client-side-libraries}

針對每個元件所列出的使用者端資料庫(clientlibs)即為 *必填* 將元件放置到頁面上時要參考的。 clientlibs提供一種方法，用於管理和最佳化瀏覽器中用於呈現元件的JavaScript和CSS的下載。

如需詳細資訊，請造訪 [適用於社群元件的Clientlibs](clientlibs.md).

## 模擬 {#impersonation}

在作者執行個體上，如果使用者通常是以管理員或開發人員的身分登入，若要以其他使用者的身分體驗元件，請使用 **[!UICONTROL 模擬]** 按鈕以輸入使用者名稱或從下拉式清單中選取，然後按一下按鈕。 按一下「回覆」以登出並結束模擬。

發佈執行個體不需要模擬。 只要使用登入/登出連結來模擬各種使用者即可，例如 [示範使用者](tutorials.md#demo-users).

## 自訂 {#customization}

啟用後，每個SCF元件都可暫時修改元件的範本、CSS和資料，以建立可能自訂專案的原型。

### 啟用自訂 {#enabling-customization}

>[!NOTE]
>
>**此工具為唯讀**. 對範本、CSS或資料所做的任何編輯都不會儲存至存放庫。

若要快速實驗自訂，請 `scg:showIde`屬性必須新增至元件頁面的內容JCR節點，並設定為true。

以comments元件為例，在作者或發佈執行個體上，以管理員許可權登入：

1. 瀏覽至 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)

   例如， [http://localhost:4503/crx/de](http://localhost:4503/crx/de)

1. 選取元件的 `jcr:content` 節點

   例如 `/content/community-components/en/comments/jcr:content`

1. 新增屬性

   * **名稱** `scg:showIde`
   * **型別** `String`
   * **值** `true`

1. 選取 **[!UICONTROL 全部儲存]**
1. 重新載入指南中的「註解」頁面

   [http://localhost:4503/content/community-components/en/comments.html](http://localhost:4503/content/community-components/en/comments.html)

1. 請注意，範本、CSS和資料現在有三個索引標籤。

![community-component5](assets/community-component5.png)

![community-component6](assets/community-component6.png)

### 範本標籤 {#templates-tab}

選取範本標籤以檢視與元件相關聯的範本。

範本編輯器可以編譯本機編輯，並將其套用至頁面頂端的範例元件例項，而不會影響存放庫中的元件。

在本機編輯時執行編譯，將透過在排水槽中放置點並將文字標示為紅色來反白顯示任何錯誤。

### CSS索引標籤 {#css-tab}

選取CSS標籤以檢視與元件相關聯的CSS。

如果元件是由多個元件組成的複合專案，則某些CSS可能會列在其他某個元件下。

CSS編輯器可以修改CSS，並將其套用至頁面頂端的範例元件例項。

您可以按一下溝渠中規則旁的按鈕，選取規則來反白使用該規則的DOM部分。

### 資料標籤 {#data-tab}

選取「資料」標籤，以顯示.social.json端點資料。 此資料可編輯，並套用至範例元件例項。

語法錯誤可能會在Gutter中標示並在編輯器中反白顯示。
