---
title: 部署社群
description: 如何部署AEM Communities
content-type: reference
topic-tags: deploying
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '1705'
ht-degree: 0%

---


# 部署社群{#deploying-communities}

## 先決條件 {#prerequisites}

* [AEM 6.5平台](/help/sites-deploying/deploy.md)

* AEM Communities授權

* 選購的授權：

   * [適用於社群的Adobe Analytics功能](/help/communities/analytics.md)
   * [MSRP適用的MongoDB](/help/communities/msrp.md)
   * [ASRP的Adobe雲端](/help/communities/asrp.md)

## 安裝檢查清單 {#installation-checklist}

**對於[AEM平台](/help/sites-deploying/deploy.md#what-is-aem)**：

* 安裝最新的[AEM 6.5更新](#aem64updates)。

* 如果未使用預設連線埠(4502、4503)，則[設定復寫代理程式](#replication-agents-on-author)。
* [復寫加密金鑰](#replicate-the-crypto-key)
* 如果支援全球化，[設定自動化翻譯](/help/sites-administering/translation.md)
（提供範例設定以進行開發）。

**針對[Communities功能](/help/communities/overview.md)**：

* 如果部署[發佈伺服器陣列](/help/sites-deploying/recommended-deploys.md#tarmk-farm)，請[識別主要發行者](#primary-publisher)

* [啟用通道服務](#tunnel-service-on-author)
* [啟用社交登入](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [設定 Adobe Analytics](/help/communities/analytics.md)
* 設定[預設電子郵件服務](/help/communities/email.md)
* 識別[共用UGC存放區](/help/communities/working-with-srp.md) (**SRP**)的選擇

   * 如果MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [安裝及設定MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [設定Solr](/help/communities/solr.md)
      * [選取MSRP](/help/communities/srp-config.md)

   * 如果關聯式資料庫SRP [(DSRP)](/help/communities/dsrp.md)

      * [安裝適用於MySQL的JDBC驅動程式](#jdbc-driver-for-mysql)
      * [安裝及設定MySQL for DSRP](/help/communities/dsrp-mysql.md)
      * [設定Solr](/help/communities/solr.md)
      * [選取DSRP](/help/communities/srp-config.md)

   * 如果AdobeSRP [(ASRP)](/help/communities/asrp.md)

      * 請與您的客戶代表合作以進行布建。
      * [選取ASRP](/help/communities/srp-config.md)

   * 若為JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * 不是共用的UGC （使用者產生的內容）存放區：

         * 從未復寫UGC。
         * UGC只會顯示在輸入它的AEM執行個體或叢集上。

      * 預設為JSRP


## 最新版本 {#latest-releases}

AEM 6.5 Communities GA包含Communities套件。 若要進一步瞭解AEM 6.5 [社群](/help/release-notes/release-notes.md#experiencemanagercommunities)的更新，請參閱[AEM 6.5發行說明](/help/release-notes/release-notes.md#communities-release-notes.html)。

### AEM 6.5更新 {#aem-updates}

從AEM 6.4開始，Communities的更新屬於AEM Cumulative Fix Pack和Service Pack的一部分。

如需AEM 6.5的最新更新，請參閱[Adobe Experience Manager 6.4 Cumulative Fix Pack和Service Pack](https://helpx.adobe.com/tw/experience-manager/aem-releases-updates.html)。

### 版本記錄 {#version-history}

和AEM 6.4及更高版本一樣，AEM Communities功能和Hotfix是AEM Communities Cumulative Fix Pack和Service Pack的一部分。 因此，沒有單獨的Feature Pack。

### MySQL的JDBC驅動程式 {#jdbc-driver-for-mysql}

一個Communities功能使用MySQL資料庫：

* 針對[DSRP](/help/communities/dsrp.md)：儲存UGC

必須單獨取得並安裝MySQL聯結器。

必要的步驟為：

1. 從[https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)下載ZIP封存

   * 版本必須>= 5.1.38

1. 擷取`mysql-connector-java-&lt;version&gt;-bin.jar (bundle) from the archive`
1. 使用Web主控台安裝並啟動套件組合：

   * 例如， https://localhost:4502/system/console/bundles
   * 選取&#x200B;**`Install/Update`**
   * 瀏覽……以選取從下載的ZIP封存解壓縮的套件組合
   * 檢查&#x200B;*Oracle Corporation的MySQLcom.mysql.jdbc*&#x200B;之JDBC驅動程式是否使用中，若未使用則啟動它（或檢查記錄檔）

1. 如果在設定JDBC之後於現有部署上進行安裝，則從Web主控台重新儲存JDBC設定，以將JDBC重新繫結至新聯結器：

   * 例如， https://localhost:4502/system/console/configMgr
   * 找出`Day Commons JDBC Connections Pool`組態，並選取以開啟組態。
   * 選取`Save`。

1. 在所有製作和發佈執行個體上重複步驟3和4。

在[網頁主控台](/help/sites-deploying/web-console.md#bundles)頁面上找到有關安裝套裝的詳細資訊。

#### 範例：已安裝MySQL聯結器套件組合 {#example-installed-mysql-connector-bundle}

![Adobe Experience Manager Web主控台MySQL聯結器套件](../assets/mysql-connector.png)

### AEM進階MLS {#aem-advanced-mls}

若要讓SRP集合（MSRP或DSRP）支援進階多語言搜尋(MLS)，除了自訂結構描述和Solr設定外，還需要新的Solr外掛程式。 所有必要專案都會封裝成可下載的zip檔案。

進階MLS下載（也稱為「phasetwo」）可從Adobe存放庫取得：

* [AEM-SOLR-MLS-phasetwo](https://repo1.maven.org/maven2/com/adobe/tat/AEM-SOLR-MLS-phasetwo/1.2.40/)

   * 1.2.40版，2016年4月6日
   * 下載AEM-SOLR-MLS-phasetwo-1.2.40.zip

如需詳細資訊和安裝資訊，請造訪SRP的[Solr組態](/help/communities/solr.md)。

### 關於封裝共用的連結 {#about-links-to-package-share}

在AEM CloudAdobe **中顯示**&#x200B;個套件

此頁面上封裝的連結不需要正在執行的AEM執行個體，因為它們會在`adobeaemcloud.com`上共用封裝。 雖然可以檢視套件，但`Install`按鈕用於將套件安裝到Adobe代管站台。 如果要在本機AEM執行個體上安裝，選取`Install`會導致錯誤。

**如何在本機AEM執行個體上安裝**

若要在本機AEM執行個體上安裝`adobeaemcloud.com`中顯示的套件，必須先將套件下載至本機磁碟：

* 選取&#x200B;**Assets**&#x200B;索引標籤
* 選取&#x200B;**下載至磁碟**

在本機AEM執行個體上，使用封裝管理員(例如，[https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/))來上傳至本機AEM封裝存放庫。

或者，使用封裝共用從本機AEM執行個體(例如，[https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/))存取封裝，`Download`按鈕會下載到本機AEM執行個體的封裝存放庫。

一旦進入本機AEM執行個體的封裝存放庫，請使用封裝管理員來安裝封裝。

如需詳細資訊，請造訪[如何使用封裝](/help/sites-administering/package-manager.md#package-share)。

## 建議的部署 {#recommended-deployments}

在AEM Communities中，公用存放區是用來儲存UGC，通常稱為[儲存資源提供者(SRP)](/help/communities/working-with-srp.md)。 建議的部署著重於為通用存放區選擇SRP選項。

公用存放區支援在發佈環境中對UGC進行稽核和分析，同時消除對UGC [復寫](/help/communities/sync.md)的需求。

* [社群內容存放區](/help/communities/working-with-srp.md) ：討論AEM Communities的SRP儲存選項

* [建議的拓撲](/help/communities/topologies.md) ：根據使用案例和SRP選擇討論要使用的拓撲

## 升級 {#upgrading}

從舊版AEM升級至AEM 6.5平台時，請務必閱讀[升級至AEM 6.5](/help/sites-deploying/upgrade.md)。

除了升級平台，請閱讀[升級至AEM Communities 6.5](/help/communities/upgrade.md)以瞭解社群變更。

## 設定 {#configurations}

### 主要發行者 {#primary-publisher}

當選擇的部署是[發佈伺服器陣列](/help/communities/topologies.md#tarmk-publish-farm)時，則必須將一個AEM發佈執行個體識別為不應在所有執行個體上發生的活動的&#x200B;**`primary publisher`**。 例如，依賴&#x200B;**通知**&#x200B;或&#x200B;**Adobe Analytics**&#x200B;的功能。

根據預設，`AEM Communities Publisher Configuration` OSGi設定是使用&#x200B;**`Primary Publisher`**&#x200B;核取方塊來設定，因此發佈伺服器陣列中的所有發佈執行個體都會自行識別為主要執行個體。

因此，必須&#x200B;**編輯所有次要發佈執行個體的組態**&#x200B;以取消勾選&#x200B;**`Primary Publisher`**&#x200B;核取方塊。

![AEM Communities發行者設定對話方塊顯示主要發行者核取方塊](../assets/primary-publisher.png)

對於發佈伺服器陣列中的所有其他（次要）發佈執行個體：

* 使用管理員許可權登入
* 存取[網頁主控台](/help/sites-deploying/configuring-osgi.md)

   * 例如，[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* 找到`AEM Communities Publisher Configuration`
* 選取編輯圖示
* 取消勾選&#x200B;**主要發行者**&#x200B;核取方塊
* 選取&#x200B;**儲存**

### 作者上的復寫代理 {#replication-agents-on-author}

復寫用於發佈環境中建立的網站內容，例如社群群組，以及使用[通道服務](#tunnel-service-on-author)管理作者環境中的成員與成員群組。

對於主要發行者，請確定[復寫代理程式設定](/help/sites-deploying/replication.md)正確識別發行伺服器和授權使用者。 預設授權使用者`admin`已經擁有適當的許可權（`Communities Administrators`的成員）。

其他使用者若要擁有適當的許可權，必須將其新增為`administrators`使用者群組（也是`Communities Administrators`的成員）的成員。

製作環境中有兩個復寫代理程式需要正確設定傳輸設定。

* 存取作者上的復寫主控台

   * 從全域導覽： **工具，部署，復寫，作者上的代理程式**

* 請對這兩個代理程式遵循相同的程式：

   * **預設代理程式（發佈）**
   * **反向復寫代理程式（反向發佈）**

      1. 選取代理程式。
      1. 選取&#x200B;**編輯**。
      1. 選取&#x200B;**傳輸**&#x200B;標籤
      1. 如果它不是連線埠`4503`，請編輯&#x200B;**URI**&#x200B;以指定正確的連線埠。

      1. 如果不是使用者`admin`，請編輯&#x200B;**使用者**&#x200B;和&#x200B;**密碼**&#x200B;以指定`administrators`使用者群組的成員。

下列影像顯示透過將連線埠從4503變更為6103的結果：

#### 預設代理程式（發佈） {#default-agent-publish}

![設定 — 限制](../assets/default-agent-publish.png)

#### 反向復寫代理程式（反向發佈） {#reverse-replication-agent-publish-reverse}

![反向復寫代理程式（發佈回覆）顯示它已經開啟或啟用。](../assets/reverse-replication-agent.png)

### 作者上的通道服務 {#tunnel-service-on-author}

使用作者環境來[建立網站](/help/communities/sites-console.md)、[修改網站屬性](/help/communities/sites-console.md#modifying-site-properties)或[管理社群成員](/help/communities/members.md)時，必須存取在發佈環境中註冊的成員（使用者），而非在作者上註冊的使用者。

通道服務使用作者上的復寫代理程式提供此存取權。

若要啟用通道服務：

* 在&#x200B;**作者**&#x200B;上，以系統管理許可權登入。
* 如果發行者不是localhost：4503或傳輸使用者不是`admin`，
然後[設定復寫代理程式](#replication-agents-on-author)。

* 存取[網頁主控台](/help/sites-deploying/configuring-osgi.md)

   * 例如，[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* 找到`AEM Communities Publish Tunnel Service`
* 選取編輯圖示
* 選取&#x200B;**啟用**&#x200B;核取方塊
* 選取&#x200B;**儲存**

![AEM Communities Publish通道服務顯示[啟用]核取方塊，已選取或已核取。](../assets/tunnel-service.png)

### 復寫加密金鑰 {#replicate-the-crypto-key}

AEM Communities有兩個功能，需要所有AEM伺服器執行個體使用相同的加密金鑰。 這些是[Analytics](/help/communities/analytics.md)和[ASRP](/help/communities/asrp.md)。

自AEM 6.3起，金鑰資料儲存在檔案系統中，不再儲存在存放庫中。

若要將關鍵資料從「作者」複製到所有其他例項，必須：

* 存取AEM例項，通常是包含要複製之關鍵素材的製作例項

   * 在本機檔案系統中找到`com.adobe.granite.crypto.file`套件

     例如，

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * `bundle.info`檔案識別該組合

   * 導覽至資料夾
例如，

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

   * 複製hmac和主要節點檔案。

* 針對每個目標AEM例項

   * 導覽至資料夾
例如，

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

   * 貼上先前複製的兩個檔案
   * 如果目標AEM執行個體正在執行，則必須[重新整理Granite加密套件](#refresh-the-granite-crypto-bundle)。

>[!CAUTION]
>
>如果已經設定了另一個以加密金鑰為基礎的安全性功能，則複製加密金鑰可能會損壞設定。 如需協助，[請連絡客戶服務](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support)。

#### 存放庫復寫 {#repository-replication}

將關鍵資料儲存在存放庫中(例如AEM 6.2和更早版本)可以保留。 在每個AEM執行個體的首次啟動（建立初始存放庫）時，指定下列系統屬性：

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>務必確認作者](#replication-agents-on-author)上的[復寫代理程式已正確設定。

將金鑰資料儲存在存放庫後，將加密金鑰從作者複製到其他例項的方式如下：

使用[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) ：

* 瀏覽至[https://&lt;server>：&lt;port>/crx/de](https://localhost:4502/crx/de)
* 選取`/etc/key`
* 開啟`Replication`索引標籤
* 選取`Replicate`

* [重新整理Granite加密套件組合](#refresh-the-granite-crypto-bundle)

![CRXDE Lite在左面板上顯示/etc/key路徑，並在右下面板中顯示Replication索引標籤。](../assets/replicare-repository.png)

#### 重新整理Granite加密套件組合 {#refresh-the-granite-crypto-bundle}

* 在每個發佈執行個體上，存取[網頁主控台](/help/sites-deploying/configuring-osgi.md)

   * 例如，[https://&lt;伺服器>：&lt;連線埠>/system/console/bundles](https://localhost:4503/system/console/bundles)

* 找到`Adobe Granite Crypto Support`套件(com.adobe.granite.crypto)
* 選取&#x200B;**重新整理**

![正在重新整理AdobeGranite加密支援組合。](../assets/refresh-granite-bundle.png)

* 過了一會兒，應該會出現&#x200B;**成功**對話方塊：
  `Operation completed successfully.`

### Apache HTTP Server {#apache-http-server}

如果使用Apache HTTP伺服器，請確定您對所有相關專案使用正確的伺服器名稱。

特別是，請注意在`RedirectMatch`中使用正確的伺服器名稱，而不是`localhost`。

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

* AEM [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)檔案
* [安裝 Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/dispatcher-install.html)
* [為社群設定Dispatcher](/help/communities/dispatcher.md)
* [已知問題](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## 相關社群檔案 {#related-communities-documentation}

* 請造訪[管理社群網站](/help/communities/administer-landing.md)，瞭解如何建立社群網站、設定社群網站範本、管理社群內容、管理成員，以及設定訊息。

* 造訪[開發Communities](/help/communities/communities.md)，瞭解社交元件架構(SCF)和自訂Communities元件和功能。

* 造訪[Authoring Communities Components](/help/communities/author-communities.md)，瞭解如何使用及設定Communities元件進行創作。

