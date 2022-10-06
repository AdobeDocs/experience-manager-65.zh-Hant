---
title: 傳統UI標籤控制台
seo-title: Classic UI Tagging Console
description: 了解傳統UI標籤控制台。
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

# 傳統UI標籤控制台{#classic-ui-tagging-console}

本節適用於傳統UI標籤控制台。

觸控最佳化UI標籤控制台為 [此處](/help/sites-administering/tags.md#tagging-console).

若要存取傳統UI標籤控制台：

* 論作者
* 以管理權限登錄
* 例如，瀏覽至主控台， [https://localhost:4502/tagging](https://localhost:4502/tagging)

![](assets/managing_tags_usingthetagasministrationconsole.png)

## 建立標籤和命名空間 {#creating-tags-and-namespaces}

1. 根據您從頭開始的層級，您可以使用 **新增**:

   如果您選取 **標籤** 您可以建立命名空間：

   ![](assets/creating_tags_andnamespaces.png)

   如果您選取命名空間(例如 **示範**)您可以在該命名空間中建立標籤：

   ![](assets/creating_tags_andnamespacesinnewnamespace.png)

1. 在這兩種情況下，請輸入

   * **標題**
(
*必填*)標籤的顯示標題。 雖然可以輸入任何字元，但建議不要使用這些特殊字元：

      * `colon (:)`  — 命名空間分隔字元
      * `forward slash (/)`  — 子標籤分隔符

      如果輸入，則不會顯示這些字元。

   * **名稱**
(
*必填*)標籤的節點名稱。

   * **說明**
(
*可選*)標籤的說明。

   * 選取 **建立**


## 編輯標籤 {#editing-tags}

1. 在右側窗格中，選取您要編輯的標籤。
1. 按一下 **編輯**.
1. 您可以修改 **標題** 和 **說明**.
1. 按一下 **儲存** 以關閉對話方塊。

## 刪除標籤 {#deleting-tags}

1. 在右側窗格中，選取您要刪除的標籤。
1. 按一下&#x200B;**刪除**。
1. 按一下 **是** 以關閉對話方塊。

   標籤不應再列出。

## 啟用和停用標籤 {#activating-and-deactivating-tags}

1. 在右側窗格中，選取您要啟用（發佈）或停用（取消發佈）的命名空間或標籤。
1. 按一下 **啟動** 或 **停用** 視需要。

## 清單 — 顯示引用標籤的位置 {#list-showing-where-tags-are-referenced}

**清單** 會使用醒目提示的標籤開啟新視窗，顯示所有頁面的路徑：

![](assets/list_showing_wheretagsarereferenced.png)

## 移動標籤 {#moving-tags}

為了協助標籤管理員和開發人員清除分類法或重新命名標籤ID，可將標籤移至新位置：

1. 開啟 **標籤** 控制台。
1. 選取標籤，然後按一下 **移動……** 在頂端工具列中（或內容功能表中）。
1. 在 **移動標籤** 對話框，定義

   * **to**，即目的地節點。
   * **重新命名為**，即新節點名稱。

1. 按一下 **移動**.

此 **移動標籤** 對話方塊如下所示：

![](assets/move_tag.png)

>[!NOTE]
>
>作者不應移動標籤或重新命名標籤ID。 必要時，作者只應 [變更標籤標題](#editing-tags).

## 合併標籤 {#merging-tags}

分類法有重複項目時，可使用合併標籤。 當標籤A合併到標籤B時，所有標籤A的頁面都將被標籤B標籤，而標籤A不再可供作者使用。

要將標籤合併到另一個標籤：

1. 開啟 **標籤** 控制台。
1. 選取標籤，然後按一下 **合併……** 在頂端工具列中（或內容功能表中）。
1. 在 **合併標籤** 對話框，定義

   * **into**，即目的地節點。

1. 按一下 **合併**.

此 **合併標籤** 對話方塊如下所示：

![](assets/mergetag.png)

## 計算標籤的使用率 {#counting-usage-of-tags}

若要查看某個標籤的使用次數：

1. 開啟 **標籤** 控制台。
1. 按一下 **計數使用量** 在頂端工具列中：「計數」欄會顯示結果。

## 管理不同語言中的標籤 {#managing-tags-in-different-languages}

選填 `title`標籤的屬性可以翻譯成多種語言。 標籤 `titles` 然後可以根據使用者語言或頁面語言來顯示。

### 定義多種語言的標籤標題 {#defining-tag-titles-in-multiple-languages}

下列程式說明如何翻譯 `title`標籤 **動物** 英語、德語和法語：

1. 前往 **標籤** 控制台。
1. 編輯標籤 **動物** low **標籤** > **Stock Photography**.
1. 添加以下語言的翻譯：

   * **英文**:動物
   * **德文**:蒂埃
   * **法文**:阿尼莫

1. 儲存變更。

對話方塊如下所示：

![](assets/edit_tag.png)

「標籤」控制台使用用戶語言設定，因此對於「動物」標籤，在用戶屬性中將語言設定為法文的用戶會顯示「動畫」。

若要將新語言新增至對話方塊，請參閱區段 [將新語言添加到編輯標籤對話框](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog) 在 **為開發人員進行標籤** 區段。

### 以指定語言在頁面屬性中顯示標籤標題 {#displaying-tag-titles-in-page-properties-in-a-specified-language}

依預設，標籤 `titles`在中，屬性會以頁面語言顯示。 頁面屬性中的標籤對話方塊有一個語言欄位，可啟用標籤的顯示 `titles`用另一種語言。 以下程式說明如何顯示標籤 `titles`法語：

1. 請參閱上一節，將法文翻譯新增至 **動物** low **標籤** > **Stock Photography**.
1. 開啟 **產品** 頁 **Geometrixx** 頁簽。
1. 開啟 **標籤/關鍵字** 對話方塊（透過選取「標籤/關鍵字」顯示區域右側的下拉式功能表）並選取 **法文** 語言。
1. 使用向左至右箭頭捲動，直到能夠選取 **Stock Photography** 標籤

   選取 **動物** (**阿尼莫**)標籤，並在對話方塊外部選取以關閉該標籤，然後將標籤新增至頁面屬性。

   ![](assets/french_tag.png)

依預設，頁面屬性對話方塊會顯示標籤 `titles`根據頁面語言。

一般而言，如果頁面語言可用，則會從頁面語言擷取標籤的語言。 當 [ `tag` 介面](/help/sites-developing/building.md#tagging-on-the-client-side) 在其他情況下（例如在表單或對話方塊中），則標籤語言會依據內容。

>[!NOTE]
>
>標籤雲和標準頁面元件中的中繼關鍵字使用本地化標籤 `titles`根據頁面語言（如果有）。
