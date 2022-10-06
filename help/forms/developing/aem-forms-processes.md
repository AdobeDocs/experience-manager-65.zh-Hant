---
title: 了解AEM Forms程式
seo-title: Understanding AEM Forms Processes
description: 了解AEM Forms程式
uuid: 7cbebe7d-f222-42fa-8eb6-d2443458a791
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools, coding
discoiquuid: ac9fe461-63e7-442b-bd1c-eb9576ef55aa
role: Developer
exl-id: 434ac316-8a01-43a6-844b-1b792f60fa21
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 0%

---

# 了解AEM Forms程式 {#understanding-aem-forms-processes}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

一組AEM Forms服務在單一檔案上運作的常見使用案例為。 您可以使用Workbench建立程式，將請求傳送至服務容器。 流程表示您正在自動化的業務流程。 如需建立程式的相關資訊，請參閱 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

一旦啟動進程，它就會變成服務，可以像其他服務一樣叫用。 標準服務（如加密服務）和源自進程的服務之間的一個區別是，後者具有執行多個操作的一個操作。 相反，標準服務有許多操作。 每個操作通常執行一個操作，例如將策略應用於文檔或加密文檔。

過程可以是短期的，也可以是長期的。 短期進程是同步執行的操作，在調用該操作的同一執行線程上執行。 短期操作與大多數寫程式語言中的標準行為類似，在這些語言中，客戶端應用程式調用方法並等待返回值。

但是，在某些情況下，由於下列因素，無法同步完成程式：

* 過程可能會跨越很長時間。
* 程式可跨越組織界限。
* 進程需要外部輸入才能完成。 例如，假設表單已傳送給不在辦公室的經理。 在這種情況下，在管理員返回並填寫表單之前，該過程不會完成。

   這些類型的進程稱為長期進程。 非同步執行長期進程，允許系統在資源允許時進行交互，並允許跟蹤和監視操作。 當調用長期進程時，AEM Forms將建立調用標識符值作為跟蹤長期進程狀態的記錄的一部分。 記錄會儲存在AEM Forms資料庫中。 您可以在不再需要長期流程記錄時將其清除。

>[!NOTE]
>
>AEM Forms不會在叫用短期程式時建立記錄。

使用調用標識符值，可以跟蹤長期進程的狀態。 例如，您可以使用進程調用標識符值來執行進程管理器操作，如終止正在運行的進程實例。

**短期流程示例**

下圖是名為 *MyApplication/EncryptDocument*.

>[!NOTE]
>
>此程式並非以現有的AEM Forms程式為基礎。 若要遵循討論如何叫用此程式的程式碼範例，請建立名為 `MyApplication/EncryptDocument` 使用Workbench。 (請參閱 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

調用此短期進程時，它將執行以下操作：

1. 獲取傳遞至流程的不安全PDF文檔作為輸入值。
1. 使用密碼加密PDF文檔。 此過程的輸入參數的名稱為 `inDoc` 而資料類型是文檔。
1. 將密碼加密的PDF文檔作為PDF檔案保存到本地檔案系統。 此過程將加密的PDF文檔返回為輸出值。 此過程的輸出參數的名稱為 `outDoc` 而資料類型是文檔。

   此進程在調用該進程的同一執行線程上同步完成。 這個短期過程的名稱是 `MyApplication/EncryptDocument`它的操作 `invoke`.

   >[!NOTE]
   >
   >通常，短期流程包含三個以上的動作。 您可以使用Workbench建立流程。 (請參閱 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

   *使用AEM表單進行程式設計*&#x200B;描述了以下可以用程式設計方式調用此短期進程的方法：

   * [使用AEM Forms Remoting傳遞不安全的檔案，以叫用短期處理程式](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting) (使用Flex應用程式)
   * [使用叫用API叫用短期處理程式](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api) （Java調用API）
   * [使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding) （網站服務範例）
   * [使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom) （網站服務範例）
   * [使用SwaRef叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref) （網站服務範例）
   * [透過HTTP使用BLOB資料叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http) （網站服務範例）
   * [使用DIME叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime) （網站服務範例）
   * [使用REST調用MyApplication/EncryptDocument進程](/help/forms/developing/invoking-aem-forms-using-rest.md)

**長期流程示例**

下圖是長期處理程式的範例。

申請人提交貸款表時，會援引此程式。 在貸款官員批准或拒絕貸款請求之前，該過程才會完成。 這個長期過程的名稱是 *FirstAppSolution/PreLoanProcess* 它的操作 `invoke_Async`. 必須非同步叫用此程式。 有關以寫程式方式調用此長期進程的資訊，請參見 [調用以人為中心的長壽命過程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

>[!NOTE]
>
>您可以依照 [建立您的第一個AEM Forms應用程式](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63).
