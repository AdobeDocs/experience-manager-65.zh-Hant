---
title: 經典UI標籤控制台
seo-title: Classic UI Tagging Console
description: 瞭解經典UI標籤控制台。
seo-description: Learn about the Classic UI Tagging Console.
uuid: 51e29422-f967-424b-a7fd-4ca2ddc6b8a3
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: b279c033-bc93-4e62-81ad-123c40b9fdd2
docset: aem65
exl-id: 8c6ba22f-5555-4e3c-998a-9353bd44715b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---

# 經典UI標籤控制台{#classic-ui-tagging-console}

此部分用於「經典UI標籤控制台」。

觸控優化的UI標籤控制台 [這裡](/help/sites-administering/tags.md#tagging-console)。

要訪問「經典UI標籤」控制台：

* 作者
* 以管理權限登錄
* 例如，瀏覽到控制台 [https://localhost:4502/tagging](https://localhost:4502/tagging)

![](assets/managing_tags_usingthetagasministrationconsole.png)

## 建立標籤和命名空間 {#creating-tags-and-namespaces}

1. 根據您從開始的級別，可以使用 **新建**:

   如果選擇 **標籤** 可以建立命名空間：

   ![](assets/creating_tags_andnamespaces.png)

   如果選擇了命名空間(例如 **演示**)可以在該命名空間中建立標籤：

   ![](assets/creating_tags_andnamespacesinnewnamespace.png)

1. 在兩種情況下都輸入

   * **標題**
(
*必需*)標籤的顯示標題。 雖然可以輸入任何字元，但建議不要使用以下特殊字元：

      * `colon (:)`  — 命名空間分隔符
      * `forward slash (/)`  — 子標籤分隔符

      如果輸入，則不顯示這些字元。

   * **名稱**
(
*必需*)標籤的節點名稱。

   * **說明**
(
*可選*)標籤的說明。

   * 選擇 **建立**


## 編輯標籤 {#editing-tags}

1. 在右窗格中，選擇要編輯的標籤。
1. 按一下 **編輯**。
1. 可以修改 **標題** 和 **說明**。
1. 按一下 **保存** 按鈕

## 刪除標籤 {#deleting-tags}

1. 在右窗格中，選擇要刪除的標籤。
1. 按一下&#x200B;**刪除**。
1. 按一下 **是** 按鈕

   標籤不應再列出。

## 激活和停用標籤 {#activating-and-deactivating-tags}

1. 在右窗格中，選擇要激活（發佈）或停用（取消發佈）的命名空間或標籤。
1. 按一下 **激活** 或 **停用** 按需要。

## 清單 — 顯示引用標籤的位置 {#list-showing-where-tags-are-referenced}

**清單** 開啟一個新窗口，顯示使用突出顯示的標籤的所有頁面的路徑：

![](assets/list_showing_wheretagsarereferenced.png)

## 移動標籤 {#moving-tags}

為幫助標籤管理員和開發人員清理分類或更名標籤ID，可以將標籤移動到新位置：

1. 開啟 **標籤** 控制台。
1. 選擇標籤並按一下 **移動……** 工具欄中。
1. 在 **移動標籤** 對話框，定義：

   * **至**&#x200B;的子菜單。
   * **更名為**，新節點名稱。

1. 按一下 **移動**。

的 **移動標籤** 對話框如下所示：

![](assets/move_tag.png)

>[!NOTE]
>
>作者不應移動標籤或更名標籤ID。 必要時，作者只應 [更改標籤標題](#editing-tags)。

## 合併標籤 {#merging-tags}

當分類具有重複項時，可以使用合併標籤。 當標籤A合併到標籤B中時，標籤A的所有頁面都將用標籤B進行標籤，並且標籤A不再可供作者使用。

將標籤合併到另一個標籤中：

1. 開啟 **標籤** 控制台。
1. 選擇標籤並按一下 **合併……** 工具欄中。
1. 在 **合併標籤** 對話框，定義：

   * **入**&#x200B;的子菜單。

1. 按一下 **合併**。

的 **合併標籤** 對話框如下所示：

![](assets/mergetag.png)

## 計數標籤的使用情況 {#counting-usage-of-tags}

要查看標籤的使用次數：

1. 開啟 **標籤** 控制台。
1. 按一下 **計數使用情況** 在頂部工具欄中：列計數顯示結果。

## 管理不同語言中的標籤 {#managing-tags-in-different-languages}

可選 `title`標籤的屬性可以翻譯成多種語言。 標籤 `titles` 然後，可根據用戶語言或頁面語言顯示。

### 定義多語言標籤標題 {#defining-tag-titles-in-multiple-languages}

以下過程說明如何轉換 `title`標籤 **動物** 英語、德語和法語：

1. 轉到 **標籤** 控制台。
1. 編輯標籤 **動物** 下 **標籤** > **股票攝影**。
1. 添加以下語言的翻譯：

   * **英語**:動物
   * **德語**:蒂埃
   * **法語**:阿尼莫

1. 儲存變更。

對話框如下所示：

![](assets/edit_tag.png)

「標籤」控制台使用用戶語言設定，因此對於「動物」標籤，在用戶屬性中將語言設定為法語的用戶，將顯示「Animaux」。

要向對話框添加新語言，請參閱一節 [向「編輯標籤」對話框添加新語言](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog) 的 **為開發人員添加標籤** 的子菜單。

### 以指定語言在頁面屬性中顯示標籤標題 {#displaying-tag-titles-in-page-properties-in-a-specified-language}

預設情況下，標籤 `titles`的子菜單。 頁面屬性中的標籤對話框具有允許顯示標籤的語言欄位 `titles`用另一種語言。 以下過程介紹如何顯示標籤 `titles`法語：

1. 請參閱上一節，將法語翻譯添加到 **動物** 下 **標籤** > **股票攝影**。
1. 開啟的頁面屬性 **產品** 英文分頁 **Geometrixx** 的子菜單。
1. 開啟 **標籤/關鍵字** 對話框（通過選擇「標籤/關鍵字」顯示區域右側的下拉菜單），然後選擇 **法語** 從右下角的下拉菜單開始。
1. 使用左箭頭滾動，直到能夠選擇 **股票攝影** 頁籤

   選擇 **動物** (**阿尼莫**)標籤並選擇對話框外部以關閉它，並將標籤添加到頁面屬性。

   ![](assets/french_tag.png)

預設情況下，「頁面屬性」對話框顯示標籤 `titles`根據頁面語言。

通常，如果頁面語言可用，則從頁面語言獲取標籤的語言。 當 [ `tag` 構件](/help/sites-developing/building.md#tagging-on-the-client-side) 在其它情況下（例如在窗體中或對話中）使用，標籤語言取決於上下文。

>[!NOTE]
>
>標籤雲和標準頁面元件中的元關鍵字使用本地化標籤 `titles`基於頁面語言（如果可用）。
