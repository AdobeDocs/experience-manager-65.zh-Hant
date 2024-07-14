---
title: 製作巢狀群組
description: 瞭解如何為Adobe Experience Manager Communities網站建立巢狀群組。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 1%

---

# 製作巢狀群組{#authoring-nested-groups}

## 建立作者群組 {#creating-groups-on-author}

在AEM Author例項上，從全域導覽：

* 選取&#x200B;**[!UICONTROL 社群]** > **[!UICONTROL 網站]**。
* 選取&#x200B;**[!UICONTROL 參與資料夾]**&#x200B;以開啟。
* 選取&#x200B;**[!UICONTROL 入門教學課程]**&#x200B;英文網站的卡片。

   * 選取卡片影像。
   * 請&#x200B;*不*&#x200B;選取圖示。

結果是到達[群組主控台](/help/communities/groups.md)：

![建立群組](assets/create-group.png)

群組功能會顯示為資料夾，在其中建立群組的例項。 若要開啟，請選取「群組」資料夾。 在Publish上建立的群組是可見的。

![create-new-group](assets/create-new-group.png)

## 建立主要藝術群組 {#create-main-arts-group}

可建立此群組，因為用於參與的網站結構包含群組的功能。 網站`Reference Template`中函式的設定預設為允許選取任何已啟用的群組範本。 因此，為此新群組選擇的範本為`Reference Group`。

這些主控台與社群網站主控台類似。

* 選取&#x200B;**[!UICONTROL 建立群組]**

* **社群群組範本**：

   * **[!UICONTROL 社群群組標題]**：藝術
   * **[!UICONTROL 社群群組說明]**：各個Arts群組的父群組
   * **[!UICONTROL 社群群組根]**： *保留為預設值*
   * **[!UICONTROL 其他可用的社群群組語言]**：使用下拉式功能表選取可用的社群群組語言。 功能表會顯示建立上層社群網站的所有語言。 使用者可以選取這些語言之一，以在此單一步驟中建立多個地區設定的群組。 相同的群組會在個別社群網站的「群組」主控台中，以多種指定語言建立。
   * **[!UICONTROL 社群群組名稱]**： arts
   * **[!UICONTROL 範本]**：下拉式選單以選取`Reference Group`
   * 選取&#x200B;**[!UICONTROL 下一步]**

![巢狀社群群組](assets/parent-to-nestedgroup.png)

使用這些設定繼續瀏覽其他面板：

* **[!UICONTROL Design]**

   * 變更設計或允許預設父網站的設計。
   * 選取&#x200B;**[!UICONTROL 「下一步」]**。

* **[!UICONTROL 設定]**

   * **[!UICONTROL 稽核]**

      * 留空（繼承自父網站）。

   * **[!UICONTROL 成員資格]**

      * 使用預設`Optional Membership.`

      * **[!UICONTROL 縮圖]**
         * `optional.*`

      * **[!UICONTROL 選取[下一步]]**。

* 選取「**[!UICONTROL 建立]**」。

### Arts Group中的巢狀群組 {#nesting-groups-within-arts-group}

`groups`資料夾現在包含兩個群組（重新整理頁面）。

![巢狀化群組](assets/create-community-group.png)

#### Publish群組 {#publish-group}

建立巢狀於`arts`群組中的群組之前，請將滑鼠游標停留在`arts`卡片上，並選取要發佈的圖示。

![publish-site](assets/publish-site.png)

等候確認群組已發佈。

![群組已發佈](assets/group-published.png)

`arts`群組也應包含`groups`資料夾，但此資料夾是空的，且可在其中建立新群組。 導覽至藝術群組資料夾，並建立三個巢狀群組，每個群組都有不同的成員資格設定：

1. **[!UICONTROL 視覺]**

   * 標題： `Visual Arts`
   * 名稱：`visual`
   * 範本： `Reference Group`
   * 成員資格：選取公開群組`Optional Membership`，開放給所有成員使用。

1. **[!UICONTROL 聽覺]**

   * 標題： `Auditory Arts`
   * 名稱：`auditory`
   * 範本： `Reference Group`
   * 成員資格：選取開放群組`Required Membership`，可供成員加入。

1. **[!UICONTROL 歷程記錄]**

   * 標題： `Art History`
   * 名稱：`history`
   * 範本： `Reference Group`
   * 成員資格：選取機密群組`Restricted Membership`，只對受邀成員可見。 例如，邀請[示範使用者](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`。

重新整理頁面，以便檢視所有三個巢狀群組（子社群）。

若要從「社群網站」主控台導覽至巢狀群組：

* 選取&#x200B;**[!UICONTROL 參與資料夾]**
* 選取&#x200B;**[!UICONTROL 入門教學課程卡]**
* 選取&#x200B;**[!UICONTROL 群組]**&#x200B;資料夾
* 選取&#x200B;**[!UICONTROL 藝術卡]**
* 選取&#x200B;**[!UICONTROL 群組]**&#x200B;資料夾

![create-new-group2](assets/create-new-group2.png)

## 發佈群組 {#publishing-groups}

![publish-site](assets/publish-site.png)

發佈主要社群網站後：

* Publish會個別顯示每個群組：

   * 正在等候確認群組已發佈。

* 在發佈巢狀內嵌的任何群組之前，先對父群組Publish：

   * 所有群組必須以由上而下方式發佈。

![群組已發佈](assets/group-published.png)

## Publish上的體驗 {#experience-on-publish}

登入時可以體驗不同的群組，例如，將[示範使用者](/help/communities/tutorials.md#demo-users)用於：

* 藝術/歷程記錄群組成員： `emily.andrews@mailinator.com/password`
   * 受限制的（秘密）群組（藝術/歷史）是可見的：
   * 能夠檢視選用的（公用）群組。
   * 能夠加入受限制的（開放的）群組。

* 群組管理員： `aaron.mcdonald@mailinator.com/password`

   * 能夠檢視選用的（公用）群組。
   * 能夠加入受限制的（開放的）群組。
   * 無法檢視受限制的（機密）群組。

存取作者上的Communities [成員與群組主控台](/help/communities/members.md)，以將其他使用者新增至與社群群組相對應的各種成員群組。
