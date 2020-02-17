---
title: 管理使用者和使用者群組
seo-title: 管理使用者和使用者群組
description: AEM Communities的使用者可自行註冊並編輯其個人檔案
seo-description: AEM Communities的使用者可自行註冊並編輯其個人檔案
uuid: aeba424e-ea7e-4da5-b94f-ea8af4caa7d2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 774c2553-b629-456b-afa7-5713490f4a0a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 管理使用者和使用者群組 {#managing-users-and-user-groups}

## 概覽 {#overview}

在AEM Communities中，在發佈環境中，使用者可以自行註冊並編輯其個人檔案。 若有適當的權限，他們也可能

* 在社群網站中建立子社群(請參 [閱社群群組](creating-groups.md))
* [協調](moderation.md) (Mederate)使用者產生的內容(UGC)
* 啟用 [資源聯繫人](resources.md)
* 有權 [為部落格](#privileged-members-group) 、日曆、QnA和論壇建立項目

在發佈環境中註冊的使用者通常稱為社 *群成員（成員）* ，以在作者環境中區分*users *。

在從作者環境建立或修改社 [群站點時](#publish-group-roles) ，將成員分配給動態建立的成員（用戶） [組之一](sites-console.md) , [](sites-console.md#modifying-site-properties) 即授予權限。 從作者環境工作時，成員可通過隧道服務從發佈環境中 [看到](#tunnel-service)。

根據設計，在發佈環境中建立的成員和成員組不應出現在作者環境中。 在作者環境中建立的使用者和使用者群組，也會以類似的方式保留在作者環境中。

當作者和發佈成員的使用者來自相同的使用者清單（例如同步自相同的LDAP目錄）時，作者和發佈環境中的使用者不會被視為擁有相同權限和群組成員資格的相同使用者。 成員和使用者的角色必須在發佈和作者（視情況而定）上分別建立。

對於發 [布群](topologies.md)，在一個發佈例項上進行的註冊和修改必須與其他發佈例項同步，以便它們能夠存取相同的使用者資料。 [有關詳細資訊， ](sync.md)請參閱用戶同步[，該同步包含一個描述 ](sync.md#what-happens-when)何時發生…….

### 貢獻限制 {#contribution-limits}

為了防止垃圾郵件，可以限製成員發佈內容的頻率。 此外，可以自動限制新註冊會員的貢獻。

如需詳細資訊，請參 [閱會員貢獻限制](limits.md)。

### 動態建立的使用者群組 {#dynamically-created-user-groups}

建立新社群網站時，會動態建立新的使用者群組，其中包含適用於作者環境(請參閱 [Author Group Roles](#author-group-roles))或發佈環境(請參閱 [Publish Group Roles](#publish-group-roles))中管理社群網站所需之各種管理功能的唯一ID(uid)和權限。

群組名稱是在社群網站建立期間，從指定網站的 [名稱產生](sites-console.md#step13asitetemplate)。 唯一ID可避免相同伺服器上具類似名稱之社群網站和社群群組的命名衝突。

例如，如果網站名稱為「*We.Retail Engage*」的網站名稱為「Engage」，則所建立的使用者群組為：

* 社群 *互動*

## 作者環境 {#author-environment}

### 隧道服務 {#tunnel-service}

使用作者環境建 [立網站](sites-console.md)、修 [改網站屬性](sites-console.md#modifying-site-properties) , [以及管理社群成員和成員群組時](members.md)，必須存取在發佈環境中註冊的使用者和使用者群組。

隧道服務使用作者上的複製代理提供此訪問。

* 如需詳細資訊，請 [參閱部署頁面](deploy-communities.md#tunnel-service-on-author) 上的設定指示

「 [社群成員」和「群組」控制台](members.md) ，僅用於管理僅在發佈環境中註冊的用戶（成員）和用戶組（成員組）。

若要管理在作者環境中註冊的使用者和使用者群組，請使用 [Security Console](../../help/sites-administering/security.md)

### 作者群組角色 {#author-group-roles}

| 如果組成員…… | 主要角色 |
|---|---|
| 管理員 | 管理員組由系統管理員組成，這些系統管理員具有社區管理員的所有能力以及管理社區管理員組的能力。 |
| 社群管理員 | 「社群管理員」群組會自動成為所有社群網站和網站上建立的任何社群群組的成員。 「社群管理員」群組的初始成員為管理員群組。 在作者環境中，社群管理員可以建立社群網站、管理網站、管理成員（他們可以禁止社群成員）以及協調內容。 |
| 社群&lt;網&#x200B;*站名稱*>網站內容管理員 | 「社群網站內容管理員」可以執行傳統的AEM製作、內容建立和修改社群網站的頁面。 |
| 社群支援經理 | 「社群啟用管理員」群組由可供指派以管理社群網站「啟用管理員」群組的使用者組成。 |
| 社群&lt;網&#x200B;*站名稱* >網站啟用管理員 | 「社群網站啟用管理員」群組由指派給管理社群網站啟用資源的使用 [者](resources.md)。 |
| 無 | 匿名網站訪客可能無法存取作者環境。 |

### 系統管理員 {#system-administrators}

管理員群組的成員是系統管理員，可針對作者和發佈環境執行AEM安裝的初始設定。

為了進行展示和開發，管理員群組的使用者ID為admin, *密碼* 為admin *的成員*。

對於生產環境，應修改預設的管理員組。

請務必遵循安全檢 [查清單](../../help/sites-administering/security-checklist.md)。

## 發佈環境 {#publish-environment}

### 成為會員 {#becoming-a-member}

在發佈環境中，視社群網 [站的設定](sites-console.md#user-management) ，網站訪客可能會成為社群成員

* 當社群網站為私人（關閉）時：
   * 透過邀請
   * 按管理員的操作

* 當社群網站為公開（開啟）時：
   * 透過自行註冊
   * 透過Facebook和Twitter的社交登入

>[!NOTE]
>
>如果網站訪客註冊為一個開放社群網站的成員，他們會自動成為相同發佈環境中其他開放社群網站的成員。

### 發佈群組角色 {#publish-group-roles}

| 如果組成員…… | 主要角色 |
|---|---|
| 社群&lt;*網站名稱*>成員 | 社群網站會員是註冊使用者。 他們可以登入、修改個人檔案、加入開放的社群群組、張貼內容至社群、傳送訊息給其他成員，以及關注網站活動。 |
| 社群&lt;網&#x200B;*站名稱*>協調者 | 社群網站協調者是受信任的社群成員，可以使用協調控制台，或在內容張貼的頁面上，大量協調UGC。 |
| 社群&lt;*網站名稱*> &lt;*群組名稱*>成員 | 社群群組成員是已加入開放社群群組或已受邀加入封閉社群群組的社群成員。 他們具有網站內該社群群組的成員能力。 |
| 社群&lt;網&#x200B;*站名稱*>群組管理員 | 社區站點組管理員是受信任的社區成員，被指派在社區站點中建立和管理子社區（組）。 其中包括提供內容內容協調的功能。 |
| *特權成員安全組* | 為限制內容建立而手動建立和維護的使用者群組。 請參閱 [特權成員組](#privileged-members-group)。 |
| 無 | 發現網站的匿名網站訪客可能會檢視並搜尋允許匿名存取的社群網站。 為了參與和張貼內容，使用者必須自行註冊（如果允許）並成為社群成員。 |

### 將成員分配給發佈組角色 {#assigning-members-to-publish-group-roles}

在作 [者環境中建立社群網站](sites-console.md) ，或在修改網站屬性時， [](sites-console.md#modifying-site-properties) ，會將成員指派到發佈環境中執行的各種角色，例如協調者、群組管理員、資源連絡人或特權成員。

[啟用隧道服務](sync.md#accessingpublishusersfromauthor) ，會使指派選擇從發佈時的成員呈現，而非作者的使用者。

選取的成員將自動指派給 [適當的群組](#publish-group-roles) ，而且當社群網站重新發佈時，會納入其會籍。

### 有特殊權限的成員群組 {#privileged-members-group}

特權成員安全組的目的是將某些社區功能的內容建立限制到社區站點成員的特權子集。

特權成員組是使用「社區組」控制台建立和管理的 [成員組](members.md)。

建立特權成員組後，在啟用 [tunnel服務後](sync.md#accessingpublishusersfromauthor)[](sites-console.md#modify-structure) ，可修改現有社區站點的結構，以將其社區功能的配置編輯為「允許特權成員」並添加建立的組。

允許指定一個或多個特權成員組的社區功能包括：

* [部落格功能](functions.md#blog-function) -限制建立新文章
* [日曆函式](functions.md#calendar-function) -限制建立新事件
* [論壇功能](functions.md#forum-function) -限制新主題的建立
* [QnA函式](functions.md#qna-function) -限制新問題的建立

當社群功能未受到保護（未指派特權成員群組）時，所有社群網站成員都可以建立功能內容（文章、事件、主題、問題）。

>[!NOTE]
>
>將用戶添加到社區站點的特權成員組中時，如果用戶也是同一社區站點的成員，則僅授予他們建立權限。

## 建立社區成員 {#creating-community-members}

### 儲存庫位置 {#repository-location}

為了讓某些功能正常運作，必須建立具有適當權限的使用者和使用者群組。

在中建立成員時， `/home/users/community`這些成員將繼承為成員的配置檔案授予讀取權限的正確ACL。

同樣地，自訂社群使用者群組（例如特權成員群組）也應在中建立 `/home/groups/community`。

使用「社 [群成員」和「群組」控制台](members.md) ，將在這些路徑中建立用戶和組。

若要指定自訂路徑，必須使用傳統安全性UI，您可從 [https://&lt;server>:&lt;port>/useradmin存取](http://localhost:4503/useradmin)。

要為自定義成員路徑提供讀取權限，在所有發佈實例上，請設定類似於 `/home/users/community`的ACL:

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

要在所有發佈實例上為自定義成員組路徑（如/home/groups/mycompany）提供適當的權限，請設定ACL類似 `/home/groups/community`:

```xml
<allow
  jcr:primaryType="rep:GrantACE"
  rep:principalName="community-administrators"
  rep:privileges="{Name}[jcr:read]"  />
```

### 控制台 {#consoles}

只有作者環境才提供4種不同的控制台：

| 控制台 | 工具、安全性、使用者 | 工具、安全性、群組 | 社群、成員 | 社群、群組 |
|----------|-----------------------|------------------------|------------------------------------------------------------|------------------------------------------------------------|
| 管理 | 作者使用者 | 作者的使用者群組 | 發佈時的成員 | 發佈時的成員組 |
| requires | 管理員權限 | 管理員權限 | 管理員權限，隧道服務，發佈群組的使用者同步 | 管理員權限，隧道服務，發佈群組的使用者同步 |

### 社群支援管理員角色 {#community-enablement-manager-role}

啟用社群通常不允許網站訪客自行註冊 [](overview.md#enablement-community) ，因為每個成員都有相關成本。 讓使用者管理啟用學員和資源 [的方式](#author-group-roles) ，是指派 `enablement manager` 作 [者在建立網站時](sites-console.md#enablement) (新增為群組成員 `Community <site-name> Siteenablementmanagers`)。 此外， `enablement manager` 還負責指派學 [習資源給社群成員](resources.md) ，讓作者也能參與。

只有全域群組成員的使 `Community Enablement Managers` 用者才能被選為特 `enablement manager` 定社群網站的使用者。

若要建立可指派角色的使用者 `Community Site Enablement Manager`，請使用傳統UI安全性主控台來指定路徑：

在作者實例上：

1. 以管理員權限登入，瀏覽至傳統UI安全性主控台。
例如， [http://localhost:4502/useradmin](http://localhost:4502/useradmin)

2. 從「編輯」菜單中，選擇「創 **[!UICONTROL 建用戶」]**。
3. 填寫對話 `Create User` 框。
   * 路徑必須是 `/home/users/community`
4. 選擇「創 **[!UICONTROL 建」]**

![chlimage_1-130](assets/chlimage_1-130.png)

* 在左窗格中，搜尋新建立的使用者，並選擇顯示在右窗格中。

![chlimage_1-131](assets/chlimage_1-131.png)

在左窗格中：

1. 清除搜索框並選擇隱藏 **[!UICONTROL 用戶]**
2. 找到並拖 `community-enablementmanagers` 曳至右 **** 窗格中新使用者的「群組」索引標籤

![chlimage_1-132](assets/chlimage_1-132.png)

### 社群管理員角色 {#community-administrators-role}

如「作者群組角色 [](#author-group-roles) 」圖表所述，「社群管理員」群組的成員可以建立社群網站、管理網站、管理成員（他們可以禁止社群成員）以及協調內容。

遵循建立使用者並將其指派給啟用管理員角色的相 [同步驟](#communitysiteenablementmanagerrole)，但在使用者的「群 `ommunity-administrators` 組」標籤下新增c群組。

### LDAP整合 {#ldap-integration}

AEM支援使用LDAP來驗證使用者，以及建立使用者帳戶。 這在「使用AEM 6 [設定LDAP」中有詳細說明](../../help/sites-administering/ldap-config.md)。

以下是社區成員和成員組的特定配置詳細資訊。

1. 為每個AEM發佈例項設定LDAP
2. [LDAP身份提供程式](../../help/sites-administering/ldap-config.md#configuring-the-ldap-identity-provider)

   * 無特殊指示

3. [同步處理程式](../../help/sites-administering/ldap-config.md#configuring-the-synchronization-handler)

   * 設定下列屬性：

      * **[!UICONTROL 使用者自動會籍]**: `community-<site name>-<uid>-members`
      * **[!UICONTROL 用戶路徑前置詞]**: `/community`
      * **[!UICONTROL 群組路徑首碼]**: `/community`

4. [外部登錄模組](../../help/sites-administering/ldap-config.md#the-external-login-module)

   * 無特殊指示

這會導致用戶被自動分配給社區站點的成員組和儲存庫位置 `/home/users/community` , `/home/groups/community`以便他們繼承查看彼此配置檔案的適當權限。

* 值 `User auto membership` 應為屬性， `rep:authorizableId` 而非描述 `givenName` 檔的（顯示名稱）。

## 在AEM例項之間同步使用者 {#synchronizing-users-among-aem-instances}

使用發 [布群](topologies.md)，請先將使用者匯入至一個例項，然後讓使用者同步至 [](sync.md) Sling將使用者散發至其他發佈例項，以確保使用者在每個發佈例項上擁有相同的路徑。

如果匯入使用者群組，為確保使用者群組在每個發佈例項上具有相同的路徑，請匯入至一個例項，然後建立要匯出的 [套件](../../help/sites-administering/package-manager.md#creating-a-new-package) ，並將該套件安裝在所有其他發佈例項上。

雖然未來版本將包含透過使用者同步來同步使用者群組的功能，但目前只有使用者群組的*會籍*會在使用者同步執行時同步。

## 關於社群群組 {#about-community-groups}

在討論群組時，有兩個不同的主題：

* **[社群群](overview.md#communitygroups)**組社群群組是在社群網站的發佈環境中建立的子社群，可支援社群群組的建立。 建立社群群組會產生更多頁面新增至網站，並以類似其父社群網站的方式進行管理。 如需詳細資訊，請[造訪開發人員的Community Group Essentials](essentials-groups.md)，以及[作者的Community Group](creating-groups.md)。

* **[成員組](../../help/sites-administering/security.md)**成員組是成員可能屬於的組，並通過組控制台進行管理。 本頁討論的大部分內容都是關於成員組的。 自動為社區站點建立的成員組(前置詞為&#x200B;*`Community`*)可以稱為社區組，因此必須考慮討論的上下文。
