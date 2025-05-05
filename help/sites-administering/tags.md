---
title: 管理標記
description: 瞭解如何管理Adobe Experience Manager中的標籤。
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
exl-id: ff041ef0-e566-4373-818e-76680ff668d8
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1769'
ht-degree: 9%

---

# 管理標記 {#administering-tags}

標籤是一種將網站內容分類的快速輕鬆方法。 它們可視為關鍵字或標籤（中繼資料），以便在搜尋結果中更快地找到內容。

在Adobe Experience Manager (AEM)中，標籤可以是

* 頁面的內容節點（請參閱[使用標籤](/help/sites-authoring/tags.md)）

* 資產的中繼資料節點(請參閱[管理數位Assets的中繼資料](/help/assets/metadata.md))

除了頁面和資產，標籤還用於AEM Communities功能

* 使用者產生的內容（請參閱[標籤UGC）](/help/communities/tag-ugc.md)

* 啟用資源（請參閱[標籤啟用資源](/help/communities/functions.md#catalog-function)）

## 標記功能 {#tag-features}

AEM中的部分標籤功能包括：

* 標籤可以分組到各種名稱空間中。 此類階層允許建立分類。 這些分類法在整個 AEM 中都適用。
* 新建立標籤的主要限制是在特定名稱空間中必須是唯一的。
* 標籤的標題不應包含標籤路徑分隔字元（如果存在的話，也不會顯示）

   * 冒號`:` — 分隔名稱空間標籤
   * 正斜線`/` — 分隔子標籤

* 作者和網站訪客可套用標籤。 無論由誰建立，所有形式的標記都可在指定給頁面或搜尋時用於選取。
* 「tag-administrators」群組的成員以及擁有`/content/cq:tags`修改許可權的成員可以建立標籤並修改其分類。

   * 包含子標籤的標籤稱為容器標籤
   * 非容器標籤的標籤稱為分葉標籤
   * 標籤名稱空間是葉標籤或容器標籤

* [搜尋元件](https://helpx.adobe.com/tw/experience-manager/core-components/using/quick-search.html)使用標籤來協助尋找內容。
* 標籤由[Teaser元件](https://helpx.adobe.com/tw/experience-manager/core-components/using/teaser.html)使用，該元件會監視使用者的標籤雲以提供目標內容。
* 如果標籤是內容的重要方面

   * 請務必封裝標籤與使用這些標籤的頁面
   * 請確定[標籤許可權](#setting-tag-permissions)啟用讀取存取權

## 標記主控台 {#tagging-console}

「標籤」主控台可用來建立和管理標籤及其分類。 一個目標是避免有許多與基本相同的事物相關的類似標籤：例如，頁面和頁面或鞋子和鞋子。

標籤可透過分組到名稱空間、在建立新標籤之前檢視現有標籤的使用情況，以及重新組織而不中斷標籤與目前參照內容的連線來管理。

若要存取「標籤」主控台：

* 作者
* 以管理許可權登入
* 從全域導覽

   * 選取&#x200B;**`Tools`**
   * 選取&#x200B;**`General`**
   * 選取&#x200B;**`Tagging`**

![managing_tags_usingthetagasministrationconsole](assets/managing_tags_usingthetagasministrationconsolea.png)

### 建立命名空間 {#creating-a-namespace}

若要建立名稱空間，請選取&#x200B;**`Create Namespace`**&#x200B;圖示。

名稱空間本身是標籤，不會包含任何子標籤。 但是，若要繼續建立分類法，請[建立子標籤](#creating-tags)，這些標籤又可能是分葉標籤或容器標籤。

![chlimage_1-183](assets/chlimage_1-183a.png) ![creating_tags_andnamespaces](assets/creating_tags_andnamespacesa.png)

* **標題**
  *（必要）*&#x200B;名稱空間的顯示標題。

* **名稱**
  *（選擇性）*&#x200B;名稱空間的名稱。 如果未指定，則會從標題建立有效的節點名稱。 請參閱 [TagID](/help/sites-developing/framework.md#tagid)。

* **說明**
  *（選擇性）*&#x200B;名稱空間的描述。

輸入必要資訊後

* 選取&#x200B;**建立**

### 標籤作業 {#operations-on-tags}

選取名稱空間或其他標籤後，您便可以進行下列操作：

* [檢視屬性](#viewing-tag-properties)
* [參考](#showing-tag-references)
* [建立標記](#creating-tags)
* [編輯](#editing-tags)
* [移動](#moving-tags)
* [合併](#merging-tags)
* [發佈](#publishing-tags)
* [未發佈](#unpublishing-tags)
* [刪除](#deleting-tags)

![chlimage_1-184](assets/chlimage_1-184.png)

當瀏覽器視窗不夠寬以顯示所有圖示時，最右邊的圖示會群組在&#x200B;**`... More`**&#x200B;圖示下，這會在選取時顯示隱藏作業圖示的下拉式清單。

![chlimage_1-185](assets/chlimage_1-185.png)

### 選取名稱空間標籤 {#selecting-a-namespace-tag}

第一次選取時，如果名稱空間不含任何標籤，則屬性會顯示在右側，否則子標籤會顯示。 選取的每個標籤都會顯示其所包含的標籤，如果沒有子標籤，則會顯示其屬性。

若要選取操作標籤，並選取多個專案，請僅選取標題旁的圖示。 選取標題將只會顯示屬性或開啟標籤以顯示其內容。

![chlimage_1-186](assets/chlimage_1-186.png) ![chlimage_1-187](assets/chlimage_1-187.png)

### 檢視標記屬性 {#viewing-tag-properties}

![chlimage_1-188](assets/chlimage_1-188.png)

選取名稱空間或其他標籤時，選取&#x200B;**`View Properties`**&#x200B;圖示可顯示有關`name`、上次編輯時間和參照數目的資訊。 如果發佈，則會顯示上次發佈的時間以及發佈者的ID。 此資訊會顯示在標籤欄左側的欄中。

![chlimage_1-189](assets/chlimage_1-189.png)

### 顯示標籤參照 {#showing-tag-references}

![chlimage_1-190](assets/chlimage_1-190.png)

選取名稱空間或其他標籤時，選取&#x200B;**參考**&#x200B;圖示將會識別標籤已套用的內容。

初始顯示是套用的標籤計數。

![chlimage_1-191](assets/chlimage_1-191.png)

透過選取計數右側的箭頭，會列出參照名稱。

當游標停留在參照上時，參照的路徑會顯示為工具提示。

![chlimage_1-192](assets/chlimage_1-192.png)

### 建立標記 {#creating-tags}

![chlimage_1-193](assets/chlimage_1-193.png)

當選取名稱空間或其他標籤時（選取標題旁的圖示），可透過選取&#x200B;**`Create Tag`**&#x200B;圖示為目前標籤建立子標籤。

![chlimage_1-194](assets/chlimage_1-194.png)

* **標題**
*（必要） *標籤的顯示標題。

* **名稱**
*（選用） *標籤的名稱。 如果未指定，則會從標題建立有效的節點名稱。 請參閱 [TagID](/help/sites-developing/framework.md#tagid)。

* **描述**
*（選用） *標籤的說明。

輸入必要資訊後

* 選取&#x200B;**建立**

### 編輯標記 {#editing-tags}

![chlimage_1-195](assets/chlimage_1-195.png)

選取名稱空間或其他標籤時，可以變更標題、說明，並透過選取&#x200B;**`Edit`**&#x200B;圖示提供標題的當地語系化。

完成編輯後，選取&#x200B;**儲存**。

如需如何新增語言翻譯的詳細資料，請參閱「[管理不同語言的標記](#managing-tags-in-different-languages)」一節。

![chlimage_1-196](assets/chlimage_1-196.png)

### 移動標記 {#moving-tags}

![chlimage_1-197](assets/chlimage_1-197.png)

選取名稱空間或其他標籤時，選取&#x200B;**`Move`**&#x200B;圖示可讓標籤管理員和開發人員將標籤移至新位置或重新命名以清理分類。 所選取的標記是容器標記時，若移動該標記，所有子標記也會跟著移動。

>[!NOTE]
>
>建議僅允許作者[編輯](#editing-tags)標籤的`title`，不要移動或重新命名標籤。

![chlimage_1-198](assets/chlimage_1-198.png)

* **路徑**
  *（唯讀）*&#x200B;選取標籤的目前路徑。

* **移至**
瀏覽至要移動標籤的新路徑。

* **重新命名為**
最初顯示標籤目前的`name`。 可輸入新的`name`。

* 選取&#x200B;**儲存**

### 合併標記 {#merging-tags}

![chlimage_1-199](assets/chlimage_1-199.png)

分類法有重複專案時，可使用合併標籤。 標籤A合併至標籤B時，所有以標籤A標籤的頁面都會以標籤B標籤，且標籤A不再可供作者使用。

選取名稱空間或其他標籤時，選取&#x200B;**合併**&#x200B;圖示會開啟一個面板，其中可能選取要合併的路徑。

![chlimage_1-200](assets/chlimage_1-200.png)

* **路徑**
  *（唯讀）*&#x200B;選取要合併至其他標籤的標籤路徑。

* **合併至**
瀏覽以選取要合併的標籤路徑。

>[!NOTE]
>
>合併之後，原先選取的&#x200B;**路徑**&#x200B;將（實際上）不再存在。
>
>移動或合併參照的標籤時，並不會實際刪除標籤，因此可以保留參照。

### 發佈標記 {#publishing-tags}

![chlimage_1-201](assets/chlimage_1-201.png)

選取名稱空間或其他標籤時，請選取&#x200B;**Publish**&#x200B;圖示以在發佈環境中啟動標籤。 與頁面內容類似，無論是否為容器標籤，都只會發佈選取的標籤。

若要發佈分類（名稱空間和子標籤），最佳實務是建立名稱空間的[套件](/help/sites-administering/package-manager.md) （請參閱[分類根節點](/help/sites-developing/framework.md#taxonomy-root-node)）。 在建立套件之前，請務必[套用許可權](#setting-tag-permissions)至名稱空間。

### 取消發佈標記 {#unpublishing-tags}

![chlimage_1-202](assets/chlimage_1-202.png)

選取名稱空間或其他標籤時，選取&#x200B;**取消發佈**&#x200B;圖示將會停用作者環境中的標籤，並將其從發佈環境中移除。 與`Delete`作業類似，如果選取的標籤是容器標籤，則其所有子標籤將在作者環境中停用，並從發佈環境中移除。

### 刪除標記 {#deleting-tags}

![chlimage_1-203](assets/chlimage_1-203.png)

選取名稱空間或其他標籤時，選取&#x200B;**刪除**&#x200B;圖示將會從作者環境中永久移除標籤。 如果該標記已發布，也會將其從發佈環境中移除。如果選取的標籤是容器標籤，則會一併移除其所有子標籤。

## 設定標籤許可權 {#setting-tag-permissions}

標籤許可權是[&#39;安全（預設值）&#39;](/help/sites-administering/production-ready.md)；此為發佈環境的最佳實務，需要明確允許標籤讀取許可權。 基本上，這是透過在作者上設定許可權後建立標籤名稱空間的套件，並在所有發佈執行個體上安裝套件來完成。

* 在作者執行個體上

   * 以管理許可權登入
   * 存取[安全性主控台](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console)，

      * 例如，瀏覽至http://localhost:4502/useradmin

   * 在左窗格中，選取要授與[讀取許可權](/help/sites-administering/security.md#permissions)的群組（或使用者）
   * 在右窗格中，找到&#x200B;**Path &#x200B;** 到「標籤名稱空間」

      * 例如，`/content/cq:tags/mycommunity`

   * 選取&#x200B;**讀取**&#x200B;資料行中的`checkbox`
   * 選取&#x200B;**儲存**

![chlimage_1-204](assets/chlimage_1-204.png)

* 確認所有發佈執行個體都具有相同許可權

   * 一種方法是在作者上[建立名稱空間套件](/help/sites-administering/package-manager.md#package-manager)

      * 在`Advanced`索引標籤上，為`AC Handling`選取`Overwrite`

   * 復寫封裝

      * 從封裝管理員選擇`Replicate`

## 管理不同語言的標記 {#managing-tags-in-different-languages}

標籤的`title`屬性可以翻譯成多種語言。 一旦翻譯，就可以根據使用者語言或頁面語言顯示適當的標籤`title`。

### 定義多種語言的標籤標題 {#defining-tag-titles-in-multiple-languages}

以下說明如何將標籤&#x200B;**Animals**&#x200B;的`title`從英文翻譯成德文和法文。

首先，請選取&#x200B;**Stock Photography**&#x200B;名稱空間下的標籤，然後選取&#x200B;**`Edit`**&#x200B;圖示（請參閱[編輯標籤](#editing-tags)區段）。

「編輯標籤」面板可讓您選擇要將標籤標題當地語系化的語言。

選取每種語言時，會出現一個文字輸入方塊，可在其中輸入翻譯的標題。

輸入所有翻譯之後，請選取&#x200B;**儲存**&#x200B;以結束編輯模式。

![chlimage_1-205](assets/chlimage_1-205.png)

一般而言，為標籤選擇的語言會從頁面語言中取得（可用時）。 當[`tag` Widget](/help/sites-developing/building.md#tagging-on-the-client-side)用於其他情況時（例如，表單或對話方塊中），標籤語言會依據內容而定。

「標籤」控制檯並非使用頁面語言設定，而是使用使用者語言設定。 在「標籤」控制檯中，若使用者在使用者屬性中將語言設定為法文，則會針對「Animaux」標籤顯示「Animaux」。

若要新增語言到對話方塊，請參閱[新增語言到編輯標籤對話方塊](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog)。

>[!NOTE]
>
>標準頁面元件中的標籤雲和中繼關鍵字會根據頁面語言使用當地語系化的標籤`titles` （如果有的話）。

## 資源 {#resources}

* [為開發人員加上標籤](/help/sites-developing/tags.md)

  有關標籤架構和延伸並在自訂應用程式中包含標籤的資訊。

* [傳統UI標籤主控台](/help/sites-administering/classic-console.md)
