---
title: 升級後檢查和疑難排解
seo-title: 升級後檢查和疑難排解
description: 瞭解如何疑難排解升級後可能出現的問題。
seo-description: 瞭解如何疑難排解升級後可能出現的問題。
uuid: 3f525f2c-8d25-4bb8-a57e-3adf667edde8
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 5a67aa9f-e5eb-4d7e-89da-2ee1a45eb8ce
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 升級後檢查和疑難排解{#post-upgrade-checks-and-troubleshooting}

## 升級後檢查 {#post-upgrade-checks}

在就 [地升級後](/help/sites-deploying/in-place-upgrade.md) ，應執行下列活動以完成升級。 假設AEM已從6.5 jar開始，且已部署升級的程式碼庫。

* [驗證日誌是否成功升級](#main-pars-header-290365562)

* [驗證OSGi捆綁包](#main-pars-header-1637350649)

* [驗證Oak版本](#main-pars-header-1293049773)

* [檢查PreUpgradeBackup資料夾](#main-pars-header-988995987)

* [頁面的初始驗證](#main-pars-header-20827371)
* [套用AEM Service Pack](#main-pars-header-215142387)

* [移轉AEM功能](#main-pars-header-1434457709)

* [驗證計畫維護配置](#main-pars-header-1552730183)

* [啟用複製代理](#main-pars-header-823243751)

* [啟用自訂排程工作](#main-pars-header-244535083)

* [執行測試計畫](#main-pars-header-1167972233)

### 驗證升級成功的日誌 {#verify-logs-for-upgrade-success}

**upgrade.log**

過去，檢查實例的升級後狀態需要仔細檢查各種日誌檔案、儲存庫的部分和啟動板。 產生升級後報告有助於在上線前偵測有缺陷的升級。

此功能的主要用途是減少需要手動解釋或跨多個端點執行複雜解析邏輯，以限定升級成功與否。 該解決方案旨在為外部自動化系統提供明確的資訊，以便對更新的成功或已識別的失敗做出反應。

更具體地說，它可確保：

* 升級架構偵測到的升級失敗可集中在單一升級報告中；
* 升級報告包括有關必要手動干預的指標。

為瞭解決此問題，已對檔案中生成日誌的方式進行了 `upgrade.log` 更改。

以下是範例報表，其中顯示升級期間無錯誤：

![1487887443006](assets/1487887443006.png)

以下是範例報表，顯示升級程式期間未安裝的套件：

![1487887532730](assets/1487887532730.png)

**error.log**

在使用目標版本jar啟動AEM期間和之後，應仔細檢查error.log。 應審查任何警告或錯誤。 一般而言，最好在記錄檔開頭尋找問題。 日誌中稍後發生的錯誤，實際上可能是檔案中較早調出的根本原因的副作用。 如果發生重複錯誤和警告，請參閱下 [面的升級問題分析](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-the-upgrade)。

### 驗證OSGi捆綁包 {#verify-osgi-bundles}

導覽至OSGi主控 `/system/console/bundles` 台，並查看是否未啟動任何組合。 如果有任何捆綁包處於安裝狀態，請咨詢以 `error.log` 確定根問題。

### 驗證Oak版本 {#verify-oak-version}

升級後，您應會看到Oak版本已更 **新為1.10.2**。 若要確認Oak版本，請導覽至OSGi主控台，並查看與Oak bundles相關的版本：Oak Core、Oak Commons、Oak Segment Tar。

### 檢查PreUpgradeBackup資料夾 {#inspect-preupgradebackup-folder}

在升級期間，AEM將嘗試備份自訂項目，並將它們儲存在下方 `/var/upgrade/PreUpgradeBackup/<time-stamp-of-upgrade>`。 為了在CRXDE Lite中查看此資料夾，您可能需要暫 [時啟用CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md)。

具有時間戳的資料夾應具有名為 `mergeStatus` 的值的屬性 `COMPLETED`。 要處 **理的資料夾** ，應為空白，且覆 **** 寫節點會指出在升級期間覆寫了哪些節點。 下方的內 **容** ，表示升級期間無法安全合併的內容。 如果您的實作依賴任何子節點（而且您的升級程式碼套件尚未安裝），則需要手動合併這些節點。

在本練習後，如果在「舞台(Stage)」或「生產(Production)」環境中，則禁用CRXDE Lite。

### 頁面的初始驗證 {#initial-validation-of-pages}

對AEM中的數個頁面執行初始驗證。 如果升級Author環境，請開啟「開始」頁和「歡迎」頁( `/aem/start.html`, `/libs/cq/core/content/welcome.html`)。 在「作者」和「發佈」環境中，都會開啟數個應用程式頁面，並進行煙霧測試，以便正確顯示。 如果發生任何問題，請咨詢 `error.log` 以進行故障診斷。

### 套用AEM Service Pack {#apply-aem-service-packs}

套用任何相關的AEM 6.5 Service Pack（如果已發行）。

### 移轉AEM功能 {#migrate-aem-features}

AEM中的數項功能需要升級後執行其他步驟。 您可在「升級程式碼與自訂」頁面上找到這些功能和在AEM 6.5中移轉 [的步驟](/help/sites-deploying/upgrading-code-and-customizations.md) 。

### 驗證計畫維護配置 {#verify-scheduled-maintenance-configurations}

#### Enable Data Store Garbage Collection {#enable-data-store-garbage-collection}

如果使用File Data Store，請確定已啟用Data Store Garbage Collection任務並將其添加到Weekly Maintenance清單。 此處說明 [說明](/help/sites-administering/data-store-garbage-collection.md)。

>[!NOTE]
>
>S3自訂資料存放區安裝或使用共用資料存放區時，不建議使用此功能。

#### 啟用線上修訂清除 {#enable-online-revision-cleanup}

如果使用MongoMK或新的TarMK區段格式，請確定已啟用「修訂清除」工作並新增至「每日維護」清單。 此處說明 [的說明](/help/sites-deploying/revision-cleanup.md)。

### 執行測試計畫 {#execute-test-plan}

根據「測試過程」部分下定義的「 [升級代碼和自定義](/help/sites-deploying/upgrading-code-and-customizations.md) 」執行 **詳細的測試計畫** 。

### 啟用複製代理 {#enable-replication-agents}

發佈環境完全升級並經過驗證後，在「作者環境」上啟用複製代理。 驗證代理是否能夠連接到相應的發佈實例。 如需事件順 [序的詳細資訊](/help/sites-deploying/upgrade-procedure.md) ，請參閱升級程式。

### 啟用自訂排程工作 {#enable-custom-scheduled-jobs}

此時，任何作為代碼庫一部分的計畫作業都可以啟用。

## 分析升級問題 {#analyzing-issues-with-upgrade}

本節包含AEM 6.3升級程式中可能遇到的問題案例。

這些案例應有助於追蹤升級相關問題的根本原因，並有助於識別專案或產品特定問題。

### 儲存庫遷移失敗 {#repository-migration-failing-}

從CRX2到Oak的資料移轉，對於任何以CQ 5.4為基礎的Source Instances開始的情形都可行。請務必確實遵照本文檔中的升級說明（包括準備） `repository.xml`，確保沒有通過JAAS啟動自定義驗證器，並且在開始遷移之前已檢查實例是否不一致。

如果遷移仍然失敗，您可以通過檢查來找出根本原因 `upgrade.log`。 如果尚未知道問題，請向客戶支援報告。

### 升級未運行 {#the-upgrade-did-not-run}

在開始準備步驟之前，請務必使用java -jar aem-quickstart.jar命令 **先執行source** instance。 為確保快速啟動。properties檔案正確生成，必須執行此操作。 如果缺少，升級將無法運作。 或者，您也可以查看源實例的安裝資料夾 `crx-quickstart/conf` 下的位置，檢查檔案是否存在。 此外，當啟動AEM以開始升級時，必須使用java -jar aem-quickstart.jar命令來執行它。 從開始指令碼開始時，不會在升級模式中啟動AEM。

### 包和包無法更新 {#packages-and-bundles-fail-to-update-}

如果在升級期間無法安裝套件，則其所包含的套件也不會更新。 此類問題通常是由資料存放區配置錯誤所造成。 它們也會在 **error** .log中顯 **示為ERROR** 和WARN消息。 由於在大多數情況下預設登錄可能無法運行，因此您可以直接使用CRXDE來檢查和查找配置問題。

### 某些AEM Bundles未切換至作用中狀態 {#some-aem-bundles-are-not-switching-to-the-active-state}

如果捆綁包未啟動，則應檢查是否存在任何未滿足的從屬關係。

如果出現此問題，但是它基於失敗的軟體包安裝，導致軟體包無法升級，它們將被視為與新版本不相容。 如需如何疑難排解此問題的詳細資訊，請參 **閱上述的Packages and Bundles Fail to Update** 。

此外，建議您比較最新AEM 6.5執行個體的套件清單與升級的執行個體，以偵測未升級的套件。 這將提供更詳細的搜尋範圍 `error.log`。

### 自訂組合不切換至作用中狀態 {#custom-bundles-not-switching-to-the-active-state}

如果您的自訂搭售未切換至作用中狀態，則很可能有程式碼未匯入變更API。 這通常會導致不滿足要求的從屬關係。

已移除的API應在先前的某個版本中標示為已過時。 您可能會在此取代通知中找到有關直接轉換程式碼的指示。 Adobe的目標是盡可能進行語義版本修訂，讓版本能夠指示變更的中斷。

此外，最好檢查是否絕對需要導致問題的更改，如果不需要，請進行恢復。 此外，在嚴格的語義版本修訂後，檢查軟體包導出的版本增加是否超出必要。

### 故障平台UI {#malfunctioning-platform-ui}

如果某些UI功能在升級後無法正常運作，您應先檢查介面的自訂覆蓋。 某些結構可能已變更，而覆蓋可能需要更新或已過時。

接著，檢查是否有任何Javascript錯誤，這些錯誤可追蹤至自訂新增的擴充功能，這些擴充功能會連結至用戶端程式庫。 自訂CSS也會套用相同的功能，這可能會對AEM版面造成問題。

最後，檢查Javascript可能無法處理的設定錯誤。 通常情況下，副檔名會不當停用。

### 故障自訂元件、範本或UI擴充功能 {#malfunctioning-custom-components-templates-or-ui-extensions}

在大多數情況下，這些問題的根本原因與未啟動的捆綁包或未安裝的軟體包的根本原因相同，但問題在首次使用元件時開始出現的唯一差異。

處理錯誤自訂程式碼的方法是先進行煙霧測試，以找出原因。 找到後，請查看文章此連結區 [段中] ，以取得修正建議的方式。

### /etc下缺少自定義 {#missing-customizations-under-etc}

`/apps` 並且 `/libs` 由升級處理得當，但升級後 `/etc` 可能需要手動還原下的 `/var/upgrade/PreUpgradeBackup` 變更。 請務必檢查此位置是否有需要手動合併的任何內容。

### 分析error.log和upgrade.log {#analyzing-the-error.log-and-upgrade.log}

在大多數情況下，需要查閱記錄檔以找出問題的原因。 但是，在升級時，也需要監視相關性問題，因為舊捆綁包可能無法正確升級。

執行此操作的最佳方式是移除所有預期與您所面對之問題無關的訊息，以刪除error.log。 您可以透過像grep這樣的工具，使用：

```shell
grep -v UnrelatedErrorString
```

有些錯誤訊息可能無法立即解釋。 在這種情況下，查看發生錯誤的上下文也有助於瞭解錯誤的建立位置。 您可以使用下列項目來分隔錯誤：

* `grep -B` 在錯誤前添加行；

或

* `grep -A` ，以在後面添加行。

在少數情況下，也可以找到WARN訊息，因為可能存在導致此狀態的有效案例，而應用程式不一定能判斷這是否為實際錯誤。 請確定您也參考這些訊息。

### 聯絡Adobe支援 {#contacting-adobe-support}

如果您已閱讀本頁的建議，但仍有問題，請聯絡Adobe支援。 為了盡可能向負責您案例的支援工程師提供更多資訊，請確保包含升級的upgrade.log檔案。
