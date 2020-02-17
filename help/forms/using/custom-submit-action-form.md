---
title: 編寫最適化表單的自訂提交動作
seo-title: 編寫最適化表單的自訂提交動作
description: AEM Forms可讓您建立最適化表單的自訂「提交」動作。 本文說明為最適化表單新增自訂「提交」動作的程式。
seo-description: AEM Forms可讓您建立最適化表單的自訂「提交」動作。 本文說明為最適化表單新增自訂「提交」動作的程式。
uuid: fd8e1dac-b997-4e86-aaf6-3507edcb3070
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 2a2e1156-4a54-4b0a-981c-d527fe22a27e
docset: aem65
translation-type: tm+mt
source-git-commit: dfa983db4446cbb0cbdeb42297248aba55b3dffd

---


# 編寫最適化表單的自訂提交動作{#writing-custom-submit-action-for-adaptive-forms}

最適化表單需要「提交」動作來處理使用者指定的資料。 「提交」操作決定使用自適應表單對提交的資料執行的任務。 Adobe Experience Manager(AEM)包含 [OOTB Submit動作](../../forms/using/configuring-submit-actions.md) ，可展現您可使用使用者提交資料執行的自訂工作。 例如，您可以執行工作，例如傳送電子郵件或儲存資料。

## 提交動作的工作流程 {#workflow-for-a-submit-action}

流程圖描述了在最適化表單中按一下「提交」按鈕時觸發的「提交」 **[!UICONTROL 操作]** 的工作流。 檔案附件元件中的檔案會上傳至伺服器，而表單資料會以已上傳檔案的URL更新。 在用戶端中，資料會以JSON格式儲存。 用戶端會傳送Ajax要求給內部servlet，以按照您指定的資料，並以XML格式傳回。 客戶端用操作欄位整理此資料。 它通過表單提交操作將資料提交到最終servlet（指南提交servlet）。 然後，Servlet將控制項轉發到「提交」操作。 「提交」動作可將請求轉送至其他sling資源，或將瀏覽器重新導向至其他URL。

![描述「提交」操作工作流的流程圖](assets/diagram1.png)

### XML資料格式 {#xml-data-format}

XML資料會使用請求參數傳送至 **`jcr:data`** servlet。 提交動作可存取參數以處理資料。 以下程式碼說明XML資料的格式。 綁定到「表單」(Form)模型的欄位將出現在該 **`afBoundData`** 部分。 未綁定的欄位將顯示在 `afUnoundData`部分中。 如需檔案格式的詳細資訊，請參 `data.xml` 閱預填 [最適化表單欄位的簡介](../../forms/using/prepopulate-adaptive-form-fields.md)。

```xml
<?xml ?>
<afData>
<afUnboundData>
<data>
<field1>value</field2>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
</data>
</afUnboundData>
<afBoundData>
<!-- xml corresponding to the Form Model /XML Schema -->
</afBoundData>
</afData>
```

### 動作欄位 {#action-fields}

「提交」動作可將隱藏的輸入欄位(使用HTML [輸入](https://developer.mozilla.org/en/docs/Web/HTML/Element/Input) 標籤)新增至轉譯的HTML表單。 這些隱藏欄位可包含處理表單提交時所需的值。 提交表單時，這些欄位值會張貼回請求參數，「提交」動作可在提交處理期間使用。 輸入欄位稱為動作欄位。

例如，您也可以擷取填寫表單所花費的時間的「提交」動作，可以新增隱藏的輸入欄位 `startTime` 和 `endTime`。

指令碼可在表單轉譯時 `startTime` 和表 `endTime` 單提交前分別提供和欄位的值。 然後，「提交」 `post.jsp` 動作指令碼可以使用請求參數存取這些欄位，並計算填寫表單所需的總時間。

### 檔案附件 {#file-attachments}

提交操作還可以使用您使用檔案附件元件上傳的檔案附件。 提交動作指令碼可使用sling [RequestParameter API存取這些檔案](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html)。 API [的isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) 方法有助於識別請求參數是檔案還是表單欄位。 您可以重複「提交」動作中的「請求」參數，以識別「檔案附件」參數。

下列范常式式碼會識別請求中的檔案附件。 接著，它會使用「取得API」將資料讀 [入檔案](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get())。 最後，它使用資料建立Document物件並附加至清單。

```java
RequestParameterMap requestParameterMap = slingRequest.getRequestParameterMap();
for (Map.Entry<String, RequestParameter[]> param : requestParameterMap.entrySet()) {
    RequestParameter rpm = param.getValue()[0];
    if(!rpm.isFormField()) {
        fileAttachments.add(new Document(rpm.get()));
    }
}
```

### 轉送路徑和重新導向URL {#forward-path-and-redirect-url}

執行所需操作後，提交Servlet將請求轉發到轉發路徑。 操作使用setForwardPath API在指南提交servlet中設定前向路徑。

如果動作未提供前向路徑，「提交servlet」會使用「重新導向URL」重新導向瀏覽器。 作者使用「最適化表單編輯」對話方塊中的「感謝頁面」設定重新導向URL。 您也可以透過「提交」動作或「指南提交servlet」中的setRedirectUrl API來設定「重新導向URL」。 您也可以使用指南提交servlet中的setRedirectParameters API，設定傳送至重新導向URL的請求參數。

>[!NOTE]
>
>作者提供「重新導向URL」（使用「感謝頁面設定」）。 [OOTB提交動作](../../forms/using/configuring-submit-actions.md) ：使用「重新導向URL」，從正向路徑參考的資源重新導向瀏覽器。
>
>您可以編寫自訂的「提交」動作，將請求轉送至資源或servlet。 Adobe建議執行正向路徑資源處理的指令碼，在處理完成時，將請求重新導向至「重新導向URL」。

## Submit action {#submit-action}

A Submit action is a sling:Folder, that includes:

* **addfields.jsp**:此指令碼提供在轉譯期間新增至HTML檔案的動作欄位。 使用此指令碼，在post.POST.jsp指令碼中新增提交期間所需的隱藏輸入參數。
* **dialog.xml**:此指令碼類似於「CQ元件」對話方塊。 它提供作者自訂的設定資訊。 當您選擇「提交」操作時，這些欄位將顯示在「最適化表單編輯」對話框的「提交操作」頁籤中。
* **post.POST.jsp**:Submit servlet會使用您提交的資料和前面幾節中的其他資料調用此指令碼。 只要提及在本頁中執行動作，即表示執行post.POST.jsp指令碼。 若要將Submit動作註冊為最適化表單，以便在「最適化表單編輯」對話方塊中顯示，請將這些屬性新增至sling:Folder:

   * **guideComponentType** of type String and **value fd/af/components/guidesubmittype**
   * **guideDataModel** ，其類型為String，指定適用於Submit動作的最適化表單類型。 **XFA架構** 的最適化表單支援xfa，而 **XSD架構的最適化表單** 則支援xsd。 **不使用** XDP或XSD的最適化表單支援basic。 若要在多種類型的最適化表單上顯示動作，請新增對應的字串。 以逗號分隔每個字串。 例如，若要讓動作在以XFA和XSD為基礎的最適化表單上顯示，請分別指 **定值xfa****和xsd** 。

   * **jcr:String類型的** description。 此屬性的值顯示在「最適化表單編輯」對話框的「提交操作」頁籤的「提交操作」清單中。 OOTB操作在CRX儲存庫中的位置/libs/fd/af/components **/guidesubmittype處存在**。

## 建立自訂的「提交」動作 {#creating-a-custom-submit-action}

請執行下列步驟，以建立自訂的「送出」動作，將資料儲存在CRX存放庫中，然後傳送電子郵件給您。 最適化表單包含將資料儲存在CRX儲存庫的OOTB Submit動作商店內容（已過時）。 此外，CQ還提供 [Mail](https://docs.adobe.com/docs/en/cq/current/javadoc/com/day/cq/mailer/package-summary.html) API，可用來傳送電子郵件。 在使用Mail API之前， [請通過系統]控制台配置(https://docs.adobe.com/docs/en/cq/current/administering/notification.html?wcmmode=disabled#Configuring Mail Service)Day CQ mail服務。 您可以重複使用「儲存內容（已過時）」操作將資料儲存在儲存庫中。 在CRX儲存庫的/libs/fd/af/components/guidesubmittype/store位置，可使用「儲存內容（已過時）」操作。

1. 登入URL https://&lt;server>:&lt;port> /crx/de/index.jsp的CRXDE Lite。 在/apps/custom_submit_action檔案夾中建立具有屬性sling:Folder和名稱store_and_mail的節點。 如果custom_submit_action資料夾不存在，請建立它。

   ![描述使用屬性sling:Folder建立節點的螢幕擷取](assets/step1.png)

1. **提供必填的設定欄位。**

   新增「商店」動作所需的設定。 將Store動作的 **cq:dialog** 節點從/libs/fd/af/components/guidesubmittype/store複製至/apps/custom_submit_action/store_and_email的動作資料夾。

   ![顯示對話框節點複製到操作資料夾的螢幕截圖](assets/step2.png)

1. **提供設定欄位以提示作者進行電子郵件設定。**

   最適化表單也提供「電子郵件」動作，可傳送電子郵件給使用者。 根據您的需求自訂此動作。 導覽至/libs/fd/af/components/guidesubmittype/email/dialog。 將cq:dialog節點內的節點複製到「提交」動作的cq:dialog節點(/apps/custom_submit_action/store_and_email/dialog)。

   ![自訂電子郵件動作](assets/step3.png)

1. **在「最適化表單編輯」對話方塊中使動作可用。**

   在store_and_email節點中新增下列屬性：

   * **guideComponentType** of **String** and value **fd/af/components/guidesubmittype**

   * **guideDataModel** , **of type** String and value **xfa, xsd, basic**

   * **jcr:Description** of type **String** and value **Store and Email Action**

1. 開啟任何最適化表單。 按一下「 **開始** 」旁的「編輯」按鈕 **，開啟最適化表****** 單容器的「編輯」對話方塊。 新動作會顯示在「提交動 **作** 」標籤中。 選擇「存 **儲」和「電子郵件操作** 」會顯示在對話框節點中添加的配置。

   ![「提交操作配置」對話框](assets/store_and_email_submit_action_dialog.jpg)

1. **使用動作完成工作。**

   將post.POST.jsp指令碼添加到操作中。 (/apps/custom_submit_action/store_and_mail/)。

   執行OOTB商店動作（post.POST.jsp指令碼）。 使用 [FormsHelper.runAction](https://docs.adobe.com/docs/en/cq/current/javadoc/com/day/cq/wcm/foundation/forms/FormsHelper.html#runAction(java.lang.String, java.lang.String, org.apache.sling.api.resource.Resource, org.apache.sling.api.SlingHttpServletRequest, org.apache.sling.api.SlingHttpServletResponse)API,CQ會在您的程式碼中提供來執行Store動作。 在JSP檔案中添加以下代碼：

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   若要傳送電子郵件，程式碼會從設定讀取收件者的電子郵件地址。 要在操作指令碼中獲取配置值，請使用以下代碼讀取當前資源的屬性。 同樣地，您也可以讀取其他配置檔案。

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   最後，使用CQ Mail API來傳送電子郵件。 使用 [](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html) SimpleEmail類建立電子郵件對象，如下所示：

   >[!NOTE]
   >
   >請確定JSP檔案的名稱為post.POST.jsp。

   ```java
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <%@page import="com.day.cq.wcm.foundation.forms.FormsHelper,
          org.apache.sling.api.resource.ResourceUtil,
          org.apache.sling.api.resource.ValueMap,
                   com.day.cq.mailer.MessageGatewayService,
     com.day.cq.mailer.MessageGateway,
     org.apache.commons.mail.Email,
                   org.apache.commons.mail.SimpleEmail" %>
   <%@taglib prefix="sling"
                   uri="https://sling.apache.org/taglibs/sling/1.0" %>
   <%@taglib prefix="cq"
                   uri="https://www.day.com/taglibs/cq/1.0"
   %>
   <cq:defineObjects/>
   <sling:defineObjects/>
   <%
           String storeContent =
                       "/libs/fd/af/components/guidesubmittype/store";
           FormsHelper.runAction(storeContent, "post", resource,
                                   slingRequest, slingResponse);
    ValueMap props = ResourceUtil.getValueMap(resource);
    Email email = new SimpleEmail();
    String[] mailTo = props.get("mailto", new String[0]);
    email.setFrom((String)props.get("from"));
           for (String toAddr : mailTo) {
               email.addTo(toAddr);
      }
    email.setMsg((String)props.get("template"));
    email.setSubject((String)props.get("subject"));
    MessageGatewayService messageGatewayService =
                       sling.getService(MessageGatewayService.class);
    MessageGateway messageGateway =
                   messageGatewayService.getGateway(SimpleEmail.class);
    messageGateway.send(email);
   %>
   ```

   在最適化表單中選取動作。 動作會傳送電子郵件並儲存資料。

