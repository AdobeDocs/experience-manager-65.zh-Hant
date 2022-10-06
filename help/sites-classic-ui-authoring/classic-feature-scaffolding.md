---
title: 支架
seo-title: Scaffolding
description: 有時候，您可能需要建立一組大型頁面，這些頁面共用相同的結構但內容不同。 透過支架，您可以建立表單（支架），其欄位可反映您想要的頁面結構，然後使用此表單根據此結構輕鬆建立頁面。
seo-description: Sometimes you may need to create a large set of pages that share the same structure but have differing content. With scaffolding you can create a form (a scaffold) with fields that reflect the structure you want for your pages and then use this form to easily create pages based on this structure.
uuid: 5904abc0-b256-4da4-a7d7-3c17ea299648
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: a63e5732-b1a3-4639-9838-652af401e788
docset: aem65
exl-id: 58e61302-cfb4-4a3d-98d4-3c92baa2ad42
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1448'
ht-degree: 0%

---

# 支架{#scaffolding}

有時候，您可能需要建立一組大型頁面，這些頁面共用相同的結構但內容不同。 透過標準AEM介面，您需要建立每個頁面、將適當的元件拖曳至頁面上，並個別填入每個頁面。

透過支架，您可以建立表單（支架），其欄位可反映您想要的頁面結構，然後使用此表單根據此結構輕鬆建立頁面。

>[!NOTE]
>
>支架（在傳統UI中） [尊重MSM繼承](#scaffolding-with-msm-inheritance).

## 支架的運作方式 {#how-scaffolding-works}

支架儲存在 **工具** 網站管理員的主控台。

* 開啟 **工具** 主控台，然後按一下 **預設頁面支架**.
* 在此下，按一下 **geometrixx**.
* 在 **geometrixx** 你會找到 *架構頁面* 呼叫 **新聞**. 按兩下以開啟此頁面。

![howscaffold_work](assets/howscaffolds_work.png)

架構由表單組成，其中包含將組成要建立之頁面之每個內容片段的欄位，以及可透過 **頁面屬性** 框架頁面的URL。

![pageprops](assets/pageprops.png)

支架頁面屬性包括：

* **標題文字**:這是這個腳手架頁面本身的名稱。 在此範例中，它稱為「News」。
* **說明**:這會顯示在支架頁面的標題下方。
* **目標範本**:這是此架構建立新頁面時將使用的範本。 在此範例中，它是 *Geometrrixx內容頁面* 範本。
* **目標路徑**:這是上層頁面的路徑，此架構會在其下建立新頁面。 在此範例中，路徑為 */content/geometrixx/en/news*.

腳手架的身體是形狀。 當使用者想要使用架構來建立頁面時，他會填寫表單並點按 *建立*，位於底部。 在 **新聞** 上方的範例包含下列欄位：

* **標題**:這是要建立的頁面的名稱。 此欄位一律存在於每個架構上。
* **文字**:此欄位對應至產生頁面上的文字元件。
* **影像**:此欄位對應至產生頁面上的影像元件。
* **影像/進階**: **標題**:影像的標題。
* **影像/進階**: **替代文字**:影像的替代文字。
* **影像/進階**: **說明**:影像的說明。
* **影像/進階**: **大小**:影像的大小。
* **標籤/關鍵字**:要指派給此頁面的中繼資料。 此欄位一律存在於每個架構上。

### 建立架構 {#creating-a-scaffold}

若要建立新架構，請前往 **工具** 控制台，然後 **預設頁面支架** 並建立新頁面。 將提供單頁範本類型， *腳手架模板。*

前往 **頁面屬性** ，並將 *標題文字*, *說明*, *目標範本* 和 *目標路徑*，如上所述。

接下來，您必須定義此架構將建立的頁面結構。 若要這麼做，請進 **[設計模式](/help/sites-authoring/page-authoring.md#sidekick)** 在架構頁面上。 隨即出現連結，可讓您編輯 **對話編輯器**.

![cq5_dialog_editor](assets/cq5_dialog_editor.png)

使用對話框編輯器，可指定每次使用此架構建立新頁時將建立的屬性。

架構的對話方塊定義的運作方式與元件的對話方塊類似(請參閱 [元件](/help/sites-developing/components.md))。 但有幾項重要差異適用：

* 元件對話框定義呈現為普通對話框（如對話框編輯器的中間窗格中所示），架構對話框定義（儘管它們在對話框編輯器中顯示為普通對話框）在架構頁上呈現為架構表單(如 **新聞** 支架)。
* 元件對話方塊僅提供定義單一特定元件內容所需之值的欄位。 架構對話方塊必須提供要建立之頁面每個段落中每個屬性的欄位。
* 在元件對話方塊中，用於轉譯指定內容的元件為隱式，因此 `sling:resourceType` 在建立段落時自動填充段落的屬性。 使用框架時，必須由對話框本身提供定義給定段落的內容和指定元件的所有資訊。 在架構對話方塊中，必須使用 *隱藏* 欄位，在建立頁面時提交此資訊。

看看這個例子 **新聞** 對話方塊編輯器中的架構對話方塊有助於說明此作法的運作方式。 進入架構頁面上的設計模式，然後按一下對話方塊編輯器連結。

現在，按一下對話方塊欄位 **「對話框」>「頁簽面板」>「文本」>「文本」**，如下所示：

![textedit](assets/textedit.png)

此欄位的屬性清單將顯示在對話方塊編輯器的右側，如下所示：

![list_of_properties](assets/list_of_properties.png)

請注意此欄位的名稱屬性。 它有值

`./jcr:content/par/text/text`

這是屬性的名稱，當使用架構建立頁面時，此欄位的內容將寫入此屬性的名稱。 屬性會以代表要建立之頁面之節點的相對路徑來表示。 它會指定位於節點文字下方的屬性文字，該文字位於節點部分之下，節點部分本身是頁面節點下方jcr:content節點的子節點。

這定義將輸入到此欄位的文字的內容儲存位置。 不過，我們還需要為此內容指定另外兩個特性：

* 此處儲存的字串必須解譯為 *富文本*，和
* 應使用哪個元件將此內容呈現至產生的頁面。

請注意，在正常元件對話框中，您不必指定此資訊，因為該資訊隱含在該對話框已綁定到特定元件的事實中。

要指定使用隱藏欄位的這兩個資訊。 按一下第一個隱藏欄位 **對話框>頁簽面板>文本>隱藏**，如下所示：

![隱藏](assets/hidden.png)

此隱藏欄位的屬性如下：

![hidden_list_props](assets/hidden_list_props.png)

此隱藏欄位的名稱屬性為

`./jcr:content/par/text/textIsRich`

這是布林屬性，用於解譯儲存在的文字字串 `./jcr:content/par/text/text`.

因為我們知道文字應該解讀為RTF，我們會指定 `value` 此欄位的屬性為 `true`.

>[!CAUTION]
>
>對話方塊編輯器可讓使用者變更 *現有* 屬性。 若要新增屬性，使用者必須使用 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). 例如，當使用對話框編輯器將新隱藏欄位添加到對話框定義時，它沒有 *value* 屬性（亦即名稱為「value」的屬性）。 如果相關的隱藏欄位需要預設值 *value* 屬性，則必須使用其中一個CRX工具手動新增此屬性。 無法將值與對話方塊編輯器本身一起新增。 不過，一旦屬性存在，就可以使用對話方塊編輯器編輯其值。

按一下第二個隱藏欄位即可看到，如下所示：

![hidden2](assets/hidden2.png)

此隱藏欄位的屬性如下：

![hidden_list_props2](assets/hidden_list_props2.png)

此隱藏欄位的名稱屬性為

`./jcr:content/par/text/sling:resourceType`

而為此屬性指定的固定值為

`foundation/components/textimage`

這指定用於呈現此段落的文本內容的元件為 *文字影像* 元件。 搭配使用 `isRichText` 在其他隱藏欄位中指定的布林值，元件可以呈現儲存在的實際文字字串 `./jcr:content/par/text/text` 以所需的方式。

### 具有MSM繼承的支架 {#scaffolding-with-msm-inheritance}

在傳統UI中，架構會與MSM繼承（若適用）完全整合。

當您在 **支架** 模式（使用sidekick底部的圖示）接受繼承的任何元件都會以：

* 鎖定符號(對於大多數元件；例如文字和標題)
* 帶有文字的遮罩 **按一下可取消繼承** （適用於影像元件）

這顯示在取消繼承前，無法編輯元件。

![chlimage_1](assets/chlimage_1.jpeg)

>[!NOTE]
>
>這可與 [編輯頁面內容時繼承的元件](/help/sites-authoring/editing-content.md#inheritedcomponentsclassicui).

按一下鎖定符號或影像圖示可讓您中斷繼承：

* 符號將更改為開啟的掛鎖。
* 解除鎖定後，您就可以編輯內容。

![chlimage_1-1](assets/chlimage_1-1.jpeg)

解鎖後，按一下解鎖的掛鎖符號可以恢復繼承 — 這將丟失您所做的任何編輯。

>[!NOTE]
>
>如果在頁面層級取消繼承（來自「頁面屬性」的「Livecopy」索引標籤），則所有元件都可在 **支架** 模式（它們將顯示為未鎖定狀態）。
