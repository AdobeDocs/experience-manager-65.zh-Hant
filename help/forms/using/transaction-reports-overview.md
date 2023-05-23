---
title: 事務處理報表概覽
seo-title: Transaction Reports Overview
description: 保留已提交的所有表單、已呈現的互動式通信、轉換為一種格式的文檔以及更多
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

# 事務處理報表概覽{#transaction-reports-overview}

## 簡介 {#introduction}

在AEM Forms，事務報表允許您保留自指定日期以來在AEM Forms部署中發生的所有事務的計數。 目標是提供有關產品使用情況的資訊，並幫助業務相關人員瞭解其數字處理量。 事務示例包括：

* 提交自適應表單、HTML5表單或表單集
* 互動式通信的打印或網路版本的再現
* 文檔從一個檔案格式轉換到另一個檔案格式

有關被視為事務處理的詳細資訊，請參見 [可計費API](../../forms/using/transaction-reports-billable-apis.md)。

預設情況下禁用事務記錄。 你可以 [啟用交易記錄記錄](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports) 從Web控AEM制台。 您可以查看有關作者、處理或發佈實例的事務處理報告。 查看所有事務處理合計的作者或處理實例的事務處理報表。 查看發佈實例的事務報表，以查看僅在運行報表的發佈實例上發生的所有事務的計數。

不要在同一實例上創作內容（建立自適應表單、互動式通信、主題和其他創作活動）和處理文檔(使用工作流、文檔服務和其他處AEM理活動)。 對於用於創作內容的AEM Forms伺服器，保留禁用事務記錄。 為用於處理文檔的AEM Forms伺服器啟用事務記錄。

![示例事務 — 報告 — 作者–1](assets/sample-transaction-report-author-1.png)

某個事務在指定期間（刷新緩衝區時間+反向複製時間）內保留在緩衝區中。 預設情況下，事務計數在事務報表中反映大約需要90秒。

提交PDF表單、使用代理UI預覽互動式通信或使用非標準表單提交方法等操作不會作為事務處理入賬。 AEM Forms提供API來記錄此類交易。 從自定義實現調用API以記錄事務。

## 支援的拓撲 {#supported-topology}

交易報告僅在AEM FormsOSGi環境上提供。 它支援作者發佈、作者處理發佈和僅處理拓撲。 例如，拓撲，請參見 [用於AEM Forms的體系結構和部署拓撲](../../forms/using/transaction-reports-overview.md)。

事務計數從發佈實例反向複製到作者或處理實例。 下面顯示一個指示性的作者發佈拓撲：

![簡單作者發佈拓撲](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>AEM Forms事務報表不支援只包含發佈實例的拓撲。

### 使用交易記錄報表的准則 {#guidelines-for-using-transaction-reports}

* 禁用所有作者實例的事務報表，因為作者實例的報表包括創作活動期間註冊的事務。
* 啟用 **僅顯示發佈中的事務** 的子常式。 您還可以僅查看特定發佈實例上實際事務的每個發佈實例的事務處理報表。
* 不要使用作者實例運行工作流和處理文檔。
* 在使用事務報告之前，如果您具有包含發佈伺服器的頂層，請確保對所有發佈實例啟用了反向複製。
* 事務資料從發佈實例反向複製到僅對應的作者或處理實例。 作者或處理實例無法進一步將資料複製到另一個實例。 例如，如果具有作者處理 — 發佈拓撲，則聚合事務資料僅複製到處理實例。

## 相關文章 {#related-articles}

* [查看和瞭解事務處理報表](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [事務處理報表可開單API](../../forms/using/transaction-reports-billable-apis.md)
* [記錄自定義實現的事務](/help/forms/using/record-transaction-custom-implementation.md)
