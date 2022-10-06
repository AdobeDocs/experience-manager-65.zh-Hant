---
title: Communities用戶同步
seo-title: Communities User Synchronization
description: 使用者同步如何運作
seo-description: How user synchronization works
uuid: 772b82bd-a66c-4c1d-b80b-dcff77c873a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 97286c2c-f6e3-43ec-b1a9-2abb58616778
docset: aem65
role: Admin
exl-id: ecd30f5d-ad31-4482-96d3-c92f1cf91336
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '2483'
ht-degree: 2%

---

# Communities用戶同步 {#communities-user-synchronization}

## 簡介 {#introduction}

在AEM Communities中，從發佈環境（視設定的權限而定）, *網站訪客* 可 *成員*，建立 *使用者群組*，以及編輯 *成員配置檔案* .

*使用者資料* 是用來指 *使用者*, *使用者設定檔* 和 *使用者群組*.

*成員* 是用來指 *使用者* 註冊於發佈環境，而非在製作環境中註冊的使用者。

如需使用者資料的詳細資訊，請造訪 [管理使用者和使用者群組](/help/communities/users.md).

## 在發佈伺服器陣列間同步使用者 {#synchronizing-users-across-a-publish-farm}

根據設計，在發佈環境中建立的使用者資料不會出現在製作環境中。

在製作環境中建立的大部分使用者資料，都會保留在製作環境中，不會同步或複製到發佈例項。

當 [拓撲](/help/communities/topologies.md) 是 [發佈農場](/help/sites-deploying/recommended-deploys.md#tarmk-farm)，必須與其他發佈例項同步一個發佈例項上的註冊和修改。 成員必須能夠登入並查看其任何發佈節點上的資料。

啟用使用者同步後，系統會自動在伺服器陣列中的發佈執行個體間同步使用者資料。

### 用戶同步設定說明 {#user-sync-setup-instructions}

如需如何在發佈伺服器陣列間啟用同步的詳細逐步指示，請參閱：

* [使用者同步](/help/sites-administering/sync.md)

## 使用者在背景同步  {#user-sync-in-the-background}

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **vlt包**

   此檔案是發佈商上完成的所有變更的zip檔案，需要分發給各發佈商。 發佈伺服器上的更改生成由更改事件偵聽器選擇的事件。 這會建立包含所有變更的vlt套件。

* **分發包**

   其中包含Sling的發佈資訊。 這是關於內容需要分發的位置，以及上次分發的時間的資訊。

## 當…… {#what-happens-when}

### 從Communities Sites控制台發佈站點 {#publish-site-from-communities-sites-console}

在作者上，從發佈社群網站時 [Communities Sites主控台](/help/communities/sites-console.md)，效果是 [複製](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents) 關聯頁面，Sling則會分發動態建立的社群使用者群組，包括其成員資格。

### 使用者是在發佈時建立或編輯設定檔 {#user-is-created-or-edits-profile-on-publish}

根據設計，在發佈環境中建立的使用者和設定檔（例如透過自行註冊、社交登入、LDAP驗證）不會出現在製作環境中。

當拓撲為 [發佈農場](/help/communities/topologies.md) 和使用者同步已正確設定， *使用者* 和 *使用者設定檔* 會使用Sling分送在整個發佈伺服器陣列中同步。

### 在發佈時建立新社群群組 {#new-community-group-is-created-on-publish}

雖然從發佈例項開始，但實際上會發生在製作例項上建立社群群組（這會產生新網站頁面和新使用者群組）。

在程式中，新網站頁面會複製到所有發佈執行個體。 動態建立的社群使用者群組及其成員資格已分發至所有發佈執行個體。

### 使用安全控制台建立用戶或組 {#users-or-user-groups-are-created-using-security-console}

根據設計，在發佈環境中建立的使用者資料不會出現在製作環境中，反之亦然。

當 [使用者管理與安全性](/help/sites-administering/security.md) console用於在發佈環境中新增使用者，使用者同步會將新使用者及其群組成員資格同步至其他發佈執行個體（如有必要）。 使用者同步也會同步透過安全性主控台建立的使用者群組。

### 使用者在發佈時發佈內容 {#user-posts-content-on-publish}

對於使用者產生的內容(UGC)，在發佈執行個體上輸入的資料可透過 [配置的SRP](/help/communities/srp-config.md).

## 最佳實務 {#bestpractices}

依預設，使用者同步為 **停用**. 啟用用戶同步涉及修改 *現有* OSGi設定。 啟用使用者同步後，不應新增任何設定。

使用者同步需仰賴製作環境來管理使用者資料分配，即使使用者資料並非建立在製作上亦然。

**必備條件**

1. 如果使用者和使用者群組已在一個發佈者上建立，建議您 [手動同步](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups) 在配置和啟用用戶同步之前，將用戶資料發送給所有發佈者。

   啟用使用者同步後，只會同步新建立的使用者和群組。

1. 確認已安裝最新程式碼：

   * [AEM平台更新](https://helpx.adobe.com/tw/experience-manager/kb/aem62-available-hotfixes.html)
   * [AEM Communities更新](/help/communities/deploy-communities.md#latestfeaturepack)

若要在AEM Communities上啟用使用者同步，必須進行下列設定。 請確定這些設定正確，以防止Sling內容分送失敗。

### Apache Sling Distribution Agent — 同步代理工廠 {#apache-sling-distribution-agent-sync-agents-factory}

此設定會擷取要在發佈者間同步的內容。 設定位於製作執行個體上。 作者必須追蹤所有發佈者，以及同步所有資訊的位置。

設定中的預設值適用於單一發佈執行個體。 由於使用者同步對同步多個發佈例項（例如對於發佈伺服器陣列）非常有用，因此需要將其他發佈例項新增至設定。

**如何同步內容？**

製作執行個體會偵測發佈者的匯出端點。 每當特定發佈者上建立或更新使用者時(n)，作者就會從其匯出端點取得內容，並 [推播內容](/help/communities/sync.md#main-pars-image-1413756164) 至其他發佈者（n-1，即內容擷取所在的發佈者以外）。

要配置Apache Sling同步代理配置：

1. 以AEM製作執行個體的管理員權限登入。
1. 存取 [Web主控台](/help/sites-deploying/configuring-osgi.md). 例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. 找出 **Apache Sling Distribution Agent — 同步代理工廠**.

   * 選取要開啟以進行編輯的現有設定（鉛筆圖示）。

      驗證名稱： **socialpubsync。**

   * 選取 **已啟用** 核取方塊。
   * 選擇 **使用多個隊列。**
   * 指定 **導出器端點** 和 **匯入工具端點** （您可以新增更多匯出工具和匯入工具端點）。

      這些端點會定義您要從何處取得內容，以及要推送內容的位置。 作者從指定的匯出工具端點擷取內容，並將內容推送至發佈工具（其擷取內容的發佈工具除外）。
   ![sync-agent-fact](assets/sync-agent-fact.png)

### AdobeGranite分發 — 加密密碼傳輸機密提供程式 {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

它可讓作者識別已授權的使用者，即擁有將使用者資料從作者同步到發佈的權限。

此 [已建立授權用戶](/help/sites-administering/sync.md#createauthuser) 在所有發佈執行個體上，可協助發佈者與作者連線，並在作者上設定Sling分送。 此授權使用者具備所有必要條件 [ACL](/help/sites-administering/sync.md#howtoaddacl).

每當要在發佈者上安裝資料或從發佈者擷取資料時，作者就會使用此設定中設定的憑證（使用者名稱和密碼）與發佈者連線。

使用授權使用者將作者與發佈者連線：

1. 以AEM製作執行個體的管理員權限登入。
1. 存取 [Web主控台](/help/sites-deploying/configuring-osgi.md).

   例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
1. 找出 **AdobeGranite分發 — 加密的密碼傳輸機密提供程式。**
1. 選取要開啟以進行編輯的現有設定（鉛筆圖示）。

   驗證屬性 **socialpubsync** - **publishUser.**

1. 將使用者名稱和密碼設為 [授權使用者](/help/sites-administering/sync.md#createauthorizeduser).

   例如， **usersync — 管理員**

![granite-passwrd-trans](assets/granite-paswrd-trans.png)

### Apache Sling Distribution Agent — 佇列代理工廠 {#apache-sling-distribution-agent-queue-agents-factory}

此設定用於設定您要在不同發佈者間同步的資料。 在 **允許的根**，則「var/community/distribution/diff」會啟動，而建立的復製程式會從發佈商擷取資料，並將其安裝在其他發佈商上。

要配置要同步的資料（節點路徑），請執行以下操作：

1. 以管理員權限登入您的發佈執行個體。
1. 存取 [Web主控台](/help/sites-deploying/configuring-osgi.md).

   例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. 找出 **Apache Sling Distribution Agent — 佇列代理工廠**.
1. 選取要開啟以進行編輯的現有設定（鉛筆圖示）。

   驗證名稱： **socialpubsync -reverse**

1. 選取 **已啟用** 核取方塊並儲存。
1. 指定要在中複製的節點路徑 **允許的根**.
1. 對每個 **發佈** 例項。

   ![queue-agent-fact](assets/queue-agents-fact.png)

### AdobeGranite分佈 — 差異觀察器工廠 {#adobe-granite-distribution-diff-observer-factory}

此設定會同步各發佈者的群組成員資格。
如果更改某個發佈者中組的成員資格時，不會更新其他發佈者的成員資格，請確保 **ref:members** 新增至 **查找屬性名稱**.

要確保成員同步：

1. 以管理員權限登入您的發佈執行個體。
1. 存取 [Web主控台](/help/sites-deploying/configuring-osgi.md).

   例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

1. 找出 **AdobeGranite分佈 — 差異觀察器工廠**.
1. 選取要開啟以進行編輯的現有設定（鉛筆圖示）。

   驗證 **代理名稱：socialpubsync -reverse**.

1. 選取 **已啟用** 核取方塊。
1. 指定 **rep:members** 作為中屬性名稱的說明 **查找屬性名稱**，並儲存。

   ![diff-obs](assets/diff-obs.png)

### Apache Sling Distribution觸發程式 — 排程觸發程式工廠 {#apache-sling-distribution-trigger-scheduled-triggers-factory}

此設定可讓您設定輪詢間隔（在此間隔內，發佈者會被Ping通，且作者會提取變更），以同步各發佈者的變更。

作者每30秒輪詢一次發佈者（預設）。 如果資料夾中存在任何包 `/var/sling/distribution/packages/  socialpubsync -  vlt /shared`，則會擷取這些套件並安裝至其他發佈者。

更改輪詢間隔：

1. 以AEM製作執行個體的管理員權限登入。
1. 存取 [Web主控台](/help/sites-deploying/configuring-osgi.md)，例如 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. 找出 **Apache Sling Distribution觸發程式 — 排程觸發程式工廠**

   * 選取要開啟以進行編輯的現有設定（鉛筆圖示）。

      驗證 **socialpubsync -scheduled-trigger**

   * 將間隔（以秒為單位）設定為所需間隔並保存。

   ![排程觸發器](assets/scheduled-trigger.png)

### AEM Communities使用者同步接聽程式 {#aem-communities-user-sync-listener}

如需Sling分送中訂閱與後續項目有所差異的問題，請檢查 **AEM Communities使用者同步接聽程式** 設定：

* NodeTypes
* 可忽略屬性
* 可忽略節點
* DistributedFolders

若要同步訂閱、追蹤和通知

在每個AEM發佈例項上：

1. 以管理員權限登入。
1. 存取 [Web主控台](/help/sites-deploying/configuring-osgi.md). 例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. 找出 **AEM Communities使用者同步接聽程式**.
1. 選取要開啟以進行編輯的現有設定（鉛筆圖示）

   驗證名稱： **socialpubsync -scheduled-trigger**

1. 設定下列項目 **NodeTypes**:

   `rep:User`

   `nt:unstructured`

   `nt:resource`

   `rep:ACL`

   `sling:Folder`

   `sling:OrderedFolder`

   此屬性中指定的節點類型將同步，並且通知資訊（隨後是部落格和配置）會在不同發佈者之間同步。

1. 在中添加要同步的所有資料夾 **DistributedFolders**. 例如，

   `segments/scoring`

   `social/relationships`

   `activities`

1. 設定 **無葉節** 至：

   `.tokens`

   `system`

   `rep:cache` （由於我們使用黏著工作階段，因此不需要將此節點同步至不同的發佈者）。

   ![user-sync-listner](assets/user-sync-listner.png)

### 唯一Sling ID {#unique-sling-id}

AEM製作例項使用Sling ID來識別資料傳回的位置，以及發佈商需要（或不需要）將套件傳回的位置。

確認發佈伺服器陣列中的所有發佈者都有唯一的Sling ID。 如果Sling ID在發佈伺服器陣列中用於多個發佈執行個體相同，則使用者同步將會失敗。 由於作者不知道要從何處擷取套件，以及要在何處安裝套件。

若要確保發佈伺服器陣列中發佈者的唯一Sling ID，請在每個發佈執行個體上：

1. 瀏覽至 [https://_主機：埠_/system/console/status-slingsettings](https://localhost:4503/system/console/status-slingsettings).
1. 檢查 **Sling ID**.

   ![slid](assets/slingid.png)

   如果發佈例項的Sling ID符合任何其他發佈例項的Sling ID，則：

1. 停止具有相符Sling ID的其中一個發佈執行個體。
1. 在 `crx-quickstart/launchpad/felix` 目錄，搜索並刪除名為 *sling.id.file。*

   例如，在Linux系統上：

   `rm -i $(find . -type f -name sling.id.file)`

   例如，在Windows系統上：

   使用Windows資源管理器並搜索 `sling.id.file`

1. 啟動發佈例項。 啟動時，系統會為其指派新的Sling ID。
1. 驗證 **Sling ID** 現在是唯一的。

重複這些步驟，直到所有發佈執行個體都有唯一的Sling ID。

### 保管庫包生成器工廠 {#vault-package-builder-factory}

要正確同步更新，必須修改保管庫包生成器以便用戶同步。
在 `/home/users`, `*/rep:cache` 節點。 它是一個快取，用於發現如果我們查詢節點的主名，則可以直接使用此快取。

若 `rep :cache` 節點會在發佈者之間同步。

為確保在各發佈者之間正確同步更新，請在每個AEM發佈例項上：

1. 存取 [Web主控台](/help/sites-deploying/configuring-osgi.md)

   例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).
1. 找出 **Apache Sling Distribution Packaging - Vault Package Builder Factory**

   產生器名稱：socialpubsync-vlt

1. 選取編輯圖示。
1. 添加兩個包節點篩選器：
   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`
1. 策略處理
   * 要用新節點覆蓋現有的rep:policy節點，請添加第三個包篩選器： `/home/users|+.*/rep:policy`
   * 為防止策略分發，請設定： `Acl Handling: IGNORE`

   ![保管包生成器工廠](assets/vault-package-builder-factory.png)

## 疑難排解AEM Communities中的Sling散發 {#troubleshoot-sling-distribution-in-aem-communities}

如果Sling發佈失敗，請嘗試下列除錯步驟：

1. **檢查 [未正確新增配置](/help/sites-administering/sync.md#improperconfig)**

   請確定未新增或編輯多個設定，而是應編輯現有的預設設定。
1. **檢查配置**

   確保 [配置](/help/communities/sync.md#bestpractices) 可在您的AEM製作例項中適當設定，如 [最佳實務](/help/communities/sync.md#main-pars-header-863110628).

1. **檢查授權的使用者權限**

   如果未正確安裝軟體包，請檢查 [授權使用者](/help/sites-administering/sync.md#createauthuser) 在第一個Publish例項中建立的ACL正確無誤。

   若要驗證，而非 [已建立授權使用者](/help/sites-administering/sync.md#createauthuser) 變更 [AdobeGranite分發 — 加密密碼傳輸機密提供程式](/help/sites-administering/sync.md#adobegraniteencpasswrd) 在製作例項上進行設定，以使用管理員使用者憑證。 現在，請嘗試再次安裝程式包。 如果使用者同步可搭配管理員憑證正常運作，則表示建立的發佈使用者沒有適當的ACL。

1. **檢查比較觀察器工廠配置**

   如果發佈伺服器陣列中只有特定節點未同步（例如，群組成員未同步），請確保 [AdobeGranite分佈 — 差異觀察器工廠](/help/sites-administering/sync.md#diffobserver) 設定已啟用， **代表：成員** 設定於 **查找屬性名稱**.

1. **檢查AEM Communities用戶同步監聽器配置。** 如果已建立的使用者已同步，但訂閱和後續項目無法運作，請確定AEM Communities使用者同步接聽程式設定有：

   * 節點類型 — 設定為 **rep:User, nt:unstructured**, **nt:resource**, **rep:ACL**, **sling:Folder**，和 **sling:OrderedFolder**.
   * 可忽略節點 — 設定為 **.token**, **系統**，和 **rep:cache**.
   * 分佈式資料夾 — 設定到要分佈的資料夾。

1. **檢查在發佈執行個體上建立使用者時產生的記錄**

   如果上述設定已適當設定，但使用者同步無法運作，請檢查建立使用者時產生的記錄。

   檢查記錄檔的順序是否相同，如下所示：

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

除錯：

1. 禁用用戶同步：
1. 在AEM製作例項上，使用管理員權限登入。

   1. 存取 [Web主控台](/help/sites-deploying/configuring-osgi.md). 例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. 找出設定 **Apache Sling Distribution Agent — 同步代理工廠**.
   1. 取消選取 **已啟用** 框。

      在製作執行個體上停用使用者同步時，會停用（匯出工具和匯入工具）端點，且製作執行個體為靜態。 此 **vlt** 製作不會ping或擷取套件。

      現在，如果使用者是在發佈執行個體上建立，則 **vlt** 套件建立於 */var/sling/distribution/packages/ socialpubsync - vlt/data* 節點。 如果作者將這些套件推送至其他服務。 您可以下載並擷取此資料，以檢查所有屬性都推送至其他服務。

1. 前往發佈者，然後在發佈者上建立使用者。 因此，會建立事件。
1. 檢查 [記錄順序](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities)，建立時建立。
1. 檢查 **vlt** 套件建立於 **/var/sling/distribution/packages/socialpubsync-vlt-data**.
1. 現在，在AEM製作例項上啟用使用者同步。
1. 在發佈者上，在 **Apache Sling Distribution Agent — 同步代理工廠**.
我們可以下載並擷取套件資料，以檢查哪些屬性已推送至其他發佈者，以及哪些資料已遺失。
