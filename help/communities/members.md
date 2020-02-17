---
title: 成員和組管理控制台
seo-title: 成員和組管理控制台
description: 如何訪問成員和組管理控制台
seo-description: 如何訪問成員和組管理控制台
uuid: 2e93e861-a066-4189-91db-f8b784bc5aea
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ccabf301-b417-48aa-8501-8360fd9f3e36
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 成員和組管理控制台 {#members-groups-management-consoles}

## 概覽 {#overview}

AEM Communities功能通常要求網站訪客必須先註冊並登入，才能參與發佈環境中的社群。 其使用者註冊只需存在於發佈環境中，通常稱為 *成員* ，以區分其與在作者環境中注 *冊的使用者* 。

### 發佈時的成員（使用者） {#members-users-on-publish}

使用「社群成員」和「組」控制台，可以從作者環境建立和管理在 *發佈**環境中註冊的成員和成* 員組。 只有在啟用隧道服務 [時](deploy-communities.md#tunnel-service-on-author) ，才可能。

### 作者使用者 {#users-on-author}

若要管理在作者環境中註冊的使 *用者和群組* ，必須使用平台的安全性主控台：

* 從全域導覽選擇 `Tools, Security, Users`
* 從全域導覽選擇 `Tools, Security, Groups`

>[!NOTE]
>
>在部署並啟用範例內容後，許多範例使用者都存在於作者和發佈環境中。 使用nosamplecontent執行模式執行時，這些使 [用者將不存在](../../help/sites-administering/production-ready.md)。

## 成員控制台 {#members-console}

在作者環境中，要訪問「成員」控制台以管理在發佈環境中註冊的成員：

* 從全域導覽：導 **[!UICONTROL 覽>社群>成員]**

>[!CAUTION]
>
>如果未啟用隧道服務，則無法使 [用](deploy-communities.md#tunnel-service-on-author) Members控制台。

![chlimage_1-119](assets/chlimage_1-119.png)

### 搜尋 {#search-features}

選取標題左側的側面板圖示， `Members` 以切換開啟搜尋側面板。

![chlimage_1-120](assets/chlimage_1-120.png) ![chlimage_1-121](assets/chlimage_1-121.png)

選取標題左側的搜尋圖示，以 `Members` 切換已關閉的搜尋面板。

### 成員統計資訊 {#member-statistics}

當使用者是 `Views`啟用Adobe Analytics的一 `Posts`或多個社群網站的成員時，會顯示、 `Follows`和更新的 `Likes` 欄 [](sites-console.md#analytics)。

### 匯出 CSV {#export-csv}

選取連 `Export CSV` 結會將所有成員下載為逗號分隔值的清單，以適合匯入試算表。

欄標題為

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## 建立新成員 {#create-new-member}

選 `Create Member` 擇以在發佈環境中建立用戶。

![chlimage_1-122](assets/chlimage_1-122.png)

### 一般——成員詳細資訊 {#general-member-details}

大部分欄位都是成員日後可填寫其描述檔的選填欄位。

* **[!UICONTROL ID]**(必&#x200B;*要*)可授權的ID是成員的登入ID。
依預設，ID會設為所需電子郵件地址的值。
   *建立後，ID就無法修改。*

* **[!UICONTROL 電子郵件地址]**(必&#x200B;*要*)成員的電子郵件地址。
成員在更新其個人資料時可能變更其電子郵件地址。如果ID預設為電子郵件地址，則 *當變更* email地址時，ID不會變更。

* **[!UICONTROL 密碼]**(*必要*)登入密碼。

* **[!UICONTROL 重新輸入密碼]**(必&#x200B;*要*)重新輸入密碼以進行驗證。

* **[!UICONTROL 將成員添加到站點]**(*可選*)從現有社區站點中選擇，以便將成員添加到社區站點的成員組。

* **[!UICONTROL 將成員添加到組]**(*可選*)從現有成員組中選擇，以便將成員添加到該組。

* 選擇保 **[!UICONTROL 存]**

### 一般——帳戶設定 {#general-account-settings}

在「帳戶設定」下，社群管理員可以

* **[!UICONTROL 狀態]**
   * UnbandedA會員無法登入，無法檢視頁面或參與需要登入的活動。 他們仍可以匿名造訪開放社群網站。

   * 非禁用A會員可完全存取社群網站。
   預設為 `Not Banned`。

* **[!UICONTROL 貢獻限制]**如果勾選，會員張貼內容的能力就會受到限制。
預設值取決於貢獻限制的設定。
請參 [閱會員繳費限制](limits.md)。

* **[!UICONTROL 更改密]**&#x200B;碼修改現有成員時存在的連結。 提供社區管理員重設成員密碼的能力。

### 一般——像片 {#general-photo}

若要為成員提供頭像，請先選取「 **[!UICONTROL 上傳影像]** 」，然後選擇。jpg、.png、.tif或。gif類型的影像。 影像的偏好大小為240 x 240像素，72 dpi。

### GENERAL - Add Member to Sites {#general-add-member-to-sites}

該成員可以添加到一個或多個社區站點的成員組。 首先，在文字方塊中輸入文字。

### GENERAL - Add Member to Groups {#general-add-member-to-groups}

成員可以添加到一個或多個成員組。 首先，在文字方塊中輸入文字。

### 標章標籤 {#badges-tab}

此面 `BADGES` 板提供手動指派徽章及廢止徽章的功能。 標章可用於指派的角色以及通常應得的標章。

另請參閱 [計分和標章](implementing-scoring.md)。

![chlimage_1-123](assets/chlimage_1-123.png)

* **[!UICONTROL 新增標章]**
   * 開始鍵入以從可用標 [章中選擇](badges.md)。 選取徽章後，請選擇每個網站或所有網站，此徽章應與成員的頭像一起顯示在這些網站上。
   * 可以選擇多個標章和網站。
* **[!UICONTROL 移除標章]**
   * 選取徽章旁邊的垃圾桶圖示以移除它

## 群組主控台 {#groups-console}

「群組」控制台可從作者環境使用，允許建立和管理在發佈環境中註冊的成員組。 它對於：
* [特權成員組](users.md#privilegedmembersgroups)
* 基於組的啟用資 [源分配](resources.md)

要訪問組控制台：
* 從全域導覽：導 **[!UICONTROL 覽>社群>群組]**

>[!CAUTION]
>
>如果未啟用隧道服務，則無法使 [用組](deploy-communities.md#tunnel-service-on-author) 控制台。

### 建立新群組 {#create-new-group}

選 `Add Group` 取以在發佈環境中建立群組。

![chlimage_1-124](assets/chlimage_1-124.png)

建立新發佈端成員組的必填欄位包括：

* **[!UICONTROL ID]**(必&#x200B;*要*)群組唯一ID。
   *建立後，ID就無法修改。*

* **[!UICONTROL 名稱]**(*可選*)群組的顯示名稱。

   預設值為ID。

* **[!UICONTROL 說明]**(*可選*)群組用途和權限的說明。

* **[!UICONTROL 新增成員至群組]**(*可選*)選取要納入為群組初始成員的發佈端成員。

* 選擇保 **[!UICONTROL 存]**

## 授權管理員 {#authorized-administrators}

在Communities成員控制台中使用成員時，必須以具有適當權限的用戶身份登錄，並且要正確配置隧道服務所使用的 [複製代理](deploy-communities.md#tunnel-service-on-author) 。

如果未登入為 `admin`，則登入的使用者必須是使用者群組的 `administrators` 成員。

另請參 [閱Author上的複製代理](deploy-communities.md#replication-agents-on-author)。
