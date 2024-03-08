---
title: 撰寫最適化表單的自訂提交動作
description: AEM Forms可讓您為最適化表單建立自訂提交動作。 本文主要說明為最適化表單新增自訂提交動作的程式。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 7c3d0dac-4e19-4eb3-a43d-909d526acd55
source-git-commit: db0e9d6105484b37e2e21e49bf0f95cef9da2a62
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 1%

---

# 撰寫最適化表單的自訂提交動作{#writing-custom-submit-action-for-adaptive-forms}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/custom-submit-action-form.html) |
| AEM 6.5 | 本文章 |

調適型表單需要提交動作來處理使用者指定的資料。 提交動作會決定使用最適化表單提交之資料所執行的工作。 Adobe Experience Manager (AEM)包含 [現成可用的提交動作](../../forms/using/configuring-submit-actions.md) 會示範您可使用使用者提交的資料執行的自訂工作。 例如，您可以執行工作，例如傳送電子郵件或儲存資料。

## 提交動作的工作流程 {#workflow-for-a-submit-action}

此流程圖會說明提交動作的工作流程，此動作會在您按一下 **[!UICONTROL 提交]** 最適化表單中的按鈕。 檔案附件元件中的檔案會上傳至伺服器，而表單資料會以上傳檔案的URL更新。 在使用者端內，資料會以JSON格式儲存。 使用者端傳送Ajax要求至內部servlet，它會處理您指定的資料並以XML格式傳回。 使用者端會使用動作欄位整理此資料。 它會透過「表單提交」動作將資料提交至最終servlet （引導提交servlet）。 然後，Servlet將控制項轉送給Submit動作。 提交動作可以將請求轉送至不同的Sling資源，或將瀏覽器重新導向至其他URL。

![說明「提交」動作之工作流程的流程圖](assets/diagram1.png)

### XML資料格式 {#xml-data-format}

XML資料會使用傳送至servlet。 **`jcr:data`** 要求引數。 提交動作可以存取引數以處理資料。 下列程式碼說明XML資料的格式。 與表單模型繫結的欄位會出現在 **`afBoundData`** 區段。 未繫結的欄位會出現在 `afUnoundData`區段。 如需格式化的詳細資訊， `data.xml` 檔案，請參閱 [預先填入最適化表單欄位簡介](../../forms/using/prepopulate-adaptive-form-fields.md).

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

提交動作可以新增隱藏的輸入欄位(使用HTML [輸入](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input) 標籤)至已呈現的表單HTML。 這些隱藏欄位可包含處理表單提交時所需的值。 提交表單時，這些欄位值會傳回為請求引數，提交動作可在提交處理期間使用這些引數。 輸入欄位稱為動作欄位。

例如，同時擷取填寫表單所需時間的提交動作可以新增隱藏的輸入欄位 `startTime` 和 `endTime`.

指令碼可提供 `startTime` 和 `endTime` 分別於表單轉譯時及表單提交前之欄位。 提交ActionScript `post.jsp` 接著，可使用請求引數存取這些欄位，並計算填寫表單所需的總時間。

### 檔案附件 {#file-attachments}

提交動作也可以使用您使用「檔案附件」元件上傳的檔案附件。 提交動作指令碼可使用Sling存取這些檔案 [RequestParameter API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html). 此 [isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) api的方法有助於識別請求引數是檔案或表單欄位。 您可以在「提交」動作中反複執行「要求」引數，以識別「檔案附件」引數。

下列範常式式碼會識別請求中的檔案附件。 接下來，它會使用 [取得API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get()). 最後，它會使用資料建立Document物件，並將其附加至清單。

```java
RequestParameterMap requestParameterMap = slingRequest.getRequestParameterMap();
for (Map.Entry<String, RequestParameter[]> param : requestParameterMap.entrySet()) {
    RequestParameter rpm = param.getValue()[0];
    if(!rpm.isFormField()) {
        fileAttachments.add(new Document(rpm.get()));
    }
}
```

### 轉寄路徑和重新導向URL {#forward-path-and-redirect-url}

執行必要的動作後，提交servlet會將請求轉送至轉送路徑。 動作會使用setForwardPath API在指南提交servlet中設定轉寄路徑。

如果動作未提供轉寄路徑，則提交servlet會使用重新導向URL重新導向瀏覽器。 作者會使用「最適化表單編輯」對話方塊中的「感謝頁面」設定，來設定重新導向URL。 您也可以透過提交動作或指南提交servlet中的setRedirectUrl API來設定重新導向URL。 您也可以使用指南提交servlet中的setRedirectParameters API，設定傳送至重新導向URL的要求引數。

>[!NOTE]
>
>作者會提供重新導向URL （使用感謝頁面設定）。 [現成可用的提交動作](../../forms/using/configuring-submit-actions.md) 使用重新導向URL，從轉送路徑參照的資源重新導向瀏覽器。
>
>您可以編寫自訂Submit動作，將請求轉發到資源或servlet。 Adobe建議在處理完成時，為轉送路徑執行資源處理的指令碼會將要求重新導向至重新導向URL。

## 提交動作 {#submit-action}

提交動作是sling：Folder，包含下列專案：

* **addfields.jsp**：此指令碼提供在轉譯期間新增至HTML檔案中的動作欄位。 使用此指令碼，在post.post.jsp.jsp指令碼中新增提交期間所需的隱藏POST引數。
* **dialog.xml**：此指令碼類似於CQ元件對話方塊。 它提供作者自訂的設定資訊。 當您選取提交動作時，欄位會顯示在「最適化表單編輯」對話方塊的「提交動作」索引標籤中。
* **post.POST.jsp**：提交servlet會呼叫此指令碼，其中包含您提交的資料以及前幾節中的其他資料。 在此頁面中只要提到要執行動作，就表示要執行post.post.jspPOST檔。 若要以最適化表單註冊提交動作以顯示於最適化表單編輯對話方塊中，請將這些屬性新增至 `sling:Folder`：

   * **guideComponentType** 字串和值的型別 **fd/af/components/guidesubmittype**
   * **guideDataModel** 字串型別，指定適用於提交動作的最適化表單型別。 **xfa** 支援XFA型最適化表單，但 **xsd** 支援XSD型最適化表單。 **基本** 不使用XDP或XSD的最適化表單支援。 若要顯示多種最適化表單型別的動作，請新增對應的字串。 以逗號分隔每個字串。 例如，若要讓動作顯示在XFA和XSD型最適化表單上，請指定值 **xfa** 和 **xsd** （分別）。

   * **jcr：description** 型別字串的。 此屬性的值會顯示在「最適化表單編輯」對話方塊之「提交動作」索引標籤的「提交」動作清單中。 現成的動作會顯示在位置的CRX存放庫中 **/libs/fd/af/components/guidesubmittype**.

## 建立自訂提交動作 {#creating-a-custom-submit-action}

執行以下步驟來建立自訂提交動作，將資料儲存在CRX存放庫中，然後傳送電子郵件給您。 最適化表單包含現成的提交動作儲存內容（已棄用），可將資料儲存在CRX存放庫。 此外，CQ提供 [郵件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hant) 可用於傳送電子郵件的API。 使用Mail API之前， [設定](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=en&amp;wcmmode=disabled) 經由系統主控台的Day CQ Mail服務。 您可以重複使用「儲存內容（已棄用）」動作，將資料儲存在存放庫中。 存放區內容（已棄用）動作可在CRX存放庫中的/libs/fd/af/components/guidessubmittype/store位置取得。

1. 在URL https://登入CRXDE Lite&lt;server>：&lt;port>/crx/de/index.jsp. 在/apps/custom_submit_action資料夾中建立具有sling：Folder屬性並命名為store_and_mail的節點。 建立custom_submit_action資料夾（如果尚未存在）。

   ![熒幕擷圖說明如何使用屬性sling：Folder建立節點](assets/step1.png)

1. **提供必要設定欄位。**

   新增存放區動作所需的設定。 複製 **cq：dialog** /libs/fd/af/components/guidessubmittype/store中的存放區動作節點，移至位於/apps/custom_submit_action/store_and_email的動作資料夾。

   ![熒幕擷圖顯示對話方塊節點複製到動作資料夾的過程](assets/step2.png)

1. **提供設定欄位以提示作者設定電子郵件。**

   最適化表單也提供電子郵件動作，可向使用者傳送電子郵件。 根據您的需求自訂此動作。 導覽至/libs/fd/af/components/guidessubmittype/email/dialog。 將cq：dialog節點內的節點複製到提交動作(/apps/custom_submit_action/store_and_email/dialog)的cq：dialog節點。

   ![自訂電子郵件動作](assets/step3.png)

1. **在「最適化表單編輯」對話方塊中讓動作可用。**

   在store_and_email節點中新增下列屬性：

   * **guideComponentType** 型別 **字串** 和值 **fd/af/components/guidesubmittype**

   * **guideDataModel** 型別 **字串** 和值 **xfa， xsd，基本**

   * **jcr：description** 型別 **字串** 和值 **存放區和電子郵件動作**

1. 開啟任何最適化表單。 按一下 **編輯** 按鈕旁邊 **開始** 以開啟 **編輯** 最適化表單容器的對話方塊。 新動作會顯示在 **提交動作** 標籤。 選取 **存放區和電子郵件動作** 顯示對話方塊節點中新增的組態。

   ![提交動作設定對話方塊](assets/store_and_email_submit_action_dialog.jpg)

1. **使用動作完成任務。**

   將post.jsp.jspPOST碼新增至您的動作。 (/apps/custom_submit_action/store_and_mail/)。

   執行現成可用的商店動作(post.space.jspPOST檔)。 使用 [FormsHelper.runAction](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hant)(java.lang.String， java.lang.String， org.apache.sling.api.resource.Resource， org.apache.sling.api.SlingHttpServletRequest， org.apache.sling.api.SlingHttpServletResponse) CQ在您的程式碼中提供，以執行「儲存」動作的API。 在JSP檔案中新增下列程式碼：

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   若要傳送電子郵件，程式碼會從設定中讀取收件者的電子郵件地址。 若要在動作的指令碼中擷取設定值，請使用下列程式碼讀取目前資源的屬性。 同樣地，您可以讀取其他組態檔。

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   最後，使用CQ Mail API傳送電子郵件。 使用 [簡單電子郵件](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html) 類別以建立電子郵件物件，如下所示：

   >[!NOTE]
   >
   >確定JSP檔案的名稱為post.postPOST.jsp。

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

   選取最適化表單中的動作。 動作會傳送電子郵件並儲存資料。
