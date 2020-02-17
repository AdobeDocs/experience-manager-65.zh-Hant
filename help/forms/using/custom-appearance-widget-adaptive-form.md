---
title: 建立最適化表單欄位的自訂外觀
seo-title: 建立最適化表單欄位的自訂外觀
description: 在最適化表單中自訂現成可用的元件外觀。
seo-description: 在最適化表單中自訂現成可用的元件外觀。
uuid: 1aa36443-774a-49fb-b3d1-d5a2d5ff849a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: d388acef-7313-4e68-9395-270aef6ef2c6
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 建立最適化表單欄位的自訂外觀{#create-custom-appearances-for-adaptive-form-fields}

## 簡介 {#introduction}

最適化表單可運用 [外觀架構](/help/forms/using/introduction-widgets.md) ，協助您為最適化表單欄位建立自訂外觀，並提供不同的使用者體驗。 例如，以切換按鈕取代選項按鈕和核取方塊，或使用自訂jQuery增效模組來限制使用者在諸如電話號碼或電子郵件ID等欄位中的輸入。

本檔案說明如何使用jQuery外掛程式來建立最適化表單欄位的替代體驗。 此外，它還展示了一個示例，用於為數字欄位元件建立自定義外觀，以顯示為數字步進器或滑塊。

我們先來看一下本文使用的關鍵術語和概念。

**外觀** ：指最適化表單欄位中各種元素的樣式、外觀和感覺。 它通常包含標籤、提供輸入的互動區域、說明圖示，以及欄位的簡短和長篇說明。 本文討論的外觀定制適用於該領域輸入區域的外觀。

**jQuery plugin** （jQuery增效模組）提供以jQuery Widget架構為基礎的標準機制，以實作替代外觀。

**ClientLib** :AEM用戶端處理中由複雜JavaScript和CSS程式碼驅動的用戶端程式庫系統。 如需詳細資訊，請參閱使用用戶端程式庫。

**原型** A Maven項目模板工具包定義為Maven項目的原始模式或模型。 如需詳細資訊，請參閱原型簡介。

**使用者控制** ：指介面工具集中包含欄位值的主要元素，並由外觀架構用來將自訂介面工具集UI與最適化表單模型系結。

## 建立自訂外觀的步驟 {#steps-to-create-a-custom-appearance}

建立自定義外觀的高級步驟如下：

1. **建立專案**:建立Maven專案，以產生要部署在AEM上的內容套件。
1. **擴充現有的Widget類別**:擴充現有的介面工具集類別並覆寫所需的類別。
1. **建立客戶端庫**:建立程 `clientLib: af.customwidget` 式庫並新增所需的JavaScript和CSS檔案。

1. **建立並安裝專案**:建立Maven專案，並在AEM上安裝產生的內容套件。
1. **更新最適化表單**:更新最適化表單欄位屬性，以使用自訂外觀。

### 建立專案 {#create-a-project}

主原型是建立自訂外觀的起點。 待用原型的詳細內容如下：

* **儲存庫**:https://repo.adobe.com/nexus/content/groups/public/
* **對象ID**:自訂外觀原型
* **群組ID**:com.adobe.aemforms
* **版本**:1.0.4

執行以下命令以基於原型建立本地項目：

`mvn archetype:generate -DarchetypeRepository=https://repo.adobe.com/nexus/content/groups/public/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

該命令從儲存庫下載Maven插件和原型資訊，並根據以下資訊生成項目：

* **groupId**:產生的Maven專案所使用的群組ID
* **artifactId**:生成的Maven項目使用的對象ID。
* **版本**:產生的Maven專案版本。
* **package**:用於檔案結構的包。
* **artifactName**:產生的AEM套件的對象名稱。
* **packageGroup**:產生的AEM套件的套件群組。
* **widgetName**:用於參考的外觀名稱。

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

### 擴充現有的Widget類別 {#extend-an-existing-widget-class}

建立專案範本後，請視需要進行下列變更：

1. 將協力廠商外掛程式相依性加入專案。

   1. 將協力廠商或自訂jQuery增效模組置於資料夾中， `jqueryplugin/javascript` 並將相關的CSS檔案置於資料 `jqueryplugin/css` 夾中。 如需詳細資訊，請參閱資料夾下的JS和CSS `jqueryplugin/javascript and jqueryplugin/css` 檔案。

   1. 修改和 `js.txt` 檔案 `css.txt` ，以包含jQuery外掛程式的任何其他JavaScript和CSS檔案。

1. 將協力廠商外掛程式與架構整合，讓自訂外觀架構與jQuery外掛程式之間互動。 新介面工具集只有在您擴充或覆寫下列函式後，才能運作。

<table>
 <tbody>
  <tr>
   <td><strong>函數</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td><code>render</code></td>
   <td>render函式返回構件的預設HTML元素的jQuery對象。 預設的HTML元素應為可聚焦類型。 例如， <code>&lt;a&gt;</code>、 <code>&lt;input&gt;</code>和 <code>&lt;li&gt;</code>。 傳回的元素會當做 <code>$userControl</code>。 如果指 <code>$userControl</code> 定上述限制，則類的函式會如 <code>AbstractWidget</code> 預期般運作，否則某些常用API（焦點、按一下）需要變更。 </td>
  </tr>
  <tr>
   <td><code>getEventMap</code></td>
   <td>傳回將HTML事件轉換為XFA事件的地圖。 <br /> <code class="code">{
      blur: XFA_EXIT_EVENT,
      }</code><br /> 此範例顯示 <code>blur</code> 是HTML事件， <code>XFA_EXIT_EVENT</code> 是對應的XFA事件。 </td>
  </tr>
  <tr>
   <td><code>getOptionsMap</code></td>
   <td>傳回地圖，其中提供選項變更時要執行之動作的詳細資訊。 鍵是提供給介面工具集的選項，值是在偵測到選項變更時呼叫的函式。 介面工具集提供所有常用選項（除和外）的處 <code>value</code> 理 <code>displayValue</code>常式。</td>
  </tr>
  <tr>
   <td><code>getCommitValue</code></td>
   <td>每當jQuery Widget的值儲存在XFA模型（例如在文字欄位的退出事件上）時，jQuery Widget架構就會載入函式。 實作應傳回儲存在介面工具集中的值。 處理常式會隨附選項的新值。</td>
  </tr>
  <tr>
   <td><code>showValue</code></td>
   <td>預設情況下，在XFA中輸入事件時， <code>rawValue</code> 將顯示該欄位。 此函式的呼叫是要向使 <code>rawValue</code> 用者顯示。 </td>
  </tr>
  <tr>
   <td><code>showDisplayValue</code></td>
   <td>依預設，在退出事件時的XFA中， <code>formattedValue</code> 會顯示欄位。 此函式的呼叫是要向使 <code>formattedValue</code> 用者顯示。 </td>
  </tr>
 </tbody>
</table>

1. 視需要更新資料夾 `integration/javascript` 中的JavaScript檔案。

   * 以實際的 `__widgetName__` 介面工具集名稱取代文字。
   * 從適當的現成可用介面工具集類別擴充介面工具集。 在大多數情況下，它是與要替換的現有Widget對應的Widget類。 父類名稱用於多個位置，因此建議搜索檔案中字串的所有實例，並將其替換 `xfaWidget.textField` 為實際使用的父類。
   * 擴充方 `render` 法以提供替代UI。 它是呼叫jQuery外掛程式以更新UI或互動行為的位置。 方 `render` 法應傳回使用者控制元素。

   * 擴充方 `getOptionsMap` 法以覆寫由於介面工具集變更而影響的任何選項設定。 函式返回映射，該映射提供了在選項更改時要執行的操作的詳細資訊。 鍵是提供給介面工具集的選項，而值是偵測到選項變更時呼叫的函式。
   * 此方 `getEventMap` 法會對應由介面工具集觸發的事件，以及最適化表單模型所需的事件。 預設值會對應預設介面工具集的標準HTML事件，若觸發替代事件，則需要更新。
   * 並應 `showDisplayValue` 用顯 `showValue` 示和編輯圖片子句，可以被覆蓋以具有替代行為。

   * 當事 `getCommitValue` 件發生時，自適應表單框架會調用 `commit`該方法。 通常是退出事件，但下拉式清單、選項按鈕和核取方塊元素在變更時除外)。 如需詳細資訊，請參 [閱最適化表單運算式](../../forms/using/adaptive-form-expressions.md#p-value-commit-script-p)。

   * 範本檔案提供各種方法的範例實作。 移除不要擴充的方法。

### 建立用戶端程式庫 {#create-a-client-library}

Maven原型產生的範例專案會自動建立必要的用戶端程式庫，並將它們封裝在具有類別的用戶端程式庫中 `af.customwidgets`。 在執行時期中會自動包含中 `af.customwidgets` 可用的JavaScript和CSS檔案。

### 建立和安裝 {#build-and-install}

若要建立專案，請在shell上執行下列命令，以產生需要安裝在AEM伺服器上的CRX套件。

`mvn clean install`

>[!NOTE]
>
>主項目引用POM檔案中的遠程儲存庫。 這僅供參考，根據Maven標準，儲存庫資訊將捕獲到檔案中 `settings.xml` 。

### 更新最適化表單 {#update-the-adaptive-form}

要將自定義外觀應用於最適化表單域，請執行以下操作：

1. 在編輯模式中開啟最適化表單。
1. 開啟 **要套用自訂外觀之欄位的「屬性** 」對話方塊。
1. 在「樣 **式** 」(Styling `CSS class` )頁籤中，更新屬 `widget_<widgetName>` 性以添加格式的外觀名稱。 例如： **widget_numericstepper**

## 範例：建立自訂外觀 {#sample-create-a-custom-appearance-nbsp}

現在，讓我們看一個示例，以建立數字欄位的自定義外觀，使其顯示為數字步進器或滑塊。 執行以下步驟：

1. 執行以下命令以基於Maven原型建立本地項目：

   `mvn archetype:generate -DarchetypeRepository=https://repo.adobe.com/nexus/content/groups/public/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

   它提示您指定下列參數的值。
   *此範例中使用的值會以粗體反白顯示*。

   `Define value for property 'groupId': com.adobe.afwidgets`

   `Define value for property 'artifactId': customWidgets`

   `Define value for property 'version': 1.0.1-SNAPSHOT`

   `Define value for property 'package': com.adobe.afwidgets`

   `Define value for property 'artifactName': customWidgets`

   `Define value for property 'packageGroup': adobe/customWidgets`

   `Define value for property 'widgetName': numericStepper`

1. 導覽至 `customWidgets` （屬性的指定值）目 `artifactID` 錄，然後執行下列命令以產生Eclipse專案：

   `mvn eclipse:eclipse`

1. 開啟Eclipse工具並執行下列動作以匯入Eclipse專案：

   1. 選擇「 **[!UICONTROL 檔案」>「匯入」>「現有專案至工作區」]**。

   1. 瀏覽並選擇執行命令的檔案 `archetype:generate` 夾。

   1. 按一 **[!UICONTROL 下完成]**。

      ![eclipse-screption](assets/eclipse-screenshot.png)

1. 選擇要用於自訂外觀的介面工具集。 此範例使用下列數值步進器Widget:

   [https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html](https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html)

   在Eclipse專案中，檢閱檔案中的外掛程式 `plugin.js` 碼，以確保符合外觀的需求。 在此示例中，外觀滿足以下要求：

   * 數值步進器應從擴展 `- $.xfaWidget.numericInput`。
   * 介面 `set value` 工具集的方法會在焦點位於欄位後設定值。 這是最適化表單Widget的必備要求。
   * 必須 `render` 覆寫方法，才能叫用 `bootstrapNumber` 方法。

   * 除了外掛程式的主要原始碼外，外掛程式沒有其他相依性。
   * 範例不會在步進器上執行任何樣式，因此不需要額外的CSS。
   * 對 `$userControl` 像應該可用於方 `render` 法。 它是使用外掛程式 `text` 碼複製的類型欄位。

   * 停用 **欄位時** ，應停用+ **** 和——按鈕。

1. 將(jQuery增效模 `bootstrap-number-input.js` 組)的內容取代為檔案的內 `numericStepper-plugin.js` 容。
1. 在檔案 `numericStepper-widget.js` 中，新增下列程式碼以覆寫演算方法以叫用外掛程式並傳回物 `$userControl` 件：

   ```java
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

1. 在檔 `numericStepper-widget.js` 案中，覆寫屬 `getOptionsMap` 性以覆寫存取選項，並在停用模式中隱藏+和——按鈕。

   ```java
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

1. 保存更改，導航到包含檔案的文 `pom.xml` 件夾，然後執行以下Maven命令以生成項目：

   `mvn clean install`

1. 使用AEM Package Manager安裝套件。

1. 在編輯模式中開啟您要套用自訂外觀的最適化表單，並執行下列動作：

   1. 按一下右鍵要應用外觀的欄位，然後按一下「編 **[!UICONTROL 輯]** 」(Edit)以開啟「編輯元件」(Edit Component)對話框。

   1. 在「樣式」索引標籤中，更新 **[!UICONTROL 要新增的CSS類別]** 屬性 `widget_numericStepper`。

您剛建立的新外觀現在可供使用。
