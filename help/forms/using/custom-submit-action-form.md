---
title: 撰寫最適化表單的自訂提交動作
seo-title: Writing custom Submit action for adaptive forms
description: AEM Forms可讓您建立最適化表單的自訂「提交」動作。 本文說明為適用性表單新增自訂提交動作的程式。
seo-description: AEM Forms lets you create custom Submit action for Adaptive forms. This article describes the procedure to add custom Submit action for Adaptive forms.
uuid: fd8e1dac-b997-4e86-aaf6-3507edcb3070
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 2a2e1156-4a54-4b0a-981c-d527fe22a27e
docset: aem65
exl-id: 7c3d0dac-4e19-4eb3-a43d-909d526acd55
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1629'
ht-degree: 0%

---

# 撰寫最適化表單的自訂提交動作{#writing-custom-submit-action-for-adaptive-forms}

適用性表單需要提交動作，以處理使用者指定的資料。 「提交」動作會決定您使用最適化表單提交之資料所執行的任務。 Adobe Experience Manager(AEM)包含 [OOTB提交操作](../../forms/using/configuring-submit-actions.md) 展示可使用使用者提交的資料執行的自訂工作。 例如，您可以執行工作，例如傳送電子郵件或儲存資料。

## 「提交」動作的工作流程 {#workflow-for-a-submit-action}

流程圖描述了按一下 **[!UICONTROL 提交]** 按鈕。 檔案附件元件中的檔案會上傳到伺服器，而表單資料會以上傳檔案的URL更新。 在用戶端內，資料會以JSON格式儲存。 用戶端會傳送Ajax要求至內部servlet，以按摩您指定的資料，並以XML格式傳回。 用戶端會使用動作欄位來整理此資料。 它通過「表單提交」操作將資料提交到最終的Servlet（指南提交Servlet）。 然後，Servlet將控制項轉發到Submit操作。 Submit動作可將要求轉送至其他Sling資源，或將瀏覽器重新導向至其他URL。

![描述「提交」操作工作流的流程圖](assets/diagram1.png)

### XML資料格式 {#xml-data-format}

XML資料會使用 **`jcr:data`** 要求參數。 提交動作可存取參數以處理資料。 以下代碼描述XML資料的格式。 綁定到表單模型的欄位將顯示在 **`afBoundData`** 區段。 未綁定的欄位顯示在 `afUnoundData`區段。 如需 `data.xml` 檔案，請參閱 [預先填入最適化表單欄位的簡介](../../forms/using/prepopulate-adaptive-form-fields.md).

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

「提交」動作可新增隱藏的輸入欄位(使用HTML [輸入](https://developer.mozilla.org/en/docs/Web/HTML/Element/Input) 標籤)轉換為轉譯的表單HTML。 這些隱藏欄位可包含處理表單提交時所需的值。 提交表單時，這些欄位值會以請求參數的形式發回，「提交」動作可在提交處理期間使用。 輸入欄位稱為動作欄位。

例如，如果「提交」動作也擷取填寫表單所花的時間，則可新增隱藏的輸入欄位 `startTime` 和 `endTime`.

指令碼可提供 `startTime` 和 `endTime` 表單轉譯時和表單提交前的欄位。 提交操作指令碼 `post.jsp` 之後，您就可以使用請求參數存取這些欄位，並計算填寫表單所需的總時間。

### 檔案附件 {#file-attachments}

提交操作也可以使用使用檔案附件元件上傳的檔案附件。 提交動作指令碼可使用Sling存取這些檔案 [RequestParameter API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html). 此 [isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) API的方法有助於識別要求參數是檔案還是表單欄位。 您可以反覆查看提交動作中的請求參數，以識別檔案附件參數。

下列范常式式碼可識別請求中的檔案附件。 接下來，會使用 [取得API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get()). 最後，它使用資料建立文檔對象並將其附加到清單中。

```java
RequestParameterMap requestParameterMap = slingRequest.getRequestParameterMap();
for (Map.Entry<String, RequestParameter[]> param : requestParameterMap.entrySet()) {
    RequestParameter rpm = param.getValue()[0];
    if(!rpm.isFormField()) {
        fileAttachments.add(new Document(rpm.get()));
    }
}
```

### 前進路徑和重新導向URL {#forward-path-and-redirect-url}

執行所需操作後，提交servlet將請求轉發到轉發路徑。 動作會使用setForwardPath API來設定指南提交Servlet中的前進路徑。

如果動作未提供轉送路徑，則提交servlet會使用重新導向URL來重新導向瀏覽器。 作者會使用「適用性表單編輯」對話方塊中的「感謝頁面」設定來設定重新導向URL。 您也可以透過提交動作或指南提交servlet中的setRedirectUrl API來設定重新導向URL。 您也可以使用指南提交servlet中的setRedirectParameters API來設定傳送至重新導向URL的要求參數。

>[!NOTE]
>
>作者提供重新導向URL（使用感謝頁面設定）。 [OOTB提交操作](../../forms/using/configuring-submit-actions.md) 使用「重新導向URL」，從正向路徑參考的資源重新導向瀏覽器。
>
>您可以撰寫自訂的「提交」動作，將請求轉送至資源或servlet。 Adobe建議執行正向路徑資源處理的指令碼在處理完成時，將要求重新導向至重新導向URL。

## 提交動作 {#submit-action}

提交動作是sling:Folder，包含下列項目：

* **addfields.jsp**:此指令碼提供在轉譯期間新增至HTML檔案的動作欄位。 使用此指令碼，在post.POST.jsp指令碼中添加提交期間所需的隱藏輸入參數。
* **dialog.xml**:此指令碼類似於CQ元件對話方塊。 提供作者自訂的設定資訊。 當您選取「提交」動作時，欄位會顯示在「適用性表單編輯」對話方塊的「提交動作」標籤中。
* **post.POST.jsp**:Submit servlet會使用您提交的資料以及前幾節中的其他資料來呼叫此指令碼。 在此頁面中提及執行動作即表示執行post.POST.jsp指令碼。 若要使用最適化表單註冊「提交」動作，以在「適用性表單編輯」對話方塊中顯示，請將這些屬性新增至sling:Folder:

   * **guideComponentType** 類型字串和值 **fd/af/components/guidesubmittype**
   * **guideDataModel** 類型字串，指定適用「提交」動作的適用性表單類型。 **xfa** 支援XFA型適用性表單，而 **xd** 支援XSD型適用性表單。 **基本** 不使用XDP或XSD的適用性表單支援。 若要在多種適用性表單類型上顯示動作，請新增對應的字串。 以逗號分隔每個字串。 例如，若要讓動作在XFA和XSD型適用性表單上可見，請指定值 **xfa** 和 **xd** 分別為5個。

   * **jcr:description** 類型。 此屬性的值顯示在「適用性表單編輯」對話框的「提交操作」頁簽的「提交操作」清單中。 OOTB動作會顯示在CRX存放庫的位置 **/libs/fd/af/components/guidesubmittype**.

## 建立自訂提交動作 {#creating-a-custom-submit-action}

執行下列步驟以建立自訂的「提交」動作，將資料儲存在CRX存放庫，然後傳送電子郵件給您。 適用性表單包含將資料儲存在CRX存放庫的OOTB提交動作存放區內容（已淘汰）。 此外，CQ也提供 [郵件](https://docs.adobe.com/docs/en/cq/current/javadoc/com/day/cq/mailer/package-summary.html) 可用於傳送電子郵件的API。 使用郵件API之前， [設定](https://docs.adobe.com/docs/en/cq/current/administering/notification.html?wcmmode=disabled#Configuring郵件服務)透過系統主控台提供Day CQ Mail服務。 您可以重複使用「儲存內容（已廢止）」動作，將資料儲存在存放庫中。 「儲存內容（已廢止）」動作可在CRX存放庫的/libs/fd/af/components/guidesubmittype/store位置取得。

1. 在URL https://登入CRXDE Lite&lt;server>:&lt;port>/crx/de/index.jsp。 在/apps/custom_submit_action資料夾中，使用屬性sling:Folder和name store_and_mail建立節點。 建立custom_submit_action資料夾（如果尚未存在）。

   ![螢幕擷圖，說明使用屬性sling:Folder建立節點的方式](assets/step1.png)

1. **提供必填的設定欄位。**

   添加儲存操作所需的配置。 複製 **cq:dialog** 儲存操作節點，從/libs/fd/af/components/guidesubmittype/store指向/apps/custom_submit_action/store_and_email的操作資料夾。

   ![螢幕截圖顯示對話框節點複製到操作資料夾](assets/step2.png)

1. **提供設定欄位以提示作者進行電子郵件設定。**

   適用性表單也提供「電子郵件」動作，可傳送電子郵件給使用者。 根據您的需求自訂此動作。 導覽至/libs/fd/af/components/guidesubmittype/email/dialog。 將cq:dialog節點內的節點複製到提交動作的cq:dialog節點(/apps/custom_submit_action/store_and_email/dialog)。

   ![自訂電子郵件動作](assets/step3.png)

1. **讓動作可在「最適化表單編輯」對話方塊中使用。**

   在store_and_email節點中新增下列屬性：

   * **guideComponentType** 類型 **字串** 和值 **fd/af/components/guidesubmittype**

   * **guideDataModel** 類型 **字串** 和值 **xfa, xsd, basic**

   * **jcr:description** 類型 **字串** 和值 **儲存和電子郵件動作**

1. 開啟任何最適化表單。 按一下 **編輯** 按鈕 **開始** 開啟 **編輯** 最適化表單容器的對話方塊。 新動作會顯示在 **提交操作** 標籤。 選取 **儲存和電子郵件動作** 顯示在對話框節點中添加的配置。

   ![提交操作配置對話框](assets/store_and_email_submit_action_dialog.jpg)

1. **使用操作完成任務。**

   將post.POST.jsp指令碼新增至動作。 (/apps/custom_submit_action/store_and_mail/)。

   執行OOTB儲存動作(post.POST.jsp指令碼)。 使用 [FormsHelper.runAction](https://docs.adobe.com/docs/en/cq/current/javadoc/com/day/cq/wcm/foundation/forms/FormsHelper.html#runAction(java.lang.String, java.lang.String, org.apache.sling.api.resource.Resource, org.apache.sling.api.SlingHttpServletRequest, org.apache.sling.api.SlingHttpServletResponse))CQ在您的程式碼中提供的API，用以執行「儲存」動作。 在JSP檔案中添加以下代碼：

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   若要傳送電子郵件，程式碼會從設定讀取收件者的電子郵件地址。 若要擷取動作指令碼中的設定值，請使用下列程式碼讀取目前資源的屬性。 同樣地，您也可以讀取其他組態檔。

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   最後，使用CQ Mail API來傳送電子郵件。 使用 [SimpleEmail](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html) 類以建立電子郵件對象，如下所示：

   >[!NOTE]
   >
   >確保JSP檔案的名稱為post.POST.jsp。

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
