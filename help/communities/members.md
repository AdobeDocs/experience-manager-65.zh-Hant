---
title: 成員與群組管理主控台
description: 如何存取成員與群組管理主控台
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: b64e24d2-8407-484c-8216-8d328ef5fa4f
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 1%

---


# 成員與群組管理主控台 {#members-groups-management-consoles}

## 概觀 {#overview}

AEM Communities功能通常要求網站訪客先註冊並登入，才能參與發佈環境的社群。 他們的使用者註冊只需要存在於發佈環境中，通常稱為&#x200B;*成員*，以區別於在作者環境中註冊的&#x200B;*使用者*。

### Publish上的成員（使用者） {#members-users-on-publish}

使用Communities成員和群組主控台，可在&#x200B;*發佈*&#x200B;環境中註冊的成員和成員群組可從&#x200B;*作者*&#x200B;環境建立和管理。 只有啟用[通道服務](deploy-communities.md#tunnel-service-on-author)時，才可以執行此動作。

### 作者上的使用者 {#users-on-author}

若要管理在&#x200B;*作者*&#x200B;環境中註冊的使用者和群組，必須使用平台的安全性主控台：

* 從全域導覽中選取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]**。
* 從全域導覽中選取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 群組]**。

>[!NOTE]
>
>部署並啟用範例內容後，製作和發佈環境中都會存在許多範例使用者。 使用[nosamplecontent執行模式](../../help/sites-administering/production-ready.md)執行時，這些使用者將不會出現。

## 成員主控台 {#members-console}

在作者環境中，若要存取「成員」主控台以管理在發佈環境中註冊的成員：

* 從全域導覽中，選取&#x200B;**[!UICONTROL 導覽]** > **[!UICONTROL 社群]** > **[!UICONTROL 成員]**

>[!CAUTION]
>
>如果未啟用[通道服務](deploy-communities.md#tunnel-service-on-author)，將無法使用[成員]主控台。

![成員主控台](assets/member-console1.png)

### 搜尋 {#search-features}

選取`Members`標題左側的側面板圖示，以切換開啟搜尋側面板。

![搜尋側面板圖示。](assets/leftpanel-icon.png)


![成員主控台的篩選選項](assets/member-console2.png)

選取`Members`標題左側的搜尋圖示，將搜尋側面板切換為關閉。

### 成員統計資料 {#member-statistics}

顯示`Views`、`Posts`、`Follows`和`Likes`的欄會在使用者為啟用Adobe Analytics [的一或多個社群網站成員時更新](sites-console.md#analytics)。

### 匯出 CSV {#export-csv}

選取`Export CSV`連結會以逗號分隔值清單的形式下載所有成員，適合匯入試算表。

欄標題為

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## 建立新成員 {#create-new-member}

選取`Create Member`以在發佈環境中建立使用者。

![建立新成員視窗](assets/create-member1.png)

### 一般 — 成員詳細資訊 {#general-member-details}

大多數欄位是可選欄位，成員稍後可填寫其設定檔。

* **[!UICONTROL 識別碼]**

（*必要*）可授權識別碼是成員的登入識別碼。
根據預設，ID會設定為所需電子郵件地址的值。
*建立之後，ID就不可修改*。

* **[!UICONTROL 電子郵件地址]**

（*必要*）成員的電子郵件地址。
成員可以在更新設定檔時變更電子郵件地址。I
若此ID預設為電子郵件地址，則當電子郵件地址變更時，此ID將*不會*&#x200B;變更。

* **[!UICONTROL 密碼]**

  （*必要*）登入密碼。

* **[!UICONTROL Retype密碼]**

  （*必要*）請重新輸入密碼以進行驗證。

* **[!UICONTROL 新增成員至網站]**

  （*選擇性*）從現有的社群網站中選取，以將成員新增至社群網站的成員群組。

* **[!UICONTROL 新增成員至群組]**

  （*選擇性*）從現有的成員群組中選取，以將成員新增至該群組。

* 選取&#x200B;**[!UICONTROL 儲存]**

### 一般 — 帳戶設定 {#general-account-settings}

在「帳戶設定」底下，社群管理員可以：

* **[!UICONTROL 狀態]**
   * 已禁止
成員無法登入，導致他們無法檢視頁面或參與需要登入的活動。 他們仍可匿名造訪開放的社群網站。

   * 未禁止
成員具有社群網站的完整存取權。

  預設值為`Not Banned`。

* **[!UICONTROL 貢獻限制]**

  如果勾選，則成員發佈內容的能力有限。
預設值視貢獻限制的設定而定。
請參閱[成員貢獻限制](limits.md)。

* **[!UICONTROL 變更密碼]**

  修改現有成員時顯示的連結。 提供社群管理員重設成員密碼的功能。

### 一般 — 像片 {#general-photo}

若要提供成員的顯示圖片，請先選取&#x200B;**[!UICONTROL 上傳影像]**，然後選擇型別為.jpg、.png、.tif或.gif的影像。 影像的偏好大小為240 x 240畫素，畫素為72 dpi。

### 一般 — 新增成員至網站 {#general-add-member-to-sites}

成員可以新增至一或多個社群網站的成員群組。 首先，在文字方塊中輸入文字。

### 一般 — 新增成員至群組 {#general-add-member-to-groups}

成員可以新增至一或多個成員群組。 首先，在文字方塊中輸入文字。

### 徽章索引標籤 {#badges-tab}

`BADGES`面板提供手動指派徽章並撤銷的功能。 徽章可能是用於指派的角色和通常獲得的徽章。

另請參閱[評分與徽章](implementing-scoring.md)。

![編輯成員資格設定視窗](assets/create-member2.png)

* **[!UICONTROL 新增徽章]**
   * 開始輸入以從[可用的徽章](badges.md)中選取。 選取徽章後，請選擇每個網站或所有網站，徽章應隨成員頭像一起顯示。
   * 可選擇多個徽章和網站。
* **[!UICONTROL 移除徽章]**
   * 選取徽章旁的垃圾桶圖示以將其移除。

## 群組主控台 {#groups-console}

「群組」主控台可從製作環境取得，可讓您建立和管理在發佈環境中註冊的成員群組。 它對[有特殊許可權的成員群組](users.md#privilegedmembersgroups)特別有用。

若要存取「群組」主控台：
* 從全域導覽中，選取&#x200B;**[!UICONTROL 導覽]** > **[!UICONTROL 社群]** > **[!UICONTROL 群組]**。

>[!CAUTION]
>
>如果未啟用[通道服務](deploy-communities.md#tunnel-service-on-author)，將無法使用群組主控台。

### 建立新群組 {#create-new-group}

選取`Add Group`以在發佈環境中建立群組。

![建立新群組視窗](assets/group-console1.png)

建立發佈端成員群組的必填欄位包括：

* **[!UICONTROL 識別碼]**

  （*必要*）群組唯一識別碼。

  *建立之後，ID就不可修改。*

* **[!UICONTROL 名稱]**

  (*Optional*)群組的顯示名稱。

  預設值為ID。

* **[!UICONTROL 說明]**

  (*Optional*)群組用途與許可權的說明。

* **[!UICONTROL 新增成員至群組]**

  （*選擇性*）選取要作為群組初始成員包含的發佈端成員。

* 選取&#x200B;**[!UICONTROL 儲存]**

## 授權管理員 {#authorized-administrators}

使用Communities成員主控台中的成員時，必須以具有適當許可權的使用者身分登入，且必須正確設定[通道服務](deploy-communities.md#tunnel-service-on-author)所使用的復寫代理程式。

如果未以`admin`登入，則登入使用者必須是`administrators`使用者群組的成員。

另請參閱作者[&#128279;](deploy-communities.md#replication-agents-on-author)上的復寫代理。
