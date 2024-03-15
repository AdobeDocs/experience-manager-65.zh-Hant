---
title: 為JEE上的AEM Forms記錄自訂元件API的交易。
description: 使用TransactionRecorder API來記錄自訂元件的交易。
feature: Transaction Reports
source-git-commit: d0db00de6b767a12a9492bbbcec49a8c5d25ff27
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# 為JEE上的AEM Forms記錄自訂元件API的交易 {#record-a-transaction-for-custom-components}

當您在自訂元件中使用可記帳API時，可以啟用元件的交易報告。 若要啟用交易報告，請修改 `component.xml` 建立元件檔案，並在需要啟用交易報告的作業底下新增以下指定的標籤。

**標籤**： `<transaction-operation-type>CONVERT</transaction-operation-type> // Supported values are SUBMIT, CONVERT, RENDER.`

| 舊的作業標籤 | 新操作標籤 |
| ----------- | ----------- |
| `<operation>`<br> `<.... tags`<br>`<...>`<br>`<operation>` | `<operation>`<br> `<.... tags`<br>`<...>`<br>`<transaction-operation-type>CONVERT</transaction-operation-type`<br>`<operation>` |

如果需要為API擷取多個交易，例如，在批次API中，交易計數可能會隨輸入計數而改變。在這些情況下，您需要在API層次處理交易計數。 記錄變動交易次數的指定步驟如下：

1. 匯入類別 `"com.adobe.idp.dsc.InvocationContextStack"` 在程式碼中。 此類別屬於 `adobe-livecycle-client.jar` sdk檔案。 sdk檔案位於 `<AEM_Forms_JEE_Install>\sdk\client-libs\common`

   >[!NOTE]
   > 如果您已在使用者端專案中套用檔案，請以新檔案更新上述共用的使用者端檔案。

1. 在需要記錄各種交易的API中：
   1. 新增邏輯以將交易計數儲存在某些整數變數中，例如 `transaction_count`.
   1. 作業成功時，新增 `InvocationContextStack.recordTransactionCount(transaction_count)`.

<!--For example, you can set count for your custom component by importing class `"com.adobe.idp.dsc.InvocationContextStack"` in the code available at `adobe-livecycle-client.jar`  and determine the transaction count basis API input/result and add (In this case we add count is equal to 3):
`InvocationContextStack.recordTransactionCount(<count>).` to 
`InvocationContextStack.recordTransactionCount(3)`.-->

## 相關文章

* [在JEE上啟用和檢視AEM Forms的交易報告](/help/forms/using/transaction-report-overview-jee.md)
* [適用於AEM Forms on JEE的計費API清單](/help/forms/using/transaction-reports-billable-apis-jee.md)


