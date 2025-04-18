---
title: 瞭解AEM Forms流程
description: 瞭解AEM Forms的流程包含表單建立、提交、資料處理、驗證、整合、工作流程自動化和輸出管理。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools, coding
role: Developer
exl-id: 434ac316-8a01-43a6-844b-1b792f60fa21
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 939a2efa64c853928a9082aa30d7338e98deb695
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 0%

---

# 瞭解AEM Forms流程 {#understanding-aem-forms-processes}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

一組在單一檔案上操作的AEM Forms服務的常見使用案例。 您可以使用Workbench建立處理作業，將請求傳送至服務容器。 流程代表您正在自動化的業務流程。 如需有關建立程式的資訊，請參閱[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。

程式一旦啟動，就會變成服務，並可像其他服務一樣叫用。 標準服務（例如Encryption服務）與源自處理序的服務之間的一個差異，是後者有一個執行許多動作的作業。 相反地，標準服務有很多操作。 每個操作通常會執行一個動作，例如將原則套用到檔案或加密檔案。

程式可以是短期或長期。 短期程式是在從中叫用的相同執行緒上同步執行的操作。 短期作業可與大多數程式設計語言中的標準行為相提並論，在這些行為中，使用者端應用程式會呼叫方法並等待傳回值。

但是，在某些情況下，由於以下因素，流程無法同步完成：

* 一個流程可能持續相當長的時間。
* 一個流程可以跨越組織界限。
* 處理序需要外部輸入才能完成。 例如，考慮將表單傳送給不在辦公室的經理的情況。 在此情況下，在管理員返回並填寫表單之前，該程式不會完成。

  這些型別的程式稱為長期程式。 非同步執行長時間的流程，以便在資源允許時讓系統互動，並允許追蹤和監控操作。 叫用長期處理程式時，AEM Forms會建立叫用識別碼值，作為追蹤長期處理程式狀態之記錄的一部分。 記錄儲存在AEM Forms資料庫中。 您可在不再需要長期處理記錄時將其清除。

>[!NOTE]
>
>叫用短期程式時，AEM Forms不會建立記錄。

您可以使用引動識別碼值來追蹤長期處理程式的狀態。 例如，您可以使用處理序呼叫識別碼值來執行「處理序管理員」作業，例如終止執行中的處理序執行處理。

**短期處理程式範例**

下圖是名為&#x200B;*MyApplication/EncryptDocument*&#x200B;的短期處理序範例。

>[!NOTE]
>
>此程式並非以現有AEM Forms程式為基礎。 若要跟隨討論如何叫用此程式的程式碼範例，請使用Workbench建立名為`MyApplication/EncryptDocument`的程式。 （請參閱[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

叫用此短期處理程式時，會執行下列動作：

1. 取得不安全的PDF檔案，該檔案會作為輸入值傳遞至處理序。
1. 使用密碼加密PDF檔案。 此處理序的輸入引數名稱是`inDoc`，資料型別是document。
1. 將密碼加密的PDF檔案儲存為PDF檔案至本機檔案系統。 此程式會傳回加密的PDF檔案作為輸出值。 此處理序的輸出引數名稱是`outDoc`，資料型別是document。

   此程式會在從中叫用它的相同執行緒上同步完成。 此短期處理序的名稱為`MyApplication/EncryptDocument`，其作業為`invoke`。

   >[!NOTE]
   >
   >通常一個短暫的流程包含三個以上的動作。 您可以使用「維護作業」來建立處理。 （請參閱[使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。）

   *使用AEM Forms進行程式設計*&#x200B;說明下列以程式設計方式叫用此短期處理序的方式：

   * [使用AEM Forms Remoting傳遞不安全的檔案，以叫用短期程式](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting) (使用Flex應用程式)
   * [使用叫用API](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api) (Java™叫用API)叫用短期處理程式
   * [使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding) （Web服務範例）
   * [使用MTOM叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom) （Web服務範例）
   * [使用SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)叫用AEM Forms （Web服務範例）
   * [透過HTTP使用BLOB資料叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http) （Web服務範例）
   * [使用DIME叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime) （Web服務範例）
   * [使用REST叫用MyApplication/EncryptDocument程式](/help/forms/developing/invoking-aem-forms-using-rest.md)

**長期處理程式範例**

下圖是長期流程的範例。

當申請人提交貸款表單時，會呼叫此處理。 在貸款專員核准或拒絕貸款請求之前，該流程不會完成。 此長期處理序的名稱為&#x200B;*FirstAppSolution/PreLoanProcess*，其作業為`invoke_Async`。 此程式必須以非同步方式叫用。 如需以程式設計方式叫用這個長效處理序的相關資訊，請參閱[叫用以人為中心的長效處理序](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。

>[!NOTE]
>
>您可以依照[建立您的第一個AEM Forms應用程式](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)中指定的教學課程來建立此程式。
