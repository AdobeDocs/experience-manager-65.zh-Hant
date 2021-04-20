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
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2510'
ht-degree: 2%

---


# 社區用戶同步{#communities-user-synchronization}

## 簡介 {#introduction}

在AEM Communities，從發佈環境（視設定的權限而定）,*網站訪客*&#x200B;可成為&#x200B;*成員*、建立&#x200B;*使用者群組*，並編輯其&#x200B;*成員描述檔*。

*使* 用者資料是用來指代使用者、使 *用者*&#x200B;分析 *及使* 用者群組 **。

*會* 籍是指在發佈環境中注 ** 冊的使用者，而非在作者環境中註冊的使用者。

有關用戶資料的詳細資訊，請訪問[管理用戶和用戶組](/help/communities/users.md)。

## 同步發佈群{#synchronizing-users-across-a-publish-farm}的使用者

根據設計，在發佈環境中建立的使用者資料不會出現在作者環境中。

在作者環境中建立的大部分使用者資料都會保留在作者環境中，不會同步或複製至發佈例項。

當[拓撲](/help/communities/topologies.md)為[發佈群](/help/sites-deploying/recommended-deploys.md#tarmk-farm)時，在一個發佈實例上進行的註冊和修改必須與其他發佈實例同步。 成員必須能夠登入並查看其資料在任何發佈節點上。

啟用用戶同步後，群中的發佈實例間的用戶資料會自動同步。

### 用戶同步設定說明{#user-sync-setup-instructions}

有關如何啟用發佈群的同步的詳細、逐步說明，請參閱：

* [用戶同步](/help/sites-administering/sync.md)

## 背景{#user-sync-in-the-background}中的使用者同步

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **vlt套件**

   它是發佈商上所有變更的zip檔案，需要在發佈商間散發。 發佈者上的變更會產生由變更事件接聽程式挑選的事件。 這會建立包含所有變更的vlt套件。

* **散發套件**

   它包含Sling的散發資訊。 這是內容需要在何處發佈，以及上次何時發佈的資訊。

## 當……{#what-happens-when}

### 從Communities Sites控制台{#publish-site-from-communities-sites-console}發佈網站

在作者上，當社群網站從[Communities Sites主控台](/help/communities/sites-console.md)發佈時，其效果是[replicate](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents)相關頁面，而Sling則分發動態建立的社群使用者群組，包括其會籍。

### 在發佈{#user-is-created-or-edits-profile-on-publish}時建立或編輯用戶配置檔案

根據設計，在發佈環境（例如自行註冊、社交登入、LDAP驗證）中建立的使用者和設定檔不會出現在作者環境中。

當拓撲為[publish farm](/help/communities/topologies.md)且已正確設定使用者同步時，使用Sling散發，將&#x200B;*user*&#x200B;和&#x200B;*user profile*&#x200B;同步到發佈群。

### 在Publish {#new-community-group-is-created-on-publish}上建立新的社群群組

雖然從發佈例項開始，但實際上會在作者例項上建立社群群組，以產生新網站頁面和新的使用者群組。

在程式中，新網站頁面會複製到所有發佈例項。 動態建立的社群使用者群組及其會籍是Sling散布至所有發佈例項。

### 使用Security Console {#users-or-user-groups-are-created-using-security-console}建立使用者或使用者群組

根據設計，在發佈環境中建立的使用者資料不會出現在作者環境中，反之亦然。

當使用[使用者管理與安全性](/help/sites-administering/security.md)主控台來在發佈環境中新增使用者時，使用者同步會視需要將新使用者及其群組成員資格同步到其他發佈執行個體。 使用者同步也會同步透過安全性主控台建立的使用者群組。

### 使用者在發佈時發佈內容{#user-posts-content-on-publish}

對於用戶生成的內容(UGC)，在發佈實例上輸入的資料通過[配置的SRP](/help/communities/srp-config.md)訪問。

## 最佳做法{#bestpractices}

依預設，使用者同步為&#x200B;**disabled**。 啟用用戶同步涉及修改&#x200B;*existing* OSGi配置。 啟用使用者同步後，不應新增任何新的設定。

使用者同步需仰賴作者環境來管理使用者資料分佈，即使使用者資料並非建立在作者上。

**必備條件**

1. 如果使用者和使用者群組已在一個發佈者上建立，建議在設定並啟用使用者同步之前，手動將使用者資料同步至所有發佈者。[](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups)

   啟用使用者同步後，僅會同步新建立的使用者和群組。

1. 請確定已安裝最新的代碼：

   * [AEM平台更新](https://helpx.adobe.com/tw/experience-manager/kb/aem62-available-hotfixes.html)
   * [AEM Communities更新](/help/communities/deploy-communities.md#latestfeaturepack)

在AEM Communities啟用用戶同步時，必須進行以下配置。 請確定這些設定正確，以防止sling內容散發失敗。

### Apache Sling Distribution Agent - Sync Agents Factory {#apache-sling-distribution-agent-sync-agents-factory}

此設定會擷取要在發佈者之間同步的內容。 此組態位於Author執行個體上。 「作者」必須追蹤所有位於其中的發佈者，以及同步所有資訊的位置。

配置中的預設值是單個發佈實例的預設值。 由於使用者同步對同步多個發佈例項（例如對於發佈群）很有用，因此需要將其他發佈例項新增至設定。

**內容如何同步？**

編寫實例ping發佈器的導出端點。 每當在特定發佈者(n)上建立或更新使用者時，「作者」會從其匯出端點取得內容，並且[將內容](/help/communities/sync.md#main-pars-image-1413756164)推送至其他發佈者（n-1，即與擷取內容的發佈者不同）。

若要設定Apache Sling Sync Agents設定：

1. 以管理員權限登入您的作AEM者例項。
1. 訪問[Web控制台](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html)。 例如，[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
1. 找到&#x200B;**Apache Sling Distribution Agent - Sync Agents Factory**。

   * 選取要開啟以進行編輯的現有設定（鉛筆圖示）。

      驗證名稱：**socialpubsync.**

   * 選中&#x200B;**Enabled**&#x200B;複選框。
   * 選擇&#x200B;**使用多個隊列。**
   * 指定&#x200B;**匯出器端點**&#x200B;和&#x200B;**匯入器端點**（您可以新增更多匯出器和匯入器端點）。

      這些端點會定義您要從何處取得內容，以及要將內容推播到何處。 作者從指定的導出器端點提取內容，並將內容推送到發佈者（其從中提取內容的發佈者除外）。
   ![sync-agent-fact](assets/sync-agent-fact.png)

### Adobe花崗岩分佈——加密密碼傳輸機密提供者{#adobe-granite-distribution-encrypted-password-transport-secret-provider}

它可讓作者識別已授權的使用者，即具有從作者同步使用者資料以進行發佈的權限。

在所有發佈例項上建立的[授權使用者](/help/sites-administering/sync.md#createauthuser)可協助發佈者與作者連線，並在作者上設定Sling散發。 此授權用戶具有所有必需的[ACL](/help/sites-administering/sync.md#howtoaddacl)。

每當要在發佈者上安裝資料或從發佈者擷取資料時，作者就會使用此設定中設定的認證（使用者名稱和密碼）連線發佈者。

若要使用授權使用者連線作者與發佈者：

1. 以管理員權限登入您的作AEM者例項。
1. 訪問[Web控制台](/help/sites-deploying/configuring-osgi.md)。

   例如，[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
1. 找到&#x200B;**Adobe花崗岩分佈——加密密碼傳輸機密提供程式。**
1. 選取要開啟以進行編輯的現有設定（鉛筆圖示）。

   驗證屬性&#x200B;**socialpubsync** - **publishUser.**

1. 將用戶名和密碼設定為[授權用戶](/help/sites-administering/sync.md#createauthorizeduser)。

   例如，**usersync - admin**

![花崗——密碼——轉移](assets/granite-paswrd-trans.png)

### Apache Sling Distribution Agent - Queue Agents Factory {#apache-sling-distribution-agent-queue-agents-factory}

此設定可用來設定您要在發佈者間同步的資料。 當在&#x200B;**允許根**&#x200B;中指定的路徑中建立／更新資料時，「var/community/distribution/diff」將激活，並且建立的複製器從發佈商提取資料，並將其安裝到其他發佈商。

要配置要同步的資料（節點路徑）:

1. 以管理員權限登入您的作者例項。
1. 訪問[Web控制台](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html)。

   例如，[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)。

1. 找到&#x200B;**Apache Sling Distribution Agent - Queue Agents Factory**。
1. 選取要開啟以進行編輯的現有設定（鉛筆圖示）。

   驗證名稱：**socialpubsync -reverse**

1. 選中&#x200B;**Enabled**&#x200B;複選框並保存。
1. 指定要在&#x200B;**允許的根**&#x200B;中複製的節點路徑。
1. 對每個&#x200B;**publish**&#x200B;例項重複。

   ![隊列代理——事實](assets/queue-agents-fact.png)

### Adobe花崗岩分佈——比較觀察器工廠{#adobe-granite-distribution-diff-observer-factory}

此設定會同步發佈者的群組成員資格。
如果變更某個發佈者中的群組成員資格並未更新其他發佈者的成員資格，請確定**ref:members**&#x200B;已新增至&#x200B;**已搜尋的屬性名稱**。

要確保成員同步：

1. 以管理員權限登入您的作AEM者例項。
1. 訪問[Web控制台](https://helpx.adobe.com/experience-manager/6-4/help/sites-deploying/configuring-osgi.html)。

   例如，[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)。

1. 找到&#x200B;**Adobe花崗岩分佈——比較觀察器工廠**。
1. 選取要開啟以進行編輯的現有設定（鉛筆圖示）。

   驗證&#x200B;**代理名：socialpubsync -reverse**。

1. 選中&#x200B;**Enabled**&#x200B;複選框。
1. 指定&#x200B;**rep:members**&#x200B;作為&#x200B;**lookdproperties names**&#x200B;和Save中propertyName的說明。

   ![diff-obs](assets/diff-obs.png)

### Apache Sling Distribution Trigger - Scheduled Triggers Factory {#apache-sling-distribution-trigger-scheduled-triggers-factory}

此設定可讓您設定輪詢間隔（在輪詢間隔後，發佈者會被Ping化，而作者會提取變更），以同步發佈者的變更。

作者會每30秒（預設值）對發行者進行投票。 如果資料夾`/var/sling/distribution/packages/  socialpubsync -  vlt /shared`中存在任何軟體包，則它將讀取這些軟體包並將其安裝在其他發佈器上。

要更改輪詢間隔：

1. 以管理員權限登入您的作AEM者例項。
1. 訪問[Web控制台](/help/sites-deploying/configuring-osgi.md)，例如[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. 找到&#x200B;**Apache Sling Distribution Trigger - Scheduled Triggers Factory**

   * 選取要開啟以進行編輯的現有設定（鉛筆圖示）。

      驗證&#x200B;**socialpubsync -scheduled-trigger**

   * 將「間隔」（以秒為單位）設定為所需間隔並保存。

   ![scheduled-trigger](assets/scheduled-trigger.png)

### AEM Communities用戶同步偵聽器{#aem-communities-user-sync-listener}

若是Sling散發中訂閱與後續有差異的問題，請檢查下列屬性是否已設定在&#x200B;**AEM Communities使用者同步接聽程式**&#x200B;組態中：

* NodeTypes
* 可忽略屬性
* 可忽略節點
* DistributedFolders

若要同步訂閱、追蹤和通知

在每個AEM發佈例項上：

1. 以管理員權限登入。
1. 訪問[Web控制台](/help/sites-deploying/configuring-osgi.md)。 例如，[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)。
1. 找到&#x200B;**AEM Communities用戶同步偵聽器**。
1. 選取要開啟以進行編輯的現有設定（鉛筆圖示）

   驗證名稱：**socialpubsync -scheduled-trigger**

1. 設定以下&#x200B;**NodeTypes**:

   `rep:User`

   `nt:unstructured`

   `nt:resource`

   `rep:ACL`

   `sling:Folder`

   `sling:OrderedFolder`

   此屬性中指定的節點類型將同步，不同發佈者之間會同步通知資訊（部落格和後面的設定）。

1. 在&#x200B;**DistributedFolders**&#x200B;中添加要同步的所有資料夾。 例如，

   `segments/scoring`

   `social/relationships`

   `activities`

1. 將&#x200B;**inconobalenodes**&#x200B;設為：

   `.tokens`

   `system`

   `rep:cache` （由於我們使用嚴格作業，因此不需要將此節點同步至不同的發佈者）。

   ![user-sync-listner](assets/user-sync-listner.png)

### 唯一Sling ID {#unique-sling-id}

AEMauthor instance使用Sling ID來識別資料來自何處，以及它需要（或不需要）將套件傳回給哪些發佈者。

請確定發佈農場中的所有發佈者都有唯一的Sling ID。 如果Sling ID與發佈群中多個發佈例項的相同，則使用者同步將失敗。 由於作者不知道要從何處擷取套件，以及要在何處安裝套件。

若要確保發佈群組中發佈者的唯一Sling ID，請在每個發佈例項上：

1. 瀏覽至[https://_host:port_/system/console/status-slingsettings](https://localhost:4503/system/console/status-slingsettings)。
1. 檢查&#x200B;**Sling ID**&#x200B;的值。

   ![slingid](assets/slingid.png)

   如果發佈例項的Sling ID符合任何其他發佈例項的Sling ID，則：

1. 停止其中一個具有相符Sling ID的發佈例項。
1. 在`crx-quickstart/launchpad/felix`目錄中，搜索並刪除名為&#x200B;*sling.id.file.*&#x200B;的檔案

   例如，在Linux系統上：

   `rm -i $(find . -type f -name sling.id.file)`

   例如，在Windows系統上：

   使用Windows檔案總管並搜尋`sling.id.file`

1. 啟動發佈例項。 在啟動時，會指派新的Sling ID。
1. 驗證&#x200B;**Sling ID**&#x200B;現在是唯一的。

重複這些步驟，直到所有發佈例項都有唯一的Sling ID。

### Vault Package Builder Factory {#vault-package-builder-factory}

要正確同步更新，必須修改儲存庫包生成器以用於用戶同步。
在`/home/users`中，建立`*/rep:cache`節點。 它是一個快取，用於發現，如果我們查詢節點的主體名稱，則可以直接使用該快取。

如果`rep :cache`節點在發佈商之間同步，則用戶同步可以停止。

為確保每個發佈例項的更新在發佈者之間正確同AEM步：

1. 訪問[Web控制台](/help/sites-deploying/configuring-osgi.md)

   例如，[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)。
1. 找到&#x200B;**Apache Sling Distribution Packaging - Vault Package Builder Factory**

   建立器名稱：socialpubsync-vlt

1. 選擇編輯表徵圖。
1. 添加兩個包節點篩選器：
   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`
1. 政策處理
   * 要用新節點覆蓋現有rep :policy節點，請添加第三個包過濾器：`/home/users|+.*/rep:policy`
   * 要防止策略被分發，請設定：`Acl Handling: IGNORE`

   ![保險儲存包生成器工廠](assets/vault-package-builder-factory.png)

## 疑難排解AEM Communities的Sling散發{#troubleshoot-sling-distribution-in-aem-communities}

如果Sling散發失敗，請嘗試下列除錯步驟：

1. **檢查是否未 [正確添加配置](/help/sites-administering/sync.md#improperconfig)**

   請確定未新增或編輯多個設定，而應編輯現有的預設設定。
1. **檢查配置**

   請確定所有[組態](/help/communities/sync.md#bestpractices)在您的AEM作者實例中已正確設定，如[最佳實務](/help/communities/sync.md#main-pars-header-863110628)中所述。

1. **檢查授權的使用者權限**

   如果軟體包未正確安裝，則檢查在第一個發佈實例中建立的[授權用戶](/help/sites-administering/sync.md#createauthuser)是否具有正確的ACL。

   若要驗證此項，請改變作者例項上的[已建立的授權使用者](/help/sites-administering/sync.md#createauthuser)，而不是變更「Adobe花崗岩分佈——加密密碼傳輸機密提供者」](/help/sites-administering/sync.md#adobegraniteencpasswrd)組態，以使用管理員使用者憑證。 [現在，請嘗試再次安裝軟體包。 如果用戶同步與管理員憑據配合工作正常，則表示建立的發佈用戶沒有適當的ACL。

1. **檢查比較觀察器工廠配置**

   如果發佈群中只有特定節點未同步——例如，群組成員未同步——請確保[Adobe花崗岩分佈——比較觀察器工廠](/help/sites-administering/sync.md#diffobserver)配置已啟用，並且&#x200B;**rep:成員**&#x200B;在&#x200B;**查找的屬性名稱**&#x200B;中設定。

1. **檢查AEM Communities用戶同步偵聽器配置。** 如果已建立的用戶是同步的，但預訂和跟隨的用戶沒有工作，則確保「AEM Communities用戶同步監聽器」配置具有：

   * 節點類型——設定為&#x200B;**rep:User, nt :unstructured**, **nt :resource**, **rep:ACL**, **sling:Folder**&#x200B;和&#x200B;**sling:OrderedFolder**。
   * 可忽略節點——設定為&#x200B;**.token**、**system**&#x200B;和&#x200B;**rep :cache**。
   * 分佈式資料夾——設定到要分發的資料夾。

1. **檢查在發佈實例上建立用戶時生成的日誌**

   如果上述設定已正確設定，但使用者同步仍無法運作，則請檢查在建立使用者時產生的記錄檔。

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
1. 在作AEM者例項上，以管理員權限登入。

   1. 訪問[Web控制台](/help/sites-deploying/configuring-osgi.md)。 例如，[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
   1. 找到設定&#x200B;**Apache Sling Distribution Agent - Sync Agents Factory**。
   1. 取消選中&#x200B;**Enabled**&#x200B;複選框。

      在作者實例上禁用用戶同步時，（導出器和導入器）端點將被禁用，而作者實例是靜態的。 作者不會ping或讀取&#x200B;**vlt**&#x200B;套件。

      現在，如果使用者是在發佈例項上建立，**vlt**&#x200B;套件會建立在&#x200B;*/var/sling/distribution/packages/ socialpubsync - vlt /data*&#x200B;節點中。 如果這些套件是由作者推送至其他服務。 您可以下載並擷取此資料，以檢查所有屬性都推送至其他服務。

1. 前往發行者，並在發佈者上建立使用者。 因此，會建立事件。
1. 檢查在建立用戶時建立的日誌[順序。](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities)
1. 檢查&#x200B;**vlt**&#x200B;套件是否建立於&#x200B;**/var/sling/distribution/packages/socialpubsync-vlt/data**&#x200B;上。
1. 現在，在作者例項上啟AEM用使用者同步。
1. 在發行者上，變更&#x200B;**Apache Sling Distribution Agent - Sync Agents Factory**中的匯出器或匯入器端點。
我們可以下載並擷取封裝資料，以檢查哪些屬性已推送至其他發佈者，以及哪些資料遺失。
