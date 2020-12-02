---
title: 管理標籤
seo-title: 管理標籤
description: 瞭解如何在AEM中管理標籤。
seo-description: 瞭解如何在AEM中管理標籤。
uuid: 77e1280a-feea-4edd-94b6-4fb825566c42
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 69253ee9-8c28-436b-9331-6fb875f64cba
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd
workflow-type: tm+mt
source-wordcount: '1769'
ht-degree: 0%

---


# 管理標籤{#administering-tags}

標籤是快速且簡單的網站內容分類方法。 它們可視為關鍵字或標籤（中繼資料），可讓搜尋結果更快速找到內容。

在Adobe Experience Manager(AEM)中，標籤可以是

* 頁面的內容節點（請參閱[使用標籤](/help/sites-authoring/tags.md)）

* 資產的中繼資料節點（請參閱[管理數位資產的中繼資料](/help/assets/metadata.md)）

除了頁面和資產外，標籤也用於AEM Communities功能

* 使用者產生的內容（請參閱[標籤UGC）](/help/communities/tag-ugc.md)

* 啟用資源（請參閱[標籤啟用資源](/help/communities/functions.md#catalog-function)）

## 標籤功能{#tag-features}

AEM中標籤的部分功能包括：

* 標籤可分組為各種名稱空間。 這種層次結構允許建立分類。 這些分類在AEM中是全域性的。
* 新建立標籤的主要限制是，這些標籤在特定命名空間中必須是唯一的。
* 標籤的標題不應包含標籤路徑分隔字元（如果存在，也不會顯示）

   * 冒號`:` —— 分隔namespace標籤
   * 正斜線`/` —— 分隔子標籤

* 標籤可由作者和網站訪客套用。 不論其建立者為何，在指派給頁面或搜尋時，都可使用所有形式的標籤供選取。
* 「tag-administrators」組的成員和具有`/content/cq:tags`修改權限的成員可以建立標籤並修改其分類。

   * 包含子標籤的標籤稱為容器標籤
   * 非容器標籤的標籤稱為葉標籤
   * 標籤命名空間是葉標籤或容器標籤

* [搜尋元件](https://helpx.adobe.com/experience-manager/core-components/using/quick-search.html)會使用標籤來協助尋找內容。
* [Teaser元件](https://helpx.adobe.com/experience-manager/core-components/using/teaser.html)會使用標籤，它會監視使用者的標籤雲以提供目標內容。
* 如果標籤是內容的重要方面

   * 請務必使用使用標籤的頁面來封裝標籤
   * 確保[標籤權限](#setting-tag-permissions)啟用讀取訪問

## 標籤控制台{#tagging-console}

「標籤」控制台用於建立和管理標籤及其分類。 其中一個目標是避免使用許多與基本相同的標籤：例如，頁面和頁面，鞋類和鞋類。

標籤的管理方式為：將標籤分組為命名空間、在建立新標籤之前檢閱現有標籤的使用情形，以及重新組織標籤，而不會中斷標籤與目前參考內容的連線。

要訪問標籤控制台：

* 在作者上
* 以管理權限登入
* 從全局導航

   * 選擇&#x200B;**`Tools`**
   * 選擇&#x200B;**`General`**
   * 選擇&#x200B;**`Tagging`**

![managing_tags_usingthetagasministrationconsole](assets/managing_tags_usingthetagasministrationconsolea.png)

### 建立命名空間{#creating-a-namespace}

要建立新的命名空間，請選擇&#x200B;**`Create Namespace`**&#x200B;表徵圖。

namespace本身是標籤，不需要包含任何子標籤。 不過，若要繼續建立分類，請[建立子標籤](#creating-tags)，而子標籤又可以是葉標籤或容器標籤。

![chlimage_1-183](assets/chlimage_1-183a.png) ![creating_tags_andnamespaces](assets/creating_tags_andnamespacesa.png)

* **標題**

   *（必要）* namespace的顯示標題。

* **名稱**
   *（可選）* namespace的名稱。如果未指定，則從「標題」建立有效的節點名稱。 請參閱[TagID](/help/sites-developing/framework.md#tagid)。

* **說明**

   *（可選）* namespace的說明。

在輸入所需資訊後

* 選擇&#x200B;**建立**

### 標籤{#operations-on-tags}的操作

選擇命名空間或其他標籤可使用下列操作：

* [檢視屬性](#viewing-tag-properties)
* [引用](#showing-tag-references)
* [建立標記](#creating-tags)
* [編輯](#editing-tags)
* [移動](#moving-tags)
* [合併](#merging-tags)
* [發佈](#publishing-tags)
* [未發佈](#unpublishing-tags)
* [刪除](#deleting-tags)

![chlimage_1-184](assets/chlimage_1-184.png)

當瀏覽器視窗不夠寬以顯示所有圖示時，最右邊的圖示會分組在&#x200B;**`... More`**&#x200B;圖示下方，如此當選取時，會顯示隱藏作業圖示的下拉式清單。

![chlimage_1-185](assets/chlimage_1-185.png)

### 選擇名稱空間標籤{#selecting-a-namespace-tag}

首次選擇時，如果命名空間不包含任何標籤，則屬性會顯示在右側，否則會顯示子標籤。 選取的每個標籤都會顯示其所包含的標籤，或其屬性（如果沒有子標籤）。

要選擇操作的標籤，並且要進行多選，請僅選擇標題旁的表徵圖。 選取標題時，只會顯示屬性，或開啟標籤以顯示其內容。

![chlimage_1-186](assets/chlimage_1-186.png) ![chlimage_1-187](assets/chlimage_1-187.png)

### 查看標籤屬性{#viewing-tag-properties}

![chlimage_1-188](assets/chlimage_1-188.png)

選擇命名空間或其他標籤時，選擇&#x200B;**`View Properties`**&#x200B;表徵圖會顯示有關`name`、上次編輯時間和引用數的資訊。 如果已發佈，則會顯示上次發佈的時間和發佈者的ID。 這些資訊會顯示在標籤欄左側的欄中。

![chlimage_1-189](assets/chlimage_1-189.png)

### 顯示標籤引用{#showing-tag-references}

![chlimage_1-190](assets/chlimage_1-190.png)

選擇命名空間或其他標籤時，選擇&#x200B;**References**&#x200B;表徵圖將標識已應用標籤的內容。

初始顯示是套用的標籤計數。

![chlimage_1-111](assets/chlimage_1-191.png)

通過選擇計數右側的箭頭，將列出參考名稱。

將滑鼠指標暫留在參照上時，參照的路徑會顯示為工具提示。

![chlimage_1-112](assets/chlimage_1-192.png)

### 建立標籤{#creating-tags}

![chlimage_1-193](assets/chlimage_1-193.png)

當選取namespace或其他標籤時（透過選取標題旁的圖示），可選取&#x200B;**`Create Tag`**&#x200B;圖示來建立目前標籤的子標籤。

![chlimage_1-194](assets/chlimage_1-194.png)

* **Title**
*（必要）*標籤的顯示標題。

* **名稱**
*（選用）*標籤的名稱。如果未指定，則從「標題」建立有效的節點名稱。 請參閱[TagID](/help/sites-developing/framework.md#tagid)。

* **說明**
*（選用）*標籤的說明。

在輸入所需資訊後

* 選擇&#x200B;**建立**

### 編輯標籤{#editing-tags}

![chlimage_1-195](assets/chlimage_1-195.png)

當選取namespace或其他標籤時，可以變更標題、說明，並選取**`Edit`**圖示來提供標題的本地化。

進行編輯後，選擇&#x200B;**保存**。

有關添加語言翻譯的詳細資訊，請參閱[管理不同語言中的標籤](#managing-tags-in-different-languages)一節。

![chlimage_1-196](assets/chlimage_1-196.png)

### 移動標籤{#moving-tags}

![chlimage_1-197](assets/chlimage_1-197.png)

選擇命名空間或其他標籤時，選擇&#x200B;**`Move`**&#x200B;表徵圖將允許標籤管理員和開發人員通過將標籤移動到新位置或更名來清理分類。 當選取的標籤是容器標籤時，移動標籤也會移動所有子標籤。

>[!NOTE]
>
>建議作者僅能編輯[標籤的`title`，而不能移動或重新命名標籤。](#editing-tags)

![chlimage_1-198](assets/chlimage_1-198.png)

* **路徑**

   *（唯讀）* 選取標籤的目前路徑。

* **移**
至瀏覽至要移動標籤的新路徑。

* **重新命**
名為最初顯示 
`name`標籤上。可輸入新`name`。

* 選擇&#x200B;**保存**

### 合併標籤{#merging-tags}

![chlimage_1-199](assets/chlimage_1-199.png)

當分類有重複項時，可使用合併標籤。 當標籤A合併到標籤B時，標籤A的所有頁面都將被標籤為標籤B，而標籤A不再可供作者使用。

當選擇命名空間或其他標籤時，選擇&#x200B;**Merge**&#x200B;表徵圖將開啟一個面板，其中可以選擇要合併的路徑。

![chlimage_1-200](assets/chlimage_1-200.png)

* **路徑**

   *（只讀）* 選定要合併到其他標籤中的標籤的路徑。

* **合併**
到瀏覽以選擇要合併到的標籤路徑。

>[!NOTE]
>
>合併後，原先選取的&#x200B;**Path**&#x200B;將不再存在。
>
>當移動或合併參考標籤時，標籤不會實際刪除，因此可以維護參考。

### 發佈標籤{#publishing-tags}

![chlimage_1-201](assets/chlimage_1-201.png)

選取命名空間或其他標籤時，選取&#x200B;**Publish**&#x200B;圖示，以在發佈環境中啟動標籤。 與頁面內容類似，只會發佈選取的標籤，不論它是否為容器標籤。

要發佈分類（命名空間和子標籤），最佳做法是建立命名空間的[包](/help/sites-administering/package-manager.md)（請參見[分類根節點](/help/sites-developing/framework.md#taxonomy-root-node)）。 在建立包之前，請務必[將權限](#setting-tag-permissions)應用到命名空間。

### 取消發佈標籤{#unpublishing-tags}

![chlimage_1-202](assets/chlimage_1-202.png)

當選取命名空間或其他標籤時，選取「取消發佈&#x200B;****」圖示會停用作者環境中的標籤，並將它從發佈環境中移除。 與`Delete`操作類似，如果選取的標籤是容器標籤，則其所有子標籤將在作者環境中停用，並從發佈環境中移除。

### 刪除標籤{#deleting-tags}

![chlimage_1-203](assets/chlimage_1-203.png)

當選取namespace或其他標籤時，選擇&#x200B;**Delete**&#x200B;圖示將永久移除作者環境中的標籤。 如果標籤已發佈，也會從發佈環境中移除。 如果選取的標籤是容器標籤，其所有子標籤也會移除。

## 設定標籤權限{#setting-tag-permissions}

標籤權限為[&#39;secure（依預設）&#39;](/help/sites-administering/production-ready.md);此為發佈環境的最佳做法，要求明確允許標籤的讀取權限。 基本上，這是透過在作者上設定權限後建立「標籤命名空間」的套件，並在所有發佈例項上安裝此套件來完成。

* 在作者實例上

   * 以管理權限登入
   * 訪問[安全控制台](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console),

      * 例如，瀏覽至http://localhost:4502/useradmin
   * 在左窗格中，選擇要授予[讀權限](/help/sites-administering/security.md#permissions)的組（或用戶）
   * 在右窗格中，找到「標籤命名空間」的**路徑**

      * 例如，`/content/cq:tags/mycommunity`
   * 在&#x200B;**Read**&#x200B;欄中選擇`checkbox`
   * 選擇&#x200B;**保存**



![chlimage_1-204](assets/chlimage_1-204.png)

* 確保所有發佈例項都擁有相同的權限

   * 一種方法是在作者上建立名稱空間的[軟體包](/help/sites-administering/package-manager.md#package-manager)

      * 在`Advanced`標籤上，對於`AC Handling`，請選擇`Overwrite`
   * 複製包

      * 從包管理器選擇`Replicate`


## 管理不同語言的標籤{#managing-tags-in-different-languages}

標籤的`title`屬性可以翻譯成多種語言。 翻譯後，可以根據用戶語言或頁面語言顯示相應的標籤`title`。

### 定義多語言標籤標題{#defining-tag-titles-in-multiple-languages}

以下說明如何將標籤&#x200B;**Animals**&#x200B;的`title`從英文翻譯為德文和法文。

首先，在&#x200B;**Stock Photography**&#x200B;命名空間下選擇標籤，然後選擇**`Edit`**圖示（請參閱[編輯標籤](#editing-tags)區段）。

「編輯標籤」面板提供選擇標籤標題本地化語言的功能。

在選擇每種語言時，將出現一個文本輸入框，可在其中輸入翻譯的標題。

輸入所有翻譯後，選擇&#x200B;**保存**&#x200B;退出編輯模式。

![chlimage_1-205](assets/chlimage_1-205.png)

一般而言，為標籤選擇的語言是從頁面語言（若有）取用。 當[ `tag`介面工具集](/help/sites-developing/building.md#tagging-on-the-client-side)用於其他情況（例如在表單或對話方塊中）時，標籤語言會依據內容而定。

「標籤」控制台不使用頁面語言設定，而是使用用戶語言設定。 在「標籤」控制台中，對於「動物」標籤，在其用戶屬性中將語言設定為法語的用戶，將顯示「Animaux」。

要向對話框添加新語言，請參閱[將新語言添加到編輯標籤對話框](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog)。

>[!NOTE]
>
>標準頁面元件中的標籤雲和中繼關鍵字會根據頁面語言（若有的話）使用本地化的標籤`titles`。

## 資源 {#resources}

* [為開發人員加上標籤](/help/sites-developing/tags.md)

   有關標籤框架以及在自定義應用程式中擴展和包括標籤的資訊。

* [傳統UI標籤控制台](/help/sites-administering/classic-console.md)

