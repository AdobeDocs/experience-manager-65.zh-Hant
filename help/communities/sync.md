---
title: 社群用戶同步
seo-title: 社群用戶同步
description: 使用者同步的運作方式
seo-description: 使用者同步的運作方式
uuid: 772b82bd-a66c-4c1d-b80b-dcff77c873a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 97286c2c-f6e3-43ec-b1a9-2abb58616778
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# 社群用戶同步{#communities-user-synchronization}

## 簡介 {#introduction}

在AEM Communities中，從發佈環境（視設定的權限而定）, *網站訪客可能* 成為 **&#x200B;成員 *、建立*&#x200B;使用者群組 *，以及編輯* 其成員設定檔。

*使用者資料* ，是指使用者 *、使用者*&#x200B;設定檔 *和使* 用者群組 **。

*會員* 是指在發佈環境中注 *冊的使用者* ，而非在作者環境中註冊的使用者。

如需使用者資料的詳細資訊，請造 [訪管理使用者和使用者群組](/help/communities/users.md)。

## 同步發佈群組中的使用者 {#synchronizing-users-across-a-publish-farm}

根據設計，在發佈環境中建立的使用者資料不會出現在作者環境中。

在作者環境中建立的大部分使用者資料都會保留在作者環境中，不會同步或複製至發佈例項。

當拓 [撲為發](/help/communities/topologies.md) 布場時 [](/help/sites-deploying/recommended-deploys.md#tarmk-farm)，在一個發佈實例上進行的註冊和修改需要與其它發佈實例同步。 成員必須能夠登入並查看其資料在任何發佈節點上。

啟用用戶同步後，群中的發佈實例間的用戶資料會自動同步。

### 用戶同步設定說明 {#user-sync-setup-instructions}

有關如何啟用發佈群的同步的詳細逐步說明，請參閱

* [用戶同步](/help/sites-administering/sync.md)

## 使用者在背景同步 {#user-sync-in-the-background}

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **vlt package**:是發佈者上所做所有變更的zip檔案，需要在發佈者間散發。 發佈者上的變更會產生由變更事件接聽程式挑選的事件。 這會建立包含所有變更的vlt套件。

* **distribution package**:包含Sling的散發資訊。 這是內容需要在何處發佈，以及上次何時發佈的資訊。

## 當…… {#what-happens-when}

### 從Communities Sites console發佈網站 {#publish-site-from-communities-sites-console}

在作者上，當社群網站從 [Communities Sites主控台發佈時](/help/communities/sites-console.md)[](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents) ，其效果是複製相關頁面，而Sling則會分發動態建立的社群使用者群組，包括其會籍。

### 使用者已建立或在發佈時編輯設定檔 {#user-is-created-or-edits-profile-on-publish}

根據設計，在發佈環境（例如自行註冊、社交登入、LDAP驗證）中建立的使用者和設定檔不會出現在作者環境中。

當拓撲是發佈群 [，且使用者同步已正確設定時，會使](/help/communities/topologies.md) 用Sling *distribution在發佈群中同步使用者和* 使用者設定檔 ** 。

### 「發佈」上會建立新的社群群組 {#new-community-group-is-created-on-publish}

雖然從發佈例項開始，但實際上會在作者例項上建立社群群組，以產生新網站頁面和新的使用者群組。

在程式中，新網站頁面會複製到所有發佈例項。 動態建立的社群使用者群組及其會籍是Sling散布至所有發佈例項。

### 使用者或使用者群組是使用Security console建立的 {#users-or-user-groups-are-created-using-security-console}

根據設計，在發佈環境中建立的使用者資料不會出現在作者環境中，反之亦然。

當使用 [User Administration and Security](/help/sites-administering/security.md) Console在發佈環境中新增使用者時，使用者同步會視需要將新使用者及其群組成員資格同步到其他發佈執行個體。 使用者同步也會同步透過安全性主控台建立的使用者群組。

### 使用者在發佈時張貼內容 {#user-posts-content-on-publish}

對於用戶生成的內容(UGC)，在發佈實例上輸入的資料通過配置的SRP [訪問](/help/communities/srp-config.md)。

## Best practices {#bestpractices}

依預設，使用者同步會 **停用**。 啟用用戶同步涉及修改 *現有* OSGi配置。 啟用使用者同步後，不應新增任何新的設定。

使用者同步需仰賴作者環境來管理使用者資料分佈，即使使用者資料並非建立在作者上。

**必備條件**

1. 如果使用者和使用者群組已在一個發佈者上建立，建議在設定並啟用使用者同步 [前](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups) ，手動將使用者資料同步至所有發佈者。
啟用使用者同步後，僅會同步新建立的使用者和群組。

1. 請確定已安裝最新的代碼：

   * [AEM平台更新](https://helpx.adobe.com/experience-manager/kb/aem62-available-hotfixes.html)
   * [AEM Communities更新](/help/communities/deploy-communities.md#latestfeaturepack)

在AEM Communities上啟用使用者同步時，必須進行下列設定。 請確定這些設定正確，以防止sling內容散發失敗。

### Apache Sling Distribution Agent —— 同步代理工廠 {#apache-sling-distribution-agent-sync-agents-factory}

此設定會擷取要在發佈者之間同步的內容。 此組態位於Author執行個體上。 「作者」必須追蹤所有位於其中的發佈者，以及同步所有資訊的位置。

配置中的預設值是單個發佈實例的預設值。 由於使用者同步對同步多個發佈例項（例如對於發佈群）很有用，因此需要將其他發佈例項新增至設定。

**內容如何同步？**

編寫實例ping發佈器的導出端點。 每當在特定發佈者(n)上建立或更新使用者時，「作者」會從其匯出端點取得內容，並將內容推送至其他發佈者( [](/help/communities/sync.md#main-pars-image-1413756164) n-1，即從中擷取內容的發佈者除外)。

若要設定Apache Sling Sync Agents設定

在AEM作者實例上：

1. 以管理員權限登入。
1. 存取 [Web Console](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html)。 例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
1. 找 **到Apache Sling Distribution Agent - Sync Agents Factory。**

   * 選取要開啟以進行編輯的現有設定（鉛筆圖示）。
   驗證名稱：socialpubsync **.**

   * 選中「啟 **用** 」核取方塊。
   * 選擇 **使用多個隊列。**
   * 指定 **匯出端點** 和匯 **入工具端點** （您可以新增更多匯出工具和匯入工具端點）。

      這些端點會定義您要從何處取得內容，以及要將內容推播到何處。 作者從指定的導出器端點提取內容，並將內容推送到發佈者（其從中提取內容的發佈者除外）。


![sync-agent-fact](assets/sync-agent-fact.png)

### Adobe Granite Distribution —— 加密密碼傳輸機密提供者 {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

它可讓作者識別已授權的使用者，即具有從作者同步使用者資料以進行發佈的權限。

在所 [有發佈例項上建立的授權使用者](/help/sites-administering/sync.md#createauthuser) ，可協助發佈者與作者連線，並在作者上設定Sling散發。 此授權用戶擁有所有必要 [的ACL](/help/sites-administering/sync.md#howtoaddacl)。

每當要在發佈者上安裝資料或從發佈者擷取資料時，作者就會使用此設定中設定的認證（使用者名稱和密碼）連線發佈者。

使用授權使用者連線作者與發佈者

在AEM作者實例上：

1. 以管理員權限登入。
1. 存取 [Web Console](/help/sites-deploying/configuring-osgi.md)。

   例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
1. 找到 **Adobe Granite Distribution —— 加密密碼傳輸機密提供者。**
1. 選取要開啟以進行編輯的現有設定（鉛筆圖示）。

   驗證屬性 **socialpubsync** - **publishUser。**

1. 將使用者名稱和密碼設 [定給授權使用者](/help/sites-administering/sync.md#createauthorizeduser)。

   例如， **usersync - admin**

![花崗——密碼——轉移](assets/granite-paswrd-trans.png)

### Apache Sling Distribution Agent - Queue Agents Factory {#apache-sling-distribution-agent-queue-agents-factory}

此設定可用來設定您要在發佈者間同步的資料。 在「允許的根」中指定的路徑中建立／更新資料時，「var/community/distribution/diff」將被激活，而建立的複製器將從發佈商中提取資料，並將其安裝到其他發佈商。 ****

配置要同步的資料（節點路徑）

在AEM發佈例項上：

1. 以管理員權限登入。
1. 存取 [Web Console](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html)。

   例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)。

1. 找 **到Apache Sling Distribution Agent - Queue Agents Factory。**
1. 選取要開啟以進行編輯的現有設定（鉛筆圖示）。

   驗證名稱：socialpubsync **-reverse。**

1. 選中「啟 **用** 」核取方塊並儲存。
1. 指定要在允許的根中複製的節 **點路徑**。
1. 對每個發佈例 **項重複** 。

![隊列代理——事實](assets/queue-agents-fact.png)

### Adobe Granite Distribution - Diff Observer Factory {#adobe-granite-distribution-diff-observer-factory}

此設定會同步發佈者的群組成員資格。
如果變更某個發佈者中的群組成員資格並未更新其他發佈者的成員資格，請確定 **ref:members** 已新增至已 **尋找的屬性名稱**。

確保成員同步

在每個AEM發佈例項上：

1. 以管理員權限登入。
1. 存取 [Web Console](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html)。

   例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)。

1. 找到 **Adobe Granite Distribution - Diff Observer Factory。**
1. 選取要開啟以進行編輯的現有設定（鉛筆圖示）。

   驗證 **代理名稱：socialpubsync -reverse**。

1. 選中「啟 **用** 」核取方塊。
1. 指定 **rep:members** 作為查找的屬性名稱中 **的propertyName的說明**，並指定Save。

![diff-obs](assets/diff-obs.png)

### Apache Sling Distribution Trigger —— 計畫觸發器工廠 {#apache-sling-distribution-trigger-scheduled-triggers-factory}

此設定可讓您設定輪詢間隔（在輪詢間隔後，發佈者會被Ping化，而作者會提取變更），以同步發佈者的變更。

作者會每30秒（預設值）對發行者進行投票。 如果資料夾 */var/sling/distribution/packages/ socialpubsync - vlt /shared*，則會擷取這些封裝，並將它們安裝在其他發佈者上。

更改輪詢間隔

在AEM作者實例上：

1. 以管理員權限登入。
1. 存取 [Web Console](/help/sites-deploying/configuring-osgi.md)，例如 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. 找到 **Apache Sling Distribution Trigger —— 計畫觸發器工廠**

   * 選取要開啟以進行編輯的現有設定（鉛筆圖示）

      驗證 **socialpubsync -scheduled-trigger**

   * 將「間隔」（以秒為單位）設定為所需間隔並保存。

![scheduled-trigger](assets/scheduled-trigger.png)

### AEM Communities使用者同步接聽程式 {#aem-communities-user-sync-listener}

如果Sling散發中訂閱與後續版本有差異，請檢查 **AEM Communities User Sync Listener組態中是否已設定下列屬性** :

* NodeTypes
* 可忽略屬性
* 可忽略節點
* DistributedFolders

若要同步訂閱、追蹤和通知

在每個AEM發佈例項上：

1. 以管理員權限登入。
1. 存取 [Web Console](/help/sites-deploying/configuring-osgi.md)。 例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)。
1. 找到 **AEM Communities使用者同步接聽程式。**
1. 選取要開啟以進行編輯的現有設定（鉛筆圖示）

   驗證名稱： **socialpubsync -scheduled-trigger**

1. 設定以下 **NodeTypes**:

   rep：用戶

   nt:unstructured

   nt：資源

   rep:ACL

   sling:Folder

   sling:OrderedFolder

   此屬性中指定的節點類型將同步，不同發佈者之間會同步通知資訊（部落格和後面的設定）。

1. 在 **DistributedFolders中添加要同步的所有資料夾**。 例如，

   區段／計分

   社交／關係

   活動

1. 將忽略 **值設定為** :

   .token

   系統

   rep:cache（由於我們使用粘滯會話，因此不需要將此節點同步到不同的發佈者）

![user-sync-listner](assets/user-sync-listner.png)

### 唯一Sling ID {#unique-sling-id}

AEM作者例項使用Sling ID來識別資料來自何處，以及它需要（或不需要）將套件傳回給哪些發佈者。

請確定發佈農場中的所有發佈者都有唯一的Sling ID。 如果Sling ID與發佈群中多個發佈例項的相同，則使用者同步將失敗。 由於作者不知道要從何處擷取套件，以及要在何處安裝套件。

若要確保發佈場中發佈者的唯一Sling ID

在每個發佈例項上：

1. 瀏覽至 [https://_host:port_/system/console/status-slingsettings](https://localhost:4503/system/console/status-slingsettings)。
1. 檢查 **Sling ID的值。**

![slingid](assets/slingid.png)

如果發佈例項的Sling ID符合任何其他發佈例項的Sling ID，則：

1. 停止其中一個具有相符Sling ID的發佈例項。
1. 在目錄 `crx-quickstart/launchpad/felix` 中，搜索並刪除名為sling.id.file的 *檔案。*

   例如，在Linux系統上：

   `rm -i $(find . -type f -name sling.id.file)`

   例如，在Windows系統上：

   使用Windows檔案總管和搜尋 `sling.id.file`

1. 啟動發佈例項。 在啟動時，會指派新的Sling ID。
1. 驗證 **Sling ID現在是唯一的** 。

重複這些步驟，直到所有發佈例項都有唯一的Sling ID。

### Vault Package Builder Factory {#vault-package-builder-factory}

要正確同步更新，必須修改儲存庫包生成器以用於用戶同步。
在 **/home/users**&#x200B;中，會建立***/rep:cache **node。 它是一個快取，用於發現，如果我們查詢節點的主體名稱，則可以直接使用該快取。

如果各發佈商之間的節點 `rep :cache `保持同步，則用戶同步可以停止。

為確保更新在發佈者之間正確同步

在每個AEM發佈例項上：

1. 存取 [Web Console](/help/sites-deploying/configuring-osgi.md)

   例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)。
1. 找到 **Apache Sling Distribution Packaging - Vault Package Builder Factory**

   建立器名稱：socialpubsync-vlt

1. 選擇編輯表徵圖。
1. 添加兩個包節點篩選器：
   * /home/users|-.*/.tokens
   * /home/users|**-**.*/rep:cache

1. 政策處理

   * 要用新節點覆蓋現有rep:policy節點，請添加第三個包過濾器：

      /home/users|**+**.*/rep:policy

   * 要防止策略被分發，請設定

      Acl處理：忽略

![保險儲存包生成器工廠](assets/vault-package-builder-factory.png)

## 疑難排解AEM Communities中的Sling散發 {#troubleshoot-sling-distribution-in-aem-communities}

如果Sling散發失敗，請嘗試下列除錯步驟：

1. **檢查是否[未正確添加配置](/help/sites-administering/sync.md#improperconfig)。** 請確定未新增或編輯多個設定，而應編輯現有的預設設定。
1. **檢查配置**。 請確定您的AEM Author [](/help/communities/sync.md#bestpractices)例項中已正確設定所有設定，如「最佳實務」中 [所述](/help/communities/sync.md#main-pars-header-863110628)。
1. **檢查授權的使用者權限**。 如果軟體包未正確安裝，則檢查在第一個 [Publish實例中建立的授權用戶](/help/sites-administering/sync.md#createauthuser) ，是否具有正確的ACL。

   若要驗證此項，請改變作者 [例項上的「](/help/sites-administering/sync.md#createauthuser) Adobe Granite Distribution - Encrypted Password Transport Secret Provider [](/help/sites-administering/sync.md#adobegraniteencpasswrd) 」設定，以使用管理員使用者憑證。 現在，請嘗試再次安裝軟體包。 如果用戶同步與管理員憑據配合工作正常，則表示建立的發佈用戶沒有適當的ACL。

1. **檢查比較觀察器工廠配置**。 如果發佈群中只有特定節點未同步——例如，群組成員未同步——則請確定 [Adobe Granite Distribution - Diff Observer Factory](/help/sites-administering/sync.md#diffobserver) configuration已啟用，並 **表示：成員** 在查找的屬性 **名稱中設定**。
1. **檢查AEM Communities使用者同步監聽器設定。** 如果已建立的使用者已同步，但訂閱和後續作業無法運作，請確定AEM Communities使用者同步接聽程式設定有：

   * 節點類型——設定為 **rep:Nt :unstructured**, **nt :resource**, **rep:ACL**, ******sling:FolderSling, and Sling:OrderedFolder**
   * 可忽略節點——設為 **.token**、 **system**&#x200B;和 **rep :cache**
   * 分佈式資料夾——設定到要分發的資料夾

1. **檢查在「發佈」實例上建立用戶時生成的日誌**。 如果上述設定已正確設定，但使用者同步仍無法運作，則請檢查在建立使用者時產生的記錄檔。

   檢查日誌順序是否相同，如下所示：

   ```shell
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ2: ADD paths=[/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK], user=communities-user-admin
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ3: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy], user=communities-user-admin
   15.05.2016 18:33:01.757 *INFO* [sling-oak-observation-7431] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_ebb27ad9-a861-4405-9342-d64c916654e2:0.0.1
   15.05.2016 18:33:01.820 *INFO* [sling-oak-observation-7422] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_58811273-5861-48fe-95d2-4aff367b99c3:0.0.1
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK/profile]
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ4: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK/profile], user=communities-user-admin
   15.05.2016 18:33:02.273 *INFO* [sling-oak-observation-7430] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337182039_f34f4fa6-10b9-42eb-8740-4da9d4d38f99:0.0.1
   ```

   若要除錯：

   1. 禁用用戶同步：
   1. 在AEM作者例項上，以管理員權限登入。

      1. 存取 [Web Console](/help/sites-deploying/configuring-osgi.md)。 例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
      1. 找到設定 **Apache Sling Distribution Agent - Sync Agents Factory**。
      1. 取消選 **取「啟用** 」核取方塊。
在作者實例上禁用用戶同步時，（導出器和導入器）端點將被禁用，而作者實例是靜態的。 作 **者不** 會ping或擷取vlt套件。
現在，如果使用者是在發佈例項上建立， **vlt** package is created in */var/sling/distribution/packages/ socialpubsync - vlt /data* node. 如果這些套件是由作者推送至其他服務。 您可以下載並擷取此資料，以檢查所有屬性都推送至其他服務。
   1. 前往發行者，並在發佈者上建立使用者。 因此，會建立事件。
   1. 檢查在 [建立用戶時建立的日](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities)志順序。
   1. 檢查**vlt **package是否在 **/var/sling/distribution/packages/socialpubsync-vlt/data上建立**。
   1. 現在，在AEM作者例項上啟用使用者同步。
   1. 在發行者上，變更 **Apache Sling Distribution Agent - Sync Agents Factory中的匯出器或匯入器端點**。
我們可以下載並擷取封裝資料，以檢查哪些屬性已推送至其他發佈者，以及哪些資料遺失。
