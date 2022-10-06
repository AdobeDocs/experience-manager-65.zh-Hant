---
title: 查看和了解交易報告
seo-title: Viewing and Understanding Transaction Reports
description: 使用交易報告就產品使用情況做出明智決策，並重新平衡對硬體和軟體的投資。
seo-description: Use transaction reports to make an informed decision about the product usage and rebalancing investments in hardware and software.
uuid: 56d9f01d-4778-47c9-bbb2-6650a73a3f59
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c04c488b-73f3-49ba-9e89-f97497965757
docset: aem65
exl-id: 3c7cbe1f-ac81-4df9-96b2-662cbc5f2075
source-git-commit: 75e1697c301dca3a649833a45caa1753fdc81514
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 0%

---

# 查看和了解交易報告{#viewing-and-understanding-transaction-reports}

交易報表可讓您擷取及追蹤已提交的表單、已處理的檔案及已轉譯的檔案數量。 跟蹤這些交易的目標是就產品使用情況做出明智的決策，並重新平衡對硬體和軟體的投資。 如需詳細資訊，請參閱 [AEM Forms交易報表概述](../../forms/using/transaction-reports-overview.md).

## 設定交易報表  {#setting-up-transaction-reports}

AEM Forms附加套件提供交易報表功能。 如需在所有製作和發佈執行個體上安裝附加套件的相關資訊，請參閱 [安裝和設定AEM表單](/help/forms/using/installing-configuring-aem-forms-osgi.md). 安裝AEM Forms附加元件套件後，請執行下列作業：

* 在所有發佈執行個體上啟用反向復寫
* 啟用交易報表
* 提供查看交易報告的權限
* （可選）配置事務處理刷新期間和發件箱 [](/help/forms/using/installing-configuring-aem-forms-osgi.md)

>[!NOTE]
>
>* AEM Forms交易報表不支援僅包含發佈例項的拓撲。
>* 使用交易報表之前，請確定已對所有發佈執行個體啟用反向復寫。
>* 交易資料會從發佈例項反向複製至僅對應的製作或處理例項。 製作或處理例項無法進一步將資料複製至其他例項。
>


### 在所有發佈執行個體上啟用反向復寫 {#enable-reverse-replication-on-all-the-publish-instances}

交易報表使用反向復寫來合併從發佈實例到製作實例的交易計數。 在所有發佈執行個體上設定反向復寫。 有關設定反向複製的詳細說明，請參見 [複製](/help/sites-deploying/replication.md).

### 啟用交易報表 {#enable-transaction-reports}

交易報表預設為停用。 您可以從AEM Web Console啟用報表。 若要在AEM Forms環境中啟用交易報表，請對所有製作和發佈例項執行下列步驟：

1. 以管理員身分登入AEM執行個體。 前往 **工具** > **操作** > **Web主控台**.
1. 找出並開啟 **Forms Transaction Reporting** 服務。
1. 選擇「記錄事務處理」複選框。 按一下「**儲存**」。

   在所有製作和發佈例項上重複步驟1至3。

### 提供查看交易報告的權限 {#provide-rights-to-view-a-transaction-report}

只有fd-administrator組的成員才能查看事務報告。 要允許用戶查看事務報告，請使用戶成為fd-administrator組的成員。 如需讓使用者成為AEM群組的成員的相關指示，請參閱 [使用者、群組和存取權限管理](/help/sites-administering/user-group-ac-admin.md).

### （可選）配置事務處理刷新期間和發件箱 {#optional-configure-transaction-flush-period-and-outboxes}

事務在儲存在儲存庫中之前先快取在記憶體中。 此程式會依循，以確保不會經常寫入存放庫。 預設情況下，快取期間（事務刷新期間）設定為60秒。 您可以變更預設期間以符合您的環境。 執行下列步驟以變更預設的快取期間：

1. 以管理員身分登入製作執行個體。 前往 **工具** > **操作** > **Web主控台**.
1. 找出並開啟 **Forms交易存放庫儲存提供者** 服務。
1. 指定 **事務處理刷新期間** 欄位。 按一下「**儲存**」。

反向復寫會將交易資料複製到製作執行個體的預設寄件匣。 您可以將交易資料放入自訂寄件匣中。 執行下列步驟以指定自訂寄件匣：

1. 以管理員身分登入製作執行個體。 前往 **工具** > **操作** > **Web主控台**.
1. 找出並開啟 **Forms交易存放庫儲存提供者** 服務。
1. 指定自訂寄件匣的名稱 **出貨箱** 欄位。 按一下「**儲存**」。所有製作執行個體上都會建立具有指定名稱的輸出方塊。

## 查看交易報表 {#viewing-the-transaction-report}

您可以檢視製作或發佈例項的交易報表。 製作例項的交易報表可提供已設定製作和發佈例項上發生的所有交易的匯總。 發佈例項的交易報表提供僅在基礎發佈例項發生的交易計數。 執行下列步驟來檢視報表：

1. 登入AEM Forms伺服器，位置為 `https://[hostname]:'port'`.
1. 導覽至 **工具** > **Forms**>**查看交易報表**.

## 了解報表 {#understanding-the-report}

AEM Forms會顯示自設定日期以來的交易報表，如下列摘要報表所示：

![sample-transaction-report-author](assets/sample-transaction-report-author.png)

* 使用 **將日期重設為今天** 重置交易記錄的選項。 將日期重置為今天時，將丟失所有以前的交易記錄。 當您重設製作例項的日期時，變更不會影響發佈例項的交易報表，反之也不會影響。
* 使用 **僅顯示發佈實例的事務** 檢視僅在已設定的發佈執行個體或發佈伺服器陣列上發生的所有交易。
* 使用類別： **已處理的文檔**, **已呈現的文檔**，和 **Forms已提交** 查看相應的事務。 有關這些類別中記錄的事務處理類型，請參閱 [計費交易報表API](../../forms/using/transaction-reports-billable-apis.md).

## 查看事務報告日誌 {#view-transaction-reporting-logs}

交易報表會將報表中顯示的所有資訊和記錄中的其他一些資訊置於報表中。 記錄檔中提供的資訊對進階使用者很有幫助。 例如，記錄檔會將交易劃分為多個精細類別，而報告中顯示的三個統一類別則不同。 記錄檔可在 `error.log` 檔案 `/crx-repository/logs/` 目錄。 即使您未從AEM Web Console啟用交易報表，記錄仍可供使用。

## 相關文章 {#related-articles}

* [交易報表概述](../../forms/using/transaction-reports-overview.md)
* [交易報表計費API](../../forms/using/transaction-reports-billable-apis.md)
* [記錄自訂實施的交易](/help/forms/using/record-transaction-custom-implementation.md)
