---
title: 事務處理報表概覽
seo-title: 事務處理報表概覽
description: 記住所有提交的表單、轉換的互動式通訊、轉換為一種格式的檔案等
seo-description: 記住所有提交的表單、轉換的互動式通訊、轉換為一種格式的檔案等
uuid: 2c3dc1f3-5bbf-4aab-aa84-7aef5aabadf6
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b2c09e6b-a1d8-4b30-af2c-988442a3a986
docset: aem65
translation-type: tm+mt
source-git-commit: 8f90dc4865126d52e04effc9197ef7145b1a167e

---


# 事務處理報表概覽{#transaction-reports-overview}

## 簡介 {#introduction}

AEM Forms中的交易報表可讓您記住自AEM Forms部署指定日期以來發生的所有交易計數。 其目的在於提供產品使用的相關資訊，並協助業務相關人員瞭解其數位處理量。 交易範例包括：

* 提交最適化表單、HTML5表單或表單集
* 互動式通訊的列印版或網頁版轉譯
* 將文檔從一種檔案格式轉換為另一種檔案格式

有關被視為事務處理的詳細資訊，請參 [閱計費API](../../forms/using/transaction-reports-billable-apis.md)。

事務記錄預設為停用。 您可以 [從AEM Web Console](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports) 啟用交易記錄。 您可以檢視有關作者、處理或發佈例項的交易報表。 查看所有事務處理匯總的作者或處理實例的事務處理報告。 檢視發佈例項上的交易報表，以計算僅在執行報表之發佈例項上發生的所有交易計數。

請勿在相同AEM例項上編寫內容（建立最適化表單、互動式通訊、主題和其他編寫活動）及處理檔案（使用工作流程、檔案服務和其他處理活動）。 針對用於製作內容的AEM Forms伺服器，請停用交易記錄。 讓用於處理檔案的AEM Forms伺服器啟用交易記錄。

![sample-transaction-report-author-1](assets/sample-transaction-report-author-1.png)

事務在指定期間（刷新緩衝時間+反向複製時間）內保留在緩衝區中。 依預設，交易計數大約需要90秒才能反映在交易報表中。

提交PDF表單、使用代理UI預覽互動式通訊或使用非標準表單提交方法等動作不會視為交易。 AEM Forms提供API來記錄此類交易。 從您的自訂實作呼叫API以記錄交易。

## 支援的拓撲 {#supported-topology}

交易報表僅適用於OSGi環境上的AEM Forms。 它支援作者——發佈、作者——處理——發佈，並僅支援處理拓撲。 例如，請參閱「AEM Forms [的架構和部署拓撲」](../../forms/using/transaction-reports-overview.md)。

事務計數從發佈實例反向複製到作者或處理實例。 指示性的作者發佈拓撲如下：

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>AEM Forms交易報表不支援僅包含發佈例項的拓撲。

### 使用事務處理報表的准則 {#guidelines-for-using-transaction-reports}

* 停用所有作者例項的交易報表，因為作者例項的報表包括製作活動期間註冊的交易。
* 啟用作 **者例項上的「僅顯示發佈中的交易** 」選項，以檢視所有發佈例項的累積交易。 您也可以檢視每個發佈例項上的交易報表，以取得該特定發佈例項上的實際交易。
* 請勿使用作者例項來執行工作流程和處理檔案。
* 在使用事務報告之前，如果您具有包含發佈伺服器的拓撲，請確保對所有發佈實例啟用了反向複製。
* 交易資料會從發佈例項反向複製至僅對應的作者或處理例項。 作者或處理例項無法進一步將資料複製至其他例項。 例如，如果您有作者處理——發佈拓撲，則聚合事務資料僅複製到處理實例。

## 相關文章 {#related-articles}

* [查看和瞭解事務處理報表](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [事務處理報表可開單API](../../forms/using/transaction-reports-billable-apis.md)
* [記錄自訂實作的交易](/help/forms/using/record-transaction-custom-implementation.md)

