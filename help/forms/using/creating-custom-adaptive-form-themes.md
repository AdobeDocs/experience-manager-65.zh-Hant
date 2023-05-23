---
title: 建立自定義自適應窗體主題
seo-title: Creating custom adaptive form themes
description: 自適應表單主AEM題是用於定義自適應表單樣式（外觀和樣式）的客戶端庫。 瞭解如何建立自定義自適應表單主題。
seo-description: An adaptive form theme is an AEM client library that you use to define the styles (look and feel) for an adaptive form. Learn how you can create custom adaptive form themes.
uuid: b25df10e-b07c-4e9d-a799-30f1c6fb3c44
content-type: reference
topic-tags: customization
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 437e6581-4eb1-4fbd-a6da-86b9c90cec89
exl-id: 73b0057f-082d-4502-90e2-5e41b52c1185
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# 建立自定義自適應窗體主題 {#creating-custom-adaptive-form-themes}

>[!CAUTION]
>
>AEM Forms提供 [主題編輯器](/help/forms/using/themes.md) 建立和修改自適應表單的能力 [主題](/help/forms/using/themes.md)。 只有從未升級的版本升級，才能執行本文中列出的步驟 [主題編輯器](/help/forms/using/themes.md) 而且您對使用Less/CSS檔案（主題前編輯方法）建立的主題已有投資。

## 必備條件 {#prerequisites}

* 瞭解LESS(Leaner CSS)框架
* 如何在Adobe Experience Manager建立客戶端庫
* [建立自適應表單模板](/help/forms/using/custom-adaptive-forms-templates.md) 用於使用您建立的主題

## 自適應窗體主題 {#adaptive-form-theme}

安 **自適應窗體主題** 是用AEM於定義自適應表單樣式（外觀和樣式）的客戶端庫。

建立 **自適應模板** 並將主題應用於模板。 然後，使用此自定義模板建立 **自適應形式**。

![自適應表單和客戶端庫](assets/hierarchy.png)

## 建立自適應窗體主題 {#to-create-an-adaptive-form-theme}

>[!NOTE]
>
>以下過程使用節點、屬性和AEM資料夾等對象的示例名稱進行說明。
>
>如果使用名稱執行這些步驟，則生成的模板應與以下快照類似：

![林主題自適應表單快照](assets/thumbnail.png)
**圖：** *林主題示例*

1. 建立類型的節點 `cq:ClientLibraryFolder` 下 `/apps`的下界。

   例如，建立以下節點：

   `/apps/myAfThemes/forestTheme`

1. 添加多值字串屬性 `categories` 並相應設定其值。

   例如，將屬性設定為： `af.theme.forest`。

   ![CRX儲存庫快照](assets/3-2.png)

1. 添加兩個資料夾， `less` 和 `css`，和檔案 `css.txt` 到步驟1中建立的節點：

   * `less` 資料夾：包含 `less` 在其中定義變數檔案 `less` 變數和 `less mixins` 用於管理.css樣式。

      此資料夾包含 `less` 變數檔案， `less` 混入檔案， `less` 檔案使用混合和變數定義樣式。 然後，所有這些較少的檔案都以styles.less格式導入。

   * `css`資料夾：包含.css檔案，在該檔案中定義要在主題中使用的靜態樣式。

   **較少變數檔案**:這些檔案是定義或覆蓋用於定義CSS樣式的變數的檔案。

   自適應表單提供在以下.less檔案中定義的OOTB變數：

   * `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less`
   * `/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   自適應表單還提供了以下定義的第三方變數：

   `/apps/clientlibs/fd/af/third-party/less/variables.less`

   可以使用自適應表單中提供的較少變數，可以覆蓋這些變數，也可以建立新的較少變數。

   >[!NOTE]
   >
   >在導入較少預處理器的檔案時，在import語句中指定檔案的相對路徑。

   覆蓋變數示例：

   ```css
   @button-background-color: rgb(19, 102, 44);
   @button-border-color: rgb(19, 102, 44);
   @button-border-size: 0px;
   @button-padding: 10px 15px;
   @button-font-color: #ffffff;
   ```

   要覆蓋 `less`變數：

   1. 導入預設自適應表單變數：

      `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   1. 然後導入包含被覆蓋變數的較少檔案。

   新變數定義示例：

   ```css
   @button-focus-bg-color: rgb(40, 208, 90);
   @button-hover-bg-color: rgb(30, 156, 67);
   ```

   **較少混合檔案：** 可以定義接受變數作為參數的函式。 這些函式的輸出是結果樣式。 在不同樣式中使用這些混合，以避免重複CSS樣式。

   自適應表單提供了在以下位置定義的OOTB混合：

   * `/apps/clientlibs/fd/af/guidetheme/common/less/adaptiveforms-mixins.less`

   自適應表單還提供了在以下定義的第三方混合：

   * `/apps/clientlibs/fd/af/third-party/less/mixins.less`

   混合定義示例：

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

   **Styles.less檔案：** 使用此檔案可以包括客戶端庫中需要使用的所有較少的檔案（變數、混合、樣式）。

   在以下示例中 `styles.less` 檔案，導入語句可以按任意順序放置。

   導入以下.less檔案的語句是必需的：

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

   的 `css.txt` 包含要為庫下載的.css檔案的路徑。

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
   >styles.less檔案不是必需的。 這意味著，如果尚未定義任何自定義樣式、變數或混合，則無需建立此檔案。
   >
   >但是，如果不在css.txt檔案中建立style.less檔案，則需要取消對以下行的注釋：
   >
   >**`#base=less`**
   >
   >並注釋以下行：
   >
   >**`styles.less`**

## 在自適應窗體中使用主題 {#to-use-a-theme-in-an-adaptive-form}

建立自適應表單主題後，請執行以下步驟以在自適應表單中使用此主題：

1. 要包括在中建立的主題，請執行以下操作： [建立自適應窗體主題](/help/forms/using/creating-custom-adaptive-form-themes.md#p-to-create-an-adaptive-form-theme-p) 部分，建立類型的自定義頁 `cq:Component`。

   例如 `/apps/myAfCustomizations/myAfPages/forestPage`

   1. 添加 `sling:resourceSuperType` 屬性，將其值設定為 `fd/af/components/page/base`。

      ![CRX儲存庫快照](assets/1-2.png)

   1. 要使用頁面中的主題，需要向節點添加覆蓋檔案library.jsp。

      然後，導入在建立此文章的自適應窗體主題部分中建立的主題。

      以下示例代碼段將導入 `af.theme.forest` 的子菜單。

      ```jsp
      <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
      <cq:includeClientLib categories="af.theme.forest"/>
      ```

   1. **可選**:在自定義頁中，根據需要覆蓋header.jsp、footer.jsp和body.jsp。

1. 建立自定義模板(例如： `/apps/myAfCustomizations/myAfTemplates/forestTemplate`)，其jcr:content指向在上一步中建立的自定義頁面(例如： `myAfCustomizations/myAfPages/forestPage)`。

   ![CRX儲存庫快照](assets/2-1.png)

1. 使用在上一步中建立的模板建立「自適應」表單。 自適應表單的外觀由在建立本文自適應表單主題部分中建立的主題定義。
