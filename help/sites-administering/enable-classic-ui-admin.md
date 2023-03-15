---
title: Admin Console
seo-title: Admin Consoles
description: 了解如何使用AEM中可用的Admin Console。
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

依預設，已停用透過管理控制台切換至傳統UI的功能。 因此，將滑鼠游標移至特定控制台圖示上時會顯示的快顯圖示（可存取傳統UI）將不再顯示。

每個主控台的 `/libs/cq/core/content/nav` 可個別重新啟用，以便 **傳統UI** 將滑鼠移到控制台圖示上時，選項會再次彈出。

在此範例中，我們將重新啟用Sites主控台的傳統UI。

1. 使用CRXDE Lite，尋找與要重新啟用傳統UI之Admin Console相對應的節點。 可在下方找到：

   `/libs/cq/core/content/nav`

   例如

   [ `https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. 選取與要重新啟用傳統UI之主控台相對應的節點。 例如，我們將重新啟用Sites主控台的傳統UI。

   `/libs/cq/core/content/nav/sites`

1. 使用 **覆蓋節點** 選項；例如：

   * **路徑**: `/apps/cq/core/content/nav/sites`
   * **重疊位置**: `/apps/`
   * **匹配節點類型**:活動（選取核取方塊）

1. 將下列布林屬性新增至覆蓋節點：

   `enableDesktopOnly = {Boolean}true`

1. 此 **傳統UI** 「管理控制台」中的彈出視窗選項可再次使用「 」選項。

   ![](assets/syui-01-2019-02-27-15-16-55.png)

對您要重新啟用傳統UI版本存取權的每個主控台重複這些步驟。
