---
title: 交易報表概觀
description: 保持提交的所有表單、演算的互動式通訊、轉換為另一種格式的檔案等專案的計數
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Transaction Reports
exl-id: bb812614-f4d8-4f57-bea2-8f7d31457039
solution: Experience Manager, Experience Manager Forms
source-git-commit: d3822f4dee1b0d571aa06142f4a4f6e27874cf53
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# OSGi上AEM Forms的交易報告 {#transaction-reports-overview}

<!--## Introduction {#introduction}

Transaction reports in AEM Forms let you keep a count of all transactions taken place since a specified date on your AEM Forms deployment. The objective is to provide information about product usage and help business stakeholders understand their digital processing volumes. Examples of a transaction include:

* Submission of an adaptive form, an HTML5 Form, or a form set
* Rendition of a print or a web version of an interactive communication
* Conversion of a document from one file format to another

For more information on what is considered a transaction, see [Billable APIs](../../forms/using/transaction-reports-billable-apis.md).-->

交易記錄預設為停用。 您可以 [啟用交易記錄](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports) 從AEM Web主控台。 您可以檢視關於作者、處理或發佈執行個體的交易報告。 檢視所有交易彙總之作者或處理執行個體的交易報告。 在發佈執行個體上檢視交易報告，以取得僅在該發佈執行個體上發生的所有交易的計數，該發佈執行個體是執行報告的來源。

請勿在同一AEM例項上製作內容（建立最適化表單、互動式通訊、主題和其他製作活動）並處理檔案（使用工作流程、檔案服務和其他處理活動）。 讓用來製作內容的AEM Forms伺服器停用交易記錄。 讓用來處理檔案的AEM Forms伺服器保持啟用交易記錄。

![sample-transaction-report-author-1](assets/sample-transaction-report-author-1.png)

交易在緩衝區中保留指定的期間（排清緩衝區時間+反向復寫時間）。 依預設，交易計數大約需要90秒才會反映在交易報表中。

提交PDF表單、使用代理程式UI預覽互動式通訊或使用非標準表單提交方法等動作不會計為交易。 AEM Forms提供API來記錄這類交易。 從您的自訂實作中呼叫API以記錄交易。

## 支援的拓撲 {#supported-topology}

交易報告只能在OSGi環境的AEM Forms上使用。 它支援author-publish、author-processing-publish並僅處理拓撲。 例如，拓撲，請參閱 [AEM Forms的架構和部署拓撲](../../forms/using/transaction-reports-overview.md).

交易計數會從發佈執行個體反向復寫到製作或處理執行個體。 指示性的作者 — 發佈拓撲顯示如下：

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>AEM Forms交易報表不支援僅包含發佈例項的拓撲。

### 使用交易報表的准則 {#guidelines-for-using-transaction-reports}

* 停用所有編寫執行個體的交易報告，因為編寫執行個體的報告包含在編寫活動期間註冊的交易。
* 啟用 **僅顯示來自發佈的交易** 編寫執行個體上的選項，用於檢視來自所有發佈執行個體的累積交易。 您也可以檢視每個發佈執行個體的交易報告，瞭解僅限該特定發佈執行個體的實際交易。
* 請勿使用作者執行個體來執行工作流程和處理檔案。
* 在使用交易報告之前，如果您擁有發佈伺服器的主題，請確定所有發佈執行個體都啟用了反向復寫。
* 交易資料會從發佈執行個體反向復寫至僅對應的製作或處理執行個體。 製作或處理執行個體無法進一步將資料復寫至其他執行個體。 例如，如果您有author-processing-publish拓撲，則彙總的交易資料只會復寫到處理執行個體。

## 相關文章 {#related-articles}

* [在OSGi上檢視和瞭解AEM Forms的交易報告](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [透過OSGi為AEM Forms提供交易報表可記帳API](../../forms/using/transaction-reports-billable-apis.md)
* [在OSGi上記錄AEM Forms的自訂實作交易](/help/forms/using/record-transaction-custom-implementation.md)
