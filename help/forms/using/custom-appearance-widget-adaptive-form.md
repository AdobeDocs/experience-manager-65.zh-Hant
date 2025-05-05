---
title: 建立最適化表單欄位的自訂外觀
description: 在Adaptive Forms中自訂現成元件的外觀。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 770e257a-9ffd-46a4-9703-ff017ce9caed
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
source-git-commit: 8a77756e8ba771c8de9950c2323bef8f23cc59b4
workflow-type: tm+mt
source-wordcount: '1702'
ht-degree: 0%

---

# 建立最適化表單欄位的自訂外觀{#create-custom-appearances-for-adaptive-form-fields}

## 簡介 {#introduction}

最適化表單使用[外觀架構](/help/forms/using/introduction-widgets.md)來協助您建立最適化表單欄位的自訂外觀，並提供不同的使用者體驗。 例如，使用切換按鈕取代單選按鈕和核取方塊，或使用自訂jQuery外掛程式來限制使用者在電話號碼或電子郵件ID等欄位中的輸入。

本檔案說明如何使用jQuery外掛程式，為最適化表單欄位建立這些替代體驗。 此外，它展示了一個範例，說明如何為數值欄位元件建立自訂外觀，使其顯示為數值步進器或滑桿。

首先，我們來瞭解一下本文使用的主要辭彙和概念。

**外觀**&#x200B;參考最適化表單欄位中各種元素的樣式、外觀和風格，以及組織。 它通常包括標籤、提供輸入的互動區域、說明圖示，以及欄位的簡短和詳細說明。 本文討論的外觀自訂適用於欄位輸入區域的外觀。

**jQuery外掛程式**&#x200B;提供基於jQuery Widget架構的標準機制，以實作替代外觀。

**ClientLib** AEM使用者端處理中的使用者端程式庫系統，由複雜的JavaScript和CSS程式碼驅動。 如需詳細資訊，請參閱使用使用者端資料庫。

**Archetype**&#x200B;定義為Maven專案原始模式或模型的Maven專案範本工具組。 如需詳細資訊，請參閱原型簡介。

**使用者控制項**&#x200B;參考包含欄位值的Widget中的主要元素，該主要元素由外觀架構用於繫結自訂Widget UI與最適化表單模型。

## 建立自訂外觀的步驟 {#steps-to-create-a-custom-appearance}

建立自訂外觀的高層級步驟如下：

1. **建立專案**：建立Maven專案，此專案會產生內容套件以部署在AEM上。
1. **擴充現有的Widget類別**：擴充現有的Widget類別並覆寫必要的類別。
1. **建立使用者端資料庫**：建立`clientLib: af.customwidget`資料庫並新增必要的JavaScript和CSS檔案。

1. **建置並安裝專案**：建置Maven專案，並在AEM上安裝產生的內容封裝。
1. **更新最適化表單**：更新最適化表單欄位屬性以使用自訂外觀。

### 建立專案 {#create-a-project}

maven原型是建立自訂外觀的起點。 要使用的原型的詳細資訊如下：

* **存放庫**： https://repo1.maven.org/maven2/com/adobe/
* **成品ID**： custom-appearance-archetype
* **群組識別碼**： com.adobe.aemforms
* **版本**： 1.0.4

執行以下命令，根據原型建立本機專案：

`mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

該命令會從存放庫下載Maven外掛程式和原型資訊，並根據以下資訊產生專案：

* **groupId**：產生的Maven專案所使用的群組ID
* **artifactId**：產生的Maven專案所使用的成品ID。
* **版本**：產生的Maven專案的版本。
* **封裝**：用於檔案結構的封裝。
* **artifactName**：產生的AEM封裝的成品名稱。
* **packageGroup**：產生的AEM封裝的封裝群組。
* **widgetName**：用於參照的外觀名稱。

產生的專案具有以下結構：

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

建立專案範本後，視需要執行下列變更：

1. 將協力廠商外掛程式相依性納入專案中。

   1. 將協力廠商或自訂jQuery外掛程式放在`jqueryplugin/javascript`資料夾中，並將相關的CSS檔案放在`jqueryplugin/css`資料夾中。 如需詳細資訊，請參閱`jqueryplugin/javascript and jqueryplugin/css`資料夾下的JS和CSS檔案。

   1. 修改`js.txt`和`css.txt`檔案，加入jQuery外掛程式的任何其他JavaScript和CSS檔案。

1. 將協力廠商外掛程式與框架整合，以啟用自訂外觀框架與jQuery外掛程式之間的互動。 只有在您擴充或覆寫下列功能後，新Widget才能運作。

<table>
 <tbody>
  <tr>
   <td><strong>函數</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td><code>render</code></td>
   <td>轉譯器函式會傳回Widget預設HTML元素的jQuery物件。 預設HTML元素應為可聚焦型別。 例如，<code>&lt;a&gt;</code>、<code>&lt;input&gt;</code>和<code>&lt;li&gt;</code>。 傳回的專案用作<code>$userControl</code>。 如果<code>$userControl</code>指定上述條件約束，則<code>AbstractWidget</code>類別的功能會如預期般運作，否則某些常見的API （焦點、點按）需要變更。 </td>
  </tr>
  <tr>
   <td><code>getEventMap</code></td>
   <td>傳回對應以將HTML事件轉換為XFA事件。 <br /> <code class="code">&lbrace;
      blur: XFA_EXIT_EVENT,
      &rbrace;</code><br />此範例顯示<code>blur</code>是HTML事件，而<code>XFA_EXIT_EVENT</code>是相對應的XFA事件。 </td>
  </tr>
  <tr>
   <td><code>getOptionsMap</code></td>
   <td>傳回提供選項變更時執行動作詳細資訊的對應。 這些鍵是提供給Widget的選項，值是偵測到選項變更時呼叫的函式。 Widget為所有常用選項（除了<code>value</code>和<code>displayValue</code>）提供處理常式。</td>
  </tr>
  <tr>
   <td><code>getCommitValue</code></td>
   <td>每當jQuery Widget的值儲存在XFA模型中（例如，在文字欄位的退出事件中），jQuery Widget架構就會載入函式。 實作應傳回儲存在Widget中的值。 處理常式會提供選項的新值。</td>
  </tr>
  <tr>
   <td><code>showValue</code></td>
   <td>依預設，在XFA中，輸入事件時會顯示欄位的<code>rawValue</code>。 呼叫此函式是為了向使用者顯示<code>rawValue</code>。 </td>
  </tr>
  <tr>
   <td><code>showDisplayValue</code></td>
   <td>依預設，在退出事件的XFA中，會顯示欄位的<code>formattedValue</code>。 呼叫此函式是為了向使用者顯示<code>formattedValue</code>。 </td>
  </tr>
 </tbody>
</table>

1. 視需要更新`integration/javascript`資料夾中的JavaScript檔案。

   * 以實際的Widget名稱取代文字`__widgetName__`。
   * 從適當的現成可用Widget類別延伸Widget。 在大多數情況下，該物件是與要取代的現有Widget相對應的Widget類別。 父類別名稱使用於多個位置，因此建議搜尋檔案中字串`xfaWidget.textField`的所有執行個體，並將它們取代為實際使用的父類別。
   * 擴充`render`方法以提供替代的UI。 這是叫用jQuery外掛程式以更新UI或互動行為的位置。 `render`方法應該傳回使用者控制專案。

   * 擴充`getOptionsMap`方法，以覆寫任何由於Widget變更而受影響的選項設定。 此函式會傳回對應，提供選項變更時執行動作的詳細資訊。 鍵是提供給Widget的選項，值是偵測到選項變更時呼叫的函式。
   * `getEventMap`方法將對應由Widget觸發的事件，以及最適化表單模型所需的事件。 預設值對應預設Widget的標準HTML事件，如果觸發替代事件，則需要更新。
   * `showDisplayValue`與`showValue`套用顯示與編輯圖片子句，而且可以覆寫為有替代行為。

   * `commit`事件發生時，最適化表單架構會呼叫`getCommitValue`方法。 一般而言，這是退出事件（除了在變更時發生的下拉式清單、選項按鈕和核取方塊元素以外）。 如需詳細資訊，請參閱[最適化Forms運算式](../../forms/using/adaptive-form-expressions.md#p-value-commit-script-p)。

   * 範本檔案提供各種方法的範例實作。 移除不可擴充的方法。

### 建立使用者端資源庫 {#create-a-client-library}

Maven原型產生的範例專案會自動建立所需的使用者端資料庫，並將其包裝到類別為`af.customwidgets`的使用者端資料庫中。 `af.customwidgets`中可用的JavaScript和CSS檔案會在執行階段自動納入。

### 建置和安裝 {#build-and-install}

若要建置專案，請在殼層上執行以下命令，以產生需要安裝在AEM伺服器上的CRX套件。

`mvn clean install`

>[!NOTE]
>
>maven專案是指POM檔案內的遠端存放庫。 這僅供參考，根據Maven標準，存放庫資訊會在`settings.xml`檔案中擷取。

### 更新最適化表單 {#update-the-adaptive-form}

若要將自訂外觀套用至最適化表單欄位：

1. 在編輯模式中開啟最適化表單。
1. 開啟要套用自訂外觀之欄位的&#x200B;**屬性**&#x200B;對話方塊。
1. 在&#x200B;**樣式**&#x200B;索引標籤中，更新`CSS class`屬性以以`widget_<widgetName>`格式新增外觀名稱。 例如： **widget_numericstepper**

## 範例：建立自訂外觀   {#sample-create-a-custom-appearance-nbsp}

現在來看看範例，如何建立自訂外觀，讓數值欄位以數值步進器或滑桿顯示。 執行下列步驟：

1. 執行以下命令，根據Maven原型建立本機專案：

   `mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

   它會提示您指定下列引數的值。
   *此範例中使用的值會以粗體顯示*。

   `Define value for property 'groupId': com.adobe.afwidgets`

   `Define value for property 'artifactId': customWidgets`

   `Define value for property 'version': 1.0.1-SNAPSHOT`

   `Define value for property 'package': com.adobe.afwidgets`

   `Define value for property 'artifactName': customWidgets`

   `Define value for property 'packageGroup': adobe/customWidgets`

   `Define value for property 'widgetName': numericStepper`

1. 導覽至`customWidgets` （為`artifactID`屬性指定的值）目錄，然後執行下列命令來產生Eclipse專案：

   `mvn eclipse:eclipse`

1. 開啟Eclipse工具，並執行下列動作以匯入Eclipse專案：

   1. 選取&#x200B;**[!UICONTROL 檔案>匯入>將現有專案匯入Workspace]**。

   1. 瀏覽並選取您執行`archetype:generate`命令的資料夾。

   1. 按一下&#x200B;**[!UICONTROL 完成]**。

      ![eclipse-screenshot](assets/eclipse-screenshot.png)

1. 選取要用於自訂外觀的Widget。 此範例使用下列數值步進器Widget：

   [https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html](https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html)

   在Eclipse專案中，檢閱`plugin.js`檔案中的外掛程式程式碼，確保符合外觀要求。 在此範例中，外觀符合下列需求：

   * 數值步進器應從`- $.xfaWidget.numericInput`延伸。
   * Widget的`set value`方法會在焦點位於欄位之後設定值。 這是最適化表單Widget的強制要求。
   * 必須覆寫`render`方法才能叫用`bootstrapNumber`方法。

   * 外掛程式除了主要原始程式碼外，沒有其他相依性。
   * 範例不會在步進器上執行任何樣式，因此不需要額外的CSS。
   * `$userControl`物件應該可供`render`方法使用。 它是使用外掛程式程式碼複製的`text`型別欄位。

   * 停用欄位時，應該停用&#x200B;**+**&#x200B;和&#x200B;**-**&#x200B;按鈕。

1. 將`bootstrap-number-input.js` （jQuery外掛程式）的內容取代為`numericStepper-plugin.js`檔案的內容。
1. 在`numericStepper-widget.js`檔案中，新增下列程式碼以覆寫轉譯方法，以叫用外掛程式並傳回`$userControl`物件：

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

1. 在`numericStepper-widget.js`檔案中，覆寫`getOptionsMap`屬性以覆寫存取選項，並在停用模式中隱藏+和 — 按鈕。

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

1. 儲存變更，導覽至包含`pom.xml`檔案的資料夾，然後執行下列Maven命令以建置專案：

   `mvn clean install`

1. 使用AEM Package Manager安裝套件。

1. 在您要套用自訂外觀的編輯模式中開啟最適化表單，然後執行下列動作：

   1. 在您要套用外觀的欄位上按一下滑鼠右鍵，然後按一下&#x200B;**[!UICONTROL 編輯]**&#x200B;以開啟「編輯元件」對話方塊。

   1. 在[樣式]索引標籤中，更新&#x200B;**[!UICONTROL CSS類別]**&#x200B;屬性以新增`widget_numericStepper`。

您建立的新外觀現在可供使用。
