---
title: 自訂HTML5表單的錯誤訊息
seo-title: 自訂HTML5表單的錯誤訊息
description: 瞭解如何自訂HTML5表單的錯誤訊息顯示，包括如何變更其位置和外觀。
seo-description: 瞭解如何自訂HTML5表單的錯誤訊息顯示，包括如何變更其位置和外觀。
uuid: 6f48b64e-858f-4323-ad50-88e25f3c2e3d
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 44e49789-9075-41b3-bce8-03e8efce2d5a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 自訂HTML5表單的錯誤訊息 {#customizing-error-messages-for-html-forms}

在HTML5表單中，立即可用的錯誤訊息和警告具有固定的位置和外觀（字型和顏色），錯誤只會針對選取的欄位顯示，而且只會顯示一個錯誤。

文章提供將HTML5表單錯誤訊息自訂至、

* 更改錯誤消息的外觀和位置。 您可以在任何欄位的頂端、底部和右側顯示錯誤。
* 在任意給定時刻顯示多個欄位的錯誤消息。
* 顯示錯誤而不考慮選取的欄位。

## 自訂錯誤訊息 {#customizing-error-messages-nbsp}

在自訂錯誤訊息之前，請先下載並解壓縮附加的套件(CustomErrorManager-1.0-SNAPSHOT.zip)。

提取包後，開啟CustomErrorManager-1.0-SNAPSHOT資料夾。 它包含jcr_root和META-INF資料夾。 這些檔案夾包含自訂錯誤訊息所需的CSS和。JS檔案。

[取得檔案](assets/customerrormanager-1.0-snapshot.zip)

### 自定義錯誤消息的位置 {#customizing-the-position-of-error-messages-nbsp}

若要自訂錯誤訊息的位置，請針對每個錯誤和警告欄位新增&lt;div>標籤，將&lt;div>標籤置於左或右，並在&lt;div>標籤上套用css樣式。 如需詳細步驟，請參閱下列程式：

1. 導覽至資 `CustomErrorManager-1.0-SNAPSHOT`料夾並開啟資 `etc\clientlibs\mf-custom-error-manager\CustomErrorManager\javascript` 料夾。
1. 開啟檔 `customErrorManager.js` 案以進行編輯。 檔案 `markError` 中的函式接受以下參數：

   |  |  |
   |---|---|
   | jqWidget | jqWidget是Widget的控制代碼。 |
   | msg | 包含錯誤消息 |
   | 類型 | 表示是錯誤還是警告 |

1. 在開箱即用的實作中，欄位右側會顯示錯誤訊息。 若要讓錯誤訊息出現在頂端，請使用下列程式碼。

   ```
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
1. 導覽至檔 `CustomErrorManager-1.0-SNAPSHOT` 案夾並建立jcr_root和META-INF檔案夾的封存。 將封存重新命名為CustomErrorManager-1.0-SNAPSHOT.zip。
1. 使用套件管理器來上傳及安裝套件。

## 顯示多個欄位的錯誤訊息 {#display-error-messages-for-multiple-fields-nbsp}

使用附加的包可同時顯示所有欄位的錯誤消息。 若要顯示單一錯誤訊息，請使用預設描述檔。

### 自定義錯誤消息的外觀。  {#customizing-the-appearance-of-error-messages-nbsp}

1. 導覽至etc\clientlibs\mf-custom-error-manager\CustomErrorManager\css folder。

1. 開啟檔案sample.css以進行編輯。css檔案包含2個ID- #customError, #customWarning。 您可以使用這些ID來變更各種屬性，例如顏色、字型大小等。

   使用下列程式碼來變更錯誤／警告訊息的字型大小和顏色。

   ```
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
1. 導覽至CustomErrorManager-1.0-SNAPSHOT檔案夾，並建立jcr_root和META-INF檔案夾的封存。 將封存重新命名為CustomErrorManager-1.0-SNAPSHOT.zip。
1. 使用套件管理員來上傳及安裝套件。

## 使用新的描述檔來轉換表格。  {#render-the-form-with-the-new-profile-nbsp}

現成可用的html5表格會使用預設描述檔：https://&lt;server>/content/xfaforms/profiles/default.html?contentRoot=&lt;xdp location>&amp;template=&lt;xdp的名稱>

若要檢視含有自訂錯誤訊息的表單，請轉換含有錯誤描述檔的表單：https://&lt;server>/content/xfaforms/profiles/error.html?contentRoot=&lt;xdp location>&amp;template=&lt;xdp的名稱>

>[!NOTE]
>
>附加的軟體包安裝錯誤配置檔案。

