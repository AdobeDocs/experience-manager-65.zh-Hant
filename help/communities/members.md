---
title: 成員與群組管理主控台
description: 如何存取成員與群組管理主控台
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: b64e24d2-8407-484c-8216-8d328ef5fa4f
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 3%

---


# 成員與群組管理主控台 {#members-groups-management-consoles}

## 概觀 {#overview}

AEM Communities功能通常要求網站訪客先註冊並登入，才能參與發佈環境的社群。 他們的使用者註冊只需要存在於發佈環境中，通常稱為 *成員* 以區別他們 *使用者* 已在作者環境中註冊。

### 發佈上的成員（使用者） {#members-users-on-publish}

使用在中註冊的Communities成員和群組主控台、成員和成員群組 *發佈* 環境可從以下位置建立和管理： *作者* 環境。 只有當 [通道服務](deploy-communities.md#tunnel-service-on-author) 已啟用。

### 作者上的使用者 {#users-on-author}

用於管理在中註冊的使用者和群組 *作者* 環境，必須使用平台的安全性主控台：

* 在全域導覽中選取 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]**.
* 在全域導覽中選取 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 群組]**.

>[!NOTE]
>
>部署並啟用範例內容後，製作和發佈環境中都會存在許多範例使用者。 執行時，這些使用者將不會出現 [nosamplecontent執行模式](../../help/sites-administering/production-ready.md).

## 成員主控台 {#members-console}

在作者環境中，若要存取「成員」主控台以管理在發佈環境中註冊的成員：

* 在全域導覽中選取 **[!UICONTROL 導覽]** > **[!UICONTROL Communities]** > **[!UICONTROL 成員]**

>[!CAUTION]
>
>如果符合以下條件，則無法使用成員主控台： [通道服務](deploy-communities.md#tunnel-service-on-author) 未啟用。

![成員主控台](assets/member-console1.png)

### 搜尋 {#search-features}

選取左側面板圖示 `Members` 標題以切換開啟搜尋側面板。

![搜尋側面板圖示。](assets/leftpanel-icon.png)


![成員主控台的篩選選項](assets/member-console2.png)

選取左側的搜尋圖示 `Members` 標題可將搜尋側面板切換為關閉。

### 成員統計資料 {#member-statistics}

顯示的欄 `Views`， `Posts`， `Follows` 和 `Likes` 當使用者是一或多個具有Adobe Analytics的社群網站成員時，就會更新 [已啟用](sites-console.md#analytics).

### 匯出 CSV {#export-csv}

選取 `Export CSV` 連結會將所有成員下載為逗號分隔值清單，適合匯入試算表中。

欄標題為

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## 建立新成員 {#create-new-member}

選取 `Create Member` 以在發佈環境中建立使用者。

![建立新成員視窗](assets/create-member1.png)

### 一般 — 成員詳細資訊 {#general-member-details}

大多數欄位是可選欄位，成員稍後可填寫其設定檔。

* **[!UICONTROL ID]**

(*必填*)可授權專案ID是成員的登入ID。
根據預設，ID會設定為所需電子郵件地址的值。
*ID建立後即不可修改*.

* **[!UICONTROL 電子郵件地址]**

(*必填*)成員的電子郵件地址。
成員在更新設定檔時可能會變更其電子郵件地址。I如果ID預設為電子郵件地址，則ID將 *非* 變更電子郵件地址時變更。

* **[!UICONTROL 密碼]**

  (*必填*)登入密碼。

* **[!UICONTROL 重新鍵入密碼]**

  (*必填*)重新輸入密碼以進行驗證。

* **[!UICONTROL 新增成員至網站]**

  (*可選*)從現有的社群網站中選取，將成員新增至社群網站的成員群組。

* **[!UICONTROL 將成員新增至群組]**

  (*可選*)從現有成員群組中選取，以將成員新增到該群組。

* 選取 **[!UICONTROL 儲存]**

### 一般 — 帳戶設定 {#general-account-settings}

在「帳戶設定」底下，社群管理員可以：

* **[!UICONTROL 狀態]**
   * 已禁止會員無法登入，導致無法檢視頁面或參與需要登入的活動。 他們仍可匿名造訪開放的社群網站。

   * 未禁止成員具有社群網站的完整存取權。

  預設為 `Not Banned`.

* **[!UICONTROL 貢獻限制]**

  如果勾選，則成員發佈內容的能力有限。
預設值視貢獻限制的設定而定。
另請參閱 [成員貢獻限制](limits.md).

* **[!UICONTROL 變更密碼]**

  修改現有成員時顯示的連結。 提供社群管理員重設成員密碼的功能。

### 一般 — 像片 {#general-photo}

若要為成員提供顯示圖片，請從選取 **[!UICONTROL 上傳影像]** 並選擇.jpg、.png、.tif或.gif型別的影像。 影像的偏好大小為240 x 240畫素，畫素為72 dpi。

### 一般 — 新增成員至網站 {#general-add-member-to-sites}

成員可以新增至一或多個社群網站的成員群組。 首先，在文字方塊中輸入文字。

### 一般 — 新增成員至群組 {#general-add-member-to-groups}

成員可以新增至一或多個成員群組。 首先，在文字方塊中輸入文字。

### 徽章索引標籤 {#badges-tab}

此 `BADGES` 面板提供手動指派徽章及撤銷徽章的功能。 徽章可能是用於指派的角色和通常獲得的徽章。

另請參閱 [評分和徽章](implementing-scoring.md).

![編輯成員資格設定視窗](assets/create-member2.png)

* **[!UICONTROL 新增徽章]**
   * 開始輸入以從中選取 [可用的徽章](badges.md). 選取徽章後，請選擇每個網站或所有網站，徽章應隨成員頭像一起顯示。
   * 可選擇多個徽章和網站。
* **[!UICONTROL 移除徽章]**
   * 選取徽章旁的垃圾桶圖示以將其移除。

## 群組主控台 {#groups-console}

「群組」主控台可從製作環境取得，可讓您建立和管理在發佈環境中註冊的成員群組。 它尤其可用於 [有特殊許可權的成員群組](users.md#privilegedmembersgroups).

若要存取「群組」主控台：
* 在全域導覽中選取 **[!UICONTROL 導覽]** > **[!UICONTROL Communities]** > **[!UICONTROL 群組]**.

>[!CAUTION]
>
>如果符合以下條件，則無法使用群組主控台： [通道服務](deploy-communities.md#tunnel-service-on-author) 未啟用。

### 建立新群組 {#create-new-group}

選取 `Add Group` 以在發佈環境中建立群組。

![建立新群組視窗](assets/group-console1.png)

建立發佈端成員群組的必填欄位包括：

* **[!UICONTROL ID]**

  (*必填*)群組唯一ID。

  *ID建立後即不可修改。*

* **[!UICONTROL 名稱]**

  (*可選*)群組的顯示名稱。

  預設值為ID。

* **[!UICONTROL 說明]**

  (*可選*)群組用途和許可權的說明。

* **[!UICONTROL 將成員新增至群組]**

  (*可選*)選取要作為群組初始成員包含的發佈端成員。

* 選取 **[!UICONTROL 儲存]**

## 授權管理員 {#authorized-administrators}

使用Communities成員控制檯中的成員時，必須以具有適當許可權的使用者身分登入，且為使用的復寫代理程式。 [通道服務](deploy-communities.md#tunnel-service-on-author) 進行正確設定。

如果未登入為 `admin`，則登入使用者必須是 `administrators` 使用者群組。

另請參閱 [作者上的復寫代理](deploy-communities.md#replication-agents-on-author).
