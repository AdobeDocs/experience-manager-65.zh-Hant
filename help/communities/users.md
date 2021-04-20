---
title: 管理使用者和使用者群組
seo-title: 管理使用者和使用者群組
description: AEM Communities的使用者可自行註冊並編輯個人檔案
seo-description: AEM Communities的使用者可自行註冊並編輯個人檔案
uuid: aeba424e-ea7e-4da5-b94f-ea8af4caa7d2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 774c2553-b629-456b-afa7-5713490f4a0a
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2184'
ht-degree: 0%

---


# 管理用戶和用戶組{#managing-users-and-user-groups}

## 概覽 {#overview}

在AEM Communities，在發佈環境中，使用者可自行註冊並編輯其個人檔案。 若有適當的權限，他們也可以：

* 在社群網站中建立子社群（請參閱[社群群組](creating-groups.md)）。

* [協](moderation.md) 調使用者產生的內容(UGC)。

* 成為[啟用資源](resources.md)聯繫人。

* 具有[特權](#privileged-members-group)以建立部落格、日曆、QnA和論壇的條目。

在發佈環境中註冊的用戶通常稱為&#x200B;*社區成員（成員）*，以便在作者環境中將他們與&#x200B;*用戶*&#x200B;區分開。

通過將成員分配給在社區站點從作者環境建立的[或[已修改的](sites-console.md#modifying-site-properties)時動態建立的[成員（用戶）組之一來授予權限。 ](#publish-group-roles)](sites-console.md)從作者環境工作時，成員可通過[隧道服務](#tunnel-service)從發佈環境中看到。

根據設計，在發佈環境中建立的成員和成員組不應出現在作者環境中。 在作者環境中建立的使用者和使用者群組，也會以類似的方式保留在作者環境中。

當作者和發佈成員的使用者來自相同的使用者清單（例如同步自相同的LDAP目錄）時，作者和發佈環境中的使用者不會被視為擁有相同權限和群組成員資格的相同使用者。 成員和使用者的角色必須在發佈和作者（視情況而定）上分別建立。

對於[publish farm](topologies.md)，在一個發佈實例上進行的註冊和修改必須與其他發佈實例同步，以便它們能夠訪問相同的用戶資料。 有關詳細資訊，請參閱[用戶同步](sync.md)，其中包含描述[發生時……的部分](sync.md#what-happens-when)。

### 貢獻限制 {#contribution-limits}

為了防止垃圾郵件，可以限製成員發佈內容的頻率。 此外，可以自動限制新註冊會員的貢獻。

如需詳細資訊，請參閱[成員貢獻限制](limits.md)。

### 動態建立的使用者群組{#dynamically-created-user-groups}

建立新社群網站時，會動態建立新的使用者群組，其中包含適用於作者環境（請參閱[作者群組角色](#author-group-roles)）或發佈環境（請參閱[發佈群組角色](#publish-group-roles)）中管理社群網站所需的各種管理功能的唯一ID(uid)和權限。

群組名稱是在[社群網站建立](sites-console.md#step13asitetemplate)期間，根據指定網站的名稱產生。 唯一ID可避免相同伺服器上具類似名稱之社群網站和社群群組的命名衝突。

例如，如果網站名稱為「We.Retail Engage」的網站名稱為「*engage*」，則所建立的使用者群組為：

* 社區&#x200B;*參與*&#x200B;成員

## 作者環境{#author-environment}

### 隧道服務{#tunnel-service}

當使用作者環境建立站點](sites-console.md)、[修改站點屬性](sites-console.md#modifying-site-properties)和[管理社區成員和成員組](members.md)時，必須訪問在發佈環境中註冊的用戶和組。[

隧道服務使用作者上的複製代理提供此訪問。

* 如需詳細資訊，請參閱部署頁面上的[設定指示](deploy-communities.md#tunnel-service-on-author)。

[社區成員和組控制台](members.md)僅用於管理僅在發佈環境中註冊的用戶（成員）和用戶組（成員組）。

要管理在作者環境中註冊的用戶和用戶組，請使用[安全控制台](../../help/sites-administering/security.md)

### 作者群組角色{#author-group-roles}

| 如果組成員…… | 主要角色 |
|---|---|
| 管理員 | 管理員組由系統管理員組成，這些系統管理員具有社區管理員的所有能力以及管理社區管理員組的能力。 |
| 社群管理員 | 「社群管理員」群組會自動成為所有社群網站和網站上建立的任何社群群組的成員。 「社群管理員」群組的初始成員為管理員群組。 在作者環境中，社群管理員可以建立社群網站、管理網站、管理成員（他們可以禁止社群成員）以及協調內容。 |
| 社群&lt;*網站名稱*> Sitecontentmanager | 「社群網站內容管理員」可以執行傳統AEM的社群網站製作、內容建立和修改頁面。 |
| 社群支援經理 | 「社群啟用管理員」群組由可供指派以管理社群網站「啟用管理員」群組的使用者組成。 |
| 社群&lt;*網站名稱* >網站啟用管理員 | 「社群網站啟用管理員」群組由指派來管理社群網站啟用[資源](resources.md)的使用者組成。 |
| 無 | 匿名網站訪客可能無法存取作者環境。 |

### 系統管理員{#system-administrators}

管理員群組成員是系統管理員，可為作者和發佈環境執行AEM初始安裝設定。

為了進行展示和開發，管理員群組的成員的使用者ID為&#x200B;*admin*，密碼為&#x200B;*admin*。

對於生產環境，應修改預設的管理員組。

請務必遵循[安全檢查清單](../../help/sites-administering/security-checklist.md)。

## 發佈環境{#publish-environment}

### 成為成員{#becoming-a-member}

在發佈環境中，根據社群網站的[settings](sites-console.md#user-management)，網站訪客可能會成為社群成員：

* 當社群網站為私人（關閉）時：
   * 透過邀請
   * 按管理員的操作

* 當社群網站為公開（開啟）時：
   * 透過自行註冊
   * 透過Facebook和Twitter的社交登入

>[!NOTE]
>
>如果網站訪客註冊為一個開放社群網站的成員，他們會自動成為相同發佈環境中其他開放社群網站的成員。

### 發佈群組角色{#publish-group-roles}

| 如果組成員…… | 主要角色 |
|---|---|
| 社區&lt;*站點名稱*>成員 | 社群網站會員是註冊使用者。 他們可以登入、修改個人檔案、加入開放的社群群組、張貼內容至社群、傳送訊息給其他成員，以及關注網站活動。 |
| 社群&lt;*網站名稱*>協調者 | 社群網站協調者是受信任的社群成員，可以使用協調控制台，或在內容張貼的頁面上，大量協調UGC。 |
| 團體&lt;*站點名*> &lt;*組名*&#x200B;成員 | 社群群組成員是已加入開放社群群組或已受邀加入封閉社群群組的社群成員。 他們具有網站內該社群群組的成員能力。 |
| 團體&lt;*站點名稱*>組管理員 | 社區站點組管理員是受信任的社區成員，被指派在社區站點中建立和管理子社區（組）。 其中包括提供內容內容協調的功能。 |
| *特權成員安全組* | 為限制內容建立而手動建立和維護的使用者群組。 請參閱[特權成員組](#privileged-members-group)。 |
| 無 | 發現網站的匿名網站訪客可能會檢視並搜尋允許匿名存取的社群網站。 為了參與和張貼內容，使用者必須自行註冊（如果允許）並成為社群成員。 |

### 分配成員以發佈組角色{#assigning-members-to-publish-group-roles}

當[在作者環境中建立社區站點](sites-console.md)或[修改站點屬性時，](sites-console.md#modifying-site-properties)成員可以被分配到發佈環境中執行的各種角色，如協調者、組管理員、資源聯繫人或特權成員。

[啟用隧道服](sync.md#accessingpublishusersfromauthor) 務會導致分配選擇由發佈時的成員而不是作者的用戶顯示。

所選成員將自動分配給[適當的組](#publish-group-roles)，並在社區站點被（重新）發佈時包括其成員資格。

### 有特殊權限的成員群組 {#privileged-members-group}

特權成員安全組的目的是將某些社區功能的內容建立限制到社區站點成員的特權子集。

特權成員組是使用[Communities Groups控制台](members.md)建立和管理的成員組。

建立特權成員組後，在[隧道服務啟用](sync.md#accessingpublishusersfromauthor)的情況下，現有社區站點的結構可以是[modified](sites-console.md#modify-structure)，以將其社區功能的配置編輯為「允許特權成員」並添加建立的組。

允許指定一個或多個特權成員組的社區功能包括：

* [部落格功能](functions.md#blog-function) -限制建立新文章。
* [日曆函式](functions.md#calendar-function) -限制建立新事件。
* [論壇功能](functions.md#forum-function) -限制新主題的建立。
* [QnA函式](functions.md#qna-function) -限制建立新問題。

當社群功能未受到保護（未指派特權成員群組）時，所有社群網站成員都可以建立功能內容（文章、事件、主題、問題）。

>[!NOTE]
>
>將用戶添加到社區站點的特權成員組中時，如果用戶也是同一社區站點的成員，則僅授予他們建立權限。

## 建立社區成員{#creating-community-members}

### 儲存庫位置{#repository-location}

為了讓某些功能正常運作，必須建立具有適當權限的使用者和使用者群組。

在`/home/users/community`中建立成員時，這些成員將繼承為成員的配置檔案授予讀取權限的適當ACL。

同樣地，自訂社群使用者群組（例如特權成員群組）應建立在`/home/groups/community`中。

使用[Communities Members and Groups控制台](members.md)將在這些路徑中建立用戶和組。

若要指定自訂路徑，必須使用傳統安全性UI，您可從[https://&lt;server>:&lt;port>/useradmin](http://localhost:4503/useradmin)存取。

要為自定義成員路徑提供讀取權限，在所有發佈實例上，請設定類似`/home/users/community`的ACL:

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

要在所有發佈實例上為自定義成員組路徑（如/home/groups/mycompany）提供適當的權限，請設定類似`/home/groups/community`的ACL:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### 控制台{#consoles}

只有作者環境才提供4種不同的控制台：

| 控制台 | 工具、安全性、使用者 | 工具、安全性、群組 | 社群、成員 | 社群、群組 |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| 管理 | 作者使用者 | 作者的使用者群組 | 發佈時的成員 | 發佈時的成員組 |
| requires | 管理員權限 | 管理員權限 | 管理員權限，隧道服務，發佈群組的使用者同步 | 管理員權限，隧道服務，發佈群組的使用者同步 |

### 社群啟用管理員角色{#community-enablement-manager-role}

對於[啟用社群](overview.md#enablement-community)，通常不允許網站訪客自行註冊，因為每個成員都有相關成本。 使用者在作者上建立網站時，將`enablement manager`[的[角色](#author-group-roles)指派給的](sites-console.md#enablement)（新增為群組`Community <site-name> Siteenablementmanagers`的成員）來管理啟用學員和資源。 `enablement manager`還負責[將學習資源](resources.md)分配給作者的社區成員。

只有全局`Community Enablement Managers`組成員的用戶才能被選擇為特定社區站點的`enablement manager`。

要建立可被指派`Community Site Enablement Manager`角色的用戶，請使用傳統UI安全控制台來指定路徑：

在作者實例上：

1. 以管理員權限登入，瀏覽至傳統UI安全性主控台。

   例如，[http://localhost:4502/useradmin](http://localhost:4502/useradmin)

2. 從「編輯」菜單中，選擇「建立用戶」。****
3. 填寫`Create User`對話方塊。
   * 路徑必須為`/home/users/community`。
4. 選擇 **[!UICONTROL 建立]**。

   ![create-community-user](assets/create-community-user.png)

* 在左窗格中，搜尋新建立的使用者，並選擇顯示在右窗格中。

   ![社群使用者](assets/view-community-user.png)

在左窗格中：

1. 清除搜索框並選擇&#x200B;**[!UICONTROL 隱藏用戶]**。
2. 找到`community-enablementmanagers`並拖曳至右窗格中新使用者的&#x200B;**[!UICONTROL 群組]**&#x200B;標籤。

   ![assign-group](assets/assign-group.png)

### 社區管理員角色{#community-administrators-role}

如[作者群組角色](#author-group-roles)圖表所述，社群管理員群組成員可以建立社群網站、管理網站、管理成員（他們可以禁止社群成員）以及協調內容。

請遵循建立並指派使用者至[啟用管理員](#communitysiteenablementmanagerrole)角色的相同步驟，但在使用者的「群組」標籤下新增c `ommunity-administrators`群組。

### LDAP整合{#ldap-integration}

支AEM持使用LDAP來驗證用戶以及建立用戶帳戶。 這在[使用6](../../help/sites-administering/ldap-config.md)配置LDAPAEM中有詳細說明。

以下是社區成員和成員組的特定配置詳細資訊。

1. 為每個發佈實例配AEM置LDAP。
2. [LDAP身份提供程式](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * 無特殊指示

3. [同步處理程式](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * 設定下列屬性：

      * **[!UICONTROL 使用者自動會籍]**:  `community-<site name>-<uid>-members`
      * **[!UICONTROL 用戶路徑前置詞]**:  `/community`
      * **[!UICONTROL 群組路徑首碼]**:  `/community`

4. [外部登錄模組](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * 無特殊指示

這會導致用戶被自動分配給社區站點的成員組，儲存庫位置為`/home/users/community`和`/home/groups/community` ，因此他們繼承了查看彼此配置檔案的適當權限。

* `User auto membership`值應為`rep:authorizableId`屬性，而非描述檔的`givenName`（顯示名稱）。

## 在例項之AEM間同步用戶{#synchronizing-users-among-aem-instances}

當使用[publish farm](topologies.md)時，請先將使用者匯入至一個例項，然後[讓使用者sync](sync.md)讓Sling將使用者散發至其他發佈例項，以確保使用者在每個發佈例項上擁有相同的路徑。

如果匯入使用者群組，為確保使用者群組在每個發佈例項上擁有相同的路徑，請匯入至一個例項，然後[建立要匯出的套件](../../help/sites-administering/package-manager.md#creating-a-new-package)，並將該套件安裝在所有其他發佈例項上。

雖然透過使用者同步的使用者群組同步將納入未來發行版本，但目前只有使用者群組的&#x200B;*會籍*&#x200B;會員資格會在使用者同步執行時同步。

## 關於社群組{#about-community-groups}

在討論群組時，有兩個不同的主題：

* **[社群群組](overview.md#communitygroups)**

   社群群群組是可在發佈環境中為支援建立社群群組的社群網站建立的子社群。 建立社群群組會產生更多頁面新增至網站，並以類似其父社群網站的方式進行管理。 如需詳細資訊，請造訪開發人員的[社群群組基本資訊](essentials-groups.md)，以及作者的[社群群組](creating-groups.md)。

* **[成員組](../../help/sites-administering/security.md)**

   成員組是成員可屬於的組，並通過組控制台進行管理。 本頁討論的大部分內容都是關於成員組的。 為社區站點自動建立的成員組（前置詞&#x200B;*`Community`*）可以稱為社區組，因此必須考慮討論的上下文。
