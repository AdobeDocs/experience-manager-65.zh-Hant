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
source-git-commit: 6693baecb1345c30385eb04caeb03960925f46c3
workflow-type: tm+mt
source-wordcount: '1898'
ht-degree: 1%

---


# 部署社區{#deploying-communities}

## 必備條件 {#prerequisites}

* [AEM 6.5平台](/help/sites-deploying/deploy.md)

* AEM Communities授權

* 適用於下列產品的可選授權：

   * [Adobe Analytics for Communities功能](/help/communities/analytics.md)
   * [MSRP專用的MongoDB](/help/communities/msrp.md)
   * [適用於ASRP的Adobe Cloud](/help/communities/asrp.md)

## 安裝檢查清單{#installation-checklist}

**適用於 [AEM平台](/help/sites-deploying/deploy.md#what-is-aem)**

* 安裝最新[AEM 6.5更新](#aem64updates)

* 如果不使用預設埠(4502、4503)，則[配置複製代理](#replication-agents-on-author)
* [複製加密密鑰](#replicate-the-crypto-key)
* 如果支援全球化，[設定自動翻譯](/help/sites-administering/translation.md)
（提供開發的範例設定）

**針對社 [群功能](/help/communities/overview.md)**

* 如果部署[publish farm](/help/sites-deploying/recommended-deploys.md#tarmk-farm),[會識別主要發佈者](#primary-publisher)

* [啟用隧道服務](#tunnel-service-on-author)
* [啟用社交登入](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [設定Adobe Analytics](/help/communities/analytics.md)
* 設定[預設電子郵件服務](/help/communities/email.md)
* 確定[共用UGC儲存](/help/communities/working-with-srp.md)(**SRP**)的選擇

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
   對於&#x200B;**[啟用功能](/help/communities/overview.md#enablement-community)**

   * [安裝和配置FFmpeg](/help/communities/ffmpeg.md)
   * [安裝MySQL的JDBC驅動程式](#jdbc-driver-for-mysql)
   * [安裝AEM Communities SCORM-Engine](#scorm-package)
   * [安裝和配置MySQL以啟用](/help/communities/mysql.md)





## 最新版本{#latest-releases}

AEM 6.5 Communities GA包含Communities套件。 若要瞭解AEM 6.5 [Communities](/help/release-notes/release-notes.md#experiencemanagercommunities)的更新，請參閱[AEM 6.5發行說明](/help/release-notes/release-notes.md#communities-release-notes.html)。

### AEM 6.5更新{#aem-updates}

從AEM 6.4開始，「社群」的更新會以AEM Cumulative Fix Pack和Service Pack的一部份提供。

如需AEM 6.5的最新更新，請參閱[Adobe Experience Manager 6.4 Cumulative Fix Pack和Service Packs](https://helpx.adobe.com/experience-manager/aem-releases-updates.html)。

### 版本歷史記錄{#version-history}

和AEM 6.4及更新版本一樣，AEM Communities功能和修補程式是AEM Communities累積修補程式套件和服務套件的一部分。 因此，沒有單獨的功能套件。

### MySQL {#jdbc-driver-for-mysql}的JDBC驅動程式

兩個社區功能使用MySQL資料庫：

* 對於[enablement](/help/communities/enablement.md):錄制SCORM活動和學員
* 對於[DSRP](/help/communities/dsrp.md):儲存使用者產生的內容(UGC)

MySQL連接器必須單獨獲得和安裝。

必要的步驟包括：

1. 從[https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)下載ZIP封存

   * 版本必須>= 5.1.38

1. 從存檔檔案中提取mysql-connector-java-&lt;version>-bin.jar(bundle)
1. 使用Web主控台安裝並啟動套件：

   * 例如，https://localhost:4502/system/console/bundles
   * 選取 **`Install/Update`**
   * 瀏覽……若要選取從下載的ZIP封存解壓縮的套件
   * 檢查&#x200B;*Oracle Corporation的MySQLcom.mysql.jdbc* JDBC驅動程式是否處於活動狀態，如果沒有，則啟動它（或檢查日誌）

1. 如果在配置JDBC後在現有部署上安裝，則通過從Web控制台中保存JDBC配置，將JDBC重新綁定到新連接器：
   * 例如，https://localhost:4502/system/console/configMgr
   * 找到`Day Commons JDBC Connections Pool`配置
   * 選擇以開啟
   * 選取 `Save`

1. 對所有作者和發佈例項重複步驟3和4

有關安裝捆綁的詳細資訊，請參見[Web控制台](/help/sites-deploying/web-console.md)頁。

#### 範例：已安裝MySQL連接器包{#example-installed-mysql-connector-bundle}

![連接器束](assets/connector-bundle.png)

### SCORM包{#scorm-package}

可分享的內容物件參考模型(SCORM)是數位學習的標準與規格集合。 SCORM也定義如何將內容封裝在可轉讓的ZIP檔案中。

[enablement](/help/communities/overview.md#enablement-community)功能需要AEM Communities SCORM引擎。 AEM 6.5 Communities支援的Scorm套件：

* [cq-social-scorm-package,2.3.7版，](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) 其中包含 [SCORM 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) 引擎。

**安裝SCORM套件**

1. 從Package Share安裝[cq-social-scorm-package 2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg)版。
1. 從cq實例下載`/libs/social/config/scorm/database_scormengine_data.sql`並在mysql伺服器中執行該實例，以建立升級的scormEngineDB模式。
1. 在發佈商的`https://<hostname>:<port>/system/console/configMgr` CSRF篩選器的「排除的路徑」屬性中新增`/content/communities/scorm/RecordResults`。


#### SCORM記錄{#scorm-logging}

在安裝後，所有啟用活動都會詳盡記錄到系統控制台。

如果需要，可將`RusticiSoftware.*`包的日誌級別設定為WARN。

有關使用日誌的資訊，請參閱[使用審計記錄和日誌檔案](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)。

### AEM Advanced MLS {#aem-advanced-mls}

若要支援進階多語言搜尋(MLS)的SRP集合（MSRP或DSRP），除了自訂架構和Solr組態外，還需要新的Solr外掛程式。 所有必要項目都封裝在可下載的zip檔案中。

進階MLS下載（也稱為&#39;phasetwo&#39;）可從Adobe儲存庫取得：

* [AEM-SOLR-MLS-phasetwo](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/tat/AEM-SOLR-MLS-phasetwo/1.2.40/)

   * 版本1.2.40,2016年4月6日
   * 下載AEM-SOLR-MLS-phasetwo-1.2.40.zip

有關詳細資訊和安裝資訊，請訪問[Solr Configuration](/help/communities/solr.md) for SRP。

### 關於包共用{#about-links-to-package-share}的連結

**Adobe AEM Cloud中可見的套件**

此頁面上的封裝連結不需要執行AEM例項，因為它們要在`adobeaemcloud.com`上封裝共用。 當可檢視套件時，`Install`按鈕會用來將套件安裝至Adobe代管網站。 如果想要安裝在本機AEM例項上，選取`Install`將會產生錯誤。

**如何安裝在本機AEM例項**

若要在本機AEM例項上安裝`adobeaemcloud.com`中可見的套件，必須先將套件下載至本機磁碟：

* 選擇&#x200B;**Assets**&#x200B;標籤
* 選擇&#x200B;**下載到磁碟**

在本機AEM例項中，使用套件管理器(例如[https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/))，以上傳至本機AEM的套件儲存庫。

或者，從本機AEM例項(例如[https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/))使用套件共用來存取套件，`Download`按鈕將下載至本機AEM例項的套件儲存庫。

在本機AEM例項的套件儲存庫中，使用套件管理器安裝套件。

有關詳細資訊，請訪問[如何使用包](/help/sites-administering/package-manager.md#package-share)。

## 建議的部署{#recommended-deployments}

在AEM Communities中，共用商店用來儲存使用者產生的內容(UGC)，通常稱為[儲存資源提供者(SRP)](/help/communities/working-with-srp.md)。 建議的部署中心是為公用商店選擇SRP選項。

公用商店支援在發佈環境中協調和分析UGC，同時不需要UGC的[複製](/help/communities/sync.md)。

* [社群內容商店](/help/communities/working-with-srp.md) :討論AEM社群的SRP儲存選項

* [建議的拓撲](/help/communities/topologies.md) :根據使用案例和SRP選擇討論要使用的拓撲

## 升級{#upgrading}

從舊版AEM升級至AEM 6.5平台時，請務必閱讀「升級至AEM 6.5[」。](/help/sites-deploying/upgrade.md)

除了升級平台外，請閱讀「升級至AEM Communities 6.5[」以瞭解社群變更。](/help/communities/upgrade.md)

## 設定 {#configurations}

### 主要發行者{#primary-publisher}

當選擇的部署是[publish farm](/help/communities/topologies.md#tarmk-publish-farm)時，對於不應發生在所有例項上的活動，例如依賴&#x200B;**通知**&#x200B;或&#x200B;**Adobe Analytics**&#x200B;的功能，必須將一個AEM發佈例項識別為&#x200B;**`primary publisher`**。

預設情況下，`AEM Communities Publisher Configuration` OSGi配置已選中&#x200B;**`Primary Publisher`**&#x200B;複選框，這樣發佈群中的所有發佈實例都將自標識為主實例。

因此，必須&#x200B;**編輯所有次要發佈實例的配置** ，以取消選中&#x200B;**`Primary Publisher`**&#x200B;複選框。

![primary-publisher](assets/primary-publisher.png)

對於發佈群中的所有其他（次要）發佈例項：

* 具有管理員權限的登入
* 訪問[Web控制台](/help/sites-deploying/configuring-osgi.md)

   * 例如，[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* 找到`AEM Communities Publisher Configuration`
* 選取編輯圖示
* 取消選中&#x200B;**Primary Publisher**&#x200B;框
* 選擇&#x200B;**保存**

### 作者上的複製代理{#replication-agents-on-author}

複製用於在發佈環境中建立的站點內容，如社區組，以及使用[tunnel service](#tunnel-service-on-author)從作者環境管理成員和成員組。

對於主發佈者，請確保[複製代理配置](/help/sites-deploying/replication.md)正確標識發佈伺服器和授權用戶。 預設授權用戶`admin,`已具有相應的權限（是`Communities Administrators`的成員）。

為了讓某些其他用戶擁有相應的權限，必須將其作為成員添加到`administrators`用戶組（也是`Communities Administrators`的成員）。

作者環境中有兩個複製代理需要正確配置傳輸配置。

* 在作者上訪問複製控制台

   * 在全局導航中，導航至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 複製]** > **[!UICONTROL 作者上的代理]**

* 對於兩個代理，請遵循相同的流程：

   * **預設代理（發佈）**
   * **反向複製代理（發佈反向）**

      1. 選擇代理
      1. 選擇&#x200B;**edit**
      1. 選擇&#x200B;**Transport**&#x200B;頁籤
      1. 如果不是埠`4503`，請編輯&#x200B;**URI**&#x200B;以指定正確的埠

      1. 如果不是用戶`admin`，請編輯&#x200B;**User**&#x200B;和&#x200B;**Password**&#x200B;以指定`administrators`用戶組的成員

以下影像顯示將埠從4503更改為6103的結果：

#### 預設代理（發佈）{#default-agent-publish}

![default-agent-publish](assets/default-agent-publish.png)

#### 反向複製代理（發佈反向）{#reverse-replication-agent-publish-reverse}

![反向複製代理](assets/reverse-replication-agent.png)

### 作者{#tunnel-service-on-author}上的隧道服務

使用作者環境建立站點[、](/help/communities/sites-console.md)修改站點屬性[或](/help/communities/sites-console.md#modifying-site-properties)管理社區成員[時，必須訪問在發佈環境中註冊的成員（用戶），而不是在作者上註冊的用戶。](/help/communities/members.md)

隧道服務使用作者上的複製代理提供此訪問。

要啟用隧道服務，請執行以下操作：

* 以管理權限登入您的作者實例。
* 如果發佈者不是localhost:4503或transport user不是`admin`,
然後，[配置複製代理](#replication-agents-on-author)

* 訪問[Web控制台](/help/sites-deploying/configuring-osgi.md)

   * 例如，[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* 找到`AEM Communities Publish Tunnel Service`
* 選取編輯圖示
* 選中&#x200B;**enable**&#x200B;框
* 選擇&#x200B;**保存**

   ![隧道服務](assets/tunnel-service.png)

### 複製加密密鑰{#replicate-the-crypto-key}

AEM Communities有兩項功能，需要所有AEM伺服器執行個體使用相同的加密金鑰。 這些是[Analytics](/help/communities/analytics.md)和[ASRP](/help/communities/asrp.md)。

自AEM 6.3起，關鍵資料會儲存在檔案系統中，而不會再儲存在儲存庫中。

為了將關鍵材料從作者複製到所有其他實例，必須：

* 存取AEM例項（通常為作者例項），其中包含要複製的關鍵材料

   * 在本地檔案系統中找到`com.adobe.granite.crypto.file`包，
例如，

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * `bundle.info`檔案將標識包
   * 導覽至資料夾，
例如，

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

      * 複製hmac和主節點檔案


* 針對每個目標AEM例項

   * 導覽至資料夾，
例如，

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * 貼上先前複製的2個檔案
   * 如果目標AEM實例當前正在運行，則需要[刷新Granite Crypto bundle](#refresh-the-granite-crypto-bundle)


>[!CAUTION]
>
>如果已經配置了基於加密密鑰的其他安全功能，則複製加密密鑰可能會損壞配置。 如需協助，請聯絡客戶服務[。](https://helpx.adobe.com/tw/marketing-cloud/contact-support.html)

#### 儲存庫複製{#repository-replication}

如同AEM 6.2及舊版軟體一樣，將關鍵資料儲存在儲存庫中，可在每個AEM例項的首次啟動時指定下列系統屬性（會建立初始儲存庫），以保留它：

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>請務必驗證author](#replication-agents-on-author)上的[複製代理是否正確配置。

將密鑰材料儲存在儲存庫中後，將加密密鑰從作者複製到其他實例的方式如下：

使用[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* 瀏覽至[https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* 選取 `/etc/key`
* 開啟`Replication`標籤
* 選取 `Replicate`

* [刷新Granite加密包](#refresh-the-granite-crypto-bundle)

   ![replicare-repository](assets/replicare-repository.png)

#### 刷新Granite加密包{#refresh-the-granite-crypto-bundle}

* 在每個發佈實例上，訪問[Web控制台](/help/sites-deploying/configuring-osgi.md)

   * 例如，[https://&lt;server>:&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* 找到`Adobe Granite Crypto Support`組合(com.adobe.granite.crypto)
* 選擇&#x200B;**刷新**

   ![花崗石密碼](assets/granite-crypto.png)

* 片刻後，應出現&#x200B;**Success**對話方塊：
   `Operation completed successfully.`

### Apache HTTP Server {#apache-http-server}

如果使用Apache HTTP伺服器，請確保對所有相關條目使用正確的伺服器名稱。

請特別留意使用`RedirectMatch`中正確的伺服器名稱，而非`localhost`。

#### httpd.conf示例{#httpd-conf-sample}

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

* AEM的[Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)檔案
* [安裝 Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [配置Dispatcher for Communities](/help/communities/dispatcher.md)
* [已知問題](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## 相關社群檔案{#related-communities-documentation}

* 請造訪[管理社群網站](/help/communities/administer-landing.md)，以瞭解如何建立社群網站、設定社群網站範本、協調社群內容、管理成員以及設定訊息。

* 請造訪[開發社群](/help/communities/communities.md)以瞭解社交元件架構(SCF)和自訂社群元件和功能。

* 請造訪[編寫社群元件](/help/communities/author-communities.md)，以瞭解如何編寫和設定社群元件。

