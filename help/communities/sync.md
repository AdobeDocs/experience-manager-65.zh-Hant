---
title: 社區用戶同步
seo-title: Communities User Synchronization
description: 用戶同步的工作方式
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

# 社區用戶同步 {#communities-user-synchronization}

## 簡介 {#introduction}

在AEM Communities，從發佈環境（取決於配置的權限）, *站點訪問者* 可能 *成員*&#x200B;建立 *用戶組*，編輯 *成員配置檔案* 。

*用戶資料* 是指 *用戶*。 *用戶配置檔案* 和 *用戶組*。

*成員* 是指 *用戶* 在發佈環境中註冊，而不是在作者環境中註冊的用戶。

有關用戶資料的詳細資訊，請訪問 [管理用戶和用戶組](/help/communities/users.md)。

## 在發佈場中同步用戶 {#synchronizing-users-across-a-publish-farm}

按照設計，在發佈環境中建立的用戶資料不會出現在作者環境中。

在作者環境中建立的大多數用戶資料都打算保留在作者環境中，不會同步或複製到發佈實例。

當 [拓撲](/help/communities/topologies.md) 是 [發佈場](/help/sites-deploying/recommended-deploys.md#tarmk-farm)，對一個發佈實例進行的註冊和修改需要與其他發佈實例同步。 成員需要能夠登錄並查看其任何發佈節點上的資料。

啟用用戶同步後，用戶資料將自動在伺服器場中的發佈實例之間同步。

### 用戶同步設定說明 {#user-sync-setup-instructions}

有關如何啟用發佈伺服器場之間的同步的詳細、逐步說明，請參閱：

* [用戶同步](/help/sites-administering/sync.md)

## 用戶在後台同步  {#user-sync-in-the-background}

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **vlt包**

   它是發佈伺服器上完成的所有更改的壓縮檔案，需要在發佈伺服器之間分發。 發佈伺服器上的更改生成由更改事件偵聽器選取的事件。 這將建立包含所有更改的vlt包。

* **分發包**

   它包含Sling的分發資訊。 這是有關內容需要在何處分發以及上次何時分發的資訊。

## 當…… {#what-happens-when}

### 從社區站點控制台發佈站點 {#publish-site-from-communities-sites-console}

在作者中，當從 [社區站點控制台](/help/communities/sites-console.md)，效果是 [複製](/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents) Sling分發動態建立的社區用戶組，包括其成員身份。

### 用戶已建立或在發佈時編輯配置檔案 {#user-is-created-or-edits-profile-on-publish}

按照設計，在發佈環境中建立的用戶和配置檔案（如通過自註冊、社交登錄、LDAP身份驗證）不會出現在作者環境中。

當拓撲為 [發佈場](/help/communities/topologies.md) 和用戶同步已正確配置， *用戶* 和 *用戶配置檔案* 使用Sling分發在發佈場中同步。

### 在發佈時建立新社區組 {#new-community-group-is-created-on-publish}

雖然從發佈實例啟動，但社區組建立實際上會在作者實例上發生，該建立會導致新網站頁和新用戶組。

作為流程的一部分，新網站頁將複製到所有發佈實例。 動態建立的社區用戶組及其成員是Sling分發給所有發佈實例。

### 使用安全控制台建立用戶或用戶組 {#users-or-user-groups-are-created-using-security-console}

按照設計，在發佈環境中建立的用戶資料不會出現在作者環境中，反之亦然。

當 [用戶管理和安全](/help/sites-administering/security.md) 控制台用於在發佈環境中添加新用戶，用戶同步將根據需要將新用戶及其組成員身份與其他發佈實例同步。 用戶同步還將同步通過安全控制台建立的用戶組。

### 用戶在發佈時發佈內容 {#user-posts-content-on-publish}

對於用戶生成的內容(UGC)，通過 [已配置SRP](/help/communities/srp-config.md)。

## 最佳做法 {#bestpractices}

預設情況下，用戶同步為 **禁用**。 啟用用戶同步涉及修改 *現有* OSGi配置。 啟用用戶同步後，不應添加任何新配置。

用戶同步依靠作者環境來管理用戶資料分發，即使用戶資料不是由作者建立的。

**必備條件**

1. 如果用戶和用戶組已在一個發佈伺服器上建立，建議 [手動同步](/help/sites-administering/sync.md#manually-syncing-users-and-user-groups) 在配置和啟用用戶同步之前，將用戶資料發送給所有發佈者。

   啟用用戶同步後，只同步新建立的用戶和組。

1. 確保已安裝最新代碼：

   * [AEM平台更新](https://helpx.adobe.com/tw/experience-manager/kb/aem62-available-hotfixes.html)
   * [AEM Communities更新](/help/communities/deploy-communities.md#latestfeaturepack)

在AEM Communities上啟用用戶同步需要以下配置。 確保這些配置正確，以防止掛起內容分發失敗。

### Apache Sling分發代理 — 同步代理工廠 {#apache-sling-distribution-agent-sync-agents-factory}

此配置將讀取要在發佈器之間同步的內容。 配置在Author實例上。 作者必須跟蹤所有位於此處的發佈者以及同步所有資訊的位置。

配置中的預設值是單個發佈實例的預設值。 由於用戶同步對同步多個發佈實例非常有用，因此需要將其他發佈實例添加到配置中。

**內容如何同步？**

作者實例ping發佈器的導出器終結點。 每當在特定發佈器上建立或更新用戶(n)時，作者將從其導出端點獲取內容， [推送內容](/help/communities/sync.md#main-pars-image-1413756164) 到其他發佈者（n-1，即從中提取內容的發佈者除外）。

要配置Apache Sling同步代理配置：

1. 使用作者實例的管理員權AEM限登錄。
1. 訪問 [Web控制台](/help/sites-deploying/configuring-osgi.md)。 比如說， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
1. 定位 **Apache Sling分發代理 — 同步代理工廠**。

   * 選擇要開啟以進行編輯的現有配置（鉛筆表徵圖）。

      驗證名稱： **社會黨。**

   * 選擇 **已啟用** 複選框。
   * 選擇 **使用多個隊列。**
   * 指定 **導出器終結點** 和 **導入程式終結點** （可以添加更多導出器和導入器端點）。

      這些端點定義了要從何處獲取內容以及要推送內容的位置。 作者從指定的導出器終結點提取內容並將內容推送到發佈器（它從中獲取內容的發佈器除外）。
   ![同步代理事實](assets/sync-agent-fact.png)

### Adobe花崗岩分佈 — 加密密碼傳輸機密提供程式 {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

它使作者能夠識別授權用戶，即具有從作者同步用戶資料到發佈的權限。

的 [已授權用戶建立](/help/sites-administering/sync.md#createauthuser) 在所有發佈實例上幫助發佈者與作者連接並配置作者上的Sling分發。 此授權用戶具有所有必需項 [ACL](/help/sites-administering/sync.md#howtoaddacl)。

無論何時要在發佈伺服器上安裝資料或從發佈伺服器獲取資料，作者都會使用此配置中設定的憑據（用戶名和密碼）與發佈伺服器連接。

要使用授權用戶將作者與發佈者連接：

1. 使用作者實例的管理員權AEM限登錄。
1. 訪問 [Web控制台](/help/sites-deploying/configuring-osgi.md)。

   比如說， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
1. 定位 **Adobe花崗岩分佈 — 加密密碼傳輸機密提供程式。**
1. 選擇要開啟以進行編輯的現有配置（鉛筆表徵圖）。

   驗證屬性 **社會性公共同步** - **publishUser。**

1. 將用戶名和密碼設定為 [授權用戶](/help/sites-administering/sync.md#createauthorizeduser)。

   比如說， **用戶同步 — 管理員**

![花崗岩](assets/granite-paswrd-trans.png)

### Apache Sling分發代理 — 隊列代理工廠 {#apache-sling-distribution-agent-queue-agents-factory}

此配置用於配置要跨發佈伺服器同步的資料。 在中指定的路徑中建立/更新資料時 **允許的根**，激活「var/community/distribution/diff」，建立的復製程式將從發佈伺服器中提取資料並將其安裝到其他發佈伺服器上。

要配置要同步的資料（節點路徑）:

1. 使用發佈實例的管理員權限登錄。
1. 訪問 [Web控制台](/help/sites-deploying/configuring-osgi.md)。

   比如說， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)。

1. 定位 **Apache Sling分發代理 — 隊列代理工廠**。
1. 選擇要開啟以進行編輯的現有配置（鉛筆表徵圖）。

   驗證名稱： **反向**

1. 選擇 **已啟用** 複選框並保存。
1. 指定要在中複製的節點路徑 **允許的根**。
1. 對每個 **發佈** 實例。

   ![排隊代理 — 事實](assets/queue-agents-fact.png)

### Adobe花崗岩分佈 — 差異觀察工廠 {#adobe-granite-distribution-diff-observer-factory}

此配置將同步發佈伺服器的組成員身份。
如果更改某個發佈者中的組成員身份不更新其他發佈者的組成員身份，請確保 **ref:members** 添加到 **查找屬性名稱**。

要確保成員同步：

1. 使用發佈實例的管理員權限登錄。
1. 訪問 [Web控制台](/help/sites-deploying/configuring-osgi.md)。

   比如說， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)。

1. 定位 **Adobe花崗岩分佈 — 差異觀察工廠**。
1. 選擇要開啟以進行編輯的現有配置（鉛筆表徵圖）。

   驗證 **代理名稱：反向**。

1. 選擇 **已啟用** 複選框。
1. 指定 **rep：成員** 作為中屬性Name的說明 **查找屬性名稱**，並保存。

   ![差異obs](assets/diff-obs.png)

### Apache Sling分發觸發器 — 計畫觸發器工廠 {#apache-sling-distribution-trigger-scheduled-triggers-factory}

通過此配置，您可以配置輪詢間隔（在輪詢間隔後，發佈者被ping並由作者提取更改），以在發佈者之間同步更改。

作者每30秒輪詢一次發佈者（預設）。 如果資料夾中存在任何包 `/var/sling/distribution/packages/  socialpubsync -  vlt /shared`然後，它將獲取這些包並將其安裝到其他發佈器上。

要更改輪詢間隔：

1. 使用作者實例的管理員權AEM限登錄。
1. 訪問 [Web控制台](/help/sites-deploying/configuring-osgi.md)，例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. 定位 **Apache Sling分發觸發器 — 計畫觸發器工廠**

   * 選擇要開啟以進行編輯的現有配置（鉛筆表徵圖）。

      驗證 **socialpubsync -scheduledtrigger**

   * 將「間隔（秒）」設定為所需的間隔，然後保存。

   ![調度觸發器](assets/scheduled-trigger.png)

### AEM Communities用戶同步偵聽器 {#aem-communities-user-sync-listener}

有關Sling分發中訂閱和後續訂閱中存在差異的問題，請檢查以下屬性 **AEM Communities用戶同步偵聽器** 設定配置：

* 節點類型
* 可忽略屬性
* 可忽略節點
* 分佈式資料夾

同步訂閱、跟蹤和通知

在每個發AEM布實例上：

1. 使用管理員權限登錄。
1. 訪問 [Web控制台](/help/sites-deploying/configuring-osgi.md)。 比如說， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)。
1. 定位 **AEM Communities用戶同步偵聽器**。
1. 選擇要開啟以進行編輯的現有配置（鉛筆表徵圖）

   驗證名稱： **socialpubsync -scheduledtrigger**

1. 設定以下 **節點類型**:

   `rep:User`

   `nt:unstructured`

   `nt:resource`

   `rep:ACL`

   `sling:Folder`

   `sling:OrderedFolder`

   此屬性中指定的節點類型將同步，通知資訊（隨後是部落格和配置）將在不同的發佈者之間同步。

1. 添加要同步的所有資料夾 **分佈式資料夾**。 例如，

   `segments/scoring`

   `social/relationships`

   `activities`

1. 設定 **無知的頌歌** 至：

   `.tokens`

   `system`

   `rep:cache` （由於我們使用粘滯會話，因此不需要將此節點同步到不同的發佈者）。

   ![用戶同步清單器](assets/user-sync-listner.png)

### 唯一吊帶ID {#unique-sling-id}

作AEM者實例使用Sling ID來標識資料的來源以及它需要（或不需要）將包發回到哪些發佈者。

確保發佈場中的所有發佈者都具有唯一的Sling ID。 如果發佈場中多個發佈實例的Sling ID相同，則用戶同步將失敗。 由於作者不知道從何處獲取軟體包以及在何處安裝軟體包。

要確保發佈場中發佈者的唯一Sling ID，請在每個發佈實例上：

1. 瀏覽到 [https://_主機：埠_/system/console/status slingsettings](https://localhost:4503/system/console/status-slingsettings)。
1. 檢查 **吊帶ID**。

   ![斯萊德](assets/slingid.png)

   如果發佈實例的Sling ID與任何其他發佈實例的Sling ID匹配，則：

1. 停止具有匹配Sling ID的發佈實例之一。
1. 在 `crx-quickstart/launchpad/felix` 目錄，搜索並刪除名為 *sling.id.file。*

   例如，在Linux系統上：

   `rm -i $(find . -type f -name sling.id.file)`

   例如，在Windows系統上：

   使用Windows資源管理器並搜索 `sling.id.file`

1. 啟動發佈實例。 啟動時，將為其分配新的Sling ID。
1. 驗證 **吊帶ID** 現在是獨一無二的。

重複這些步驟，直到所有發佈實例都具有唯一的Sling ID。

### 保管庫包生成器工廠 {#vault-package-builder-factory}

要正確同步更新，必須修改保管庫包生成器以進行用戶同步。
在 `/home/users`的 `*/rep:cache` 建立節點。 它是一個快取，用於發現如果我們查詢某個節點的主體名稱，則可以直接使用該快取。

如果 `rep :cache` 節點在發佈伺服器之間同步。

要確保在每個發佈實例上在發佈伺服器之間正確同步AEM更新，請：

1. 訪問 [Web控制台](/help/sites-deploying/configuring-osgi.md)

   比如說， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)。
1. 查找 **Apache Sling分發包 — Vault包生成器工廠**

   生成器名稱：社會黨。

1. 選擇編輯表徵圖。
1. 添加兩個包節點篩選器：
   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`
1. 策略處理
   * 要用新節點覆蓋現有rep :policy節點，請添加第三個包篩選器： `/home/users|+.*/rep:policy`
   * 要防止分發策略，請設定： `Acl Handling: IGNORE`

   ![保險儲存包生成器工廠](assets/vault-package-builder-factory.png)

## 診斷AEM Communities的Sling分發問題 {#troubleshoot-sling-distribution-in-aem-communities}

如果Sling分發失敗，請嘗試以下調試步驟：

1. **檢查 [未正確添加的配置](/help/sites-administering/sync.md#improperconfig)**

   請確保不添加或編輯多個配置，而應編輯現有預設配置。
1. **檢查配置**

   確保 [配置](/help/communities/sync.md#bestpractices) 在AEM作者實例中設定，如中所述 [最佳做法](/help/communities/sync.md#main-pars-header-863110628)。

1. **檢查授權用戶權限**

   如果軟體包安裝不正確，請檢查 [授權用戶](/help/sites-administering/sync.md#createauthuser) 在第一個發佈實例中建立的ACL正確。

   驗證此項，而不是 [已建立授權用戶](/help/sites-administering/sync.md#createauthuser) 更改 [Adobe花崗岩分佈 — 加密密碼傳輸機密提供程式](/help/sites-administering/sync.md#adobegraniteencpasswrd) 在Author實例上配置以使用Admin用戶憑據。 現在，請嘗試重新安裝軟體包。 如果用戶同步在管理員憑據上工作正常，則表示建立的發佈用戶沒有適當的ACL。

1. **檢查比較觀察器出廠配置**

   如果僅特定節點未在發佈場之間同步 — 例如，組成員未同步 — 則確保 [Adobe花崗岩分佈 — 差異觀察工廠](/help/sites-administering/sync.md#diffobserver) 配置已啟用， **代表：成員** 設定 **查找屬性名稱**。

1. **檢查AEM Communities用戶同步監聽器配置。** 如果已建立的用戶已同步，但訂閱和以下內容未工作，則請確保AEM Communities用戶同步監聽程式配置具有：

   * 節點類型 — 設定為 **rep：用戶， nt：非結構化**。 **nt：資源**。 **rep:ACL**。 **sling：資料夾**, **sling:OrderedFolder**。
   * 可忽略節點 — 設定為 **.標籤**。 **系統**, **rep:cache**。
   * 分佈式資料夾 — 設定為要分發的資料夾。

1. **檢查在發佈實例上建立用戶時生成的日誌**

   如果已適當設定上述配置，但用戶同步不工作，則檢查在用戶建立時生成的日誌。

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

調試：

1. 禁用用戶同步：
1. 在作AEM者實例上，使用管理員權限登錄。

   1. 訪問 [Web控制台](/help/sites-deploying/configuring-osgi.md)。 比如說， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
   1. 找到配置 **Apache Sling分發代理 — 同步代理工廠**。
   1. 取消選擇 **已啟用** 的子菜單。

      在對作者實例禁用用戶同步時，將禁用（導出器和導入器）終結點，並且作者實例是靜態的。 的 **VLT** 檔案包不被作者ping或讀取。

      現在，如果在發佈實例上建立用戶， **VLT** 包建立於 */var/sling/distribution/packages/ socialpubsync - vlt/data* 的下界。 如果這些包被作者推送到其他服務。 您可以下載並提取此資料，以檢查將哪些屬性推送到其他服務。

1. 轉到發佈伺服器，然後在發佈伺服器上建立用戶。 結果，建立事件。
1. 檢查 [日誌順序](/help/communities/sync.md#troubleshoot-sling-distribution-in-aem-communities)，在用戶建立時建立。
1. 檢查 **VLT** 包建立於 **/var/sling/distribution/packages/socialpubsync vlt/data**。
1. 現在，啟用作者實例上AEM的用戶同步。
1. 在發佈伺服器上，在 **Apache Sling分發代理 — 同步代理工廠**。
我們可以下載並提取包資料，以檢查所有屬性被推送到其他發佈器，以及哪些資料丟失。
