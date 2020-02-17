---
title: 將Form bridge與HTML5表單的自訂入口網站整合
seo-title: 將Form bridge與HTML5表單的自訂入口網站整合
description: 您可以使用FormBridge API從HTML頁面取得或設定表單欄位的值，並送出表單。
seo-description: 您可以使用FormBridge API從HTML頁面取得或設定表單欄位的值，並送出表單。
uuid: c8911f82-1a25-47a5-9a06-19b5dce74a2c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bd9bf095-d74d-458c-afe7-fab04050849d
docset: aem65
translation-type: tm+mt
source-git-commit: 19299fb5fc764d0e71c0ea3a5ec2286183dd6861

---


# 將Form bridge與HTML5表單的自訂入口網站整合{#integrating-form-bridge-with-custom-portal-for-html-forms}

FormBridge是HTML5 Forms Bridge API，可讓您與表單互動。 如需FormBridge API參考，請參閱 [FormBridge API參考](/help/forms/using/form-bridge-apis.md)。

您可以使用FormBridge API從HTML頁面取得或設定表單欄位的值，並送出表單。 例如，您可以使用API來建立類似精靈的體驗。

現有的HTML應用程式可運用FormBridge API與表單互動，並將它內嵌在HTML頁面中。 您可以使用下列步驟，使用Form Bridge API來設定欄位的值。

## 將HTML5表格整合至網頁 {#integrating-html-forms-to-a-web-page}

1. **選擇描述檔或建立描述檔**

   1. 在CRX DE介面中，導航至： `https://[server]:[port]/crx/de`。
   1. 使用管理員憑證登入。
   1. 建立描述檔或選擇現有描述檔。

      有關如何建立配置檔案的詳細資訊，請參 [閱建立新配置檔案](/help/forms/using/custom-profile.md)。

1. **修改HTML描述檔**

   在描述檔轉譯器中加入XFA執行時期、XFA地區設定程式庫和XFA表單HTML程式碼片段、設計您的網頁，並將表單置於網頁內。

   例如，使用下列程式碼片段，建立包含兩個輸入欄位和表單的應用程式，以展示表單與外部應用程式之間的互動。

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
   >第9 **行包含** CSS樣式和JavaScript檔案的其他JSP參考，以設計頁面。
   >
   >
   >第18行的&lt;div id=&quot;rightdiv&quot;>標 **簽包含** XFA表單的HTML程式碼片段。
   頁面樣式化為兩個容器： **左****右**。 正確的容器有表格。 左側容器有兩個輸入欄位，並包含外部HTML頁面的一部分。
   下列螢幕擷取畫面顯示表單在瀏覽器中的顯示方式。

   ![入口](assets/portal.jpg)

   左側是 **HTML頁面的一部分**。 包含欄位的右側是 **xfa表格**。

1. **從頁面存取表格欄位**

   以下是您可新增的範例指令碼，以在表單欄位中設定值。

   例如，如果要使用欄位 **名字和** 姓氏中的值設定 **EmployeeName** ，請調用 ******** window.formBridge.setFieldValue函式。

   同樣地，您也可以呼叫 **window.formBridge.getFieldValue** API來讀取值。

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

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
