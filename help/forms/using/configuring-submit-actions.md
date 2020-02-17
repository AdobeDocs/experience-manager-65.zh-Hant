---
title: 設定「提交」動作
seo-title: 設定「提交」動作
description: AEM Forms可讓您設定提交動作，以定義提交後如何處理最適化表單。 您可以使用內建的提交動作，或從頭開始編寫您自己的動作。
seo-description: AEM Forms可讓您設定提交動作，以定義提交後如何處理最適化表單。 您可以使用內建的提交動作，或從頭開始編寫您自己的動作。
uuid: 4368d648-88ea-4f84-a051-46296a1a084e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 9d8d7044-ffce-4ab4-9543-a2d2f9da31e3
docset: aem65
translation-type: tm+mt
source-git-commit: 6bd09bca68ea1fcec2dca7694dd3d39dc5153bfc

---


# 設定「提交」動作{#configuring-the-submit-action}

## 提交動作簡介 {#introduction-to-submit-actions}

當使用者按一下最適化表單上的「提交」按鈕時，會觸發提交動作。 您可以在最適化表單上設定提交動作。 最適化表單提供一些現成可用的提交動作。 您可以複製並延伸預設的提交動作，以建立您自己的提交動作。 不過，根據您的要求，您可以撰寫並註冊自己的提交動作，以處理提交表單中的資料。 提交動作可使用同 [步或非同步提交](../../forms/using/asynchronous-submissions-adaptive-forms.md)。

您可以在側欄中「最適化表單容 **器** 」屬性的「提交」區段中設定提交動作。

![設定提交動作](assets/thank-you-setting.png)

設定提交動作

最適化表單的預設提交動作包括：

* 提交到REST端點
* 傳送電子郵件
* 透過電子郵件傳送PDF
* 叫用表單工作流程
* 使用表單資料模型提交
* 表單入口網站提交動作
* 叫用AEM工作流程

>[!NOTE]
>
>透過電子郵件傳送PDF的提交動作僅適用於使用XFA範本做為表單模型的最適化表單。

>[!NOTE]
>
>請確定 [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM folder
>存在. 目錄需要臨時儲存附件。 如果目錄不存在，請建立該目錄。

>[!CAUTION]
>
>如果您以 [XML](../../forms/using/prepopulate-adaptive-form-fields.md) 或JSON資料來預先填寫表單範本、表單資料模型或架構式最適化表單，並抱怨資料不包含&lt;afData>、&lt;afBoundData>和&lt;/afUnboundData>標籤的架構（XML架構、JSON架構、表單範本或表單資料模型），則會填入無界欄位的資料(UnbounboundedData>有界欄位是沒有bindref屬 [性的自適應表單欄位](../../forms/using/prepopulate-adaptive-form-fields.md) )。

您可以撰寫自訂的提交動作，讓最適化表單符合使用案例。 如需詳細資訊，請參 [閱撰寫最適化表單的自訂提交動作](../../forms/using/custom-submit-action-form.md)。

## 提交到REST端點 {#submit-to-rest-endpoint}

「提 **交至REST端點** 」提交選項會將表單中填入的資料傳遞至已設定的確認頁面，作為HTTP GET請求的一部分。 您可以新增要請求的欄位名稱。 請求的格式為：

`{fieldName}={request parameter name}`

如下圖所示， `param1` 並以 `param2` 參數的形式傳遞，其值會從文字方塊和數值方塊欄位復 **制** , **** 以供下一個動作使用。

您也可以 **啟用POST請求** ，並提供URL以張貼請求。 若要將資料提交至代管表單的AEM伺服器，請使用與AEM伺服器根路徑對應的相對路徑。 例如，/content/forms/af/SampleForm.html。 若要將資料送出至任何其他伺服器，請使用絕對路徑。

![配置Rest端點提交操作](assets/action-config.png)

配置Rest端點提交操作

>[!NOTE]
若要將欄位傳遞為REST URL中的參數，所有欄位都必須有不同的元素名稱，即使欄位放在不同的面板上亦然。

### 將提交的資料張貼至資源或外部休息端點 {#post-submitted-data-to-a-resource-or-external-rest-end-point-nbsp}

使用「 **提交到REST端點** 」(Submit to REST Endpoint)操作，將提交的資料發佈到其餘URL。 URL可以是內部（轉譯表單的伺服器）或外部伺服器。

若要將資料張貼至內部伺服器，請提供資源路徑。 資料會張貼在資源的路徑上。 例如，/content/restEndPoint。 對於這些貼文請求，使用提交請求的驗證資訊。

若要將資料張貼至外部伺服器，請提供URL。 URL的格式為https://host:port/path_to_rest_end_point。 請確定您已設定路徑以匿名方式處理POST請求。

![映射作為感謝頁面參數傳遞的欄位值](assets/post-enabled-actionconfig.png)

在上述範例中，使用者輸入的資訊會 `textbox` 使用參數來擷取 `param1`。 用於張貼使用下列方式擷取之資料的 `param1` 語法：

`String data=request.getParameter("param1");`

同樣地，用於發佈XML資料和附件的參數也 `dataXml` 是 `attachments`。

例如，您在指令碼中使用這兩個參數，將資料剖析至其餘端點。 您使用下列語法來儲存和剖析資料：

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

在此示例中， `data` 儲存XML資料，並 `att` 儲存附件資料。

## 傳送電子郵件 {#send-email}

「傳 **送電子郵件** 」提交動作會在表單成功提交時，傳送電子郵件給一或多個收件者。 產生的電子郵件可以包含預先定義格式的表單資料。

>[!NOTE]
所有表格欄位都必須有不同的元素名稱，即使這些名稱位於不同的面板上)，以便在電子郵件中包含表格資料。

## Send PDF via Email {#send-pdf-via-email}

「透 **過電子郵件傳送PDF** 」提交動作會在表單提交成功時，以包含表單資料的PDF傳送電子郵件給一或多個收件者。

**** 注意：此提交操作適用於具有記錄文檔模板的基於XFA的適應性表單和基於XSD的適應性表單。

## Invoke a forms workflow {#invoke-a-forms-workflow}

「提 **交至表單」工作流程** 「提交」選項會將資料xml和檔案附件（如果有的話）傳送至JEE上現有的Adobe LiveCycle或AEM Forms程式。

如需如何設定「提交至表單」工作流程提交動作的詳細資訊，請參閱「 [使用表單工作流程提交和處理表單資料」](../../forms/using/submit-form-data-livecycle-process.md)。

## 使用表單資料模型提交 {#submit-using-form-data-model}

「使 **用表單資料模型提交」(Submit using Form Data Model** )操作將表單資料模型中指定資料模型對象的已提交自適應表單資料寫入其資料源。 在配置提交操作時，您可以選擇要將其提交的資料寫入其資料源的資料模型對象。

此外，您也可以使用表單資料模型和記錄檔案(DoR)將表單附件提交至資料來源。

如需表單資料模型的詳細資訊，請參 [閱「AEM Forms資料整合」](../../forms/using/data-integration.md)。

## 表單入口網站提交動作 {#forms-portal-submit-action}

「表 **單入口網站提交動作** 」選項可讓表單資料透過AEM Forms入口網站提供。

如需Forms Portal和送出動作的詳細資訊，請參閱「 [草稿與送出」元件](../../forms/using/draft-submission-component.md)。

## Invoke an AEM Workflow {#invoke-an-aem-workflow}

「叫 **用AEM Workflow** submit」動作會將最適化表單與AEM Workflow建立關聯。 提交表單時，相關工作流程會自動在處理節點上啟動。 此外，它還會將資料檔案、附件和記錄檔案（如果適用）放在工作流程的裝載位置。

在使用「叫 **用AEM Workflow** submit」(AEM Workflow [送出)動](../../forms/using/configuring-the-processing-server-url-.md)作之前，請設定AEM DS設定。 如需有關建立AEM工作流程的詳細資訊，請參閱「 [OSGi上以表單為中心的工作流程」](../../forms/using/aem-forms-workflow.md)。

## Adaptive Form中的伺服器端重新驗證 {#server-side-revalidation-in-adaptive-form}

通常，在任何線上資料擷取系統中，開發人員會在用戶端放置一些javascript驗證，以強制執行一些業務規則。 但是在現代瀏覽器中，使用者可以略過這些驗證，並使用各種技術（例如Web Browser devTools Console）手動進行提交。 這些技術也適用於適應性形式。 表單開發人員可以建立各種驗證邏輯，但技術上來說，使用者可以略過這些驗證邏輯，並將無效的資料送出至伺服器。 無效的資料會中斷表單作者已強制執行的業務規則。

伺服器端重新驗證功能也提供執行最適化表單作者在伺服器上設計最適化表單時所提供驗證的功能。 它可防止在表單驗證中呈現的資料提交和違反業務規則的行為受到任何可能的危害。

### 在伺服器上驗證什麼？ {#what-to-validate-on-server-br}

在伺服器上重新運行自適應表單的出廠設定(OOTB)欄位驗證，包括：

* 必要
* 驗證圖片子句
* 驗證運算式

### 啟用伺服器端驗證 {#enabling-server-side-validation-br}

使用側 **欄中Adaptive Form Container下的Revalidate on server** （在伺服器上重新驗證），以啟用或停用目前表單的伺服器端驗證。

![啟用伺服器端驗證](assets/revalidate-on-server.png)

啟用伺服器端驗證

如果使用者略過這些驗證並送出表單，伺服器會再次執行驗證。 如果驗證在伺服器端失敗，則會停止提交交易。 最終用戶再次呈現原始形式。 擷取的資料和提交的資料會以錯誤呈現給使用者。

### 支援驗證運算式中的自訂函式 {#supporting-custom-functions-in-validation-expressions-br}

有時，如果是複雜的驗 **證規則**，完全的驗證指令碼會駐留在自訂函式中，而作者會從欄位驗證運算式呼叫這些自訂函式。 若要讓此自訂函式館在執行伺服器端驗證時已知可用，表單作者可在「Adaptive Form Container」屬性的「 **Basic** 」（基本）標籤下設定AEM用戶端程式庫的名稱，如下所示。

![支援驗證運算式中的自訂函式](assets/clientlib-cat.png)

支援驗證運算式中的自訂函式

作者可依最適化表單設定自訂javascript程式庫。 在程式庫中，僅保留可重複使用的函式，而這些函式依賴於jquery和undershore.js協力廠商程式庫。

## 提交動作的錯誤處理 {#error-handling-on-submit-action}

作為AEM安全性與強化准則的一部分，請設定自訂錯誤頁面，例如404.jsp和500.jsp。 在提交表單404或500錯誤時，會呼叫這些處理常式。 在「發佈」節點上觸發這些錯誤代碼時，也會調用處理程式。

如需詳細資訊，請參 [閱自訂錯誤處理常式所顯示的頁面](/help/sites-developing/customizing-errorhandler-pages.md)。
