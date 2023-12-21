---
title: 設定提交動作
description: Forms可讓您設定提交動作，以定義提交後處理最適化表單的方式。 您可以使用內建提交動作，或從頭開始編寫您自己的動作。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: 04efb4ad-cff6-4e05-bcd2-98102f052452
source-git-commit: 9f88eeb6770c59f7a52db30f19f3a1a78cbc401b
workflow-type: tm+mt
source-wordcount: '2581'
ht-degree: 49%

---

# 設定提交動作 {#configuring-the-submit-action}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，用來[建立新的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html) |
| AEM 6.5 | 本文章 |


## 提交動作簡介 {#introduction-to-submit-actions}

當使用者按一下最適化表單上的提交按鈕時，就會觸發提交動作。 您可以在最適化表單上設定提交動作。 調適型表單提供一些立即可用的提交動作。 您可以複製並擴充預設提交動作，以建立您自己的提交動作。 不過，您可以根據自己的需求，編寫並註冊自己的提交動作，以處理提交表單中的資料。 提交動作可使用 [同步或非同步提交](../../forms/using/asynchronous-submissions-adaptive-forms.md).

您可在以下位置設定提交動作： **提交** 側邊欄中的最適化表單容器屬性的區段。

![設定提交動作](assets/thank-you-setting.png)

設定提交動作

最適化表單可用的預設提交動作如下：

* 提交到 REST 端點
* 寄送電子郵件
* 透過電子郵件傳送PDF
* 叫用Forms Workflow
* 使用表單資料模型提交
* Forms Portal提交動作
* 叫用AEM工作流程
* 提交至 Power Automate

>[!NOTE]
>
>透過電子郵件傳送PDF提交動作僅適用於使用XFA範本作為表單模型的最適化表單。

>[!NOTE]
>
>確保 [AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM資料夾
>「 」已存在。 需要目錄才能暫時儲存附件。 如果目錄不存在，請建立目錄。

>[!CAUTION]
>
>如果您 [預填](../../forms/using/prepopulate-adaptive-form-fields.md) 表單範本、表單資料模型或結構描述型調適型表單針對不含資料的結構描述（XML結構描述、JSON結構描述、表單範本或表單資料模型）提出XML或JSON資料投訴 &lt;afdata>， &lt;afbounddata>、和 &lt;/afunbounddata> 標籤，則無限制欄位的資料(無限制欄位是自適應表單欄位，無 [bindref](../../forms/using/prepopulate-adaptive-form-fields.md) 屬性)。

您可以撰寫最適化表單的自訂提交動作，以符合您的使用案例。 如需詳細資訊，請參閱 [撰寫最適化表單的自訂提交動作](../../forms/using/custom-submit-action-form.md).

## 提交到 REST 端點 {#submit-to-rest-endpoint}

此 **提交至REST端點** 提交選項會將表單中填寫的資料傳遞至已設定的確認頁面，作為HTTPGET請求的一部分。 您可以新增要求的欄位名稱。要求的格式為：

`{fieldName}={request parameter name}`

如下圖所示， `param1` 和 `param2` 是以引數傳遞，其值複製自 **文字方塊** 和 **數值方塊** 下一個動作的欄位。

您也可以「**啟用 POST 要求**」並提供用於發佈要求的 URL。若要將資料提交至託管表單的Experience Manager伺服器，請使用與Experience Manager伺服器根路徑對應的相對路徑。 例如， /content/forms/af/SampleForm.html。 若要將資料提交到任何其他伺服器，請使用絕對路徑。

![設定 REST 端點提交動作](assets/action-config.png)

設定Rest端點提交動作

>[!NOTE]
>
若要將欄位做為 REST URL 的參數傳遞，所有欄位都必須具有不同的元素名稱，即使這些欄位位於不同面板上也是如此。

### 將提交的資料發佈到資源或外部Rest端點  {#post-submitted-data-to-a-resource-or-external-rest-end-point-nbsp}

使用「**提交到 REST 端點**」動作會將提交的資料發佈到 REST URL。該 URL 可以是內部伺服器 (呈現表單的伺服器) 或外部伺服器。

若要將資料發佈到內部伺服器，請提供資源的路徑。資料會發佈到資源的路徑。例如 /content/restEndPoint。對於此類發佈要求，會使用提交要求的驗證資訊。

若要將資料發佈到外部伺服器，請提供 URL。URL的格式為https://host:port/path_to_rest_end_point。 請確保設定以匿名方式處理 POST 要求的路徑。

![做為「感謝頁面」參數傳遞之欄位值的對應](assets/post-enabled-actionconfig.png)

在上面的範例中，在 `textbox` 輸入的資訊是使用 `param1` 參數來擷取。使用 `param1` 發佈所擷取之資料的語法是：

`String data=request.getParameter("param1");`

同樣地，用於發佈 XML 資料和附件的參數是 `dataXml` 和 `attachments`。

例如，您會在指令碼中使用這兩個參數將資料剖析到 REST 端點。您會使用以下語法來儲存和剖析資料：

`String data=request.getParameter("dataXml");`
`String att=request.getParameter("attachments");`

在這個範例中，`data` 會儲存 XML 資料，而 `att` 會儲存附件資料。

## 寄送電子郵件 {#send-email}

此 **傳送電子郵件** 提交動作會在成功提交表單時傳送電子郵件給一或多個收件者。 產生的電子郵件可以包含預先定義的格式表單資料。

>[!NOTE]
>
所有表單欄位都必須有不同的元素名稱（即使它們放在不同的面板上），才能在電子郵件中包含表單資料。

## 透過電子郵件傳送PDF {#send-pdf-via-email}

此 **透過電子郵件傳送PDF** 提交動作會在成功提交表單時，傳送內含表單資料PDF的電子郵件給一或多個收件者。

>[!NOTE]
>
此提交動作適用於具有記錄檔案範本的XFA型最適化表單和XSD型最適化表單。

## 叫用Forms Workflow {#invoke-a-forms-workflow}

此 **提交至Forms Workflow** 提交選項會將資料xml和檔案附件（如果有的話）傳送至現有的AdobeLiveCycle或JEE程式上的AEM Forms。

如需有關如何設定「提交至Forms Workflow」提交動作的資訊，請參閱 [使用表單工作流程提交和處理您的表單資料](../../forms/using/submit-form-data-livecycle-process.md).

## 使用表單資料模型提交 {#submit-using-form-data-model}

此 **使用表單資料模型提交** 提交動作會將表單資料模型中指定資料模型物件的已提交最適化表單資料寫入其資料來源。 設定提交動作時，您可以選擇資料模型物件，將其提交的資料寫入其資料來源。

此外，您可以使用表單資料模型和記錄檔案(DoR)將表單附件提交至資料來源。

如需表單資料模型的相關資訊，請參閱 [AEM Forms資料整合](../../forms/using/data-integration.md).

## Forms Portal提交動作 {#forms-portal-submit-action}

此 **Forms Portal提交動作** 選項可透過AEM Forms入口網站提供表單資料。

如需Forms入口網站與提交動作的詳細資訊，請參閱 [草稿和提交元件](../../forms/using/draft-submission-component.md).

## 叫用 AEM 工作流程 {#invoke-an-aem-workflow}

「**[!UICONTROL 叫用 AEM 工作流程]**」提交動作會將最適化表單與 [AEM 工作流程](/help/sites-developing/workflows-models.md)建立關聯。提交表單後，相關聯的工作流程就會在作者執行個體上自動開始。您可以將資料檔案、附件和記錄檔案儲存至相對資料夾，或工作流程裝載下的資料夾，或儲存至變數。 如果工作流程標示為外部資料儲存，則變數選項可用，而不是裝載選項。 您可以從可用於工作流程模型的變數清單中選取。如果工作流程是在後續階段標記為外部資料儲存空間，而不是在建立工作流程時標記，則請確保已經具備所需的變數設定。

使用之前 **叫用AEM工作流程** 提交動作， [設定Experience ManagerDS設定](../../forms/using/configuring-the-processing-server-url-.md). 如需建立AEM工作流程的詳細資訊，請參閱 [OSGi上以表單為中心的工作流程](../../forms/using/aem-forms-workflow.md).

提交動作會將下列專案置於工作流程的裝載位置。 但請注意，如果工作流程模型標示為外部資料儲存，則只會顯示「變數」選項，而不會顯示「裝載」選項。

* **資料檔案**：包含提交給最適化表單的資料。您可以使用「**[!UICONTROL 資料檔案路徑]**」選項來指定相對於承載的檔案名稱和檔案路徑。例如，`/addresschange/data.xml` 路徑會建立一個名為 `addresschange` 的資料夾，並將其置於相對於承載的位置。您也可以僅指定 `data.xml`，僅發送提交的資料而不建立資料夾階層。使用變數選項，並從工作流程模型可用的變數清單中選取變數。

>[!NOTE]
>
無論工作流程模型是否標示為外部資料儲存，都可以使用變數。

* **附件**：您可以使用「**[!UICONTROL 附件路徑]**」選項，指定用來儲存上傳到最適化表單之附件的資料夾名稱。該資料夾會建立在相對於承載的位置。如果工作流程標記為外部資料儲存空間，請使用變數選項，並從工作流程模型可用的變數清單中選取變數。

* **記錄文件**：包含為最適化表單產生的記錄文件。您可以使用「**[!UICONTROL 記錄文件路徑]**」選項指定記錄文件檔案的名稱，以及相對於承載的檔案路徑。例如，`/addresschange/DoR.pdf` 路徑會在相對於承載的位置建立一個名為 `addresschange` 的資料夾，並將 `DoR.pdf` 放置在相對於承載的位置。您也可以指定 `DoR.pdf` 僅儲存記錄文件而不建立資料夾階層。如果工作流程標記為外部資料儲存空間，請使用變數選項，並從工作流程模型可用的變數清單中選取變數。

## 提交至 Power Automate {#microsoft-power-automate}

您可以設定最適化表單，在提交時執行 Microsoft® Power Automate Cloud Flow。設定的最適化表單會將擷取的資料、附件和記錄文件傳送到 Power Automate Cloud Flow 進行處理。那有助於建置自訂資料擷取體驗，同時利用 Microsoft® Power Automate 的強大功能，根據擷取的資料建置商業邏輯，並將客戶工作流程自動化。以下是整合最適化表單與 Microsoft® Power Automate 後，可以執行的部分操作範例：

* 在 Power Automate 業務流程中使用最適化表單資料
* 使用 Power Automate 將擷取的資料傳送到 500 多個資料來源或任何公開可用的 API
* 對擷取的資料執行複雜的計算
* 按預定義的排程將最適化表單資料儲存到儲存系統

最適化表單編輯器提供&#x200B;**叫用 Microsoft® Power Automate 流程**&#x200B;提交動作，將最適化表單資料、附件和記錄文件發送到 Power Automate Cloud Flow。若要使用提交動作將擷取的資料傳送至Microsoft®Power Automate， [連線您的AEM Forms執行個體與Microsoft® Power Automate](/help/forms/using/forms-microsoft-power-automate-integration.md)

在設定成功之後，使用[叫用 Microsoft® Power Automate 流程](/help/forms/using/forms-microsoft-power-automate-integration.md#use-the-invoke-a-microsoft&reg;-power-automate-flow-submit-action-to-send-data-to-a-power-automate-flow-use-the-invoke-microsoft-power-automate-flow-submit-action)提交動作，將資料傳送到 Power Automate Flow。

## 提交至Microsoft® SharePoint清單{#submit-to-sharedrive}

「**[!UICONTROL 提交到 SharePoint]**」提交動作會將最適化表單與 Microsoft® SharePoint 儲存空間建立連結。您可以將表單資料檔案、附件或記錄檔案提交至連線的Microsoft® Sharepoint儲存體。

### 將最適化表單連線至Microsoft® SharePoint清單 {#connect-af-sharepoint-list}

若要使用 [!UICONTROL 提交至SharePoint清單] 以最適化表單提交動作：

1. [建立SharePoint清單設定](#create-sharepoint-list-configuration)：它會將AEM Forms連線至您的Microsoft® Sharepoint清單儲存空間。
1. [在最適化表單中使用表單資料模型提交](#use-submit-using-fdm)：此動作會將您的最適化表單連線至設定的Microsoft® SharePoint。

#### 建立SharePoint清單設定 {#create-sharepoint-list-configuration}

若要將AEM Forms連線至您的Microsoft®Sharepoint清單：

1. 前往 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** >  **[!UICONTROL Microsoft® SharePoint]**.
1. 選取一個&#x200B;**設定容器**。設定會儲存在選取的設定容器中。
1. 按一下 **[!UICONTROL 建立]** > **[!UICONTROL SharePoint清單]** 下拉式清單中的。 此時會顯示 SharePoint 設定精靈。
1. 指定「**[!UICONTROL 標題]**」、「**[!UICONTROL 用戶端 ID]**」、「**[!UICONTROL 用戶端密碼]**」和「**[!UICONTROL OAuth URL]**」。如需有關如何擷取 OAuth URL 之用戶端 ID、用戶端密碼、租用戶 ID 的資訊，請參閱 [Microsoft® 文件](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)。
   * 您可以從 Microsoft® Azure 入口網站擷取應用程式的 `Client ID` 和 `Client Secret`。
   * 在 Microsoft® Azure 入口網站中，將重新導向 URI 新增為 `https://[author-instance]/libs/cq/sharepointlist/content/configurations/wizard.html`。以作者執行個體的 URL 取代 `[author-instance]`。
   * 新增API許可權 `offline_access` 和 `Sites.Manage.All` 在 **Microsoft® Graph** 索引標籤以提供讀取/寫入許可權。 新增 `AllSites.Manage` 中的許可權 **Sharepoint** 索引標籤以與SharePoint資料進行遠端互動。
   * 使用 OAuth URL：`https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`。從 Microsoft® Azure 入口網站，以應用程式的 `tenant-id` 取代 `<tenant-id>`。

     >[!NOTE]
     >
     **用戶端密碼**&#x200B;欄位為必填或選用，取決於您的 Azure Active Directory 應用程式設定。如果您的應用程式設定為使用用戶端密碼，就必須提供用戶端密碼。

1. 按一下「**[!UICONTROL 連結]**」。連結成功後，就會顯示 `Connection Successful` 訊息。
1. 選取 **[!UICONTROL SharePoint網站]** 和 **[!UICONTROL SharePoint清單]** 下拉式清單中的。
1. 點選 **[!UICONTROL 建立]** 以建立Microsoft® SharePointList的雲端設定。

#### 在最適化表單中使用表單資料模型提交 {#use-submit-using-fdm}

您可以在調適型表單中使用已建立的SharePoint清單設定，以在SharePoint清單中儲存資料或產生的記錄檔案。 執行以下步驟，在最適化表單中使用SharePoint清單儲存體設定：

1. [使用Microsoft建立表單資料模型](/help/forms/using/create-form-data-model.md)
1. [設定表單資料模型以擷取及傳送資料](/help/forms/using/work-with-form-data-model.md#configure-services)
1. [建立最適化表單](/help/forms/using/create-adaptive-form.md).
1. [使用表單資料模型設定提交動作](/help/forms/using/configuring-submit-actions.md#submit-using-form-data-model-submit)

提交表單時，資料會儲存在指定的Microsoft® Sharepoint清單儲存空間中。

>[!NOTE]
>
Microsoft® SharePoint清單不支援下列欄型別：
* 影像欄
* 中繼資料欄
* 人員欄
* 外部資料欄


>[!NOTE]
>
若要設定值，請[使用 AEM SDK 產生 OSGi 設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=zh-Hant#generating-osgi-configurations-using-the-aem-sdk-quickstart)，並[將設定部署至](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=zh-Hant#deployment-process)您的 Cloud Service 執行個體。

## 最適化表單中的伺服器端重新驗證 {#server-side-revalidation-in-adaptive-form}

一般而言，在任何線上資料擷取系統中，開發人員都會在用戶端放置一些 JavaScript 驗證，以強制執行一些業務規則。但在現代的瀏覽器中，一般使用者可以略過那些驗證，並使用各種技巧 (例如 Web Browser DevTools Console) 手動進行提交。這些技巧對於最適化表單也是有效的。 表單開發人員可以建立各種驗證邏輯，但技術上而言，一般使用者可以略過那些驗證邏輯並提交無效的資料給伺服器。無效的資料會破壞表單作者強制執行的業務規則。

伺服器端重新驗證功能也提供在伺服器上設計最適化表單時，執行最適化表單作者所提供的驗證的功能。 這樣可以避免對提交的資料造成任何可能的危害，以及在表單驗證方面違反業務規則。

### 伺服器上會進行哪些驗證？ {#what-to-validate-on-server-br}

在伺服器上重新執行的所有適用性表單的現成可用(OOTB)欄位驗證包括：

* 必填
* 驗證圖片子句
* 驗證運算式

### 啟用伺服器端驗證 {#enabling-server-side-validation-br}

使用在側邊欄「最適化表單容器」下方的「**在伺服器上重新驗證**」，即可對目前表單啟用或停用伺服器端驗證。

![啟用伺服器端驗證](assets/revalidate-on-server.png)

啟用伺服器端驗證

如果一般使用者略過那些驗證並提交表單，伺服器將再次執行驗證。如果伺服器端驗證失敗，就會停止提交交易。系統會再次對一般使用者呈現原始表單。擷取的資料和提交的資料會做為錯誤呈現給使用者。

>[!NOTE]
>
伺服器端驗證會驗證表單模型。建議您建立個別的使用者端程式庫進行驗證，不要將其與相同使用者端程式庫中的HTML樣式和DOM操作等其他專案混合。

### 支援驗證運算式中的自訂函數 {#supporting-custom-functions-in-validation-expressions-br}

有時，如果有複雜的驗證規則，確切的驗證指令碼會位於自訂函式中，且作者會從欄位驗證運算式呼叫這些自訂函式。 若要在執行伺服器端驗證時公開和提供此自訂函數程式庫，表單作者可以在「最適化表單容器」屬性的「**基礎**」標籤下方，設定 AEM 用戶端程式庫的名稱，如以下所示。

![支援驗證運算式中的自訂函數](assets/clientlib-cat.png)

支援驗證運算式中的自訂函數

作者可以根據每個最適化表單設定customJavaScript程式庫。 程式庫中只會保留可重複使用的函數，這些函數與 jquery 和 underscore.js 第三方程式庫有相依性。

## 提交動作的錯誤處理 {#error-handling-on-submit-action}

在Experience Manager安全性和強化准則中，請設定自訂錯誤頁面，例如404.jsp和500.jsp。 提交表單時出現404或500錯誤時，會呼叫這些處理常式。 在Publish節點上觸發這些錯誤碼時，也會呼叫處理常式。

如需詳細資訊，請參閱 [自訂錯誤處理常式顯示的頁面](/help/sites-developing/customizing-errorhandler-pages.md).
