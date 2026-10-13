---
title: 社群主控台
description: 從全域導覽面板瞭解可在製作環境中使用的Adobe Experience Manager社群主控台。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 36f2e3d2-46c7-48a8-a1e9-213f581bd9f3
solution: Experience Manager
feature: Communities
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%
---
# 社群主控台 {#communities-consoles}

AEM Communities的主控台可在全域導覽面板的製作環境中取得，且可讓您存取管理工作，例如：

* [建立社群網站](sites-console.md)
* 正在新增[群組](groups.md)巢狀在網站內
* 管理[社群網站範本](sites.md)
* 管理[社群成員](members.md)
* [正在稽核](moderate-ugc.md)使用者產生的內容(UGC)
* 建立[自訂徽章](badges.md)
* 正在設定UGC[&#128279;](srp-config.md)的預設儲存體

當[UGC存放區](working-with-srp.md)設定為製作和發佈環境共用的公用存放區時，可在製作和發佈環境中使用的[仲裁主控台](moderation.md)會在UGC的單一執行個體上運作。

在作者環境中，以管理員許可權登入後，`Communities`主控台可從導覽和工具主控台取得。

>[!NOTE]
>
>在發佈環境中，登入成員具有適當許可權時，[社群網站](sites-console.md)會顯示`Administration`功能表專案。

## 全域導覽面板 {#global-navigation-panel}

選取左上角的`Adobe Experience Manager`圖示，以開啟全域導覽面板並存取兩個圖示：

* [導覽主控台](#navigation-console)
* [工具主控台](tools.md)

## 導覽主控台 {#navigation-console}

若要存取各種Communities主控台，請從全域導覽中選取&#x200B;**導覽， Communities**。

![社群](assets/communities.png)

* [Sites](sites-console.md)

  Sites主控台可在作者環境中存取，以建立和管理社群網站及其[群組](groups.md)。

* [審核](moderation.md)

  「協調」主控台適用於在製作環境中大量協調UGC。 在「發佈」環境中，對於一個或多個社群網站，指派角色為[社群版主](users.md#publishenvironmentusersandgroups)的社群成員，可以存取類似的批次仲裁主控台。

* [成員、群組](members.md)

  「成員」和「群組」主控台用於從作者環境管理存在於發佈環境中的社群成員和成員群組。

* [報告](reports.md)

  「報表」主控台是當社群網站啟用[Adobe Analytics](sites-console.md#analytics)時，產生工作總攬、頁面檢視和張貼內容(UGC)報表的位置。 主控台僅適用於「作者」環境。

## 工具主控台 {#tools-console}

若要存取[社群工具](tools.md) （先前為管理主控台），請從全域導覽： **[!UICONTROL 工具]** > **[!UICONTROL 社群]**
