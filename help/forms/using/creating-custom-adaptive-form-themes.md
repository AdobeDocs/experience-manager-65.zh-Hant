---
title: 建立自訂最適化表單主題
seo-title: 建立自訂最適化表單主題
description: 最適化表單主題是AEM用戶端資料庫，可用來定義最適化表單的樣式（外觀和風格）。 了解如何建立自訂最適化表單主題。
seo-description: 最適化表單主題是AEM用戶端資料庫，可用來定義最適化表單的樣式（外觀和風格）。 了解如何建立自訂最適化表單主題。
uuid: b25df10e-b07c-4e9d-a799-30f1c6fb3c44
content-type: reference
topic-tags: customization
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 437e6581-4eb1-4fbd-a6da-86b9c90cec89
exl-id: 73b0057f-082d-4502-90e2-5e41b52c1185
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%

---

# 建立自訂最適化表單主題{#creating-custom-adaptive-form-themes}

>[!CAUTION]
>
>AEM Forms提供[主題編輯器](/help/forms/using/themes.md)功能，可建立及修改最適化表單[主題](/help/forms/using/themes.md)。 只有當您從沒有[主題編輯器](/help/forms/using/themes.md)的版本升級，且您對使用較少/CSS檔案（預先主題編輯器方法）建立的主題已有現有投資時，才可執行本文章所列的步驟。

## 必備條件 {#prerequisites}

* 了解LESS(Leaner CSS)框架
* 如何在Adobe Experience Manager中建立用戶端程式庫
* [使用您建立的](/help/forms/using/custom-adaptive-forms-templates.md) 主題建立最適化表單範本

## 最適化表單主題{#adaptive-form-theme}

**最適化表單主題**&#x200B;是AEM用戶端資料庫，您可用來定義最適化表單的樣式（外觀和風格）。

您可以建立&#x200B;**適用性範本**&#x200B;並將主題套用至範本。 然後，可使用此自訂範本建立&#x200B;**最適化表單**。

![適用性表單和用戶端程式庫](assets/hierarchy.png)

## 建立最適化表單主題{#to-create-an-adaptive-form-theme}的方式

>[!NOTE]
>
>以下過程使用AEM對象的示例名稱（如節點、屬性和資料夾）進行描述。
>
>如果使用名稱執行這些步驟，則生成的模板應與以下快照相似：

![森林主題自適應表](assets/thumbnail.png)
**單快照圖：** *森林主題範例*

1. 在`/apps`節點下建立`cq:ClientLibraryFolder`類型的節點。

   例如，建立下列節點：

   `/apps/myAfThemes/forestTheme`

1. 將多值字串屬性`categories`添加到節點並適當設定其值。

   例如，將屬性設為：`af.theme.forest`。

   ![CRX儲存庫快照](assets/3-2.png)

1. 將兩個資料夾`less`和`css`以及一個檔案`css.txt`添加到步驟1中建立的節點中：

   * `less` 資料夾：包含 `less` 用來定義變數和 `less` 管 `less mixins` 理.css樣式的變數檔案。

      此資料夾由`less`變數檔案、`less` mixin檔案、`less`檔案組成，這些檔案使用mixin和變數定義樣式。 然後，所有這些較少的檔案都以styles.less導入。

   * `css`資料夾：包含.css檔案，您可在其中定義要在主題中使用的靜態樣式。

   **變數檔案較少**:這些是檔案，您可在其中定義或覆寫用於定義CSS樣式的變數。

   適用性表單提供下列.less檔案中定義的OOTB變數：

   * `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less`
   * `/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   適用性表單也提供下列項目中定義的第三方變數：

   `/apps/clientlibs/fd/af/third-party/less/variables.less`

   您可以使用適用性表單提供的較少變數、可以覆寫這些變數，或可以建立新的較少變數。

   >[!NOTE]
   >
   >導入較少前置處理器的檔案時，在導入語句中指定檔案的相對路徑。

   覆寫變數的範例：

   ```css
   @button-background-color: rgb(19, 102, 44);
   @button-border-color: rgb(19, 102, 44);
   @button-border-size: 0px;
   @button-padding: 10px 15px;
   @button-font-color: #ffffff;
   ```

   若要覆寫`less`變數：

   1. 匯入預設適用性表單變數：

      `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   1. 然後匯入包含覆寫變數的較少檔案。

   新變數定義範例：

   ```css
   @button-focus-bg-color: rgb(40, 208, 90);
   @button-hover-bg-color: rgb(30, 156, 67);
   ```

   **混合檔案較少：** 您可以定義接受變數作為引數的函式。這些函式的輸出即為產生的樣式。 在不同樣式內使用這些混合，以避免重複的CSS樣式。

   適用性表單提供以下定義的OOTB mixin:

   * `/apps/clientlibs/fd/af/guidetheme/common/less/adaptiveforms-mixins.less`

   適用性表單也提供下列項目中定義的第三方混合：

   * `/apps/clientlibs/fd/af/third-party/less/mixins.less`

   範例mixin定義：

   ```css
   .rounded-corners (@radius) {
     -webkit-border-radius: @radius;
     -moz-border-radius: @radius;
     -ms-border-radius: @radius;
     -o-border-radius: @radius;
     border-radius: @radius;
   }
   
   .border(@color, @type, @size) {
      border: @color @size @type;
   }
   ```

   **Styles.less File:** 使用此檔案來包含用戶端程式庫中需要使用的所有較少檔案（變數、mixin、樣式）。

   在以下示例`styles.less`檔案中，可以按任意順序放置匯入語句。

   匯入下列.less檔案的陳述式為必填：

   * `globalvariables.less`
   * `layoutvariables.less`
   * `components.less`
   * `layouts.less`

   ```css
   @import "../../../clientlibs/fd/af/guidetheme/common/less/globalvariables.less";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/layoutvariables.less";
   @import "forestTheme-variables";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/components.less";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/layouts.less";
   
   /* custom styles */
   
   .guidetoolbar {
     input[type="button"], button, .button {
       .rounded-corners (@button-radius);
       &:hover {
         background-color: @button-hover-bg-color;
       }
       &:focus {
         background-color: @button-focus-bg-color;
       }
     }
   }
   
   form {
       background-image: url(../images/forest.png);
    background-repeat: no-repeat;
    background-size: 100%;
   }
   ```

   `css.txt`包含要為程式庫下載的.css檔案路徑。

   例如：

   ```javascript
   #base=/apps/clientlibs/fd/af/third-party/css
   bootstrap.css
   
   #base=less
   styles.less
   
   #base=/apps/clientlibs/fd/xfaforms/xfalib/css
   datepicker.css
   listboxwidget.css
   scribble.css
   dialog.css
   ```

   >[!NOTE]
   >
   >styles.less檔案不是必需的。 這表示若您尚未定義任何自訂樣式、變數或mixin，則不需要建立此檔案。
   >
   >但是，如果不建立style.less檔案，則需要在css.txt檔案中取消注釋以下行：
   >
   >**`#base=less`**
   >
   >並註解下列行：
   >
   >**`styles.less`**

## 在最適化表單{#to-use-a-theme-in-an-adaptive-form}中使用主題

建立最適化表單主題後，請執行下列步驟以在最適化表單中使用此主題：

1. 若要包含在[中建立的主題以建立最適化表單主題](/help/forms/using/creating-custom-adaptive-form-themes.md#p-to-create-an-adaptive-form-theme-p)區段，請建立類型`cq:Component`的自訂頁面。

   例如， `/apps/myAfCustomizations/myAfPages/forestPage`

   1. 新增`sling:resourceSuperType`屬性，並將其值設為`fd/af/components/page/base`。

      ![CRX儲存庫快照](assets/1-2.png)

   1. 若要使用頁面中的主題，需要將覆蓋檔案library.jsp添加到節點。

      然後，您會匯入在中建立的主題，以建立本文的最適化表單主題區段。

      下列范常式式碼片段匯入`af.theme.forest`主題。

      ```jsp
      <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
      <cq:includeClientLib categories="af.theme.forest"/>
      ```

   1. **可選**:在自訂頁面中，視需要覆寫header.jsp、footer.jsp和body.jsp。

1. 建立自訂範本(例如：`/apps/myAfCustomizations/myAfTemplates/forestTemplate`)，其jcr:content指向上一步中建立的自訂頁面(例如：`myAfCustomizations/myAfPages/forestPage)`。

   ![CRX儲存庫快照](assets/2-1.png)

1. 使用上一步中建立的範本建立最適化表單。 最適化表單的外觀與風格由本文「建立最適化表單主題」一節中建立的主題所定義。
