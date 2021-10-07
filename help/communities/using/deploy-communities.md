---
title: 部署社群
seo-title: Deploying Communities
description: 如何部署AEM Communities
seo-description: How to deploy AEM Communities
content-type: reference
topic-tags: deploying
source-git-commit: 14a33b14043869614efcdbf8cb413333d0fa644b
workflow-type: tm+mt
source-wordcount: '1881'
ht-degree: 1%

---


# 部署社群{#deploying-communities}

## 必備條件 {#prerequisites}

* [AEM 6.5平台](/help/sites-deploying/deploy.md)

* AEM Communities授權

* 可選許可：

   * [Adobe Analytics for Communities功能](/help/communities/analytics.md)
   * [MSRP適用的MongoDB](/help/communities/msrp.md)
   * [適用於ASRP的Adobe雲](/help/communities/asrp.md)

## 安裝檢查清單 {#installation-checklist}

**針對 [AEM平台](/help/sites-deploying/deploy.md#what-is-aem)**:

* 安裝最新的[AEM 6.5更新](#aem64updates)。

* 如果未使用預設埠(4502, 4503)，則[配置複製代理](#replication-agents-on-author)。
* [複製加密密鑰](#replicate-the-crypto-key)
* 如果支援全球化，請[設定自動翻譯](/help/sites-administering/translation.md)
（提供開發用的範例設定）。

**針對「社 [群」功能](/help/communities/overview.md)**:

* 如果部署[publish farm](/help/sites-deploying/recommended-deploys.md#tarmk-farm),[將標識主發佈伺服器](#primary-publisher)

* [啟用通道服務](#tunnel-service-on-author)
* [啟用社交登入](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [設定Adobe Analytics](/help/communities/analytics.md)
* 設定[預設電子郵件服務](/help/communities/email.md)
* 確定[共用UGC儲存的選擇](/help/communities/working-with-srp.md)(**SRP**)

   * 如果MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [安裝和配置MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [配置Solr](/help/communities/solr.md)
      * [選擇MSRP](/help/communities/srp-config.md)
   * 如果關係資料庫SRP [(DSRP)](/help/communities/dsrp.md)

      * [安裝MySQL的JDBC驅動程式](#jdbc-driver-for-mysql)
      * [安裝和配置DSRP適用的MySQL](/help/communities/dsrp-mysql.md)
      * [配置Solr](/help/communities/solr.md)
      * [選擇DSRP](/help/communities/srp-config.md)
   * 如果AdobeSRP [(ASRP)](/help/communities/asrp.md)

      * 與您的帳戶代表合作以進行布建。
      * [選擇ASRP](/help/communities/srp-config.md)
   * 如果JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * 不是共用UGC儲存：

         * UGC從未複製。
         * UGC只會顯示在輸入UGC的AEM例項或叢集上。
      * 預設為JSRP

   針對&#x200B;**[啟用功能](/help/communities/overview.md#enablement-community)**

   * [安裝和配置FFmpeg](/help/communities/ffmpeg.md)
   * [安裝MySQL的JDBC驅動程式](#jdbc-driver-for-mysql)
   * [安裝AEM Communities SCORM引擎](#scorm-package)
   * [安裝並配置MySQL以啟用](/help/communities/mysql.md)






## 最新發行 {#latest-releases}

AEM 6.5 Communities GA包含Communities套件。 若要了解AEM 6.5 [Communities](/help/release-notes/release-notes.md#experiencemanagercommunities)的更新，請參閱[AEM 6.5發行說明](/help/release-notes/release-notes.md#communities-release-notes.html)。

### AEM 6.5更新 {#aem-updates}

自AEM 6.4開始，Communities的更新會隨AEM Cumulative Fix Pack和Service Pack一併提供。

如需AEM 6.5的最新更新，請參閱[Adobe Experience Manager 6.4 Cumulative Fix Pack和Service Pack](https://helpx.adobe.com/tw/experience-manager/aem-releases-updates.html)。

### 版本記錄 {#version-history}

與AEM 6.4及更新版本一樣，AEM Communities功能和Hotfix是AEM Communities Cumulative Fix Pack和Service Pack的一部分。 因此，沒有單獨的功能套件。

### MySQL的JDBC驅動程式 {#jdbc-driver-for-mysql}

兩個Communities功能使用MySQL資料庫：

* 對於[啟用](/help/communities/enablement.md):記錄SCORM活動和學習者
* 對於[DSRP](/help/communities/dsrp.md):儲存用戶生成的內容(UGC)

必須單獨獲得並安裝MySQL連接器。

必要步驟為：

1. 從[https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)下載ZIP封存

   * 版本必須>= 5.1.38

1. 提取 `mysql-connector-java-&lt;version&gt;-bin.jar (bundle) from the archive`
1. 使用Web主控台來安裝和啟動套件組合：

   * 例如， https://localhost:4502/system/console/bundles
   * 選取 **`Install/Update`**
   * 瀏覽……以選取從下載的ZIP封存擷取的套件組合
   * 檢查&#x200B;*Oracle公司的MySQLcom.mysql.jdbc* JDBC驅動程式是否處於活動狀態，如果未活動，則啟動它（或檢查日誌）

1. 如果在配置JDBC後在現有部署上進行安裝，則從Web控制台中重新保存JDBC配置，將JDBC重新綁定到新連接器：

   * 例如， https://localhost:4502/system/console/configMgr
   * 找到`Day Commons JDBC Connections Pool`配置並選擇以開啟配置。
   * 選取 `Save`.

1. 在所有製作和發佈執行個體上重複步驟3和4。

有關安裝套件的詳細資訊，請參見[Web控制台](/help/sites-deploying/web-console.md#bundles)頁。

#### 範例：已安裝的MySQL連接器套件組合 {#example-installed-mysql-connector-bundle}

![](../assets/mysql-connector.png)

### SCORM套件 {#scorm-package}

共用內容物件參考模型(SCORM)是數位學習的標準和規格的集合。 SCORM也定義了如何將內容封裝成可傳輸的ZIP檔案。

[enablement](/help/communities/overview.md#enablement-community)功能需要AEM Communities SCORM引擎。 AEM 6.5社群支援的Scorm套件：

* [cq-social-scorm-package,2.3.7版](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) ，包含 [SCORM 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) 引擎。

**安裝SCORM包**

1. 從「封裝共用」安裝[cq-social-scorm-package，版本2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg)
1. 從cq實例下載`/libs/social/config/scorm/database_scormengine_data.sql`並在mysql伺服器中執行該實例，以建立升級的scormEngineDB架構。
1. 從發佈者的`https://<hostname>:<port>/system/console/configMgr`，在CSRF篩選器的「排除路徑」屬性中新增`/content/communities/scorm/RecordResults`。

#### SCORM記錄 {#scorm-logging}

安裝後，所有啟用活動都會正確記錄到系統主控台。

如果需要，可將`RusticiSoftware.*`包的日誌級別設定為WARN。

有關使用日誌的資訊，請參閱[使用審計記錄和日誌檔案](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)。

### AEM進階MLS {#aem-advanced-mls}

為了支援進階多語言搜尋(MLS),SRP集合（MSRP或DSRP）除了自訂結構和Solr組態外，還需要新的Solr外掛程式。 所有必要項目都封裝成可下載的zip檔案。

您可從Adobe存放庫取得進階MLS下載（也稱為「phasetwo」）:

* [AEM-SOLR-MLS-phasetwo](https://repo1.maven.org/maven2/com/adobe/tat/AEM-SOLR-MLS-phasetwo/1.2.40/)

   * 1.2.40版，2016年4月6日
   * 下載AEM-SOLR-MLS-phasetwo-1.2.40.zip

有關詳細資訊和安裝資訊，請訪問SRP的[Solr配置](/help/communities/solr.md)。

### 關於封裝共用的連結 {#about-links-to-package-share}

**AdobeAEM Cloud中可見的套件**

此頁面上的套件連結不需要AEM的執行個體，因為它們要在`adobeaemcloud.com`上套件共用。 在可查看包時，`Install`按鈕用於將包安裝到托管Adobe的站點中。 如果想要安裝在本機AEM執行個體上，選取`Install`將會導致錯誤。

**如何在本機AEM執行個體上安裝**

若要在本機AEM執行個體上安裝顯示於`adobeaemcloud.com`的套件，必須先將套件下載至本機磁碟：

* 選取&#x200B;**Assets**&#x200B;標籤
* 選擇&#x200B;**下載到磁碟**

在本機AEM例項上，使用套件管理器(例如[https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/))，上傳至本機AEM套件存放庫。

或者，從本機AEM例項使用套件共用來存取套件(例如[https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/)), `Download`按鈕將下載至本機AEM例項的套件存放庫。

進入本機AEM例項的套件存放庫後，請使用套件管理器來安裝套件。

如需詳細資訊，請造訪[如何使用套件](/help/sites-administering/package-manager.md#package-share)。

## 建議的部署 {#recommended-deployments}

在AEM Communities中，公用存放區用於儲存使用者產生的內容(UGC)，且通常稱為[儲存資源提供者(SRP)](/help/communities/working-with-srp.md)。 建議的部署中心是為通用商店選擇SRP選項。

公用存放區支援在發佈環境中協調UGC並啟用分析，同時不需要UGC的[復寫](/help/communities/sync.md)。

* [社群內容商店](/help/communities/working-with-srp.md) :討論AEM社群的SRP儲存選項

* [建議的拓撲](/help/communities/topologies.md) :根據使用案例和SRP選擇討論要使用的拓撲

## 升級 {#upgrading}

從舊版AEM升級至AEM 6.5平台時，請務必閱讀[升級至AEM 6.5](/help/sites-deploying/upgrade.md)。

除了升級平台，請閱讀[升級至AEM Communities 6.5](/help/communities/upgrade.md)以了解Communities的變更。

## 設定 {#configurations}

### 主要發行者 {#primary-publisher}

當選擇的部署是[publish farm](/help/communities/topologies.md#tarmk-publish-farm)時，對於不應在所有例項上發生的活動(例如依賴&#x200B;**notifications**&#x200B;或&#x200B;**Adobe Analytics**&#x200B;的功能)，必須將一個AEM發佈例項識別為&#x200B;**`primary publisher`**。

預設情況下， `AEM Communities Publisher Configuration` OSGi設定會以核取的&#x200B;**`Primary Publisher`**&#x200B;核取方塊進行設定，因此發佈伺服器陣列中的所有發佈執行個體都會自行識別為主要。

因此，必須&#x200B;**編輯所有次要發佈執行個體**&#x200B;上的設定，以取消勾選&#x200B;**`Primary Publisher`**&#x200B;核取方塊。

![](../assets/primary-publisher.png)

針對發佈伺服器陣列中的所有其他（次要）發佈執行個體：

* 以管理員權限登入
* 訪問[Web控制台](/help/sites-deploying/configuring-osgi.md)

   * 例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* 找到`AEM Communities Publisher Configuration`
* 選取編輯圖示
* 取消選中&#x200B;**主發佈者**&#x200B;複選框
* 選擇&#x200B;**保存**

### 製作上的復寫代理 {#replication-agents-on-author}

復寫用於在發佈環境中建立的網站內容，例如社群群組，以及使用[tunnel service](#tunnel-service-on-author)管理製作環境中的成員和成員群組。

對於主發佈者，請確保[複製代理配置](/help/sites-deploying/replication.md)正確標識發佈伺服器和授權用戶。 預設授權用戶`admin`已具有相應權限（是`Communities Administrators`的成員）。

為了讓某些其他用戶擁有相應的權限，他們必須作為成員添加到`administrators`用戶組（也是`Communities Administrators`的成員）。

製作環境中有兩個復寫代理需要正確設定傳輸設定。

* 在作者上存取復寫主控台

   * 從全域導覽：**工具、部署、複製、作者上的代理**

* 請對兩個代理執行相同的程式：

   * **預設代理（發佈）**
   * **反向復寫代理（發佈反向）**

      1. 選擇代理。
      1. 選擇&#x200B;**edit**。
      1. 選擇&#x200B;**Transport**&#x200B;頁簽
      1. 如果沒有埠`4503`，請編輯&#x200B;**URI**&#x200B;以指定正確的埠。

      1. 如果不是用戶`admin`，請編輯&#x200B;**用戶**&#x200B;和&#x200B;**密碼**&#x200B;以指定`administrators`用戶組的成員。

下圖顯示將埠從4503更改為6103的結果：

#### 預設代理（發佈） {#default-agent-publish}

![設定限制](../assets/default-agent-publish.png)

#### 反向復寫代理（發佈反向） {#reverse-replication-agent-publish-reverse}

![](../assets/reverse-replication-agent.png)

### 作者的通道服務 {#tunnel-service-on-author}

使用製作環境建立網站[](/help/communities/sites-console.md)、[修改網站屬性](/help/communities/sites-console.md#modifying-site-properties)或[管理社群成員](/help/communities/members.md)時，必須存取在發佈環境中註冊的成員（使用者），而非在作者上註冊的使用者。

隧道服務使用製作上的復寫代理提供此存取。

啟用通道服務：

* 在&#x200B;**author**&#x200B;上，使用管理權限登入。
* 如果發佈者不是localhost:4503或傳輸使用者不是`admin`,
然後[配置複製代理](#replication-agents-on-author)。

* 訪問[Web控制台](/help/sites-deploying/configuring-osgi.md)

   * 例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* 找到`AEM Communities Publish Tunnel Service`
* 選取編輯圖示
* 選擇&#x200B;**enable**&#x200B;複選框
* 選擇&#x200B;**保存**

![](../assets/tunnel-service.png)

### 複製加密密鑰 {#replicate-the-crypto-key}

AEM Communities有兩項功能需要所有AEM伺服器執行個體使用相同的加密金鑰。 這些是[Analytics](/help/communities/analytics.md)和[ASRP](/help/communities/asrp.md)。

自AEM 6.3起，重要資料會儲存在檔案系統中，而不再儲存在存放庫中。

若要將主要資料從作者複製到所有其他執行個體，必須：

* 存取AEM例項，通常為製作例項，其中包含要複製的重要資料

   * 在本地檔案系統中找到`com.adobe.granite.crypto.file`捆綁包

      例如，

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * `bundle.info`檔案將標識包
   * 導覽至資料夾
例如，

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * 複製hmac和主節點檔案。



* 針對每個目標AEM例項

   * 導覽至資料夾
例如，

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * 貼上先前複製的2個檔案
   * 如果目標AEM例項目前執行中，則必須[重新整理Granite加密套件組合](#refresh-the-granite-crypto-bundle)。


>[!CAUTION]
>
>如果已基於加密密鑰配置了另一個安全功能，則複製加密密鑰可能會損壞配置。 如需協助，請[聯絡客戶服務](https://helpx.adobe.com/tw/marketing-cloud/contact-support.html)。

#### 存放庫復寫 {#repository-replication}

如同AEM 6.2及更舊版本一樣，將關鍵資料儲存在儲存庫中，可借由在每個AEM例項（會建立初始存放庫）首次啟動時指定下列系統屬性來保留：

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>請務必確認作者](#replication-agents-on-author)上的[復寫代理已正確設定。

將金鑰資料儲存在存放庫中，將加密金鑰從製作複製到其他執行個體的方式如下：

使用[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) :

* 瀏覽至[https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* 選取 `/etc/key`
* 開啟`Replication`標籤
* 選取 `Replicate`

* [重新整理Granite加密套件](#refresh-the-granite-crypto-bundle)

![](../assets/replicare-repository.png)

#### 重新整理Granite加密套件組合 {#refresh-the-granite-crypto-bundle}

* 在每個發佈實例上，訪問[Web控制台](/help/sites-deploying/configuring-osgi.md)

   * 例如， [https://&lt;server>:&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* 找到`Adobe Granite Crypto Support`套件組合(com.adobe.granite.crypto)
* 選擇&#x200B;**刷新**

![](../assets/refresh-granite-bundle.png)

* 稍後，應會出現&#x200B;**Success**對話方塊：
   `Operation completed successfully.`

### Apache HTTP Server {#apache-http-server}

如果使用Apache HTTP伺服器，請確保對所有相關條目使用正確的伺服器名稱。

尤其是，請務必在`RedirectMatch`中使用正確的伺服器名稱，而不是`localhost`。

#### httpd.conf範例 {#httpd-conf-sample}

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

* AEM [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)檔案
* [安裝 Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [為社群設定Dispatcher](/help/communities/dispatcher.md)
* [已知問題](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## 相關社群檔案 {#related-communities-documentation}

* 請訪問[管理社區站點](/help/communities/administer-landing.md)了解如何建立社區站點、配置社區站點模板、協調社區內容、管理成員和配置消息。

* 請造訪[開發社群](/help/communities/communities.md)以了解社交元件架構(SCF)和自訂社群元件和功能。

* 請造訪[編寫社群元件](/help/communities/author-communities.md)，了解如何使用和設定社群元件。

