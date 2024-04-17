---
title: Admin Console
description: 瞭解如何使用Adobe Experience Manager中可用的Admin Console。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: d4de517e-50bc-4ca5-89b1-295d259fd5bb
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# Admin Console{#admin-consoles}

依預設，透過Admin Console切換至傳統UI的功能會停用。 因此，將滑鼠懸停在特定主控台圖示上時看到的快顯視窗圖示將不再顯示，這些圖示可讓您存取傳統UI。

每個在中有Classic UI版本的主控台 `/libs/cq/core/content/nav` 可個別重新啟用，以便 **傳統UI** 當選項滑過時，控制檯圖示上方會再次彈出該選項。

在此範例中，您正在為Sites主控台重新啟用Classic UI 。

1. 使用CRXDE Lite，尋找與您要為其重新啟用傳統UI的Admin Console對應的節點。 這些檔案位於下列位置：

   `/libs/cq/core/content/nav`

   例如

   [`https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](https://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. 選取與您要為其重新啟用傳統UI的主控台對應的節點。 在此範例中，您將會為Sites主控台重新啟用傳統UI。

   `/libs/cq/core/content/nav/sites`

1. 使用建立覆蓋 **覆蓋節點** 選項；例如：

   * **路徑**： `/apps/cq/core/content/nav/sites`
   * **覆蓋位置**： `/apps/`
   * **符合節點型別**：作用中（選取核取方塊）

1. 將下列布林屬性新增至覆蓋的節點：

   `enableDesktopOnly = {Boolean}true`

1. 此 **傳統UI** 選項在Admin Console中再次作為彈出視窗選項提供。

   ![傳統UI彈出式選項](assets/syui-01-2019-02-27-15-16-55.png)

針對您想要重新啟用Classic UI版本存取權的每個主控台，重複這些步驟。
