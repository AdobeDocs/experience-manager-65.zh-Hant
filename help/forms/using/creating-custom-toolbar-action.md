---
title: 建立自訂工具列動作
seo-title: Creating a custom toolbar action
description: 表單開發人員可在AEM Forms中為最適化表單建立自訂工具列動作。 使用自訂動作，表單作者可以為使用者提供更多工作流程和選項。
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

# 建立自訂工具列動作{#creating-a-custom-toolbar-action}

## 必備條件 {#prerequisite}

建立自訂工具列動作之前，請先熟悉 [使用用戶端程式庫](/help/sites-developing/clientlibs.md) 和 [使用CRXDE Lite開發](/help/sites-developing/developing-with-crxde-lite.md).

## 什麼是動作 {#what-is-an-action-br}

適用性表單提供工具列，可讓表單作者設定一組選項。 這些選項定義為最適化表單的動作。 按一下「面板」工具列中的「編輯」按鈕，設定最適化表單支援的動作。

![預設工具欄操作](assets/default_toolbar_actions.png)

除了預設提供的動作集之外，您還可以在工具列中建立自訂動作。 例如，您可以新增動作，讓使用者在提交表單之前檢閱所有最適化表單欄位。

## 在最適化表單中建立自訂動作的步驟 {#steps}

為了說明如何建立自訂工具列動作，下列步驟將引導您建立按鈕，讓使用者在提交已填寫的表單前，先檢閱所有最適化表單欄位。

1. 最適化表單支援的所有預設動作都顯示在 `/libs/fd/af/components/actions` 檔案夾。 在CRXDE中，複製 `fileattachmentlisting` 節點從 `/libs/fd/af/components/actions/fileattachmentlisting` to `/apps/customaction`.

1. 將節點複製到 `apps/customaction` 資料夾，將節點名稱更名為 `reviewbeforesubmit`. 此外，請變更 `jcr:title` 和 `jcr:description` 節點的屬性。

   此 `jcr:title` 屬性包含工具列對話方塊中顯示的動作名稱。 此 `jcr:description` 屬性包含當使用者將指標暫留在動作上時，所顯示的詳細資訊。

   ![用於工具欄定製的節點層次](assets/action3.png)

1. 選擇 `cq:template` 節點 `reviewbeforesubmit` 節點。 請確定 `guideNodeClass` 屬性為 `guideButton` 變更 `jcr:title` 屬性。
1. 變更 `cq:Template` 節點。 在目前範例中，將type屬性變更為按鈕。

   類型值會新增為元件所產生HTML中的CSS類別。 使用者可以使用該CSS類別來設定其動作的樣式。 行動裝置和案頭裝置的預設樣式是針對按鈕、提交、重設和儲存類型值而提供。

1. 從最適化表單編輯工具列對話方塊中選取自訂動作。 面板的工具欄中將顯示「審閱」按鈕。

   ![工具列中提供自訂動作](assets/custom_action_available_in_toolbar.png) ![顯示自訂建立的工具列動作](assets/action7.png)

1. 要為「查看」按鈕提供功能，請在init.jsp檔案中添加一些JavaScript和CSS代碼以及伺服器端代碼，該代碼出現在 `reviewbeforesubmit` 節點。

   在中新增下列程式碼 `init.jsp`.

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

   在 `ReviewBeforeSubmit.js` 檔案。

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

   將下列程式碼新增至 `ReviewBeforeSubmit.css` 檔案。

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

1. 若要驗證自訂動作的功能，請在「預覽」模式中開啟最適化表單，然後按一下工具列中的「檢閱」 。

   >[!NOTE]
   >
   >此 `GuideBridge` 程式庫未在製作模式中載入。 因此，此自訂動作在製作模式中無法運作。

   ![自訂檢閱按鈕的動作展示](assets/action9.png)

## 範例 {#samples}

以下歸檔包含內容包。 套件包含與上述自訂工具列動作示範相關的最適化表單。

[取得檔案](assets/customtoolbaractiondemo.zip)
