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
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2215'
ht-degree: 2%

---

# 社群功能{#community-functions}

社群體驗中預期的功能型別眾所周知。 社群功能可作為社群功能使用。 基本上，這些頁面是預先接線的一或多個頁面，用於實作社群功能，該功能不僅需要以製作模式將元件新增至頁面。 這些是建置區塊，用來定義[社群網站範本](/help/communities/sites.md)的結構，社群網站是從這些範本[建立的](/help/communities/sites-console.md)。

建立社群網站後，可以使用標準[AEM編寫模式](/help/sites-authoring/editing-content.md)將內容新增到產生的頁面。 社群功能主控台提供各種社群功能。

>[!NOTE]
>
>建立[社群網站](/help/communities/sites-console.md)、[社群網站範本](/help/communities/sites.md)、[社群群組範本](/help/communities/tools-groups.md)及[社群功能](/help/communities/functions.md)的主控台僅供作者環境使用。

## 社群功能主控台 {#community-functions-console}

若要在製作環境中存取社群功能主控台：

* 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 社群]** > **[!UICONTROL 社群功能]**。

![社群功能](assets/community-functions.png)

## 預先建立的函式 {#pre-built-functions}

以下簡述AEM Communities所提供的功能。 每個功能都包含一或多個AEM頁面，其中包含以連線方式連線在一起的Communities元件，此功能可輕鬆整合至[社群網站範本](/help/communities/sites.md)。

社群網站範本提供社群網站的結構，包括登入、使用者設定檔、通知、訊息、網站功能表、搜尋、主題設定和品牌功能。

### 標題和URL設定 {#title-and-url-settings}

**標題**&#x200B;和&#x200B;**URL**&#x200B;是所有社群功能通用的屬性。

將社群功能新增至社群網站範本或在[修改](/help/communities/sites-console.md#modifying-site-properties)社群網站的結構時新增時，會開啟該功能的對話方塊，以便設定標題和URL。

#### 設定功能詳細資料 {#configuration-function-details}

![title-url-details](assets/title-url-details.png)

* **標題**

  （*必要*）網站功能表中出現的文字

* **URL**

  （*必要*）用來產生URI的名稱。 名稱必須符合AEM和JCR所強加的[命名慣例](/help/sites-developing/naming-conventions.md)。

例如，使用在[快速入門](/help/communities/getting-started.md)教學課程之後建立的網站，如果

* 標題=網頁
* URL =頁面

接著，頁面的URL會是https://localhost:4503/content/sites/engage/en/page.html

而頁面的功能表連結會顯示為：

![engage-page](assets/engage-page.png)

### 活動資料流功能 {#activity-stream-function}

活動資料流函式是具有[活動資料流元件](/help/communities/activities.md)且已選取所有檢視（所有活動、使用者活動及後續專案）的頁面。 另請參閱開發人員的[Activity Stream Essentials](/help/communities/essentials-activities.md)

新增至範本時，下列對話方塊隨即開啟：

#### 設定功能詳細資料 {#configuration-function-details-1}

![函式詳細資料](assets/function-details.png)

* [標題和URL設定](#title-and-url-settings)

* **顯示[我的活動]檢視**

  如果選取，「活動」頁面會包含索引標籤，該索引標籤會根據目前成員在社群內產生的活動來篩選活動。 預設為已選取。

* **顯示[所有活動]檢視**

  如果選取，「活動」頁面會包含標籤，其中包含社群內產生且目前成員有權存取的所有活動。 預設為已選取。

* **顯示[新聞摘要]檢視**

  如果選取，「活動」頁面會包含索引標籤，以根據目前成員所關注的活動來篩選活動。 預設為已選取。

### 部落格功能 {#blog-function}

部落格功能是具有[部落格元件](/help/communities/blog-feature.md)的頁面，其設定用於標籤、檔案上傳、追蹤、成員自我編輯、投票及稽核。 另請參閱開發人員的[部落格要點](/help/communities/blog-developer-basics.md)。

新增至範本時，下列對話方塊隨即開啟：

![部落格元件](assets/blog-component.png)

* [標題和URL設定](#title-and-url-settings)

* **允許有特殊許可權的成員**

  如果選取，部落格僅允許有特殊許可權的成員選取[有特殊許可權的成員群組](/help/communities/users.md#privileged-members-group)，以建立文章。 如果未選取，則允許建立所有社群成員。 預設為取消選取。

* **允許檔案上傳**

  如果選取，部落格會包含成員上傳檔案的功能。 預設為已選取。

* **允許執行緒式回覆**

  若未選取，部落格會允許回覆（評論）文章，但不允許回複評論。 預設為已選取。

* **允許主要內容**

  如果選取，部落格會識別為[精選內容](/help/communities/featured.md)。 預設為已選取。

### 日曆功能 {#calendar-function}

行事曆功能是具有[行事曆元件](/help/communities/calendar.md)設定為允許標籤的頁面。 另請參閱開發人員的[行事曆要點](/help/communities/calendar-basics-for-developers.md)。

新增至範本時，下列對話方塊隨即開啟：

![行事曆詳細資料](assets/calendar-details.png)

* [標題和URL設定](#title-and-url-settings)

* **允許釘選**

  如果選取，論壇允許將主題回覆釘選到評論清單的開頭。 預設為已選取。

* **允許有特殊許可權的成員**

  如果選取，部落格僅允許有特殊許可權的成員選取[有特殊許可權的成員群組](/help/communities/users.md#privileged-members-group)，以建立文章。 如果未選取，則允許建立所有社群成員。 預設為取消選取。

* **允許檔案上傳**

  如果選取，部落格會包含成員上傳檔案的功能。 預設為已選取。

* **允許執行緒式回覆**

  若未選取，部落格會允許回覆（評論）文章，但不允許回複評論。 預設為已選取。

* **允許主要內容**

  如果選取，其內容會識別為[精選內容](/help/communities/featured.md)。 預設為已選取。

### 主要內容功能 {#featured-content-function}

主要內容功能是具有[主要內容元件](/help/communities/featured.md)的頁面，設定為允許新增和刪除評論。

每個元件可允許或不允許具有功能內容的功能（請參閱[部落格功能](#blog-function)、[行事曆功能](#calendar-function)、[論壇功能](#forum-function)、[構思功能](#ideation-function)和[QnA功能](#qna-function)）。

新增至範本時，[標題和URL設定](#title-and-url-settings)的唯一設定。

### 檔案庫功能 {#file-library-function}

檔案庫函式是具有[檔案庫元件](/help/communities/file-library.md)的頁面，其設定為允許新增和刪除註解。

新增至範本時，[標題和URL設定](#title-and-url-settings)的唯一設定。

### 論壇功能 {#forum-function}

論壇功能是具有[論壇元件](/help/communities/forum.md)的頁面，該元件已設定為標籤、檔案上傳、追蹤、成員自我編輯、投票及稽核。

新增至範本時，下列對話方塊隨即開啟：

#### 設定功能詳細資料 {#configuration-function-details-2}

![論壇 — 元件1](assets/forum-component1.png)

* [標題和URL設定](#title-and-url-settings)

* **允許釘選**

  如果選取，論壇允許將主題回覆釘選到評論清單的開頭。 預設為已選取。

* **允許有特殊許可權的成員**

  如果選取，論壇僅允許有特殊許可權的成員透過選擇[有特殊許可權的成員群組](/help/communities/users.md#privileged-members-group)來張貼主題。 如果未選取，則允許所有社群成員張貼。 預設為取消選取。

* **允許檔案上傳**

  如果選取，論壇會包含成員上傳檔案的功能。 預設為已選取。

* **允許執行緒式回覆**

  如果未選取，論壇會允許對主題發表評論，但不允許回覆這些評論。 預設為已選取。

* **允許主要內容**

  如果選取，元件的內容會識別為[精選內容](/help/communities/featured.md)。 預設為已選取。

### 群組功能 {#groups-function}

>[!CAUTION]
>
>群組函式必須&#x200B;*不是*&#x200B;網站結構或社群網站範本中的&#x200B;*第一個，也不是唯一的*&#x200B;函式。
>
>必須包含其他任何函式，例如[頁面函式](#page-function)，並先列出。

群組功能可讓社群成員在發佈環境中的社群網站內建立子社群。

根據[設定](/help/communities/sites-console.md#groupmanagement)，當「群組」功能包含在[社群網站範本](/help/communities/sites.md)中時，群組可以是公用或私用，而一或多個社群群組範本可設定為在實際建立社群群組時提供範本選擇（例如從發佈環境）。 [社群群組範本](/help/communities/tools-groups.md)會指定為群組頁面建立的社群功能，例如論壇和行事曆。

建立社群群組時，會為新群組動態建立成員群組，成員可以指派或加入該群組。 如需詳細資訊，請參閱[管理使用者和使用者群組](/help/communities/users.md)。

截至Communities [Feature Pack 1](/help/communities/deploy-communities.md#latestfeaturepack)，社群群組是使用[Communities Sites的「群組」主控台](/help/communities/groups.md)在作者環境中建立，而且可在啟用時於發佈環境中建立。

新增至範本時，下列對話方塊隨即開啟：

![group-template-config](assets/group-template-config.png)

* [標題和URL設定](#title-and-url-settings)

* **選取群組範本**

  一個下拉式清單，可讓您選取一或多個已啟用的群組範本，新社群群組（在發佈環境中）的未來建立者可從中進行選擇。

* **允許有特殊許可權的成員**

  如果選取，則論壇僅允許有特殊許可權的成員透過選擇[有特殊許可權的成員安全性群組](/help/communities/users.md#privileged-members-group)來張貼主題。 如果未選取，則允許所有社群成員張貼。 預設為取消選取。

* **允許建立Publish**

  如果選取，獲授權的社群成員可以在發佈環境中建立群組。 如果取消選取，則只能從Communities Sites的「群組」主控台在作者環境中建立新群組（子社群）。
預設為已選取。

### 創意力功能 {#ideation-function}

創意力函式是具有一個[創意力元件](/help/communities/ideation-feature.md)的頁面。

新增至範本時，會開啟下列對話方塊，其中指定範本的預設「標題」和URL名稱，以及預設顯示設定：

![創意力函式](assets/ideation-function.png)

* [標題和URL設定](#title-and-url-settings)

* **允許有特殊許可權的成員**

  如果選取，則論壇僅允許有特殊許可權的成員透過選擇[有特殊許可權的成員安全性群組](/help/communities/users.md#privileged-members-group)來張貼主題。 如果未選取，則允許所有社群成員張貼。 預設為取消選取。

* **允許檔案上傳**

  如果選取，構思包括成員上傳檔案的能力。 預設為已選取。

* **允許執行緒式回覆**

  如果未選取，此創意允許主題回覆（註解），但不允許回覆註解。 預設為已選取。

* **允許主要內容**

  如果選取，其內容會識別為[精選內容](/help/communities/featured.md)。 預設為已選取。

### 排行榜功能 {#leaderboard-function}

排行榜功能是包含一個[排行榜元件](/help/communities/enabling-leaderboard.md)的頁面。

**注意**：排行榜元件在&#x200B;*之後*&#x200B;需要進一步的設定，才能從包含排行榜功能的社群範本建立社群網站。 指定排行榜元件的[規則](/help/communities/enabling-leaderboard.md#rules-tab)，這些規則取決於社群網站[評分和徽章](/help/communities/implementing-scoring.md)的設定。

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

頁面功能會新增空白頁面至社群網站，並附加至社群網站的功能：登入、功能表、通知、訊息、主題設定和品牌推廣。 內容已使用[標準AEM編寫模式](/help/sites-authoring/editing-content.md)新增至頁面。

新增至範本時，[標題和URL設定](#title-and-url-settings)的唯一設定。

### QnA 功能 {#qna-function}

QnA函式是具有[QnA元件](/help/communities/working-with-qna.md)的頁面，該元件已設定用於標籤、檔案上傳、追蹤、自我編輯、投票和稽核的成員。

新增至範本時，此設定允許對有特殊許可權的成員進行限制：

![qna-dialog](assets/qna-dialog.png)

* [標題和URL設定](#title-and-url-settings)

* **允許釘選**

  如果選取，論壇允許將主題回覆釘選到評論清單的開頭。 預設為已選取。

* **允許有特殊許可權的成員**

  如果選取，則QnA論壇只允許有特殊許可權的成員透過選擇[有特殊許可權的成員群組](/help/communities/users.md#privileged-members-group)來張貼問題。 如果未選取，則允許所有社群成員張貼。 預設為取消選取。

* **允許檔案上傳**

  如果選取，QnA論壇則包含成員上傳檔案的功能。 預設為已選取。

* **允許執行緒式回覆**

  如果未選取，QnA論壇允許對張貼的問題進行評論（回答），但不允許對回答進行回覆。 預設為已選取。

* **允許主要內容**

  如果選取，其內容會識別為[精選內容](/help/communities/featured.md)。 預設為已選取。

## 建立社群功能 {#create-community-function}

選取位於社群功能主控台頂端的`Create Community Function`圖示，即可建立社群功能。 您可以根據相同AEM Blueprint建立多個函式，然後透過在作者編輯模式下開啟以唯一自訂。

![create-community-function](assets/create-community-function.png)

### 社群功能名稱 {#community-function-name}

![function-name](assets/function-name.png)

在「社群功能名稱」面板上，會設定名稱、說明，以及功能是啟用還是停用：

* **社群功能名稱**

  用於顯示和儲存的函式名稱。

* **社群功能描述**

  顯示的函式說明。

* **已停用/已啟用**

  控制函式是否可參照的切換開關。

### AEM 藍圖 {#aem-blueprint}

![aem-blueprint](assets/aem-blueprint.png)

在`AEM Blueprint`面板上，可以選取作為社群功能基礎實作的Blueprint。

社群功能是一個迷你網站，包含一或多個頁面，預先有線以納入社群網站，包括登入、使用者設定檔、通知、訊息、網站功能表、搜尋、主題設定和品牌功能。 建立函式之後，就可以[在作者編輯模式中開啟函式](#open-community-function)，並自訂頁面或元件設定。

由於社群功能是以[Blueprint](/help/sites-administering/msm-livecopy.md#creatingablueprint)的[即時副本](/help/sites-administering/msm.md#live-copies)實作，因此可以轉出對功能所做的變更，該功能會影響從[社群網站範本](/help/communities/sites.md)或包含該功能的[社群群組範本](/help/communities/tools-groups.md)建立的所有社群網站頁面。 也可以解除頁面與其父Blueprint的關聯，以進行頁面層級修改。

另請參閱[多網站管理員](/help/sites-administering/msm.md)。

### 縮圖 {#thumbnail}

![功能縮圖](assets/funtion-thumbnail.png)

在「縮圖」面板上，可能會上傳影像以顯示在[社群功能主控台](#community-functions-console)中。

## 開啟社群功能 {#open-community-function}

![開啟函式](assets/open-function.png)

選取`Open Community Function`圖示以進入作者編輯模式，以便編寫頁面內容並修改功能元件的設定。

### 設定元件 {#configuring-components}

社群功能是以AEM Blueprint的即時副本實作，其詳細資訊記錄在[多網站管理員](/help/sites-administering/msm.md)下。

您不僅可以製作頁面內容，也可以設定元件。

如果在已建立的社群網站頁面上設定元件，則可能需要取消[繼承](/help/sites-administering/msm-livecopy.md#changing-live-copy-content)才能設定元件。 組態完成後，應重新建立繼承。

如需設定詳細資料，請造訪作者的[社群元件](/help/communities/author-communities.md)。

## 編輯社群功能 {#edit-community-function}

![edit-function](assets/edit-function.png)

選取`Edit Community Function`圖示以使用與[建立社群函式](#create-community-function)相同的面板來編輯函式的屬性，包括啟用或停用函式。
