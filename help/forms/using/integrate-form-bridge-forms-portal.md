---
title: 將Form Bridge與自定義門戶整合，用於HTML5個表單
seo-title: Integrating Form Bridge with custom portal for HTML5 forms
description: 您可以使用FormBridge API從HTML頁獲取或設定表單域的值並提交表單。
seo-description: You can use the FormBridge API to get or set the values of form fields from the HTML page and submit the form.
uuid: c8911f82-1a25-47a5-9a06-19b5dce74a2c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bd9bf095-d74d-458c-afe7-fab04050849d
docset: aem65
feature: Mobile Forms
exl-id: 89118bb8-6ec8-4048-b3d6-5c73a9eea33e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---

# 將Form Bridge與自定義門戶整合，用於HTML5個表單{#integrating-form-bridge-with-custom-portal-for-html-forms}

FormBridge是HTML5forms bridge API，允許您與表單交互。 有關FormBridge API引用，請參見 [FormBridge API參考](/help/forms/using/form-bridge-apis.md)。

您可以使用FormBridge API從HTML頁獲取或設定表單域的值並提交表單。 例如，可以使用API構建類似嚮導的體驗。

現有HTML應用程式可以利用FormBridge API與表單交互並將其嵌入HTML頁。 可以使用以下步驟使用「表單橋」API設定欄位的值。

## 將HTML5表單整合到網頁 {#integrating-html-forms-to-a-web-page}

1. **選擇配置檔案或建立配置檔案**

   1. 在CRX DE介面中，導航到： `https://'[server]:[port]'/crx/de`。
   1. 使用管理員憑據登錄。
   1. 建立配置檔案或選擇現有配置檔案。

      有關如何建立配置檔案的詳細資訊，請參閱 [建立新配置檔案](/help/forms/using/custom-profile.md)。

1. **修改HTML配置檔案**

   將XFA運行時、XFA語言環境庫和XFA表單HTML段包括在配置檔案呈現器中，設計網頁，並將表單放在網頁內。

   例如，使用以下代碼段建立一個包含兩個輸入欄位和一個表單的應用程式，以演示表單與外部應用程式之間的交互。

   ```xml
   <%@ page session="false"
                  contentType="text/html; charset=utf-8"%><%
   %><%@ taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
   %><!DOCTYPE html>
   <html manifest="${param.offlineSpec}">
       <head>
          <cq:include script="formRuntime.jsp"/>
           <!-- Portal Scripts and Styles -->
          <cq:include script="portalheader.jsp"/>
       </head>
       <body>
           <div id="leftdiv" >
               <div id="leftdivcontentarea">
                   <!-- Portal Body -->
                 <cq:include script="portalbody.jsp"/>
               </div>
           </div>
           <div id="rightdiv">
               <div id="formBody">
               <cq:include script="config.jsp"/>
               <!-- Form body -->
               <cq:include script="formBody.jsp"/>
               <!  --To assist in page transitions -- add navigation, based on scrolling -->
               <cq:include  script="../nav/scroll/nav_footer.jsp"/>
               <cq:include script="footer.jsp"/>
               </div>
           </div>
       </body>
   </html>
   ```

   >[!NOTE]
   >
   >的 **行9**，包含用於設計頁面的CSS樣式和JavaScript檔案的其他JSP引用。
   >
   >
   >的 &lt;div id=&quot;rightdiv&quot;> 標籤 **上海地鐵18號線** 包含XFA表單的HTML段。
   該頁面按兩個容器的樣式設定： **左** 和 **右**。 正確的容器有形狀。 左容器有兩個輸入欄位和外部HTML頁的一部分。
   以下螢幕抓圖顯示了表單在瀏覽器中的顯示方式。

   ![門戶](assets/portal.jpg)

   左側是 **HTML頁**。 包含欄位的右側是 **xfa格式**。

1. **從頁面訪問表單域**

   下面是一個示例指令碼，您可以添加它以在表單欄位中設定值。

   例如，如果要設定 **員工姓名** 使用欄位中的值 **名字** 和 **姓氏**，調用 **window.formBridge.setFieldValue** 的子菜單。

   同樣，您可以通過調用 **window.formBridge.getFieldValue** API。

   ```javascript
   $(function() {
               $(".input").blur(function() {
                   window.formBridge.setFieldValue(
                               'xfa.form.form1.#subform[0].EmployeeName',
                                $("#lname").val()+' '+$("#fname").val()
                              )
                   });
           });
   ```
