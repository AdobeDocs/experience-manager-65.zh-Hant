---
title: 管理用戶和用戶組
seo-title: Managing Users and User Groups
description: AEM Communities用戶可自行註冊和編輯其個人資料
seo-description: Users of AEM Communities can self-register and edit their profiles
uuid: aeba424e-ea7e-4da5-b94f-ea8af4caa7d2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 774c2553-b629-456b-afa7-5713490f4a0a
role: Admin
exl-id: 4237085a-d70d-41de-975d-153f58336daa
source-git-commit: cc0574ae22758d095a3ca6b91f0ceae4a8691f0e
workflow-type: tm+mt
source-wordcount: '1920'
ht-degree: 0%

---

# 管理用戶和用戶組 {#managing-users-and-user-groups}

## 概觀 {#overview}

在AEM Communities，在發佈環境中，用戶可以自行註冊和編輯其配置檔案。 如果具有相應的權限，它們還可以：

* 在社區站點內建立子社區(請參閱 [社區組](creating-groups.md))。

* [中等](moderation.md) 用戶生成的內容(UGC)。

* 是 [特權](#privileged-members-group) 建立部落格、日曆、QnA和論壇的條目。

在發佈環境中註冊的用戶通常稱為 *社區成員（成員）* 將它們與 *用戶* 在作者環境中。

通過將成員分配給 [成員（用戶）組](#publish-group-roles) 在社區站點 [建立](sites-console.md) 或 [修改](sites-console.md#modifying-site-properties) 從作者的環境中。 從作者環境工作時，成員可通過 [隧道服務](#tunnel-service)。

按照設計，在發佈環境中建立的成員和成員組不應出現在作者環境中。 在作者環境中建立的用戶和用戶組也同樣打算保留在作者環境中。

當作者和發佈成員的用戶來自同一用戶清單時，在作者和發佈環境中，他們不被視為具有相同權限和組成員資格的同一用戶。 成員和用戶的角色必須在發佈和作者時酌情單獨建立。

對於 [發佈場](topologies.md)，在一個發佈實例上進行的註冊和修改需要與其他發佈實例同步，以便它們能夠訪問相同的用戶資料。 有關詳細資訊，請參閱 [用戶同步](sync.md)，其中包含描述 [當……](sync.md#what-happens-when)。

### 貢獻限制 {#contribution-limits}

為了防止垃圾郵件，可以限製成員發佈內容的頻率。 此外，可以自動限制新註冊成員的貢獻。

有關詳細資訊，請參閱 [成員繳費限制](limits.md)。

### 動態建立的用戶組 {#dynamically-created-user-groups}

建立新社區站點時，將動態建立新用戶組，其中包含uniquie id(uid)和權限，這些權限適用於在作者環境中管理社區站點所需的各種管理功能(請參見 [作者組角色](#author-group-roles))或發佈環境(請參見 [發佈組角色](#publish-group-roles))。

組的名稱是在 [社區網站建立](sites-console.md#step13asitetemplate)。 唯一的ID可避免同一伺服器上同類命名的社區站點和社區組的命名衝突。

例如，如果站點名稱為「*參與*&#x200B;對於標題為「We.Retail Engage」的網站，則建立的用戶組之一將是：

* 社區 *參與* 成員

## 作者環境 {#author-environment}

### 隧道服務 {#tunnel-service}

使用作者環境時 [建立站點](sites-console.md)。 [修改站點屬性](sites-console.md#modifying-site-properties) 和 [管理社區成員和成員組](members.md)，必須訪問在發佈環境中註冊的用戶和用戶組。

隧道服務使用作者上的複製代理提供此訪問。

* 有關詳細資訊，請參閱 [配置說明](deploy-communities.md#tunnel-service-on-author) 在部署頁面上。

的 [社區成員和組控制台](members.md) 僅用於管理僅在發佈環境中註冊的用戶（成員）和用戶組（成員組）。

要管理在作者環境中註冊的用戶和用戶組，請使用 [安全控制台](../../help/sites-administering/security.md)

### 作者組角色 {#author-group-roles}

| 如果組成員…… | 主要角色 |
|---|---|
| 管理員 | 管理員組由系統管理員組成，他們具有社區管理員的所有能力以及管理社區管理員組的能力。 |
| 社群管理員 | 「社區管理員」組將自動成為所有社區站點和在該站點上建立的任何社區組的成員。 「社區管理員」組的初始成員是管理員組。 在作者環境中，社區管理員能夠建立社區站點、管理站點、管理成員（他們可以禁止社區成員），以及適當的內容。 |
| 社區&lt;*站點名稱*>站點內容管理器 | 社區站點內容管理器可以執行社區AEM站點的傳統創作、內容建立和修改頁面。 |
| 無 | 匿名站點訪問者可能無法訪問作者環境。 |

### 系統管理員 {#system-administrators}

管理員組的成員是系統管理員，他們能夠為作者和發佈環境AEM執行安裝的初始設定。

為了進行演示和開發，管理員組具有用戶ID為 *管理員* 密碼為 *管理員*。

對於生產環境，應修改預設的管理員組。

請務必遵循 [安全核對表](../../help/sites-administering/security-checklist.md)。

## 發佈環境 {#publish-environment}

### 成為成員 {#becoming-a-member}

在發佈環境中，根據 [設定](sites-console.md#user-management) 在社區站點中，站點訪問者可以成為社區成員：

* 當社區站點為私有（關閉）時：
   * 通過邀請
   * 按管理員的操作

* 當社區站點為公共站點（開啟）時：
   * 通過自註冊
   * 通過社交登錄Facebook和Twitter

>[!NOTE]
>
>如果站點訪問者註冊為一個開放社區站點的成員，則他們將自動成為同一發佈環境中其他開放社區站點的成員。

### 發佈組角色 {#publish-group-roles}

| 如果組成員…… | 主要角色 |
|---|---|
| 社區&lt;*站點名稱*>成員 | 社區站點成員是註冊用戶。 他們可以登錄、修改其配置檔案、加入一個開放的社區組、將內容發佈到社區、向其他成員發送消息以及關注網站活動。 |
| 社區&lt;*站點名稱*>審閱人 | 社區站點主持人是可信的社區成員，能夠使用審核控制台或上下文在內容發佈頁面上批量調整UGC。 |
| 社區&lt;*站點名稱*> &lt;*組名稱*>成員 | 社區組成員是已加入開放社區組或已被邀請加入封閉社區組的社區成員。 他們具有站點內該社區組的成員能力。 |
| 社區&lt;*站點名稱*>組管理員 | 社區站點組管理員是受信任的社區成員，被分配來建立和管理社區站點內的子社區（組）。 其中包括提供上下文審核的能力。 |
| *特權成員安全組* | 為限制內容建立而手動建立和維護的用戶組。 請參閱 [特權成員組](#privileged-members-group)。 |
| 無 | 發現該站點的匿名站點訪問者可以查看和搜索允許匿名訪問的社區站點。 為了參與和發佈內容，用戶必須自行註冊（如果允許）並成為社區成員。 |

### 為發佈組角色分配成員 {#assigning-members-to-publish-group-roles}

當 [建立社區網站](sites-console.md) 在作者環境中，或 [修改站點屬性，](sites-console.md#modifying-site-properties) 可以為成員分配在發佈環境中執行的各種角色，如審閱人、組管理員、資源聯繫人或特權成員。

[啟用隧道服務](sync.md#accessingpublishusersfromauthor) 導致分配選項由發佈時的成員而不是作者上的用戶提供。

所選成員將自動分配給 [合適的團隊](#publish-group-roles) 社區網站（重新發佈）時，將包括其成員身份。

### 有特殊權限的成員群組 {#privileged-members-group}

特權成員安全組的目的是將某些社區功能的內容建立限制到社區站點成員的特權子集。

特權成員組是使用 [社區組控制台](members.md)。

建立特權成員組後， [隧道服務已啟用](sync.md#accessingpublishusersfromauthor)，現有社區網站的結構可能 [修改](sites-console.md#modify-structure) 編輯其社區功能的配置以「允許特權成員」並添加建立的組。

允許指定一個或多個特權成員組的社區函式包括：

* [部落格功能](functions.md#blog-function)  — 限制新文章的建立。
* [日曆函式](functions.md#calendar-function)  — 限制新事件的建立。
* [論壇功能](functions.md#forum-function)  — 限制新主題的建立。
* [QnA函式](functions.md#qna-function)  — 限制建立新問題。

當社區功能未得到保護（未分配特權成員組）時，則允許所有社區站點成員建立功能內容（文章、事件、主題、問題）。

>[!NOTE]
>
>將用戶添加到社區站點的特權成員組將僅在用戶也是同一社區站點的成員時授予他們建立權限。

## 建立社區成員 {#creating-community-members}

### 儲存庫位置 {#repository-location}

為了使某些功能正常工作，需要建立具有適當權限的用戶和用戶組。

建立成員時 `/home/users/community`，它們將繼承為成員配置檔案授予讀取權限的正確ACL。

同樣，自定義社區用戶組（如特權成員組）應在 `/home/groups/community`。

使用 [社區成員和組控制台](members.md) 將在這些路徑中建立用戶和組。

要指定自定義路徑，需要使用經典安全UI，該UI可在 [https://&lt;server>:&lt;port>/useradmin](http://localhost:4503/useradmin)。

要為自定義成員路徑授予讀權限，請在所有發佈實例上設定類似於 `/home/users/community`:

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

為自定義成員組路徑（如/home/groups/mycompany）在所有發佈實例集ACL上提供適當的權限，類似於 `/home/groups/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### 控制台 {#consoles}

僅在作者環境中提供四個獨立的控制台：

| 控制台 | 工具、安全性、用戶 | 工具、安全性、組 | 社區，成員 | 社區、組 |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| 管理 | 作者 | 作者的用戶組 | 發佈成員 | 發佈時的成員組 |
| 要求 | 管理員權限 | 管理員權限 | 管理員權限，隧道服務，用戶同步發佈場 | 管理員權限，隧道服務，用戶同步發佈場 |

### 社區管理員角色 {#community-administrators-role}

如 [作者組角色](#author-group-roles) 圖表中，社區管理員組的成員能夠建立社區站點、管理站點、管理成員（他們可以禁止社區成員）和中等內容。

按照建立用戶並將用戶分配給啟用管理器角色的相同步驟操作，但添加c `ommunity-administrators` 組。

### LDAP整合 {#ldap-integration}

支AEM持使用LDAP驗證用戶以及建立用戶帳戶。 詳細資訊 [配置LDAPAEM 6](../../help/sites-administering/ldap-config.md)。

以下是特定於社區成員和成員組的一些配置詳細資訊。

1. 為每個發佈實例配AEM置LDAP。
2. [LDAP標識提供程式](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * 沒有特殊說明

3. [同步處理程式](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * 設定以下屬性：

      * **[!UICONTROL 用戶自動成員身份]**: `community-<site name>-<uid>-members`
      * **[!UICONTROL 用戶路徑前置詞]**: `/community`
      * **[!UICONTROL 組路徑前置詞]**: `/community`

4. [外部登錄模組](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * 沒有特殊說明

這將導致用戶被自動分配給社區站點的成員組和儲存庫位置 `/home/users/community` 和 `/home/groups/community`，以便他們繼承查看彼此的配置檔案的適當權限。

* 的 `User auto membership` 值應為 `rep:authorizableId` 屬性，不是 `givenName` （顯示名稱）。

## 在實例之間同AEM步用戶 {#synchronizing-users-among-aem-instances}

使用 [發佈場](topologies.md)，通過將用戶首先導入到一個實例和 [啟用用戶同步](sync.md) 將用戶分發到其他發佈實例。

如果導入用戶組，要確保用戶組在每個發佈實例上具有相同的路徑，請導入到一個實例，然後 [建立包](../../help/sites-administering/package-manager.md#creating-a-new-package) 導出，並將該軟體包安裝到所有其他發佈實例上。

雖然通過用戶同步的用戶組同步將包含在將來的版本中，但目前僅 *成員* 在用戶同步運行時同步。

## 關於社區組 {#about-community-groups}

在討論小組時，有兩個不同的主題：

* **[社區組](overview.md#communitygroups)**

   社區組是在發佈環境中為支援建立社區組的社區站點建立的子社區。 建立社區組會導致添加到網站的更多頁面，並且以類似於其父社區站點的方式進行管理。 有關詳細資訊，請訪問 [社區組要件](essentials-groups.md) 為開發商和 [社區組](creating-groups.md) 作者。

* **[成員組](../../help/sites-administering/security.md)**

   成員組是成員可能屬於的組，並通過組控制台進行管理。 本頁上的討論大多集中在成員組。 為社區站點自動建立的成員組，其前置詞為 *`Community`*，可稱為社區組，因此必須考慮討論的背景。
