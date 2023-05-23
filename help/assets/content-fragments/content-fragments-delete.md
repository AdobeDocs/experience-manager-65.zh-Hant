---
title: 內容片段 - 刪除考量事項
description: 在中定義內容片段刪除策略之前，請查看這些重要注意事項AEM。 內容片段是提供無頭內容的強大工具，刪除它們的含義必須仔細考慮。
feature: Content Fragments
role: User
exl-id: 6212457e-a171-4c33-8d19-54c26516e981
source-git-commit: de38dbb9d0ce523543c11e665c02034f4b38f1e6
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 9%

---

# 內容片段 - 刪除考量事項 {#content-fragments-delete-considerations}

在中定義內容片段刪除策略之前，請查看這些重要注意事項AEM。 內容片段是提供無頭內容的強大工具，刪除它們的含義必須仔細考慮。

## 權限 — 刪除或不刪除 {#permissions-delete-or-not-delete}

刪除內容的能力非常強大，但可能是敏感的，許多行業需要限制和控制這些權限的分配方式。

關於刪除權限，必須在兩個級別考慮內容片段：

1. **內容片段作為單個實體。**

   * **用例**:需要編輯/更新內容片段的用戶 —  **並刪除整個片段**。
   * **權限**:的 [刪除](/help/sites-administering/security.md#actions) 權限可以 [通過用戶和/或組管理分配](/help/sites-administering/security.md#managing-permissions)。

2. **構成內容片段的多個子實體；例如，變體，子節點。**

   內容片段編輯器的基本操作要求可以刪除此類臨時子元素。 例如，在操縱變體時；編輯元資料或管理關聯內容時。

   * **用例**:需要編輯/更新內容片段的用戶 —  **不允許刪除整個片段**。
   * **權限**:請參閱 [僅編輯器功能所需的權限](#permissions-required-for-editor-functionality-only)。

>[!NOTE]
>
>當用戶沒有 [刪除](/help/sites-administering/security.md#actions) 權限，內容片段編輯器在 *只讀* 的子菜單。

>[!NOTE]
>
>另請參閱 [如何審核用戶管理操AEM作](/help/sites-administering/audit-user-management-operations.md)。

## 僅編輯器功能所需的權限 {#permissions-required-for-editor-functionality-only}

對於需要編輯/更新內容片段而不允許他們刪除整個片段的使用者 ****，必須指派特定權限，因為內容片段編輯器的基本操作要求可以刪除暫時的子元素。

例如，在操縱變體時；編輯元資料或管理關聯內容時。

>[!NOTE]
>
>編輯/更新內容片段所需的刪除權限包含在「刪除」權限中 [通過用戶和/或組管理分配](/help/sites-administering/security.md#managing-permissions)。

編輯/更新片段所需的權限需要應用於包含內容片段的節點或相應的父節點（位於以下任何級別） `/content/dam`)。 當分配給這樣的父節點時，權限將應用於該分支中的所有節點。

例如，將保存所有內容片段的資料夾，如：

* `/content/dam/contentfragments`

>[!CAUTION]
>
>設定權限 `/content/dam` 也是可能的，因為所有內容片段都儲存在這裡。
>
>但是，此操作將相同的刪除權限應用於 *全部* 其他資產類型。

允許特定用戶和/或組編輯/更新內容片段的權限先決條件是：

>[!NOTE]
>
>此清單顯示所需的所有權限，而不僅顯示刪除權限。

* 對於「內容片段」節點或資料夾：

   * `jcr:addChildNodes`、`jcr:modifyProperties`

* 對於 `jcr:content`所有內容片段的節點：

   * `jcr:addChildNodes`, `jcr:modifyProperties` 和 `jcr:removeChildNodes`

* 適用於以下所有節點 `jcr:content` 所有內容片段：

   * `jcr:addChildNodes`。 `jcr:modifyProperties` 和 `jcr:removeChildNodes`。 `jcr:removeNode`

這些 `remove` 權限必須 [在CRXDE Lite內使用訪問控制清單進行管理](/help/sites-administering/user-group-ac-admin.md#access-right-management)。

的 `add` 和 `modify` 也可以在CRXDE Lite中或使用用戶管理控制台管理權限。

例如， `remove` 組的權限 `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)
