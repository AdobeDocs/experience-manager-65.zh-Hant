---
title: 部署社群
seo-title: 部署社群
description: 如何部署AEM Communities
seo-description: 如何部署AEM Communities
uuid: 18d9b424-004d-43b2-968a-318e27a93759
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: c8d7355f-5a70-40d1-bf22-62fab8002ea0
docset: aem65
translation-type: tm+mt
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---


# 部署社群{#deploying-communities}

## 必備條件 {#prerequisites}

* [AEM 6.5平台](/help/sites-deploying/deploy.md)

* AEM Communities授權

* 適用於：

   * [Adobe Analytics for Communities功能](/help/communities/analytics.md)
   * [MSRP專用的MongoDB](/help/communities/msrp.md)
   * [適用於ASRP的Adobe Cloud](/help/communities/asrp.md)

## 安裝檢查清單 {#installation-checklist}

**適用於[AEM平台](/help/sites-deploying/deploy.md#what-is-aem)**

* 安裝最新 [的AEM 6.5更新](#aem64updates)

* 如果不使用預設埠(4502、4503)，則配置 [複製代理](#replication-agents-on-author)
* [複製加密密鑰](#replicate-the-crypto-key)
* 如果支援全球化， [請設定自動翻譯](/help/sites-administering/translation.md)（提供示例設定以用於開發）

**針對社[群功能](/help/communities/overview.md)**

* 如果部署發 [布群](/help/sites-deploying/recommended-deploys.md#tarmk-farm), [請識別主要發佈者](#primary-publisher)

* [啟用隧道服務](#tunnel-service-on-author)
* [啟用社交登入](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [設定Adobe Analytics](/help/communities/analytics.md)
* 設定預設 [電子郵件服務](/help/communities/email.md)
* 識別共用 [UGC儲存](/help/communities/working-with-srp.md) (**SRP**)的選擇

   * 如果MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [安裝和配置MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [配置Solr](/help/communities/solr.md)
      * [選擇MSRP](/help/communities/srp-config.md)
   * 如果關係資料庫SRP [(DSRP)](/help/communities/dsrp.md)

      * [安裝MySQL的JDBC驅動程式](#jdbc-driver-for-mysql)
      * [安裝和配置MySQL for DSRP](/help/communities/dsrp-mysql.md)
      * [配置Solr](/help/communities/solr.md)
      * [選擇DSRP](/help/communities/srp-config.md)
   * 如果Adobe SRP [(ASRP)](/help/communities/asrp.md)

      * 與您的帳戶代表合作進行布建
      * [選擇ASRP](/help/communities/srp-config.md)
   * 如果JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * 非共用的UGC商店：

         * UGC從未複製
         * UGC僅可在輸入AEM例項或叢集上顯示
      * 預設值為JSRP
   針對啟 **[用功能](/help/communities/overview.md#enablement-community)**

   * [安裝和配置FFmpeg](/help/communities/ffmpeg.md)
   * [安裝MySQL的JDBC驅動程式](#jdbc-driver-for-mysql)
   * [安裝AEM Communities SCORM-Engine](#scorm-package)
   * [安裝和配置MySQL以啟用](/help/communities/mysql.md)






## 最新版本 {#latest-releases}

AEM 6.5 Communities GA隨附Communities套件。 若要瞭解AEM 6.5 [Communities的更新](/help/release-notes/release-notes.md#experiencemanagercommunities)，請 [參閱AEM 6.5發行說明](/help/release-notes/release-notes.md#communities-release-notes.html)。

### AEM 6.5更新 {#aem-updates}

從AEM 6.4開始，「社群」的更新會以AEM Cumulative Fix Pack和Service Pack的一部份提供。

如需AEM 6.5的最新更新，請參閱 [Adobe Experience Manager 6.4 Cumulative Fix Packs和Service Packs](https://helpx.adobe.com/experience-manager/aem-releases-updates.html)。

### 版本記錄 {#version-history}

和AEM 6.4及更新版本一樣，AEM Communities功能和修補程式是AEM Communities累積修補程式套件和服務套件的一部分。 因此，沒有單獨的功能套件。

### MySQL的JDBC驅動程式 {#jdbc-driver-for-mysql}

兩個社區功能使用MySQL資料庫：

* 若要 [啟用](/help/communities/enablement.md) :錄制SCORM活動和學員
* 針對 [DSRP](/help/communities/dsrp.md) :儲存使用者產生的內容(UGC)

MySQL連接器必須單獨獲得和安裝。

必要的步驟有：

1. 從https://dev.mysql.com/downloads/connector/j/下載ZIP封 [存](https://dev.mysql.com/downloads/connector/j/)

   * 版本必須>= 5.1.38

1. 從存檔檔案中提取mysql-connector-java-&lt;version>-bin.jar(bundle)
1. 使用Web主控台安裝並啟動套件：

   * 例如，https://localhost:4502/system/console/bundles
   * 選取 **`Install/Update`**
   * 瀏覽……若要選取從下載的ZIP封存解壓縮的套件
   * 檢查 *Oracle Corporation的MySQLcom.mysql.jdbc* JDBC驅動程式是否處於活動狀態，如果沒有，則啟動它（或檢查日誌）

1. 如果在配置JDBC後在現有部署上安裝，則通過從Web控制台中保存JDBC配置，將JDBC重新綁定到新連接器：

   * 例如，https://localhost:4502/system/console/configMgr
   * 找到配 `Day Commons JDBC Connections Pool` 置
   * 選擇以開啟
   * 選取 `Save`

1. 對所有作者和發佈例項重複步驟3和4

有關安裝捆綁的詳細資訊，請參閱「 [Web控制台](/help/sites-deploying/web-console.md) 」頁。

#### 範例：已安裝MySQL連接器包 {#example-installed-mysql-connector-bundle}

![](/help/communities/assets/chlimage_1-125.png)

### SCORM套件 {#scorm-package}

可分享的內容物件參考模型(SCORM)是數位學習的標準與規格集合。 SCORM也定義如何將內容封裝在可轉讓的ZIP檔案中。

AEM Communities SCORM引擎是啟用功能的必 [要](/help/communities/overview.md#enablement-community) 。 AEM 6.5 Communities支援的Scorm套件：

* [cq-social-scorm-package,2.3.7版](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) ，包含 [SCORM 2017.1引擎](https://rusticisoftware.com/blog/scorm-engine-2017-released/) 。

**安裝SCORM套件**

1. 從「 [Package Share」（套件共用）安裝2.3.7版的cq-social-scorm](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) -package。
1. 從cq `/libs/social/config/scorm/database_scormengine_data.sql` 實例下載並在mysql伺服器中執行該實例，以建立升級的scormEngineDB模式。
1. 在發 `/content/communities/scorm/RecordResults` 布者的CSRF篩選器中新增「排除的路徑」 `https://<hostname>:<port>/system/console/configMgr` 屬性。


#### SCORM記錄 {#scorm-logging}

在安裝後，所有啟用活動都會詳盡記錄到系統控制台。

如果需要，可將包的日誌級別設定為WARN `RusticiSoftware.*` 。

有關使用日誌的資訊，請參 [閱使用審計記錄和日誌檔案](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)。

### AEM Advanced MLS {#aem-advanced-mls}

若要支援進階多語言搜尋(MLS)的SRP集合（MSRP或DSRP），除了自訂架構和Solr組態外，還需要新的Solr外掛程式。 所有必要項目都封裝在可下載的zip檔案中。

進階MLS下載（也稱為&#39;phasetwo&#39;）可從Adobe儲存庫取得：

* [AEM-SOLR-MLS-phasetwo](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/tat/AEM-SOLR-MLS-phasetwo/1.2.40/)

   * 版本1.2.40,2016年4月6日
   * 下載AEM-SOLR-MLS-phasetwo-1.2.40.zip

如需詳細資訊和安裝資訊，請造 [訪SRP的Solr Configuration](/help/communities/solr.md) 。

### 關於包共用的連結 {#about-links-to-package-share}

**Adobe AEM Cloud中可見的套件**

此頁面上的封裝連結不需要執行AEM例項，因為它們要在上共用 `adobeaemcloud.com`。 雖然可檢視套件， `Install` 但按鈕是用來將套件安裝至Adobe代管網站。 如果想要安裝在本機AEM例項上，選取 `Install` 將會產生錯誤。

**如何安裝在本機AEM例項**

若要安裝本機AEM例 `adobeaemcloud.com` 項中可見的套件，必須先將套件下載至本機磁碟：

* 選取「資 **產** 」標籤
* 選擇 **下載到磁碟**

在本機AEM例項上，使用套件管理器(例如 [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/))，以上傳至本機AEM的套件儲存庫。

或者，從本機AEM例項(例如 [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/))使用套件共用來存取套件， `Download` 按鈕會下載至本機AEM例項的套件儲存庫。

在本機AEM例項的套件儲存庫中，使用套件管理器安裝套件。

如需詳細資訊，請 [造訪How to Work With Packages](/help/sites-administering/package-manager.md#package-share)。

## 建議的部署 {#recommended-deployments}

在AEM Communities中，共用商店用來儲存使用者產生的內容(UGC)，通常稱為儲 [存資源提供者(SRP)](/help/communities/working-with-srp.md)。 建議的部署中心是為公用商店選擇SRP選項。

通用商店支援在發佈環境中協調和分析UGC，同時不需要復 [制](/help/communities/sync.md) UGC。

* [社群內容商店](/help/communities/working-with-srp.md) :討論AEM社群的SRP儲存選項

* [建議的拓撲](/help/communities/topologies.md) :根據使用案例和SRP選擇討論要使用的拓撲

## 升級 {#upgrading}

從舊版AEM升級至AEM 6.5平台時，請務必閱讀「 [Upgrading to AEM 6.5」](/help/sites-deploying/upgrade.md)。

除了升級平台外，請閱讀「 [升級至AEM Communities 6.5](/help/communities/upgrade.md) 」以瞭解「社群」變更。

## 設定 {#configurations}

### 主要發行者 {#primary-publisher}

當選擇的部署是發 [布場](/help/communities/topologies.md#tarmk-publish-farm)，則必須將一個AEM發佈例項識別為不應發生在所有例項的活動，例如依賴通知或 **`primary publisher`** Adobe Analytics的功能 ********。

預設情況下， `AEM Communities Publisher Configuration` OSGi配置配置中選中了該複選框， **`Primary Publisher`** 這樣發佈群中的所有發佈實例都將自標識為主實例。

因此，必須編輯所有 **次要發佈例項的配置** ，以取消勾選 **`Primary Publisher`** 核取方塊。

![](/help/communities/assets/chlimage_1-126.png)

對於發佈群中的所有其他（次要）發佈例項：

* 具有管理員權限的登入
* 存取網 [路主控台](/help/sites-deploying/configuring-osgi.md)

   * 例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* 找到 `AEM Communities Publisher Configuration`
* 選取編輯圖示
* 取消選中「主 **要發佈者** 」框
* 選擇保 **存**

### 作者上的複製代理 {#replication-agents-on-author}

複製用於在發佈環境中建立的站點內容，如社區組，以及使用隧道服務從作者環境管理成員和成 [員組](#tunnel-service-on-author)。

對於主發佈者，請確保「復 [制代理配置](/help/sites-deploying/replication.md) 」正確標識發佈伺服器和授權用戶。 預設的授權使 `admin,` 用者已擁有適當的權限(為 `Communities Administrators`成員)。

為了讓某些其他使用者擁有適當的權限，他們必須新增為使用者群 `administrators` 組(也是使用者的成 `Communities Administrators`員)。

作者環境中有兩個複製代理需要正確配置傳輸配置。

* 在作者上訪問複製控制台

   * 從全域導覽，導覽至「 **[UIControl工具>部署>複製>作者代理」]**

* 對於兩個代理，請遵循相同的流程：

   * **預設代理（發佈）**
   * **反向複製代理（發佈反向）**

      1. 選擇代理
      1. 選擇編 **輯**
      1. 選擇「傳 **輸** 」頁籤
      1. 如果不是端 `4503`口，請編輯 **URI** ，以指定正確的埠

      1. 如果不是用 `admin`戶，請編輯 **用戶和** 密碼 **，以指定用戶組**`administrators` 的成員

以下影像顯示將埠從4503更改為6103的結果：

#### 預設代理（發佈） {#default-agent-publish}

![](/help/communities/assets/chlimage_1-127.png)

#### 反向複製代理（發佈反向） {#reverse-replication-agent-publish-reverse}

![](/help/communities/assets/chlimage_1-128.png)

### 作者的隧道服務 {#tunnel-service-on-author}

當使用作者環境 [建立網站](/help/communities/sites-console.md)、修改網站屬性 [](/help/communities/sites-console.md#modifying-site-properties) 或管理社群成員時 [](/help/communities/members.md)，必須存取在發佈環境中註冊的成員（使用者），而非在作者上註冊的使用者。

隧道服務使用作者上的複製代理提供此訪問。

要啟用隧道服務：

* 論作 **者**
* 使用管理權限登入
* 如果發佈者不是localhost:4503或傳輸用戶不是， `admin`則 [配置複製代理](#replication-agents-on-author)

* 存取 [Web Console](/help/sites-deploying/configuring-osgi.md)

   * 例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* 找到 `AEM Communities Publish Tunnel Service`
* 選取編輯圖示
* 勾選「 **啟用** 」方塊
* 選擇保 **存**

![](/help/communities/assets/chlimage_1-129.png)

### 複製加密密鑰 {#replicate-the-crypto-key}

AEM Communities有兩項功能，需要所有AEM伺服器執行個體使用相同的加密金鑰。 這些是 [Analytics](/help/communities/analytics.md) 和 [ASRP](/help/communities/asrp.md)。

自AEM 6.3起，關鍵資料會儲存在檔案系統中，而不會再儲存在儲存庫中。

為了將關鍵材料從作者複製到所有其他實例，必須：

* 存取AEM例項（通常為作者例項），其中包含要複製的關鍵材料

   * 在本機檔 `com.adobe.granite.crypto.file` 案系統中尋找包，例如，

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * 檔 `bundle.info` 案會識別套件
   * 導覽至資料夾，例如

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * 複製hmac和主檔案



* 針對每個目標AEM例項

   * 導覽至資料夾，例如

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * 貼上先前複製的2個檔案
   * 如果目標AEM實 [例當前正在運行](#refresh-the-granite-crypto-bundle) ，則需要刷新Granite Crypto包


>[!CAUTION]
>
>如果已經配置了基於加密密鑰的其他安全功能，則複製加密密鑰可能會損壞配置。 如需協助，請 [聯絡客戶服務](https://helpx.adobe.com/marketing-cloud/contact-support.html)。

#### 儲存庫複製 {#repository-replication}

如同AEM 6.2及舊版軟體一樣，將關鍵資料儲存在儲存庫中，可在每個AEM例項的首次啟動時指定下列系統屬性（會建立初始儲存庫），以保留它：

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>請務必驗證作者上的復 [制代理是否正確](#replication-agents-on-author) 配置。

在儲存庫中儲存密鑰材料後，將加密密鑰從作者複製到其他實例的方式如下：

使用 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) :

* 瀏覽 [至https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* 選取 `/etc/key`
* 開啟標 `Replication` 簽
* 選取 `Replicate`

* [刷新Granite加密包](#refresh-the-granite-crypto-bundle)

![](/help/communities/assets/chlimage_1-130.png)

#### 刷新Granite加密包 {#refresh-the-granite-crypto-bundle}

* 在每個發佈例項上，存取 [Web Console](/help/sites-deploying/configuring-osgi.md)

   * 例如， [https://&lt;server>:&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* 找 `Adobe Granite Crypto Support` 到包(com.adobe.granite.crypto)
* 選擇「刷 **新」**

![](/help/communities/assets/chlimage_1-131.png)

* 稍後，應會出現「 **成功** 」對話方塊：
   `Operation completed successfully.`

### Apache HTTP Server {#apache-http-server}

如果使用Apache HTTP伺服器，請確保對所有相關條目使用正確的伺服器名稱。

請特別留意使用正確的伺服器名稱，而非 `localhost`在中 `RedirectMatch`。

#### httpd.conf示例 {#httpd-conf-sample}

```shell
<IfModule alias_module>
     # XAMPP does not have a favicon; this prevents any 404 errors which may arise.
     Redirect 404 /favicon.ico
     <Location /favicon.ico>
         ErrorDocument 404 "No favicon"
     </Location>

    # Return from "Sign Out" generates response header directing you to "/", generating a 404 error
    # The RedirectMatch resolves it correctly when modified for the target Community Site :
    RedirectMatch ^/$ https://[server name]/content/sites/engage/en.html
 ...
 </IfModule>
```

### Dispatcher {#dispatcher}

如果使用Dispatcher，請參閱：

* AEM的 [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) documentation
* [安裝 Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [配置Dispatcher for Communities](/help/communities/dispatcher.md)
* [已知問題](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## 相關社群檔案 {#related-communities-documentation}

* 請造 [訪管理社群網站](/help/communities/administer-landing.md) ，以瞭解如何建立社群網站、設定社群網站範本、協調社群內容、管理成員以及設定訊息。

* 請造 [訪開發社群](/help/communities/communities.md) ，以瞭解社交元件架構(SCF)及自訂社群元件與功能。

* 請造 [訪編寫社群元件](/help/communities/author-communities.md) ，以瞭解如何使用和設定社群元件。

