---
title: 為最適化表單欄位建立自訂外觀
seo-title: Create custom appearances for adaptive form fields
description: 在適用性Forms中自訂現成可用元件的外觀。
seo-description: Customize appearance of out-of-the-box components in Adaptive Forms.
uuid: 1aa36443-774a-49fb-b3d1-d5a2d5ff849a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: d388acef-7313-4e68-9395-270aef6ef2c6
docset: aem65
exl-id: 770e257a-9ffd-46a4-9703-ff017ce9caed
source-git-commit: 8a24ca02762e7902b7d0033b36560629ee711de1
workflow-type: tm+mt
source-wordcount: '1713'
ht-degree: 0%

---

# 為最適化表單欄位建立自訂外觀{#create-custom-appearances-for-adaptive-form-fields}

## 簡介 {#introduction}

適用性表單可運用 [外觀框架](/help/forms/using/introduction-widgets.md) 可協助您為最適化表單欄位建立自訂外觀，並提供不同的使用者體驗。 例如，使用切換按鈕取代選項按鈕和核取方塊，或使用自訂jQuery外掛程式，限制使用者在電話號碼或電子郵件ID等欄位中的輸入。

本檔案說明如何使用jQuery外掛程式，為最適化表單欄位建立這些替代體驗。 此外，它還展示了一個示例，以建立數值欄位元件的自定義外觀，以作為數字步進器或滑塊顯示。

先來看看本文使用的主要術語和概念。

**外觀** 是指最適化表單欄位中各種元素的樣式、外觀和風格及組織。 它通常包括標籤、提供輸入的互動區、幫助表徵圖以及欄位的簡短和長說明。 本文討論的外觀定制適用於欄位輸入區域的外觀。

**jQuery外掛程式** 提供基於jQuery Widget架構的標準機制，以實作替代外觀。

**ClientLib** AEM用戶端處理中由複雜JavaScript和CSS程式碼驅動的用戶端程式庫系統。 如需詳細資訊，請參閱使用用戶端程式庫。

**原型** Maven項目模板工具包，定義為Maven項目的原始模式或模型。 如需詳細資訊，請參閱原型簡介。

**使用者控制** 指介工具集中包含欄位值的主要元素，並用於外觀架構，將自訂介面工具集UI與最適化表單模型系結。

## 建立自訂外觀的步驟 {#steps-to-create-a-custom-appearance}

建立自訂外觀的高階步驟如下：

1. **建立專案**:建立Maven專案，以產生要部署在AEM上的內容套件。
1. **擴展現有的Widget類**:擴展現有的Widget類並覆蓋所需的類。
1. **建立用戶端程式庫**:建立 `clientLib: af.customwidget` 程式庫，並新增必要的JavaScript和CSS檔案。

1. **建置和安裝專案**:建立Maven專案，並在AEM上安裝產生的內容套件。
1. **更新最適化表單**:更新最適化表單欄位屬性以使用自訂外觀。

### 建立專案 {#create-a-project}

模仿原型是建立自訂外觀的起點。 要使用的原型詳細資訊如下：

* **存放庫**:https://repo1.maven.org/maven2/com/adobe/
* **工件ID**:自訂外觀原型
* **群組Id**:com.adobe.aemforms
* **版本**:1.0.4

執行下列命令，根據原型建立本機專案：

`mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

命令會從存放庫下載Maven外掛程式和原型資訊，並根據下列資訊產生專案：

* **groupId**:產生的Maven專案使用的群組ID
* **artifactId**:生成的Maven項目使用的工件ID。
* **版本**:產生的Maven專案的版本。
* **套件**:用於檔案結構的包。
* **artifactName**:生成的AEM包的對象名。
* **packageGroup**:產生的AEM套件的套件群組。
* **widgetName**:用於引用的外觀名稱。

產生的專案具有下列結構：

```java
─<artifactId>

 └───src

     └───main

         └───content

             └───jcr_root

                 └───etc

                     └───clientlibs

                         └───custom

                             └───<widgetName>

                                 ├───common [client library - af.customwidgets which encapsulates below clientLibs]

                                 ├───integration [client library - af.customwidgets.<widgetName>_widget which contains template files for integrating a third-party plugin with Adaptive Forms]

                                 │   ├───css

                                 │   └───javascript

                                 └───jqueryplugin [client library - af.customwidgets.<widgetName>_plugin which holds the third-party plugins and related dependencies]

                                     ├───css

                                     └───javascript
```

### 擴展現有的Widget類 {#extend-an-existing-widget-class}

建立專案範本後，視需要進行下列變更：

1. 將第三方外掛程式相依性納入專案。

   1. 將協力廠商或自訂jQuery外掛程式放入 `jqueryplugin/javascript` 資料夾和相關的CSS檔案 `jqueryplugin/css` 檔案夾。 如需詳細資訊，請參閱 `jqueryplugin/javascript and jqueryplugin/css` 檔案夾。

   1. 修改 `js.txt` 和 `css.txt` 檔案，以包含jQuery外掛程式的任何其他JavaScript和CSS檔案。

1. 將協力廠商外掛程式與架構整合，以啟用自訂外觀架構與jQuery外掛程式之間的互動。 只有在您擴充或覆寫下列函式後，新介面工具集才能運作。

<table>
 <tbody>
  <tr>
   <td><strong>函數</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td><code>render</code></td>
   <td>呈現函式返回Widget預設HTML元素的jQuery對象。 預設HTML元素應為可聚焦類型。 例如， <code>&lt;a&gt;</code>, <code>&lt;input&gt;</code>，和 <code>&lt;li&gt;</code>. 傳回的元素會作為 <code>$userControl</code>. 若 <code>$userControl</code> 指定上述約束， <code>AbstractWidget</code> 類別可如預期般運作，否則某些常見API（焦點、按一下）需要變更。 </td>
  </tr>
  <tr>
   <td><code>getEventMap</code></td>
   <td>傳回對應以將HTML事件轉換為XFA事件。 <br /> <code class="code">{
      blur: XFA_EXIT_EVENT,
      }</code><br /> 此範例顯示 <code>blur</code> 是HTML事件，且 <code>XFA_EXIT_EVENT</code> 是對應的XFA事件。 </td>
  </tr>
  <tr>
   <td><code>getOptionsMap</code></td>
   <td>傳回地圖，提供變更選項時要執行之動作的詳細資訊。 鍵是提供給介面工具集的選項，值是每當檢測到選項中的更改時調用的函式。 介面工具集為所有常用選項( <code>value</code> 和 <code>displayValue</code>)。</td>
  </tr>
  <tr>
   <td><code>getCommitValue</code></td>
   <td>每當jQuery Widget的值儲存在XFA模型中（例如，在文本欄位的退出事件上）時，jQuery Widget架構就會載入函式。 實作應傳回儲存在介面工具集中的值。 處理常式會隨選項的新值提供。</td>
  </tr>
  <tr>
   <td><code>showValue</code></td>
   <td>依預設，在XFA中，輸入事件時， <code>rawValue</code> 的下一頁。 此函式的呼叫是為了顯示 <code>rawValue</code> 對使用者。 </td>
  </tr>
  <tr>
   <td><code>showDisplayValue</code></td>
   <td>依預設，在退出事件的XFA中， <code>formattedValue</code> 的下一頁。 此函式的呼叫是為了顯示 <code>formattedValue</code> 對使用者。 </td>
  </tr>
 </tbody>
</table>

1. 更新 `integration/javascript` 資料夾（視需要）。

   * 取代文字 `__widgetName__` 具有實際的介面工具集名稱。
   * 從適當的現成Widget類別擴充Widget。 在大多數情況下，它是與要取代的現有介面工具集相對應的介面工具集類別。 父類名稱用於多個位置，因此建議搜索字串的所有實例 `xfaWidget.textField` ，並將其替換為實際使用的父類。
   * 擴充 `render` 提供替代UI的方法。 這是叫用jQuery外掛程式以更新UI或互動行為的位置。 此 `render` 方法應傳回使用者控制元素。

   * 擴充 `getOptionsMap` 方法來覆寫因介面工具集的變更而受影響的任何選項設定。 函式會傳回對應，提供在選項變更時要執行之動作的詳細資訊。 鍵是提供給介面工具集的選項，值是每當檢測到選項的更改時調用的函式。
   * 此 `getEventMap` 方法會將介面工具集所觸發的事件，與最適化表單模型所需的事件對應。 預設值會對應預設介面工具集的標準HTML事件，且如果觸發替代事件，則需要更新。
   * 此 `showDisplayValue` 和 `showValue` 應用display and edit picture子句，並且可以被覆蓋以具有替代行為。

   * 此 `getCommitValue` 方法在 `commit`事件。 一般來說，它是退出事件，但下拉式清單、選項按鈕和核取方塊元素在變更時發生除外)。 如需詳細資訊，請參閱 [適用性Forms運算式](../../forms/using/adaptive-form-expressions.md#p-value-commit-script-p).

   * 範本檔案提供各種方法的範例實施。 移除不要擴充的方法。

### 建立用戶端程式庫 {#create-a-client-library}

Maven原型產生的範例專案會自動建立必要的用戶端程式庫，並將它們包裝至具有類別的用戶端程式庫中 `af.customwidgets`. 在 `af.customwidgets` 會在執行階段自動包含。

### 建置和安裝 {#build-and-install}

若要建置專案，請在殼層上執行下列命令，以產生需要安裝在AEM伺服器上的CRX套件。

`mvn clean install`

>[!NOTE]
>
>Maven專案會參照POM檔案中的遠端存放庫。 這僅供參考，而根據Maven標準，存放庫資訊會擷取於 `settings.xml` 檔案。

### 更新最適化表單 {#update-the-adaptive-form}

若要將自訂外觀套用至最適化表單欄位：

1. 在編輯模式中開啟最適化表單。
1. 開啟 **屬性** 對話框，用於要應用自定義外觀的欄位。
1. 在 **樣式** 頁簽，更新 `CSS class` 屬性，以在 `widget_<widgetName>` 格式。 例如： **widget_numericstepper**

## 範例：建立自訂外觀   {#sample-create-a-custom-appearance-nbsp}

現在，讓我們查看一個示例，以建立數字欄位的自定義外觀，以作為數字步進器或滑塊顯示。 執行下列步驟：

1. 執行下列命令，以根據Maven原型建立本機專案：

   `mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

   它會提示您為下列參數指定值。
   *此範例中使用的值會以粗體強調顯示*.

   `Define value for property 'groupId': com.adobe.afwidgets`

   `Define value for property 'artifactId': customWidgets`

   `Define value for property 'version': 1.0.1-SNAPSHOT`

   `Define value for property 'package': com.adobe.afwidgets`

   `Define value for property 'artifactName': customWidgets`

   `Define value for property 'packageGroup': adobe/customWidgets`

   `Define value for property 'widgetName': numericStepper`

1. 導覽至 `customWidgets` (為指定的值 `artifactID` 屬性)目錄，並執行下列命令以產生Eclipse專案：

   `mvn eclipse:eclipse`

1. 開啟Eclipse工具，然後執行下列操作以匯入Eclipse專案：

   1. 選擇 **[!UICONTROL 檔案>匯入>將現有專案匯入工作區]**.

   1. 瀏覽並選取您執行的資料夾 `archetype:generate` 命令。

   1. 按一下 **[!UICONTROL 完成]**.

      ![eclipse — 螢幕截圖](assets/eclipse-screenshot.png)

1. 選取要用於自訂外觀的介面工具集。 此示例使用以下數字步進器小部件：

   [https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html](https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html)

   在Eclipse專案中，檢閱 `plugin.js` 檔案，確保符合外觀的要求。 在此示例中，外觀滿足以下要求：

   * 數字步進器應從 `- $.xfaWidget.numericInput`.
   * 此 `set value` 介面工具集的方法會在焦點位於欄位後設定值。 這是最適化表單Widget的必要需求。
   * 此 `render` 調用方法時需要覆蓋方法 `bootstrapNumber` 方法。

   * 除了外掛程式的主要原始碼外，外掛程式沒有其他相依性。
   * 示例不對步進器執行任何樣式，因此不需要其他CSS。
   * 此 `$userControl` 物件應可供使用 `render` 方法。 這是 `text` 使用外掛程式程式碼複製的類型。

   * 此 **+** 和 **-** 欄位停用時，應停用按鈕。

1. 替換 `bootstrap-number-input.js` （jQuery外掛程式），而 `numericStepper-plugin.js` 檔案。
1. 在 `numericStepper-widget.js` 檔案中，新增下列程式碼以覆寫呈現方法以叫用外掛程式並傳回 `$userControl` 物件：

   ```javascript
   render : function() {
        var control = $.xfaWidget.numericInput.prototype.render.apply(this, arguments);
        var $control = $(control);
        var controlObject;
        try{
            if($control){
            $control.bootstrapNumber();
            var id = $control.attr("id");
            controlObject = $("#"+id);
            }
        }catch (exc){
             console.log(exc);
        }
        return controlObject;
   }
   ```

1. 在 `numericStepper-widget.js` 檔案，覆蓋 `getOptionsMap` 屬性來覆寫存取選項，並在停用模式中隱藏+和 — 按鈕。

   ```javascript
   getOptionsMap: function(){
       var parentOptionsMap = $.xfaWidget.numericInput.prototype.getOptionsMap.apply(this,arguments),
   
       newMap = $.extend({},parentOptionsMap,
   
        {
   
              "access": function(val) {
              switch(val) {
                 case "open" :
                   this.$userControl.removeAttr("readOnly");
                   this.$userControl.removeAttr("aria-readonly");
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
                 case "nonInteractive" :
                 case "protected" :
                   this.$userControl.attr("disabled", "disabled");
                   this.$userControl.attr("aria-disabled", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
                case "readOnly" :
                   this.$userControl.attr("readOnly", "readOnly");
                   this.$userControl.attr("aria-readonly", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
               default :
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
             }
          },
      });
      return newMap;
    }
   ```

1. 儲存變更，導覽至包含 `pom.xml` ，然後執行以下Maven命令來生成項目：

   `mvn clean install`

1. 使用AEM Package Manager安裝套件。

1. 在編輯模式中開啟您要套用自訂外觀的最適化表單，並執行下列動作：

   1. 按一下右鍵要應用外觀的欄位，然後按一下 **[!UICONTROL 編輯]** 開啟「編輯元件」對話框。

   1. 在樣式索引標籤中，更新 **[!UICONTROL CSS類]** 要添加的屬性 `widget_numericStepper`.

您剛建立的新外觀現在可供使用。
