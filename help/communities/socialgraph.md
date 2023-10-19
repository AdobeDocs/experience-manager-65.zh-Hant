---
title: 使用社交圖
description: 瞭解如何將以下元件新增到頁面，以讓登入社群成員關注活動或受到關注。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 2cd1436b-3727-4757-b28e-70756be78a4e
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---

# 使用社交圖 {#using-social-graph}

## 簡介 {#introduction}

社群成員可關注的功能 [活動](activities.md) 並遵循透過兩個元件建立： `Follow` 和 `Following`.

此 `Follow` 元件必須與另一個資源相關聯，而且已為社群成員和功能建立此關聯。

此 `Following` 元件僅列出目前成員之後的成員，或目前成員之後的成員。 此成員間關係的社交圖表包含在為建立的使用者個人資料中 [社群網站](overview.md#communitiessites).

## 新增關注專案至頁面 {#adding-following-to-a-page}

如果想要新增 `Following` 元件至作者模式下的頁面，找到元件 `Communities / Following` 並將其拖曳至社交圖應出現的頁面上。

如需必要資訊，請造訪 [Communities元件基本知識](basics.md).

當 [必要的使用者端程式庫](essentials-socialgraph.md#essentials-for-client-side) 包含，這就是 `Following` 元件出現：

![關注](assets/following.png)

## 設定下列專案 {#configuring-following}

目前，必須設定屬性，才能判斷元件是否顯示 `follows` 關係，或 `following` 關係。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱 [社交圖基本資訊](essentials-socialgraph.md) 開發人員頁面。
