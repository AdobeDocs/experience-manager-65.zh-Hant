---
title: 管理使用者和使用者群組
seo-title: 管理使用者和使用者群組
description: AEM Communities的使用者可以自行註冊和編輯其設定檔
seo-description: AEM Communities的使用者可以自行註冊和編輯其設定檔
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
source-wordcount: '2183'
ht-degree: 0%

---

# 管理使用者和使用者群組 {#managing-users-and-user-groups}

## 概覽 {#overview}

在AEM Communities中，使用者可在發佈環境中自行註冊和編輯其設定檔。 有了適當的權限，他們也可以：

* 在社群網站內建立子社群（請參閱[社群群組](creating-groups.md)）。

* [](moderation.md) 協調使用者產生的內容(UGC)。

* 是[啟用資源](resources.md)聯繫人。

* 為[特權](#privileged-members-group)建立部落格、日曆、QnA和論壇的條目。

在發佈環境中註冊的使用者通常稱為&#x200B;*社群成員（成員）*，以便與製作環境中的&#x200B;*使用者*&#x200B;區分。

權限的授予方式是將成員分配給在社區站點從作者環境建立[](sites-console.md)或[已修改](sites-console.md#modifying-site-properties)時動態建立的[成員（用戶）組之一。 ](#publish-group-roles)從製作環境工作時，會透過[tunnel服務](#tunnel-service)從發佈環境中看到成員。

根據設計，在發佈環境中建立的成員和成員組不應出現在製作環境中。 在製作環境中建立的使用者和使用者群組，也同樣打算保留在製作環境中。

當製作使用者和發佈成員的使用者來自相同的使用者清單時（例如從相同的LDAP目錄同步），在製作和發佈環境中，他們不會被視為具有相同權限和群組成員資格的相同使用者。 成員和使用者的角色必須在發佈時和作者時酌情分別建立。

對於[publish farm](topologies.md)，一個發佈實例上的註冊和修改需要與其他發佈實例同步，以便它們能夠訪問相同的用戶資料。 有關詳細資訊，請參閱[用戶同步](sync.md)，其中包括描述[發生時……的部分](sync.md#what-happens-when)。

### 貢獻限制 {#contribution-limits}

為了防止垃圾郵件，可以限製成員發佈內容的頻率。 此外，可以自動限制新註冊成員的繳款。

如需詳細資訊，請參閱[成員貢獻限制](limits.md)。

### 動態建立的使用者群組 {#dynamically-created-user-groups}

建立新社群網站時，系統會以唯一ID(uid)和權限動態建立新使用者群組，這些權限適用於在製作環境（請參閱[製作群組角色](#author-group-roles)）或發佈環境（請參閱[發佈群組角色](#publish-group-roles)）中管理社群網站所需的各種管理功能。

群組的名稱是在[社群網站建立](sites-console.md#step13asitetemplate)期間從指定網站的名稱產生。 唯一ID可避免同一伺服器上同樣命名之社群網站和社群群組的命名衝突。

例如，如果網站名稱為「*engage*」，則所建立的使用者群組之一是：

* 社區&#x200B;*參與*&#x200B;成員

## 製作環境 {#author-environment}

### 通道服務 {#tunnel-service}

使用製作環境[建立網站](sites-console.md)、[修改網站屬性](sites-console.md#modifying-site-properties)和[管理社群成員和成員群組](members.md)時，必須存取在發佈環境中註冊的使用者和使用者群組。

隧道服務使用製作上的復寫代理提供此存取。

* 如需詳細資訊，請參閱部署頁面上的[配置指示](deploy-communities.md#tunnel-service-on-author)。

[Communities成員和組控制台](members.md)僅用於管理僅在發佈環境中註冊的用戶（成員）和用戶組（成員組）。

若要管理在製作環境中註冊的使用者和使用者群組，請使用[安全主控台](../../help/sites-administering/security.md)

### 作者群組角色 {#author-group-roles}

| 如果組成員…… | 主要角色 |
|---|---|
| 管理員 | 管理員組由系統管理員組成，他們具有社區管理員的所有能力以及管理社區管理員組的能力。 |
| 社群管理員 | 社區管理員組自動成為所有社區站點和站點上建立的任何社區組的成員。 社區管理員組的初始成員是管理員組。 在製作環境中，社群管理員可以建立社群網站、管理網站、管理成員（他們可以禁止社群的成員），以及協調內容。 |
| 社群&lt;*網站名稱*> Sitecontentmanager | 「社群網站內容管理員」可以執行傳統的AEM製作、內容建立和社群網站的修改頁面。 |
| 社群培訓經理 | 「社群啟用管理員」群組包含可供指派管理社群網站「啟用管理員」群組的使用者。 |
| 社區&lt;*站點名稱* > Siteenablementmanagers | 「社群網站啟用管理員」群組包含指派給管理社群網站啟用[資源](resources.md)的使用者。 |
| 無 | 匿名網站訪客可能無法存取製作環境。 |

### 系統管理員 {#system-administrators}

管理員群組的成員是系統管理員，可為製作和發佈環境執行AEM安裝的初始設定。

為了進行演示和開發，管理員組的用戶ID為&#x200B;*admin*&#x200B;且密碼為&#x200B;*admin*&#x200B;的成員。

對於生產環境，應修改預設管理員群組。

請務必遵循[安全檢查清單](../../help/sites-administering/security-checklist.md)。

## 發佈環境 {#publish-environment}

### 成為會員 {#becoming-a-member}

在發佈環境中，視社群網站的[settings](sites-console.md#user-management)而定，網站訪客可能會成為社群成員：

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
| 社區&lt;*站點名稱*>成員 | 社區站點成員是註冊用戶。 他們可以登入、修改其設定檔、加入開放的社群群組、將內容張貼至社群、傳送訊息給其他成員，以及遵循網站活動。 |
| 社群&lt;*網站名稱*>協調者 | 社群網站協調者是值得信賴的社群成員，可以在張貼內容的頁面上，使用協調控制台或內容來大量協調UGC。 |
| 社區&lt;*站點名*> &lt;*組名*>成員 | 社群群組成員是已加入開放社群群組或受邀加入封閉社群群組的社群成員。 他們具有網站內該社群群組的成員的能力。 |
| 社區&lt;*站點名稱*>組管理員 | 社區站點組管理員是受信任的社區成員，被分配來建立和管理社區站點內的子社區（組）。 其中包括提供內容內協調的功能。 |
| *特權成員安全組* | 為限制內容建立而手動建立和維護的使用者群組。 請參閱[特權成員組](#privileged-members-group)。 |
| 無 | 探索到網站的匿名網站訪客可以檢視並搜尋允許匿名存取的社群網站。 若要參與並張貼內容，使用者必須自行註冊（如果允許）並成為社群成員。 |

### 為發佈組角色分配成員 {#assigning-members-to-publish-group-roles}

當[在作者環境中建立社群網站](sites-console.md)時，或當[修改網站屬性時，](sites-console.md#modifying-site-properties)成員可被指派在發佈環境中執行的各種角色，例如協調者、群組管理員、資源聯絡人或有權限的成員。

[啟用通道服](sync.md#accessingpublishusersfromauthor) 務會導致在發佈時從成員而不是作者上的用戶顯示分配選擇。

所選成員將自動分配給[相應的組](#publish-group-roles)，並且當社區站點（重新）發佈時將包括其成員資格。

### 有特殊權限的成員群組 {#privileged-members-group}

特權成員安全組的目的是將某些社區功能的內容建立限制在社區站點成員的特權子集。

特權成員組是使用[Communities組控制台](members.md)建立和管理的成員組。

建立特權成員組後，在[tunnel服務啟用](sync.md#accessingpublishusersfromauthor)的情況下，現有社區站點的結構可以是[modified](sites-console.md#modify-structure)，以編輯其社區功能的配置，使其為「允許特權成員」並添加已建立的組。

允許指定一個或多個特權成員組的社區功能包括：

* [部落格功能](functions.md#blog-function)  — 限制建立新文章。
* [日曆函式](functions.md#calendar-function)  — 限制建立新事件。
* [論壇功能](functions.md#forum-function)  — 限制建立新主題。
* [QnA函式](functions.md#qna-function)  — 限制建立新問題。

當社群功能未受到保護時（未分配特權成員組），則允許所有社區站點成員建立功能內容（文章、事件、主題、問題）。

>[!NOTE]
>
>只有將用戶添加到社區站點的特權成員組時，如果用戶也是同一社區站點的成員，則只授予他們建立權限。

## 建立社群成員 {#creating-community-members}

### 儲存庫位置 {#repository-location}

為了讓某些功能正常運作，需要建立具有適當權限的使用者和使用者群組。

在`/home/users/community`中建立成員時，它們將繼承為成員的配置檔案提供讀取權限的正確ACL。

同樣，自訂社群使用者群組（例如有權限的成員群組）也應建立在`/home/groups/community`中。

使用[Communities Members and Groups控制台](members.md)將在這些路徑中建立用戶和組。

若要指定自訂路徑，必須使用傳統安全UI，可在[https://&lt;server>:&lt;port>/useradmin](http://localhost:4503/useradmin)存取。

要為自定義成員路徑授予讀取權限，請在所有發佈實例上設定類似於`/home/users/community`的ACL:

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

要在所有發佈實例上為自定義成員組路徑（如/home/groups/mycompany）提供適當的權限，請設定類似於`/home/groups/community`的ACL:

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

網站訪客自行註冊的能力通常不允許用於[啟用社群](overview.md#enablement-community)，因為每個成員都有相關的成本。 在作者的網站建立期間](sites-console.md#enablement)，由指派`enablement manager` [的[角色](#author-group-roles)的使用者管理啟用學習者和資源（新增為群組`Community <site-name> Siteenablementmanagers`的成員）。 `enablement manager`還負責[將學習資源](resources.md)指派給作者的社群成員。

只有全局`Community Enablement Managers`組成員的用戶才能被選擇為特定社區站點的`enablement manager`。

要建立可被分配`Community Site Enablement Manager`角色的用戶，請使用傳統UI安全控制台來指定路徑：

在製作例項上：

1. 以管理員權限登入，瀏覽至傳統UI安全主控台。

   例如， [http://localhost:4502/useradmin](http://localhost:4502/useradmin)

2. 從「編輯」菜單中，選擇「建立用戶」**[!UICONTROL 。]**
3. 填寫`Create User`對話方塊。
   * 路徑必須為`/home/users/community`。
4. 選擇 **[!UICONTROL 建立]**。

   ![create-community-user](assets/create-community-user.png)

* 在左窗格中，搜索新建立的用戶並選擇顯示在右窗格中。

   ![社群使用者](assets/view-community-user.png)

在左窗格中：

1. 清除搜索框並選擇&#x200B;**[!UICONTROL 隱藏用戶]**。
2. 找到`community-enablementmanagers`並拖曳至右窗格中新使用者的&#x200B;**[!UICONTROL 群組]**&#x200B;標籤。

   ![assign-group](assets/assign-group.png)

### 社群管理員角色 {#community-administrators-role}

如[作者群組角色](#author-group-roles)圖表所述，社群管理員群組成員可以建立社群網站、管理網站、管理成員（他們可以禁止社群成員），以及協調內容。

按照建立用戶並將其分配給[啟用管理器](#communitysiteenablementmanagerrole)角色的相同步驟操作，但在用戶的「組」頁簽下添加c `ommunity-administrators`組。

### LDAP整合 {#ldap-integration}

AEM支援使用LDAP來驗證使用者以及建立使用者帳戶。 在[使用AEM 6](../../help/sites-administering/ldap-config.md)配置LDAP中會詳細說明。

以下是特定於社區成員和成員組的一些配置詳細資訊。

1. 為每個AEM發佈執行個體配置LDAP。
2. [LDAP標識提供程式](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * 無特殊說明

3. [同步處理程式](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * 設定下列屬性：

      * **[!UICONTROL 用戶自動成員資格]**:  `community-<site name>-<uid>-members`
      * **[!UICONTROL 用戶路徑前置詞]**:  `/community`
      * **[!UICONTROL 群組路徑首碼]**:  `/community`

4. [外部登入模組](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * 無特殊指示

這會導致用戶被自動分配給社區站點的成員組，而儲存庫位置為`/home/users/community`和`/home/groups/community`，這樣他們就繼承了查看彼此配置檔案的相應權限。

* `User auto membership`值應為`rep:authorizableId`屬性，而非設定檔的`givenName`（顯示名稱）。

## 在AEM執行個體之間同步使用者 {#synchronizing-users-among-aem-instances}

使用[publish farm](topologies.md)時，請先將使用者匯入至一個例項，並[讓使用者同步](sync.md)以Sling將使用者散布至其他發佈例項，以確保使用者在每個發佈例項上擁有相同的路徑。

如果匯入使用者群組，為確保使用者群組在每個發佈執行個體上擁有相同的路徑，請匯入至一個執行個體，然後[建立要匯出的套件](../../help/sites-administering/package-manager.md#creating-a-new-package)，並將該套件安裝在所有其他發佈執行個體上。

雖然透過使用者同步同步的使用者群組將納入未來的發行版本中，目前只有使用者群組的&#x200B;*成員資格*&#x200B;會在使用者同步執行時同步。

## 關於社群群組 {#about-community-groups}

討論群組時，有兩個不同的主題：

* **[社群群組](overview.md#communitygroups)**

   社群群組是可在發佈環境中為社群網站建立的子社群，可支援社群群組的建立。 建立社群群組會導致網站新增更多頁面，且以類似於其父社群網站的方式進行管理。 如需詳細資訊，請造訪開發人員的[社群群組要點](essentials-groups.md)和作者的[社群群組](creating-groups.md)。

* **[成員組](../../help/sites-administering/security.md)**

   成員組是成員可能屬於的組，並通過組控制台進行管理。 本頁討論的大部分內容都專門討論成員組。 為社區站點自動建立的成員組（前置詞為&#x200B;*`Community`*）可以稱為社區組，因此必須考慮討論的上下文。
