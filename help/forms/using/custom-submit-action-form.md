---
title: 為自適應表單編寫自定義提交操作
seo-title: Writing custom Submit action for adaptive forms
description: AEM Forms允許您為自適應表單建立自定義提交操作。 本文介紹為Adaptive表單添加自定義提交操作的過程。
seo-description: AEM Forms lets you create custom Submit action for Adaptive forms. This article describes the procedure to add custom Submit action for Adaptive forms.
uuid: fd8e1dac-b997-4e86-aaf6-3507edcb3070
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 2a2e1156-4a54-4b0a-981c-d527fe22a27e
docset: aem65
exl-id: 7c3d0dac-4e19-4eb3-a43d-909d526acd55
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '1616'
ht-degree: 1%

---

# 為自適應表單編寫自定義提交操作{#writing-custom-submit-action-for-adaptive-forms}

自適應表單要求提交操作以處理用戶指定的資料。 「提交」(Submit)操作確定使用自適應表單對提交的資料執行的任務。 Adobe Experience Manager(AEM包括 [OOTB提交操作](../../forms/using/configuring-submit-actions.md) 演示了可以使用用戶提交的資料執行的自定義任務。 例如，您可以執行任務，如發送電子郵件或儲存資料。

## 提交操作的工作流 {#workflow-for-a-submit-action}

流程圖描述了在按一下「提交」(Submit)操作時觸發的「提交」(Submit)操作的工作流 **[!UICONTROL 提交]** 按鈕。 「檔案附件」元件中的檔案將上載到伺服器，並使用上載檔案的URL更新表單資料。 在客戶端中，資料以JSON格式儲存。 客戶端向內部Servlet發送Ajax請求，該Servlet按照您指定的資料進行消息處理，並以XML格式返回資料。 客戶端將此資料與操作欄位進行整理。 它通過表單提交操作將資料提交到最終的Servlet（指南提交Servlet）。 然後，Servlet將控制項轉發到「提交」操作。 「提交」(Submit)操作可以將請求轉發到其他吊索資源或將瀏覽器重定向到另一個URL。

![描述提交操作的工作流的流程圖](assets/diagram1.png)

### XML資料格式 {#xml-data-format}

XML資料使用 **`jcr:data`** 請求參數。 提交操作可以訪問參數來處理資料。 以下代碼描述XML資料的格式。 綁定到「表單」模型的欄位將出現在 **`afBoundData`** 的子菜單。 未綁定的欄位出現在 `afUnoundData`的子菜單。 有關格式的詳細資訊 `data.xml` 檔案，請參閱 [預填充自適應表單域簡介](../../forms/using/prepopulate-adaptive-form-fields.md)。

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

### 操作欄位 {#action-fields}

「提交」操作可以添加隱藏的輸入欄位(使用HTML [輸入](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input) 標籤)到呈現的窗體HTML。 這些隱藏欄位可以包含處理表單提交時需要的值。 在提交表單時，這些欄位值會作為請求參數被傳回，「提交」操作可以在提交處理過程中使用這些參數。 輸入欄位稱為操作欄位。

例如，「提交」操作還捕獲填寫表單所花的時間，可添加隱藏的輸入欄位 `startTime` 和 `endTime`。

指令碼可以提供 `startTime` 和 `endTime` 欄位。 提交ActionScript `post.jsp` 然後，可以使用請求參數訪問這些欄位並計算填寫表單所需的總時間。

### 檔案附件 {#file-attachments}

提交操作還可以使用使用「檔案附件」元件上載的檔案附件。 提交操作指令碼可以使用sling訪問這些檔案 [RequestParameter API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html)。 的 [是窗體欄位](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) API的方法有助於確定請求參數是檔案還是表單域。 您可以在「提交」操作中迭代「請求」參數，以標識「檔案附件」參數。

以下示例代碼標識請求中的檔案附件。 接下來，它使用 [獲取API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get())。 最後，它使用資料建立一個Document對象並將其附加到清單。

```java
RequestParameterMap requestParameterMap = slingRequest.getRequestParameterMap();
for (Map.Entry<String, RequestParameter[]> param : requestParameterMap.entrySet()) {
    RequestParameter rpm = param.getValue()[0];
    if(!rpm.isFormField()) {
        fileAttachments.add(new Document(rpm.get()));
    }
}
```

### 轉發路徑和重定向URL {#forward-path-and-redirect-url}

執行所需操作後，提交servlet將請求轉發到轉發路徑。 操作使用setForwardPath API在指南提交servlet中設定前向路徑。

如果操作未提供轉發路徑，則提交servlet使用重定向URL重定向瀏覽器。 作者使用「自適應表單編輯」對話框中的「感謝」頁配置配置重定向URL。 您還可以通過「提交」操作或「指南提交servlet」中的setRedirectUrl API配置重定向URL。 您還可以使用指南提交servlet中的setRedirectParameters API配置發送到重定向URL的請求參數。

>[!NOTE]
>
>作者提供重定向URL（使用「感謝」頁面配置）。 [OOTB提交操作](../../forms/using/configuring-submit-actions.md) 使用重定向URL將瀏覽器從轉發路徑引用的資源中重定向。
>
>您可以編寫一個自定義提交操作，將請求轉發到資源或servlet。 Adobe建議執行正向路徑資源處理的指令碼在處理完成後將請求重定向到重定向URL。

## 提交動作 {#submit-action}

「提交」(Submit)操作是sling:Folder，其中包括以下內容：

* **addfields.jsp**:此指令碼提供在格式副本期間添加到HTML檔案的操作欄位。 使用此指令碼可在post.POST.jsp指令碼中添加提交期間所需的隱藏輸入參數。
* **對話框.xml**:此指令碼與「CQ元件」對話框類似。 它提供了作者自定義的配置資訊。 選擇「提交」操作後，這些欄位將顯示在「自適應表單編輯」對話框的「提交操作」頁籤中。
* **post.POST.jsp**:Submit Servlet使用您提交的資料和前面各節中的附加資料調用此指令碼。 在此頁中任何提到運行操作都意味著運行post.POST.jsp指令碼。 要將「提交」操作註冊到「自適應表單編輯」對話框中顯示的自適應表單，請將這些屬性添加到sling:Folder:

   * **guideComponentType** 字串和值類型 **fd/af/元件/指導提交類型**
   * **guideDataModel** 類型字串，指定適用提交操作的自適應表單的類型。 **xfa** 支援基於XFA的自適應表單，而 **xx** 支援基於XSD的自適應表單。 **基本** 不支援不使用XDP或XSD的自適應表單。 要在多種類型的自適應表單上顯示操作，請添加相應的字串。 用逗號分隔每個字串。 例如，要使基於XFA和XSD的自適應表單上的操作可見，請指定值 **xfa** 和 **xx** 分別進行。

   * **jcr：說明** 類型。 此屬性的值顯示在「自適應表單編輯」對話框的「提交操作」頁籤的「提交操作」清單中。 OOTB操作存在於位置的CRX儲存庫中 **/libs/fd/af/components/guidesubmittype**。

## 建立自定義提交操作 {#creating-a-custom-submit-action}

執行以下步驟建立自定義提交操作，該操作將資料保存在CRX儲存庫中，然後向您發送電子郵件。 自適應表單包含OOTB提交操作儲存內容（已棄用），該內容將資料保存在CRX儲存庫中。 此外， CQ還提供 [郵件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hant) 可用於發送電子郵件的API。 在使用Mail API之前， [配置](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hant&amp;wcmmode=已禁用) CQ Mail服務通過系統控制台。 您可以重用「儲存內容」（已棄用）操作將資料儲存在儲存庫中。 「儲存內容（已棄用）」操作可在CRX儲存庫中的/libs/fd/af/components/guidesubmittype/store位置使用。

1. 登錄到CRXDE Lite，網址為https://&lt;server>:&lt;port>/crx/de/index.jsp。 在/apps/custom_submit_action資料夾中，使用sling:Folder和name store_and_mail屬性建立節點。 如果custom_submit_action資料夾不存在，請建立它。

   ![描述使用屬性sling:Folder建立節點的螢幕快照](assets/step1.png)

1. **提供必需的配置欄位。**

   添加儲存操作所需的配置。 複製 **cq：對話框** 「儲存」操作的節點（從/libs/fd/af/components/guidesubmittype/store到/apps/custom_submit_action/store_and_email上的操作資料夾）。

   ![螢幕快照顯示對話框節點複製到操作資料夾](assets/step2.png)

1. **提供配置欄位以提示作者進行電子郵件配置。**

   自適應表單還提供向用戶發送電子郵件的電子郵件操作。 根據您的要求自定義此操作。 導航至/libs/fd/af/components/guidesubmittype/email/dialog。 將cq:dialog節點中的節點複製到「提交」操作(/apps/custom_submit_action/store_and_email/dialog)的cq:dialog節點。

   ![自定義電子郵件操作](assets/step3.png)

1. **使操作在「自適應表單編輯」對話框中可用。**

   在store_and_email節點中添加以下屬性：

   * **guideComponentType** 類型 **字串** 價值 **fd/af/元件/指導提交類型**

   * **guideDataModel** 類型 **字串** 價值 **xfa、xsd、基本**

   * **jcr：說明** 類型 **字串** 價值 **儲存和電子郵件操作**

1. 開啟任何自適應窗體。 按一下 **編輯** 按鈕 **開始** 開啟 **編輯** 對話框。 新操作將顯示在 **提交操作** 頁籤。 選擇 **儲存和電子郵件操作** 顯示在對話框節點中添加的配置。

   ![提交操作配置對話框](assets/store_and_email_submit_action_dialog.jpg)

1. **使用操作完成任務。**

   將post.POST.jsp指令碼添加到操作。 (/apps/custom_submit_action/store_and_mail/)。

   運行OOTB儲存操作(post.POST.jsp指令碼)。 使用 [FormsHelper.runAction](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=zh-Hant)(java.lang.string, java.lang.String, org.apache.sling.api.resource., org.apache.sling.api.SlingHttpServletRequest, org.apache.sling.api.SlingHttpServletResponse)API,CQ在代碼中提供以運行Store操作。 在JSP檔案中添加以下代碼：

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   要發送電子郵件，代碼會從配置中讀取收件人的電子郵件地址。 要在操作的指令碼中提取配置值，請使用以下代碼讀取當前資源的屬性。 同樣，您也可以讀取其他配置檔案。

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   最後，使用CQ Mail API發送電子郵件。 使用 [簡單電子郵件](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html) 類以建立電子郵件對象，如下所示：

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

   在自適應窗體中選擇操作。 該操作會發送電子郵件並儲存資料。
