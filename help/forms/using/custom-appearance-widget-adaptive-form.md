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

適用性表單會運用[外觀架構](/help/forms/using/introduction-widgets.md)，協助您為適用性表單欄位建立自訂外觀，並提供不同的使用者體驗。 例如，使用切換按鈕取代選項按鈕和核取方塊，或使用自訂jQuery外掛程式，限制使用者在電話號碼或電子郵件ID等欄位中的輸入。

本檔案說明如何使用jQuery外掛程式，為最適化表單欄位建立這些替代體驗。 此外，它還展示了一個示例，以建立數值欄位元件的自定義外觀，以作為數字步進器或滑塊顯示。

先來看看本文使用的主要術語和概念。

**** 外觀：指最適化表單欄位中各種元素的樣式、外觀和風格及組織。它通常包括標籤、提供輸入的互動區、幫助表徵圖以及欄位的簡短和長說明。 本文討論的外觀定制適用於欄位輸入區域的外觀。

**jQuery** plugin提供基於jQuery Widget框架的標準機制，以實作替代外觀。

**** ClientLib由複雜的JavaScript和CSS程式碼驅動的AEM用戶端處理中的用戶端程式庫系統。如需詳細資訊，請參閱使用用戶端程式庫。

**** 原型Maven專案範本工具套件定義為Maven專案的原始模式或模型。如需詳細資訊，請參閱原型簡介。

**User** Control（用戶控制）引用介面工具集中包含欄位值的主要元素，並用於外觀框架，用於將自定義介面工具集UI與自適應表單模型綁定。

## 建立自訂外觀的步驟 {#steps-to-create-a-custom-appearance}

建立自訂外觀的高階步驟如下：

1. **建立專案**:建立Maven專案，以產生要部署在AEM上的內容套件。
1. **擴展現有的Widget類**:擴展現有的Widget類並覆蓋所需的類。
1. **建立用戶端程式庫**:建立程 `clientLib: af.customwidget` 式庫並新增必要的JavaScript和CSS檔案。

1. **建置和安裝專案**:建立Maven專案，並在AEM上安裝產生的內容套件。
1. **更新最適化表單**:更新最適化表單欄位屬性以使用自訂外觀。

### 建立專案 {#create-a-project}

模仿原型是建立自訂外觀的起點。 要使用的原型詳細資訊如下：

* **存放庫**:https://repo1.maven.org/maven2/com/adobe/
* **工件Id**:自訂外觀原型
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

   1. 將第三方或自訂jQuery外掛程式放入`jqueryplugin/javascript`資料夾，並將相關CSS檔案放入`jqueryplugin/css`資料夾。 如需詳細資訊，請參閱`jqueryplugin/javascript and jqueryplugin/css`資料夾下的JS和CSS檔案。

   1. 修改`js.txt`和`css.txt`檔案，以包含jQuery外掛程式的任何其他JavaScript和CSS檔案。

1. 將協力廠商外掛程式與架構整合，以啟用自訂外觀架構與jQuery外掛程式之間的互動。 只有在您擴充或覆寫下列函式後，新介面工具集才能運作。

<table>
 <tbody>
  <tr>
   <td><strong>函數</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td><code>render</code></td>
   <td>呈現函式返回Widget預設HTML元素的jQuery對象。 預設HTML元素應為可聚焦類型。 例如，<code>&lt;a&gt;</code>、<code>&lt;input&gt;</code>和<code>&lt;li&gt;</code>。 傳回的元素會作為<code>$userControl</code>使用。 如果<code>$userControl</code>指定上述限制，則<code>AbstractWidget</code>類的函式將如預期運作，否則某些常見API（焦點、按一下）需要更改。 </td>
  </tr>
  <tr>
   <td><code>getEventMap</code></td>
   <td>傳回對應以將HTML事件轉換為XFA事件。 <br /> <code class="code">{
      blur: XFA_EXIT_EVENT,
      }</code><br /> 此範例顯示 <code>blur</code> 是HTML事件， <code>XFA_EXIT_EVENT</code> 是對應的XFA事件。 </td>
  </tr>
  <tr>
   <td><code>getOptionsMap</code></td>
   <td>傳回地圖，提供變更選項時要執行之動作的詳細資訊。 鍵是提供給介面工具集的選項，值是每當檢測到選項中的更改時調用的函式。 介面工具集為所有公用選項（<code>value</code>和<code>displayValue</code>除外）提供處理程式。</td>
  </tr>
  <tr>
   <td><code>getCommitValue</code></td>
   <td>每當jQuery Widget的值儲存在XFA模型中（例如，在文本欄位的退出事件上）時，jQuery Widget架構就會載入函式。 實作應傳回儲存在介面工具集中的值。 處理常式會隨選項的新值提供。</td>
  </tr>
  <tr>
   <td><code>showValue</code></td>
   <td>依預設，在輸入事件時的XFA中，會顯示欄位的<code>rawValue</code>。 調用此函式是為了向用戶顯示<code>rawValue</code>。 </td>
  </tr>
  <tr>
   <td><code>showDisplayValue</code></td>
   <td>依預設，在退出事件時的XFA中，會顯示欄位的<code>formattedValue</code>。 調用此函式是為了向用戶顯示<code>formattedValue</code>。 </td>
  </tr>
 </tbody>
</table>

1. 視需要更新`integration/javascript`資料夾中的JavaScript檔案。

   * 將文本`__widgetName__`替換為實際的Widget名稱。
   * 從適當的現成Widget類別擴充Widget。 在大多數情況下，它是與要取代的現有介面工具集相對應的介面工具集類別。 父類名用於多個位置，因此建議搜索檔案中字串`xfaWidget.textField`的所有實例，並將它們替換為實際使用的父類。
   * 擴充`render`方法以提供替代UI。 這是叫用jQuery外掛程式以更新UI或互動行為的位置。 `render`方法應傳回使用者控制元素。

   * 擴充`getOptionsMap`方法，以覆寫因介面工具集中的變更而影響的任何選項設定。 函式會傳回對應，提供在選項變更時要執行之動作的詳細資訊。 鍵是提供給介面工具集的選項，值是每當檢測到選項的更改時調用的函式。
   * `getEventMap`方法會將介面工具集觸發的事件與最適化表單模型所需的事件對應。 預設值會對應預設介面工具集的標準HTML事件，且如果觸發替代事件，則需要更新。
   * `showDisplayValue`和`showValue`應用顯示和編輯圖片子句，可以覆蓋以具有替代行為。

   * 當`commit`事件發生時，適用性表單架構會呼叫`getCommitValue`方法。 一般來說，它是退出事件，但下拉式清單、選項按鈕和核取方塊元素在變更時發生除外)。 如需詳細資訊，請參閱[適用性Forms運算式](../../forms/using/adaptive-form-expressions.md#p-value-commit-script-p)。

   * 範本檔案提供各種方法的範例實施。 移除不要擴充的方法。

### 建立用戶端程式庫 {#create-a-client-library}

Maven原型產生的範例專案會自動建立必要的用戶端程式庫，並以`af.customwidgets`類別將它們包裝到用戶端程式庫中。 在執行階段會自動包含`af.customwidgets`中可用的JavaScript和CSS檔案。

### 建置和安裝 {#build-and-install}

若要建置專案，請在殼層上執行下列命令，以產生需要安裝在AEM伺服器上的CRX套件。

`mvn clean install`

>[!NOTE]
>
>Maven專案會參照POM檔案中的遠端存放庫。 這僅供參考，而且根據Maven標準，儲存庫資訊會在`settings.xml`檔案中捕獲。

### 更新最適化表單 {#update-the-adaptive-form}

若要將自訂外觀套用至最適化表單欄位：

1. 在編輯模式中開啟最適化表單。
1. 為要應用自定義外觀的欄位開啟&#x200B;**屬性**&#x200B;對話框。
1. 在&#x200B;**Styling**&#x200B;標籤中，更新`CSS class`屬性以`widget_<widgetName>`格式添加外觀名稱。 例如：**widget_numericstepper**

## 範例：建立自訂外觀   {#sample-create-a-custom-appearance-nbsp}

現在，讓我們查看一個示例，以建立數字欄位的自定義外觀，以作為數字步進器或滑塊顯示。 執行下列步驟：

1. 執行下列命令，以根據Maven原型建立本機專案：

   `mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

   它會提示您為下列參數指定值。
   *此範例中使用的值會以粗體*&#x200B;強調顯示。

   `Define value for property 'groupId': com.adobe.afwidgets`

   `Define value for property 'artifactId': customWidgets`

   `Define value for property 'version': 1.0.1-SNAPSHOT`

   `Define value for property 'package': com.adobe.afwidgets`

   `Define value for property 'artifactName': customWidgets`

   `Define value for property 'packageGroup': adobe/customWidgets`

   `Define value for property 'widgetName': numericStepper`

1. 導覽至`customWidgets`（為`artifactID`屬性指定的值）目錄，然後執行以下命令以生成Eclipse項目：

   `mvn eclipse:eclipse`

1. 開啟Eclipse工具，然後執行下列操作以匯入Eclipse專案：

   1. 選取「**[!UICONTROL 檔案>匯入>將現有專案匯入Workspace]**」。

   1. 瀏覽並選擇執行`archetype:generate`命令的資料夾。

   1. 按一下&#x200B;**[!UICONTROL 完成]**。

      ![eclipse — 螢幕截圖](assets/eclipse-screenshot.png)

1. 選取要用於自訂外觀的介面工具集。 此示例使用以下數字步進器小部件：

   [https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html](https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html)

   在Eclipse專案中，檢閱`plugin.js`檔案中的外掛程式程式碼，確保其符合外觀的需求。 在此示例中，外觀滿足以下要求：

   * 數值步進器應從`- $.xfaWidget.numericInput`擴展。
   * 介面工具集的`set value`方法會在焦點位於欄位後設定值。 這是最適化表單Widget的必要需求。
   * 需要覆蓋`render`方法以調用`bootstrapNumber`方法。

   * 除了外掛程式的主要原始碼外，外掛程式沒有其他相依性。
   * 示例不對步進器執行任何樣式，因此不需要其他CSS。
   * `$userControl`物件應可用於`render`方法。 此欄位為`text`類型的欄位，會以外掛程式程式碼複製。

   * 禁用欄位時，應禁用&#x200B;**+**&#x200B;和&#x200B;**-**&#x200B;按鈕。

1. 將`bootstrap-number-input.js`（jQuery外掛程式）的內容替換為`numericStepper-plugin.js`檔案的內容。
1. 在`numericStepper-widget.js`檔案中，添加以下代碼以覆蓋呈現方法以調用插件並返回`$userControl`對象：

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

1. 在`numericStepper-widget.js`檔案中，覆蓋`getOptionsMap`屬性以覆蓋訪問選項，並在禁用模式下隱藏+和 — 按鈕。

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

1. 保存更改，導航到包含`pom.xml`檔案的資料夾，然後執行以下Maven命令以生成項目：

   `mvn clean install`

1. 使用AEM Package Manager安裝套件。

1. 在編輯模式中開啟您要套用自訂外觀的最適化表單，並執行下列動作：

   1. 按一下右鍵要應用外觀的欄位，然後按一下&#x200B;**[!UICONTROL Edit]**&#x200B;以開啟「Edit Component（編輯元件）」對話框。

   1. 在樣式標籤中，更新&#x200B;**[!UICONTROL CSS類]**&#x200B;屬性以新增`widget_numericStepper`。

您剛建立的新外觀現在可供使用。
