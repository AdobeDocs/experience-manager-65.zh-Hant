---
title: 瞭解AEM Forms進程
seo-title: Understanding AEM Forms Processes
description: 瞭解AEM Forms進程
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

# 瞭解AEM Forms進程 {#understanding-aem-forms-processes}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

一個通用案例是一組AEM Forms服務在單個檔案上運行。 您可以通過使用Workbench建立流程將請求發送到服務容器。 流程表示您正在自動執行的業務流程。 有關建立進程的資訊，請參見 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。

一旦某個進程被激活，它就會成為服務，並且可以像其他服務一樣被調用。 標準服務（如加密服務）與源自進程的服務之間的一個區別是，進程具有一個執行多個操作的操作。 相反，標準服務有許多操作。 每個操作通常執行一個操作，例如將策略應用於文檔或加密文檔。

進程可以是短期的，也可以是長期的。 短生命週期進程是同步執行的操作，並在調用該進程的同一執行線程上執行。 短期操作與大多數寫程式語言中的標準行為類似，在這些語言中，客戶端應用程式調用方法並等待返回值。

但是，有些情況下，由於以下因素，無法同步完成進程：

* 進程可以跨越大量時間。
* 流程可以跨越組織邊界。
* 進程需要外部輸入才能完成。 例如，考慮將表單發送給不在辦公室的經理的情況。 在這種情況下，只有經理返回並填寫表單後，該過程才會完成。

   這些類型的進程稱為長期進程。 非同步地執行長壽命處理，允許系統在資源許可時進行交互，並允許對操作進行跟蹤和監視。 當調用長壽命進程時，AEM Forms會建立調用標識符值，作為跟蹤長壽命進程狀態的記錄的一部分。 記錄儲存在AEM Forms資料庫中。 您可以在不再需要長期流程記錄時清除這些記錄。

>[!NOTE]
>
>AEM Forms在調用短時間進程時不會建立記錄。

使用調用標識符值，可以跟蹤長壽命進程的狀態。 例如，可以使用進程調用標識符值來執行進程管理器操作，如終止正在運行的進程實例。

**短期流程示例**

下圖是名為的短時間進程的示例 *MyApplication/EncryptDocument*。

>[!NOTE]
>
>該進程不基於現有的AEM Forms進程。 要跟隨討論如何調用此進程的代碼示例，請建立一個名為 `MyApplication/EncryptDocument` 使用Workbench。 (請參閱 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。)

調用此短時間進程時，它將執行以下操作：

1. 獲取作為輸入值傳遞給流程的無擔保PDF文檔。
1. 使用密碼加密PDF文檔。 此進程的輸入參數的名稱為 `inDoc` 資料類型是文檔。
1. 將密碼加密的PDF文檔另存為PDF檔案到本地檔案系統。 此進程將加密的PDF文檔返回為輸出值。 此進程的輸出參數的名稱為 `outDoc` 資料類型是文檔。

   此進程在調用該進程的同一執行線程上同步完成。 這個短暫過程的名稱是 `MyApplication/EncryptDocument`它的運作 `invoke`。

   >[!NOTE]
   >
   >通常，短期過程包含三個以上的操作。 使用Workbench建立流程。 (請參閱 [使用Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63)。)

   *用表格編AEM程*&#x200B;介紹了以下可以以寫程式方式調用此短暫進程的方法：

   * [通過使用AEM Forms遠程處理傳遞不安全文檔來調用短時間流程](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting) (使用Flex應用程式)
   * [使用調用API調用短期進程](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api) （Java調用API）
   * [使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding) （Web服務示例）
   * [使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom) （Web服務示例）
   * [使用SwaRef調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref) （Web服務示例）
   * [通過HTTP調用AEM Forms使用BLOB資料](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http) （Web服務示例）
   * [使用DIME調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime) （Web服務示例）
   * [使用REST調用MyApplication/EncryptDocument進程](/help/forms/developing/invoking-aem-forms-using-rest.md)

**長壽命流程實例**

下圖是長壽命流程的示例。

申請人提交貸款表時會調用此流程。 在貸款幹事批准或拒絕貸款請求之前，該程式尚未完成。 這個長生不老的過程 *FirstAppSolution/PreLoanProcess* 它的運作 `invoke_Async`。 必須非同步調用此進程。 有關以寫程式方式調用此長期進程的資訊，請參見 [調用以人為中心的長壽命進程](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)。

>[!NOTE]
>
>可以按照中指定的教程建立此過程 [建立第一個AEM Forms應用程式](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)。
