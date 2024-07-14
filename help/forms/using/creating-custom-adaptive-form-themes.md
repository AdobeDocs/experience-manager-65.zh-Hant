---
title: 建立自訂最適化表單主題
description: 最適化表單主題是Adobe Experience Manager使用者端資料庫，可用來定義最適化表單的樣式（外觀）。 瞭解如何建立自訂最適化表單主題。
content-type: reference
topic-tags: customization
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 73b0057f-082d-4502-90e2-5e41b52c1185
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
source-git-commit: 8a77756e8ba771c8de9950c2323bef8f23cc59b4
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 0%

---

# 建立自訂最適化表單主題 {#creating-custom-adaptive-form-themes}

>[!CAUTION]
>
>Adobe Experience Manager (AEM) Forms提供[主題編輯器](/help/forms/using/themes.md)功能，可建立和修改最適化表單[主題](/help/forms/using/themes.md)。 您必須從沒有[佈景主題編輯器](/help/forms/using/themes.md)的版本升級，而且您已經投資使用Less/CSS檔案建立佈景主題（佈景主題編輯器前方法），才可執行本文列出的步驟。

## 先決條件 {#prerequisites}

* LESS (Leaner CSS)架構的相關知識
* 如何在Adobe Experience Manager中建立使用者端資源庫
* [建立最適化表單範本](/help/forms/using/custom-adaptive-forms-templates.md)，以使用您建立的主題

## 最適化表單主題 {#adaptive-form-theme}

**最適化表單主題**&#x200B;是AEM使用者端資料庫，可用來定義最適化表單的樣式（外觀）。

您建立&#x200B;**最適化範本**，並將主題套用至範本。 然後，您可以使用此自訂範本來建立&#x200B;**最適化表單**。

![最適化表單和使用者端資料庫](assets/hierarchy.png)

## 建立最適化表單主題 {#to-create-an-adaptive-form-theme}

>[!NOTE]
>
>以下程式使用AEM物件的範例名稱（例如節點、屬性和資料夾）進行說明。
>
>如果使用名稱來遵循這些步驟，則產生的範本應類似於以下快照：

![樹系主題的最適化表單快照](assets/thumbnail.png)
**圖：** *樹系佈景主題範例*

1. 在`/apps`節點下建立型別`cq:ClientLibraryFolder`的節點。

   例如，建立下列節點：

   `/apps/myAfThemes/forestTheme`

1. 將多值字串屬性`categories`新增至節點，並適當地設定其值。

   例如，將屬性設定為： `af.theme.forest`。

   ![CRX儲存機制快照](assets/3-2.png)

1. 將兩個資料夾`less`和`css`以及檔案`css.txt`新增到步驟1中建立的節點：

   * `less`資料夾：包含您定義用來管理.css樣式的`less`變數和`less mixins`的`less`變數檔案。

     此資料夾包含`less`個變數檔案、`less`個mixin檔案、`less`個使用mixin定義樣式的檔案，以及變數。 然後所有這`less`個檔案都會以樣式匯入.less.

   * `css`資料夾：包含.css檔案，您可以在其中定義主題中使用的靜態樣式。

   **較少變數檔案**：這些是您定義或覆寫用於定義CSS樣式的變數的檔案。

   調適型表單提供下列`.less`個檔案中定義的現成可用變數：

   * `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less`
   * `/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   調適型表單也提供中定義的協力廠商變數：

   `/apps/clientlibs/fd/af/third-party/less/variables.less`

   您可以使用隨最適化表單提供的`less`變數、覆寫這些變數，或建立新的`less`變數。

   >[!NOTE]
   >
   >匯入較少前置處理器的檔案時，請在匯入陳述式中指定檔案的相對路徑。

   覆寫變數的範例：

   ```css
   @button-background-color: rgb(19, 102, 44);
   @button-border-color: rgb(19, 102, 44);
   @button-border-size: 0px;
   @button-padding: 10px 15px;
   @button-font-color: #ffffff;
   ```

   覆寫`less`變數：

   1. 匯入預設最適化表單變數：

      `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   1. 然後匯入包含被覆寫變數的較少檔案。

   新變數定義範例：

   ```css
   @button-focus-bg-color: rgb(40, 208, 90);
   @button-hover-bg-color: rgb(30, 156, 67);
   ```

   **較少mixin檔案：**&#x200B;您可以定義接受變數做為引數的函式。 這些函式的輸出是產生的樣式。 請在不同的樣式中使用這些Mixin，以避免重複CSS樣式。

   調適型表單提供中定義的現成Mixin：

   * `/apps/clientlibs/fd/af/guidetheme/common/less/adaptiveforms-mixins.less`

   調適型表單也提供中定義的協力廠商Mixin：

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

   **Styles.less檔案：**&#x200B;使用此檔案來包含您必須在使用者端資料庫中使用的所有`less`檔案（變數、mixin、樣式）。

   在下列範例`styles.less`檔案中，匯入陳述式可以任意順序放置。

   匯入下列`.less`個檔案的陳述式是強制性的：

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

   `css.txt`包含要為資料庫下載的.css檔案路徑。

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
   >styles.less檔案不是強制性的。 這表示如果您尚未定義任何自訂樣式、變數或mixin，則不需要建立此檔案。
   >
   >不過，如果您未建立style.less檔案，則必須在css.txt檔案中取消註解下列行：
   >
   >**`#base=less`**
   >
   >並註解下列行：
   >
   >**`styles.less`**

## 在最適化表單中使用佈景主題 {#to-use-a-theme-in-an-adaptive-form}

建立最適化表單主題後，請執行以下步驟以在最適化表單中使用此主題：

1. 若要包含在[中建立的佈景主題以建立最適化表單佈景主題](/help/forms/using/creating-custom-adaptive-form-themes.md#p-to-create-an-adaptive-form-theme-p)區段，請建立型別`cq:Component`的自訂頁面。

   例如 `/apps/myAfCustomizations/myAfPages/forestPage`

   1. 新增`sling:resourceSuperType`屬性並將其值設定為`fd/af/components/page/base`。

      ![CRX儲存機制快照](assets/1-2.png)

   1. 若要在頁面中使用主題，您必須將覆寫檔案library.jsp新增至節點。

      接著，您可以匯入在「建立最適化表單主題」一節中建立的主題。

      下列範常式式碼片段會匯入`af.theme.forest`主題。

      ```jsp
      <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
      <cq:includeClientLib categories="af.theme.forest"/>
      ```

   1. **選擇性**：在自訂頁面中，視需要覆寫header.jsp、footer.jsp和body.jsp。

1. 建立自訂範本（例如： `/apps/myAfCustomizations/myAfTemplates/forestTemplate`），其jcr：content指向在上一步建立的自訂頁面（例如： `myAfCustomizations/myAfPages/forestPage)`）。

   ![CRX儲存機制快照](assets/2-1.png)

1. 使用上一步建立的範本建立最適化表單。 最適化表單的外觀是由本文中「建立最適化表單主題」一節中所建立的主題所定義。
