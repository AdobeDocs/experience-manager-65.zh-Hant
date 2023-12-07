---
title: 社群功能
description: 瞭解如何存取社群功能主控台
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 2395c895-c611-43ac-abb6-c2bc4b4a41f4
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2215'
ht-degree: 2%

---

# 社群功能{#community-functions}

社群體驗中預期的功能型別眾所周知。 社群功能可作為社群功能使用。 基本上，這些頁面是預先接線的一或多個頁面，用於實作社群功能，該功能不僅需要以製作模式將元件新增至頁面。 它們是用於定義結構的基礎要素 [社群網站範本](/help/communities/sites.md) 社群網站所在位置 [已建立](/help/communities/sites-console.md).

建立社群網站後，可使用標準將內容新增到產生的頁面 [AEM製作模式](/help/sites-authoring/editing-content.md). 社群功能主控台提供各種社群功能。

>[!NOTE]
>
>用於建立的控制檯 [社群網站](/help/communities/sites-console.md)， [社群網站範本](/help/communities/sites.md)， [社群群組範本](/help/communities/tools-groups.md)、和 [社群功能](/help/communities/functions.md) 僅供作者環境使用。

## 社群功能主控台 {#community-functions-console}

若要在製作環境中存取社群功能主控台：

* 瀏覽至 **[!UICONTROL 工具]** > **[!UICONTROL Communities]** > **[!UICONTROL 社群功能]**.

![社群功能](assets/community-functions.png)

## 預先建立的函式 {#pre-built-functions}

以下簡述AEM Communities所提供的功能。 每個函式都包含一或多個AEM頁面，這些頁面包含Communities元件，這些元件已連線在一起，構成可輕鬆整合至的功能 [社群網站範本](/help/communities/sites.md).

社群網站範本提供社群網站的結構，包括登入、使用者設定檔、通知、訊息、網站功能表、搜尋、主題設定和品牌功能。

### 標題和URL設定 {#title-and-url-settings}

**標題** 和 **URL** 是所有社群功能通用的屬性。

將社群功能新增至社群網站範本或新增至 [修改](/help/communities/sites-console.md#modifying-site-properties) 在社群網站的結構中，會開啟函式的對話方塊，以便設定標題和URL。

#### 設定功能詳細資料 {#configuration-function-details}

![title-url-details](assets/title-url-details.png)

* **標題**

  (*必填*)顯示在網站功能表中的文字

* **URL**

  (*必填*)用來產生URI的名稱。 名稱必須符合 [命名慣例](/help/sites-developing/naming-conventions.md) 由AEM和JCR所強制。

例如，使用從下列位置建立的網站 [快速入門](/help/communities/getting-started.md) 教學課程，如果

* 標題=網頁
* URL =頁面

接著，頁面的URL會是https://localhost:4503/content/sites/engage/en/page.html

而頁面的功能表連結會顯示為：

![engage-page](assets/engage-page.png)

### 活動資料流功能 {#activity-stream-function}

活動資料流函式是具有 [活動資料流元件](/help/communities/activities.md) 已選取所有檢視（所有活動、使用者活動及後續活動）。 另請參閱 [Activity Stream Essentials](/help/communities/essentials-activities.md) 適用於開發人員。

新增至範本時，下列對話方塊隨即開啟：

#### 設定功能詳細資料 {#configuration-function-details-1}

![function-details](assets/function-details.png)

* [標題和URL設定](#title-and-url-settings)

* **顯示「我的活動」檢視**

  如果選取，「活動」頁面會包含索引標籤，該索引標籤會根據目前成員在社群內產生的活動來篩選活動。 預設為已選取。

* **顯示「所有活動」檢視**

  如果選取，「活動」頁面會包含標籤，其中包含社群內產生且目前成員有權存取的所有活動。 預設為已選取。

* **顯示「新聞資訊源」檢視**

  如果選取，「活動」頁面會包含索引標籤，以根據目前成員所關注的活動來篩選活動。 預設為已選取。

### 部落格功能 {#blog-function}

部落格功能是具有 [部落格元件](/help/communities/blog-feature.md) 針對標籤、檔案上傳、追蹤、成員自我編輯、投票和稽核進行設定。 另請參閱 [部落格要點](/help/communities/blog-developer-basics.md) 適用於開發人員。

新增至範本時，下列對話方塊隨即開啟：

![部落格元件](assets/blog-component.png)

* [標題和URL設定](#title-and-url-settings)

* **允許有特殊許可權的成員**

  如果選取，則部落格僅允許擁有特殊許可權的成員透過選擇 [有特殊許可權的成員群組](/help/communities/users.md#privileged-members-group). 如果未選取，則允許建立所有社群成員。 預設為取消選取。

* **允許檔案上傳**

  如果選取，部落格會包含成員上傳檔案的功能。 預設為已選取。

* **允許執行緒式回覆**

  若未選取，部落格會允許回覆（評論）文章，但不允許回複評論。 預設為已選取。

* **允許主要內容**

  如果選取，則會將部落格識別為 [主要內容](/help/communities/featured.md). 預設為已選取。

### 日曆功能 {#calendar-function}

行事曆功能是具有 [日曆元件](/help/communities/calendar.md) 設定為允許標籤。 另請參閱 [行事曆要點](/help/communities/calendar-basics-for-developers.md) 適用於開發人員。

新增至範本時，下列對話方塊隨即開啟：

![calendar-details](assets/calendar-details.png)

* [標題和URL設定](#title-and-url-settings)

* **允許釘選**

  如果選取，論壇允許將主題回覆釘選到評論清單的開頭。 預設為已選取。

* **允許有特殊許可權的成員**

  如果選取，則部落格僅允許擁有特殊許可權的成員透過選擇 [有特殊許可權的成員群組](/help/communities/users.md#privileged-members-group). 如果未選取，則允許建立所有社群成員。 預設為取消選取。

* **允許檔案上傳**

  如果選取，部落格會包含成員上傳檔案的功能。 預設為已選取。

* **允許執行緒式回覆**

  若未選取，部落格會允許回覆（評論）文章，但不允許回複評論。 預設為已選取。

* **允許主要內容**

  如果選取，則會將其內容識別為 [主要內容](/help/communities/featured.md). 預設為已選取。

### 主要內容功能 {#featured-content-function}

主要內容功能是具有 [主要內容元件](/help/communities/featured.md) 已設定為允許新增和刪除註解。

每個元件可允許或不允許特色內容功能(請參閱 [部落格功能](#blog-function)， [行事曆功能](#calendar-function)， [論壇功能](#forum-function)， [創意力功能](#ideation-function)、和 [QnA函式](#qna-function))。

將新增到範本時，唯一的設定是 [標題和URL設定](#title-and-url-settings).

### 檔案庫功能 {#file-library-function}

檔案庫函式是具有 [檔案庫元件](/help/communities/file-library.md) 已設定為允許新增和刪除註解。

將新增到範本時，唯一的設定是 [標題和URL設定](#title-and-url-settings).

### 論壇功能 {#forum-function}

論壇功能是具有 [論壇元件](/help/communities/forum.md) 針對標籤、檔案上傳、追蹤、成員自我編輯、投票和稽核進行設定。

新增至範本時，下列對話方塊隨即開啟：

#### 設定功能詳細資料 {#configuration-function-details-2}

![論壇 — 元件1](assets/forum-component1.png)

* [標題和URL設定](#title-and-url-settings)

* **允許釘選**

  如果選取，論壇允許將主題回覆釘選到評論清單的開頭。 預設為已選取。

* **允許有特殊許可權的成員**

  如果選取，論壇僅允許有特殊許可權的成員透過選擇 [有特殊許可權的成員群組](/help/communities/users.md#privileged-members-group). 如果未選取，則允許所有社群成員張貼。 預設為取消選取。

* **允許檔案上傳**

  如果選取，論壇會包含成員上傳檔案的功能。 預設為已選取。

* **允許執行緒式回覆**

  如果未選取，論壇會允許對主題發表評論，但不允許回覆這些評論。 預設為已選取。

* **允許主要內容**

  如果選取，則會將元件的內容識別為 [主要內容](/help/communities/featured.md). 預設為已選取。

### 群組功能 {#groups-function}

>[!CAUTION]
>
>群組功能必須 *非* 成為 *第一或唯一* 在網站結構或社群網站範本中起作用。
>
>任何其他函式，例如 [頁面函式](#page-function)，必須先包含並列出。

群組功能可讓社群成員在發佈環境中的社群網站內建立子社群。

依據 [設定](/help/communities/sites-console.md#groupmanagement) 當「群組」功能包含在 [社群網站範本](/help/communities/sites.md)，群組可以是公用或私用，而一或多個社群群組範本可設定為在實際建立社群群組時（例如從發佈環境）提供範本選擇。 A [社群群組範本](/help/communities/tools-groups.md) 指定針對群組頁面建立的Communities功能，例如論壇和行事曆。

建立社群群組時，會為新群組動態建立成員群組，成員可以指派或加入該群組。 如需詳細資訊，請參閱 [管理使用者和使用者群組](/help/communities/users.md).

社群起始 [feature pack 1](/help/communities/deploy-communities.md#latestfeaturepack)，社群群組是在作者環境中使用 [社群網站的群組主控台](/help/communities/groups.md)、和，可在啟用時於發佈環境中建立。

新增至範本時，下列對話方塊隨即開啟：

![group-template-config](assets/group-template-config.png)

* [標題和URL設定](#title-and-url-settings)

* **選取群組範本**

  一個下拉式清單，可讓您選取一或多個已啟用的群組範本，新社群群組（在發佈環境中）的未來建立者可從中進行選擇。

* **允許有特殊許可權的成員**

  如果選取，論壇僅允許有特殊許可權的成員透過選擇 [有特殊許可權的成員安全性群組](/help/communities/users.md#privileged-members-group). 如果未選取，則允許所有社群成員張貼。 預設為取消選取。

* **允許發佈建立**

  如果選取，獲授權的社群成員可以在發佈環境中建立群組。 如果取消選取，則只能從Communities Sites的「群組」主控台在作者環境中建立新群組（子社群）。
預設為已選取。

### 創意力功能 {#ideation-function}

創意力功能是具備此功能的頁面 [創意力元件](/help/communities/ideation-feature.md).

新增至範本時，會開啟下列對話方塊，其中指定範本的預設「標題」和URL名稱，以及預設顯示設定：

![創意力功能](assets/ideation-function.png)

* [標題和URL設定](#title-and-url-settings)

* **允許有特殊許可權的成員**

  如果選取，論壇僅允許有特殊許可權的成員透過選擇 [有特殊許可權的成員安全性群組](/help/communities/users.md#privileged-members-group). 如果未選取，則允許所有社群成員張貼。 預設為取消選取。

* **允許檔案上傳**

  如果選取，構思包括成員上傳檔案的能力。 預設為已選取。

* **允許執行緒式回覆**

  如果未選取，此創意允許主題回覆（註解），但不允許回覆註解。 預設為已選取。

* **允許主要內容**

  如果選取，則會將其內容識別為 [主要內容](/help/communities/featured.md). 預設為已選取。

### 排行榜功能 {#leaderboard-function}

排行榜功能是一頁有排行榜 [排行榜元件](/help/communities/enabling-leaderboard.md).

**注意**：排行榜元件需要進一步設定 *晚於* 社群網站是從包含排行榜功能的社群範本建立的。 指定排行榜元件的 [規則](/help/communities/enabling-leaderboard.md#rules-tab)，取決於 [評分和徽章](/help/communities/implementing-scoring.md) 適用於社群網站。

新增至範本時，會開啟下列對話方塊，其中指定範本的預設「標題」和URL名稱，以及預設顯示設定：

![排行榜對話方塊](assets/leaderboard-dialog.png)

* [標題和URL設定](#title-and-url-settings)

* **顯示徽章**

  如果選取，則排行榜會包含徽章圖示欄。
預設為取消選取。

* **顯示徽章名稱**

  如果選取，則排行榜會包含徽章名稱的欄。
預設為取消選取。

* **顯示頭像**

  如果選取，成員的頭像影像會包含在排行榜中，位於其名稱連結旁邊，以連結至其成員設定檔。
預設為取消選取。

### 頁面功能 {#page-function}

頁面功能會新增空白頁面至社群網站，並附加至社群網站的功能：登入、功能表、通知、訊息、主題設定和品牌推廣。 使用將內容新增到頁面 [標準AEM編寫模式](/help/sites-authoring/editing-content.md).

將新增到範本時，唯一的設定是 [標題和URL設定](#title-and-url-settings).

### QnA 功能 {#qna-function}

QnA函式是具有 [QnA元件](/help/communities/working-with-qna.md) 針對標籤、檔案上傳、追蹤、成員自我編輯、投票和稽核進行設定。

新增至範本時，此設定允許對有特殊許可權的成員進行限制：

![qna-dialog](assets/qna-dialog.png)

* [標題和URL設定](#title-and-url-settings)

* **允許釘選**

  如果選取，論壇允許將主題回覆釘選到評論清單的開頭。 預設為已選取。

* **允許有特殊許可權的成員**

  如果選取，QnA論壇僅允許有特殊許可權的成員透過選擇 [有特殊許可權的成員群組](/help/communities/users.md#privileged-members-group). 如果未選取，則允許所有社群成員張貼。 預設為取消選取。

* **允許檔案上傳**

  如果選取，QnA論壇則包含成員上傳檔案的功能。 預設為已選取。

* **允許執行緒式回覆**

  如果未選取，QnA論壇允許對張貼的問題進行評論（回答），但不允許對回答進行回覆。 預設為已選取。

* **允許主要內容**

  如果選取，則會將其內容識別為 [主要內容](/help/communities/featured.md). 預設為已選取。

## 建立社群功能 {#create-community-function}

選取以下專案即可建立社群功能 `Create Community Function` 圖示位於社群功能主控台頂端。 您可以根據相同AEM Blueprint建立多個函式，然後透過在作者編輯模式下開啟以唯一自訂。

![create-community-function](assets/create-community-function.png)

### 社群功能名稱 {#community-function-name}

![function-name](assets/function-name.png)

在「社群功能名稱」面板上，會設定名稱、說明，以及功能是啟用還是停用：

* **社群功能名稱**

  用於顯示和儲存的函式名稱。

* **社群功能說明**

  顯示的函式說明。

* **已停用/已啟用**

  控制函式是否可參照的切換開關。

### AEM 藍圖 {#aem-blueprint}

![aem-blueprint](assets/aem-blueprint.png)

在 `AEM Blueprint` 面板中，可選取作為社群功能基礎實作的Blueprint。

社群功能是一個迷你網站，包含一或多個頁面，預先有線以納入社群網站，包括登入、使用者設定檔、通知、訊息、網站功能表、搜尋、主題設定和品牌功能。 建立函式後，您就可以 [開啟函式](#open-community-function) 在作者編輯模式中並自訂頁面或元件設定。

由於社群功能是以 [即時副本](/help/sites-administering/msm.md#live-copies) 的 [Blueprint](/help/sites-administering/msm-livecopy.md#creatingablueprint)，因此您可以轉出對函式所做的變更，這些變更會影響從 [社群網站範本](/help/communities/sites.md) 或 [社群群組範本](/help/communities/tools-groups.md) 其中包含函式。 也可以解除頁面與其父Blueprint的關聯，以進行頁面層級修改。

另請參閱 [多站點管理員](/help/sites-administering/msm.md).

### 縮圖 {#thumbnail}

![函式 — 縮圖](assets/funtion-thumbnail.png)

在「縮圖」面板上，可上傳影像以顯示在 [社群功能主控台](#community-functions-console).

## 開啟社群功能 {#open-community-function}

![開啟函式](assets/open-function.png)

選取 `Open Community Function` 圖示可進入作者編輯模式，以便編寫頁面內容及修改功能元件的設定。

### 設定元件 {#configuring-components}

社群功能會實作為AEM Blueprint的即時副本，其詳細資訊記錄於 [多站點管理員](/help/sites-administering/msm.md).

您不僅可以製作頁面內容，也可以設定元件。

若在建立的社群網站頁面上設定元件，則可能需要取消 [繼承](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) 以設定元件。 組態完成後，應重新建立繼承。

如需設定詳細資訊，請造訪 [Communities元件](/help/communities/author-communities.md) 適用於作者。

## 編輯社群功能 {#edit-community-function}

![edit-function](assets/edit-function.png)

選取 `Edit Community Function` 圖示可使用與相同的面板編輯函式的屬性 [建立社群功能](#create-community-function)，包括啟用或停用函式。
