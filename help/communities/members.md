---
title: 成員和組管理控制台
seo-title: Members & Groups Management Consoles
description: 如何訪問成員和組管理控制台
seo-description: How to access Members and Groups Management consoles
uuid: 2e93e861-a066-4189-91db-f8b784bc5aea
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ccabf301-b417-48aa-8501-8360fd9f3e36
role: Admin
exl-id: b64e24d2-8407-484c-8216-8d328ef5fa4f
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 4%

---

# 成員和組管理控制台 {#members-groups-management-consoles}

## 概觀 {#overview}

AEM Communities功能通常要求網站訪問者在參與發佈環境中的社區之前必須進行註冊和登錄。 其用戶註冊只需存在於發佈環境中，通常稱為 *成員* 將它們與 *用戶* 在作者環境中註冊。

### 發佈上的成員（用戶） {#members-users-on-publish}

使用在中註冊的「社區成員」和「組」控制台、成員和成員組 *發佈* 環境可從中建立和管理 *作者* 環境。 僅當 [隧道服務](deploy-communities.md#tunnel-service-on-author) 的子菜單。

### 作者用戶 {#users-on-author}

用於管理在中註冊的用戶和組 *作者* 環境，是使用平台安全控制台的必要條件：

* 從全局導航中，選擇 **[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 用戶]**。
* 從全局導航中，選擇 **[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 組]**。

>[!NOTE]
>
>在部署和啟用示例內容後，許多示例用戶都存在於作者和發佈環境中。 這些用戶在與 [nosamplecont運行模式](../../help/sites-administering/production-ready.md)。

## 成員控制台 {#members-console}

在作者環境中，要訪問「成員」控制台以管理在發佈環境中註冊的成員：

* 從全局導航中，選擇 **[!UICONTROL 導航]** > **[!UICONTROL 社區]** > **[!UICONTROL 成員]**

>[!CAUTION]
>
>如果 [隧道服務](deploy-communities.md#tunnel-service-on-author) 未啟用。

![member-console1](assets/member-console1.png)

### 搜尋 {#search-features}

選擇左側的側面板表徵圖 `Members` 頁眉，以切換開啟搜索側面板。

![](assets/leftpanel-icon.png)


![member-console2](assets/member-console2.png)

選擇位於 `Members` 按鈕，切換關閉的搜索側面板。

### 成員統計資訊 {#member-statistics}

顯示的列 `Views`。 `Posts`。 `Follows` 和 `Likes` 當用戶是一個或多個社區站點的成員且與Adobe Analytics [啟用](sites-console.md#analytics)。

### 匯出 CSV {#export-csv}

選擇 `Export CSV` 連結導致將所有成員下載為逗號分隔值清單，適合導入到電子錶格中。

列標題為

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## 建立新成員 {#create-new-member}

選擇 `Create Member` 以便在發佈環境中建立用戶。

![create-member1](assets/create-member1.png)

### 常規 — 成員詳細資訊 {#general-member-details}

大多數欄位是成員以後可以在其配置檔案中填寫的可選欄位。

* **[!UICONTROL ID]**

(*必需*)可授權ID是成員的登錄ID。
預設情況下，ID設定為所需電子郵件地址的值。
*建立後，ID不能修改*。

* **[!UICONTROL 電子郵件地址]**

(*必需*)成員的電子郵件地址。
成員在更新其配置檔案時可能更改其電子郵件地址。I如果ID預設為電子郵件地址，則ID將 *不* 更改電子郵件地址時更改。

* **[!UICONTROL 密碼]**

   (*必需*)登錄密碼。

* **[!UICONTROL 重新鍵入密碼]**

   (*必需*)重新輸入密碼以進行驗證。

* **[!UICONTROL 新增成員至網站]**

   (*可選*)從現有社區站點中選擇以將成員添加到社區站點的成員組。

* **[!UICONTROL 將成員新增至群組]**

   (*可選*)從現有成員組中選擇以將成員添加到該組。

* 選擇 **[!UICONTROL 保存]**

### 常規 — 帳戶設定 {#general-account-settings}

在「帳戶」設定下，社區管理員可以：

* **[!UICONTROL 狀態]**
   * 禁止成員無法登錄，無法查看頁面或參與需要登錄的活動。 他們可能仍會匿名訪問一個開放的社區網站。

   * 未禁止成員有權完全訪問社區站點。

   預設值為 `Not Banned`。

* **[!UICONTROL 貢獻限制]**

   如果選中，則成員發佈內容的能力將受到限制。
預設值取決於貢獻限制的配置。
請參閱 [成員繳費限制](limits.md)。

* **[!UICONTROL 變更密碼]**

   修改現有成員時存在的連結。 提供社區管理員重置成員密碼的功能。

### 常規 — 照片 {#general-photo}

要為成員提供虛擬形象，請從選擇 **[!UICONTROL 上載映像]** 並選擇.jpg、.png、.tif或.gif類型的影像。 影像的首選大小為240 x 240像素，72 dpi。

### 常規 — 將成員添加到站點 {#general-add-member-to-sites}

成員可以添加到一個或多個社區站點的成員組。 首先在文本框中輸入文本。

### 常規 — 將成員添加到組 {#general-add-member-to-groups}

成員可以添加到一個或多個成員組。 首先在文本框中輸入文本。

### 「徽章」頁籤 {#badges-tab}

的 `BADGES` 面板提供了手動分配徽章和撤消徽章的功能。 這些徽章可用於指定的角色以及通常獲得的徽章。

另請參閱 [評分和徽章](implementing-scoring.md)。

![create-member2](assets/create-member2.png)

* **[!UICONTROL 添加徽章]**
   * 開始鍵入以從中選擇 [可用徽章](badges.md)。 選擇徽章後，選擇每個站點或所有站點，徽章應隨成員的虛擬形象一起顯示在這些站點上。
   * 可以選擇多個徽章和站點。
* **[!UICONTROL 刪除徽章]**
   * 選擇徽章旁邊的垃圾桶表徵圖將其刪除。

## 組控制台 {#groups-console}

「組」(Groups)控制台可從作者環境獲得，用於建立和管理在發佈環境中註冊的成員組。 對於 [特權成員組](users.md#privilegedmembersgroups)。

要訪問組控制台：
* 從全局導航中，選擇 **[!UICONTROL 導航]** > **[!UICONTROL 社區]** > **[!UICONTROL 組]**。

>[!CAUTION]
>
>如果 [隧道服務](deploy-communities.md#tunnel-service-on-author) 未啟用。

### 建立新群組 {#create-new-group}

選擇 `Add Group` 以便在發佈環境中建立組。

![group-console1](assets/group-console1.png)

建立新發佈端成員組的必填欄位為：

* **[!UICONTROL ID]**

   (*必需*)組唯一ID。

   *建立後，ID不能修改。*

* **[!UICONTROL 名稱]**

   (*可選*)組的顯示名稱。

   預設值為ID。

* **[!UICONTROL 說明]**

   (*可選*)組目的和權限的說明。

* **[!UICONTROL 將成員新增至群組]**

   (*可選*)選擇要作為組初始成員包括的發佈端成員。

* 選擇 **[!UICONTROL 保存]**

## 授權管理員 {#authorized-administrators}

在社區成員控制台中使用成員時，必須以具有適當權限的用戶身份登錄，以及由 [隧道服務](deploy-communities.md#tunnel-service-on-author) 才能正確配置。

如果未登錄為 `admin`，則登錄用戶必須是 `administrators` 用戶組。

另請參閱 [作者上的複製代理](deploy-communities.md#replication-agents-on-author)。
