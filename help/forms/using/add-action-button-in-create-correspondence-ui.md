---
title: 在建立通信UI中新增自訂動作/按鈕
seo-title: Add custom action/button in Create Correspondence UI
description: 了解如何在建立通信UI中新增自訂動作/按鈕
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

# 在建立通信UI中新增自訂動作按鈕 {#add-custom-action-button-in-create-correspondence-ui}

## 概觀 {#overview}

通信管理解決方案可讓您將自訂動作新增至「建立通信」使用者介面。

本檔案中的案例說明如何在「建立通信使用者介面」中建立按鈕，以共用信函作為附加至電子郵件的審核PDF。

### 必備條件 {#prerequisites}

若要完成此案例，您需要下列項目：

* CRX和JavaScript相關知識
* LiveCycle伺服器

## 案例：在建立通信用戶介面中建立按鈕，以發送信函以供審核 {#scenario-create-the-button-in-the-create-correspondence-user-interface-to-send-a-letter-for-review}

將具有動作的按鈕（此處傳送信函以供檢閱）新增至「建立通信使用者介面」，包括：

1. 將按鈕新增至建立通信使用者介面
1. 將動作處理新增至按鈕
1. 新增LiveCycle程式以啟用動作處理

### 將按鈕新增至建立通信使用者介面 {#add-the-button-to-the-create-correspondence-user-interface}

1. 前往 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身分登入。
1. 在應用程式資料夾中，建立名為 `defaultApp` 路徑/結構類似defaultApp資料夾（位於設定資料夾中）。 使用下列步驟建立資料夾：

   1. 以滑鼠右鍵按一下 **defaultApp** 資料夾（位於以下路徑），然後選取 **覆蓋節點**:

      /libs/fd/cm/config/defaultApp/

      ![覆蓋節點](assets/1_defaultapp.png)

   1. 確定「覆蓋節點」對話方塊有下列值：

      **路徑：** /libs/fd/cm/config/defaultApp/

      **覆蓋位置：** /apps/

      **匹配節點類型：** 已勾選

      ![覆蓋節點](assets/2_defaultappoverlaynode.png)

   1. 按一下&#x200B;**「確定」**。
   1. 按一下 **全部儲存**.

1. 複製/apps分支下的acmExtensionsConfig.xml檔案（存在於/libs分支下）。

   1. 前往「/libs/fd/cm/config/defaultApp/acmExtensionsConfig.xml」

   1. 以滑鼠右鍵按一下acmExtensionsConfig.xml檔案，然後選取 **複製**.

      ![複製acmExtensionsConfig.xml](assets/3_acmextensionsconfig_xml_copy.png)

   1. 以滑鼠右鍵按一下 **defaultApp** 資料夾（位於「/apps/fd/cm/config/defaultApp/，」），然後選取 **貼上**.
   1. 按一下 **全部儲存**.

1. 連按兩下您新在應用程式資料夾中建立的acmExtentionsConfig.xml副本。 檔案隨即開啟供編輯。
1. 找出下列程式碼：

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

1. 若要傳送電子郵件，您可以使用LiveCycleForms Workflow。 在acmExtensionsConfig.xml中的modelExtension標籤下新增customAction標籤，如下所示：

   ```xml
    <customAction name="Letter Review" label="Letter Review" tooltip="Letter Review" styleName="" permissionName="forms-users" actionHandler="CM.domain.CCRCustomActionHandler">
         <serviceName>Forms Workflow -> SendLetterForReview/SendLetterForReviewProcess</serviceName>
       </customAction>
   ```

   ![customAction標籤](assets/5_acmextensionsconfig_xml.png)

   modelExtension標籤有一組customAction子標籤，用於配置操作按鈕的操作、權限和外觀。 以下是customAction設定標籤的清單：

   | **名稱** | **說明** |
   |---|---|
   | 名稱 | 要執行的動作的英數字元名稱。 此標籤的值為必要值，必須是唯一的（在modelExtension標籤內），且必須以字母開頭。 |
   | 標籤 | 要在動作按鈕上顯示的標籤 |
   | 工具提示 | 按鈕的工具提示文字，當使用者將游標暫留在按鈕上時，就會顯示此文字。 |
   | styleName | 應用於操作按鈕的自定義樣式的名稱。 |
   | permissionName | 只有當使用者擁有permissionName所指定的權限時，才會顯示對應的動作。 將permissionName指定為 `forms-users`，所有使用者都能存取此選項。 |
   | actionHandler | 用戶按一下按鈕時調用的ActionHandler類的完全限定名稱。 |

   除了上述參數外，還可能有其他與customAction相關聯的設定。 這些附加配置可通過CustomAction對象提供給處理程式。

   | **名稱** | **說明** |
   |---|---|
   | serviceName | 如果customAction包含名為serviceName的子標籤，則按一下相關按鈕/連結時，將調用一個進程，該進程的名稱由serviceName標籤表示。 確保此進程與Letter PostProcess具有相同的簽名。 在服務名稱中新增「Forms Workflow->」首碼。 |
   | 標籤名稱中包含cm_前置詞的參數 | 如果customAction包含以名稱cm_開頭的子標籤，則在後置處理（無論是信函後置處理或serviceName標籤所代表的特殊處理）中，這些參數可在輸入XML代碼中的相關標籤下使用，並刪除cm_前置詞。 |
   | actionName | 每當貼文處理因點按而發生時，提交的XML都會在標籤下方包含一個特殊標籤，其名稱為使用者動作的名稱。 |

1. 按一下 **全部儲存**.

#### 在/apps分支中建立具有屬性檔案的區域設定資料夾 {#create-a-locale-folder-with-properties-file-in-the-apps-branch}

ACMExtensionsMessages.properties檔案包含「建立通信」用戶介面中各欄位的標籤和工具提示消息。 為了讓自訂動作/按鈕正常運作，請在/apps分支中製作此檔案的復本。

1. 以滑鼠右鍵按一下 **地區** 資料夾（位於以下路徑），然後選取 **覆蓋節點**:

   /libs/fd/cm/config/defaultApp/locale

1. 確定「覆蓋節點」對話方塊有下列值：

   **路徑：** /libs/fd/cm/config/defaultApp/locale

   **覆蓋位置：** /apps/

   **匹配節點類型：** 已勾選

1. 按一下&#x200B;**「確定」**。
1. 按一下 **全部儲存**.
1. 按一下右鍵以下檔案並選擇 **複製**:

   `/libs/fd/cm/config/defaultApp/locale/ACMExtensionsMessages.properties`

1. 以滑鼠右鍵按一下 **地區** 資料夾（位於以下路徑），然後選取 **貼上**:

   `/apps/fd/cm/config/defaultApp/locale/`

   ACMExtensionsMessages.properties檔案是在地區設定資料夾中複製的。

1. 要將新添加的自定義操作/按鈕的標籤本地化，請為中的相關區域設定建立ACMExtensionsMessages.properties檔案 `/apps/fd/cm/config/defaultApp/locale/`.

   例如，若要將本文中建立的自訂動作/按鈕翻譯為當地語系化，請建立名為ACMExtensionsMessages_fr.properties的檔案，並輸入下列項目：

   `loc.letterInstance.letterreview.label=Revue De Lettre`

   同樣地，您可以在此檔案中新增更多屬性，例如工具提示和樣式。

1. 按一下 **全部儲存**.

#### 重新啟動Adobe資產撰寫器建置區塊套件組合 {#restart-the-adobe-asset-composer-building-block-bundle}

進行每個伺服器端變更後，請重新啟動Adobe資產撰寫器建置區塊套件組合。 在此案例中，伺服器端的acmExtensionsConfig.xml和ACMExtensionsMessages.properties檔案經過編輯，因此Adobe資產撰寫器建置區塊套件組合需要重新啟動。

>[!NOTE]
>
>您可能需要清除瀏覽器快取。

1. 前往 `https://[host]:'port'/system/console/bundles`. 如有必要，請以管理員身分登入。

1. 找出Adobe資產撰寫器建置區塊套件組合。 重新啟動套件組合：按一下停止，然後按一下開始。

   ![Adobe資產撰寫器建置區塊](assets/6_assetcomposerbuildingblockbundle.png)

重新啟動Adobe資產撰寫器建置區塊套件組合後，自訂按鈕會顯示在建立通信使用者介面中。 您可以在建立通信使用者介面中開啟信函，以預覽自訂按鈕。

### 將動作處理新增至按鈕 {#add-action-handling-to-the-button}

預設情況下，建立通信用戶介面在cm.domain.js檔案中的以下位置具有ActionHandler的實現：

/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccr/js/cm.domain.js

對於自訂動作處理，請在CRX的/apps分支中建立cm.domain.js檔案的覆蓋。

在按一下動作/按鈕時處理動作/按鈕包含下列邏輯：

* 將新新增的動作設為可見/隱藏：透過覆寫actionVisible()函式來完成。
* 啟用/禁用新添加的操作：透過覆寫actionEnabled()函式來完成。
* 使用者按一下按鈕時的實際動作處理：覆寫handleAction()函式的實作。

1. 前往 `https://'[server]:[port]'/[ContextPath]/crx/de`. 如有必要，請以管理員身分登入。

1. 在應用程式資料夾中，建立名為 `js` (位於CRX的/apps分支中，其結構類似於下列資料夾：

   `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

   使用下列步驟建立資料夾：

   1. 以滑鼠右鍵按一下 **js** 資料夾（位於以下路徑），然後選取 **覆蓋節點**:

      `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

   1. 確定「覆蓋節點」對話方塊有下列值：

      **路徑：** /libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js

      **覆蓋位置：** /apps/

      **匹配節點類型：** 已勾選

   1. 按一下&#x200B;**「確定」**。
   1. 按一下 **全部儲存**.

1. 在js資料夾中，使用按鈕的動作處理程式碼，建立名為ccrcustomization.js的檔案，步驟如下：

   1. 以滑鼠右鍵按一下 **js** 資料夾（位於以下路徑），然後選取 **建立>建立檔案**:

      `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/js`

      將檔案命名為ccrcustomization.js。

   1. 連按兩下ccrcustomization.js檔案，以在CRX中開啟它。
   1. 在檔案中，貼上下列程式碼，然後按一下 **全部儲存**:

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

### 新增LiveCycle程式以啟用動作 <span class="acrolinxCursorMarker"></code>處理 {#add-the-livecycle-process-to-enable-action-span-class-acrolinxcursormarker-span-handling}

在此案例中，請啟用下列元件，這些元件是附加元件.zip檔案的一部分：

* DSC元件jar(DSCSample.jar)
* 發送供審核流程LCA的信函(SendLetterForReview.lca)

下載並解壓縮components.zip檔案，以取得DSCSample.jar和SendLetterForReview.lca檔案。 按照以下過程中的指定使用這些檔案。
[取得檔案](assets/components.zip)

#### 配置LiveCycle伺服器以運行LCA進程 {#configure-the-livecycle-server-to-run-the-lca-process}

>[!NOTE]
>
>只有在您處於OSGI設定中，且要實作的自訂類型需要LC整合時，才需要執行此步驟。

LCA進程在LiveCycle伺服器上運行，需要伺服器地址和登錄憑據。

1. 前往 `https://'[server]:[port]'/system/console/configMgr` 並以管理員身分登入。
1. 找出AdobeLiveCycle用戶端SDK設定，然後按一下 **編輯** （編輯圖示）。 「配置」面板隨即開啟。

1. 輸入以下詳細資訊，然後按一下 **儲存**:

   * **伺服器Url**:操作處理程式代碼使用的Send For Review服務的LC伺服器的URL。
   * **使用者名稱**:LC伺服器的管理員用戶名
   * **密碼**:管理員用戶名的密碼

   ![AdobeLiveCycle用戶端SDK設定](assets/3_clientsdkconfiguration.png)

#### 安裝LiveCycle歸檔(LCA) {#install-livecycle-archive-lca}

啟用電子郵件服務流程所需的LiveCycle流程。

>[!NOTE]
>
>若要檢視此程式的功用，或自行建立類似程式，您需要Workbench。

1. 以管理員身分登入以LiveCycle® Server adminui() `https:/[lc server]/:[lc port]/adminui`.

1. 導覽至 **首頁>服務>應用程式和服務>應用程式管理**.

1. 如果SendLetterForReview應用程式已存在，請跳過此過程中的其餘步驟，否則繼續執行後續步驟。

   ![UI中的SendLetterForReview應用程式](assets/12_applicationmanagementlc.png)

1. 按一下 **匯入**.

1. 按一下 **選擇檔案** 並選擇SendLetterForReview.lca。

   ![選擇SendLetterForReview.lca檔案](assets/14_sendletterforreview_lca.png)

1. 按一下 **預覽**.

1. 選擇 **匯入完成時，將資產部署至執行階段**.

1. 按一下 **匯入**.

#### 將ServiceName添加到允許清單服務清單 {#adding-servicename-to-the-allowlist-service-list}

在Experience Manager伺服器中提及您要存取Experience Manager伺服器的LiveCycle服務。

1. 以管理員身分登入 `https:/[host]:'port'/system/console/configMgr`.

1. 找到並按一下 **AdobeLiveCycle用戶端SDK設定**. AdobeLiveCycle用戶端SDK設定面板隨即顯示。
1. 在「服務名稱」清單中，按一下+圖示並新增服務名稱 **SendLetterForReview/SendLetterForReviewProcess**.

1. 按一下「**儲存**」。

#### 設定電子郵件服務 {#configure-the-email-service}

在此案例中，若要讓通信管理能夠傳送電子郵件，請在LiveCycle伺服器中設定電子郵件服務。

1. 使用管理員憑證登入，以LiveCycle伺服器adminui `https:/[lc server]:[lc port]/adminui`.

1. 導覽至 **首頁>服務>應用程式和服務>服務管理**.

1. 找到並按一下 **EmailService**.

1. 在 **SMTP主機**，設定電子郵件服務。

1. 按一下「**儲存**」。

#### 配置DSC服務 {#configure-the-dsc-service}

若要使用通信管理API，請下載DSCSample.jar（附於本檔案中，作為components.zip的一部分）並上傳至LiveCycle伺服器。 將DSCSample.jar檔案上傳到LiveCycle伺服器後，Experience Manager伺服器使用DSCSample.jar檔案來訪問renderLetter API。

如需詳細資訊，請參閱 [將AEM Forms與AdobeLiveCycle](/help/forms/using/aem-livecycle-connector.md).

1. 更新DSCSample.jar中cmsa.properties中的Experience Manager伺服器URL，該位置如下：

   DSCSample.jar\com\adobe\livecycle\cmsa.properties

1. 在設定檔案中提供下列參數：

   * **crx.serverUrl**=https:/host:port/[內容路徑]/[AEM URL]
   * **crx.username**=Experience Manager用戶名
   * **crx.password**=Experience Manager密碼
   * **crx.appRoot**=/content/apps/cm

   >[!NOTE]
   >
   >每次在伺服器端進行任何變更時，請重新啟動LiveCycle伺服器。

   DSCSample.jar檔案使用renderLetter API。 如需renderLetter API的詳細資訊，請參閱 [介面LetterRenderService](https://www.adobe.io/experience-manager/reference-materials/6-5/forms/javadocs/index.html?com/adobe/icc/ddg/api/LetterRenderService.html).

#### 將DSC匯入LiveCyle {#import-dsc-to-livecyle}

DSCSample.jar檔案使用renderLetter API從DSC作為輸入提供的XML資料中，將字母轉譯為PDF位元組。 如需renderLetter和其他API的詳細資訊，請參閱 [信函轉譯服務](https://www.adobe.io/experience-manager/reference-materials/6-5/forms/javadocs/index.html?com/adobe/icc/ddg/api/LetterRenderService.html).

1. 啟動Workbench並登入。
1. 選擇 **「窗口」>「顯示視圖」>「元件」**. 元件檢視會新增至Workbench ES2。

1. 按一下右鍵 **元件** 選取 **安裝元件**.

1. 選取 **DSCSample.jar** 檔案，然後按一下 **開啟**.
1. 按一下右鍵 **RenderWrapper** 選取 **開始元件**. 如果元件啟動，元件名稱旁會出現綠色箭頭。

## 發送信函以供審核 {#send-letter-for-review}

設定好傳送信函以供審核的動作和按鈕後：

1. 清除瀏覽器快取。

1. 在建立通信UI中，按一下 **信件審閱** 並指定審核者的電子郵件ID。

1. 按一下 **提交**.

![森德雷維](assets/sendreview.png)

審核者從系統收到一封電子郵件，信件作為PDF附件。
