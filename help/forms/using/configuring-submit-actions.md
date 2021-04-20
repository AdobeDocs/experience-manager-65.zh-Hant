---
title: 設定「提交」動作
seo-title: 設定「提交」動作
description: Forms可讓您設定提交動作，以定義提交後如何處理最適化表單。 您可以使用內建的提交動作，或從頭開始編寫您自己的動作。
uuid: 4368d648-88ea-4f84-a051-46296a1a084e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9d8d7044-ffce-4ab4-9543-a2d2f9da31e3
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: ebe7042b931869c3b4b7204e3ce7afa52d56f0ef
workflow-type: tm+mt
source-wordcount: '1514'
ht-degree: 1%

---


# 配置提交操作{#configuring-the-submit-action}

## 提交操作簡介{#introduction-to-submit-actions}

當使用者按一下最適化表單上的「提交」按鈕時，會觸發提交動作。 您可以在最適化表單上設定提交動作。 最適化表單提供一些現成可用的提交動作。 您可以複製並延伸預設的提交動作，以建立您自己的提交動作。 不過，根據您的要求，您可以撰寫並註冊自己的提交動作，以處理提交表單中的資料。 提交操作可以使用[同步或非同步提交](../../forms/using/asynchronous-submissions-adaptive-forms.md)。

您可以在側欄的「最適化表單容器」屬性的&#x200B;**Submission**&#x200B;區段中設定提交動作。

![設定提交動作](assets/thank-you-setting.png)

設定提交動作

最適化表單的預設提交動作包括：

* 提交到REST端點
* 傳送電子郵件
* 透過電子郵件傳送PDF
* 叫用Forms Workflow
* 使用表單資料模型提交
* Forms門戶網站提交操作
* 叫用工AEM作流程

>[!NOTE]
>
>透過電子郵件傳送PDF的提交動作僅適用於使用XFA範本做為表單模型的最適化表單。

>[!NOTE]
>
>請確定[AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM folder
>存在. 目錄需要臨時儲存附件。 如果目錄不存在，請建立該目錄。

>[!CAUTION]
>
>如果您[prefill](../../forms/using/prepopulate-adaptive-form-fields.md)表單範本、表單資料模型或架構式自適應表單，且XML或JSON資料會抱怨至資料不包含&lt;afData>、&lt;afBoundData>和&lt;/afUnboundData>標籤的架構（XML架構、JSON架構、表單範本或表單資料模型），則資料無界欄位（無界欄位是自適應表單欄位，沒有自適應表單的[bindref](../../forms/using/prepopulate-adaptive-form-fields.md)屬性）。

您可以撰寫自訂的提交動作，讓最適化表單符合使用案例。 如需詳細資訊，請參閱[針對最適化表單撰寫自訂提交動作](../../forms/using/custom-submit-action-form.md)。

## 提交到REST端點{#submit-to-rest-endpoint}

**提交到REST端點**&#x200B;提交選項將表單中填充的資料傳遞到配置的確認頁，作為HTTPGET請求的一部分。 您可以新增要請求的欄位名稱。 請求的格式為：

`{fieldName}={request parameter name}`

如下圖所示，`param1`和`param2`會以參數的形式傳遞，其值會從&#x200B;**textbox**&#x200B;和&#x200B;**numeric box**&#x200B;欄位複製，以供下一個動作使用。

您也可以&#x200B;**啟用POST請求**，並提供URL以張貼請求。 要向托管表單的Experience Manager伺服器提交資料，請使用與Experience Manager伺服器的根路徑對應的相對路徑。 例如，/content/forms/af/SampleForm.html。 若要將資料送出至任何其他伺服器，請使用絕對路徑。

![配置Rest端點提交操作](assets/action-config.png)

配置Rest端點提交操作

>[!NOTE]
若要將欄位傳遞為REST URL中的參數，所有欄位都必須有不同的元素名稱，即使欄位放在不同的面板上亦然。

### 將提交的資料張貼至資源或外部休息端點  {#post-submitted-data-to-a-resource-or-external-rest-end-point-nbsp}

使用&#x200B;**提交到REST端點**&#x200B;操作將提交的資料發佈到其餘URL。 URL可以是內部（轉譯表單的伺服器）或外部伺服器。

若要將資料張貼至內部伺服器，請提供資源路徑。 資料會張貼在資源的路徑上。 例如，/content/restEndPoint。 對於這些貼文請求，使用提交請求的驗證資訊。

若要將資料張貼至外部伺服器，請提供URL。 URL的格式為https://host:port/path_to_rest_end_point。 請確定您已設定路徑以匿名方式處理POST請求。

![映射作為感謝頁面參數傳遞的欄位值](assets/post-enabled-actionconfig.png)

在上述範例中，使用參數`param1`擷取使用者在`textbox`中輸入的資訊。 使用`param1`張貼擷取資料的語法為：

`String data=request.getParameter("param1");`

同樣地，用於發佈XML資料和附件的參數是`dataXml`和`attachments`。

例如，您在指令碼中使用這兩個參數，將資料剖析至其餘端點。 您使用下列語法來儲存和剖析資料：

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

在此示例中，`data`儲存XML資料，而`att`儲存附件資料。

## 傳送電子郵件 {#send-email}

**傳送電子郵件**&#x200B;提交動作會在表單成功提交時傳送電子郵件給一或多個收件者。 產生的電子郵件可以包含預先定義格式的表單資料。

>[!NOTE]
所有表格欄位都必須有不同的元素名稱，即使這些名稱位於不同的面板上)，以便在電子郵件中包含表格資料。

## 透過電子郵件傳送PDF {#send-pdf-via-email}

**透過電子郵件傳送PDF**&#x200B;提交動作會在成功提交表單時，傳送含有表單資料之PDF的電子郵件給一或多個收件者。

>[!NOTE]
此提交操作適用於具有記錄文檔模板的基於XFA的適應性表單和基於XSD的適應性表單。

## 叫用Forms Workflow{#invoke-a-forms-workflow}

**提交到Forms Workflow**&#x200B;提交選項將資料xml和檔案附件（如果有）發送到現有AdobeLiveCycle或AEM Forms的JEE流程。

如需如何設定「提交至Forms Workflow提交」動作的詳細資訊，請參閱[使用表單工作流程](../../forms/using/submit-form-data-livecycle-process.md)提交和處理表單資料。

## 使用表單資料模型提交 {#submit-using-form-data-model}

**使用表單資料模型提交操作將表單資料模型中指定資料模型對象的已提交自適應表單資料寫入其資料源。**&#x200B;在配置提交操作時，您可以選擇要將其提交的資料寫入其資料源的資料模型對象。

此外，您也可以使用表單資料模型和記錄檔案(DoR)將表單附件提交至資料來源。

如需表單資料模型的詳細資訊，請參閱[AEM Forms資料整合](../../forms/using/data-integration.md)。

## Forms門戶網站提交操作{#forms-portal-submit-action}

**Forms門戶提交操作**&#x200B;選項使表單資料可通過AEM Forms門戶獲得。

有關Forms門戶網站和提交行動的詳細資訊，請參閱[草稿和提交部分](../../forms/using/draft-submission-component.md)。

## 叫用AEM工作流{#invoke-an-aem-workflow}

**叫用Workflow&lt;a1/AEM>提交操作將自適應表單與WorkflowAEM關聯。**&#x200B;提交表單時，相關工作流程會自動在處理節點上啟動。 此外，它還會將資料檔案、附件和記錄檔案（如果適用）放在工作流程的裝載位置。

在使用&#x200B;**叫用WorkflowAEM**&#x200B;提交操作之前，[配置Experience ManagerDS設定](../../forms/using/configuring-the-processing-server-url-.md)。 如需有關建立工作AEM流程的詳細資訊，請參閱OSGi](../../forms/using/aem-forms-workflow.md)上的[表單導向工作流程。

## Adaptive Form {#server-side-revalidation-in-adaptive-form}中的伺服器端重新驗證

通常，在任何線上資料擷取系統中，開發人員會在用戶端放置一些JavaScript驗證，以執行一些業務規則。 但是在現代瀏覽器中，使用者可以略過這些驗證，並使用各種技術（例如Web Browser DevTools Console）手動進行提交。 這些技術也適用於自適應表單。 表單開發人員可以建立各種驗證邏輯，但技術上來說，使用者可以略過這些驗證邏輯，並將無效的資料送出至伺服器。 無效的資料會中斷表單作者已強制執行的業務規則。

伺服器端重新驗證功能也提供執行最適化表單作者在伺服器上設計最適化表單時所提供驗證的功能。 它可防止在表單驗證中呈現的資料提交和違反業務規則的行為受到任何可能的危害。

### 在伺服器上驗證什麼？{#what-to-validate-on-server-br}

在伺服器上重新運行的自適應表單的現成可用(OOTB)欄位驗證包括：

* 必要
* 驗證圖片子句
* 驗證運算式

### 啟用伺服器端驗證{#enabling-server-side-validation-br}

使用側欄中「Adaptive Form Container」（最適化表單容器）下的「Revalidate on server&lt;a1/」（在伺服器上重新驗證）來啟用或禁用當前表單的伺服器端驗證。****

![啟用伺服器端驗證](assets/revalidate-on-server.png)

啟用伺服器端驗證

如果使用者略過這些驗證並送出表單，伺服器會再次執行驗證。 如果驗證在伺服器端失敗，則會停止提交交易。 最終用戶將再次顯示原始表單。 擷取的資料和提交的資料會以錯誤呈現給使用者。

>[!NOTE]
伺服器端驗證會驗證表單模型。 建議您建立個別的用戶端程式庫以進行驗證，而不要將它與HTML樣式和DOM控制等其他項目混合在相同的用戶端程式庫中。

### 支援驗證運算式{#supporting-custom-functions-in-validation-expressions-br}中的自訂函式

有時，如果有複雜的驗證規則，則完全的驗證指令碼會位於自訂函式中，而作者會從欄位驗證運算式呼叫這些自訂函式。 為了在執行伺服器端驗證時使此自定義函式館為已知和可用，表單作者可以在Adaptive Form Container屬性的&#x200B;**Basic**&#x200B;頁籤下配置客戶端庫的名稱，如下所示。

![支援驗證運算式中的自訂函式](assets/clientlib-cat.png)

支援驗證運算式中的自訂函式

作者可以依據最適化表單來設定customJavaScript程式庫。 在程式庫中，僅保留可重複使用的函式，這些函式依賴於jquery和undershore.js協力廠商程式庫。

## 提交操作{#error-handling-on-submit-action}時出錯處理

作為Experience Manager安全性和強化准則的一部分，請設定自訂錯誤頁面，例如404.jsp和500.jsp。 在提交表單404或500錯誤時，會呼叫這些處理常式。 在「發佈」節點上觸發這些錯誤代碼時，也會調用處理程式。

如需詳細資訊，請參閱[自訂錯誤處理常式](/help/sites-developing/customizing-errorhandler-pages.md)所顯示的頁面。
