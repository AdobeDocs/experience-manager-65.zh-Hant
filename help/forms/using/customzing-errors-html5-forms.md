---
title: 自訂HTML5表單的錯誤訊息
seo-title: Customizing error messages for HTML5 forms
description: 了解如何自訂HTML5表單的錯誤訊息顯示，包括如何變更其位置和外觀。
seo-description: Learn how to customize the display of error messages for HTML5 forms including how to change their position and appearance.
uuid: 6f48b64e-858f-4323-ad50-88e25f3c2e3d
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 44e49789-9075-41b3-bce8-03e8efce2d5a
feature: Mobile Forms
exl-id: c4ae53a3-8de1-4985-a73e-829749de9814
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# 自訂HTML5表單的錯誤訊息 {#customizing-error-messages-for-html-forms}

在HTML5表單中，錯誤訊息和警告的立即可用位置和外觀（字型和顏色）固定，錯誤只針對選定欄位顯示，並且只顯示一個錯誤。

文章提供自訂HTML5表單錯誤訊息的步驟，

* 更改錯誤消息的外觀和位置。 您可以讓錯誤顯示在任何欄位的頂端、底部和右側。
* 在任何指定時刻顯示多個欄位的錯誤訊息。
* 顯示與欄位無關的錯誤是否已選取。

## 自訂錯誤訊息  {#customizing-error-messages-nbsp}

自訂錯誤訊息之前，請下載並解壓縮附加的套件(CustomErrorManager-1.0-SNAPSHOT.zip)。

解壓包後，開啟CustomErrorManager-1.0-SNAPSHOT資料夾。 它包含jcr_root和META-INF資料夾。 這些資料夾包含自訂錯誤訊息所需的CSS和.JS檔案。

[取得檔案](assets/customerrormanager-1.0-snapshot.zip)

### 自訂錯誤訊息的位置  {#customizing-the-position-of-error-messages-nbsp}

若要自訂錯誤訊息的位置，請新增 &lt;div> 標籤中填入 &lt;div> 標籤，並在 &lt;div> 標籤。 如需詳細步驟，請參閱下列程式：

1. 導覽至 `CustomErrorManager-1.0-SNAPSHOT`資料夾並開啟 `etc\clientlibs\mf-custom-error-manager\CustomErrorManager\javascript` 檔案夾。
1. 開啟 `customErrorManager.js` 檔案進行編輯。 此 `markError` 函式接受下列參數：

   |  |  |
   |---|---|
   | jqWidget | jqWidget是widget的控點。 |
   | msg | 包含錯誤訊息 |
   | 類型 | 表示錯誤或警告 |

1. 在現成可用的實作中，錯誤訊息會顯示在欄位右側。 若要讓錯誤訊息出現在頂端，請使用下列程式碼。

   ```javascript
   markError: function (jqWidget, msg, type) {
               var element = jqWidget.element,                                //Gives the div containing widget
                   pos = $(element).offset(),                          //Calculates the position of the div in the view port
                                                                   msgHeight = xfalib.view.util.TextMetrics.measureExtent(msg).height + 5;  //Calculating the height of the Error Message
                   styles = {};
                   styles.left = pos.left + "px";         // Assign the desired left position using pos.left. Here it is calculated for exact left of the field
                   styles.top = pos.top - msgHeight + "px";  // Assign the desired top position using pos.top. Here it is calculated for top of the field
               if (type != "warning") {
                   if(!jqWidget.errorDiv){
                                                                                   //Adding the warning div if it is not present already
                       jqWidget.errorDiv=$("<div id='customError'></div>").appendTo('body');
                   }
                   jqWidget.$css(jqWidget.errorDiv.get(0), styles); // Applying the styles to the warning div
                   jqWidget.errorDiv.text(msg).show();                     //Showing the warning message
               } else {
                   if(!jqWidget.errorDiv){
                                                                                   //Adding the error div if it is not present already
                       jqWidget.errorDiv=$("<div id='customWarning'></div>").appendTo('body');
                   }
                   jqWidget.$css(jqWidget.errorDiv.get(0), styles); // Applying the styles to the error div
                   jqWidget.errorDiv.text(msg).show();                     //Showing the warning message
               }
   
           },
   ```

1. 儲存並關閉檔案。
1. 導覽至 `CustomErrorManager-1.0-SNAPSHOT` 資料夾，並建立jcr_root和META-INF資料夾的封存。 將封存重新命名為CustomErrorManager-1.0-SNAPSHOT.zip。
1. 使用套件管理器來上傳和安裝套件。

## 顯示多個欄位的錯誤訊息  {#display-error-messages-for-multiple-fields-nbsp}

使用附加的包同時顯示所有欄位的錯誤消息。 若要顯示單一錯誤訊息，請使用預設設定檔。

### 自訂錯誤訊息的外觀。  {#customizing-the-appearance-of-error-messages-nbsp}

1. 導覽至etc\clientlibs\mf-custom-error-manager\CustomErrorManager\css folder。

1. 開啟要編輯的檔案sample.css。css檔案包含2個id- #customError、#customWarning。 您可以使用這些id來變更各種屬性，例如顏色、字型大小等。

   使用以下代碼更改錯誤/警告消息的字型大小和顏色。

   ```css
   #customError {
   color: #0000FF; // it changes the color of Error Message
   display:none;
   position:absolute;
   opacity:0.85;
   font-size: 24px;  // it changes the font size of Error Message
   z-index:5;
   }
   
   #customWarning {
   color: #00FF00;  // it changes the color of Warning Message
   display:none;
   position:absolute;
   opacity:0.85;
   font-size: 18px;   // it changes the font size of Warning Message
   z-index:5;
   }
   
   Save the changes.
   ```

1. 儲存並關閉檔案。
1. 導航到CustomErrorManager-1.0-SNAPSHOT資料夾，並建立jcr_root和META-INF資料夾的存檔。 將封存重新命名為CustomErrorManager-1.0-SNAPSHOT.zip。
1. 使用套件管理器來上傳和安裝套件。

## 使用新的配置檔案呈現表單。  {#render-the-form-with-the-new-profile-nbsp}

html5表單會立即使用預設設定檔：https://&lt;server>/content/xfaforms/profiles/default.html?contentRoot=&lt;xdp location=&quot;&quot;>&amp;template=&lt;name of=&quot;&quot; the=&quot;&quot; xdp=&quot;&quot;>

若要檢視含有自訂錯誤訊息的表單，請以錯誤設定檔呈現表單：https://&lt;server>/content/xfaforms/profiles/error.html?contentRoot=&lt;xdp location=&quot;&quot;>&amp;template=&lt;name of=&quot;&quot; the=&quot;&quot; xdp=&quot;&quot;>

>[!NOTE]
>
>附加的軟體包安裝錯誤配置檔案。
