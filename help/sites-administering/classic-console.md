---
title: 傳統UI標籤控制台
seo-title: 傳統UI標籤控制台
description: 了解傳統UI標籤控制台。
seo-description: 了解傳統UI標籤控制台。
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
source-wordcount: '871'
ht-degree: 0%

---

# 傳統UI標籤控制台{#classic-ui-tagging-console}

本節適用於傳統UI標籤控制台。

觸控最佳化UI標籤控制台位於[此處](/help/sites-administering/tags.md#tagging-console)。

若要存取傳統UI標籤控制台：

* 論作者
* 以管理權限登錄
* 瀏覽至主控台
例如， [https://localhost:4502/tagging](https://localhost:4502/tagging)

![](assets/managing_tags_usingthetagasministrationconsole.png)

## 建立標籤和命名空間{#creating-tags-and-namespaces}

1. 根據您從頭開始的級別，可以使用&#x200B;**New**&#x200B;建立標籤或命名空間：

   如果選擇&#x200B;**標籤**，則可以建立命名空間：

   ![](assets/creating_tags_andnamespaces.png)

   如果您選取命名空間（例如&#x200B;**Demo**），可以在該命名空間中建立標籤：

   ![](assets/creating_tags_andnamespacesinnewnamespace.png)

1. 在這兩種情況下，請輸入

   * **標題**
(
*必要*)標籤的顯示標題。雖然可以輸入任何字元，
建議不要使用這些特殊字元：

      * `colon (:)`  — 命名空間分隔字元
      * `forward slash (/)`  — 子標籤分隔符

      如果輸入，則不會顯示這些字元。

   * **名稱**
(
*必要*)標籤的節點名稱。

   * **說明**
(
*選用*)標籤的說明。

   * 選擇&#x200B;**建立**


## 編輯標籤{#editing-tags}

1. 在右側窗格中，選取您要編輯的標籤。
1. 按一下「**編輯**」。
1. 您可以修改&#x200B;**Title**&#x200B;和&#x200B;**Description**。
1. 按一下&#x200B;**Save**&#x200B;以關閉對話框。

## 刪除標籤{#deleting-tags}

1. 在右側窗格中，選取您要刪除的標籤。
1. 按一下&#x200B;**Delete**。
1. 按一下「**是**」以關閉對話方塊。

   標籤不應再列出。

## 啟用和停用標籤{#activating-and-deactivating-tags}

1. 在右側窗格中，選取您要啟用（發佈）或停用（取消發佈）的命名空間或標籤。
1. 視需要按一下「**啟用**」或「**停用**」。

## 清單 — 顯示引用標籤的位置{#list-showing-where-tags-are-referenced}

**** 會使用醒目提示的標籤，顯示所有頁面路徑的新視窗：

![](assets/list_showing_wheretagsarereferenced.png)

## 移動標籤{#moving-tags}

為了協助標籤管理員和開發人員清除分類法或重新命名標籤ID，可將標籤移至新位置：

1. 開啟&#x200B;**Tagging**&#x200B;控制台。
1. 選擇標籤，然後按一下&#x200B;**移動……**（在頂端工具列中），或在內容功能表中)。
1. 在&#x200B;**移動標籤**&#x200B;對話方塊中，定義：

   * **到**，即目的地節點。
   * **重新命名為**，即為新節點名稱。

1. 按一下&#x200B;**移動**。

**移動標籤**&#x200B;對話框如下所示：

![](assets/move_tag.png)

>[!NOTE]
>
>作者不應移動標籤或重新命名標籤ID。 必要時，作者只應[變更標籤標題](#editing-tags)。

## 正在合併標籤{#merging-tags}

分類法有重複項目時，可使用合併標籤。 標籤A合併到標籤B時，所有標籤有標籤A的頁面都會加上標籤B的標籤，而標籤A已不再可供作者使用。

要將標籤合併到另一個標籤：

1. 開啟&#x200B;**Tagging**&#x200B;控制台。
1. 選擇標籤，然後按一下&#x200B;**合併……**（在頂端工具列中），或在內容功能表中)。
1. 在&#x200B;**合併標籤**&#x200B;對話方塊中，定義：

   * **進入**，即目的地節點。

1. 按一下&#x200B;**Merge**。

**合併標籤**&#x200B;對話框如下所示：

![](assets/mergetag.png)

## 計算標籤的使用{#counting-usage-of-tags}

若要查看某個標籤的使用次數：

1. 開啟&#x200B;**Tagging**&#x200B;控制台。
1. 按一下頂端工具列中的&#x200B;**計算使用量**:「計數」欄會顯示結果。

## 管理不同語言的標籤{#managing-tags-in-different-languages}

標籤的可選`title`屬性可以翻譯成多種語言。 然後，可以根據用戶語言或頁面語言顯示標籤`titles`。

### 以多種語言定義標籤標題{#defining-tag-titles-in-multiple-languages}

以下過程說明如何將標籤&#x200B;**Animals**&#x200B;的`title`翻譯成英文、德文和法文：

1. 前往&#x200B;**Tagging**&#x200B;主控台。
1. 編輯&#x200B;**Animals**&#x200B;在&#x200B;**Tags** > **Stock Photography**&#x200B;下方的標籤。
1. 添加以下語言的翻譯：

   * **英文**:動物
   * **德文**:蒂埃
   * **法文**:阿尼莫

1. 儲存變更。

對話方塊如下所示：

![](assets/edit_tag.png)

「標籤」控制台使用用戶語言設定，因此對於「動物」標籤，在用戶屬性中將語言設定為法文的用戶會顯示「動畫」。

要向對話框添加新語言，請參閱&#x200B;**Developers**&#x200B;部分中的[Adding a New Language to the Edit Tag Dialog](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog)一節。

### 以指定語言{#displaying-tag-titles-in-page-properties-in-a-specified-language}在頁面屬性中顯示標籤標題

依預設，頁面屬性中的標籤`titles`會以頁面語言顯示。 頁面屬性中的標籤對話方塊有一個語言欄位，可讓以不同語言顯示標籤`titles`。 以下過程說明如何以法文顯示標籤`titles`:

1. 請參閱上一節，將法文翻譯新增至&#x200B;**Tags** > **Stock Photography**&#x200B;下方的&#x200B;**Animals**。
1. 開啟&#x200B;**Geometrixx**&#x200B;網站英文分支中&#x200B;**產品**&#x200B;頁面的頁面屬性。
1. 開啟&#x200B;**標籤/關鍵字**&#x200B;對話框（通過選擇「標籤/關鍵字」顯示區域右側的下拉菜單），然後從右下角的下拉菜單中選擇&#x200B;**法語**&#x200B;語言。
1. 使用左 — 右箭頭捲動，直到能夠選取&#x200B;**Stock Photography**&#x200B;標籤

   選取&#x200B;**Animals**(**Animaux**)標籤，然後在對話方塊外部選取以關閉該標籤，並將標籤新增至頁面屬性。

   ![](assets/french_tag.png)

依預設，「頁面屬性」對話方塊會根據頁面語言顯示`titles`標籤。

一般而言，如果頁面語言可用，則會從頁面語言擷取標籤的語言。 當在其他情況下（例如在表單或對話方塊中）使用[ `tag`介面工具集](/help/sites-developing/building.md#tagging-on-the-client-side)時，標籤語言會依據內容而定。

>[!NOTE]
>
>標籤雲和標準頁面元件中的中繼關鍵字會根據頁面語言使用本地化標籤`titles`（如果可用）。
