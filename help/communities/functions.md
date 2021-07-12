---
title: 社群功能
seo-title: 社群功能
description: 了解如何存取社群功能主控台
seo-description: 了解如何存取社群功能主控台
uuid: d3d70134-f318-4709-a673-b01a3467d980
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 91833914-b811-4355-a97d-e1a9cb7441f1
docset: aem65
role: Admin
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2458'
ht-degree: 6%

---


# 社群功能{#community-functions}

社群體驗預期的功能類型眾所周知。 社群功能可作為社群功能使用。 基本上，這些頁面是預先連線以實作社群功能的一或多個頁面，而這項功能不僅需要以製作模式將元件新增至頁面。 它們是用來定義[社群網站範本](/help/communities/sites.md)的結構的建置塊，從中建立社群網站[](/help/communities/sites-console.md)。

建立社群網站後，可使用標準[AEM製作模式](/help/sites-authoring/editing-content.md)將內容新增至產生的頁面。 如社群功能主控台所示，提供各種社群功能。

>[!NOTE]
>
>建立[社群網站](/help/communities/sites-console.md)、[社群網站範本](/help/communities/sites.md)、[社群群組範本](/help/communities/tools-groups.md)和[社群功能](/help/communities/functions.md)的主控台僅用於製作環境。

## 社區功能控制台 {#community-functions-console}

若要進入製作環境中的社群功能主控台：

* 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 社群]** > **[!UICONTROL 社群函式]**。

![社群功能](assets/community-functions.png)

## 預先建立的函式 {#pre-built-functions}

以下是隨AEM Communities提供的功能簡要說明。 每個函式都包括一個或多個AEM頁面，其中包含連接到功能中的Communities元件，該功能可輕鬆整合到[社區站點模板](/help/communities/sites.md)中。

社群網站範本提供社群網站的結構，包括登入、使用者設定檔、通知、傳訊、網站功能表、搜尋、貼圖和品牌推廣功能。

### 標題和URL設定 {#title-and-url-settings}

**** 標題和 **** URL是所有社群函式通用的屬性。

當[修改](/help/communities/sites-console.md#modifying-site-properties)社區站點結構時，將社區函式添加到社區站點模板或添加社區函式時，將開啟該函式的對話框，以便可以配置標題和URL。

#### 設定功能詳細資料 {#configuration-function-details}

![title-url-details](assets/title-url-details.png)

* **標題**

   （*必要*）網站功能表中顯示的文字

* **URL**

   （*必要*）用於生成URI的名稱。 名稱必須符合AEM和JCR所強加的[命名慣例](/help/sites-developing/naming-conventions.md)。

例如，使用在[快速入門](/help/communities/getting-started.md)教學課程之後建立的網站，如果

* 標題=網頁
* URL =頁面

然後，頁面的URL為https://localhost:4503/content/sites/engage/en/page.html

頁面的功能表連結顯示為：

![參與頁面](assets/engage-page.png)

### 活動資料流功能 {#activity-stream-function}

活動流函式是具有[活動流元件](/help/communities/activities.md)的頁面，其中已選擇所有視圖（所有活動、用戶活動和以下）。 另請參閱開發人員適用的[Activity Stream Essentials](/help/communities/essentials-activities.md) 。

將新增至範本時，會開啟下列對話方塊：

#### 設定功能詳細資料 {#configuration-function-details-1}

![函式詳細資料](assets/function-details.png)

* [標題和URL設定](#title-and-url-settings)

* **顯示「我的活動」檢視**

   如果選中，「活動」頁面將包含一個頁簽，該頁簽將根據當前成員在社區內生成的活動來篩選活動。 已選取預設值。

* **顯示「所有活動」檢視**

   如果選中，「活動」頁面將包含一個頁簽，該頁簽包含當前成員有權訪問的社區內生成的所有活動。 已選取預設值。

* **顯示「新聞資訊源」檢視**

   如果選中，「活動」頁包含一個頁簽，該頁簽根據當前成員正在跟蹤的活動篩選活動。 已選取預設值。

### 指定任務功能 {#assignments-function}

工作總攬函式是定義[社區站點以啟用](/help/communities/overview.md#enablement-community)的基本功能。 它可為社群成員指派啟用資源。 另請參閱開發人員的[Assignments Essentials](/help/communities/essentials-assignments.md)。

此函式是[啟用附加元件](/help/communities/enablement.md)的功能。 啟用附加元件需要額外的授權才能在生產環境中使用。

新增至範本時，唯一的設定是[標題和URL設定](#title-and-url-settings)。

### 部落格功能 {#blog-function}

部落格函式是一個具有[部落格元件](/help/communities/blog-feature.md)的頁面，該元件用於標籤、檔案上傳、跟蹤、成員自我編輯、投票和調節。 另請參閱開發人員適用的[部落格要點](/help/communities/blog-developer-basics.md) 。

將新增至範本時，會開啟下列對話方塊：

![部落格元件](assets/blog-component.png)

* [標題和URL設定](#title-and-url-settings)

* **允許有特殊權限的成員**

   如果選中，則部落格僅允許特權成員通過允許選擇[特權成員組](/help/communities/users.md#privileged-members-group)來建立文章。 如果未選擇，則允許所有社區成員建立。 已取消選取預設值。

* **允許檔案上傳**

   如果選取，部落格將包含成員上傳檔案的功能。 已選取預設值。

* **允許執行緒式回覆**

   如果未選取，部落格會允許對文章的回覆（留言），但是不允許對留言的回覆。 已選取預設值。

* **允許主要內容**

   若已選取，則會將部落格識別為[精選內容](/help/communities/featured.md)。 已選取預設值。

### 日曆功能 {#calendar-function}

日曆函式是一個具有[日曆元件](/help/communities/calendar.md)的頁面，該元件配置為允許進行標籤。 對於開發人員，另請參閱[Calendar Essentials](/help/communities/calendar-basics-for-developers.md)。

將新增至範本時，會開啟下列對話方塊：

![日曆 — 詳細資訊](assets/calendar-details.png)

* [標題和URL設定](#title-and-url-settings)

* **允許釘選**

   如果選中，論壇允許將主題回覆固定到評論清單的開頭。 已選取預設值。

* **允許有特殊權限的成員**

   如果選中，則部落格僅允許特權成員通過允許選擇[特權成員組](/help/communities/users.md#privileged-members-group)來建立文章。 如果未選擇，則允許所有社區成員建立。 已取消選取預設值。

* **允許檔案上傳**

   如果選取，部落格將包含成員上傳檔案的功能。 已選取預設值。

* **允許執行緒式回覆**

   如果未選取，部落格會允許對文章的回覆（留言），但是不允許對留言的回覆。 已選取預設值。

* **允許主要內容**

   如果選取，則其內容識別為[精選內容](/help/communities/featured.md)。 已選取預設值。

### 目錄功能 {#catalog-function}

目錄函式使[啟用社區](/help/communities/overview.md#enablement-community)成員能夠瀏覽未分配給他們的啟用資源。 開發人員請參閱[標籤啟用資源](/help/communities/tag-resources.md)和[目錄要點](/help/communities/catalog-developer-essentials.md)。

如果社群網站的屬性` [Show in Catalog](/help/communities/resources.md)`設為true，所有目錄中都會顯示其所有啟用資源和學習路徑。 若要明確包含資源和學習路徑，必須將[pre-filter](/help/communities/catalog-developer-essentials.md#pre-filters)套用至目錄。

新增至範本時，設定可指定用於設定向網站訪客呈現的標籤篩選器的標籤命名空間：

![目錄函式](assets/catalog-function.png)

* [標題和URL設定](#title-and-url-settings)

* **選取所有命名空間**

   選取的標籤命名空間會定義訪客可選取的標籤，以篩選目錄中所列的啟用資源清單。
如果選取，則社群網站允許的所有標籤命名空間都可用。
如果取消選取，則可以選取社群網站允許的一或多個命名空間。
已選取預設值。

### 精選內容功能 {#featured-content-function}

精選內容函式是一個頁面，其中[精選內容元件](/help/communities/featured.md)設定為允許新增及刪除註解。

每個元件可允許或禁止功能內容（請參閱[部落格函式](#blog-function)、[日曆函式](#calendar-function)、[論壇函式](#forum-function)、[標識函式](#ideation-function)和[QnA函式](#qna-function)）。

新增至範本時，唯一的設定是[標題和URL設定](#title-and-url-settings)。

### 檔案庫功能 {#file-library-function}

檔案庫函式是一個頁，其[檔案庫元件](/help/communities/file-library.md)被配置為允許添加和刪除注釋。

新增至範本時，唯一的設定是[標題和URL設定](#title-and-url-settings)。

### 論壇功能 {#forum-function}

論壇函式是一個具有[論壇元件](/help/communities/forum.md)的頁面，該元件用於標籤、檔案上載、跟蹤、成員自我編輯、投票和調節。

將新增至範本時，會開啟下列對話方塊：

#### 設定功能詳細資料 {#configuration-function-details-2}

![forum-component1](assets/forum-component1.png)

* [標題和URL設定](#title-and-url-settings)

* **允許釘選**

   如果選中，論壇允許將主題回覆固定到評論清單的開頭。 已選取預設值。

* **允許有特殊權限的成員**

   如果選中，則論壇僅允許特權成員通過允許選擇[特權成員組](/help/communities/users.md#privileged-members-group)來發佈主題。 如果未選取，則允許所有社群成員張貼。 已取消選取預設值。

* **允許檔案上傳**

   如果選中，論壇將包括成員上傳檔案的功能。 已選取預設值。

* **允許執行緒式回覆**

   如果未選中，論壇將允許對某個主題進行評論，但不允許對這些評論進行回復。 已選取預設值。

* **允許主要內容**

   如果選取，則元件的內容被識別為[精選內容](/help/communities/featured.md)。 已選取預設值。

### 組函式 {#groups-function}

>[!CAUTION]
>
>群組函式必須&#x200B;*不*&#x200B;是網站結構或社群網站範本中的&#x200B;*第一個或唯一的*&#x200B;函式。
>
>必須先包含並列出任何其他函式，例如[page函式](#page-function)。

群組功能可讓社群成員在發佈環境的社群網站內建立子社群。

根據[settings](/help/communities/sites-console.md#groupmanagement)，當「組」函式包含在[社區站點模板](/help/communities/sites.md)中時，這些組可以是公用或專用組，並且一個或多個社區組模板可配置為在實際建立社區組時（例如從發佈環境）提供模板的選擇。 [社區組模板](/help/communities/tools-groups.md)指定為組頁面（如論壇和日曆）建立的社區功能。

建立社區組時，會為新組動態建立成員組，可將成員分配或加入到新組。 如需詳細資訊，請參閱[管理使用者和使用者群組](/help/communities/users.md)。

自Communities [Feature Pack 1](/help/communities/deploy-communities.md#latestfeaturepack)起，社群群組是使用[Communities網站的群組主控台](/help/communities/groups.md)在製作環境中建立，且可於啟用時在發佈環境中建立。

將新增至範本時，會開啟下列對話方塊：

![group-template-config](assets/group-template-config.png)

* [標題和URL設定](#title-and-url-settings)

* **選取群組範本**

   一個下拉式清單，可供選取一或多個已啟用的群組範本，新社群群組的未來建立者（在發佈環境中）可從中選擇。

* **允許有特殊權限的成員**

   如果選中，則論壇僅允許特權成員通過允許選擇[特權成員安全組](/help/communities/users.md#privileged-members-group)來發佈主題。 如果未選取，則允許所有社群成員張貼。 已取消選取預設值。

* **允許發佈建立**

   如果選取，獲授權的社群成員可以在發佈環境中建立群組。 如果取消選取，則只能從Communities網站的群組控制台在製作環境中建立新群組（子社群）。
已選取預設值。

### 創意力功能 {#ideation-function}

標識函式是一個包含[標識元件](/help/communities/ideation-feature.md)的頁。

將其添加到模板時，將開啟以下對話框，該對話框指定預設的標題和URL名稱以及模板的預設顯示設定：

![識別函式](assets/ideation-function.png)

* [標題和URL設定](#title-and-url-settings)

* **允許有特殊權限的成員**

   如果選中，則論壇僅允許特權成員通過允許選擇[特權成員安全組](/help/communities/users.md#privileged-members-group)來發佈主題。 如果未選取，則允許所有社群成員張貼。 已取消選取預設值。

* **允許檔案上傳**

   如果選中，則構想包括成員上載檔案的功能。 已選取預設值。

* **允許執行緒式回覆**

   如果未選取，則建議允許對主題的回覆（留言），但不允許對留言的回覆。 已選取預設值。

* **允許主要內容**

   如果選取，則其內容識別為[精選內容](/help/communities/featured.md)。 已選取預設值。

### 排行榜功能 {#leaderboard-function}

排行榜功能是一個[排行榜元件](/help/communities/enabling-leaderboard.md)的頁面。

**注意**:從社區模板建立社區站點 ** 後，該社區站點需要進一步配置，該模板包括了該社區模板的排行榜功能。指定排行榜元件的[rules](/help/communities/enabling-leaderboard.md#rules-tab)，這取決於社區站點的[評分和徽章](/help/communities/implementing-scoring.md)的配置。

將其添加到模板時，將開啟以下對話框，該對話框指定預設的標題和URL名稱以及模板的預設顯示設定：

![排行榜對話](assets/leaderboard-dialog.png)

* [標題和URL設定](#title-and-url-settings)

* **顯示徽章**

   如果選中，則排行榜中會包含徽章表徵圖的列。
已取消選取預設值。

* **顯示徽章名稱**

   如果選中，則排行榜中將包含徽章名稱的列。
已取消選取預設值。

* **顯示頭像**

   如果選中，成員的頭像影像將包含在排行榜中，位於其成員配置檔案的名稱連結旁。
已取消選取預設值。

### 頁面功能 {#page-function}

頁面函式會在社群網站中新增一個空白頁面，將其連線至社群網站的功能：登入、功能表、通知、傳訊、主題和品牌推廣。 使用[標準AEM製作模式](/help/sites-authoring/editing-content.md)將內容新增至頁面。

新增至範本時，唯一的設定是[標題和URL設定](#title-and-url-settings)。

### QnA 功能 {#qna-function}

QnA函式是一個具有[QnA元件](/help/communities/working-with-qna.md)的頁，該元件用於標籤、檔案上載、跟蹤、成員以自我編輯、投票和調節。

將新增至範本時，設定會允許限制有權限的成員：

![qna-dialog](assets/qna-dialog.png)

* [標題和URL設定](#title-and-url-settings)

* **允許釘選**

   如果選中，論壇允許將主題回覆固定到評論清單的開頭。 已選取預設值。

* **允許有特殊權限的成員**

   如果選中，則QnA論壇僅允許特權成員通過允許選擇[特權成員組](/help/communities/users.md#privileged-members-group)來發佈問題。 如果未選取，則允許所有社群成員張貼。 已取消選取預設值。

* **允許檔案上傳**

   如果選中，QnA論壇將包括成員上載檔案的功能。 已選取預設值。

* **允許執行緒式回覆**

   如果未選擇，則QnA論壇允許對已發佈的問題進行評論（回答），但不允許對答案進行答復。 已選取預設值。

* **允許主要內容**

   如果選取，則其內容識別為[精選內容](/help/communities/featured.md)。 已選取預設值。

## 建立社群功能 {#create-community-function}

通過選擇位於「社區功能」控制台頂部的`Create Community Function`表徵圖，可以建立社區功能。 您可以建立以相同AEM Blueprint為基礎的多個函式，然後在製作編輯模式中開啟，以唯一自訂。

![create-community-function](assets/create-community-function.png)

### 社群功能名稱 {#community-function-name}

![function-name](assets/function-name.png)

在「社區函式名稱」面板中，將配置名稱、說明以及函式是啟用還是禁用：

* **社群功能名稱**

   用於顯示和儲存的函式名稱。

* **社群功能說明**

   顯示的函式說明。

* **禁用/啟用**

   控制函式是否可參考的切換開關。

### AEM 藍圖 {#aem-blueprint}

![aem-blueprint](assets/aem-blueprint.png)

在`AEM Blueprint`面板上，可以選取作為社群函式基礎實作的Blueprint。

社群功能是一個迷你網站，包含一或多個頁面，並預先連線以納入社群網站，包括登入、使用者設定檔、通知、傳訊、網站功能表、搜尋、貼圖和品牌功能。 建立函式後，您就可以[在作者編輯模式中開啟函式](#open-community-function)，並自訂頁面或元件設定。

由於社群函式被實作為[blueprint](/help/sites-administering/msm-livecopy.md#creatingablueprint)的[即時副本](/help/sites-administering/msm.md#live-copies)，因此可以轉出對函式所做的更改，該更改影響從[社區站點模板](/help/communities/sites.md)或[社區組模板](/help/communities/tools-groups.md)建立的所有社區站點頁，該模板包括該函式。 您也可以將頁面與其上層Blueprint取消關聯，以進行頁面層級的修改。

另請參閱[多站點管理器](/help/sites-administering/msm.md)。

### 縮圖 {#thumbnail}

![函式縮圖](assets/funtion-thumbnail.png)

在「縮圖」面板上，可以上傳影像以顯示在[社群功能控制台](#community-functions-console)中。

## 開啟社群功能 {#open-community-function}

![open-function](assets/open-function.png)

選取`Open Community Function`圖示，以進入作者編輯模式，以編寫頁面內容及修改功能元件的設定。

### 配置元件 {#configuring-components}

社群函式以AEM Blueprint的即時副本的形式實施，其詳細資訊記錄在[Multi Site Manager](/help/sites-administering/msm.md)下。

不僅可製作頁面內容，也可設定元件。

如果在已建立的社區站點的頁面上配置元件，則可能需要取消[繼承](/help/sites-administering/msm-livecopy.md#changing-live-copy-content)來配置元件。 完成設定時，應重新建立繼承。

如需設定詳細資訊，請造訪作者的[Communities元件](/help/communities/author-communities.md)。

## 編輯社群功能 {#edit-community-function}

![編輯函式](assets/edit-function.png)

選取`Edit Community Function`圖示，使用與[建立社群函式](#create-community-function)相同的面板來編輯函式的屬性，包括啟用或停用函式。
