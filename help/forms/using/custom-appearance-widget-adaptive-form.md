---
title: 為自適應表單域建立自定義外觀
seo-title: Create custom appearances for adaptive form fields
description: 在Adaptive Forms中定制現成元件的外觀。
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

# 為自適應表單域建立自定義外觀{#create-custom-appearances-for-adaptive-form-fields}

## 簡介 {#introduction}

自適應表單利用 [外觀框架](/help/forms/using/introduction-widgets.md) 幫助您為自適應表單域建立自定義外觀，並提供不同的用戶體驗。 例如，用切換按鈕替換單選按鈕和複選框，或使用自定義jQuery插件限制用戶在電話號碼或電子郵件ID等欄位中的輸入。

本文檔介紹如何使用jQuery插件為自適應表單域建立這些替代體驗。 此外，它還展示了一個示例，用於為數字欄位元件建立一個自定義外觀，以顯示為數字步進器或滑塊。

首先來看本文使用的關鍵術語和概念。

**外觀** 指適應性表單域中各種元素的樣式、外觀和感覺以及組織。 它通常包括標籤、提供輸入的交互區域、幫助表徵圖以及欄位的簡短和長說明。 本文所討論的外觀定制方法適用於該欄位輸入區域的外觀。

**jQuery插件** 提供基於jQuery構件框架的標準機制，以實現替代外觀。

**客戶端庫** 一種客戶端庫系統，AEM由複雜的JavaScript和CSS代碼驅動。 有關詳細資訊，請參閱使用客戶端庫。

**原型** Maven項目模板化工具包，定義為Maven項目的原始模式或模型。 有關詳細資訊，請參閱原型簡介。

**用戶控制項** 引用構件中包含欄位值的主元素，該元素由外觀框架用於將自定義構件UI與自適應表單模型綁定。

## 建立自定義外觀的步驟 {#steps-to-create-a-custom-appearance}

在高級別上建立自定義外觀的步驟如下：

1. **建立項目**:建立生成要部署的內容包的Maven項AEM目。
1. **擴展現有小部件類**:擴展現有小部件類並覆蓋所需類。
1. **建立客戶端庫**:建立 `clientLib: af.customwidget` 庫並添加所需的JavaScript和CSS檔案。

1. **生成並安裝項目**:生成Maven項目並在上安裝生成的內容包AEM。
1. **更新自適應窗體**:更新自適應表單域屬性以使用自定義外觀。

### 建立項目 {#create-a-project}

主原型是建立自定義外觀的起點。 所用原型詳情如下：

* **儲存庫**:https://repo1.maven.org/maven2/com/adobe/
* **項目ID**:定制外觀原型
* **組ID**:com.adobe.aemforms
* **版本**:1.0.4

執行以下命令以基於原型建立本地項目：

`mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

該命令從儲存庫中下載Maven插件和原型資訊，並基於以下資訊生成項目：

* **組ID**:生成的Maven項目使用的組ID
* **項目ID**:生成的Maven項目使用的項目ID。
* **版本**:生成的Maven項目的版本。
* **包**:用於檔案結構的包。
* **項目名稱**:生成的包的對AEM像名。
* **包組**:生成的包的包AEM組。
* **小部件名稱**:用於引用的外觀名稱。

生成的項目具有以下結構：

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

### 擴展現有小部件類 {#extend-an-existing-widget-class}

建立項目模板後，根據需要進行以下更改：

1. 包括項目的第三方插件依賴項。

   1. 將第三方或自定義jQuery插件置於 `jqueryplugin/javascript` 資料夾和相關的CSS檔案 `jqueryplugin/css` 的子菜單。 有關詳細資訊，請參閱 `jqueryplugin/javascript and jqueryplugin/css` 的子菜單。

   1. 修改 `js.txt` 和 `css.txt` 檔案，以包括jQuery插件的任何其他JavaScript和CSS檔案。

1. 將第三方插件與框架整合，以啟用自定義外觀框架與jQuery插件之間的交互。 只有在擴展或覆蓋以下功能後，新小部件才能正常工作。

<table>
 <tbody>
  <tr>
   <td><strong>函數</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td><code>render</code></td>
   <td>呈現函式返回小部件的預設HTML元素的jQuery對象。 預設HTML元素應為可聚焦類型。 比如說， <code>&lt;a&gt;</code>。 <code>&lt;input&gt;</code>, <code>&lt;li&gt;</code>。 返回的元素用作 <code>$userControl</code>。 如果 <code>$userControl</code> 指定上述約束， <code>AbstractWidget</code> 類按預期工作，否則某些常見API（焦點，按一下）需要更改。 </td>
  </tr>
  <tr>
   <td><code>getEventMap</code></td>
   <td>返回將HTML事件轉換為XFA事件的映射。 <br /> <code class="code">{
      blur: XFA_EXIT_EVENT,
      }</code><br /> 此示例說明 <code>blur</code> 是HTML事件 <code>XFA_EXIT_EVENT</code> 是相應的XFA事件。 </td>
  </tr>
  <tr>
   <td><code>getOptionsMap</code></td>
   <td>返回一個映射，該映射提供有關在更改選項時要執行的操作的詳細資訊。 鍵是提供給小部件的選項，值是每當檢測到選項的更改時調用的函式。 該構件為所有常用選項(除 <code>value</code> 和 <code>displayValue</code>)。</td>
  </tr>
  <tr>
   <td><code>getCommitValue</code></td>
   <td>只要jQuery小部件的值保存在XFA模型中（例如，在文本欄位的退出事件上）,jQuery小部件框架就會載入該函式。 實現應返回小部件中保存的值。 該處理程式提供了該選項的新值。</td>
  </tr>
  <tr>
   <td><code>showValue</code></td>
   <td>預設情況下，在XFA中輸入事件時， <code>rawValue</code> 的上界。 調用此函式可顯示 <code>rawValue</code> 到用戶。 </td>
  </tr>
  <tr>
   <td><code>showDisplayValue</code></td>
   <td>預設情況下，在XFA on exit事件中， <code>formattedValue</code> 的上界。 調用此函式可顯示 <code>formattedValue</code> 到用戶。 </td>
  </tr>
 </tbody>
</table>

1. 在中更新JavaScript檔案 `integration/javascript` 資料夾。

   * 替代文字 `__widgetName__` 具有實際小部件名稱。
   * 從合適的開箱構件類擴展構件。 在大多數情況下，它是與要替換的現有小部件對應的小部件類。 父類名在多個位置使用，因此建議搜索字串的所有實例 `xfaWidget.textField` ，並將其替換為使用的實際父類。
   * 擴展 `render` 提供備用UI的方法。 它是調用jQuery插件以更新UI或交互行為的位置。 的 `render` 方法應返回用戶控制項元素。

   * 擴展 `getOptionsMap` 方法，以覆蓋因構件更改而受影響的任何選項設定。 該函式返回一個映射，該映射提供了選項更改時要執行的操作的詳細資訊。 鍵是提供給小部件的選項，值是每當檢測到選項的更改時調用的函式。
   * 的 `getEventMap` 方法將小部件觸發的事件與自適應表單模型所需的事件進行映射。 預設值映射預設小部件的標準HTML事件，如果觸發了備用事件，則需要更新。
   * 的 `showDisplayValue` 和 `showValue` 應用display and edit picture子句，並且可以覆蓋以具有替代行為。

   * 的 `getCommitValue` 方法由自適應表單框架調用 `commit`事件。 通常，它是退出事件，但下拉、單選按鈕和複選框元素在更改時發生的除外)。 有關詳細資訊，請參見 [自適應Forms表達式](../../forms/using/adaptive-form-expressions.md#p-value-commit-script-p)。

   * 模板檔案為各種方法提供了示例實現。 刪除不要擴展的方法。

### 建立客戶端庫 {#create-a-client-library}

由Maven原型生成的示例項目會自動建立所需的客戶端庫，並將它們包裝到具有類別的客戶端庫中 `af.customwidgets`。 中提供的JavaScript和CSS檔案 `af.customwidgets` 在運行時自動包含。

### 生成和安裝 {#build-and-install}

要生成項目，請在shell上執行以下命令以生成需要安裝在伺服器上的CRXAEM包。

`mvn clean install`

>[!NOTE]
>
>maven項目指POM檔案內的遠程儲存庫。 這僅供參考，根據Maven標準，儲存庫資訊在 `settings.xml` 的子菜單。

### 更新自適應窗體 {#update-the-adaptive-form}

要將自定義外觀應用於自適應表單域：

1. 在編輯模式下開啟自適應窗體。
1. 開啟 **屬性** 對話框，用於應用自定義外觀的欄位。
1. 在 **造型** 頁籤，更新 `CSS class` 屬性，以在 `widget_<widgetName>` 的子菜單。 例如： **widget_numeristepper**

## 示例：建立自定義外觀   {#sample-create-a-custom-appearance-nbsp}

現在，讓我們看一個示例，以為數字欄位建立一個自定義外觀，使其顯示為數字步進器或滑塊。 執行以下步驟：

1. 執行以下命令以基於Maven原型建立本地項目：

   `mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

   它提示您為以下參數指定值。
   *此示例中使用的值以粗體加亮*。

   `Define value for property 'groupId': com.adobe.afwidgets`

   `Define value for property 'artifactId': customWidgets`

   `Define value for property 'version': 1.0.1-SNAPSHOT`

   `Define value for property 'package': com.adobe.afwidgets`

   `Define value for property 'artifactName': customWidgets`

   `Define value for property 'packageGroup': adobe/customWidgets`

   `Define value for property 'widgetName': numericStepper`

1. 導航到 `customWidgets` (為 `artifactID` 屬性)目錄，並執行以下命令以生成Eclipse項目：

   `mvn eclipse:eclipse`

1. 開啟Eclipse工具，然後執行以下操作以導入Eclipse項目：

   1. 選擇 **[!UICONTROL 「檔案」(File)>「導入」(Import)>「現有項目」(Existing Projects)到Workspace]**。

   1. 瀏覽並選擇執行資料夾 `archetype:generate` 的子菜單。

   1. 按一下 **[!UICONTROL 完成]**。

      ![eclipse螢幕截圖](assets/eclipse-screenshot.png)

1. 選擇要用於自定義外觀的構件。 此示例使用以下數字步進小部件：

   [https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html](https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html)

   在Eclipse項目中，查看 `plugin.js` 檔案，確保其符合外觀要求。 在此示例中，外觀符合以下要求：

   * 數字步進器應從 `- $.xfaWidget.numericInput`。
   * 的 `set value` 小部件的方法在焦點位於欄位後設定值。 它是自適應表單構件的必備要求。
   * 的 `render` 需要重寫方法以調用 `bootstrapNumber` 的雙曲餘切值。

   * 除了插件的主原始碼之外，插件沒有其他依賴項。
   * 該示例在步進器上不執行任何樣式設定，因此不需要附加CSS。
   * 的 `$userControl` 對象應可用於 `render` 的雙曲餘切值。 它是 `text` 使用插件代碼克隆的類型。

   * 的 **+** 和 **-** 在禁用欄位時，應禁用按鈕。

1. 替換 `bootstrap-number-input.js` （jQuery插件） `numericStepper-plugin.js` 的子菜單。
1. 在 `numericStepper-widget.js` 檔案，添加以下代碼以覆蓋調用插件的render方法並返回 `$userControl` 對象：

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

1. 在 `numericStepper-widget.js` 檔案，覆蓋 `getOptionsMap` 屬性，以覆蓋訪問選項，並在禁用模式下隱藏+和 — 按鈕。

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

1. 保存更改，導航到包含 `pom.xml` ，然後執行以下Maven命令來生成項目：

   `mvn clean install`

1. 使用包管理器安AEM裝包。

1. 在要應用自定義外觀的編輯模式下開啟自適應窗體，然後執行以下操作：

   1. 按一下右鍵要應用外觀的欄位，然後按一下 **[!UICONTROL 編輯]** 開啟「編輯元件」(Edit Component)對話框。

   1. 在「樣式」(Styling)頁籤中，更新 **[!UICONTROL CSS類]** 添加屬性 `widget_numericStepper`。

您剛建立的新外觀現在可供使用。
