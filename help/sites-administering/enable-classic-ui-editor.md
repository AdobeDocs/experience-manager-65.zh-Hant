---
title: 編輯器
description: 瞭解如何切換回傳統UI編輯器。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: 8540e1f0-22d7-4f48-85d9-7c44eb7185df
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 5ef752af-d616-5b23-8312-06964e46b208
    internal-label: Administering
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 3%
---

# 編輯器{#editor}

依預設，從編輯器切換到傳統UI的功能已停用。

若要在&#x200B;**頁面資訊**&#x200B;功能表中重新啟用&#x200B;**在傳統UI中開啟**&#x200B;選項，請遵循下列步驟。

1. 使用CRXDE Lite尋找下列節點：

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   例如

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. 使用&#x200B;**覆蓋節點**&#x200B;選項建立覆蓋；例如：

   * **路徑**： `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **覆蓋位置**： `/apps/`
   * **符合節點型別**：作用中（選取核取方塊）

1. 將下列多值文字屬性新增至覆蓋的節點：

   `sling:hideProperties = ["granite:hidden"]`

1. 編輯頁面時，**頁面資訊**&#x200B;功能表中再次提供&#x200B;**在傳統UI中開啟**&#x200B;選項。

   從頁面資訊![在傳統UI中開啟選項](assets/syui-03-2019-02-27-15-19-48.png)
