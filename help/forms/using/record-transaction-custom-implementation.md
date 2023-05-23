---
title: 記錄自定義實現的事務
seo-title: Record a transaction for custom implementations
description: 使用TransactionRecorder API記錄未自動入帳為事務的操作
seo-description: Use the TransactionRecorder API to record actions which are not accounted as transactions automatically
uuid: a22b1a0b-7553-4a17-8fb4-a3bee97b4a98
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 0d961630-573b-4c8e-902f-996f1d1265b6
exl-id: a1d97b15-14a6-4c3d-bdd3-6366f7acdfc8
source-git-commit: 18cfefb794382b5314b18a62645f1fba28d314a2
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# 記錄自定義實現的事務 {#record-a-transaction-for-custom-implementations}

使用TransactionRecorder API記錄未自動入帳為事務的操作

您可以使用自定義代碼提交PDF表單或將代理UI預覽URL發送給最終用戶以預覽互動式通信。 或者，您使用自定義方法提交表單，而不是使用隨AEM Forms提供的提交方法。 以前提到的AEM FormsAPI的所有操作和自定義實現均不作為事務處理入賬。 AEM Forms提供了一個API [事務記錄器](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/aem/transaction/core/ITransactionRecorder.html)，將這些操作記錄為事務。

要記錄事務處理，請編寫 [標準sling servlet](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/store-and-retrieve-af-with-2fa/create-servlet.html?lang=en) 從客戶端調用servlet記錄事務。 可以使用或任何其AJAX它標準方法調用servlet。

## 伺服器端代碼示例 {#sample-server-sided-code}

可以使用以下示例代碼從Java™類使用自定義OSGi包運行TransactionRecorder API。

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

## 示例客戶端代碼 {#sample-client-side-code}

可以使用以下示例代碼調用具有 `TransactionRecorder`API。

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

* [事務處理報表概覽](/help/forms/using/transaction-reports-overview.md)
* [查看和瞭解事務處理報表](/help/forms/using/viewing-and-understanding-transaction-reports.md)
* [事務處理報表可開單API](/help/forms/using/transaction-reports-billable-apis.md)
