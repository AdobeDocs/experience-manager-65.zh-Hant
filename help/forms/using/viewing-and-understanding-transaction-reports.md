---
title: 查看和瞭解事務處理報表
seo-title: 查看和瞭解事務處理報表
description: 使用交易報告就產品使用情況做出明智決策，並重新平衡對硬體和軟體的投資。
seo-description: 使用交易報告就產品使用情況做出明智決策，並重新平衡對硬體和軟體的投資。
uuid: 56d9f01d-4778-47c9-bbb2-6650a73a3f59
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c04c488b-73f3-49ba-9e89-f97497965757
docset: aem65
translation-type: tm+mt
source-git-commit: 8f90dc4865126d52e04effc9197ef7145b1a167e

---


# 查看和瞭解事務處理報表{#viewing-and-understanding-transaction-reports}

交易報表可讓您擷取並追蹤已提交表單、已處理檔案和已轉譯檔案的數量。 追蹤這些交易的目的，是為產品使用做出明智的決定，並重新平衡對硬體和軟體的投資。 如需詳細資訊，請參 [閱「AEM Forms交易報表概觀」](../../forms/using/transaction-reports-overview.md)。

## 設定事務處理報告 {#setting-up-transaction-reports}

交易報表功能是AEM表單附加元件套件的一部分。 如需在所有作者和發佈例項上安裝附加元件套件的詳細資訊，請參 [閱安裝和設定AEM表單](/help/forms/using/installing-configuring-aem-forms-osgi.md)。 安裝AEM Forms附加套件後，請執行下列動作：

* 在所有發佈實例上啟用反向複製
* 啟用交易報表
* 提供查看交易報告的權限
* （可選）配置事務處理刷新期間和出貨箱 [](/help/forms/using/installing-configuring-aem-forms-osgi.md)

>[!NOTE]
>
>* AEM Forms交易報表不支援僅包含發佈例項的拓撲。
>* 在使用事務報告之前，請確保對所有發佈實例啟用反向複製。
>* 交易資料會從發佈例項反向複製至僅對應的作者或處理例項。 作者或處理例項無法進一步將資料複製至其他例項。
>



### 在所有發佈實例上啟用反向複製 {#enable-reverse-replication-on-all-the-publish-instances}

事務報表使用反向複製來合併從發佈實例到作者實例的事務計數。 在所有發佈實例上設定反向複製。 有關設定反向複製的詳細說明，請參見 [複製](/help/sites-deploying/replication.md)。

### 啟用交易報表 {#enable-transaction-reports}

事務報表預設會停用。 您可以從AEM Web Console啟用報表。 若要在AEM Forms環境中啟用交易報表，請對所有作者和發佈例項執行下列步驟：

1. 以管理員身分登入AEM例項。 前往「工 **具** >作 **業** > **Web主控台」**。
1. 找到並開啟 **Forms Transaction Reporting服務** 。
1. 選擇「記錄事務處理」複選框。 按一下&#x200B;**「儲存」**。

   對所有作者和發佈例項重複步驟1-3。

### 提供查看交易報告的權限 {#provide-rights-to-view-a-transaction-report}

只有fd-administrator組的成員才能查看事務報告。 要允許用戶查看事務報告，請使用戶成為fd-administrator組的成員。 如需讓使用者成為AEM群組成員的指示，請參閱「使用者、群 [組和存取權限管理」](/help/sites-administering/user-group-ac-admin.md)。

### （可選）配置事務處理刷新期間和出貨箱 {#optional-configure-transaction-flush-period-and-outboxes}

事務在儲存到儲存庫之前快取在記憶體中。 依預設，快取期間（交易刷新期間）會設為60秒。 執行下列步驟以變更預設快取期間：

1. 以管理員身分登入以製作例項。 前往「工 **具** >作 **業** > **Web主控台」**。
1. 找到並開啟 **Forms Transaction Repository儲存提供程式服務** 。
1. 在「事務處理刷新期間」 **欄位中指定秒數** 。 按一下&#x200B;**「儲存」**。

反向複製會將事務資料複製到作者實例的預設外框。 您可以將交易資料放入自訂的外框。 執行下列步驟以指定自訂外框：

1. 以管理員身分登入以製作例項。 前往「工 **具** >作 **業** > **Web主控台」**。
1. 找到並開啟 **Forms Transaction Repository儲存提供程式服務** 。
1. 在「輸出方塊」欄位中指定自訂 **輸出方塊** 。 按一下&#x200B;**「儲存」**。所有作者實例上都會建立具有指定名稱的輸出框。

## 查看事務處理報表 {#viewing-the-transaction-report}

您可以檢視有關作者或發佈例項的交易報表。 作者實例的事務報表提供在已配置的作者和發佈實例上發生的所有事務的匯總。 發佈例項上的交易報表提供僅在基礎發佈例項上發生的交易計數。 執行下列步驟以檢視報表：

1. 請登入AEM Forms伺服器，網址為 `https://[hostname]:[port]`。
1. 導覽至「 **工具** >表 **單**>檢視交易報&#x200B;**表」**。

## 瞭解報表 {#understanding-the-report}

AEM Forms會顯示自設定日期起的交易報表，如以下摘要報表所示：

![sample-transaction-report-author](assets/sample-transaction-report-author.png)

* 使用「 **將日期重設為今天** 」選項來重設交易記錄。 將日期重設為今天時，所有先前的交易記錄都會遺失。 當您重設作者例項的日期時，變更不會影響「發佈」例項的交易報表，反之亦然。
* 使用「 **僅顯示發佈實例的事務」** ，查看僅在已配置的發佈實例或發佈場上發生的所有事務。
* 使用類別：Document Processed ****、Documents **Rendered**&#x200B;和Forms **Submitted** to view correspondations. 有關這些類別中入帳的事務處理類型，請參 [閱：可開單事務處理報表API](../../forms/using/transaction-reports-billable-apis.md)。

## 查看事務報告日誌 {#view-transaction-reporting-logs}

交易報表會將報表中顯示的所有資訊以及記錄檔中的某些其他資訊。 記錄檔中提供的資訊對進階使用者有幫助。 例如，記錄檔將交易分為多個細分類別，與報表中顯示的三個統一類別比較。 記錄檔位於/crx-quickstart/logs/aem-forms-transaction.log。

## 相關文章 {#related-articles}

* [事務處理報表概覽](../../forms/using/transaction-reports-overview.md)
* [事務處理報表可開單API](../../forms/using/transaction-reports-billable-apis.md)
* [記錄自訂實作的交易](/help/forms/using/record-transaction-custom-implementation.md)

