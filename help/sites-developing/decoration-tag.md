---
title: 裝飾標籤
seo-title: 裝飾標籤
description: 當轉譯網頁中的元件時，可產生HTML元素，並將轉譯的元件包裝在其中。 對於開發人員，AEM提供清晰簡單的邏輯，來控制包含元件的裝飾標籤。
seo-description: 當轉譯網頁中的元件時，可產生HTML元素，並將轉譯的元件包裝在其中。 對於開發人員，AEM提供清晰簡單的邏輯，來控制包含元件的裝飾標籤。
uuid: db796a22-b053-48dd-a50c-354dead7e8ec
contentOwner: user
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 8cb9fd6e-5e1f-43cd-8121-b490dee8c2be
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835

---


# 裝飾標籤{#decoration-tag}

>[!NOTE]
>
>本文中描述的裝飾標籤行為和選項都以 [AEM 6.3 CFP1為基礎](https://helpx.adobe.com/experience-manager/release-notes--aem-6-3-cumulative-fix-pack.html)。
>
>CFP1之前6.3中裝飾標籤的行為與AEM 6.2類似。

當轉譯網頁中的元件時，可產生HTML元素，並將轉譯的元件包裝在其中。 這主要有兩個目的：

* 元件只有在用HTML元素包住時才能編輯。
* 包裝元素用於套用HTML類別，提供：

   * 版面資訊
   * 樣式資訊

對於開發人員，AEM提供清晰簡單的邏輯，來控制包含元件的裝飾標籤。 裝飾標籤的呈現方式和呈現方式是由兩個因素的組合所定義，本頁將深入探討：

* 元件本身可以使用一組屬性來設定其裝飾標籤。
* 包含元件（HTL、JSP、dispatcher等）的指令碼可以定義包含參數的裝飾標籤。

## 建議 {#recommendations}

以下是一些一般建議，說明何時加入包裝函式元素，以協助避免遇到非預期問題：

* WCMModes（編輯或預覽模式）、例項（作者或發佈）或環境（測試或生產）之間包裝函式元素的存在不應有所不同，因此頁面的CSS和JavaScripts在所有情況下都會運作相同。
* 應將包裝函式元素新增至所有可編輯的元件，讓頁面編輯器能夠正確初始化和更新這些元件。
* 對於不可編輯的元件，如果包裝器元素不提供特定函式，則可以避免它，因此產生的標籤不會不必要地膨脹。

## 元件控制項 {#component-controls}

下列屬性和節點可套用至元件，以控制其裝飾標籤的行為：

* **`cq:noDecoration {boolean}`**:此屬性可新增至元件，而true值會強制AEM不在元件上產生任何包裝函式元素。

* **`cq:htmlTag`**節點：此節點可以添加到元件下，並具有以下屬性：

   * **`cq:tagName {String}`**:這可用來指定自訂HTML標籤，以用於封裝元件，而非預設DIV元素。
   * **`class {String}`**:這可用來指定要新增至包裝函式的css類別名稱。
   * 其他屬性名稱將會新增為HTML屬性，其字串值與提供的相同。

## 指令碼控制項 {#script-controls}

但是，包裝函式行為會因 [為使用HTL](/help/sites-developing/decoration-tag.md#htl)[或JSP](/help/sites-developing/decoration-tag.md#jsp) 來包含元素而有所不同。

### HTL {#htl}

一般而言，HTL中的包裝函式行為可歸納為：

* 預設情況下不會呈現包裝函式DIV(僅執行時 `data-sly-resource="foo"`)。
* 所有wcm模式（停用、預覽、編輯作者和發佈）的演算都相同。

包裝函式的行為也可以完全控制。

* HTL指令碼可完全控制包裝函式標籤的產生行為。
* 元件屬性( `cq:noDecoration` 如 `cq:tagName`和)也可以定義包裝函式標籤。

您可以完全控制來自HTL指令碼的包裝函式標籤及其相關邏輯的行為。

如需在HTL中開發的詳細資訊，請參閱 [HTL檔案](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html)。

#### 決策樹 {#decision-tree}

此決策樹匯總了決定包裝函式標籤行為的邏輯。

![chlimage_1-75](assets/chlimage_1-75a.png)

#### 使用案例 {#use-cases}

以下三個使用案例提供如何處理包裝函式標籤的範例，並說明控制包裝函式標籤的所需行為有多簡單。

以下所有範例都採用下列內容結構和元件：

```
/content/test/
  @resourceType = "test/components/one"
  child/
    @resourceType = "test/components/two"
```

```
/apps/test/components/
  one/
    one.html
  two/
    two.html
    cq:htmlTag/
      @cq:tagName = "article"
      @class = "component-two"
```

#### 使用案例1:包含要重複使用程式碼的元件 {#use-case-include-a-component-for-code-reuse}

最典型的使用案例是，元件由於程式碼重複使用的原因而包含其他元件。 在這種情況下，所包含的元件不需要使用其專屬的工具列和對話方塊進行編輯，因此不需要包裝函式，而會忽略元 `cq:htmlTag` 件的介面。 這可視為預設行為。

`one.html: <sly data-sly-resource="child"></sly>`

`two.html: Hello World!`

產生輸出 `/content/test.html`於：

**`Hello World!`**

例如，一個元件包括用於顯示影像的核心影像元件，通常在這種情況下，該元件使用合成資源，該合成資源包括通過將表示元件將擁有的所有屬性的Map對象傳遞到資料透明資源來包括虛擬子元件。

#### 使用案例2:包含可編輯的元件 {#use-case-include-an-editable-component}

另一個常見使用案例是容器元件包含可編輯的子元件時，例如「版面容器」。 在這種情況下，每個包含的子代都必須有一個包裝函式，才能讓編輯器正常運作（除非在屬性中明確停用）。 `cq:noDecoration`

由於內含的元件在此範例中為獨立元件，因此需要有包裝函式元素讓編輯器運作，並定義其版面配置和樣式以套用。 要觸發這種行為，有一個選 `decoration=true` 項。

`one.html: <sly data-sly-resource="${'child' @ decoration=true}"></sly>`

`two.html: Hello World!`

產生輸出 `/content/test.html`於：

**`<article class="component-two">Hello World!</article>`**

#### 使用案例3:自訂行為 {#use-case-custom-behavior}

HTL可以明確提供以下資訊，因此可以很容易地實現任意數量的複雜情況：

* **`decorationTagName='ELEMENT_NAME'`** 定義包裝函式的元素名稱。
* **`cssClassName='CLASS_NAME'`** 要定義要在其上設定的CSS類名。

`one.html: <sly data-sly-resource="${'child' @ decorationTagName='aside', cssClassName='child'}"></sly>`

`two.html: Hello World!`

結果輸 `/content/test.html`出：

**`<aside class="child">Hello World!</aside>`**

## JSP {#jsp}

使用e或加入元 `cq:includ`件時 `sling:include`,AEM的預設行為是使用DIV來包覆元素。 不過，此包裝可透過兩種方式自訂：

* 明確告訴AEM不要使用包裝元件 `cq:noDecoration`。
* 使用自訂HTML標籤，使用 `cq:htmlTag`/或包住 `cq:tagName` 元件 `decorationTagName`。

### 決策樹 {#decision-tree-1}

以下決策樹說明 `cq:noDecoration`、 `cq:htmlTag`、 `cq:tagName`和 `decorationTagName` 如何影響包裝函式行為。

![chlimage_1-3](assets/chlimage_1-3a.jpeg)

