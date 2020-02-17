---
title: 編輯者
seo-title: 編輯者
description: 瞭解如何切換回Classic UI Editor。
seo-description: 瞭解如何切換回Classic UI Editor。
uuid: ca8b07e7-014f-428e-82bd-87f3aae12f6e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 54903f3a-1e7e-4083-a2c9-b2ea4555d7fc
docset: aem65
translation-type: tm+mt
source-git-commit: 954c1d5b06b54d59f523483ce5c1af36c2083a76

---


# 編輯者{#editor}

依預設，從編輯器切換至傳統UI的功能已停用。

若要重新啟用「頁面資訊」功 **能表中的「在Classic UI****中開啟」選項** ，請依照下列步驟進行。

1. 使用CRXDE Lite，查找以下節點：

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   例如

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. 使用「覆蓋節點」選 **項建立覆蓋** ;例如：

   * **路徑**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **重疊位置**: `/apps/`
   * **匹配節點類型**:活動（選擇複選框）

1. 將下列多值文字屬性新增至覆蓋節點：

   `sling:hideProperties = ["granite:hidden"]`

1. 編輯 **頁面時，「頁面資訊」選單中會再** 次提供「在傳統UI中開啟 **** 」選項。

   ![](assets/syui-03-2019-02-27-15-19-48.png)