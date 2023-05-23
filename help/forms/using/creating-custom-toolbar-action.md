---
title: 建立自定義工具欄操作
seo-title: Creating a custom toolbar action
description: 表單開發人員可以在AEM Forms為自適應表單建立自定義工具欄操作。 使用自定義操作表單作者可以為其最終用戶提供更多工作流和選項。
seo-description: Form developers can create custom toolbar actions for adaptive forms in AEM Forms. Using custom actions form authors can provide more workflows and options to their end users.
uuid: cd785cfb-e1bb-4158-be9b-d99e04eccc02
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 4beca23f-dbb0-4e56-8047-93e4f1775418
docset: aem65
exl-id: 17f7f0e1-09d8-45cd-a4f6-0846bdb079b6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# 建立自定義工具欄操作{#creating-a-custom-toolbar-action}

## 必備條件 {#prerequisite}

在建立自定義工具欄操作之前，請熟悉 [使用客戶端庫](/help/sites-developing/clientlibs.md) 和 [用CRXDE Lite開發](/help/sites-developing/developing-with-crxde-lite.md)。

## 什麼是操作 {#what-is-an-action-br}

自適應表單提供了一個工具欄，使表單作者可以配置一組選項。 這些選項被定義為自適應表單的操作。 按一下「面板工具欄」中的「編輯」按鈕，設定自適應表單支援的操作。

![預設工具欄操作](assets/default_toolbar_actions.png)

除了預設提供的操作集之外，您還可以在工具欄中建立自定義操作。 例如，您可以添加一個操作，使用戶能夠在提交表單之前查看所有自適應表單域。

## 在自適應表單中建立自定義操作的步驟 {#steps}

為說明自定義工具欄操作的建立過程，以下步驟將指導您建立一個按鈕，供最終用戶在提交填充表單之前複查所有自適應表單域。

1. 自適應表單支援的所有預設操作都位於 `/libs/fd/af/components/actions` 的子菜單。 在CRXDE中，複製 `fileattachmentlisting` 節點 `/libs/fd/af/components/actions/fileattachmentlisting` 至 `/apps/customaction`。

1. 將節點複製到 `apps/customaction` 資料夾，將節點名稱更名為 `reviewbeforesubmit`。 另外，更改 `jcr:title` 和 `jcr:description` 節點的屬性。

   的 `jcr:title` 屬性包含工具欄對話框中顯示的操作的名稱。 的 `jcr:description` 屬性包含當用戶將指針懸停在操作上時顯示的詳細資訊。

   ![用於自定義工具欄的節點層次](assets/action3.png)

1. 選擇 `cq:template` 節點 `reviewbeforesubmit` 的下界。 確保 `guideNodeClass` 屬性 `guideButton` 改變 `jcr:title` 物業。
1. 更改 `cq:Template` 的下界。 對於當前示例，將type屬性更改為按鈕。

   類型值作為CSS類添加到元件的生成HTML中。 用戶可以使用該CSS類來設定其操作的樣式。 為按鈕、提交、重置和保存類型值提供了移動設備和台式機設備的預設樣式。

1. 從自適應表單編輯工具欄對話框中選擇自定義操作。 「審閱」按鈕顯示在面板的工具欄中。

   ![自定義操作在工具欄中可用](assets/custom_action_available_in_toolbar.png) ![顯示自定義建立的工具欄操作](assets/action7.png)

1. 要為「審閱」按鈕提供功能，請在init.jsp檔案中添加一些JavaScript和CSS代碼以及伺服器端代碼，這些代碼存在於 `reviewbeforesubmit` 的下界。

   在中添加以下代碼 `init.jsp`。

   ```jsp
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <guide:initializeBean name="guideField" className="com.adobe.aemds.guide.common.GuideButton"/>
   
   <c:if test="${not isEditMode}">
           <cq:includeClientLib categories="reviewsubmitclientlibruntime" />
   </c:if>
   
   <%--- BootStrap Modal Dialog  --------------%>
   <div class="modal fade" id="reviewSubmit" tabindex="-1">
       <div class="modal-dialog">
           <div class="modal-content">
               <div class="modal-header">
                   <h3>Review the Form Fields</h3>
               </div>
               <div class="modal-body">
                   <div class="modal-list">
                       <table class="table table-bordered">
                           <tr class="name">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Name is: </label>
                               </td>
                           </tr>
                           <tr class="pan">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Pan Number is: </label>
                               </td>
                           </tr>
                           <tr class="dob">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Date Of Birth is: </label>
                               </td>
                           </tr>
                           <tr class="80cdeclaration">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Total 80C Declaration Amount is: </label>
                               </td>
                           </tr>
                           <tr class="rentpaid">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Total HRA Amount is: </label>
                               </td>
                           </tr>
                       </table>
                   </div>
               </div><!-- /.modal-body -->
               <div class="modal-footer">
                   <div class="fileAttachmentListingCloseButton col-md-2 col-xs-2 col-sm-2">
                       <button data-dismiss="modal">Close</button>
                   </div>
               </div>
           </div><!-- /.modal-content -->
       </div><!-- /.modal-dialog -->
   </div><!-- /.modal -->
   ```

   在 `ReviewBeforeSubmit.js` 的子菜單。

   ```javascript
   /*anonymous function to handle show of review before submit view */
   $(function () {
       if($("div.reviewbeforesubmit button[id*=reviewbeforesubmit]").length > 0) {
           $("div.reviewbeforesubmit button[id*=reviewbeforesubmit]").click(function(){
               // Create the options object to be passed to the getElementProperty API
               var options = {},
                   result = [];
               options.somExpressions = [];
               options.propertyName = "value";
               guideBridge.visit(function(model){
                   if(model.name === "name" || model.name === "pan" || model.name === "dateofbirth" || model.name === "total" || model.name === "totalmonthlyrent"){
                           options.somExpressions.push(model.somExpression);
                   }
               }, this);
               result = guideBridge.getElementProperty(options);
   
               $('#reviewSubmit .reviewlabel').each(function(index, item){
                   var data = ((result.data[index] == null) ? "No Data Filled" : result.data[index]);
                   if($(this).next().hasClass("reviewlabelvalue")){
                       $(this).next().html(data);
                   } else {
                       $(this).after($("<td></td>").addClass("reviewlabelvalue col-md-6 active").html(data));
                   }
               });
               // added because in mobile devices it was causing problem of backdrop
               $("#reviewSubmit").appendTo('body');
               $("#reviewSubmit").modal("show");
           });
       }
   });
   ```

   將以下代碼添加到 `ReviewBeforeSubmit.css` 的子菜單。

   ```css
   .modal-list .reviewlabel {
       white-space: normal;
       text-align: right;
       padding:2px;
   }
   
   .modal-list .reviewlabelvalue {
       border: #cde0ec 1px solid;
       padding:2px;
   }
   
   /* Adding icon for this action in mobile devices */
   /* This is the glyphicon provided by bootstrap eye-open */
   /* .<type> .iconButton-icon */
   .reviewbeforesubmit .iconButton-icon {
       position: relative;
       top: -8px;
       font-family: 'Glyphicons Halflings';
       font-style: normal;
   }
   
   .reviewbeforesubmit .iconButton-icon:before {
       content: "\e105"
   }
   ```

1. 要驗證自定義操作的功能，請在「預覽」模式下開啟自適應表單，然後按一下工具欄中的「審閱」。

   >[!NOTE]
   >
   >的 `GuideBridge` 未在創作模式下載入庫。 因此，此自定義操作在創作模式下不起作用。

   ![演示自定義審閱按鈕的操作](assets/action9.png)

## 示例 {#samples}

以下存檔包含一個內容包。 該軟體包包括與自定義工具欄操作的上述演示相關的自適應表單。

[取得檔案](assets/customtoolbaractiondemo.zip)
