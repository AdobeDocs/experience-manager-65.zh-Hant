---
title: 社群主控台
description: 從全域導覽面板瞭解可在製作環境中使用的Adobe Experience Manager社群主控台。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 36f2e3d2-46c7-48a8-a1e9-213f581bd9f3
source-git-commit: 0a4aca939c564720f63f055e9522e56942eaa128
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 1%

---

# 社群主控台 {#communities-consoles}

AEM Communities的主控台可在全域導覽面板的製作環境中取得，且可讓您存取管理工作，例如：

* [建立社群網站](sites-console.md)
* 新增 [群組](groups.md) 巢狀內嵌於網站
* 管理 [社群網站範本](sites.md)
* 管理 [社群成員](members.md)
* [稽核](moderate-ugc.md) 使用者產生的內容(UGC)
* 建立 [自訂徽章](badges.md)
* 設定 [UGC的預設儲存空間](srp-config.md)

時間 [UGC儲存](working-with-srp.md) 設為製作和發佈環境共用的公用存放區，因此 [稽核主控台](moderation.md)適用於製作和發佈環境，在UGC的單一例項上運作。

在作者環境中，以管理員許可權登入後， `Communities` 「導覽」和「工具」主控台提供主控台。

>[!NOTE]
>
>在發佈環境中， [社群網站](sites-console.md) 顯示 `Administration` 登入成員具有適當許可權時的功能表專案。

## 全域導覽面板 {#global-navigation-panel}

選取 `Adobe Experience Manager` 圖示來開啟「全域導覽」面板，並存取兩個圖示：

* [導覽主控台](#navigation-console)
* [工具主控台](tools.md)

## 導覽主控台 {#navigation-console}

若要存取各種Communities主控台，請從全域導覽選取 **導覽，社群**.

![社群](assets/communities.png)

* [Sites](sites-console.md)

  您可以在作者環境中存取Sites主控台，以建立及管理社群網站及其 [群組](groups.md).

* [審核](moderation.md)

  「協調」主控台適用於在製作環境中大量協調UGC。 在「發佈」環境中，指派了角色的社群成員可存取類似的大量稽核主控台。 [社群版主](users.md#publishenvironmentusersandgroups) 用於一或多個社群網站。

* [成員、群組](members.md)

  「成員」和「群組」主控台用於從作者環境管理存在於發佈環境中的社群成員和成員群組。

* [報告](reports.md)

  「報表」主控台是當社群網站具有下列條件時，產生工作總攬、頁面檢視和發佈內容(UGC)報表的位置 [已啟用Adobe Analytics](sites-console.md#analytics). 主控台僅適用於「作者」環境。

## 工具主控台 {#tools-console}

若要存取 [社群工具](tools.md) （前身為管理主控台），從全域導覽： **[!UICONTROL 工具]** > **[!UICONTROL Communities]**
