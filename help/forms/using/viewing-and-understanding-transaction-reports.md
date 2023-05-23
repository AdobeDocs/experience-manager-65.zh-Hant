---
title: 查看和瞭解事務處理報表
seo-title: Viewing and Understanding Transaction Reports
description: 使用事務報告可就產品使用情況和重新平衡硬體和軟體投資作出明智決策。
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

# 查看和瞭解事務處理報表{#viewing-and-understanding-transaction-reports}

事務處理報表允許您捕獲和跟蹤已提交表單、已處理文檔和已呈現文檔的數量。 跟蹤這些交易的目的是對產品使用情況作出明智決策，並重新平衡硬體和軟體方面的投資。 有關詳細資訊，請參見 [AEM Forms事務報表概覽](../../forms/using/transaction-reports-overview.md)。

## 設定交易記錄報表  {#setting-up-transaction-reports}

事務報表功能可作為表單附AEM加程式包的一部分。 有關在所有作者和發佈實例上安裝載入項軟體包的資訊，請參見 [安裝和配置表AEM單](/help/forms/using/installing-configuring-aem-forms-osgi.md)。 安裝完表AEM單附加軟體包後，請執行以下操作：

* 在所有發佈實例上啟用反向複製
* 啟用交易記錄報告
* 提供查看交易記錄報表的權限
* （可選）配置事務處理刷新期間和發貨箱 [](/help/forms/using/installing-configuring-aem-forms-osgi.md)

>[!NOTE]
>
>* AEM Forms事務報表不支援只包含發佈實例的拓撲。
>* 在使用事務報告之前，請確保對所有發佈實例啟用反向複製。
>* 事務資料從發佈實例反向複製到僅對應的作者或處理實例。 作者或處理實例無法進一步將資料複製到另一個實例。
>


### 在所有發佈實例上啟用反向複製 {#enable-reverse-replication-on-all-the-publish-instances}

事務報表使用反向複製來合併從發佈實例到作者實例的事務計數。 在所有發佈實例上設定反向複製。 有關設定反向複製的詳細說明，請參見 [複製](/help/sites-deploying/replication.md)。

### 啟用交易記錄報告 {#enable-transaction-reports}

預設情況下禁用事務報表。 可以從Web控制台啟AEM用報告。 要在AEM Forms環境中啟用事務報表，請對所有作者和發佈實例執行以下步驟：

1. 以管理員身AEM份登錄到實例。 轉到 **工具** > **操作** > **Web控制台**。
1. 查找並開啟 **Forms交易報告** 服務。
1. 選中「記錄事務處理」複選框。 按一下「**儲存**」。

   對所有作者和發佈實例重複步驟1-3。

### 提供查看交易記錄報表的權限 {#provide-rights-to-view-a-transaction-report}

只有fd-administrator組的成員才能查看事務報表。 要允許用戶查看事務報表，請使用戶成為fd-administrator組的成員。 有關使用戶成為組成員的說AEM明，請參見 [用戶、組和訪問權限管理](/help/sites-administering/user-group-ac-admin.md)。

### （可選）配置事務處理刷新期間和發貨箱 {#optional-configure-transaction-flush-period-and-outboxes}

事務在儲存到儲存庫之前快取在記憶體中。 執行此過程可確保不會頻繁寫入儲存庫。 預設情況下，快取期間（事務刷新期間）設定為60秒。 您可以更改預設期間以適合您的環境。 執行以下步驟以更改預設的快取期：

1. 以管理員身份登錄以編寫實例。 轉到 **工具** > **操作** > **Web控制台**。
1. 查找並開啟 **Forms事務儲存庫儲存提供程式** 服務。
1. 指定 **事務處理刷新期間** 的子菜單。 按一下「**儲存**」。

反向複製將事務資料複製到作者實例的預設發件箱。 您可以將事務資料放在自定義發件箱中。 執行以下步驟以指定自定義發件箱：

1. 以管理員身份登錄以編寫實例。 轉到 **工具** > **操作** > **Web控制台**。
1. 查找並開啟 **Forms事務儲存庫儲存提供程式** 服務。
1. 指定自定義發件框的名稱 **發件箱** 的子菜單。 按一下「**儲存**」。在所有作者實例上建立具有指定名稱的發件箱。

## 查看交易記錄報表 {#viewing-the-transaction-report}

您可以查看有關作者或發佈實例的事務處理報告。 有關作者實例的事務報表提供了在配置的作者實例和發佈實例上發生的所有事務的匯總。 發佈實例上的事務報表提供僅在基礎發佈實例上發生的事務計數。 執行以下步驟查看報告：

1. 登錄AEM Forms伺服器，地址為 `https://[hostname]:'port'`。
1. 導航到 **工具** > **Forms**>**查看事務處理報表**。

## 瞭解報告 {#understanding-the-report}

AEM Forms顯示自配置日期以來的交易記錄報告，如下面的摘要報告所示：

![示例事務 — 報告 — 作者](assets/sample-transaction-report-author.png)

* 使用 **將日期重置為今天** 選項以重置交易記錄。 將日期重置為今天時，所有以前的交易記錄都將丟失。 在作者實例上重置日期時，更改不會影響發佈實例上的事務處理報告，反之也不會影響。
* 使用 **僅顯示發佈實例的事務** 查看僅在配置的發佈實例或發佈伺服器場上發生的所有事務處理。
* 使用類別： **文檔已處理**。 **已呈現的文檔**, **Forms提交** 查看相應的事務處理。 有關在這些類別中入帳的交易記錄類型，請參閱 [可開單事務報表API](../../forms/using/transaction-reports-billable-apis.md)。

## 查看事務報告日誌 {#view-transaction-reporting-logs}

事務報告會將報告中顯示的所有資訊和一些其他資訊置於日誌中。 日誌中提供的資訊對高級用戶有幫助。 例如，日誌將事務劃分為多個細分類，與報告中顯示的三個合併類別相比。 日誌在 `error.log` 檔案 `/crx-repository/logs/` 的子菜單。 即使您未從Web控制台啟用事務報告，日誌也AEM可用。

## 相關文章 {#related-articles}

* [事務處理報表概覽](../../forms/using/transaction-reports-overview.md)
* [事務處理報表可開單API](../../forms/using/transaction-reports-billable-apis.md)
* [記錄自定義實現的事務](/help/forms/using/record-transaction-custom-implementation.md)
