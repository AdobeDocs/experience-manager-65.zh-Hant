---
title: 裝飾標記
description: 轉譯網頁中的元件時可產生 HTML 元素，將轉譯的元件圍在其中。對於開發人員來說，AEM 提供簡單清晰的邏輯，可控制圍住所含元件的裝飾標記。
exl-id: d049ebf1-7fa6-4d2c-86f9-b18e107092ea
source-git-commit: 43a30b5ba76ea470cc50a962d4f04b4a1508964d
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 10%

---

# 裝飾標記{#decoration-tag}

轉譯網頁中的元件時可產生 HTML 元素，將轉譯的元件圍在其中。這主要有兩個目的：

* 只有用HTML元素包裝元件時，才能編輯元件。
* 包裝元素用於應用HTML類，這些類提供：

   * 佈局資訊
   * 造型資訊

對於開發人員來說，AEM 提供簡單清晰的邏輯，可控制圍住所含元件的裝飾標記。裝飾標籤的呈現方式和呈現方式由兩個因素的組合來定義，此頁將深入其中：

* 所述部件本身可以配置其裝飾標籤具有一組屬性。
* 包含元件的指令碼（HTL、JSP、dispatcher等）可以使用包含參數來定義裝飾標籤的方面。

## 建議 {#recommendations}

以下是關於何時包括包裝元素的一些一般性建議，這些建議應有助於避免遇到意外問題：

* 包裝元素的存在在WCMMode（編輯或預覽模式）、實例（作者或發佈）或環境（暫存或生產）之間不應存在差異，因此頁面的CSS和JavaScripts在所有情況下都工作相同。
* 應將包裝元素添加到所有可編輯的元件中，以便頁面編輯器可以正確初始化和更新這些元件。
* 對於不可編輯的元件，如果包裝元素不提供特定功能，則可以避免它，因此，不會不必要地膨脹所得標籤。

## 元件控制項 {#component-controls}

以下屬性和節點可應用於元件以控制其裝飾標籤的行為：

* **`cq:noDecoration {boolean}`:** 此屬性可以添加到元件中，而真值強制AEM不要在元件上生成任何包裝元素。

* **`cq:htmlTag`節點：** 此節點可以添加到元件下，並可以具有以下屬性：

   * **`cq:tagName {String}`:** 這可用於指定用於包裝元件（而不是預設DIV元素）的自定義HTML標籤。
   * **`class {String}`:** 這可用於指定要添加到包裝中的css類名。
   * 其他屬性名稱將添加為與提供的String值相同的HTML屬性。

## 指令碼控制項 {#script-controls}

但是，包裝行為會因 [HTL](/help/sites-developing/decoration-tag.md#htl) 或 [JSP](/help/sites-developing/decoration-tag.md#jsp) 用於包括元素。

### HTL {#htl}

HTL中的包裝行為一般可以概括為：

* 預設情況下不呈現包裝器DIV(僅在執行 `data-sly-resource="foo"`)。
* 所有wcm模式（禁用、預覽、編輯作者和發佈）的渲染相同。

包裝器的行為也可以被完全控制。

* HTL指令碼對包裝標籤的結果行為具有完全控制。
* 元件屬性(如 `cq:noDecoration` 和 `cq:tagName`)也可以定義包裝標籤。

可以完全控制來自HTL指令碼的包裝標籤及其關聯邏輯的行為。

有關在HTL中開發的詳細資訊，請參閱 [HTL文檔](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)。

#### 決策樹 {#decision-tree}

此決策樹匯總了確定包裝標籤行為的邏輯。

![chlimage_1-75](assets/chlimage_1-75a.png)

#### 使用案例 {#use-cases}

以下三個使用案例提供了包裝標籤處理方式的示例，還說明了控制包裝標籤的所需行為是多麼簡單。

以下所有示例都假定以下內容結構和元件：

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

#### 用例1:包括用於代碼重用的元件 {#use-case-include-a-component-for-code-reuse}

最典型的用例是，當元件由於代碼重用原因而包括另一個元件時。 在這種情況下，所包含的元件不希望使用其自己的工具欄和對話框進行編輯，因此不需要包裝，也不需要元件的 `cq:htmlTag` 將被忽略。 這可以視為預設行為。

`one.html: <sly data-sly-resource="child"></sly>`

`two.html: Hello World!`

生成的輸出 `/content/test.html`:

**`Hello World!`**

示例是包括用於顯示影像的核心影像元件的元件，在這種情況下，通常使用合成資源，其包括通過將表示元件將具有的所有屬性的映射對象傳遞到資料安全資源來包括虛擬子元件。

#### 用例2:包括可編輯元件 {#use-case-include-an-editable-component}

另一個常見用例是容器元件包括可編輯的子元件（如佈局容器）時。 在此情況下，每個包含的子代都必須有一個包裝才能使編輯器工作(除非使用 `cq:noDecoration` 屬性)。

由於所包含的元件在本例中是獨立元件，因此它需要一個包裝元素以便編輯器工作，並定義其佈局和樣式以應用。 要觸發此行為， `decoration=true` 的雙曲餘切值。

`one.html: <sly data-sly-resource="${'child' @ decoration=true}"></sly>`

`two.html: Hello World!`

生成的輸出 `/content/test.html`:

**`<article class="component-two">Hello World!</article>`**

#### 用例3:自定義行為 {#use-case-custom-behavior}

可能存在任意數量的複雜情況，通過HTL的可能性，可以輕鬆實現：

* **`decorationTagName='ELEMENT_NAME'`** 定義包裝的元素名稱。
* **`cssClassName='CLASS_NAME'`** 定義要在其上設定的CSS類名。

`one.html: <sly data-sly-resource="${'child' @ decorationTagName='aside', cssClassName='child'}"></sly>`

`two.html: Hello World!`

結果輸出 `/content/test.html`:

**`<aside class="child">Hello World!</aside>`**

## JSP {#jsp}

當包含元件時使用 `cq:includ`e或 `sling:include`，中的預設行AEM為是使用DIV繞排元素。 但是，可以通過兩種方式自定義此包裝：

* 顯式告AEM訴不要使用 `cq:noDecoration`。
* 使用自定義HTML標籤使用 `cq:htmlTag`/ `cq:tagName` 或 `decorationTagName`。

### 決策樹 {#decision-tree-1}

以下診斷樹說明了 `cq:noDecoration`。 `cq:htmlTag`。 `cq:tagName`, `decorationTagName` 影響包裝行為。

![chlimage_1-3](assets/chlimage_1-3a.jpeg)
