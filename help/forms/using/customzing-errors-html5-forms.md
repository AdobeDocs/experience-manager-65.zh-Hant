---
title: 自定義HTML5表單的錯誤消息
seo-title: Customizing error messages for HTML5 forms
description: 瞭解如何自定義HTML5個表單的錯誤消息顯示，包括如何更改其位置和外觀。
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

# 自定義HTML5表單的錯誤消息 {#customizing-error-messages-for-html-forms}

在HTML5窗體中，錯誤消息和警告具有固定的位置和外觀（字型和顏色），僅為選定欄位顯示錯誤，並且只顯示一個錯誤。

文章提供了將HTML5表單錯誤消息定制到、

* 更改錯誤消息的外觀和位置。 您可以在任何欄位的頂部、底部和右側顯示錯誤。
* 在任何給定時刻顯示多個欄位的錯誤消息。
* 顯示錯誤而不考慮是否選擇了某個欄位。

## 自定義錯誤消息  {#customizing-error-messages-nbsp}

在自定義錯誤消息之前，請下載並解壓附加的包(CustomErrorManager-1.0-SNAPSHOT.zip)。

解壓包後，開啟CustomErrorManager-1.0-SNAPSHOT資料夾。 它包含jcr_root和META-INF資料夾。 這些資料夾包含自定義錯誤消息所需的CSS和.JS檔案。

[取得檔案](assets/customerrormanager-1.0-snapshot.zip)

### 自定義錯誤消息的位置  {#customizing-the-position-of-error-messages-nbsp}

要自定義錯誤消息的位置，請添加 &lt;div> 標籤每個錯誤和警告欄位，定位 &lt;div> 在左側或右側添加標籤，並在 &lt;div> 標籤。 有關詳細步驟，請參閱下面列出的步驟：

1. 導航到 `CustomErrorManager-1.0-SNAPSHOT`資料夾並開啟 `etc\clientlibs\mf-custom-error-manager\CustomErrorManager\javascript` 的子菜單。
1. 開啟 `customErrorManager.js` 檔案。 的 `markError` 檔案中的函式接受以下參數：

   |  |  |
   |---|---|
   | jqWidget | jqWidget是小部件的句柄。 |
   | msg | 包含錯誤消息 |
   | 類型 | 指示是錯誤還是警告 |

1. 在開箱後的實現中，欄位右側出現錯誤消息。 要使錯誤消息顯示在頂部，請使用以下代碼。

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

1. 保存並關閉檔案。
1. 導航到 `CustomErrorManager-1.0-SNAPSHOT` 資料夾並建立jcr_root和META-INF資料夾的存檔。 將存檔檔案更名為CustomErrorManager-1.0-SNAPSHOT.zip。
1. 使用包管理器上載和安裝包。

## 顯示多個欄位的錯誤消息  {#display-error-messages-for-multiple-fields-nbsp}

使用附加的包同時顯示所有欄位的錯誤消息。 要顯示單條錯誤消息，請使用預設配置檔案。

### 自定義錯誤消息的外觀。  {#customizing-the-appearance-of-error-messages-nbsp}

1. 導航到etc\clientlibs\mf-custom-error-manager\CustomErrorManager\css folder。

1. 開啟檔案sample.css進行編輯。css檔案包含2個id- #customError和#customWarning。 可以使用這些ID更改各種屬性，如顏色、字型大小等。

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

1. 保存並關閉檔案。
1. 導航到CustomErrorManager-1.0-SNAPSHOT資料夾，然後建立jcr_root和META-INF資料夾的存檔檔案。 將存檔檔案更名為CustomErrorManager-1.0-SNAPSHOT.zip。
1. 使用包管理器上載和安裝包。

## 使用新配置檔案渲染窗體。  {#render-the-form-with-the-new-profile-nbsp}

現在，html5表單使用預設配置檔案：https://&lt;server>/content/xfaforms/profiles/default.html?contentRoot=&lt;xdp location=&quot;&quot;>&amp;模板=&lt;name of=&quot;&quot; the=&quot;&quot; xdp=&quot;&quot;>

要查看包含自定義錯誤消息的表單，請呈現包含錯誤配置檔案的表單：https://&lt;server>/content/xfaforms/profiles/error.html?contentRoot=&lt;xdp location=&quot;&quot;>&amp;模板=&lt;name of=&quot;&quot; the=&quot;&quot; xdp=&quot;&quot;>

>[!NOTE]
>
>附加的軟體包安裝錯誤配置檔案。
