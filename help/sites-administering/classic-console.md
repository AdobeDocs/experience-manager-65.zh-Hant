---
title: 傳統UI標籤主控台
description: 瞭解Adobe Experience Manager Classic UI標籤主控台。
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
docset: aem65
exl-id: 8c6ba22f-5555-4e3c-998a-9353bd44715b
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 2%

---


# 傳統UI標籤主控台{#classic-ui-tagging-console}

本節內容適用於傳統UI標籤主控台。

>[!NOTE]
>
>請參閱[管理標籤](/help/sites-administering/tags.md#tagging-console)，以取得觸控最佳化UI標籤主控台的詳細資料。

若要存取傳統UI標籤主控台：

* 作者
* 以管理許可權登入
* 瀏覽至主控台
例如，[https://localhost:4502/tagging](https://localhost:4502/tagging)

![傳統主控台視窗](assets/managing_tags_usingthetagasministrationconsole.png)

## 建立標籤和名稱空間 {#creating-tags-and-namespaces}

1. 根據您開始使用的層級，您可以使用&#x200B;**新增**&#x200B;來建立標籤或名稱空間：

   如果您選取&#x200B;**標籤**，則可以建立名稱空間：

   ![正在建立名稱空間對話方塊](assets/creating_tags_andnamespaces.png)

   如果您選取名稱空間（例如&#x200B;**Demo**），則可以在名稱空間中建立標籤：

   ![正在建立標籤對話方塊](assets/creating_tags_andnamespacesinnewnamespace.png)

1. 在這兩種情況下，都輸入

   * **標題**
（*必要*）標籤的顯示標題。 雖然可以輸入任何字元，
建議您不要使用這些特殊字元：

      * `colon (:)` — 名稱空間分隔符號
      * `forward slash (/)` — 子標籤分隔符號

     如果輸入，將不會顯示這些字元。

   * **名稱**
（*必要*）標籤的節點名稱。

   * **描述**
（*選用*）標籤的說明。

   * 選取&#x200B;**建立**

## 編輯標記 {#editing-tags}

1. 在右側窗格中，選取您要編輯的標籤。
1. 按一下&#x200B;**編輯**。
1. 您可以修改&#x200B;**標題**&#x200B;和&#x200B;**描述**。
1. 按一下&#x200B;**儲存**&#x200B;以關閉對話方塊。

## 刪除標記 {#deleting-tags}

1. 在右側窗格中，選取您要刪除的標籤。
1. 按一下&#x200B;**刪除**。
1. 按一下&#x200B;**是**&#x200B;關閉對話方塊。

   標籤不應再列出。

## 啟用和停用標籤 {#activating-and-deactivating-tags}

1. 在右側窗格中，選取您要啟用（發佈）或停用（取消發佈）的名稱空間或標籤。
1. 視需要按一下&#x200B;**啟用**&#x200B;或&#x200B;**停用**。

## 清單 — 顯示標籤參照的位置 {#list-showing-where-tags-are-referenced}

**清單**&#x200B;會開啟新視窗，顯示使用反白標籤的所有頁面的路徑：

![尋找參照標籤的位置](assets/list_showing_wheretagsarereferenced.png)

## 移動標記 {#moving-tags}

為協助標籤管理員和開發人員清理分類或重新命名標籤ID，可以將標籤移至新位置：

1. 開啟&#x200B;**標籤**&#x200B;主控台。
1. 選取標籤，然後按一下頂端工具列（或內容功能表中）中的&#x200B;**移動……**。
1. 在&#x200B;**移動標籤**&#x200B;對話方塊中，定義：

   * **到**，目的地節點。
   * **將新節點名稱重新命名為**。

1. 按一下&#x200B;**移動**。

**移動標籤**&#x200B;對話方塊如下所示：

![移動標籤](assets/move_tag.png)

>[!NOTE]
>
>作者不應移動標籤或重新命名標籤ID。 必要時，作者應僅[變更標籤標題](#editing-tags)。

## 合併標記 {#merging-tags}

分類法有重複專案時，可使用合併標籤。 標籤A合併至標籤B時，所有標籤為標籤A的頁面都會標籤為標籤B，且標籤A不再可供作者使用。

若要將標籤合併到另一個標籤中：

1. 開啟&#x200B;**標籤**&#x200B;主控台。
1. 選取標籤，然後按一下頂端工具列（或內容功能表中）中的&#x200B;**合併……**。
1. 在&#x200B;**合併標籤**&#x200B;對話方塊中，定義：

   * **到**，目的地節點。

1. 按一下&#x200B;**合併**。

**合併標籤**&#x200B;對話方塊如下所示：

![正在合併標籤](assets/mergetag.png)

## 計算標籤的使用量 {#counting-usage-of-tags}

若要檢視標籤的使用次數：

1. 開啟&#x200B;**標籤**&#x200B;主控台。
1. 按一下頂端工具列中的&#x200B;**計數使用情形**：計數欄會顯示結果。

## 管理不同語言的標記 {#managing-tags-in-different-languages}

標籤的可選`title`屬性可以翻譯成多種語言。 然後，就可以根據使用者語言或頁面語言來顯示標籤`titles`。

### 定義多種語言的標籤標題 {#defining-tag-titles-in-multiple-languages}

下列程式說明如何將標籤&#x200B;**Animals**&#x200B;的`title`翻譯成英文、德文和法文：

1. 移至&#x200B;**標籤**&#x200B;主控台。
1. 編輯&#x200B;**標籤** > **Stock Photography**&#x200B;底下的標籤&#x200B;**Animals**。
1. 新增下列語言的翻譯：

   * **英文**：動物
   * **德文**：提爾
   * **法文**： Animaux

1. 儲存變更。

對話方塊如下所示：

![編輯標籤](assets/edit_tag.png)

「標籤」主控台使用使用者語言設定，因此對於Animal標籤，會針對在使用者屬性中將語言設定為法文的使用者顯示「Animaux」。

若要新增語言至對話方塊，請參閱&#x200B;**開發人員標籤**&#x200B;區段中的[新增語言至編輯標籤對話方塊](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog)區段。

### 以指定語言在頁面屬性中顯示標籤標題 {#displaying-tag-titles-in-page-properties-in-a-specified-language}

依照預設，頁面屬性中的標籤`titles`會以頁面語言顯示。 頁面屬性中的標籤對話方塊有一個語言欄位，可讓您以不同語言顯示標籤`titles`。 下列程式說明如何以法文顯示標籤`titles`：

1. 請參閱上一節，將法文翻譯新增至&#x200B;**標籤** > **Stock Photography**&#x200B;下方的&#x200B;**Animals**。
1. 在&#x200B;**Geometrixx**&#x200B;網站的英文分支中，開啟&#x200B;**產品**&#x200B;頁面的頁面屬性。
1. 開啟&#x200B;**標籤/關鍵字**&#x200B;對話方塊（透過選取[標籤/關鍵字]顯示區域右側的下拉式功能表），然後從右下角的下拉式功能表中選取&#x200B;**法文**&#x200B;語言。
1. 使用左右箭頭捲動，直到能夠選取&#x200B;**Stock Photography**&#x200B;標籤

   選取「**Animaux** (**Animaux**)」標籤，然後在對話方塊外部選取，以關閉該標籤，並將標籤新增至頁面屬性。

   ![正在編輯另一個標籤](assets/french_tag.png)

依預設，「頁面屬性」對話方塊會根據頁面語言顯示標籤`titles`。

一般而言，如果頁面語言可用，則會從頁面語言取得標籤的語言。 當[`tag` Widget](/help/sites-developing/building.md#tagging-on-the-client-side)用於其他情況時（例如，表單或對話方塊中），標籤語言會依據內容而定。

>[!NOTE]
>
>標準頁面元件中的標籤雲和中繼關鍵字會根據頁面語言使用當地語系化的標籤`titles` （如果有的話）。
