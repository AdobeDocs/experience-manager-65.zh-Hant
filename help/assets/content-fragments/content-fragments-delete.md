---
title: 內容片段 - 刪除考量事項
description: 在AEM中定義內容片段刪除原則前，請先檢閱這些重要考量事項。 內容片段是傳遞無頭內容的強大工具，刪除這些片段的含意必須謹慎考量。
feature: Content Fragments
role: User
exl-id: 6212457e-a171-4c33-8d19-54c26516e981
source-git-commit: de38dbb9d0ce523543c11e665c02034f4b38f1e6
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 9%

---

# 內容片段 - 刪除考量事項 {#content-fragments-delete-considerations}

在AEM中定義內容片段刪除原則前，請先檢閱這些重要考量事項。 內容片段是傳遞無頭內容的強大工具，刪除這些片段的含意必須謹慎考量。

## 權限 — 刪除或不刪除 {#permissions-delete-or-not-delete}

刪除內容的能力強大，但可能很敏感，許多行業需要限制和控制這些權限的分配方式。

關於刪除權限，內容片段必須在兩個層級考量：

1. **內容片段為單一實體。**

   * **使用案例**:需要編輯/更新內容片段的使用者 —  **並刪除整個片段**.
   * **權限**:此 [刪除](/help/sites-administering/security.md#actions) 權限可以 [透過「使用者和/或群組管理」指派](/help/sites-administering/security.md#managing-permissions).

2. **組成內容片段的多個子實體；例如，變異、子節點。**

   內容片段編輯器的基本操作要求可以刪除這種暫時的子元素。 例如，在操縱變異時；編輯中繼資料或管理相關內容時，也會一併啟用。

   * **使用案例**:需要編輯/更新內容片段的使用者 —  **而不允許刪除整個片段**.
   * **權限**:請參閱 [僅編輯器功能所需的權限](#permissions-required-for-editor-functionality-only).

>[!NOTE]
>
>當使用者沒有任何 [刪除](/help/sites-administering/security.md#actions) 權限，內容片段編輯器會在 *只讀* 模式。

>[!NOTE]
>
>另請參閱 [如何在AEM中稽核使用者管理作業](/help/sites-administering/audit-user-management-operations.md).

## 僅編輯器功能所需的權限 {#permissions-required-for-editor-functionality-only}

對於需要編輯/更新內容片段而不允許他們刪除整個片段的使用者 ****，必須指派特定權限，因為內容片段編輯器的基本操作要求可以刪除暫時的子元素。

例如，在操縱變異時；編輯中繼資料或管理相關內容時，也會一併啟用。

>[!NOTE]
>
>編輯/更新內容片段所需的刪除權限，會包含在「刪除」權限中 [透過「使用者和/或群組管理」指派](/help/sites-administering/security.md#managing-permissions).

編輯/更新片段所需的權限需要套用至包含內容片段的節點或適當的父節點（位於「 」下的任何層級） `/content/dam`)。 當指派給此父節點時，權限會套用至該分支內的所有節點。

例如，會保留所有內容片段的資料夾，例如：

* `/content/dam/contentfragments`

>[!CAUTION]
>
>在 `/content/dam` 也是可能的，因為所有內容片段都儲存在此處。
>
>但此動作會將相同的刪除權限套用至 *all* 其他資產類型。

允許特定使用者和/或群組編輯/更新內容片段的權限先決條件為：

>[!NOTE]
>
>此清單顯示所需的所有權限，而不只是刪除權限。

* 對於內容片段節點或資料夾：

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* 若 `jcr:content`所有內容片段的節點：

   * `jcr:addChildNodes`, `jcr:modifyProperties` 和 `jcr:removeChildNodes`

* 適用於以下所有節點 `jcr:content` 所有內容片段的：

   * `jcr:addChildNodes`, `jcr:modifyProperties` 和 `jcr:removeChildNodes`, `jcr:removeNode`

這些 `remove` 權限 [在CRXDE Lite內使用存取控制清單進行管理](/help/sites-administering/user-group-ac-admin.md#access-right-management).

此 `add` 和 `modify` 也可以使用CRXDE Lite管理權限，或使用「使用者管理」主控台管理權限。

例如， `remove` 組的權限 `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)
