---
title: 配置提交操作
seo-title: Configuring the Submit action
description: Forms允許您配置提交操作，以定義提交後如何處理自適應表單。 您可以使用內置提交操作或從頭開始編寫自己的內容。
uuid: 4368d648-88ea-4f84-a051-46296a1a084e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9d8d7044-ffce-4ab4-9543-a2d2f9da31e3
docset: aem65
feature: Adaptive Forms
exl-id: 04efb4ad-cff6-4e05-bcd2-98102f052452
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '1870'
ht-degree: 0%

---

# 配置提交操作{#configuring-the-submit-action}

## 提交操作簡介 {#introduction-to-submit-actions}

當用戶按一下自適應表單上的「提交」按鈕時，將觸發提交操作。 您可以在自適應表單上配置提交操作。 自適應表單提供了一些現成的提交操作。 您可以複製和擴展預設提交操作以建立您自己的提交操作。 但是，根據您的要求，您可以編寫並註冊您自己的提交操作，以處理已提交表單中的資料。 提交操作可以使用 [同步或非同步提交](../../forms/using/asynchronous-submissions-adaptive-forms.md)。

您可以在 **提交** 工具欄中。

![配置提交操作](assets/thank-you-setting.png)

配置提交操作

自適應表單中可用的預設提交操作包括：

* 提交到REST終結點
* 傳送電子郵件
* 通過電子郵件發送PDF
* 調用Forms Workflow
* 使用表單資料模型提交
* Forms門戶提交操作
* 調用工AEM作流

>[!NOTE]
>
>通過電子郵件提交操作發送PDF僅適用於使用XFA模板作為表單模型的自適應表單。

>[!NOTE]
>
>確保 [安裝AEM目錄]\crx-quickstart\temp\datamanager\ASM folder
>存在. 臨時儲存附件需要該目錄。 如果目錄不存在，請建立它。

>[!CAUTION]
>
>如果 [預填充](../../forms/using/prepopulate-adaptive-form-fields.md) 表單模板、表單資料模型或基於架構的自適應表單，其中XML或JSON資料向不包含資料的架構（XML架構、JSON架構、表單模板或表單資料模型）投訴 &lt;afdata>。 &lt;afbounddata>, &lt;/afunbounddata> 標籤，則無界域的資料(無界域是沒有 [賓德雷](../../forms/using/prepopulate-adaptive-form-fields.md) 屬性)。

您可以為自適應表單編寫自定義提交操作以完成使用案例。 有關詳細資訊，請參見 [為自適應表單編寫自定義提交操作](../../forms/using/custom-submit-action-form.md)。

## 提交到REST終結點 {#submit-to-rest-endpoint}

的 **提交到REST終結點** 提交選項將表單中填寫的資料作為HTTPGET請求的一部分傳遞到配置的確認頁。 您可以添加要請求的欄位的名稱。 請求的格式為：

`{fieldName}={request parameter name}`

如下圖所示， `param1` 和 `param2` 作為參數傳遞，其值從 **文本框** 和 **數字框** 的子菜單。

您也可以 **啟用POST請求** 並提供一個URL來發佈請求。 要向承載表單的Experience Manager伺服器提交資料，請使用與Experience Manager伺服器的根路徑對應的相對路徑。 例如，/content/forms/af/SampleForm.html。 要將資料提交到任何其他伺服器，請使用絕對路徑。

![配置REST終結點提交操作](assets/action-config.png)

配置REST終結點提交操作

>[!NOTE]
要將欄位作為REST URL中的參數傳遞，所有欄位必須具有不同的元素名稱，即使這些欄位放置在不同的面板上也是如此。

### 將提交的資料過帳到資源或外部休息終點  {#post-submitted-data-to-a-resource-or-external-rest-end-point-nbsp}

使用 **提交到REST終結點** 將提交的資料發佈到剩餘URL的操作。 該URL可以是內部（其上呈現表單的伺服器）或外部伺服器。

要將資料發佈到內部伺服器，請提供資源路徑。 資料將發佈到資源的路徑。 例如，/content/restEndPoint。 對於這種帖子請求，使用提交請求的驗證資訊。

要將資料發佈到外部伺服器，請提供URL。 URL的格式為https://host:port/path_to_rest_end_point。 確保配置路徑以匿名處理POST請求。

![作為「感謝」頁參數傳遞的欄位值的映射](assets/post-enabled-actionconfig.png)

在上例中，用戶在 `textbox` 使用參數捕獲 `param1`。 用於發佈使用 `param1` 為：

`String data=request.getParameter("param1");`

同樣，用於過帳XML資料和附件的參數是 `dataXml` 和 `attachments`。

例如，在指令碼中使用這兩個參數將資料解析到余下端點。 可以使用以下語法來儲存和分析資料：

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

在本例中， `data` 儲存XML資料， `att` 儲存附件資料。

## 傳送電子郵件 {#send-email}

的 **發送電子郵件** 提交操作會在成功提交表單時向一個或多個收件人發送電子郵件。 生成的電子郵件可以包含預定義格式的表單資料。

>[!NOTE]
所有表單域必須具有不同的元素名稱，即使它們放置在不同的面板上)，以便在電子郵件中包括表單資料。

## 通過電子郵件發送PDF {#send-pdf-via-email}

的 **通過電子郵件發送PDF** 提交操作在成功提交表單時，向一個或多個收件人發送一封包含表單資料的PDF的電子郵件。

>[!NOTE]
此提交操作可用於具有「記錄文檔」模板的基於XFA的自適應表單和基於XSD的自適應表單。

## 調用Forms Workflow {#invoke-a-forms-workflow}

的 **提交至Forms Workflow** 提交選項將資料xml和檔案附件（如果有）發送到現有AdobeLiveCycle或AEM Forms的JEE進程。

有關如何配置「提交至Forms Workflow」提交操作的資訊，請參閱 [使用表單工作流提交和處理表單資料](../../forms/using/submit-form-data-livecycle-process.md)。

## 使用表單資料模型提交 {#submit-using-form-data-model}

的 **使用表單資料模型提交** 提交操作將表單資料模型中指定資料模型對象的已提交自適應表單資料寫入其資料源。 配置提交操作時，您可以選擇要將其提交的資料寫回其資料源的資料模型對象。

此外，您可以使用表單資料模型和記錄文檔(DoR)向資料源提交表單附件。

有關表單資料模型的資訊，請參見 [AEM Forms資料整合](../../forms/using/data-integration.md)。

## Forms門戶提交操作 {#forms-portal-submit-action}

的 **Forms門戶提交操作** 選項通過AEM Forms門戶提供表單資料。

有關Forms門戶和提交操作的詳細資訊，請參閱 [草稿和提交部分](../../forms/using/draft-submission-component.md)。

## 調用工AEM作流 {#invoke-an-aem-workflow}

的 **[!UICONTROL 調用工AEM作流]** 提交操作將自適應表單與 [工AEM作流](/help/sites-developing/workflows-models.md)。 提交表單後，關聯的工作流將自動在「作者」實例上啟動。 您可以將資料檔案、附件和「記錄文檔」保存到資料夾的相對資料夾或工作流負載或變數下。 如果將工作流標籤為外部資料儲存，則變數選項可用，而非負載選項。 可以從工作流模型可用的變數清單中選擇。 如果工作流在以後階段而不是在建立工作流時被標籤為外部資料儲存，則請確保所需的變數配置已就位。

使用 **調用工AEM作流** 提交操作， [配置Experience ManagerDS設定](../../forms/using/configuring-the-processing-server-url-.md)。 有關建立工作流的AEM資訊，請參閱 [OSGi上以表單為中心的工作流](../../forms/using/aem-forms-workflow.md)。

「提交操作」(Submit Action)將下列內容置於工作流的負載位置。 但是，請注意，如果工作流模型被標籤為用於外部資料儲存，而不是負載選項，則只顯示「變數」選項。

* **資料檔案**:它包含提交到自適應表單的資料。 您可以使用 **[!UICONTROL 資料檔案路徑]** 選項，指定檔案的名稱和檔案相對於負載的路徑。 例如， `/addresschange/data.xml` 路徑建立名為 `addresschange` 並把它放在有效載荷上。 也只能指定 `data.xml` 只發送已提交的資料而不建立資料夾層次結構。 使用變數選項，然後從工作流模型可用的變數清單中選擇變數。

>[!NOTE]
無論是否為外部資料儲存標籤工作流模型，都可以使用變數。

* **附件**:您可以使用 **[!UICONTROL 附件路徑]** 的子菜單。 資料夾是相對於負載建立的。 如果將工作流標籤為外部資料儲存，請使用變數選項並從可用於工作流模型的變數清單中選擇變數。

* **記錄文檔**:它包含為自適應表單生成的記錄文檔。 您可以使用 **[!UICONTROL 記錄路徑的文檔]** 選項，指定「記錄文檔」檔案的名稱和檔案相對於負載的路徑。 例如， `/addresschange/DoR.pdf` 路徑建立名為 `addresschange` 與負載相關，並將 `DoR.pdf` 相對負載。 也只能指定 `DoR.pdf` 只保存「記錄文檔」而不建立資料夾層次結構。 如果將工作流標籤為外部資料儲存，請使用變數選項並從可用於工作流模型的變數清單中選擇變數。

## Adaptive Form中的伺服器端重新驗證 {#server-side-revalidation-in-adaptive-form}

通常，在任何線上資料捕獲系統中，開發人員都會在客戶端上進行一些JavaScript驗證，以強制執行一些業務規則。 但在現代瀏覽器中，最終用戶可以繞過這些驗證，使用各種技術（如Web瀏覽器DevTools控制台）手動執行提交。 這種技術對於自適應形式也是有效的。 表單開發人員可以建立各種驗證邏輯，但從技術上講，最終用戶可以繞過這些驗證邏輯，將無效資料提交到伺服器。 無效資料會破壞表單作者強制執行的業務規則。

伺服器端重新驗證功能還提供了在伺服器上設計自適應表單時運行自適應表單作者所提供的驗證的功能。 它防止以表單驗證形式表示的資料提交和業務規則違規的任何可能危害。

### 在伺服器上驗證什麼？ {#what-to-validate-on-server-br}

在伺服器上重新運行的自適應表單的現成(OOTB)欄位驗證包括：

* 必要
* 驗證圖片子句
* 驗證表達式

### 啟用伺服器端驗證 {#enabling-server-side-validation-br}

使用 **在伺服器上重新驗證** 的子菜單。

![啟用伺服器端驗證](assets/revalidate-on-server.png)

啟用伺服器端驗證

如果最終用戶繞過這些驗證並提交表單，伺服器將再次執行驗證。 如果驗證在伺服器端失敗，則提交事務將停止。 最終用戶再次呈現原始形式。 捕獲的資料和提交的資料作為錯誤呈現給用戶。

>[!NOTE]
伺服器端驗證會驗證表單模型。 建議建立單獨的客戶端庫以進行驗證，但不要將其與HTML樣式和DOM操作等其他內容混合到同一客戶端庫中。

### 在驗證表達式中支援自定義函式 {#supporting-custom-functions-in-validation-expressions-br}

有時，如果存在複雜的驗證規則，則確切的驗證指令碼位於自定義函式中，作者從欄位驗證表達式中調用這些自定義函式。 要使此自定義函式館在執行伺服器端驗證時已知且可用，表單作者可以在以下位置配置AEM客戶端庫的名稱： **基本** 頁籤，如下所示。

![在驗證表達式中支援自定義函式](assets/clientlib-cat.png)

在驗證表達式中支援自定義函式

作者可以按自適應格式配置customJavaScript庫。 在庫中，只保留可重用函式，這些函式依賴於jquery和underloge.js第三方庫。

## 提交操作時處理錯誤 {#error-handling-on-submit-action}

作為Experience Manager安全性和強化准則的一部分，配置自定義錯誤頁，如404.jsp和500.jsp。 在提交表單404或500錯誤時，將調用這些處理程式。 在「發佈」節點上觸發這些錯誤代碼時，也會調用處理程式。

有關詳細資訊，請參見 [自定義錯誤處理程式顯示的頁](/help/sites-developing/customizing-errorhandler-pages.md)。
