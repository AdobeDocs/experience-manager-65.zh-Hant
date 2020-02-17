---
title: 瞭解AEM Forms流程
seo-title: 瞭解AEM Forms流程
description: 'null'
seo-description: 'null'
uuid: 7cbebe7d-f222-42fa-8eb6-d2443458a791
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools
discoiquuid: ac9fe461-63e7-442b-bd1c-eb9576ef55aa
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# 瞭解AEM Forms流程 {#understanding-aem-forms-processes}

常見的使用案例是一組AEM Forms服務可在單一檔案上運作。 您可以使用Workbench建立流程，將請求傳送至服務容器。 流程代表您正在自動化的業務流程。 有關建立流程的資訊，請參 [閱使用工作台](https://www.adobe.com/go/learn_aemforms_workbench_63)。

一旦程式被激活，它就會變成服務，並可像其他服務一樣被調用。 標準服務（如加密服務）和源自進程的服務之間的一個區別是，後者有一個操作可執行多個操作。 相反，標準服務有許多操作。 每個操作通常執行一個操作，例如將策略應用於文檔或加密文檔。

流程可以是短期的或長期的。 短時進程是同步執行的操作，在調用該進程的同一執行線程上執行。 短期操作可與大多數寫程式語言中的標準行為相媲美，在這些語言中，客戶端應用程式調用方法並等待返回值。

但是，有些情況下，由於以下因素，進程無法同步完成：

* 流程可以跨越大量時間。
* 流程可以跨越組織界限。
* 流程需要外部輸入才能完成。 例如，假設某個情況表單被傳送至不在辦公室的經理。 在這種情況下，在管理員返回並填寫表單之前，該過程不會完成。

   這些類型的進程稱為長期進程。 非同步地執行長壽命進程，允許系統在資源許可的情況下進行交互，並允許跟蹤和監視操作。 當呼叫長期進程時，AEM Forms會建立呼叫識別碼值，作為追蹤長期進程狀態的記錄的一部分。 記錄會儲存在AEM Forms資料庫中。 您可以在不再需要長期流程記錄時清除這些記錄。

   **注意**:當呼叫短期處理時，AEM Forms不會建立記錄。

   使用調用標識符值，可以跟蹤長壽命進程的狀態。 例如，您可以使用進程調用標識符值來執行進程管理器操作，如終止正在運行的進程實例。

**短壽命流程示例**

下圖是名為 *MyApplication/EncryptDocument的短期流程的示例*。

>[!NOTE]
>
>此程式不以現有的AEM Forms程式為基礎。 要跟隨討論如何調用此流程的代碼示例，請使用Workbench建立一個名為的 `MyApplication/EncryptDocument` 流程。 (請參 [閱使用工作台](https://www.adobe.com/go/learn_aemforms_workbench_63)。)

調用此短時間進程時，它執行以下操作：

1. 取得將傳遞至程式的不安全PDF檔案作為輸入值。
1. 使用密碼加密PDF檔案。 此流程的輸入參數名稱為， `inDoc` 資料類型為文檔。
1. 將密碼加密的PDF檔案儲存為PDF檔案至本機檔案系統。 此程式會傳回加密的PDF檔案作為輸出值。 此進程的輸出參數的名稱為，數 `outDoc` 據類型為文檔。

   此進程在調用該進程的同一執行線程上同步完成。 這個短期過程的名稱是， `MyApplication/EncryptDocument`它的操作是 `invoke`。

   >[!NOTE]
   >
   >通常，短期流程包含三個以上的動作。 您可以使用Workbench建立流程。 (請參 [閱使用工作台](https://www.adobe.com/go/learn_aemforms_workbench_63)。)

   *使用AEM格式*&#x200B;進行程式設計，說明以下方式可以程式設計方式叫用這個短暫的程式：

   * [使用AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting) （使用Flex應用程式）傳遞不安全的檔案，以叫用短暫的程式
   * [使用調用API](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api) （Java調用API）調用短時間進程
   * [使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding) （web service範例）
   * [使用MTOM叫用AEM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom) Forms（web service範例）
   * [使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref) （web service範例）
   * [使用透過HTTP的BLOB資料叫用AEM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http) Forms（web service範例）
   * [使用DIME叫用AEM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime) Forms（web service範例）
   * [使用REST調用MyApplication/EncryptDocument進程](/help/forms/developing/invoking-aem-forms-using-rest.md)

**長期流程示例**

下圖是長期處理的範例。

當申請人提交貸款表時，將調用此流程。 在貸款官員批准或拒絕貸款申請之前，該程式尚未完成。 此長期流程的名稱是 *FirstAppSolution/PreLoanProcess* ，其操作為 `invoke_Async`。 必須以非同步方式呼叫此程式。 如需以程式設計方式叫用此長壽命程式的詳細資訊，請 [參閱叫用以人為中心的長壽命程式](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。

>[!NOTE]
>
>您可依照「建立您的第一個AEM Forms應用程式」中指 [定的教學課程來建立此程式](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)。