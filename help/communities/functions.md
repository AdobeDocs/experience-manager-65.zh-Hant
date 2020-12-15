---
title: 社群功能
seo-title: 社群功能
description: 瞭解如何存取社群功能主控台
seo-description: 瞭解如何存取社群功能主控台
uuid: d3d70134-f318-4709-a673-b01a3467d980
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 91833914-b811-4355-a97d-e1a9cb7441f1
docset: aem65
translation-type: tm+mt
source-git-commit: 3133f712be1380ae98e18e63c9598d760d2e7595
workflow-type: tm+mt
source-wordcount: '2458'
ht-degree: 6%

---


# 社群功能{#community-functions}

社群體驗預期的功能類型已廣為人知。 社群功能可做為社群功能。 基本上，這些頁面是預先連線的一或多個頁面，以實作社群功能，其需要的不只是在作者模式下將元件新增至頁面。 它們是用於定義[社區站點模板](/help/communities/sites.md)的結構的構成塊，從中建立[社區站點。](/help/communities/sites-console.md)

在建立社群網站後，就可使用標準[AEM製作模式](/help/sites-authoring/editing-content.md)將內容新增至產生的頁面。 各種社群功能如社群功能主控台所示。

>[!NOTE]
>
>用於建立[社區站點](/help/communities/sites-console.md)、[社區站點模板](/help/communities/sites.md)、[社區組模板](/help/communities/tools-groups.md)和[社區功能](/help/communities/functions.md)的控制台僅用於作者環境。

## 社區功能控制台{#community-functions-console}

要訪問作者環境中的社區功能控制台：

* 導覽至「**[!UICONTROL 工具]** > **[!UICONTROL 社群]** > **[!UICONTROL 社群功能]**」。

![社區功能](assets/community-functions.png)

## 預建函式{#pre-built-functions}

以下是AEM Communities所提供功能的簡短說明。 每個函式都包含一或多個AEM頁面，其中包含連線在功能中的Communities元件，此功能可輕鬆整合在[社群網站範本](/help/communities/sites.md)中。

社群網站範本提供社群網站的結構，包括登入、使用者設定檔、通知、訊息、網站選單、搜尋、主題和品牌功能。

### 標題和URL設定{#title-and-url-settings}

**標** 題和 **** URL是所有社群函式的通用屬性。

當社群函式被添加到社區站點模板或在[修改](/help/communities/sites-console.md#modifying-site-properties)社區站點結構時添加時，該函式的對話框開啟，以便可以配置標題和URL。

#### 設定功能詳細資料 {#configuration-function-details}

![chlimage_1-380](assets/chlimage_1-380.png)

* **標題**

   （*必要*）網站功能選單中顯示的文字

* **URL**

   （*必要*）用於生成URI的名稱。 名稱必須符合AEM和JCR所強加的[命名慣例](/help/sites-developing/naming-conventions.md)。

例如，使用從[開始使用](/help/communities/getting-started.md)教學課程建立的網站，如果

* 標題=網頁
* URL =頁面

然後，頁面的URL是https://localhost:4503/content/sites/engage/en/page.html

頁面的功能表連結會顯示為：

![chlimage_1-381](assets/chlimage_1-381.png)

### 活動資料流功能 {#activity-stream-function}

活動流函式是具有[活動流元件](/help/communities/activities.md)的頁面，其中選定了所有視圖（所有活動、用戶活動和以下）。 另請參閱[開發人員的Activity Stream Essentials](/help/communities/essentials-activities.md)。

新增至範本時，會開啟下列對話方塊：

#### 設定功能詳細資料 {#configuration-function-details-1}

![chlimage_1-382](assets/chlimage_1-382.png)

* [標題和URL設定](#title-and-url-settings)

* **顯示「我的活動」檢視**

   如果選中此選項，「活動」頁將包含一個頁籤，該頁籤根據當前成員在社區中生成的活動進行篩選。 已選取預設值。

* **顯示「所有活動」檢視**

   如果選中此選項，「活動」頁將包含一個頁籤，其中包含當前成員有權訪問的社區內生成的所有活動。 已選取預設值。

* **顯示「新聞資訊源」檢視**

   如果選中此選項，「活動」頁將包含一個頁籤，該頁籤根據當前成員正在跟蹤的活動篩選活動。 已選取預設值。

### 指定任務功能 {#assignments-function}

指派函式是定義[社群網站以啟用](/help/communities/overview.md#enablement-community)的基本功能。 它允許向社區成員分配支援資源。 另請參閱[開發人員的Assignments Essentials](/help/communities/essentials-assignments.md)。

此函式是[enablement add-on](/help/communities/enablement.md)的功能。 啟用附加元件需要額外的授權才能用於生產環境。

新增至範本時，只有[標題和URL設定](#title-and-url-settings)的組態。

### 部落格功能 {#blog-function}

部落格函式是具有[Blog元件](/help/communities/blog-feature.md)的頁面，其設定用於標籤、檔案上傳、追蹤成員以進行自我編輯、投票和協調。 另請參閱[開發人員的Blog Essentials](/help/communities/blog-developer-basics.md)。

新增至範本時，會開啟下列對話方塊：

![chlimage_1-383](assets/chlimage_1-383.png)

* [標題和URL設定](#title-and-url-settings)

* **允許有特殊權限的成員**

   如果選中此選項，則部落格僅允許特權成員通過允許選擇[特權成員組](/help/communities/users.md#privileged-members-group)來建立文章。 如果未選中，則允許所有社區成員建立。 已取消選取預設值。

* **允許檔案上傳**

   如果選取此選項，部落格會包含成員上傳檔案的功能。 已選取預設值。

* **允許執行緒式回覆**

   如果未選取，部落格會允許對文章的回覆（留言），但是不允許回覆留言。 已選取預設值。

* **允許主要內容**

   如果選取此選項，則會將部落格識別為[特色內容](/help/communities/featured.md)。 已選取預設值。

### 日曆功能 {#calendar-function}

日曆函式是具有[日曆元件](/help/communities/calendar.md)的頁，配置為允許標籤。 另請參閱[開發人員的Calendar Essentials](/help/communities/calendar-basics-for-developers.md)。

新增至範本時，會開啟下列對話方塊：

![chlimage_1-384](assets/chlimage_1-384.png)

* [標題和URL設定](#title-and-url-settings)

* **允許釘選**

   如果選中此選項，論壇允許將主題回覆釘在注釋清單的開頭。 已選取預設值。

* **允許有特殊權限的成員**

   如果選中此選項，則部落格僅允許特權成員通過允許選擇[特權成員組](/help/communities/users.md#privileged-members-group)來建立文章。 如果未選中，則允許所有社區成員建立。 已取消選取預設值。

* **允許檔案上傳**

   如果選取此選項，部落格會包含成員上傳檔案的功能。 已選取預設值。

* **允許執行緒式回覆**

   如果未選取，部落格會允許對文章的回覆（留言），但是不允許回覆留言。 已選取預設值。

* **允許主要內容**

   如果選取，其內容會識別為[特色內容](/help/communities/featured.md)。 已選取預設值。

### 目錄功能 {#catalog-function}

目錄功能使[啟用社區](/help/communities/overview.md#enablement-community)成員能夠瀏覽未分配給他們的啟用資源。 請參閱[為開發人員標籤啟用資源](/help/communities/tag-resources.md)和[Catalog Essentials](/help/communities/catalog-developer-essentials.md)。

如果社群網站的屬性` [Show in Catalog](/help/communities/resources.md)`設為true，則所有目錄中會顯示社群網站的所有啟用資源和學習路徑。 要明確包括資源和學習路徑，必須將[pre-filter](/help/communities/catalog-developer-essentials.md#pre-filters)應用到目錄。

新增至範本時，此設定可讓您指定用於設定提供給網站訪客之標籤篩選的標籤命名空間：

![目錄函式](assets/catalog-function.png)

* [標題和URL設定](#title-and-url-settings)

* **選取所有命名空間**

   所選標籤名稱空間定義哪些標籤可由訪客選擇以篩選目錄中所列的啟用資源清單。
如果選中此選項，則允許為社區站點使用的所有標籤名稱空間都可用。
如果取消選取，則可以選擇社區站點允許的一個或多個名稱空間。
已選取預設值。

### 精選內容功能{#featured-content-function}

精選內容功能是具有[精選內容元件](/help/communities/featured.md)的頁面，設定為允許新增和刪除註解。

可允許或禁止每個元件使用特徵內容的能力（請參閱[部落格函式](#blog-function)、[日曆函式](#calendar-function)、[論壇函式](#forum-function)、[標識函式](#ideation-function)和[QnA函式](#qna-function)）。

新增至範本時，只有[標題和URL設定](#title-and-url-settings)的組態。

### 檔案庫功能 {#file-library-function}

檔案庫函式是具有[檔案庫元件](/help/communities/file-library.md)的頁，配置為允許添加和刪除注釋。

新增至範本時，只有[標題和URL設定](#title-and-url-settings)的組態。

### 論壇功能 {#forum-function}

論壇函式是具有[論壇元件](/help/communities/forum.md)的頁面，該元件配置為標籤、檔案上載、跟蹤成員以自行編輯、投票和調節。

新增至範本時，會開啟下列對話方塊：

#### 設定功能詳細資料 {#configuration-function-details-2}

![chlimage_1-384](assets/chlimage_1-384.png)

* [標題和URL設定](#title-and-url-settings)

* **允許釘選**

   如果選中此選項，論壇允許將主題回覆釘在注釋清單的開頭。 已選取預設值。

* **允許有特殊權限的成員**

   如果選中此選項，則論壇僅允許特權成員通過允許選擇[特權成員組](/help/communities/users.md#privileged-members-group)來發佈主題。 如果未選取，則允許所有社群成員張貼。 已取消選取預設值。

* **允許檔案上傳**

   如果選取此選項，論壇將包含成員上傳檔案的功能。 已選取預設值。

* **允許執行緒式回覆**

   如果未選擇，論壇允許對主題進行評論，但不允許對這些評論進行回覆。 已選取預設值。

* **允許主要內容**

   如果選取此選項，則元件的內容會識別為[特色內容](/help/communities/featured.md)。 已選取預設值。

### 群組函式{#groups-function}

>[!CAUTION]
>
>群組函式必須&#x200B;*not*&#x200B;是&#x200B;*的第一個，也不是站點結構或社區站點模板中唯一的*&#x200B;函式。
>
>任何其他函式（例如[page函式](#page-function)）必須先包含並列出。

群組功能可讓社群成員在發佈環境中在社群網站內建立子社群。

視[設定](/help/communities/sites-console.md#groupmanagement)在[社群網站範本](/help/communities/sites.md)中包含群組功能時，群組可以是公用或私用，且一或多個社群群組範本可設定為在實際建立社群群組時（例如來自發佈環境）提供範本選擇。 [社群群組範本](/help/communities/tools-groups.md)指定為群組頁面（如論壇和日曆）建立哪些社群功能。

建立社區組時，會為新組動態建立成員組，可將成員分配或加入到該組。 如需詳細資訊，請參閱[管理使用者和使用者群組](/help/communities/users.md)。

從Communities [功能包1](/help/communities/deploy-communities.md#latestfeaturepack)開始，使用[Communities Sites的Groups控制台](/help/communities/groups.md)在作者環境中建立社區組，並且在啟用後可在發佈環境中建立社區組。

新增至範本時，會開啟下列對話方塊：

![chlimage_1-386](assets/chlimage_1-386.png)

* [標題和URL設定](#title-and-url-settings)

* **選取群組範本**

   允許選擇一個或多個啟用的組模板的下拉清單，新社區組（在發佈環境中）的將來建立者可從中選擇該模板。

* **允許有特殊權限的成員**

   如果選中此選項，則論壇僅允許特權成員通過允許選擇[特權成員安全組](/help/communities/users.md#privileged-members-group)來發佈主題。 如果未選取，則允許所有社群成員張貼。 已取消選取預設值。

* **允許發佈建立**

   如果選取此選項，授權社群成員可以在發佈環境中建立群組。 如果取消選取，則只能在作者環境中從「社群網站的群組」主控台建立新群組（子社群）。
已選取預設值。

### 創意力功能 {#ideation-function}

識別函式是具有一個[識別元件](/help/communities/ideation-feature.md)的頁面。

新增至範本時，會開啟下列對話方塊，指定範本的預設標題和URL名稱，以及預設顯示設定：

![chlimage_1-387](assets/chlimage_1-387.png)

* [標題和URL設定](#title-and-url-settings)

* **允許有特殊權限的成員**

   如果選中此選項，則論壇僅允許特權成員通過允許選擇[特權成員安全組](/help/communities/users.md#privileged-members-group)來發佈主題。 如果未選取，則允許所有社群成員張貼。 已取消選取預設值。

* **允許檔案上傳**

   如果選取此選項，此構想將包含成員上傳檔案的功能。 已選取預設值。

* **允許執行緒式回覆**

   如果未選取，此構想會允許對主題的回覆（留言），但不允許回覆留言。 已選取預設值。

* **允許主要內容**

   如果選取，其內容會識別為[特色內容](/help/communities/featured.md)。 已選取預設值。

### 排行榜功能 {#leaderboard-function}

排行榜功能是具有一個[排行榜元件](/help/communities/enabling-leaderboard.md)的頁面。

**注意**:在從社區模板建立社區站點 ** 後，Leenderboard元件需要進一步配置，該模板包括Leenderboard功能。指定Leaderboard元件的[規則](/help/communities/enabling-leaderboard.md#rules-tab)，該規則取決於社區站點的[計分和標章](/help/communities/implementing-scoring.md)的配置。

新增至範本時，會開啟下列對話方塊，指定範本的預設標題和URL名稱，以及預設顯示設定：

![chlimage_1-388](assets/chlimage_1-388.png)

* [標題和URL設定](#title-and-url-settings)

* **顯示徽章**

   如果選中此選項，則排行榜中會包含標誌表徵圖的列。
已取消選取預設值。

* **顯示徽章名稱**

   如果選中此選項，則標誌名稱的列將包括在排行榜中。
已取消選取預設值。

* **顯示頭像**

   如果選中此選項，成員的頭像影像將包含在排行榜中，位於其成員配置檔案的名稱連結旁邊。
已取消選取預設值。

### 頁面功能 {#page-function}

頁面功能會將空白頁面新增至社群網站，並將其連線至社群網站的功能：登入、選單、通知、訊息、主題和品牌。 使用[標準AEM製作模式](/help/sites-authoring/editing-content.md)將內容新增至頁面。

新增至範本時，只有[標題和URL設定](#title-and-url-settings)的組態。

### QnA 功能 {#qna-function}

QnA函式是一個具有[QnA元件](/help/communities/working-with-qna.md)的頁面，該元件配置為標籤、檔案上載、跟蹤成員以進行自我編輯、投票和調節。

將配置添加到模板時，該配置允許對特權成員進行限制：

![chlimage_1-384](assets/chlimage_1-384.png)

* [標題和URL設定](#title-and-url-settings)

* **允許釘選**

   如果選中此選項，論壇允許將主題回覆釘在注釋清單的開頭。 已選取預設值。

* **允許有特殊權限的成員**

   如果選中此選項，則QnA論壇僅允許特權成員通過允許選擇[特權成員組](/help/communities/users.md#privileged-members-group)來發佈問題。 如果未選取，則允許所有社群成員張貼。 已取消選取預設值。

* **允許檔案上傳**

   如果選中此選項，QnA論壇將包括成員上傳檔案的能力。 已選取預設值。

* **允許執行緒式回覆**

   如果未選取，QnA論壇允許對已張貼的問題留言（答案），但不允許回覆答。 已選取預設值。

* **允許主要內容**

   如果選取，其內容會識別為[特色內容](/help/communities/featured.md)。 已選取預設值。

## 建立社群功能 {#create-community-function}

通過選擇「社區功能」控制台頂部的`Create Community Function`表徵圖，可以建立社區功能。 您可以建立以相同AEM Blueprint為基礎的多個函式，然後以作者編輯模式開啟，進行唯一自訂。

![chlimage_1-390](assets/chlimage_1-390.png)

### 社群功能名稱 {#community-function-name}

![chlimage_1-391](assets/chlimage_1-391.png)

在「社群功能名稱」面板上，會設定名稱、說明，以及函式是啟用還是停用：

* **社群功能名稱**

   用於顯示和儲存的函式名稱。

* **社群功能說明**

   顯示的函式說明。

* **已禁用／啟用**

   控制函式是否可參考的切換開關。

### AEM 藍圖 {#aem-blueprint}

![chlimage_1-392](assets/chlimage_1-392.png)

在`AEM Blueprint`面板上，可以選擇作為社區功能基礎實現的藍圖。

社群功能是包含一或多個頁面的迷你網站，已預先連線以加入社群網站，包括登入、使用者設定檔、通知、訊息、網站選單、搜尋、主題和品牌功能。 在建立函式後，[可以在作者編輯模式下開啟函式](#open-community-function)並自定義頁面或元件設定。

由於社區函式被實作為[blueprint](/help/sites-administering/msm-livecopy.md#creatingablueprint)的[即時副本](/help/sites-administering/msm.md#live-copies)，因此可以對影響從包含該函式的[社區站點模板](/help/communities/sites.md)或[社區組模板](/help/communities/tools-groups.md)建立的所有社區站點頁的函式進行改變。 您也可以將頁面與其父藍圖取消關聯，以進行頁面層級的修改。

另請參閱[多站點管理器](/help/sites-administering/msm.md)。

### 縮圖 {#thumbnail}

![chlimage_1-393](assets/chlimage_1-393.png)

在「縮圖」面板上，影像可上傳以顯示在[社群功能主控台](#community-functions-console)中。

## 開啟社群功能 {#open-community-function}

![chlimage_1-394](assets/chlimage_1-394.png)

選擇`Open Community Function`表徵圖可進入作者編輯模式以編寫頁面內容並修改功能元件的配置。

### 配置元件{#configuring-components}

社群函式會實作為AEM Blueprint的即時副本，其詳細資訊會記錄在[ Multi Site Manager](/help/sites-administering/msm.md)中。

您不僅可以製作頁面內容，還可以設定元件。

如果在已建立的社區站點的頁面上配置元件，則可能需要取消[inheritance](/help/sites-administering/msm-livecopy.md#changing-live-copy-content)以配置元件。 配置完成時，應重新建立繼承。

有關配置詳細資訊，請訪問[Communities Components](/help/communities/author-communities.md)作者。

## 編輯社群功能 {#edit-community-function}

![chlimage_1-395](assets/chlimage_1-395.png)

選擇`Edit Community Function`表徵圖，使用與[建立社區函式](#create-community-function)相同的面板來編輯函式的屬性，包括啟用或禁用該函式。
