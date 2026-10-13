---
title: 為JEE上的AEM Forms記錄自訂元件API的交易。
description: 瞭解如何使用TransactionRecorder API來記錄自訂元件的交易。
feature: Transaction Reports
exl-id: 33e1868a-2a7f-4785-8571-95651e661e21
role: Admin, User, Developer
solution: Experience Manager, Experience Manager Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: bcb3e79d-a57e-59a4-ad50-e03803c9f153
    internal-label: Transaction Reports
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%
---
# 為JEE上的AEM Forms記錄自訂元件API的交易 {#record-a-transaction-for-custom-components}

當您在自訂元件中使用可記帳API時，可以為元件啟用交易報告。 若要啟用交易報告，請修改元件的`component.xml`檔案，並在必須啟用交易報告的作業底下新增下列指定的標籤。

**標籤**： `<transaction-operation-type>CONVERT</transaction-operation-type> // Supported values are SUBMIT, CONVERT, RENDER.`

| 舊的作業標籤 | 新操作標籤 |
| ----------- | ----------- |
| `<operation>`<br> `<.... tags`<br>`<...>`<br>`<operation>` | `<operation>`<br> `<.... tags`<br>`<...>`<br>`<transaction-operation-type>CONVERT</transaction-operation-type`<br>`<operation>` |

如果您必須為API （例如批次API）擷取多個交易，其中交易計數會隨輸入計數而改變，請在API層級處理交易計數。

**若要記錄變動的交易計數：**

1. 在程式碼中匯入類別`"com.adobe.idp.dsc.InvocationContextStack"`。 此類別是`adobe-livecycle-client.jar` sdk檔案的一部分。 sdk檔案可在`<AEM_Forms_JEE_Install>\sdk\client-libs\common`取得

   >[!NOTE]
   > 如果您已在使用者端專案中套用檔案，請以新檔案更新上述共用的使用者端檔案。

1. 在必須記錄變動交易的API中：
   1. 新增邏輯，讓您可以將交易計數儲存在某個整數變數中，例如`transaction_count`。
   1. 作業成功時，新增`InvocationContextStack.recordTransactionCount(transaction_count)`。

<!--
For example, you can set count for your custom component by importing class `"com.adobe.idp.dsc.InvocationContextStack"` in the code available at `adobe-livecycle-client.jar`  and determine the transaction count basis API input/result and add (In this case we add count is equal to 3):
`InvocationContextStack.recordTransactionCount(<count>).` to 
`InvocationContextStack.recordTransactionCount(3)`.
-->

## 相關文章

* [在JEE上啟用和檢視AEM Forms的交易報告](/help/forms/using/transaction-report-overview-jee.md)
* [適用於AEM Forms on JEE的計費API清單](/help/forms/using/transaction-reports-billable-apis-jee.md)
