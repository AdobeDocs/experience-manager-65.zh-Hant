---
title: 社區元件指南
seo-title: Community Components Guide
description: 一種互動式開發工具，用於啟動社會構成框架
seo-description: An interactive development tool to get started with the social component framework (SCF)
uuid: 120e56d1-b93c-4f92-bab4-6bb5e40e0ddf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a777a3f1-b39f-4d90-b9b6-02d3e321a86f
exl-id: 12c0eae5-fd76-4480-a012-25d3312f3570
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 2%

---

# 社區元件指南  {#community-components-guide}

「社區元件」指南是 [社會構成框架](scf.md)。 它提供了可用的AEM Communities元件或由多個元件構建的更複雜功能的清單。

除了每個元件的基本資訊，本指南還允許您嘗試SCF元件/功能的工作方式以及如何配置或定制它們。

有關與每個元件相關的開發要素的資訊，請參見 [功能和元件要素](essentials.md)。

## 快速入門 {#getting-started}

本指南用於作者(localhost:4502)和發佈(localhost:4503)實例的開發安裝。

通過瀏覽訪問「社區元件」站點

* [https://&lt;server>:&lt;port>/content/community-components/en.html](http://localhost:4502/content/community-components/en.html)

與社區元件的交互會因以下情況而異：

* 伺服器（作者或發佈）。
* 站點訪問者是否已登錄。
* 如果已登錄，則分配給成員的權限。
* 無論預設SRP是否為 [JSRP](jsrp.md)中。

在作者中，要進入編輯模式，請插入 `editor.html` 或 `cf#` 作為伺服器名後的第一個路徑段：

* 標準 UI:

   [https://&lt;server>:&lt;port>/editor.html/content/community-components/en.html](http://localhost:4502/editor.html/content/community-components/en.html)

* 傳統 UI:

   [https://&lt;server>:&lt;port>/cf#/content/community-components/en.html](http://localhost:4502/cf#/content/community-components/en.html)

>[!NOTE]
>
>在「編輯」模式下，在作者中，頁面上的連結不處於活動狀態。
>
>要導航到元件頁，請首先選擇「預覽」模式以激活連結。
>
>在瀏覽器中顯示元件頁面時，返回「編輯」模式以開啟元件的編輯對話框。
>
>有關一般創作資訊，請查看 [創作頁面的快速指南](../../help/sites-authoring/qg-page-authoring.md)。
>
>如果不熟悉AEM，請查看 [基本處理](../../help/sites-authoring/basic-handling.md)。

### 首頁 {#home-page}

指南提供了可用於沿頁面左側預覽和原型製作的SCF元件清單。

在「編輯」模式下在作者實例上查看的元件指南：

![community-component1](assets/community-component1.png)

## 元件頁 {#component-pages}

從頁面左側的清單中選擇一個元件。

![社區元件頁](assets/community-component2.png)

嚮導的主體顯示：

1. 標題：所選元件的名稱
1. [客戶端庫](#client-side-libraries):一個或多個必需類別的清單
1. [可包含](scf.md#add-or-include-a-communities-component):如果元件可以動態包含，則可以在作者編輯模式下切換狀態：

   * 如果添加，則顯示的文本為：&quot;此元件通過其par節點包含。&quot;
   * 如果包括，則顯示的文本為：&quot;此元件是動態包含的。&quot;
   * 如果不包括，則不顯示任何文本

1. 示例元件或特徵：元件或特徵的活動實例。 如果元件，則可以隨對頁籤部分中提供的模板、CSS和資料所做的更改而更改。

>[!NOTE]
>
>從左側進行選擇後，當瀏覽器窗口太窄時，元件將出現在元件清單的下方，而不是旁邊。

### 作者交互 {#author-interactions}

在作者實例上使用指南時，可以通過開啟元件對話框來體驗配置元件的過程。 在中提供開發人員資訊 [元件和功能要件](essentials.md) 對話框設定中 [社區元件](author-communities.md) 的下界。

對於「社區元件」指南，某些元件對話框設定與 [可包含](scf.md#add-or-include-a-communities-component) 切換狀態。 要在使用現有資源或動態包含的資源之間切換，請在編輯模式下選擇元件和可包含文本，然後按兩下以開啟編輯對話框：

![community-component3](assets/community-component3.png)

在 **模板** 頁籤：

![community-component4](assets/community-component4.png)

* **包含 sling:include 的子元件**

   如果未選中，則《元件指南》將使用儲存庫中的現有資源（jcr節點，它是par節點的子節點）。

   * 顯示的文本：&quot;此元件通過其par節點包含。&quot;

   如果選中，則《元件指南》將使用sling動態地包括子節點的resourceType（非現有資源）的元件。

   * 顯示的文本：&quot;此元件是動態包含的。&quot;

   未選中預設值。

### 發佈交互 {#publish-interactions}

在發佈實例上使用指南時，可以作為站點訪問者（未登錄）和登錄時具有各種權限的成員體驗元件和功能。

>[!NOTE]
>
>請注意，如果SRP預設為 [JSRP](jsrp.md)，則在發佈實例上輸入的UGC將僅在發佈時可見，並且 *不* 從 [緩和](moderate-ugc.md) 對作者實例的控制台。

## 用戶端資源庫 {#client-side-libraries}

每個元件的客戶端庫（客戶端庫）是 *要求* 將元件置於頁面上時引用。 客戶端提供了管理和優化用於在瀏覽器中呈現元件的Javascript和CSS的下載的方法。

有關詳細資訊，請訪問 [社區元件的客戶端](clientlibs.md)。

## 模擬 {#impersonation}

在作者實例上，其中一個用戶通常以管理員或開發人員身份登錄，為了體驗以其他用戶身份登錄的元件，請使用左側的文本框 **[!UICONTROL 模擬]** 按鈕，然後按一下按鈕。 按一下「還原」以註銷並結束模擬。

發佈實例不需要模擬。 只需使用「登錄/註銷」連結模擬各種用戶，如 [演示用戶](tutorials.md#demo-users)。

## 自定義 {#customization}

啟用後，每個SCF元件都可以通過臨時修改元件的模板、CSS和資料來為可能的自定義建立原型。

### 啟用自定義 {#enabling-customization}

>[!NOTE]
>
>**此工具為只讀**。 對模板、CSS或資料所做的任何編輯都不會保存到儲存庫中。

要快速實驗定制， `scg:showIde`必須將屬性添加到元件頁的內容JCR節點中，並設定為true。

以注釋元件為例，在作者或發佈實例上使用管理員權限登錄：

1. 瀏覽到 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)

   比如說， [http://localhost:4503/crx/de](http://localhost:4503/crx/de)

1. 選擇元件的 `jcr:content` 節點

   例如 `/content/community-components/en/comments/jcr:content`

1. 添加屬性

   * **名稱** `scg:showIde`
   * **類型** `String`
   * **值** `true`

1. 選擇 **[!UICONTROL 全部保存]**
1. 在指南中重新載入「注釋」頁

   [http://localhost:4503/content/community-components/en/comments.html](http://localhost:4503/content/community-components/en/comments.html)

1. 請注意，現在有3個用於「模板」、「CSS」和「資料」的頁籤。

![community-component5](assets/community-component5.png)

![community-component6](assets/community-component6.png)

### 模板頁籤 {#templates-tab}

選擇「模板」頁籤以查看與元件關聯的模板。

「模板編輯器」允許編譯本地編輯並將其應用於頁面頂部的示例元件實例，而不會影響儲存庫中的元件。

在本地編輯時運行編譯將突出顯示所有錯誤，方法是在邊欄中放置一個點，並將文本標籤為紅色。

### CSS頁籤 {#css-tab}

選擇「CSS」頁籤以查看與元件關聯的CSS。

如果元件是多個元件的組合，則某些CSS可能列在其它元件之一下。

CSS編輯器允許修改CSS並將其應用於頁面頂部的示例元件實例。

可通過按一下邊框中規則旁邊的規則來選擇規則，以使用該規則突出顯示DOM的部分。

### 資料頁籤 {#data-tab}

選擇「資料」頁籤以顯示.social.json終結點資料。 此資料是可編輯的，並應用於示例元件實例。

語法錯誤可以標籤在邊欄中，也可以在編輯器中突出顯示。
