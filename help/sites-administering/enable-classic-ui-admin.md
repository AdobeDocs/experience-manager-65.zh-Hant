---
title: Admin Console
seo-title: Admin Consoles
description: 瞭解如何使用中的可用Admin ConsoleAEM。
seo-description: Lear how to use the Admin Consoles available in AEM.
uuid: 82ab5267-2f2a-4772-85d5-678d883a0294
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6dbe82c2-7a25-49ab-a980-3635f0344817
docset: aem65
exl-id: d4de517e-50bc-4ca5-89b1-295d259fd5bb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 1%

---

# Admin Console{#admin-consoles}

預設情況下，已禁用通過管理控制台切換到經典UI的功能。 因此，在滑鼠懸停於某些控制台表徵圖上時看到的彈出表徵圖（允許訪問經典UI）不再顯示。

在中具有Classic UI版本的每個控制台 `/libs/cq/core/content/nav` 可以單獨重新啟用，以便 **經典UI** 選項在滑鼠移到控制台表徵圖上時再次彈出。

在本示例中，我們正在為站點控制台重新啟用Classic UI。

1. 使用CRXDE Lite，查找與要為其重新啟用Classic UI的管理控制台對應的節點。 它們位於：

   `/libs/cq/core/content/nav`

   例如

   [ `https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. 選擇與要為其重新啟用Classic UI的控制台對應的節點。 例如，我們將為站點控制台重新啟用經典UI。

   `/libs/cq/core/content/nav/sites`

1. 使用 **覆蓋節點** 選項；例如：

   * **路徑**: `/apps/cq/core/content/nav/sites`
   * **重疊位置**: `/apps/`
   * **匹配節點類型**:活動（選中複選框）

1. 將以下布爾屬性添加到重疊節點：

   `enableDesktopOnly = {Boolean}true`

1. 的 **經典UI** 選項在管理控制台中再次作為跨距選項可用。

   ![](assets/syui-01-2019-02-27-15-16-55.png)

對要重新啟用對經典UI版本的訪問的每個控制台重複這些步驟。
