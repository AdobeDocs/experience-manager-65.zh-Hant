---
title: 編寫巢狀群組
seo-title: Authoring Nested Groups
description: 建立巢狀群組
seo-description: Create nested groups
uuid: b377dc1b-bbb6-41c9-b0fc-8281e1410685
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 752235d2-21ac-46d2-82ed-5fec09c645e9
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
source-git-commit: 1074843a0105df39382b64defe66fc262986b9c9
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 3%

---

# 編寫巢狀群組{#authoring-nested-groups}

## 在作者上建立群組 {#creating-groups-on-author}

在AEM製作例項中，從全域導覽：

* 選擇 **[!UICONTROL 社群]** > **[!UICONTROL 網站]**.
* 選擇 **[!UICONTROL 參與資料夾]** 來開啟它。
* 選取 **[!UICONTROL 快速入門教學課程]** 英文網站。

   * 選取卡片影像。
   * 做 *not* 選取圖示。

結果會是到達 [群組主控台](/help/communities/groups.md):

![建立群組](assets/create-group.png)

群組函式會顯示為資料夾，其中會建立群組的例項。 選擇「組」資料夾以開啟它。 在發佈時建立的群組可見。

![建立 — 新建組](assets/create-new-group.png)

## 建立主要藝術群組 {#create-main-arts-group}

可以建立此組，因為參與的站點結構包括組功能。 網站的 `Reference Template` 預設值為允許選擇任何已啟用的組模板。 因此，為此新群組選擇的範本為 `Reference Group`.

這些主控台類似於Communities Sites主控台。

* 選擇 **[!UICONTROL 建立群組]**

* **社群群組範本**:

   * **[!UICONTROL 社群群組標題]**:藝術
   * **[!UICONTROL 社群群組說明]**:不同藝術團體的父團體
   * **[!UICONTROL 社群群組根]**: *保留為預設值*
   * **[!UICONTROL 其他可用的社群群組語言]**:使用下拉式功能表來選取可用的社群群組語言。 功能表會顯示建立父社群網站的所有語言。 使用者可在這些語言中選取，以在這個單一步驟中建立多個地區設定中的群組。 系統會在個別社群網站的群組控制台中，以多種指定語言建立相同的群組。
   * **[!UICONTROL 社區組名]**:藝術
   * **[!UICONTROL 範本]**:下拉式清單選取 `Reference Group`
   * 選擇 **[!UICONTROL 下一個]**

![巢狀社群群組](assets/parent-to-nestedgroup.png)

繼續使用下列設定瀏覽其他面板：

* **[!UICONTROL Design]**

   * 更改設計或允許預設父站點的設計。
   * 選擇 **[!UICONTROL 下一個]**.

* **[!UICONTROL 設定]**

   * **[!UICONTROL 審核]**

      * 保留為空（繼承自父站點）。
   * **[!UICONTROL 成員資格]**

      * 使用預設值 `Optional Membership.`

      * **[!UICONTROL 縮圖]**
         * `optional.*`
      * **[!UICONTROL 選擇下一步]**.



* 選擇 **[!UICONTROL 建立]**。

### 藝術組中的嵌套組 {#nesting-groups-within-arts-group}

此 `groups` 資料夾現在包含兩個群組（重新整理頁面）。

![嵌套組](assets/create-community-group.png)

#### 發佈群組 {#publish-group}

在內建立巢狀群組之前 `arts` 群組，暫留在 `arts` 卡片並選取「發佈」圖示以發佈。

![發佈網站](assets/publish-site.png)

等待群組已發佈的確認。

![群組已發佈](assets/group-published.png)

此 `arts` 群組也應包含 `groups` ，但空白且可建立新群組的資料夾。 導覽至藝術群組資料夾，並建立3個巢狀群組，每個群組具有不同的成員資格設定：

1. **[!UICONTROL 視覺]**

   * 標題: `Visual Arts`
   * 名稱: `visual`
   * 範本: `Reference Group`
   * 會籍：選取 `Optional Membership`，公開給所有成員。

1. **[!UICONTROL 聽覺]**

   * 標題: `Auditory Arts`
   * 名稱: `auditory`
   * 範本: `Reference Group`
   * 會籍：選取 `Required Membership`，此為開放群組，可供成員加入。

1. **[!UICONTROL 歷史]**

   * 標題: `Art History`
   * 名稱: `history`
   * 範本: `Reference Group`
   * 會籍：選取 `Restricted Membership`，此為機密群組，僅對受邀成員可見。 例如，邀請 [示範使用者](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`.

重新整理頁面以查看所有三個巢狀群組（子社群）。

要從Communities Sites控制台導航到嵌套組，請執行以下操作：

* 選擇 **[!UICONTROL 參與資料夾]**
* 選擇 **[!UICONTROL 快速入門教學課程卡]**
* 選擇 **[!UICONTROL 群組]** 資料夾
* 選擇 **[!UICONTROL 藝術卡]**
* 選擇 **[!UICONTROL 群組]** 資料夾

![create-new-group2](assets/create-new-group2.png)

## 發佈群組 {#publishing-groups}

![發佈網站](assets/publish-site.png)

發佈主要社群網站後：

* 個別發佈每個群組：

   * 等待群組已發佈的確認。

* 發佈內嵌的任何群組之前先發佈父群組：

   * 所有群組都必須以由上而下的方式發佈。

![群組已發佈](assets/group-published.png)

## 發佈體驗 {#experience-on-publish}

登入時(例如使用 [示範使用者](/help/communities/tutorials.md#demo-users) 用於：

* 藝術/歷史組成員：emily.andrews@mailinator.com
   * 受限（秘密）組（藝術/歷史）可見：
   * 可以看到選用（公開）群組。
   * 可以加入受限制（開啟）的組。

* 群組管理員：aaron.mcdonald@mailinator.com

   * 可以看到選用（公開）群組。
   * 可以加入受限制（開啟）的組。
   * 看不到受限（秘密）組。

訪問社區 [成員和組控制台](/help/communities/members.md) 在作者上，將其他使用者新增至與社群群組相對應的各種成員群組。
