---
title: JEE版AEM Forms的交易報表概觀
description: 保留所有提交、轉譯、轉換至其他格式之檔案的計數，以及執行其他作業。
feature: Transaction Reports
exl-id: 77e95631-6b0d-406e-a1b8-78f8d9cceb63
role: Admin, User, Developer
solution: "Experience Manager, Experience Manager Forms"
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# 在JEE上啟用和檢視AEM Forms的交易報告 {#transaction-reports-overview}

<!--Transaction reports in AEM Forms on JEE let you keep a count of all transactions taken place on your AEM Forms deployment. The objective is to provide information about product usage and helps business stakeholders understand their digital processing volumes. Examples of a transaction include:

* Submission of a document
* Rendition of a document
* Conversion of a document from one file format to another 

For more information on what is considered a transaction, see [Billable APIs](../../forms/using/transaction-reports-billable-apis-jee.md). Transaction log helps you to gain information about the number of documents submitted, rendered, and converted.-->

## 啟用交易報告 {#enable-transaction-reporting}

依預設，會停用交易記錄。 若要啟用交易報告，請執行下列步驟：

1. 導覽至 `/adminui` 例如，在您JEE上的AEM Forms上， `http://10.14.18.10:8080/adminui`.
1. 登入身份 **管理員**.
1. 前往 **設定** > **核心系統設定** > **設定**.
1. 按一下核取方塊，以 **啟用交易報告** 和 **儲存** 設定。

   ![sample-transaction-report-jee](assets/enable-transaction-jee.png)

1. 重新啟動伺服器。
1. 除了伺服器上的變更以外，您必須在使用者端更新 `adobe-livecycle-client.jar` 檔案（如果您使用相同的檔案）。

<!--
* You can [enable transaction recording](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports) from AEM Web Console. view transaction reports on author, processing, or publish instances. View transaction reports on author or processing instances for an aggregated sum of all transactions. View transaction reports on the publish instances for a count of all transactions that take place only on that publish instance from where the report is run.
-->

<!--Do not author content (Create adaptive forms, interactive communication, themes, and other authoring activities) and process documents (Use workflows, document services, and other processing activities) on the same AEM instance. Keep the transaction recording disabled for AEM Forms servers used to author content. Keep the transaction recording enabled for AEM Forms servers used to process documents.-->

## 檢視交易報告 {#view-transaction-report}

當您啟用交易報告時，交易計數的相關資訊可透過 [透過控制面板的交易報告](#transaction-report-dashboard) 和詳細的 [透過記錄檔傳遞異動報告](#transaction-report-logfile). 兩者皆說明如下：

### 透過控制面板的交易報告 {#transaction-report-dashboard}

透過控制面板的交易報表可提供每種交易型別的交易總數。 例如，您會獲得如影像所示的已呈現、已轉換及已提交表單總數的相關資訊。 若要取得交易報表，請執行下列動作：

1. 導覽至 `/adminui` 例如，在您的AEM Forms on JEE上： `http://10.13.15.08:8080/adminui`.
1. 登入身份 **管理員**.
1. 按一下「健康狀態監視」。
1. 瀏覽至 **交易報告器** 標籤，按一下 **計算交易總數**，現在您會看到圓形圖代表已提交、已演算或已轉換的PDF forms數量。

![sample-transaction-report-jee](assets/transaction-piechart.png)


### 透過記錄檔的交易報告 {#transaction-report-logfile}

透過記錄檔進行的交易報告提供了有關每個交易的詳細資訊。 若要存取交易記錄，請遵循相對於伺服器啟動的內容路徑。 交易會擷取到單獨的記錄檔中 `transaction_log.log` 依預設。 此 **檔案路徑** 相對於伺服器啟動內容。 不同伺服器的預設路徑如下：

```
For Jboss Turnkey:
"<AEM_Forms_Installation>/jboss/bin/transaction_log.log"

For IBM Websphere: 
"<IBM_WAS_Profile_path>/transaction_log.log"

For Oracle Weblogic:
"<Weblogic_Domain_path>/transaction_log.log"

For Jboss Cluster:
"<Jboss home>/transaction_log.log"
```

範例交易記錄的範例：
`[2024-02-28 06:11:27] [INFO] TransactionRecord{service='GeneratePDFService', operation='HtmlFileToPDF', internalService='GeneratePDFService', internalOperation='HtmlFileToPDF', transactionOperationType='CONVERT', transactionCount=1, elapsedTime=1906, transactionDate=Wed Feb 28 06:11:25 UTC 2024}`

#### 異動記錄 {#transaction-record-structure-jee}

交易記錄結構會定義如何透過各個引數來記錄每個交易，例如服務、操作、交易型別等。 下文將逐一詳細說明。 交易記錄的結構如下：

```
TransactionRecord
{
    service='...', 
    operation='...', 
    internalService='...', 
    internalOperation='...', 
    transactionOperationType='...', 
    transactionCount=..., 
    elapsedTime=..., 
    transactionDate=...
}
```

* **服務**：服務的名稱。
* **操作**：作業名稱。
* **internalService**：如果有內部呼叫，則為被呼叫者的名稱，否則與服務名稱相同。
* **internalOperation**：有內部呼叫中被呼叫者的名稱，其他名稱則與作業名稱相同。
* **transactionOperationType**：交易型別（提交、轉譯、轉換）。
* **transactioncount**：交易總數。
* **經過的時間**：呼叫起始與收到回應之間的時間。
* **transactiondate**：指出服務何時叫用的時間戳記。

**交易記錄範例**：

```
[2024-02-14 14:23:25] [INFO] TransactionRecord
{
    service='BarcodedFormsService', 
    operation='decode', 
    internalService='BarcodedFormsService', 
    internalOperation='decode', 
    transactionOperationType='CONVERT', 
    transactionCount=1, 
    elapsedTime=47405, 
    transactionDate=Wed Feb 14 14:22:37 UTC 2024
}
```

## 交易記錄頻率 {#transaction-recording-frequency}

<!--Transaction persistence involves updating the total transaction count for SUBMIT, CONVERT, and RENDER operations on the server periodically: -->

記錄交易的頻率取決於伺服器上針對成功提交、演算或轉換的每個表單進行的更新操作。

* 在 **儀表板**，交易計數會定期更新，預設為1分鐘。 您可以在下列位置設定系統屬性以更新頻率 `"com.adobe.idp.dsc.transaction.recordFrequency"`. 例如，在JBoss®上適用於JEE的AEM Forms上，新增 `-Dcom.adobe.idp.dsc.transaction.recordFrequency=5` 在 `JAVA_OPTS` 將更新頻率設為5分鐘。

* 在 **交易記錄**，則當表單成功提交、演算或轉換時，每個交易的更新都會立即發生。

<!-- A transaction remains in the buffer for a specified period (Flush Buffer time + Reverse replication time). By default, it takes approximately 90 seconds for the transaction count to reflect in the transaction report.

Actions like submitting a PDF Form, using Agent UI to preview an interactive communication, or using non-standard form submission methods are not accounted as transactions. AEM Forms provides an API to record such transactions. Call the API from your custom implementations to record a transaction.

## Supported Topology {#supported-topology}

Transaction reports are available only on AEM Forms on OSGi environment. It supports author-publish, author-processing-publish, and only processing topologies. For example, topologies, see [Architecture and deployment topologies for AEM Forms](../../forms/using/transaction-reports-overview.md).

The transaction count is reverse replicated from publish instances to author or processing instances. An indicative author-publish topology is displayed below:

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>AEM Forms transaction reports does not support topologies that contain only publish instances.

### Guidelines for using transaction reports {#guidelines-for-using-transaction-reports}

* Disable transaction reports on all author instances as reports on author instances includes transactions registered during authoring activities.
* Enable the **Show transactions from publish only** option on the author instance to view cumulative transactions from all publish instances. You can also view transaction reports on each publish instance for actual transactions on that particular publish instance only.
* Do not use author instances to run workflows and process documents.
* Before using transaction reporting, if you are have a toplogy with publish servers, ensure that the reverse replication is enabled for all the publish instances.
* Transaction data is reverse-replicated from a publish instance to only corresponding author or processing instance. The author or processing instance cannot further replicate data to another instance. For example, if you have author-processing-publish topology, aggregated transaction data is replicated only to the processing instance.-->

## 相關文章 {#related-articles}

* [適用於AEM Forms on JEE的計費API清單](../../forms/using/transaction-reports-billable-apis-jee.md)
* [為JEE上的AEM Forms記錄自訂元件API的交易](/help/forms/using/record-transaction-custom-component-jee.md)
