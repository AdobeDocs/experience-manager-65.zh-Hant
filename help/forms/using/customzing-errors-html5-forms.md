---
title: 自訂HTML5表單的錯誤訊息
description: 瞭解如何自訂HTML5表單的錯誤訊息顯示，包括如何變更其位置和外觀。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
feature: HTML5 Forms
exl-id: c4ae53a3-8de1-4985-a73e-829749de9814
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 3%

---

# 自訂HTML5表單的錯誤訊息 {#customizing-error-messages-for-html-forms}

在HTML5表單中，錯誤訊息和警告在開箱即用的位置和外觀（字型和顏色）都是固定的，錯誤只會針對選取的欄位顯示，而且只會顯示一個錯誤。

本文提供自訂HTML5表單錯誤訊息的步驟，讓您可執行下列操作：

* 變更錯誤訊息的外觀和位置。 您可以製作錯誤以顯示於任何欄位的頂端、底端和右端。
* 在任何指定時刻顯示多個欄位的錯誤訊息。
* 無論是否選取欄位，都會顯示錯誤。

## 自訂錯誤訊息  {#customizing-error-messages-nbsp}

在自訂錯誤訊息之前，請下載並解壓縮附加的套件(CustomErrorManager-1.0-SNAPSHOT.zip)。

解壓縮套件後，請開啟CustomErrorManager-1.0-SNAPSHOT資料夾。 它包含jcr_root和META-INF資料夾。 這些資料夾包含自訂錯誤訊息所需的CSS和.JS檔案。

[取得檔案](assets/customerrormanager-1.0-snapshot.zip)

### 自訂錯誤訊息的位置  {#customizing-the-position-of-error-messages-nbsp}

若要自訂錯誤訊息的位置，請新增 &lt;div> 標籤每個錯誤和警告欄位，放置 &lt;div> 標籤進行標籤，並將css樣式套用至 &lt;div> 標籤之間。 如需詳細步驟，請參閱下列程式：

1. 導覽至 `CustomErrorManager-1.0-SNAPSHOT`資料夾並開啟 `etc\clientlibs\mf-custom-error-manager\CustomErrorManager\javascript` 資料夾。
1. 開啟 `customErrorManager.js` 檔案進行編輯。 此 `markError` 函式接受下列引數：

   |   |  |
   |---|---|
   | jqWidget | jqWidget是Widget的控制代碼。 |
   | msg | 包含錯誤訊息 |
   | 類型 | 表示這是錯誤或警告 |

1. 在開箱即用的實作中，錯誤訊息會顯示在欄位右側。 若要在頂端顯示錯誤訊息，請使用下列程式碼。

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
1. 導覽至 `CustomErrorManager-1.0-SNAPSHOT` 資料夾並建立jcr_root和META-INF資料夾的封存。 將封存重新命名為CustomErrorManager-1.0-SNAPSHOT.zip。
1. 使用封裝管理員來上傳及安裝封裝。

## 顯示多個欄位的錯誤訊息  {#display-error-messages-for-multiple-fields-nbsp}

使用附加的套件同時顯示所有欄位的錯誤訊息。 若要顯示單一錯誤訊息，請使用預設設定檔。

### 自訂錯誤訊息的外觀。  {#customizing-the-appearance-of-error-messages-nbsp}

1. 導覽至etc\clientlibs\mf-custom-error-manager\CustomErrorManager\css資料夾。

1. 開啟sample.css檔案進行編輯。 css檔案包含2個ID：#customError、#customWarning。 您可以使用這些ID來變更各種屬性，例如顏色和字型大小。

   使用下列程式碼來變更錯誤/警告訊息的字型大小和顏色。

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
1. 導覽至CustomErrorManager-1.0-SNAPSHOT資料夾，並建立jcr_root和META-INF資料夾的封存。 將封存重新命名為CustomErrorManager-1.0-SNAPSHOT.zip。
1. 使用封裝管理員來上傳及安裝封裝。

## 使用新設定檔轉譯表單。  {#render-the-form-with-the-new-profile-nbsp}

html5表單現成可使用預設設定檔： `https://&lt;server&gt;/content/xfaforms/profiles/default.html?contentRoot=&lt;xdp location&gt;&template=&lt;name of the xdp&gt;`

若要檢視含有自訂錯誤訊息的表單，請使用錯誤設定檔轉譯表單： `https://&lt;server&gt;/content/xfaforms/profiles/error.html?contentRoot=&lt;xdp location&gt;&template=&lt;name of the xdp&gt;`

>[!NOTE]
>
>附加的套件會安裝錯誤設定檔。
