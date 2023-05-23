---
title: 在建立對應用戶介面中添加自定義操作/按鈕
seo-title: Add custom action/button in Create Correspondence UI
description: 瞭解如何在建立對應用戶介面中添加自定義操作/按鈕
seo-description: Learn how to add custom action/button in Create Correspondence UI
uuid: 1b2b00bb-93ef-4bfe-9fc5-25c45e4cb4b1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 046e3314-b436-47ed-98be-43d85f576789
docset: aem65
feature: Correspondence Management
exl-id: a582ba41-83cb-46f2-9de9-3752f6a7820a
source-git-commit: ba2c753cfd041ccfcd6ba7a45648234290b99d25
workflow-type: tm+mt
source-wordcount: '1881'
ht-degree: 1%

---

# 在「建立對應UI」中添加自定義操作按鈕 {#add-custom-action-button-in-create-correspondence-ui}

## 概觀 {#overview}

「通信管理」解決方案允許您將自定義操作添加到「建立通信」用戶介面。

本文檔中的方案說明了如何在「建立對應用戶介面」中建立按鈕以將信件作為附加到電子郵件的審閱PDF共用。

### 必備條件 {#prerequisites}

要完成此方案，您需要執行以下操作：

* CRX和JavaScript知識
* LiveCycle伺服器

## 方案：在「建立對應用戶介面」中建立按鈕以發送信函以供審閱 {#scenario-create-the-button-in-the-create-correspondence-user-interface-to-send-a-letter-for-review}

向「建立通信用戶介面」添加一個帶有操作（此處發送信函供審閱）的按鈕，包括：

1. 將按鈕添加到「建立對應」用戶介面
1. 向按鈕添加操作處理
1. 添加LiveCycle進程以啟用操作處理

### 將按鈕添加到「建立對應」用戶介面 {#add-the-button-to-the-create-correspondence-user-interface}

1. 轉到 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身份登錄。
1. 在應用資料夾中，建立名為 `defaultApp` 路徑/結構與defaultApp資料夾（位於config資料夾中）類似。 使用以下步驟建立資料夾：

   1. 按一下右鍵 **預設應用** 資料夾，然後選擇 **覆蓋節點**:

      /libs/fd/cm/config/defaultApp/

      ![覆蓋節點](assets/1_defaultapp.png)

   1. 確保「覆蓋節點」對話框具有以下值：

      **路徑：** /libs/fd/cm/config/defaultApp/

      **覆蓋位置：** /apps/

      **匹配節點類型：** 已選中

      ![覆蓋節點](assets/2_defaultappoverlaynode.png)

   1. 按一下&#x200B;**「確定」**。
   1. 按一下 **全部保存**。

1. 製作acmExtensionsConfig.xml檔案（存在於/libs分支下）的/apps分支下的副本。

   1. 請訪問「/libs/fd/cm/config/defaultApp/acmExtensionsConfig.xml」

   1. 按一下右鍵acmExtensionsConfig.xml檔案，然後選擇 **複製**。

      ![複製acmExtensionsConfig.xml](assets/3_acmextensionsconfig_xml_copy.png)

   1. 按一下右鍵 **預設應用** 資料夾，位於「/apps/fd/cm/config/defaultApp/，」，並選擇 **貼上**。
   1. 按一下 **全部保存**。

1. 按兩下您在apps資料夾中新建立的acmExtentionsConfig.xml的副本。 開啟檔案進行編輯。
1. 找到以下代碼：

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <extensionsConfig>
       <modelExtensions>
           <modelExtension type="LetterInstance">
     <customAction name="Preview" label="loc.letterInstance.preview.label" tooltip="loc.letterInstance.preview.tooltip" styleName="previewButton"/>
               <customAction name="Submit" label="loc.letterInstance.submit.label" tooltip="loc.letterInstance.submit.tooltip" styleName="submitButton" permissionName="forms-users"/>
               <customAction name="SaveAsDraft" label="loc.letterInstance.saveAsDraft.label" tooltip="loc.letterInstance.saveAsDraft.tooltip" styleName="submitButton" permissionName="forms-users"/>
               <customAction name="Close" label="loc.letterInstance.close.label" tooltip="loc.letterInstance.close.tooltip" styleName="closeButton"/>
           </modelExtension>
       </modelExtensions>
   </extensionsConfig>
   ```

1. 要發送電子郵件，您可以使用LiveCycleForms Workflow。 在acmExtensionsConfig.xml中的modelExtension標籤下添加customAction標籤，如下所示：

   ```xml
    <customAction name="Letter Review" label="Letter Review" tooltip="Letter Review" styleName="" permissionName="forms-users" actionHandler="CM.domain.CCRCustomActionHandler">
         <serviceName>Forms Workflow -> SendLetterForReview/SendLetterForReviewProcess</serviceName>
       </customAction>
   ```

   ![customAction標籤](assets/5_acmextensionsconfig_xml.png)

   modelExtension標籤具有一組customAction子標籤，這些標籤配置了操作按鈕的操作、權限和外觀。 以下是customAction配置標籤的清單：

   | **名稱** | **說明** |
   |---|---|
   | 名稱 | 要執行的操作的字母數字名稱。 此標籤的值是必需的，必須是唯一的（在modelExtension標籤內），並且必須以字母開頭。 |
   | 標籤 | 要在操作按鈕上顯示的標籤 |
   | 提示 | 按鈕的工具提示文本，當用戶在按鈕上移動時顯示。 |
   | 樣式名稱 | 應用於操作按鈕的自定義樣式的名稱。 |
   | 權限名稱 | 僅當用戶具有permissionName指定的權限時，才會顯示相應的操作。 將permissionName指定為 `forms-users`，所有用戶都可以訪問此選項。 |
   | 操作處理程式 | 用戶按一下按鈕時調用的ActionHandler類的完全限定名稱。 |

   除了上述參數外，還可以有與customAction關聯的其他配置。 這些附加配置可通過CustomAction對象提供給處理程式。

   | **名稱** | **說明** |
   |---|---|
   | 服務名稱 | 如果customAction包含帶有名稱serviceName的子標籤，則按一下相關按鈕/連結時，將調用具有由serviceName標籤表示的名稱的進程。 確保此進程具有與Letter PostProcess相同的簽名。 在服務名中添加&quot;Forms Workflow->&quot;前置詞。 |
   | 標籤名稱中包含cm_前置詞的參數 | 如果customAction包含以名稱cm_開頭的子標籤，則在後處理（無論是字母后處理還是由serviceName標籤表示的特殊進程）中，這些參數在輸入XML代碼中的相關標籤下可用，並刪除cm_前置詞。 |
   | 操作名稱 | 只要帖子進程因按一下而出現，提交的XML就會在標籤下包含一個特殊標籤，其名稱與用戶操作的名稱相同。 |

1. 按一下 **全部保存**。

#### 在/apps分支中使用屬性檔案建立區域設定資料夾 {#create-a-locale-folder-with-properties-file-in-the-apps-branch}

ACMExtensionsMessages.properties檔案在「建立對應」用戶介面中包括各個欄位的標籤和工具提示消息。 要使自定義操作/按鈕工作，請在/apps分支中複製此檔案。

1. 按一下右鍵 **區域** 資料夾，然後選擇 **覆蓋節點**:

   /libs/fd/cm/config/defaultApp/locale

1. 確保「覆蓋節點」對話框具有以下值：

   **路徑：** /libs/fd/cm/config/defaultApp/locale

   **覆蓋位置：** /apps/

   **匹配節點類型：** 已選中

1. 按一下&#x200B;**「確定」**。
1. 按一下 **全部保存**。
1. 按一下右鍵以下檔案並選擇 **複製**:

   `/libs/fd/cm/config/defaultApp/locale/ACMExtensionsMessages.properties`

1. 按一下右鍵 **區域** 資料夾，然後選擇 **貼上**:

   `/apps/fd/cm/config/defaultApp/locale/`

   ACMExtensionsMessages.properties檔案在區域設定資料夾中複製。

1. 要本地化新添加的自定義操作/按鈕的標籤，請為中的相關區域設定建立ACMExtensionsMessages.properties檔案 `/apps/fd/cm/config/defaultApp/locale/`。

   例如，為本地化在本文中建立的自定義操作/按鈕，請使用以下條目建立一個名為ACMExtensionsMessages_fr.properties的檔案：

   `loc.letterInstance.letterreview.label=Revue De Lettre`

   同樣，可以在此檔案中添加更多屬性，如工具提示和樣式。

1. 按一下 **全部保存**。

#### 重新啟動AdobeAsset Composer構建塊捆綁包 {#restart-the-adobe-asset-composer-building-block-bundle}

進行每次伺服器端更改後，重新啟動AdobeAsset Composer構建塊捆綁包。 在此方案中，將編輯伺服器端的acmExtensionsConfig.xml和ACMExtensionsMessages.properties檔案，因此AdobeAsset Composer構建塊捆綁需要重新啟動。

>[!NOTE]
>
>您可能需要清除瀏覽器快取。

1. 前往 `https://[host]:'port'/system/console/bundles`. 如有必要，請以管理員身份登錄。

1. 找到AdobeAsset Composer構建塊捆綁包。 重新啟動包：按一下「Stop（停止）」 ，然後按一下「Start（開始）」。

   ![Adobe資產合成器構建塊](assets/6_assetcomposerbuildingblockbundle.png)

重新啟動AdobeAsset Composer構建塊捆綁包後，自定義按鈕將顯示在「建立對應用戶介面」中。 您可以在「建立對應用戶介面」中開啟一個信函以預覽自定義按鈕。

### 將操作處理添加到按鈕 {#add-action-handling-to-the-button}

預設情況下，「建立對應」用戶介面在cm.domain.js檔案中的以下位置實現了ActionHandler:

/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccr/js/cm.domain.js

對於自定義操作處理，請在CRX的/apps分支中建立cm.domain.js檔案的覆蓋。

在按一下操作/按鈕時處理操作/按鈕包括以下邏輯：

* 使新添加的操作變為可見/不可見：通過覆蓋actionVisible()函式完成。
* 啟用/禁用新添加的操作：通過覆蓋actionEnabled()函式完成。
* 當用戶按一下按鈕時實際處理操作：通過覆蓋handleAction()函式的實現來完成。

1. 前往 `https://'[server]:[port]'/[ContextPath]/crx/de`. 如有必要，請以管理員身份登錄。

1. 在應用資料夾中，建立名為 `js` 在CRX的/apps分支中，其結構類似於以下資料夾：

   `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

   使用以下步驟建立資料夾：

   1. 按一下右鍵 **j** 資料夾，然後選擇 **覆蓋節點**:

      `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

   1. 確保「覆蓋節點」對話框具有以下值：

      **路徑：** /libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js

      **覆蓋位置：** /apps/

      **匹配節點類型：** 已選中

   1. 按一下&#x200B;**「確定」**。
   1. 按一下 **全部保存**。

1. 在js資料夾中，使用以下步驟建立名為ccrcustomization.js的檔案，該檔案包含用於按鈕操作處理的代碼：

   1. 按一下右鍵 **j** 資料夾，然後選擇 **建立>建立檔案**:

      `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

      將檔案命名為crccustomization.js。

   1. 按兩下ccrcustomization.js檔案，在CRX中開啟它。
   1. 在檔案中，貼上以下代碼並按一下 **全部保存**:

      ```javascript
      /* for adding and handling custom actions in Extensible Toolbar.
        * One instance of handler will be created for each action.
        * CM.domain.CCRCustomActionHandler is actionHandler class.
        */
      var CCRCustomActionHandler;
          CCRCustomActionHandler = CM.domain.CCRCustomActionHandler = new Class({
              className: 'CCRCustomActionHandler',
              extend: CCRDefaultActionHandler,
              construct : function(action,model){
              }
          });
          /**
           * Called when user user click an action
           * @param extraParams additional arguments that may be passed to handler (For future use)
           */
          CCRCustomActionHandler.prototype.handleAction = function(extraParams){
              if (this.action.name == CCRCustomActionHandler.SEND_FOR_REVIEW) {
                  var sendForReview = function(){
                      var serviceName = this.action.actionConfig["serviceName"];
                      var inputParams = {};
                      inputParams["dataXML"] = this.model.iccData.data;
                      inputParams["letterId"] = this.letterVO.id;
                      inputParams["letterName"] = this.letterVO.name;
                      inputParams["mailId"] = $('#email').val();
                      /*function to invoke the LivecyleService */
                      ServiceDelegate.callJSONService(this,"lc.icc.renderlib.serviceInvoker.json","invokeProcess",[serviceName,inputParams],this.onProcessInvokeComplete,this.onProcessInvokeFail);
                      $('#ccraction').modal("hide");
                  }
                  if($('#ccraction').length == 0){
                      /*For first click adding popup & setting letterName.*/
                      $("body").append(popUp);
                      $("input[id*='letterName']").val(this.letterVO.name);
                      $(document).on('click',"#submitLetter",$.proxy( sendForReview, this ));
                  }
                  $('#ccraction').modal("show");
              }
          };
          /**
           * Should the action be enabled in toolbar
           * @param extraParams additional arguements that may be passed to handler (For future use)
           * @return flag indicating whether the action should be enabled
           */
         CCRCustomActionHandler.prototype.actionEnabled = function(extraParams){
                  /*can be customized as per user requirement*/
                  return true;
          };
          /**
           * Should the action be visible in toolbar
           * @param extraParams additional arguments that may be passed to handler (For future use)
           * @return flag indicating whether the action should be enabled
           */
          CCRCustomActionHandler.prototype.actionVisible = function(extraParams){
              /*Check can be enabled for Non-Preview Mode.*/
              return true;
          };
          /*SuccessHandler*/
          CCRCustomActionHandler.prototype.onProcessInvokeComplete = function(response) {
              ErrorHandler.showSuccess("Letter Sent for Review");
          };
          /*FaultHandler*/
          CCRCustomActionHandler.prototype.onProcessInvokeFail = function(event) {
              ErrorHandler.showError(event.message);
          };
          CCRCustomActionHandler.SEND_FOR_REVIEW  = "Letter Review";
      /*For PopUp*/
          var popUp = '<div class="modal fade" id="ccraction" tabindex="-1" role="dialog" aria-hidden="true">'+
          '<div class="modal-dialog modal-sm">'+
              '<div class="modal-content">' +
                  '<div class="modal-header">'+
                      '<button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</code></button>'+
                      '<h4 class="modal-title"> Send Review </h4>'+
                  '</div>'+
                  '<div class="modal-body">'+
                      '<form>'+
                          '<div class="form-group">'+
                              '<label class="control-label">Email Id</label>'+
                              '<input type="text" class="form-control" id="email">'+
                          '</div>'+
                          '<div class="form-group">'+
                              '<label  class="control-label">Letter Name</label>'+
                              '<input id="letterName" type="text" class="form-control" readonly>'+
                          '</div>'+
                          '<div class="form-group">'+
                              '<input id="letterData" type="text" class="form-control hide" readonly>'+
                          '</div>'+
                      '</form>'+
                  '</div>'+
                  '<div class="modal-footer">'+
                     '<button type="button" class="btn btn-default" data-dismiss="modal"> Cancel </button>'+
                     '<button type="button" class="btn btn-primary" id="submitLetter"> Submit </button>'+
                  '</div>'+
              '</div>'+
          '</div>'+
      '</div>';
      ```

### 添加LiveCycle進程以啟用操作 <span class="acrolinxCursorMarker"></code>處理 {#add-the-livecycle-process-to-enable-action-span-class-acrolinxcursormarker-span-handling}

在此方案中，啟用以下元件，這些元件是附加的components.zip檔案的一部分：

* DSC元件jar(DSCSample.jar)
* 發送複查流程LCA的信函(SendLetterForReview.lca)

下載並解壓縮components.zip檔案，以獲取DSCSample.jar和SendLetterForReview.lca檔案。 按照以下過程中指定的方式使用這些檔案。
[取得檔案](assets/components.zip)

#### 配置LiveCycle伺服器以運行LCA進程 {#configure-the-livecycle-server-to-run-the-lca-process}

>[!NOTE]
>
>只有在您處於OSGI設定中，並且要實施的自定義類型需要LC整合時，才需要此步驟。

LCA進程在LiveCycle伺服器上運行，需要伺服器地址和登錄憑據。

1. 轉到 `https://'[server]:[port]'/system/console/configMgr` 並以管理員身份登錄。
1. 找到AdobeLiveCycle客戶端SDK配置，然後按一下 **編輯** （編輯表徵圖）。 將開啟「配置」面板。

1. 輸入以下詳細資訊，然後按一下 **保存**:

   * **伺服器URL**:操作處理程式碼所使用的「發送以供審閱」服務的LC伺服器的URL。
   * **用戶名**:LC伺服器的管理用戶名
   * **密碼**:管理員用戶名的密碼

   ![AdobeLiveCycle客戶端SDK配置](assets/3_clientsdkconfiguration.png)

#### 安裝LiveCycle存檔(LCA) {#install-livecycle-archive-lca}

啟用電子郵件服務流程所需的LiveCycle流程。

>[!NOTE]
>
>要查看此流程的功能或建立您自己的類似流程，您需要Workbench。

1. 以管理員身份登錄到LiveCycle®伺服器adminui，位於 `https:/[lc server]/:[lc port]/adminui`。

1. 導航到 **首頁>服務>應用程式和服務>應用程式管理**。

1. 如果SendLetterForReview應用程式已存在，請跳過此過程中的其餘步驟，否則繼續執行下一步。

   ![UI中的SendLetterForReview應用程式](assets/12_applicationmanagementlc.png)

1. 按一下 **導入**。

1. 按一下 **選擇檔案** 並選擇SendLetterForReview.lca。

   ![選擇SendLetterForReview.lca檔案](assets/14_sendletterforreview_lca.png)

1. 按一下 **預覽**。

1. 選擇 **導入完成時將資產部署到運行時**。

1. 按一下 **導入**。

#### 將ServiceName添加到Allowlist服務清單 {#adding-servicename-to-the-allowlist-service-list}

在Experience Manager伺服器中提到要訪問Experience Manager伺服器的LiveCycle服務。

1. 以管理員身份登錄到 `https:/[host]:'port'/system/console/configMgr`。

1. 查找並按一下 **AdobeLiveCycle客戶端SDK配置**。 出現AdobeLiveCycle客戶端SDK配置面板。
1. 在「服務名稱」清單中，按一下+表徵圖並添加服務名稱 **SendLetterForReview/SendLetterForReviewProcess**。

1. 按一下「**儲存**」。

#### 配置電子郵件服務 {#configure-the-email-service}

在此方案中，要使Tergement Management能夠發送電子郵件，請在LiveCycle伺服器中配置電子郵件服務。

1. 使用管理員憑據登錄以LiveCycle伺服器adminui，時間： `https:/[lc server]:[lc port]/adminui`。

1. 導航到 **首頁>服務>應用程式和服務>服務管理**。

1. 查找並按一下 **電子郵件服務**。

1. 在 **SMTP主機**，配置電子郵件服務。

1. 按一下「**儲存**」。

#### 配置DSC服務 {#configure-the-dsc-service}

要使用Tergement Management API，請下載DSCSample.jar（作為components.zip的一部分附加在本文檔中）並將其上載到LiveCycle伺服器。 將DSCSample.jar檔案上載到LiveCycle伺服器後，Experience Manager伺服器使用DSCSample.jar檔案訪問renderLetter API。

有關詳細資訊，請參見 [連接AEM Forms與AdobeLiveCycle](/help/forms/using/aem-livecycle-connector.md)。

1. 更新DSCSample.jar中cmsa.properties中的Experience Manager伺服器URL，該URL位於以下位置：

   DSCSample.jar\com\adobe\livecycle\cmsa.properties

1. 在配置檔案中提供以下參數：

   * **crx.serverUrl**=https:/host:port/[上下文路徑]/[URLAEM]
   * **crx.username**=Experience Manager用戶名
   * **crx.password**=Experience Manager密碼
   * **crx.appRoot**=/內容/應用/公分

   >[!NOTE]
   >
   >每次在伺服器端進行任何更改時，請重新啟動LiveCycle伺服器。

   DSCSample.jar檔案使用renderLetter API。 有關renderLetter API的詳細資訊，請參見 [介面LetterRenderService](https://www.adobe.io/experience-manager/reference-materials/6-5/forms/javadocs/index.html?com/adobe/icc/ddg/api/LetterRenderService.html)。

#### 將DSC導入LiveCyle {#import-dsc-to-livecyle}

DSCSample.jar檔案使用renderLetter API將DSC提供作為輸入的XML資料中的字母作為PDF位元組呈現。 有關renderLetter和其他API的詳細資訊，請參見 [信件呈現服務](https://www.adobe.io/experience-manager/reference-materials/6-5/forms/javadocs/index.html?com/adobe/icc/ddg/api/LetterRenderService.html)。

1. 啟動Workbench並登錄。
1. 選擇 **「窗口」(Window)>「顯示視圖」(Show Views)>「元件」(Components)**。 「元件」視圖將添加到Workbench ES2。

1. 按一下右鍵 **元件** 選擇 **安裝元件**。

1. 選擇 **DSCSample.jar** 檔案瀏覽器，然後按一下 **開啟**。
1. 按一下右鍵 **呈現包裝** 選擇 **啟動元件**。 如果元件啟動，則元件名稱旁邊將出現綠色箭頭。

## 發送信函供審閱 {#send-letter-for-review}

在配置了用於發送信件以供審閱的操作和按鈕後：

1. 清除瀏覽器快取。

1. 在「建立對應」UI中，按一下 **信件審閱** 並指定審閱者的電子郵件ID。

1. 按一下 **提交**。

![森德列維](assets/sendreview.png)

審閱者從系統收到一封電子郵件，信函作為PDF附件。
