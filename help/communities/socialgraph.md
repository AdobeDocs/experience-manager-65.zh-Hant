---
title: 使用社交圖表
seo-title: 使用社交圖表
description: 將下列元件新增至頁面
seo-description: 將下列元件新增至頁面
uuid: 8be6334b-e6c9-40bc-90a8-750b98419470
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 0ce57ab1-e4c6-4c38-963d-556eef8757f2
exl-id: 2cd1436b-3727-4757-b28e-70756be78a4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---

# 使用社交圖{#using-social-graph}

## 簡介 {#introduction}

社區成員遵循[活動](activities.md)以及遵循的能力通過兩個元件建立：`Follow`和`Following`。

`Follow`元件必須與其他資源相關聯，並且此關聯已為社區成員和功能建立。

`Following`元件僅列出當前成員後面或當前成員後面的成員。 此成員間關係的社交圖表包含在為[社群網站](overview.md#communitiessites)建立的用戶配置檔案中。

## 將以下內容添加到頁{#adding-following-to-a-page}

如果想要以製作模式將`Following`元件新增至頁面，請找出元件`Communities / Following`，並將其拖曳至應該出現社交圖形的頁面上。

如需必要資訊，請造訪[Communities Components Basics](basics.md)。

包含[必要的用戶端程式庫](essentials-socialgraph.md#essentials-for-client-side)時，以下是`Following`元件的顯示方式：

![下列](assets/following.png)

## 正在配置{#configuring-following}

目前，必須設定屬性以判斷元件是顯示`follows`關係，還是顯示`following`關係。

## 其他資訊 {#additional-information}

如需詳細資訊，請參閱開發人員的[社交圖表要點](essentials-socialgraph.md)頁面。
