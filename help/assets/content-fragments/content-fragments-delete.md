---
title: 內容片段 - 刪除考量事項
description: 在AEM中定義內容片段刪除原則之前，請檢閱這些重要考量。 內容片段是傳送Headless內容的強大工具，必須仔細考慮刪除這些片段的影響。
feature: Content Fragments
role: User
exl-id: 6212457e-a171-4c33-8d19-54c26516e981
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 9%

---

# 內容片段 - 刪除考量事項 {#content-fragments-delete-considerations}

在AEM中定義內容片段刪除原則之前，請檢閱這些重要考量。 內容片段是傳送Headless內容的強大工具，必須仔細考慮刪除這些片段的影響。

## 許可權 — 刪除或不刪除 {#permissions-delete-or-not-delete}

刪除內容的功能非常強大，但可能比較敏感，許多行業都需要限制和控制這些許可權的分配方式。

關於刪除許可權，內容片段必須考量為兩個層級：

1. **內容片段為單一實體。**

   * **使用案例**：需要編輯/更新內容片段的使用者 — **並刪除整個片段**。
   * **許可權**： [Delete](/help/sites-administering/security.md#actions)許可權可以透過使用者和/或群組管理](/help/sites-administering/security.md#managing-permissions)進行[指派。

2. **構成內容片段的多個子實體；例如，變化、子節點。**

   內容片段編輯器的基本操作需要可以刪除此類暫時性子元素。 例如，操控變數時；編輯中繼資料或管理關聯內容時，也可以。

   * **使用案例**：需要編輯/更新內容片段的使用者 — **不允許刪除整個片段**。
   * **許可權**：請參閱[僅編輯器功能所需的許可權](#permissions-required-for-editor-functionality-only)。

>[!NOTE]
>
>當使用者沒有任何[刪除](/help/sites-administering/security.md#actions)許可權時，內容片段編輯器會以&#x200B;*唯讀*&#x200B;模式運作。

>[!NOTE]
>
>另請參閱[如何在AEM](/help/sites-administering/audit-user-management-operations.md)中稽核使用者管理作業。

## 僅編輯器功能所需的許可權 {#permissions-required-for-editor-functionality-only}

對於需要編輯/更新內容片段而不允許他們刪除整個片段的使用者 ****，必須指派特定權限，因為內容片段編輯器的基本操作要求可以刪除暫時的子元素。

例如，操控變數時；編輯中繼資料或管理關聯內容時，也可以。

>[!NOTE]
>
>編輯/更新內容片段所需的刪除許可權包含在透過使用者和/或群組管理](/help/sites-administering/security.md#managing-permissions)指派的「刪除」許可權[中。

編輯/更新片段所需的許可權需要套用至包含內容片段的節點或適當的父節點（`/content/dam`下的任何層級）。 指派給此類父節點時，許可權將套用至該分支內的所有節點。

例如，將儲存所有內容片段的資料夾，例如：

* `/content/dam/contentfragments`

>[!CAUTION]
>
>在`/content/dam`上設定許可權也是可能的，因為所有內容片段都儲存在這裡。
>
>不過，此動作也會將相同的刪除許可權套用至&#x200B;*所有*&#x200B;其他資產型別。

允許特定使用者和/或群組編輯/更新內容片段的先決條件許可權為：

>[!NOTE]
>
>此清單顯示所需的所有許可權，而不只是刪除許可權。

* 對於內容片段節點或資料夾：

   * `jcr:addChildNodes`、`jcr:modifyProperties`

* 針對所有內容片段的`jcr:content`節點：

   * `jcr:addChildNodes`、`jcr:modifyProperties`和`jcr:removeChildNodes`

* 針對所有內容片段的`jcr:content`以下的所有節點：

   * `jcr:addChildNodes`、`jcr:modifyProperties`和`jcr:removeChildNodes`、`jcr:removeNode`

這些`remove`許可權必須由CRXDE Lite](/help/sites-administering/user-group-ac-admin.md#access-right-management)內的存取控制清單[管理。

`add`和`modify`許可權也可以在CRXDE Lite中管理，或使用使用者管理主控台。

例如，群組`content-authors-no-delete`的`remove`許可權定義：

![cf-delete-03](assets/cf-delete-03.png)
