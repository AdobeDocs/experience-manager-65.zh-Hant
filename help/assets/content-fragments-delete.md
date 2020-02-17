---
title: 內容片段——刪除考量事項
seo-title: 內容片段——刪除考量事項
description: 內容片段——刪除考量事項
seo-description: 內容片段——刪除考量事項
uuid: e7ac1809-159f-4d02-ad30-dc6c246e8a04
contentOwner: aheimoz
topic-tags: content-fragments
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: ec21237f-9186-49b4-8039-99df4db7c14a
docset: aem65
translation-type: tm+mt
source-git-commit: 6edecebec6d64a30fd05887a56d81f80863c5213

---


# 內容片段——刪除考量事項{#content-fragments-delete-considerations}

## 權限——刪除或不刪除 {#permissions-delete-or-not-delete}

刪除內容的能力強大，但可能很敏感，許多產業需要限制和控制這些權限的分發方式。

關於刪除權限，內容片段必須考慮在兩個層級：

1. **內容片段為單一實體。**

   * **使用案例**:需要編輯／更新內容片段——並刪除整 **個片段的使用者**。
   * **權限**:您可 [以透過「使](/help/sites-administering/security.md#actions) 用者」和／或「群組管理」指派「刪除」權限 [](/help/sites-administering/security.md#managing-permissions)。

1. **構成內容片段的多個子實體；例如，變化，子節點。**

   內容片段編輯器的基本操作要求可以刪除這種瞬時子元素。 例如，在操縱變化時；編輯中繼資料或管理相關內容時也一樣。

   * **使用案例**:需要編輯／更新內容片段的使用者， **而不允許刪除整個片段**。
   * **權限**:請參 [閱僅編輯器功能所需的權限](/help/assets/content-fragments-delete.md#permissions-required-for-editor-functionality-only)。

>[!NOTE]
>
>當使用者沒有任何刪 [除權限](/help/sites-administering/security.md#actions) ，內容片段編輯器會以唯 *讀模式運作* 。

>[!NOTE]
>
>另請參閱 [如何在AEM中審核使用者管理作業](/help/sites-administering/audit-user-management-operations.md)。

## 僅編輯器功能所需的權限 {#permissions-required-for-editor-functionality-only}

對於需要編輯／更新內容片段而不允許他們刪除整個片段的使用者 ****，必須指派特定權限，因為內容片段編輯器的基本操作要求可以刪除暫時的子元素。

例如，在操縱變化時；編輯中繼資料或管理相關內容時也一樣。

>[!NOTE]
>
>編輯／更新內容片段所需的刪除權限，會包含在透過「使用者」和／或「群組管理」 [指派的「刪除」權限中](/help/sites-administering/security.md#managing-permissions)。

編輯／更新片段所需的權限必須套用至包含內容片段的節點，或適當的父節點(在任何層級下 `/content/dam`)。 當指派給此類父節點時，權限將會套用至該分支中的所有節點。

例如，包含所有內容片段的資料夾，例如：

* `/content/dam/contentfragments`

>[!CAUTION]
>
>也可設定權 `/content/dam` 限，因為所有內容片段都儲存在這裡。
>
>不過，此動作也會將相同的刪除權 *限套用* 至所有其他資產類型。

允許特定使用者和／或群組編輯／更新內容片段的權限先決條件為：

>[!NOTE]
>
>此清單顯示所有所需權限，而不只是刪除權限。

* 對於「內容片段」節點或資料夾：

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* 對於所 `jcr:content`有內容片段的節點：

   * `jcr:addChildNodes`, `jcr:modifyProperties` &amp; `jcr:removeChildNodes`

* 對於所有內容片段 `jcr:content` 的下方所有節點：

   * `jcr:addChildNodes`, `jcr:modifyProperties` 而 `jcr:removeChildNodes`且 `jcr:removeNode`

這些 `remove` 權限必須使 [用CRXDE Lite中的訪問控制清單進行管理](/help/sites-administering/user-group-ac-admin.md#access-right-management)。

您也 `add` 可 `modify` 以在CRXDE Lite中管理和權限，或使用使用者管理主控台。

例如，群組權 `remove` 限的定義 `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)

