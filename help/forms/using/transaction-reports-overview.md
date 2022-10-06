---
title: 交易報表概述
seo-title: Transaction Reports Overview
description: 記下所有提交的表單、所呈現的互動式通訊、轉換為另一種格式的檔案等
seo-description: Keep a count of all the forms submitted, interactive communication rendered, Documents converted to one format to another, and more
uuid: 2c3dc1f3-5bbf-4aab-aa84-7aef5aabadf6
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b2c09e6b-a1d8-4b30-af2c-988442a3a986
docset: aem65
exl-id: bb812614-f4d8-4f57-bea2-8f7d31457039
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# 交易報表概述{#transaction-reports-overview}

## 簡介 {#introduction}

AEM Forms中的交易報表可讓您保留自AEM Forms部署上指定日期以來發生的所有交易計數。 其目標是提供產品使用資訊，並協助業務利害關係人了解其數位處理量。 交易範例包括：

* 提交最適化表單、HTML5表單或表單集
* 交互通信的打印或Web版本的轉譯
* 將文檔從一個檔案格式轉換為另一個檔案格式

如需將交易視為交易的詳細資訊，請參閱 [計費API](../../forms/using/transaction-reports-billable-apis.md).

事務記錄預設為禁用。 您可以 [啟用交易記錄](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports) 從AEM Web Console。 您可以檢視關於製作、處理或發佈例項的交易報表。 查看所有事務處理匯總的製作或處理實例的事務處理報告。 在發佈實例上查看事務報表，以查看僅在運行報表的發佈實例上發生的所有事務的計數。

請勿在相同的AEM例項上製作內容（建立最適化表單、互動式通訊、主題和其他製作活動）和處理檔案（使用工作流程、檔案服務和其他處理活動）。 對於用於製作內容的AEM Forms伺服器，請將交易記錄保留為停用狀態。 為用於處理檔案的AEM Forms伺服器啟用交易記錄。

![sample-transaction-report-author-1](assets/sample-transaction-report-author-1.png)

事務在指定期間（刷新緩衝時間+反向複製時間）保持在緩衝區中。 依預設，交易計數大約需要90秒才會反映在交易報表中。

提交PDF表單、使用代理UI預覽互動式通訊或使用非標準表單提交方法等動作不會計為交易。 AEM Forms提供API來記錄這類交易。 從您的自訂實作呼叫API以記錄交易。

## 支援的拓撲 {#supported-topology}

交易報表僅適用於OSGi環境上的AEM Forms。 它支援製作發佈、製作處理發佈，以及僅支援處理拓撲。 如需拓撲範例，請參閱 [適用於AEM Forms的架構和部署拓撲](../../forms/using/transaction-reports-overview.md).

交易計數會從發佈例項反向複製到製作或處理例項。 以下顯示指示性的作者發佈拓撲：

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>AEM Forms交易報表不支援僅包含發佈例項的拓撲。

### 使用交易報表的准則 {#guidelines-for-using-transaction-reports}

* 停用所有製作例項的交易報表，因為製作例項的報表包括製作活動期間註冊的交易。
* 啟用 **僅顯示發佈中的事務** 選項，檢視所有發佈例項的累積交易。 您也可以檢視每個發佈例項的交易報表，以取得該特定發佈例項的實際交易。
* 請勿使用製作例項來執行工作流程和處理檔案。
* 使用交易報表之前，如果您有具有發佈伺服器的主題，請確定所有發佈執行個體已啟用反向復寫。
* 交易資料會從發佈例項反向複製至僅對應的製作或處理例項。 製作或處理例項無法進一步將資料複製至其他例項。 例如，如果您有製作處理發佈拓撲，則匯總的交易資料只會複製到處理執行個體。

## 相關文章 {#related-articles}

* [查看和了解交易報表](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [交易報表計費API](../../forms/using/transaction-reports-billable-apis.md)
* [記錄自訂實施的交易](/help/forms/using/record-transaction-custom-implementation.md)
