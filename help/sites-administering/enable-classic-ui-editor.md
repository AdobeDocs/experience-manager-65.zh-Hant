---
title: 編輯者
seo-title: Editor
description: 瞭解如何切換回經典UI編輯器。
seo-description: Learn how to switch back to the Classic UI Editor.
uuid: ca8b07e7-014f-428e-82bd-87f3aae12f6e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 54903f3a-1e7e-4083-a2c9-b2ea4555d7fc
docset: aem65
exl-id: 8540e1f0-22d7-4f48-85d9-7c44eb7185df
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 6%

---

# 編輯者{#editor}

預設情況下，已禁用從編輯器切換到經典UI的功能。

重新啟用選項 **在傳統用戶介面中開啟** 的 **頁面資訊** 菜單中的命令。

1. 使用CRXDE Lite，查找以下節點：

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   例如

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. 使用 **覆蓋節點** 選項；例如：

   * **路徑**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **重疊位置**: `/apps/`
   * **匹配節點類型**:活動（選中複選框）

1. 將以下多值文本屬性添加到重疊節點：

   `sling:hideProperties = ["granite:hidden"]`

1. 的 **在傳統用戶介面中開啟** 中 **頁面資訊** 按鈕。

   ![](assets/syui-03-2019-02-27-15-19-48.png)
