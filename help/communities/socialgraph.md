---
title: 使用社交圖表
seo-title: 使用社交圖表
description: 新增下列元件至頁面
seo-description: 新增下列元件至頁面
uuid: 8be6334b-e6c9-40bc-90a8-750b98419470
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 0ce57ab1-e4c6-4c38-963d-556eef8757f2
translation-type: tm+mt
source-git-commit: 1429a099288f038510cb0a194fb55632297ef371
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---


# 使用社交圖{#using-social-graph}

## 簡介 {#introduction}

社區成員遵循[活動](activities.md)以及遵循的能力通過兩個元件建立：`Follow`和`Following`。

`Follow`元件必須與其他資源關聯，而且此關聯已為社區成員和功能建立。

`Following`元件只列出當前成員後面或當前成員後面的成員。 該成員之間關係的社交圖表包含在為[社區站點](overview.md#communitiessites)建立的用戶配置檔案中。

## 將以下內容添加到頁面{#adding-following-to-a-page}

如果想要在作者模式下將`Following`元件新增至頁面，請找出元件`Communities / Following`，並將它拖曳至社交圖形應出現的頁面上。

如需必要資訊，請造訪[Communities Components Basics](basics.md)。

當包含[必要的用戶端程式庫](essentials-socialgraph.md#essentials-for-client-side)時，`Following`元件的顯示方式如下：

![following](assets/following.png)

## 配置{#configuring-following}

目前，必須設定屬性，以判斷元件是顯示`follows`關係，還是顯示`following`關係。

## 其他資訊 {#additional-information}

開發人員的[Social Graph Essentials](essentials-socialgraph.md)頁面中有更多資訊。
