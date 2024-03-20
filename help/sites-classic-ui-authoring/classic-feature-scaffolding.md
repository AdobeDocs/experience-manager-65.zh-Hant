---
title: 支架
description: 有時您可能需要建立大型頁面集，這些頁面具有共用結構但內容不同。 使用支架，您可以建立包含欄位的表單（支架），這些欄位會反映您想要用於頁面的結構，然後使用此表單以根據此結構輕鬆建立頁面。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
exl-id: 58e61302-cfb4-4a3d-98d4-3c92baa2ad42
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 0%

---

# 支架{#scaffolding}

有時您可能需要建立大型頁面集，這些頁面具有共用結構但內容不同。 透過標準Adobe Experience Manager (AEM)介面，您需要建立每個頁面、將適當的元件拖曳到頁面上，並個別填入每個元件。

使用支架，您可以建立包含欄位的表單（支架），這些欄位會反映您想要用於頁面的結構，然後使用此表單以根據此結構輕鬆建立頁面。

>[!NOTE]
>
>支架（在傳統UI中） [遵守MSM繼承](#scaffolding-with-msm-inheritance).

## 支架如何運作 {#how-scaffolding-works}

支架儲存在 **工具** 網站管理員的控制檯。

* 開啟 **工具** 主控台，然後按一下 **預設頁面支架**.
* 在此底下，按一下 **Geometrixx**.
* 在 **Geometrixx**，您會找到 *支架頁面* 已呼叫 **新聞**. 按兩下以開啟此頁面。

![howscaffolds_work](assets/howscaffolds_work.png)

支架包含一個表單，其中包含組成要建立頁面的每個內容片段的欄位，以及四個重要引數，可透過進行存取 **頁面屬性** 架構頁面的前面。

![pageprops](assets/pageprops.png)

支架頁面屬性包括：

* **標題文字**：這是此支架頁面本身的名稱。 在此範例中，它稱為「新聞」。
* **說明**：這會顯示在支架頁面上的標題下方。
* **目標範本**：這是此支架建立頁面時將使用的範本。 在此範例中，它是 *Geometrixx內容頁面* 範本。
* **目標路徑**：這是上層頁面的路徑，此支架會在此頁面下方建立頁面。 在此範例中，路徑為 */content/geometrixx/en/news*.

架構的正文即為形式。 當使用者希望使用支架建立頁面時，他填寫表單並按一下 *建立*，在底部。 在 **新聞** 表單上範例包含下列欄位：

* **標題**：這是要建立之頁面的名稱。 此欄位一律存在於每個支架上。
* **文字**：此欄位對應結果頁面上的文字元件。
* **影像**：此欄位對應結果頁面上的影像元件。
* **Image/Advanced**： **標題**：影像標題。
* **Image/Advanced**： **替代文字**：影像的替代文字。
* **Image/Advanced**： **說明**：影像的說明。
* **Image/Advanced**： **大小**：影像的大小。
* **標籤/關鍵字**：要指派給此頁面的中繼資料。 此欄位一律存在於每個支架上。

### 建立支架 {#creating-a-scaffold}

若要建立支架，請前往 **工具** 主控台，然後 **預設頁面支架** 並建立頁面。 單一頁面範本型別可供使用， *支架範本。*

前往 **頁面屬性** ，並將 *標題文字*， *說明*， *目標範本*、和 *目標路徑*，如上所述。

接下來，您必須定義此支架將建立的頁面結構。 若要這麼做，請前往 **[設計模式](/help/sites-authoring/page-authoring.md#sidekick)** 在支架頁面上。 隨即顯示連結，讓您編輯 **對話方塊編輯器**.

![cq5_dialog_editor](assets/cq5_dialog_editor.png)

使用對話方塊編輯器，您可以指定每次使用此支架建立新頁面時將建立的屬性。

架構的對話方塊定義與元件的定義運作方式類似(請參閱 [元件](/help/sites-developing/components.md))。 不過，還是有一些重要差異：

* 元件對話方塊定義會呈現為一般對話方塊（例如，顯示在對話方塊編輯器中間窗格中），而支架對話方塊定義雖然會在對話方塊編輯器中顯示為一般對話方塊，卻會在支架頁面上呈現為支架表單(如 **新聞** 上方的支架)。
* 元件對話方塊僅提供定義單一特定元件內容所需之值的欄位。 架構對話方塊必須為要建立之頁面的每個段落中的每個屬性提供欄位。
* 如果有元件對話方塊，則用來呈現指定內容的元件是隱含的，因此 `sling:resourceType` 段落的屬性會在段落建立時自動填入。 在架構中，為指定段落定義內容和指派元件的所有資訊都必須由對話方塊本身提供。 在架構對話方塊中，此資訊必須透過以下方式提供： *隱藏* 欄位，以便在建立頁面時提交此資訊。

檢視範例 **新聞** 對話方塊編輯器中的支架對話方塊有助於說明其運作方式。 在支架頁面上進入設計模式，然後按一下對話方塊編輯器連結。

現在，按一下對話方塊欄位 **對話方塊>定位點面板>文字>文字**，如下所示：

![textedit](assets/textedit.png)

此欄位的屬性清單會顯示在對話方塊編輯器的右側，如下所示：

![list_of_properties](assets/list_of_properties.png)

請注意此欄位的名稱屬性。 它具有值

`./jcr:content/par/text/text`

這是使用支架建立頁面時，此欄位內容將寫入的屬性名稱。 屬性是以節點的相對路徑來表示，代表要建立的頁面。 它指定節點文字下方的屬性文字，節點文字本身是頁面節點下方jcr：content節點的子節點。

這會定義將輸入至此欄位之文字的內容儲存位置。 不過，我們還需要為此內容指定兩個特性：

* 在此儲存的字串必須解譯為 *RTF文字*、和
* 應使用哪個元件來將此內容轉譯至產生的頁面。

在一般元件對話方塊中，您不必指定此資訊，因為對話方塊已繫結至特定元件是隱含的。

若要指定這兩個資訊，請使用隱藏欄位。 按一下第一個隱藏欄位 **對話方塊>索引標籤面板>文字>隱藏**，如下所示：

![隱藏](assets/hidden.png)

此隱藏欄位的屬性如下：

![hidden_list_props](assets/hidden_list_props.png)

此隱藏欄位的name屬性為

`./jcr:content/par/text/textIsRich`

這是布林值屬性，用來解譯儲存在中的文字字串 `./jcr:content/par/text/text`.

因為我們知道文字應該解譯為RTF文字，所以讓我們指定 `value` 此欄位的屬性為 `true`.

>[!CAUTION]
>
>對話方塊編輯器可讓使用者變更以下專案的值 *現有* 屬性。 若要新增屬性，使用者必須使用 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). 例如，使用對話方塊編輯器將新的隱藏欄位新增到對話方塊定義時，它沒有 *值* 屬性（即名稱為「value」的屬性）。 如果有問題的隱藏欄位需要設定預設值屬性，則必須使用其中一個CRX工具手動新增此屬性。 無法以對話方塊編輯器本身新增值。 不過，屬性一旦出現，您就可使用對話方塊編輯器來編輯其值。

第二個隱藏欄位可以按一下顯示，如下所示：

![hidden2](assets/hidden2.png)

此隱藏欄位的屬性如下：

![hidden_list_props2](assets/hidden_list_props2.png)

此隱藏欄位的name屬性為

`./jcr:content/par/text/sling:resourceType`

而且為此屬性指定的固定值為

`foundation/components/textimage`

這指定用於呈現此段落文字內容的元件為 *文字影像* 元件。 搭配使用 `isRichText` 在其他隱藏欄位中指定的布林值，元件可以轉譯實際儲存的文字字串 `./jcr:content/par/text/text` 以所需方式進行。

### 使用MSM繼承的支架 {#scaffolding-with-msm-inheritance}

在傳統UI中，支架與MSM繼承完全整合（如適用）。

當您在中開啟頁面時 **支架** 模式（使用sidekick底部的圖示）任何受繼承限制的元件將以下列方式指示：

* 鎖定符號（適用於大多數元件；例如，文字和標題）
* 包含文字的遮色片 **按一下以取消繼承** （適用於影像元件）

這些符號表示在取消繼承之前，無法編輯元件。

![chlimage_1](assets/chlimage_1.jpeg)

>[!NOTE]
>
>此專案與 [編輯頁面內容時繼承的元件](/help/sites-authoring/editing-content.md#inheritedcomponentsclassicui).

按一下鎖定符號或影像圖示可讓您中斷繼承：

* 符號會變更為開啟的掛鎖。
* 解鎖後，即可編輯內容。

![chlimage_1-1](assets/chlimage_1-1.jpeg)

解鎖後，您可以按一下解鎖的掛鎖符號來還原繼承 — 這會遺失您所做的任何編輯。

>[!NOTE]
>
>如果在頁面層級取消繼承（從「頁面屬性」的「即時副本」索引標籤），則所有元件都可在以下位置編輯： **支架** 模式（會以解除鎖定狀態顯示）。
