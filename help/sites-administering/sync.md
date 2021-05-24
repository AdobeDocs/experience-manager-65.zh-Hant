---
title: 使用者同步
seo-title: 使用者同步
description: 了解AEM中的使用者同步。
seo-description: 了解AEM中的使用者同步。
uuid: 0a519daf-21b7-4adc-b419-eeb8c404c54f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: c061b358-8c0d-40d3-8090-dc9800309ab3
docset: aem65
exl-id: 89f55598-e749-42b8-8f2a-496f45face66
feature: 安全性
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '2437'
ht-degree: 2%

---

# 用戶同步{#user-synchronization}

## 簡介 {#introduction}

當部署為[publish farm](/help/sites-deploying/recommended-deploys.md#tarmk-farm)時，成員需要能夠登錄並查看其任何發佈節點上的資料。

製作環境不需要在發佈環境中建立的使用者和使用者群組（使用者資料）。

在製作環境中建立的大部分使用者資料，都會保留在製作環境中，而非複製到發佈例項。

一個發佈執行個體上進行的註冊和修改必須與其他發佈執行個體同步，才能存取相同的使用者資料。

自AEM 6.1起，當啟用使用者同步時，系統會自動在伺服器陣列中的發佈執行個體間同步使用者資料，且不會在製作時建立。

## Sling分發{#sling-distribution}

使用者資料及其[ACL](/help/sites-administering/security.md)會儲存在[Oak Core](/help/sites-deploying/platform.md)（Oak JCR下方的層）中，並使用[Oak API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/oak/api/package-tree.html)存取。 若是不經常更新，則使用[Sling Content Distribution](https://github.com/apache/sling/blob/trunk/contrib/extensions/distribution/README.md)（Sling散發）將使用者資料與其他發佈執行個體同步是合理的。

使用Sling分送來同步使用者，與傳統復寫相比的優點如下：

* *在發佈時建*&#x200B;立的使 *用者、使* 用者設定 ** 檔和使用者群組不會在作者上建立

* Sling分送會在jcr事件中設定屬性，因此可在發佈端事件接聽程式中運作，而不需擔心無限復寫回圈
* Sling發佈只會將使用者資料傳送至非原始發佈例項，消除不必要的流量
* [](/help/sites-administering/security.md) 同步中包含用戶節點中的ACLset

>[!NOTE]
>
>如果需要工作階段，建議您使用SSO解決方案或使用黏著工作階段，並讓客戶在切換至其他發佈者時登入。

>[!CAUTION]
>
>即使啟用了用戶同步，也不支援&#x200B;***administrators***&#x200B;組的同步。 相反，「導入差異」失敗將記錄在錯誤日誌中。
>
>因此，當部署為發佈伺服器陣列時，如果將使用者新增至***administrators**&#x200B;群組或從中移除，則必須在每個發佈執行個體上手動進行修改。

## 啟用用戶同步{#enable-user-sync}

>[!NOTE]
>
>預設情況下，用戶同步為`disabled`。
>
>啟用用戶同步涉及修改&#x200B;*existing* OSGi配置。
>
>啟用使用者同步後，不應新增任何設定。

使用者同步需仰賴製作環境來管理使用者資料分配，即使使用者資料並非建立在製作上亦然。 大部分（但並非全部）的設定會在製作環境中進行，每個步驟都可清楚識別要在製作或發佈上執行。

以下是啟用用戶同步所需的步驟，後面是[Troubleshooting](#troubleshooting)部分：

### 必備條件 {#prerequisites}

1. 如果已在一個發佈商上建立了用戶和用戶組，建議在配置和啟用用戶同步之前，手動將[用戶資料同步到所有發佈商。](#manually-syncing-users-and-user-groups)

啟用使用者同步後，只會同步新建立的使用者和群組。

1. 確認已安裝最新程式碼：

* [AEM平台更新](https://helpx.adobe.com/tw/experience-manager/kb/aem62-available-hotfixes.html)
* [AEM Communities更新](/help/communities/deploy-communities.md#latestfeaturepack)

### 1. Apache Sling Distribution Agent — 同步代理工廠{#apache-sling-distribution-agent-sync-agents-factory}

**啟用用戶同步**

* **論作者**

   * 以管理員權限登入
   * 訪問[Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * 找到`Apache Sling Distribution Agent - Sync Agents Factory`

      * 選取要開啟以進行編輯的現有設定（鉛筆圖示）
驗證`name`:**`socialpubsync`**

      * 選中`Enabled`複選框
      * 選擇`Save`


![](assets/chlimage_1-20.png)

### 2.建立授權用戶 {#createauthuser}

**設**
定權限此授權使用者將用於步驟3，以在作者上設定Sling散發。

* **每個發佈例項**

   * 以管理員權限登入
   * 訪問[安全控制台](/help/sites-administering/security.md)

      * 例如， [https://localhost:4503/useradmin](https://localhost:4503/useradmin)
   * 建立新用戶

      * 例如， `usersync-admin`
   * 將此用戶添加到&#x200B;**`administrators`**&#x200B;用戶組
   * [將此用戶的ACL添加到/home](#howtoaddacl)

      * `Allow jcr:all` 限制  `rep:glob=*/activities/*`



>[!CAUTION]
>
>必須建立新用戶。
>
>* 指派的預設用戶為&#x200B;**`admin`**。
>* 請勿使用`communities-user-admin user.`

>



#### 如何添加ACL {#addacls}

* 存取CRXDE Lite

   * 例如， [https://localhost:4503/crx/de](https://localhost:4503/crx/de)

* 選擇`/home`節點
* 在右窗格中，選擇`Access Control`頁簽
* 選擇`+`按鈕以添加ACL條目

   * **主要**: *搜索為用戶同步建立的用戶*
   * **類型**:  `Allow`
   * **權限**:  `jcr:all`
   * **** 限制表示：glob:  `*/activities/*`
   * 選擇&#x200B;**OK**

* 選擇&#x200B;**保存全部**

![](assets/chlimage_1-21.png)

另請參閱

* [訪問權限管理](/help/sites-administering/user-group-ac-admin.md#access-right-management)
* 疑難排解小節[在響應處理期間修改操作異常](#modify-operation-exception-during-response-processing)。

### 3.AdobeGranite分發 — 加密密碼傳輸機密提供程式 {#adobegraniteencpasswrd}

**設定權限**

在所有發佈執行個體上建立授權使用者(**`administrators`**使用者群組的成員)後，就必須在作者上將該授權使用者識別為具有將使用者資料從作者同步至發佈的權限。

* **論作者**

   * 以管理員權限登入
   * 訪問[Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * 找到`com.adobe.granite.distribution.core.impl.CryptoDistributionTransportSecretProvider.name`
   * 選取要開啟以進行編輯的現有設定（鉛筆圖示）
驗證`property name`:**`socialpubsync-publishUser`**

   * 將使用者名稱和密碼設為步驟2中發佈時建立的[授權使用者](#createauthuser)

      * 例如， `usersync-admin`


![](assets/chlimage_1-22.png)

### 4. Apache Sling Distribution Agent - Queue Agent Factory {#apache-sling-distribution-agent-queue-agents-factory}

**啟用用戶同步**

* **發佈時**:

   * 以管理員權限登入
   * 訪問[Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)
   * 找到`Apache Sling Distribution Agent - Queue Agents Factory`

      * 選取要開啟以進行編輯的現有設定（鉛筆圖示）
驗證`Name`:`socialpubsync-reverse`

      * 選中`Enabled`複選框
      * 選擇`Save`
   * **對每個發佈執行個體**復



![](assets/chlimage_1-23.png)

### 5.Adobe Social同步 — 比較觀察器工廠 {#diffobserver}

**啟用組同步**

* **在每個發佈例項上**:

   * 以管理員權限登入
   * 訪問[Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)
   * 找到&#x200B;**`Adobe Social Sync - Diff Observer Factory`**

      * 選取要開啟以進行編輯的現有設定（鉛筆圖示）

         驗證 `agent name`: `socialpubsync-reverse`

      * 選中`Enabled`複選框
      * 選擇`Save`


![](assets/screen-shot_2019-05-24at090809.png)

### 6. Apache Sling Distribution觸發程式 — 排程觸發程式工廠{#apache-sling-distribution-trigger-scheduled-triggers-factory}

**（可選）修改輪詢間隔**

依預設，作者每30秒會輪詢一次變更。 要更改此間隔：

* **論作者**

   * 以管理員權限登入
   * 訪問[Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * 找到`Apache Sling Distribution Trigger - Scheduled Triggers Factory`

      * 選取要開啟以進行編輯的現有設定（鉛筆圖示）

         * 驗證 `Name`: `socialpubsync-scheduled-trigger`
      * 將`Interval in Seconds`設定為所需間隔
      * 選擇`Save`



![](assets/chlimage_1-24.png)

## 配置多個發佈實例{#configure-for-multiple-publish-instances}

預設設定適用於單一發佈執行個體。 由於啟用用戶同步的原因是同步多個發佈實例（例如對於發佈場），因此需要將其他發佈實例添加到同步代理工廠。

### 7. Apache Sling Distribution Agent — 同步代理工廠{#apache-sling-distribution-agent-sync-agents-factory-1}

**新增發佈例項：**

* **論作者**

   * 以管理員權限登入
   * 訪問[Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如， [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
   * 找到`Apache Sling Distribution Agent - Sync Agents Factory`

      * 選取要開啟以進行編輯的現有設定（鉛筆圖示）
驗證`Name`:`socialpubsync`


![](assets/chlimage_1-25.png)

* **導出**
器端點每個發佈器都應有一個導出器端點。例如，如果有2個發佈者，localhost:4503和4504，則應有2個項目：

   * `https://localhost:4503/libs/sling/distribution/services/exporters/socialpubsync-reverse`
   * `https://localhost:4504/libs/sling/distribution/services/exporters/socialpubsync-reverse`

* **匯入**
工具端點每個發佈工具都應有匯入工具端點。例如，如果有2個發佈者，localhost:4503和4504，則應有2個項目：

   * `https://localhost:4503/libs/sling/distribution/services/importers/socialpubsync`
   * `https://localhost:4504/libs/sling/distribution/services/importers/socialpubsync`

* 選擇`Save`

### 8.AEM Communities用戶同步偵聽器{#aem-communities-user-sync-listener}

**（可選）同步其他JCR節點**

如果有需要在多個發佈執行個體間同步的自訂資料，則：

* **在每個發佈例項上**:

   * 以管理員權限登入
   * 訪問[Web控制台](/help/sites-deploying/configuring-osgi.md)

      * 例如， `https://localhost:4503/system/console/configMgr`
   * 找到`AEM Communities User Sync Listener`
   * 選取要開啟以進行編輯的現有設定（鉛筆圖示）
驗證`Name`:`socialpubsync-scheduled-trigger`


![](assets/chlimage_1-26.png)

* **節**
點類型這是要同步的節點類型清單。此處需要列出sling:Folder以外的任何節點類型（sling:folder需另行處理）。
要同步的節點類型的預設清單：

   * rep:User
   * nt:unstructured
   * nt:resource

* **可忽**
略的屬性這是在檢測到任何更改時將忽略的屬性清單。對這些屬性所做的更改可能會作為其他更改的副作用而同步（因為同步始終在節點級別），但對這些屬性所做的更改本身不會觸發同步。
要忽略的預設屬性：

   * cq:lastModified

* **可忽略**
的節點子路徑，在同步期間將完全忽略。這些子路徑下的任何內容將隨時同步。
要忽略的預設節點：

   * .token
   * 系統

* **分佈式**
資料夾大多數sling：資料夾會被忽略，因為不需要同步。此處列出幾個例外。
要同步的預設資料夾

   * 區段/計分
   * 社交/關係
   * 活動

### 9.唯一Sling ID {#unique-sling-id}

>[!CAUTION]
>
>如果Sling ID在兩個或多個發佈執行個體之間相符，則使用者群組同步將會失敗。

如果Sling ID在發佈伺服器陣列中用於多個發佈執行個體相同，則不會同步使用者群組。

若要驗證所有Sling ID值是否不同，請在每個發佈執行個體上：

1. 瀏覽`http://<host>:<port>/system/console/status-slingsettings`
1. 檢查&#x200B;**Sling ID**&#x200B;的值

![](assets/chlimage_1-27.png)

如果發佈例項的Sling ID符合任何其他發佈例項的Sling ID，則：

1. 停止具有相符Sling ID的其中一個發佈執行個體
1. 在crx-quickstart/launchpad/felix目錄中

   * 搜索並刪除名為&#x200B;*sling.id.file*&#x200B;的檔案

      * 例如，在Linux系統上：
         `rm -i $(find . -type f -name sling.id.file)`

      * 例如，在Windows系統上：
         `use windows explorer and search for *sling.id.file*`

1. 啟動發佈例項

   * 啟動時，系統會為其指派新的Sling ID

1. 驗證&#x200B;**Sling ID**&#x200B;現在是唯一的

重複這些步驟，直到所有發佈執行個體都有唯一的Sling ID。

## 保管庫包生成器工廠{#vault-package-builder-factory}

為了正確同步更新，必須修改保管包生成器以便用戶同步：

* 每個AEM發佈例項
* 訪問[Web控制台](/help/sites-deploying/configuring-osgi.md)

   * 例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* 找到`Apache Sling Distribution Packaging - Vault Package Builder Factory`

   * `Builder name: socialpubsync-vlt`

* 選取「編輯」圖示
* 新增兩個`Package Node Filters`:

   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`

* 策略處理：

   * 要用新節點覆蓋現有的rep:policy節點，請添加第三個包篩選器：

      * `/home/users|+.*/rep:policy`
   * 防止策略被分發，請設定

      * `Acl Handling:` `IGNORE`


![保管庫包生成器工廠](assets/vault-package-builder-factory.png)

## ... {#what-happens-when}時會發生什麼事

### 在發佈時自註冊或編輯配置檔案{#user-self-registers-or-edits-profile-on-publish}

根據設計，在發佈環境中建立的使用者和設定檔（自行註冊）不會出現在製作環境中。

當拓撲為[publish farm](/help/sites-deploying/recommended-deploys.md#tarmk-farm)且已正確配置用戶同步時，*user *和&#x200B;*user profile*&#x200B;會使用Sling分發在整個發佈場中同步。

### 使用安全控制台{#users-or-user-groups-are-created-using-security-console}建立用戶或組

根據設計，在發佈環境中建立的使用者資料不會出現在製作環境中，反之亦然。

當使用[使用者管理與安全性](/help/sites-administering/security.md)控制台在發佈環境中新增使用者時，使用者同步會將新使用者及其群組成員資格同步至其他發佈執行個體（如有必要）。 使用者同步也會同步透過安全性主控台建立的使用者群組。

## 疑難排解 {#troubleshooting}

### 如何讓使用者離線同步{#how-to-take-user-sync-offline}

若要讓使用者同步離線，若要[移除發佈者](#how-to-remove-a-publisher)或[手動同步資料](#manually-syncing-users-and-user-groups)，發佈佇列必須空白且安靜。

要檢查分發隊列的狀態，請執行以下操作：

* 在作者上：

   * 使用[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)

      * 在`/var/sling/distribution/packages`中查找條目

         * 使用模式`distrpackage_*`命名的資料夾節點
   * 使用[包管理器](/help/sites-administering/package-manager.md)

      * 查找掛起的包（尚未安裝）

         * 以模式`socialpubsync-vlt*`命名
         * 由`communities-user-admin`建立


當分發隊列為空時，禁用用戶同步：

* 論作者

   * *取消勾選*[Apache Sling Distribution Agent — 同步代理工廠](#apache-sling-distribution-agent-sync-agents-factory)的`Enabled`核取方塊

完成任務後，要重新啟用用戶同步：

* 論作者

   * 勾選[Apache Sling Distribution Agent — 同步代理工廠](#apache-sling-distribution-agent-sync-agents-factory)的`Enabled`核取方塊

### 使用者同步診斷 {#user-sync-diagnostics}

用戶同步診斷是一種工具，用於檢查配置並嘗試識別任何問題。

在作者上，只需從主控台導覽至&#x200B;**工具、操作、診斷、使用者同步診斷。**

只要進入用戶同步診斷控制台，就會顯示結果。

當未啟用用戶同步時，將顯示以下內容：

![](assets/chlimage_1-28.png)

#### 如何運行發佈者診斷程式{#how-to-run-diagnostics-for-publishers}

從製作環境執行診斷程式時，傳遞/失敗結果將包含[INFO]區段，顯示已設定的發佈執行個體清單以供確認。

清單中包含每個發佈執行個體的URL，該執行個體將對該執行個體執行診斷。 url參數`syncUser`附加至診斷URL，其值設定為在[步驟2](#createauthuser)中建立的&#x200B;*授權同步用戶*。

**注意**:在啟動URL之前，已授 *權的* 同步使用者必須已登入該發佈執行個體。

![](assets/chlimage_1-29.png)

### 未正確添加{#configuration-improperly-added}配置

當使用者同步無法運作時，最常見的問題是其他設定是&#x200B;*added*。 *existing *default configuration hould be a *edited*（*現有*預設配置應為edited）。

以下是編輯預設設定在Web主控台中的顯示方式檢視。 如果出現多個執行個體，應移除新增的設定。

#### （作者）一個Apache Sling Distribution Agent — 同步代理工廠{#author-one-apache-sling-distribution-agent-sync-agents-factory}

![](assets/chlimage_1-30.png)

#### （作者）一個Apache Sling Distribution Transport憑證 — 以DistributionTransportSecretProvider {#author-one-apache-sling-distribution-transport-credentials-user-credentials-based-distributiontransportsecretprovider}為基礎的使用者憑證

![](assets/chlimage_1-31.png)

#### （發佈）一個Apache Sling Distribution Agent — 佇列代理工廠{#publish-one-apache-sling-distribution-agent-queue-agents-factory}

![](assets/chlimage_1-32.png)

#### （發佈）一個Adobe Social同步 — 比較觀察器工廠{#publish-one-adobe-social-sync-diff-observer-factory}

![](assets/chlimage_1-33.png)

#### （作者）一個Apache Sling Distribution觸發程式 — 排程觸發程式工廠{#author-one-apache-sling-distribution-trigger-scheduled-triggers-factory}

![](assets/chlimage_1-34.png)

### 在響應處理期間修改操作異常{#modify-operation-exception-during-response-processing}

如果記錄中顯示下列項目：

`org.apache.sling.servlets.post.impl.operations.ModifyOperation Exception during response processing.`

`java.lang.IllegalStateException: This tree does not exist`

然後確認區段[2。 正確遵循「建立授權用戶」](#createauthuser)。

本節說明如何建立已授權使用者（此使用者存在於所有發佈執行個體上），以及在作者的「機密提供者」OSGi設定中識別他們。 預設情況下，用戶為`admin`。

授權的使用者應成為&#x200B;**`administrators`**&#x200B;使用者群組的成員，該群組的權限不應變更。

授權的使用者應在所有發佈執行個體上明確擁有下列權限和限制：

| **路徑** | **jcr:all** | **rep:glob** |
|---|---|---|
| /home | X | */活動/* |
| /home/users | X | */活動/* |
| /home/groups | X | */活動/* |

作為`administrators`群組的成員，授權的使用者應具有下列所有發佈執行個體的權限：

| **路徑** | **jcr:all** | **jcr:read** | **rep:write** |
|---|---|---|---|
| /etc/packages/sling/distribution |  |  | X |
| /libs/sling/distribution |  | X |  |
| /var |  |  | X |
| /var/eventing |  | X | X |
| /var/sling/distribution |  | X | X |

### 用戶組同步失敗{#user-group-sync-failed}

如果Sling ID在兩個或多個發佈執行個體之間相符，則使用者群組同步將會失敗。

請參閱[9節。 唯一Sling ID](#unique-sling-id)

### 手動同步使用者和使用者群組{#manually-syncing-users-and-user-groups}

* 在存在用戶和組的發佈商上：

   * [如果啟用，則禁用用戶同步](#how-to-take-user-sync-offline)
   * [建立套](/help/sites-administering/package-manager.md#creating-a-new-package) 件  `/home`

      * 編輯套件時

         * 篩選器索引標籤：添加篩選器：根路徑：`/home`
         * 進階標籤：交流處理：`Overwrite`
   * [匯出套件](/help/sites-administering/package-manager.md#downloading-packages-to-your-file-system)


* 在其他發佈例項上：

   * [匯入套件](/help/sites-administering/package-manager.md#installing-packages)

要配置或啟用用戶同步，請轉至步驟1:[Apache Sling Distribution Agent — 同步代理工廠](#apache-sling-distribution-agent-sync-agents-factory)

### 當發佈者變為不可用{#when-a-publisher-becomes-unavailable}

發佈例項無法使用時，如果日後重新上線，則不應將其移除。 變更會排入發佈者佇列，一旦重新上線，就會處理變更。

如果發佈例項永遠不會重新上線，如果永久離線，則必須移除它，因為佇列累積會在製作環境中造成相當大的磁碟空間使用。

當發佈者關閉時，製作記錄會有類似下列的例外：

```
28.01.2016 15:57:48.475 ERROR
 [pool-12-thread-34-org_apache_sling_distribution_queue_socialpubsync_endpoint1
 (org/apache/sling/distribution/queue/socialpubsync/endpoint1)]
 org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync] could not deliver package distrpackage_1454014575838_a2b45ec8-0400-42f3-bed8-ae09b66381cb
 org.apache.sling.distribution.packaging.DistributionPackageImportException: failed in importing package ...
```

### 如何刪除發佈者{#how-to-remove-a-publisher}

若要從[Apache Sling Distribution Agent - Sync Agent Factory](#apache-sling-distribution-agent-sync-agents-factory)中移除發佈者，發佈佇列必須空白且安靜。

* 在作者上：

   * [讓使用者離線同步](#how-to-take-user-sync-offline)
   * 按照[步驟7](#apache-sling-distribution-agent-sync-agents-factory)從兩個伺服器清單中刪除發佈者：

      * `Exporter Endpoints`
      * `Importer Endpoints`
   * 重新啟用用戶同步

      * 勾選[Apache Sling Distribution Agent — 同步代理工廠](#apache-sling-distribution-agent-sync-agents-factory)的`Enabled`核取方塊
