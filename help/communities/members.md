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
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 4%

---


# 成員和組管理控制台{#members-groups-management-consoles}

## 概覽 {#overview}

AEM Communities功能通常要求網站訪客在參與發佈環境的社群之前先註冊並登入。 其用戶註冊只需要存在於發佈環境中，通常稱為&#x200B;*members*，以便將其與在作者環境中註冊的&#x200B;*用戶*&#x200B;區分開來。

### 發佈{#members-users-on-publish}時的成員（使用者）

使用「社區成員」和「組」控制台，可以從&#x200B;*author*&#x200B;環境建立和管理在&#x200B;*publish*&#x200B;環境中註冊的成員和成員組。 只有在[tunnel服務](deploy-communities.md#tunnel-service-on-author)啟用時，才可以這樣做。

### 作者{#users-on-author}的使用者

要管理在&#x200B;*author*&#x200B;環境中註冊的用戶和組，必須使用平台的安全控制台：

* 在全局導航中，選擇&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 用戶]**。
* 在全局導航中，選擇&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 組]**。

>[!NOTE]
>
>在部署並啟用範例內容後，許多範例使用者都存在於作者和發佈環境中。 當使用[nosamplecontent runmode](../../help/sites-administering/production-ready.md)執行時，這些使用者將不存在。

## 成員控制台{#members-console}

在作者環境中，要訪問「成員」控制台以管理在發佈環境中註冊的成員：

* 在全局導航中，選擇&#x200B;**[!UICONTROL Navigation]** > **[!UICONTROL Communities]** > **[!UICONTROL Members]**

>[!CAUTION]
>
>如果未啟用[tunnel服務](deploy-communities.md#tunnel-service-on-author)，則無法使用成員控制台。

![member-console1](assets/member-console1.png)

### 搜尋 {#search-features}

選取`Members`標題左側的側面板圖示，以切換開啟搜尋側面板。

![](assets/leftpanel-icon.png)


![member-console2](assets/member-console2.png)

選擇`Members`標題左側的搜尋圖示，以切換已關閉的搜尋側面板。

### 成員統計資訊{#member-statistics}

當用戶是一個或多個社區站點的成員且啟用了Adobe Analytics[的](sites-console.md#analytics)時，更新顯示`Views`、`Posts`、`Follows`和`Likes`的列。

### 匯出 CSV {#export-csv}

選擇`Export CSV`連結會將所有成員下載為逗號分隔值的清單，以便匯入試算表。

欄標題為

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## 建立新成員 {#create-new-member}

選擇`Create Member`以在發佈環境中建立用戶。

![create-member1](assets/create-member1.png)

### 常規——成員詳細資訊{#general-member-details}

大部分欄位都是成員日後可填寫其描述檔的選填欄位。

* **[!UICONTROL ID]**

（*必要*）可授權的ID是成員的登入ID。
依預設，ID會設為所需電子郵件地址的值。
*建立後，ID便無法修改*。

* **[!UICONTROL 電子郵件地址]**

（*必填*）成員的電子郵件地址。
成員在更新其個人檔案時可能會變更其電子郵件地址。I
如果ID預設為電子郵件地址，當變更電子郵件地址時，ID將*not*&#x200B;變更。

* **[!UICONTROL 密碼]**

   （*必要*）登入密碼。

* **[!UICONTROL 重新鍵入密碼]**

   (*Required*)重新輸入密碼進行驗證。

* **[!UICONTROL 新增成員至網站]**

   （*可選*）從現有社區站點中選擇成員，以便將成員添加到社區站點的成員組。

* **[!UICONTROL 將成員新增至群組]**

   （*可選*）從現有成員組中選擇以將成員添加到該組。

* 選擇&#x200B;**[!UICONTROL 保存]**

### GENERAL —— 帳戶設定{#general-account-settings}

在「Account settings（帳戶設定）」下，社區管理員可以：

* **[!UICONTROL 狀態]**
   * 已禁止
會員無法登入，因此無法檢視頁面或參與需要登入的活動。 他們仍可以匿名造訪開放社群網站。

   * 未禁止
會員可以完全存取社群網站。

   預設值為`Not Banned`。

* **[!UICONTROL 貢獻限制]**

   如果勾選，會員張貼內容的能力將受到限制。
預設值取決於貢獻限制的設定。
請參閱[成員貢獻限制](limits.md)。

* **[!UICONTROL 變更密碼]**

   修改現有成員時存在的連結。 提供社區管理員重設成員密碼的能力。

### 一般——照片{#general-photo}

若要為成員提供頭像，請先選擇&#x200B;**[!UICONTROL 「上傳影像]**」，然後選擇。jpg、.png、.tif或。gif類型的影像。 影像的偏好大小為240 x 240像素，72 dpi。

### 常規——將成員添加到站點{#general-add-member-to-sites}

該成員可以添加到一個或多個社區站點的成員組。 首先，在文字方塊中輸入文字。

### 常規——將成員添加到組{#general-add-member-to-groups}

成員可以添加到一個或多個成員組。 首先，在文字方塊中輸入文字。

### 標章標籤{#badges-tab}

`BADGES`面板提供手動指派徽章和廢止徽章的功能。 標章可用於指派的角色以及通常應得的標章。

另請參閱[計分和標章](implementing-scoring.md)。

![create-member2](assets/create-member2.png)

* **[!UICONTROL 新增標章]**
   * 開始鍵入以從[可用標章](badges.md)中選擇。 選取徽章後，請選擇每個網站或所有網站，此徽章應與成員的頭像一起顯示在這些網站上。
   * 可以選擇多個標章和網站。
* **[!UICONTROL 移除標章]**
   * 選取徽章旁的垃圾桶圖示以移除它。

## 組控制台{#groups-console}

「群組」控制台可從作者環境使用，允許建立和管理在發佈環境中註冊的成員組。 它對於：
* [特權成員組](users.md#privilegedmembersgroups)
* 基於組分配[啟用資源](resources.md)

要訪問組控制台：
* 在全局導航中，選擇&#x200B;**[!UICONTROL Navigation]** > **[!UICONTROL Communities]** > **[!UICONTROL Groups]**。

>[!CAUTION]
>
>如果未啟用[tunnel service](deploy-communities.md#tunnel-service-on-author)，則無法使用組控制台。

### 建立新群組 {#create-new-group}

選擇`Add Group`以在發佈環境中建立組。

![group-console1](assets/group-console1.png)

建立新發佈端成員組的必填欄位包括：

* **[!UICONTROL ID]**

   （*必要*）群組唯一ID。

   *建立後，ID就無法修改。*

* **[!UICONTROL 名稱]**

   （*可選*）群組的顯示名稱。

   預設值為ID。

* **[!UICONTROL 說明]**

   （*可選*）群組用途和權限的說明。

* **[!UICONTROL 將成員新增至群組]**

   （*可選*）選擇要作為組初始成員包括的發佈端成員。

* 選擇&#x200B;**[!UICONTROL 保存]**

## 授權管理員{#authorized-administrators}

在Communities成員控制台中使用成員時，必須以具有適當權限的用戶身份登錄，[tunnel服務](deploy-communities.md#tunnel-service-on-author)使用的複製代理才能正確配置。

如果未以`admin`的身分登入，則登入的使用者必須是`administrators`使用者群組的成員。

另請參見[Replication Agents on Author](deploy-communities.md#replication-agents-on-author)。
