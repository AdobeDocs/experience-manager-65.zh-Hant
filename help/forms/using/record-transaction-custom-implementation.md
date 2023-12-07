---
title: 記錄自訂實作的交易
description: 使用TransactionRecorder API來記錄未自動計入交易的動作
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
exl-id: a1d97b15-14a6-4c3d-bdd3-6366f7acdfc8
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# 記錄自訂實作的交易 {#record-a-transaction-for-custom-implementations}

使用TransactionRecorder API來記錄未自動計入交易的動作

您可以使用自訂程式碼來提交PDF表單，或傳送代理程式UI預覽URL給一般使用者，以預覽互動式通訊。 或者，您也可使用自訂方法來提交表單，而不使用AEM Forms隨附的提交方法。 AEM Forms API前面提到的所有動作和自訂實作都不會計為交易。 AEM Forms提供API、 [TransactionRecorder](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/aem/transaction/core/ITransactionRecorder.html)，將這類動作記錄為交易。

若要記錄交易，請寫入 [標準sling servlet](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/store-and-retrieve-af-with-2fa/create-servlet.html?lang=en) 並從使用者端呼叫servlet來記錄交易。 您可以使用AJAX或任何其他標準方法呼叫servlet。

## 伺服器端程式碼範例 {#sample-server-sided-code}

您可以使用以下範常式式碼，使用自訂OSGi套件從Java™類別執行TransactionRecorder API。

```java
import com.adobe.aem.transaction.core.ITransactionRecorder;
import com.adobe.aem.transaction.core.model.TransactionRecord;
import com.adobe.aem.transaction.core.exception.TransactionException;
import com.adobe.aem.transaction.core.FormsTransactionConstants;

@Reference
private ITransactionRecorder transactionRecorder;

doPost (SlingHttpServletRequest request, SlingHttpServletResponse response) {
    transactionRecorder.startContext();
    TransactionRecord txRecord = extractTxRecordFromRequest(request); //extract transaction relevant data from request
    try {
        bool success = doBillableWork();
        if (success) {
            transactionRecorder.recordTransaction(txRecord);
        }
    } catch (Exception e) {
        //exception handling
    } finally {
        transactionRecorder.endContext();
    }
}

//Here, it is assumed that txInfo is passed in Stringified json form in the ajax call (in data parameter). You can pass txInfo from client in any way that you find suitable.
private TransactionRecord extractTxRecordFromRequest(SlingHttpServletRequest request) {
    BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(request.getInputStream()));
    Map<String, Object> txDataMap = new HashMap<String, Object>();
    String txData = bufferedReader.readLine();
    JSONObject txInfo= new JSONObject(txData );
    try {
        String resourceType= txInfo.getString("resourceType");
        String transactionType = txInfo.getString("transactionType");
        Integer transactionCount = (Integer)txInfo.get("transactionCount");
        //Extract all the relevant tx record attributes similarly and pass them in Transaction Record constructor as per the java doc}
        return new TransactionRecord(transactionCount, transactionType, resourceType, ..);
    } catch (JSONException e) {
        //exception handling
    } finally {
        bufferedReader.close();
    }
}
```

## 使用者端代碼範例 {#sample-client-side-code}

您可以使用以下範常式式碼來呼叫具有下列專案的servlet： `TransactionRecorder`API。

```javascript
$.ajax({
   type: 'POST',
   url: url, //servlet url
   contentType: 'application/json; UTF-8',
   data: JSON.stringify({transactionCount : 1,
                        transactionType: "SUBMIT",
                        resourceType: "FORM",
                        resourceSubType: "ADAPTIVE-FORM"}),
   success: successHandler,
   error: faultHandler
})
```

## 相關文章 {#related-articles}

* [交易報表概觀](/help/forms/using/transaction-reports-overview.md)
* [檢視與瞭解交易報表](/help/forms/using/viewing-and-understanding-transaction-reports.md)
* [交易報表可記帳API](/help/forms/using/transaction-reports-billable-apis.md)
