---
title: 使用者同步
description: 瞭解AEM中使用者同步的內部運作。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 89f55598-e749-42b8-8f2a-496f45face66
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '2433'
ht-degree: 1%

---


# 使用者同步{#user-synchronization}

## 簡介 {#introduction}

當部署是[發佈伺服器陣列](/help/sites-deploying/recommended-deploys.md#tarmk-farm)時，成員必須能夠登入並在任何Publish節點上檢視其資料。

在製作環境中不需要在發佈環境中建立的使用者和使用者群組（使用者資料）。

在製作環境中建立的大部分使用者資料旨在保留在製作環境中，而非複製到Publish例項。

在一個Publish執行個體上進行的註冊和修改必須與其他Publish執行個體同步，才能存取相同的使用者資料。

自AEM 6.1起，啟用使用者同步時，系統會自動在伺服器陣列中的Publish執行個體間同步使用者資料，而不會在作者上建立使用者資料。

## Sling散佈 {#sling-distribution}

使用者資料及其[ACL](/help/sites-administering/security.md)儲存在Oak JCR下層的[Oak Core](/help/sites-deploying/platform.md)中，並可使用[Oak API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/jackrabbit/oak/api/package-tree.html)存取。 由於不經常更新，因此使用[Sling內容發佈](https://github.com/apache/sling-old-svn-mirror/blob/trunk/contrib/extensions/distribution/README.md) （Sling發佈）將使用者資料與其他Publish執行個體同步是合理的。

與傳統復寫相比，使用Sling散發進行使用者同步的優點包括：

* 在Publish上建立的&#x200B;*使用者*、*使用者設定檔*&#x200B;和&#x200B;*使用者群組*&#x200B;不是在Author上建立的

* Sling散發會設定jcr事件中的屬性，因此可在發佈端事件接聽程式中運作，而不需要擔心無限的復寫回圈
* Sling Distribution只會將使用者資料傳送至非原始Publish例項，消除不必要的流量
* 在使用者節點中設定的[ACL](/help/sites-administering/security.md)包含在同步處理中

>[!NOTE]
>
>如果需要工作階段，建議使用SSO解決方案或使用嚴格工作階段，如果客戶被切換至其他Publish執行個體，請讓他們登入。

>[!CAUTION]
>
>不支援&#x200B;**管理員**&#x200B;群組的同步處理，即使使用者同步處理已啟用。 「匯入差異」的失敗會記錄到錯誤記錄中。
>
>因此，當部署是發佈伺服器陣列時，如果將使用者新增到&#x200B;**管理員**&#x200B;群組或從中移除，則必須在每個Publish執行個體上手動進行修改。

## 啟用使用者同步 {#enable-user-sync}

>[!NOTE]
>
>依預設，使用者同步為`disabled`。
>
>啟用使用者同步涉及修改&#x200B;*現有* OSGi設定。
>
>啟用使用者同步後，不應新增任何設定。

即使使用者資料並非建立在作者上，使用者同步仍仰賴作者環境管理使用者資料分佈。 大部分設定（但並非全部）會在作者環境中進行，且每個步驟都會清楚識別是否要在Author或Publish上執行。

以下是啟用使用者同步所需的步驟，隨後是[疑難排解](#troubleshooting)區段：

### 先決條件 {#prerequisites}

1. 如果使用者和使用者群組已在一個Publish執行個體上建立，建議在設定和啟用使用者同步之前，先將使用者資料[手動同步](#manually-syncing-users-and-user-groups)到所有Publish執行個體。

啟用使用者同步後，只會同步新建立的使用者和群組。

1. 確認已安裝最新程式碼：

* [AEM平台更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html)
* [AEM Communities更新](/help/communities/deploy-communities.md#latestfeaturepack)

### 1. Apache Sling散發代理程式 — 同步代理程式處理站 {#apache-sling-distribution-agent-sync-agents-factory}

**啟用使用者同步**

* 作者&#x200B;**上的**

   * 以系統管理員許可權登入
   * 存取[網頁主控台](/help/sites-deploying/configuring-osgi.md)

      * 例如，[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * 尋找`Apache Sling Distribution Agent - Sync Agents Factory`

      * 選取現有組態，以便開啟它進行編輯（鉛筆圖示）
驗證`name`： **`socialpubsync`**

      * 選取`Enabled`核取方塊
      * 選取`Save`

![Apache Sling散發代理程式](assets/chlimage_1-20.png)

### 2.建立授權使用者 {#createauthuser}

**設定許可權**

在步驟3中使用授權使用者來設定Author上的Sling發佈。

* 每個Publish執行個體上的&#x200B;****

   * 以系統管理員許可權登入
   * 存取[安全性主控台](/help/sites-administering/security.md)

      * 例如，[https://localhost:4503/useradmin](https://localhost:4503/useradmin)

   * 建立使用者

      * 例如，`usersync-admin`

   * 將此使用者新增至&#x200B;**`administrators`**&#x200B;使用者群組
   * [將此使用者的ACL新增至/home](#howtoaddacl)

      * 限製為`rep:glob=*/activities/*`的`Allow jcr:all`

>[!CAUTION]
>
>必須建立新使用者。
>
>* 指派的預設使用者為&#x200B;**`admin`**。
>* 不要使用`communities-user-admin user.`
>

#### 如何新增ACL {#addacls}

* 存取CRXDE Lite

   * 例如，[https://localhost:4503/crx/de](https://localhost:4503/crx/de)

* 選取`/home`節點
* 在右窗格中，選取`Access Control`索引標籤
* 若要新增ACL專案，請選取`+`按鈕

   * **主體**： *搜尋為使用者同步處理建立的使用者*
   * **類型**：`Allow`
   * **許可權**： `jcr:all`
   * **限制** `rep:glob`： `*/activities/*`
   * 選取&#x200B;**確定**

* 選取&#x200B;**全部儲存**

![新增ACL視窗](assets/chlimage_1-21.png)

另請參閱

* [存取許可權管理](/help/sites-administering/user-group-ac-admin.md#access-right-management)
* 疑難排解區段[在回應處理期間修改作業例外狀況](#modify-operation-exception-during-response-processing)。

### 3.AdobeGranite散發 — 加密的密碼傳輸機密提供者 {#adobegraniteencpasswrd}

**設定許可權**

在所有Publish執行個體上建立授權使用者（**`administrators`**&#x200B;使用者群組的成員）後，必須在Author上將該授權使用者識別為具有將使用者資料從Author同步到Publish的許可權。

* 作者&#x200B;**上的**

   * 以系統管理員許可權登入
   * 存取[網頁主控台](/help/sites-deploying/configuring-osgi.md)

      * 例如，[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * 尋找`com.adobe.granite.distribution.core.impl.CryptoDistributionTransportSecretProvider.name`
   * 若要開啟以進行編輯，請選取現有組態（鉛筆圖示）
驗證`property name`： **`socialpubsync-publishUser`**

   * 在步驟2中，將使用者名稱和密碼設定為[在Publish上建立的](#createauthuser)授權使用者

      * 例如，`usersync-admin`

![加密的密碼傳輸機密提供者](assets/chlimage_1-22.png)

### 4. Apache Sling散發代理程式 — 佇列代理程式處理站 {#apache-sling-distribution-agent-queue-agents-factory}

**啟用使用者同步**

* 每個Publish執行個體&#x200B;**上的**：

   * 以系統管理員許可權登入
   * 存取[網頁主控台](/help/sites-deploying/configuring-osgi.md)

      * 例如，[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

   * 尋找`Apache Sling Distribution Agent - Queue Agents Factory`

      * 若要開啟以進行編輯，請選取現有組態（鉛筆圖示）
驗證`Name`： `socialpubsync-reverse`

      * 選取`Enabled`核取方塊
      * 選取`Save`

   * 針對每個Publish執行個體重複&#x200B;**重複**

![佇列代理程式Factory](assets/chlimage_1-23.png)

### 5. Adobe Social同步 — 觀察者工廠差異 {#diffobserver}

**啟用群組同步**

* 每個Publish執行個體&#x200B;**上的**：

   * 以系統管理員許可權登入
   * 存取[網頁主控台](/help/sites-deploying/configuring-osgi.md)

      * 例如，[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

   * 尋找&#x200B;**`Adobe Social Sync - Diff Observer Factory`**

      * 若要開啟以進行編輯，請選取現有組態（鉛筆圖示）

        驗證`agent name`： `socialpubsync-reverse`

      * 選取`Enabled`核取方塊
      * 選取`Save`

![比較觀察者處理站](assets/screen-shot_2019-05-24at090809.png)

### 6. Apache Sling Distribution Trigger — 排程觸發程式Factory {#apache-sling-distribution-trigger-scheduled-triggers-factory}

**（選擇性）修改輪詢間隔**

依預設，作者每30秒輪詢一次變更。 變更此間隔：

* 作者&#x200B;**上的**

   * 以系統管理員許可權登入
   * 存取[網頁主控台](/help/sites-deploying/configuring-osgi.md)

      * 例如，[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * 尋找`Apache Sling Distribution Trigger - Scheduled Triggers Factory`

      * 若要開啟以進行編輯，請選取現有組態（鉛筆圖示）

         * 驗證`Name`： `socialpubsync-scheduled-trigger`

      * 將`Interval in Seconds`設定為所需的間隔
      * 選取`Save`

![排定的觸發程式Factory](assets/chlimage_1-24.png)

## 為多個Publish執行個體進行配置 {#configure-for-multiple-publish-instances}

預設設定適用於單一Publish執行個體。 由於啟用使用者同步的原因是同步多個Publish例項，例如發佈伺服器陣列，因此必須將額外的Publish例項新增至同步代理程式處理站。

### 7. Apache Sling散發代理程式 — 同步代理程式工廠 {#apache-sling-distribution-agent-sync-agents-factory-1}

**新增Publish執行個體：**

* 作者&#x200B;**上的**

   * 以系統管理員許可權登入
   * 存取[網頁主控台](/help/sites-deploying/configuring-osgi.md)

      * 例如，[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

   * 尋找`Apache Sling Distribution Agent - Sync Agents Factory`

      * 若要開啟以進行編輯，請選取現有組態（鉛筆圖示）
驗證`Name`： `socialpubsync`

![同步代理程式處理站](assets/chlimage_1-25.png)

* **匯出工具端點**
每個Publish執行個體都應該有一個匯出工具端點。 例如，如果有2個Publish執行個體localhost：4503和4504，則應該有兩個專案：

   * `https://localhost:4503/libs/sling/distribution/services/exporters/socialpubsync-reverse`
   * `https://localhost:4504/libs/sling/distribution/services/exporters/socialpubsync-reverse`

* **匯入工具端點**
每個Publish例項都應該有匯入工具端點。 例如，如果有2個Publish執行個體localhost：4503和4504，則應該有兩個專案：

   * `https://localhost:4503/libs/sling/distribution/services/importers/socialpubsync`
   * `https://localhost:4504/libs/sling/distribution/services/importers/socialpubsync`

* 選取`Save`

### 8. AEM Communities使用者同步監聽器 {#aem-communities-user-sync-listener}

**（選擇性）同步處理其他JCR節點**

如果有要在多個Publish執行個體之間同步的自訂資料，則：

* 每個Publish執行個體&#x200B;**上的**：

   * 以系統管理員許可權登入
   * 存取[網頁主控台](/help/sites-deploying/configuring-osgi.md)

      * 例如，`https://localhost:4503/system/console/configMgr`

   * 尋找`AEM Communities User Sync Listener`
   * 若要開啟以進行編輯，請選取現有組態（鉛筆圖示）
驗證`Name`： `socialpubsync-scheduled-trigger`

![AEM Communities使用者同步接聽程式](assets/chlimage_1-26.png)

* **節點型別**
這是已同步的節點型別清單。 必須在此處列出sling：Folder以外的任何節點型別（sling：folder單獨處理）。
要同步之節點型別的預設清單：

   * rep：User
   * nt:unstructured
   * nt：resource

* **可忽略的屬性**
這是偵測到任何變更時忽略的屬性清單。 對這些屬性的變更可能會因為其他變更的副作用而同步化（因為同步化一律在節點層級），但是對這些屬性的變更本身不會觸發同步化。
要忽略的預設屬性：

   * cq:lastModified

* **可忽略的節點**
同步期間被忽略的子路徑。 這些子路徑下的任何專案都不會隨時同步。
要忽略的預設節點：

   * .tokens
   * 系統

* **分散式資料夾**
大多數sling：Folders都會被忽略，因為不需要同步。 這裡列出一些例外情況。
要同步的預設資料夾

   * 區段/分數
   * 社交/關係
   * 活動

### 9.唯一Sling ID {#unique-sling-id}

>[!CAUTION]
>
>如果Sling ID在兩個或多個Publish執行個體之間相符，則使用者群組同步會失敗。

如果發佈伺服器陣列中多個Publish執行個體的Sling ID相同，則使用者群組不會同步。

若要驗證所有Sling ID值是否不同，請在每個Publish執行個體上：

1. 瀏覽至`http://<host>:<port>/system/console/status-slingsettings`
1. 檢查&#x200B;**Sling ID**&#x200B;的值

![檢查Sling ID](assets/chlimage_1-27.png)的值

如果Publish例項的Sling ID符合任何其他Publish例項的Sling ID，則：

1. 停止其中一個具有相符Sling ID的Publish執行個體
1. 在crx-quickstart/launchpad/felix目錄中

   * 搜尋並刪除名為&#x200B;*sling.id.file*&#x200B;的檔案

      * 例如，在Linux®系統上：
        `rm -i $(find . -type f -name sling.id.file)`

      * 例如，在Windows系統上：
        `use windows explorer and search for *sling.id.file*`

1. 啟動Publish執行個體

   * 在啟動時，它會被指派一個新的Sling ID

1. 驗證&#x200B;**Sling ID**&#x200B;現在是否是唯一的

重複這些步驟，直到所有Publish例項都有唯一的Sling ID為止。

## Vault Package Builder工廠 {#vault-package-builder-factory}

若要正確同步更新，必須修改用於使用者同步的Vault封裝產生器：

* 在每個AEM Publish例項上
* 存取[網頁主控台](/help/sites-deploying/configuring-osgi.md)

   * 例如，[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* 找到`Apache Sling Distribution Packaging - Vault Package Builder Factory`

   * `Builder name: socialpubsync-vlt`

* 選取編輯圖示
* 新增兩個`Package Node Filters`：

   * `/home/users|-.*/.tokens`
   * `/home/users|-.*/rep:cache`

* 原則處理：

   * 若要以新節點覆寫現有的rep：policy節點，請新增第三個封裝篩選器：

      * `/home/users|+.*/rep:policy`

   * 若要防止發佈原則，請設定

      * `Acl Handling:` `IGNORE`

![Vault Package Builder Factory](assets/vault-package-builder-factory.png)

## 當……發生什麼情況？ {#what-happens-when}

### 在Publish上自行註冊或編輯設定檔的使用者 {#user-self-registers-or-edits-profile-on-publish}

依設計，在發佈環境（自我註冊）中建立的使用者和設定檔不會出現在作者環境中。

當拓撲是[發佈伺服器陣列](/help/sites-deploying/recommended-deploys.md#tarmk-farm)且已正確設定使用者同步處理時，*使用者*&#x200B;和&#x200B;*使用者設定檔*&#x200B;會使用Sling散發跨發佈伺服器陣列進行同步處理。

### 使用者或使用者群組是使用「安全性主控台」建立的 {#users-or-user-groups-are-created-using-security-console}

依設計，在發佈環境中建立的使用者資料不會出現在製作環境中，反之亦然。

當使用[使用者管理與安全性](/help/sites-administering/security.md)主控台在發佈環境中新增使用者時，使用者同步會將新使用者及其群組成員資格同步到其他Publish執行個體（如有必要）。 使用者同步也會同步透過安全性主控台建立的使用者群組。

## 疑難排解 {#troubleshooting}

### 如何讓使用者同步處理離線 {#how-to-take-user-sync-offline}

若要讓使用者同步處理離線，或要[移除Publish執行個體](#how-to-remove-a-publish-instance)或[手動同步處理資料](#manually-syncing-users-and-user-groups)，發佈佇列必須為空白且無訊息。

檢查發佈佇列的狀態：

* 對作者：

   * 使用[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)

      * 尋找`/var/sling/distribution/packages`中的專案

         * 以模式`distrpackage_*`命名的資料夾節點

   * 使用[封裝管理員](/help/sites-administering/package-manager.md)

      * 尋找擱置中的套件（尚未安裝）

         * 以模式`socialpubsync-vlt*`命名
         * 由`communities-user-admin`建立

當發佈佇列為空時，停用使用者同步：

* 作者

   * *取消勾選*1}Apache Sling散發代理程式 — 同步代理程式處理站](#apache-sling-distribution-agent-sync-agents-factory)的`Enabled`核取方塊[

工作完成時，若要重新啟用使用者同步：

* 作者

   * 檢查[Apache Sling散發代理程式 — 同步代理程式處理站](#apache-sling-distribution-agent-sync-agents-factory)的`Enabled`核取方塊

### 使用者同步診斷 {#user-sync-diagnostics}

使用者同步診斷工具會檢查組態並嘗試找出任何問題。

在作者上，只要從主控台瀏覽&#x200B;**工具、操作、診斷、使用者同步診斷。**

只要進入User Sync Diagnostics控制檯即可顯示結果。

這是尚未啟用使用者同步時所顯示的內容：

![未啟用使用者同步診斷的警告](assets/chlimage_1-28.png)

#### 如何對Publish執行個體執行診斷 {#how-to-run-diagnostics-for-publish-instances}

從製作環境執行診斷時，通過/失敗結果包含[資訊]區段，顯示已設定的Publish執行個體清單以進行確認。

清單中包含每個Publish執行個體的URL，這些執行個體會針對該執行個體執行診斷。 URL引數`syncUser`已附加至診斷URL，其值設定為在[步驟2](#createauthuser)中建立的&#x200B;*授權同步使用者*。

**注意**：在啟動URL之前，*授權的同步使用者*&#x200B;必須已登入該Publish執行個體。

Publish執行個體的![診斷](assets/chlimage_1-29.png)

### 設定未正確新增 {#configuration-improperly-added}

當使用者同步無法運作時，最常見的問題是額外的設定已新增&#x200B;**。 相反地，*existing *預設設定應該已&#x200B;*編輯*。

以下檢視已編輯的預設設定應該如何顯示在Web主控台中。 如果出現多個執行個體，應移除新增的設定。

#### （作者）一個Apache Sling散發代理程式 — 同步代理程式工廠 {#author-one-apache-sling-distribution-agent-sync-agents-factory}

![已編輯，在Web主控台中的預設組態檢視](assets/chlimage_1-30.png)

#### （作者）一個Apache Sling散發傳輸認證 — 以使用者認證為基礎的DistributionTransportSecretProvider {#author-one-apache-sling-distribution-transport-credentials-user-credentials-based-distributiontransportsecretprovider}

![已編輯，在Web主控台中的預設組態檢視](assets/chlimage_1-31.png)

#### (Publish)一個Apache Sling散發代理程式 — 佇列代理程式工廠 {#publish-one-apache-sling-distribution-agent-queue-agents-factory}

![已編輯，在Web主控台中的預設組態檢視](assets/chlimage_1-32.png)

#### (Publish)一個Adobe Social同步 — 觀察者工廠差異 {#publish-one-adobe-social-sync-diff-observer-factory}

![已編輯，在Web主控台中的預設組態檢視](assets/chlimage_1-33.png)

#### （作者）一個Apache Sling Distribution觸發器 — 排程觸發器工廠 {#author-one-apache-sling-distribution-trigger-scheduled-triggers-factory}

![已編輯，在Web主控台中的預設組態檢視](assets/chlimage_1-34.png)

### 在回應處理期間修改作業例外狀況 {#modify-operation-exception-during-response-processing}

如果記錄中會顯示下列專案：

`org.apache.sling.servlets.post.impl.operations.ModifyOperation Exception during response processing.`

`java.lang.IllegalStateException: This tree does not exist`

然後確認區段[2。 已正確遵循建立授權的使用者](#createauthuser)。

本節說明如何建立存在於所有Publish執行個體上的授權使用者，以及在作者的「機密提供者」OSGi設定中識別他們。 依預設，使用者為`admin`。

授權的使用者應該成為&#x200B;**`administrators`**&#x200B;使用者群組的成員，而且該群組的許可權不應變更。

授權使用者在所有Publish執行個體上應明確擁有下列許可權和限制：

| **path** | **jcr：all** | **rep：glob** |
|---|---|---|
| /home | X | &#42;/activities/&#42; |
| /home/users | X | &#42;/activities/&#42; |
| /home/groups | X | &#42;/activities/&#42; |

作為`administrators`群組的成員，授權的使用者應在所有Publish執行個體上擁有下列許可權：

| **path** | **jcr：all** | **jcr：read** | **rep：write** |
|---|---|---|---|
| /etc/packages/sling/distribution |  |  | X |
| /libs/sling/distribution |  | X |  |
| /var |  |  | X |
| /var/eventing |  | X | X |
| /var/sling/distribution |  | X | X |

### 使用者群組同步失敗 {#user-group-sync-failed}

如果Sling ID在兩個或多個Publish執行個體之間相符，則使用者群組同步會失敗。

請參閱區段[9。 唯一的Sling ID](#unique-sling-id)

### 手動同步使用者和使用者群組 {#manually-syncing-users-and-user-groups}

* 在存在使用者和使用者群組的Publish執行個體上：

   * [如果啟用，請停用使用者同步](#how-to-take-user-sync-offline)
   * [建立`/home`的封裝](/help/sites-administering/package-manager.md#creating-a-new-package)

      * 編輯套件時

         * 篩選器索引標籤：新增篩選器：根路徑： `/home`
         * 進階標籤： AC處理： `Overwrite`

   * [匯出套件](/help/sites-administering/package-manager.md#downloading-packages-to-your-file-system)

* 在其他Publish執行個體上：

   * [匯入套件](/help/sites-administering/package-manager.md#installing-packages)

若要設定或啟用使用者同步，請移至步驟1： [Apache Sling Distribution Agent - Sync Agents Factory](#apache-sling-distribution-agent-sync-agents-factory)

### 當Publish執行個體無法使用時 {#when-a-publish-instance-becomes-unavailable}

當Publish執行個體無法使用時，如果日後可重新上線，則不應移除該執行個體。 系統會將變更排入Publish執行個體的佇列，並在變更重新上線時進行處理。

如果Publish例項絕不會重新上線，或是永久離線，則必須將其移除，因為佇列累積會導致在製作環境中出現顯著的磁碟空間使用量。

當Publish執行個體停用時，製作記錄會出現類似下列的例外狀況：

```
28.01.2016 15:57:48.475 ERROR
 [pool-12-thread-34-org_apache_sling_distribution_queue_socialpubsync_endpoint1
 (org/apache/sling/distribution/queue/socialpubsync/endpoint1)]
 org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync] could not deliver package distrpackage_1454014575838_a2b45ec8-0400-42f3-bed8-ae09b66381cb
 org.apache.sling.distribution.packaging.DistributionPackageImportException: failed in importing package ...
```

### 如何移除Publish執行個體 {#how-to-remove-a-publish-instance}

若要從[Apache Sling Distribution Agent - Sync Agents Factory](#apache-sling-distribution-agent-sync-agents-factory)移除Publish執行個體，發佈佇列必須為空白且無訊息。

* 對作者：

   * [讓使用者同步處理離線](#how-to-take-user-sync-offline)
   * 請依照[步驟7](#apache-sling-distribution-agent-sync-agents-factory)，從兩個伺服器清單中移除Publish執行個體：

      * `Exporter Endpoints`
      * `Importer Endpoints`

   * 重新啟用使用者同步

      * 檢查[Apache Sling散發代理程式 — 同步代理程式處理站](#apache-sling-distribution-agent-sync-agents-factory)的`Enabled`核取方塊
