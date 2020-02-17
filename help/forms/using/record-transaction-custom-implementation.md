---
title: 記錄自訂實作的交易
seo-title: 記錄自訂實作的交易
description: 使用TransactionRecorder API記錄未自動入帳為事務的操作
seo-description: 使用TransactionRecorder API記錄未自動入帳為事務的操作
uuid: a22b1a0b-7553-4a17-8fb4-a3bee97b4a98
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 0d961630-573b-4c8e-902f-996f1d1265b6
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78

---


# 記錄自訂實作的交易 {#record-a-transaction-for-custom-implementations}

使用TransactionRecorder API記錄未自動入帳為事務的操作

您可以使用自訂程式碼來送出PDF表單、傳送代理UI預覽URL給使用者以預覽互動式通訊，或使用自訂方法來送出表單，而非使用AEM表單隨附的送出方法。 AEM Forms API的所有先前提及的動作和自訂實作不會記錄為交易。 AEM Forms提供API [TransactionRecorder](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aem/transaction/core/ITransactionRecorder.html)，以記錄這類動作（例如交易）。

若要記錄交易，請撰寫標 [準sling servlet](https://helpx.adobe.com/experience-manager/using/custom-sling-servlets.html) ，並從用戶端呼叫servlet以記錄交易。 您可以使用AJAX或任何其他標準方法來呼叫servlet。

## 伺服器端程式碼範例 {#sample-server-sided-code}

您可以使用下列范常式式碼，從使用自訂OSGi套件的JAVA類別執行TransactionRecorder API。

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

## 用戶端程式碼範例 {#sample-client-side-code}

您可以使用下列范常式式碼來呼叫具有 `TransactionRecorder`API的servlet。

```
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

* [事務處理報表概覽](/help/forms/using/transaction-reports-overview.md)
* [查看和瞭解事務處理報表](/help/forms/using/viewing-and-understanding-transaction-reports.md)
* [事務處理報表可開單API](/help/forms/using/transaction-reports-billable-apis.md)

