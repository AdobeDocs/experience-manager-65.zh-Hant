---
title: 管理使用者和使用者群組
description: AEM Communities的使用者可以自行註冊及編輯其設定檔
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 4237085a-d70d-41de-975d-153f58336daa
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 0%

---

# 管理使用者和使用者群組 {#managing-users-and-user-groups}

## 概觀 {#overview}

在AEM Communities中的發佈環境中，使用者可以自行註冊及編輯其設定檔。 在提供適當的許可權下，他們也可以：

* 在社群網站內建立子社群（請參閱[社群群組](creating-groups.md)）。

* [稽核](moderation.md)使用者產生的內容(UGC)。

* 成為[有特殊許可權的](#privileged-members-group)，以建立部落格、行事曆、QnA和論壇的專案。

在發佈環境中註冊的使用者通常稱為&#x200B;*社群成員（成員）*，以便在作者環境中將其與&#x200B;*使用者*&#x200B;區分開來。

透過將成員指派給在社群網站是來自作者環境的[建立](sites-console.md)或[修改](sites-console.md#modifying-site-properties)時動態建立的[成員（使用者）群組](#publish-group-roles)之一來授與許可權。 使用作者環境時，成員可透過[通道服務](#tunnel-service)從發佈環境顯示。

依設計，在發佈環境中建立的成員和成員群組不應出現在製作環境中。 在製作環境中建立的使用者和使用者群組，其目的類似地都是要保留在製作環境中。

當作者上的使用者與發佈上的成員來自相同的使用者清單時（例如從相同的LDAP目錄同步），在作者與發佈環境中他們不會被視為擁有相同許可權和群組成員資格的相同使用者。 成員和使用者的角色必須視情況在發佈和作者上分別建立。

對於[發佈伺服器陣列](topologies.md)，對一個發佈執行個體進行的註冊和修改需要與其他發佈執行個體同步，才能存取相同的使用者資料。 如需詳細資訊，請參閱[使用者同步處理](sync.md)，其中包含描述[當……](sync.md#what-happens-when)時會發生什麼的區段。

### 貢獻限制 {#contribution-limits}

為了防止垃圾郵件，可以限制成員的張貼內容頻率。 此外，也可以自動限制新註冊成員的貢獻。

如需詳細資訊，請參閱[成員貢獻限制](limits.md)。

### 動態建立的使用者群組 {#dynamically-created-user-groups}

建立新社群網站時，會在作者環境（請參閱[作者群組角色](#author-group-roles)）或發佈環境(請參閱[Publish群組角色](#publish-group-roles))中，以適用於管理社群網站所需各種管理功能的唯一ID (uid)和許可權，動態建立新使用者群組。

群組名稱是在[社群網站建立](sites-console.md#step13asitetemplate)期間，從指定的網站名稱產生。 此唯一ID可避免相同伺服器上名稱相似之社群網站和社群群組的命名衝突。

例如，如果標題為&quot; Engage&quot;的網站的網站名稱是&quot;*engage*&quot;，則其中一個建立的使用者群組將是：

* 社群&#x200B;*參與*&#x200B;成員

## 作者環境 {#author-environment}

### 通道服務 {#tunnel-service}

使用作者環境[建立網站](sites-console.md)、[修改網站屬性](sites-console.md#modifying-site-properties)和[管理社群成員與成員群組](members.md)時，必須存取在發佈環境中註冊的使用者與使用者群組。

通道服務使用作者上的復寫代理程式提供此存取權。

* 如需詳細資訊，請參閱部署頁面上的[設定指示](deploy-communities.md#tunnel-service-on-author)。

[社群成員與群組主控台](members.md)的唯一用途是管理僅在發佈環境中註冊的使用者（成員）與使用者群組（成員群組）。

若要管理在作者環境中註冊的使用者和使用者群組，請使用[安全性主控台](../../help/sites-administering/security.md)

### 作者群組角色 {#author-group-roles}

| 如果群組的成員…… | 主要角色 |
|---|---|
| 管理員 | 管理員群組由系統管理員組成，系統管理員擁有社群管理員的所有能力以及管理社群管理員群組的能力。 |
| 社群管理員 | 社群管理員群組會自動成為所有社群網站以及在網站上建立的任何社群群組的成員。 Community Administrators群組的初始成員是administrators群組。 在作者環境中，社群管理員能夠建立社群網站、管理網站、管理成員（他們可以從社群中禁止成員）和稽核內容。 |
| 社群&lt;*網站名稱*>網站內容管理員 | 社群網站內容管理員能夠執行傳統的AEM編寫、內容建立和修改社群網站的頁面。 |
| 無 | 匿名網站訪客可能無法存取作者環境。 |

### 系統管理員 {#system-administrators}

管理員群組的成員是系統管理員，他們能夠為製作和發佈環境執行AEM安裝的初始設定。

為了示範和開發目的，管理員群組有一個成員，其使用者識別碼為&#x200B;*admin*，密碼為&#x200B;*admin*。

對於生產環境，應修改預設的管理員群組。

請務必遵循[安全性檢查清單](../../help/sites-administering/security-checklist.md)。

## Publish環境 {#publish-environment}

### 成為會員 {#becoming-a-member}

在發佈環境中，根據社群網站的[設定](sites-console.md#user-management)，網站訪客可能會成為社群成員：

* 當社群網站為私人（已關閉）時：
   * 透過邀請
   * 依管理員的動作

* 當社群網站為公開（開放）時：
   * 依自助註冊
   * 透過Facebook和Twitter的社交登入

>[!NOTE]
>
>如果網站訪客註冊為一個開放社群網站的成員，則他們會自動成為相同發佈環境中其他開放社群網站的成員。

### Publish群組角色 {#publish-group-roles}

| 如果群組的成員…… | 主要角色 |
|---|---|
| 社群&lt;*網站名稱*>成員 | 社群網站成員是註冊使用者。 他們可以登入、修改個人檔案、加入開放的社群群組、發佈內容至社群、傳送訊息給其他成員，以及關注網站活動。 |
| 社群&lt;*網站名稱*>版主 | 社群網站版主是受信任的社群成員，其能夠使用版主主控台大量版主，或是在內容張貼的頁面上使用內文中版主，來版主UGC。 |
| 社群&lt;*網站名稱*> &lt;*群組名稱*>成員 | 社群群組成員是已加入開放社群群組，或已受邀加入封閉式社群群組的社群成員。 他們擁有網站內該社群群組的成員能力。 |
| 社群&lt;*網站名稱*> Groupadministrators | 社群網站群組管理員是受信任的社群成員，其任務是在社群網站中建立和管理子社群（群組）。 包括提供內容內稽核的能力。 |
| *有特殊許可權的成員安全性群組* | 以限制內容建立為目的的手動建立和維護的使用者群組。 檢視[有特殊許可權的成員群組](#privileged-members-group)。 |
| 無 | 探索到網站的匿名網站訪客，可以檢視及搜尋允許匿名存取的社群網站。 若要參與和發佈內容，使用者必須自行註冊（如果允許）並成為社群成員。 |

### 將成員指派給Publish群組角色 {#assigning-members-to-publish-group-roles}

當[在作者環境中建立社群網站](sites-console.md)時，或當[修改網站屬性時，](sites-console.md#modifying-site-properties)成員可能會被指派在發佈環境中執行的各種角色，例如版主、群組管理員、資源聯絡人或有特殊許可權的成員。

[啟用通道服務](sync.md#accessingpublishusersfromauthor)會導致從發佈上的成員而不是作者上的使用者顯示指派選擇。

選取的成員將會自動指派給[適當的群組](#publish-group-roles)，當社群網站（重新）發佈時，將會包含他們的成員資格。

### 有特殊權限的成員群組 {#privileged-members-group}

有特殊許可權的成員安全性群組的目的，是將特定社群功能的內容建立限制在社群網站成員的有特殊許可權的子集。

有特殊許可權的成員群組是使用[社群群組主控台](members.md)建立及管理的成員群組。

建立有特殊許可權的成員群組並啟用[通道服務](sync.md#accessingpublishusersfromauthor)之後，現有社群網站的結構可以是[modified](sites-console.md#modify-structure)，以將其社群功能的設定編輯為[允許有特殊許可權的成員]並新增建立的群組。

允許指定一或多個有特殊許可權的成員群組的社群功能如下：

* [部落格功能](functions.md#blog-function) — 限制新文章的建立。
* [行事曆函式](functions.md#calendar-function) — 限制新事件的建立。
* [論壇功能](functions.md#forum-function) — 限制建立新主題。
* [QnA函式](functions.md#qna-function) — 限制建立新問題。

當社群功能未受保護（未指派有特殊許可權的成員群組）時，則允許所有社群網站成員建立功能內容（文章、事件、主題、問題）。

>[!NOTE]
>
>將使用者新增至社群網站的特權成員群組，只會授予他們建立許可權，前提是他們也是同一社群網站的成員。

## 建立社群成員 {#creating-community-members}

### 存放庫位置 {#repository-location}

為了讓某些功能正常運作，需要建立具有適當許可權的使用者和使用者群組。

在`/home/users/community`中建立成員時，會繼承賦予成員設定檔讀取許可權的適當ACL。

同樣地，自訂社群使用者群組（例如有特殊許可權的成員群組）應在`/home/groups/community`中建立。

使用[社群成員和群組主控台](members.md)將會在這些路徑中建立使用者和群組。

若要指定自訂路徑，必須使用傳統安全性UI，此使用者介面可在[https://&lt;server>：&lt;port>/useradmin](http://localhost:4503/useradmin)存取。

若要為自訂成員路徑提供讀取許可權，請在所有發佈執行個體上設定類似於`/home/users/community`的ACL：

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

若要在所有發佈執行個體上設定類似於`/home/groups/community`的ACL，為自訂成員群組路徑（例如/home/groups/mycompany）提供適當的許可權：

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### 主控台 {#consoles}

只有製作環境提供四個不同的主控台：

| 主控台 | 工具、安全性、使用者 | 工具、安全性、群組 | 社群、成員 | 社群、群組 |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| 管理 | 作者上的使用者 | 作者上的使用者群組 | 發佈上的成員 | 發佈上的成員群組 |
| 需要 | 管理員許可權 | 管理員許可權 | 管理員許可權、通道服務、發佈伺服器陣列的使用者同步 | 管理員許可權、通道服務、發佈伺服器陣列的使用者同步 |

### 社群管理員角色 {#community-administrators-role}

如[作者群組角色](#author-group-roles)圖表所述，「社群管理員」群組的成員可以建立社群網站、管理網站、管理成員（他們可以禁止社群的成員）和稽核內容。

請依照建立及指派使用者至啟用管理員角色的相同步驟進行，但在使用者的[群組]索引標籤下新增c `ommunity-administrators`群組。

### LDAP整合 {#ldap-integration}

AEM支援使用LDAP來驗證使用者並建立使用者帳戶。 這在[使用AEM 6](../../help/sites-administering/ldap-config.md)設定LDAP中有詳細說明。

以下是社群成員和成員群組的特定組態詳細資料。

1. 為每個AEM發佈執行個體設定LDAP。
2. [LDAP身分提供者](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * 無特殊指示

3. [同步處理常式](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * 設定下列屬性：

      * **[!UICONTROL 使用者自動會籍]**： `community-<site name>-<uid>-members`
      * **[!UICONTROL 使用者路徑前置詞]**： `/community`
      * **[!UICONTROL 群組路徑首碼]**： `/community`

4. [外部登入模組](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * 無特殊指示

這會導致系統自動將使用者指派給社群網站的成員群組，且存放庫位置為`/home/users/community`和`/home/groups/community`，因此這些使用者會繼承適當的許可權，以便檢視彼此的設定檔。

* `User auto membership`值應該是`rep:authorizableId`屬性，而不是設定檔中的`givenName` （顯示名稱）。

## 在AEM執行個體之間同步使用者 {#synchronizing-users-among-aem-instances}

使用[發佈伺服器陣列](topologies.md)時，請先將使用者匯入一個執行個體，然後[啟用使用者同步處理](sync.md)至Sling，將使用者分發至其他發佈執行個體，確保使用者在每個發佈執行個體上具有相同的路徑。

如果匯入使用者群組，為了確保使用者群組在每個發佈執行個體上具有相同的路徑，請匯入到一個執行個體，然後[建立套件](../../help/sites-administering/package-manager.md#creating-a-new-package)以供匯出，並在所有其他發佈執行個體上安裝該套件。

雖然透過使用者同步處理來同步使用者群組的功能將會包含在未來的發行版本中，但是目前只有使用者群組的&#x200B;*成員資格*&#x200B;會在使用者同步處理執行時進行同步處理。

## 關於社群群組 {#about-community-groups}

討論群組時，有兩個不同的主題：

* **[社群群組](overview.md#communitygroups)**

  社群群組是子社群，可在支援建立社群群組的社群網站發佈環境中建立。 建立社群群組後，會有更多頁面新增至網站，且會以類似於其上層社群網站的方式進行管理。 如需詳細資訊，請造訪開發人員的[社群群組Essentials](essentials-groups.md)，以及作者的[社群群組](creating-groups.md)。

* **[成員群組](../../help/sites-administering/security.md)**

  成員群組是成員可能所屬的群組，並可透過「群組」主控台進行管理。 本頁的大部分討論都集中在成員群組上。 為社群網站自動建立的成員群組（以&#x200B;*`Community`*&#x200B;為前置詞）可以稱為社群群組，因此必須考慮討論的內容。
