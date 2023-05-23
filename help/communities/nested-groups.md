---
title: 創作嵌套組
seo-title: Authoring Nested Groups
description: 建立嵌套組
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

# 創作嵌套組{#authoring-nested-groups}

## 在作者上建立組 {#creating-groups-on-author}

在AEM Author實例上，從全局導航：

* 選擇 **[!UICONTROL 社區]** > **[!UICONTROL 站點]**。
* 選擇 **[!UICONTROL eng adfole（參與資料夾）]** 開啟它。
* 為 **[!UICONTROL 入門教程]** 英文網站。

   * 選擇卡影像。
   * 做 *不* 選擇一個表徵圖。

結果是 [組控制台](/help/communities/groups.md):

![建立組](assets/create-group.png)

組函式將顯示為建立組實例的資料夾。 選擇「組」資料夾以將其開啟。 發佈時建立的組可見。

![新建組](assets/create-new-group.png)

## 建立主要藝術組 {#create-main-arts-group}

可以建立此組，因為用於參與的站點結構包含組功能。 站點中的函式的配置 `Reference Template` 預設值為允許選擇任何已啟用的組模板。 因此，為此新組選擇的模板是 `Reference Group`。

這些控制台與社區站點控制台類似。

* 選擇 **[!UICONTROL 建立組]**

* **社群群組範本**:

   * **[!UICONTROL 社區組標題]**:藝術
   * **[!UICONTROL 社區組說明]**:不同藝術組的父組
   * **[!UICONTROL 社區組根]**: *預設*
   * **[!UICONTROL 其他可用社區組語言]**:使用下拉菜單選擇可用的社區組語言。 該菜單顯示建立父社區網站的所有語言。 用戶可以在這些語言中進行選擇，以在此步驟中在多個語言環境中建立組。 在各個社區站點的「組」控制台中以多種指定語言建立同一組。
   * **[!UICONTROL 社區組名稱]**:藝術
   * **[!UICONTROL 模板]**:下拉選擇 `Reference Group`
   * 選擇 **[!UICONTROL 下一個]**

![嵌套的社區組](assets/parent-to-nestedgroup.png)

繼續使用以下設定查看其他面板：

* **[!UICONTROL Design]**

   * 更改設計或允許預設父站點的設計。
   * 選擇 **[!UICONTROL 下一個]**。

* **[!UICONTROL 設定]**

   * **[!UICONTROL 審核]**

      * 留空（從父站點繼承）。
   * **[!UICONTROL 成員資格]**

      * 使用預設值 `Optional Membership.`

      * **[!UICONTROL 縮圖]**
         * `optional.*`
      * **[!UICONTROL 選擇下一步]**。



* 選擇 **[!UICONTROL 建立]**。

### 藝術組內的嵌套組 {#nesting-groups-within-arts-group}

的 `groups` 資料夾現在包含兩個組（刷新頁面）。

![嵌套組](assets/create-community-group.png)

#### 發佈群組 {#publish-group}

在建立嵌套在 `arts` 組，懸停在 `arts` 並選擇發佈表徵圖以發佈。

![發佈站點](assets/publish-site.png)

等待確認組已發佈。

![組發佈](assets/group-published.png)

的 `arts` 組還應包含 `groups` 資料夾，但是空的，可以在其中建立新組。 導航到藝術組資料夾並建立3個嵌套組，每個組具有不同的成員資格設定：

1. **[!UICONTROL 視覺]**

   * 標題: `Visual Arts`
   * 名稱: `visual`
   * 範本: `Reference Group`
   * 成員身份：選擇 `Optional Membership`，一個公共組，對所有成員開放。

1. **[!UICONTROL 聽覺]**

   * 標題: `Auditory Arts`
   * 名稱: `auditory`
   * 範本: `Reference Group`
   * 成員身份：選擇 `Required Membership`，開啟的組，可供成員加入。

1. **[!UICONTROL 歷史]**

   * 標題: `Art History`
   * 名稱: `history`
   * 範本: `Reference Group`
   * 成員身份：選擇 `Restricted Membership`，一個秘密組，僅對受邀成員可見。 例如，invite [演示用戶](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`。

刷新頁面以查看所有三個嵌套組（子社區）。

要從「社區站點」控制台導航到嵌套組，請執行以下操作：

* 選擇 **[!UICONTROL eng adfole（參與資料夾）]**
* 選擇 **[!UICONTROL 入門教程卡]**
* 選擇 **[!UICONTROL 組]** 資料夾
* 選擇 **[!UICONTROL 藝術卡]**
* 選擇 **[!UICONTROL 組]** 資料夾

![create-new-group2](assets/create-new-group2.png)

## 發佈組 {#publishing-groups}

![發佈站點](assets/publish-site.png)

發佈主社區網站後：

* 單獨發佈每個組：

   * 正在等待確認組已發佈。

* 在發佈嵌套在以下內的任何組之前發佈父組：

   * 所有組必須以自上而下的方式發佈。

![組發佈](assets/group-published.png)

## 發佈體驗 {#experience-on-publish}

登錄時，可能會體驗到不同的組，例如與 [演示用戶](/help/communities/tutorials.md#demo-users) 用於：

* 藝術/歷史記錄組成員：emily.andrews@mailinator.com/password
   * 受限（秘密）群體藝術/歷史可見：
   * 可以查看可選（公共）組。
   * 可以加入受限（開啟）組。

* 組經理：aaron.mcdonald@mailinator.com/password

   * 可以查看可選（公共）組。
   * 可以加入受限（開啟）組。
   * 無法看到受限制（機密）組。

訪問社區 [成員和組控制台](/help/communities/members.md) 將其他用戶添加到與社區組對應的各個成員組。
