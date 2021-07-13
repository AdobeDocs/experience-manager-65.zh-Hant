---
title: 成員和群組管理主控台
seo-title: 成員和群組管理主控台
description: 如何存取成員和群組管理主控台
seo-description: 如何存取成員和群組管理主控台
uuid: 2e93e861-a066-4189-91db-f8b784bc5aea
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ccabf301-b417-48aa-8501-8360fd9f3e36
role: Admin
exl-id: b64e24d2-8407-484c-8216-8d328ef5fa4f
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 4%

---

# 成員和群組管理主控台 {#members-groups-management-consoles}

## 概覽 {#overview}

AEM Communities功能通常會要求網站訪客在參與發佈環境的社群之前，必須先註冊及登入。 其使用者註冊僅需存在於發佈環境中，通常稱為&#x200B;*members*，以便與在製作環境中註冊的&#x200B;*users*&#x200B;區分。

### 發佈時的成員（用戶） {#members-users-on-publish}

使用「社區成員和組」控制台，可以從&#x200B;*author*&#x200B;環境建立和管理在&#x200B;*publish*&#x200B;環境中註冊的成員和成員組。 只有啟用[tunnel服務](deploy-communities.md#tunnel-service-on-author)時，才能執行此操作。

### 作者使用者 {#users-on-author}

若要管理在&#x200B;*author*&#x200B;環境中註冊的使用者和群組，必須使用平台的安全性主控台：

* 從全局導航中，選擇&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 用戶]**。
* 從全局導航中，選擇&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 組]**。

>[!NOTE]
>
>在部署並啟用範例內容後，許多範例使用者同時存在於製作和發佈環境中。 使用[nosamplecontent執行模式](../../help/sites-administering/production-ready.md)執行時，這些使用者將不存在。

## 成員控制台 {#members-console}

在製作環境中，若要進入「成員」主控台，以管理在發佈環境中註冊的成員：

* 從全局導航中，選擇&#x200B;**[!UICONTROL 導航]** > **[!UICONTROL 社區]** > **[!UICONTROL 成員]**

>[!CAUTION]
>
>如果未啟用[tunnel服務](deploy-communities.md#tunnel-service-on-author)，則無法使用成員控制台。

![member-console1](assets/member-console1.png)

### 搜尋 {#search-features}

選取`Members`標題左側的側面板圖示，以開啟搜尋側面板。

![](assets/leftpanel-icon.png)


![member-console2](assets/member-console2.png)

選取`Members`標題左側的搜尋圖示，以切換關閉搜尋端面板。

### 成員統計資訊 {#member-statistics}

當使用者為一或多個已啟用Adobe Analytics [的社群網站的成員時，會更新顯示`Views`、`Posts`、`Follows`和`Likes`的欄。](sites-console.md#analytics)

### 匯出 CSV {#export-csv}

選擇`Export CSV`連結會將所有成員下載為逗號分隔值清單，以便導入電子錶格。

欄標題為

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## 建立新成員 {#create-new-member}

選取`Create Member`以在發佈環境中建立使用者。

![create-member1](assets/create-member1.png)

### 一般 — 成員詳細資訊 {#general-member-details}

大多數欄位是成員以後可以在其配置檔案中填寫的可選欄位。

* **[!UICONTROL ID]**

（*必要*）可授權ID是成員的登入ID。
依預設，ID會設為必要電子郵件地址的值。
*ID一經建立即無法修改*。

* **[!UICONTROL 電子郵件地址]**

（*必要*）成員的電子郵件地址。
成員在更新其配置檔案時可更改其電子郵件地址。
如果ID預設為電子郵件地址，當電子郵件地址變更時，ID將*not*&#x200B;變更。

* **[!UICONTROL 密碼]**

   （*必要*）登入密碼。

* **[!UICONTROL 重新鍵入密碼]**

   （*必要*）重新輸入密碼以進行驗證。

* **[!UICONTROL 新增成員至網站]**

   （*可選*）從現有社區站點中選擇以將成員添加到社區站點的成員組。

* **[!UICONTROL 將成員新增至群組]**

   （*可選*）從現有成員組中選擇以將成員添加到該組。

* 選擇&#x200B;**[!UICONTROL 保存]**

### 一般 — 帳戶設定 {#general-account-settings}

在「帳戶設定」下，社區管理員可以：

* **[!UICONTROL 狀態]**
   * 已禁止
成員無法登入，無法檢視頁面或參與需要登入的活動。 他們仍可以匿名訪問開放的社區站點。

   * 未禁止
成員可以完全訪問社區站點。

   預設值為`Not Banned`。

* **[!UICONTROL 貢獻限制]**

   如果勾選此選項，成員張貼內容的能力就會受限。
預設值取決於貢獻限制的設定。
請參閱[成員貢獻限制](limits.md)。

* **[!UICONTROL 變更密碼]**

   修改現有成員時出現的連結。 提供社區管理員重置成員密碼的功能。

### 一般 — 照片 {#general-photo}

要為成員提供頭像，請從選擇&#x200B;**[!UICONTROL 上載影像]**&#x200B;開始，並選擇類型為.jpg、.png、.tif或.gif的影像。 影像的優選大小為240 x 240像素，72 dpi。

### 常規 — 向站點添加成員 {#general-add-member-to-sites}

該成員可以添加到一個或多個社區站點的成員組。 首先，在文字方塊中輸入文字。

### 一般 — 向組添加成員 {#general-add-member-to-groups}

該成員可以添加到一個或多個成員組。 首先，在文字方塊中輸入文字。

### 徽章標籤 {#badges-tab}

`BADGES`面板提供手動指派徽章及撤銷徽章的功能。 徽章可用於指派的角色，以及通常獲得的徽章。

另請參閱[計分和徽章](implementing-scoring.md)。

![create-member2](assets/create-member2.png)

* **[!UICONTROL 新增徽章]**
   * 開始鍵入以從[可用徽章](badges.md)中選擇。 選擇徽章後，選擇應在其上與成員的頭像一起顯示徽章的每個站點或所有站點。
   * 可選擇多個徽章和網站。
* **[!UICONTROL 移除徽章]**
   * 選取徽章旁的垃圾桶圖示以移除它。

## 群組主控台 {#groups-console}

「群組」主控台可從製作環境取得，可建立及管理在發佈環境中註冊的成員群組。 它對以下方面特別有用：
* [特權成員組](users.md#privilegedmembersgroups)
* 基於組的[啟用資源分配](resources.md)

若要存取「群組」主控台：
* 從全局導航中，選擇&#x200B;**[!UICONTROL 導航]** > **[!UICONTROL 社區]** > **[!UICONTROL 組]**。

>[!CAUTION]
>
>如果未啟用[tunnel服務](deploy-communities.md#tunnel-service-on-author)，則無法使用組控制台。

### 建立新群組 {#create-new-group}

選取`Add Group`以在發佈環境中建立群組。

![group-console1](assets/group-console1.png)

建立新發佈端成員組的必填欄位為：

* **[!UICONTROL ID]**

   （*必要*）群組唯一ID。

   *ID一經建立即無法修改。*

* **[!UICONTROL 名稱]**

   （*選用*）群組的顯示名稱。

   預設值為ID。

* **[!UICONTROL 說明]**

   （*選用*）群組用途和權限的說明。

* **[!UICONTROL 將成員新增至群組]**

   （*選用*）選取要納入為群組初始成員的發佈端成員。

* 選擇&#x200B;**[!UICONTROL 保存]**

## 授權管理員 {#authorized-administrators}

在Communities成員控制台中使用成員時，必須以具有適當權限的用戶身份登錄，並且要正確配置[隧道服務](deploy-communities.md#tunnel-service-on-author)所使用的複製代理。

如果未以`admin`身份登錄，則登錄的用戶必須是`administrators`用戶組的成員。

另請參閱[製作上的復寫代理](deploy-communities.md#replication-agents-on-author)。
