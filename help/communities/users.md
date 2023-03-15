---
title: 管理使用者和使用者群組
seo-title: Managing Users and User Groups
description: AEM Communities的使用者可以自行註冊和編輯其設定檔
seo-description: Users of AEM Communities can self-register and edit their profiles
uuid: aeba424e-ea7e-4da5-b94f-ea8af4caa7d2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 774c2553-b629-456b-afa7-5713490f4a0a
role: Admin
exl-id: 4237085a-d70d-41de-975d-153f58336daa
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2168'
ht-degree: 0%

---

# 管理使用者和使用者群組 {#managing-users-and-user-groups}

## 概觀 {#overview}

在AEM Communities中，使用者可在發佈環境中自行註冊和編輯其設定檔。 有了適當的權限，他們也可以：

* 在社群網站內建立子社群(請參閱 [社群團體](creating-groups.md))。

* [審核](moderation.md) 使用者產生的內容(UGC)。

* Be [啟用資源](resources.md) 聯繫人。

* Be [特權](#privileged-members-group) 為部落格、日曆、QnA和論壇建立條目。

在發佈環境中註冊的使用者通常稱為 *社群成員（成員）* 區分 *使用者* 在製作環境中。

權限是指派成員至 [成員（用戶）組](#publish-group-roles) 在社群網站建立時動態建立 [已建立](sites-console.md) 或 [修改](sites-console.md#modifying-site-properties) 從製作環境中取得。 從製作環境工作時，成員可透過 [隧道服務](#tunnel-service).

根據設計，在發佈環境中建立的成員和成員組不應出現在製作環境中。 在製作環境中建立的使用者和使用者群組，也同樣打算保留在製作環境中。

當製作使用者和發佈成員的使用者來自相同的使用者清單時（例如從相同的LDAP目錄同步），在製作和發佈環境中，他們不會被視為具有相同權限和群組成員資格的相同使用者。 成員和使用者的角色必須在發佈時和作者時酌情分別建立。

若 [發佈農場](topologies.md)，一個發佈例項上所做的註冊和修改必須與其他發佈例項同步，才能存取相同的使用者資料。 如需詳細資訊，請參閱 [使用者同步](sync.md)，其中包含描述 [當……](sync.md#what-happens-when).

### 貢獻限制 {#contribution-limits}

為了防止垃圾郵件，可以限製成員發佈內容的頻率。 此外，可以自動限制新註冊成員的繳款。

如需詳細資訊，請參閱 [會員供款限制](limits.md).

### 動態建立的使用者群組 {#dynamically-created-user-groups}

建立新社群網站時，會以唯一ID(uid)和適合於製作環境中管理社群網站所需的各種管理功能的權限，動態建立新的使用者群組(請參閱 [作者群組角色](#author-group-roles))或發佈環境(請參閱 [發佈群組角色](#publish-group-roles))。

群組的名稱是在 [社群網站建立](sites-console.md#step13asitetemplate). 唯一ID可避免同一伺服器上同樣命名之社群網站和社群群組的命名衝突。

例如，如果網站名稱為「*參與*「若為名為「We.Retail Engage」的網站，則建立的使用者群組為：

* 社群 *參與* 成員

## 製作環境 {#author-environment}

### 通道服務 {#tunnel-service}

將製作環境用於 [建立網站](sites-console.md), [修改站點屬性](sites-console.md#modifying-site-properties) 和 [管理社區成員和成員組](members.md)，則必須存取在發佈環境中註冊的使用者和使用者群組。

隧道服務使用製作上的復寫代理提供此存取。

* 如需詳細資訊，請參閱 [配置說明](deploy-communities.md#tunnel-service-on-author) 在部署頁面上。

此 [Communities成員和群組主控台](members.md) 僅用於管理僅在發佈環境中註冊的使用者（成員）和使用者群組（成員群組）。

若要管理在製作環境中註冊的使用者和使用者群組，請使用 [安全控制台](../../help/sites-administering/security.md)

### 作者群組角色 {#author-group-roles}

| 如果組成員…… | 主要角色 |
|---|---|
| 管理員 | 管理員組由系統管理員組成，他們具有社區管理員的所有能力以及管理社區管理員組的能力。 |
| 社群管理員 | 社區管理員組自動成為所有社區站點和站點上建立的任何社區組的成員。 社區管理員組的初始成員是管理員組。 在製作環境中，社群管理員可以建立社群網站、管理網站、管理成員（他們可以禁止社群的成員），以及協調內容。 |
| 社群&lt;*網站名稱*> Sitecontentmanager | 「社群網站內容管理員」可以執行傳統的AEM製作、內容建立和社群網站的修改頁面。 |
| 社群培訓經理 | 「社群啟用管理員」群組包含可供指派管理社群網站「啟用管理員」群組的使用者。 |
| 社群&lt;*網站名稱* > Siteenablementmanagers | 「社群網站啟用管理員」群組包含指派給管理社群網站啟用的使用者 [資源](resources.md). |
| 無 | 匿名網站訪客可能無法存取製作環境。 |

### 系統管理員 {#system-administrators}

管理員群組的成員是系統管理員，可為製作和發佈環境執行AEM安裝的初始設定。

為了進行示範和開發，管理員組具有用戶ID為 *管理員* 密碼 *管理員*.

對於生產環境，應修改預設管理員群組。

請務必遵循 [安全性檢查清單](../../help/sites-administering/security-checklist.md).

## 發佈環境 {#publish-environment}

### 成為會員 {#becoming-a-member}

在發佈環境中，視 [設定](sites-console.md#user-management) 在社群網站中，網站訪客可能成為社群成員：

* 當社群網站為私人（關閉）時：
   * 通過邀請
   * 按管理員的操作

* 當社群網站為公用（開啟）時：
   * 通過自註冊
   * 透過Facebook和Twitter的社交登入

>[!NOTE]
>
>如果網站訪客註冊為一個開放社群網站的成員，他們會自動成為相同發佈環境中其他開放社群網站的成員。

### 發佈群組角色 {#publish-group-roles}

| 如果組成員…… | 主要角色 |
|---|---|
| 社群&lt;*網站名稱*>成員 | 社區站點成員是註冊用戶。 他們可以登入、修改其設定檔、加入開放的社群群組、將內容張貼至社群、傳送訊息給其他成員，以及遵循網站活動。 |
| 社群&lt;*網站名稱*>協調者 | 社群網站協調者是值得信賴的社群成員，可以在張貼內容的頁面上，使用協調控制台或內容來大量協調UGC。 |
| 社群&lt;*網站名稱*> &lt;*群組名稱*>成員 | 社群群組成員是已加入開放社群群組或受邀加入封閉社群群組的社群成員。 他們具有網站內該社群群組的成員的能力。 |
| 社群&lt;*網站名稱*>群組管理員 | 社區站點組管理員是受信任的社區成員，被分配來建立和管理社區站點內的子社區（組）。 其中包括提供內容內協調的功能。 |
| *特權成員安全組* | 為限制內容建立而手動建立和維護的使用者群組。 請參閱 [特權成員組](#privileged-members-group). |
| 無 | 探索到網站的匿名網站訪客可以檢視並搜尋允許匿名存取的社群網站。 若要參與並張貼內容，使用者必須自行註冊（如果允許）並成為社群成員。 |

### 為發佈組角色分配成員 {#assigning-members-to-publish-group-roles}

當 [建立社群網站](sites-console.md) 或 [修改網站屬性，](sites-console.md#modifying-site-properties) 可為成員指派在發佈環境中執行的各種角色，例如協調者、群組管理員、資源聯絡人或有權限的成員。

[啟用通道服務](sync.md#accessingpublishusersfromauthor) 導致在發佈時從成員顯示分配選擇，而不是在作者上顯示用戶。

所選成員將自動分配給 [合適的小組](#publish-group-roles) 社群網站發佈（重新發佈）時，會納入其會籍。

### 有特殊權限的成員群組 {#privileged-members-group}

特權成員安全組的目的是將某些社區功能的內容建立限制在社區站點成員的特權子集。

特權成員組是使用 [Communities群組主控台](members.md).

建立特權成員組後，使用 [已啟用隧道服務](sync.md#accessingpublishusersfromauthor)，現有社群網站的結構可能 [修改](sites-console.md#modify-structure) 將其社群函式的配置編輯為「允許特權成員」並添加已建立的組。

允許指定一個或多個特權成員組的社區功能包括：

* [部落格功能](functions.md#blog-function)  — 限制建立新文章。
* [日曆函式](functions.md#calendar-function)  — 限制建立新事件。
* [論壇功能](functions.md#forum-function)  — 限制新主題的建立。
* [QnA函式](functions.md#qna-function)  — 限制建立新問題。

當社群功能未受到保護時（未分配特權成員組），則允許所有社區站點成員建立功能內容（文章、事件、主題、問題）。

>[!NOTE]
>
>只有將用戶添加到社區站點的特權成員組時，如果用戶也是同一社區站點的成員，則只授予他們建立權限。

## 建立社群成員 {#creating-community-members}

### 儲存庫位置 {#repository-location}

為了讓某些功能正常運作，需要建立具有適當權限的使用者和使用者群組。

在中建立成員時 `/home/users/community`，它們將繼承為成員配置檔案提供讀取權限的正確ACL。

同樣地，自訂社群使用者群組（例如有權限的成員群組）也應建立在 `/home/groups/community`.

使用 [Communities成員和群組主控台](members.md) 會在這些路徑中建立使用者和群組。

若要指定自訂路徑，必須使用傳統安全性UI，可在 [https://&lt;server>:&lt;port>/useradmin](http://localhost:4503/useradmin).

為自定義成員路徑授予讀取權限，在所有發佈實例上設定ACL類似於 `/home/users/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="everyone"
  rep:privileges="{Name}[jcr:read]" >
  <rep:restrictions
    jcr:primaryType="rep:Restrictions"
    rep:glob="*/profile*" />
</allow>
```

為自訂成員組路徑（如/home/groups/mycompany）提供適當的權限，以便在所有發佈實例上設定類似的ACL `/home/groups/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### 主控台 {#consoles}

只有製作環境提供四個不同的主控台：

| 主控台 | 工具，安全性，用戶 | 工具，安全性，組 | 社區、成員 | 社區、組 |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| 管理 | 作者使用者 | 作者的使用者群組 | 發佈的成員 | 發佈時的成員組 |
| requiles | 管理員權限 | 管理員權限 | 管理員權限，隧道服務，發佈場的使用者同步 | 管理員權限，隧道服務，發佈場的使用者同步 |

### 社群啟用管理員角色 {#community-enablement-manager-role}

網站訪客自行註冊的功能通常不允許 [啟用社群](overview.md#enablement-community) 因為每個成員都有相關的成本。 培訓使用者和資源由指派 [角色](#author-group-roles) of `enablement manager` [在網站建立期間](sites-console.md#enablement) 作者（新增為群組成員） `Community <site-name> Siteenablementmanagers`)。 此 `enablement manager` 也負責 [分配學習資源](resources.md) 向社群成員致意。

只有是全球成員的用戶 `Community Enablement Managers` 群組可選為 `enablement manager` 特定社群網站。

建立可被分配角色的用戶 `Community Site Enablement Manager`，請使用傳統UI安全性主控台來指定路徑：

在製作例項上：

1. 以管理員權限登入，瀏覽至傳統UI安全主控台。

   例如， [http://localhost:4502/useradmin](http://localhost:4502/useradmin)

2. 從「編輯」菜單中，選擇 **[!UICONTROL 建立使用者]**.
3. 填入 `Create User` 對話框。
   * 路徑必須 `/home/users/community`.
4. 選擇 **[!UICONTROL 建立]**。

   ![create-community-user](assets/create-community-user.png)

* 在左窗格中，搜索新建立的用戶並選擇顯示在右窗格中。

   ![社群使用者](assets/view-community-user.png)

在左窗格中：

1. 清除搜索框並選擇 **[!UICONTROL 隱藏用戶]**.
2. 找出並拖曳 `community-enablementmanagers` 到 **[!UICONTROL 群組]** 頁簽中。

   ![assign-group](assets/assign-group.png)

### 社群管理員角色 {#community-administrators-role}

如 [作者群組角色](#author-group-roles) 圖表中，社區管理員組的成員可以建立社區站點、管理站點、管理成員（他們可以禁止社區成員），以及審核內容。

請依照建立使用者並將使用者指派給角色的相同步驟操作 [啟用管理員](#communitysiteenablementmanagerrole)，但加c `ommunity-administrators` 群組（在使用者的「群組」標籤下）。

### LDAP整合 {#ldap-integration}

AEM支援使用LDAP來驗證使用者以及建立使用者帳戶。 這在 [使用AEM 6配置LDAP](../../help/sites-administering/ldap-config.md).

以下是特定於社區成員和成員組的一些配置詳細資訊。

1. 為每個AEM發佈執行個體配置LDAP。
2. [LDAP標識提供程式](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * 無特殊說明

3. [同步處理程式](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * 設定下列屬性：

      * **[!UICONTROL 用戶自動成員資格]**: `community-<site name>-<uid>-members`
      * **[!UICONTROL 用戶路徑前置詞]**: `/community`
      * **[!UICONTROL 組路徑前置詞]**: `/community`

4. [外部登入模組](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * 無特殊指示

這會自動將用戶分配給社區站點的成員組，並將儲存庫位置分配給 `/home/users/community` 和 `/home/groups/community`，這樣他們就會繼承適當的權限，以查看彼此的設定檔。

* 此 `User auto membership` 值應為 `rep:authorizableId` 屬性，而非 `givenName` （顯示名稱）。

## 在AEM執行個體之間同步使用者 {#synchronizing-users-among-aem-instances}

使用 [發佈農場](topologies.md)，請先將使用者匯入至一個例項，以確保使用者在每個發佈例項上擁有相同的路徑 [啟用用戶同步](sync.md) 以將使用者分發至其他發佈執行個體。

如果匯入使用者群組，為確保使用者群組在每個發佈執行個體上有相同的路徑，請匯入至一個執行個體，然後 [建立套件](../../help/sites-administering/package-manager.md#creating-a-new-package) ，並將該套件安裝在所有其他發佈執行個體上。

雖然透過使用者同步同步的使用者群組將會納入未來版本，目前僅 *會籍* 使用者同步執行時，使用者群組的會同步。

## 關於社群群組 {#about-community-groups}

討論群組時，有兩個不同的主題：

* **[社群群組](overview.md#communitygroups)**

   社群群組是可在發佈環境中為社群網站建立的子社群，可支援社群群組的建立。 建立社群群組會導致網站新增更多頁面，且以類似於其父社群網站的方式進行管理。 如需詳細資訊，請造訪 [社群群組要點](essentials-groups.md) 適用於開發人員和 [社群群組](creating-groups.md) 供作者使用。

* **[成員組](../../help/sites-administering/security.md)**

   成員組是成員可能屬於的組，並通過組控制台進行管理。 本頁討論的大部分內容都專門討論成員組。 為社區站點自動建立的成員組，前置詞為 *`Community`*，可稱為社區群，因此必須考慮討論的背景。
