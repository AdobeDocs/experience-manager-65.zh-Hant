---
title: 使用社交圖
description: 瞭解如何將以下元件新增到頁面，以讓登入社群成員關注活動或受到關注。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 2cd1436b-3727-4757-b28e-70756be78a4e
solution: Experience Manager
feature: Communities
role: Admin
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
source-wordcount: '199'
ht-degree: 1%
---
# 使用社交圖 {#using-social-graph}

## 簡介 {#introduction}

社群成員追蹤[活動](activities.md)及被追蹤的能力透過兩個元件建立： `Follow`及`Following`。

`Follow`元件必須與另一個資源關聯，而且已為社群成員和功能建立此關聯。

`Following`元件只會列出目前成員之後的成員，或目前成員之後的成員。 此成員間關係的社交圖表包含在為[社群網站](overview.md#communitiessites)建立的使用者設定檔中。

## 新增關注專案至頁面 {#adding-following-to-a-page}

如果想要將`Following`元件新增至作者模式的頁面，請找到元件`Communities / Following`並將其拖曳至應顯示社交圖表的頁面上。

如需必要資訊，請造訪[社群元件基本知識](basics.md)。

納入[必要的使用者端資料庫](essentials-socialgraph.md#essentials-for-client-side)時，`Following`元件的顯示方式如下：

![正在關注](assets/following.png)

## 設定下列專案 {#configuring-following}

目前，必須設定屬性以判斷元件是否顯示`follows`關聯性或`following`關聯性。

## 其他資訊 {#additional-information}

如需開發人員的[社交圖基本資訊](essentials-socialgraph.md)頁面上的詳細資訊。
