---
title: 社群功能
seo-title: Community Functions
description: 了解如何存取社群功能主控台
seo-description: Learn how to access the Community Functions console
uuid: d3d70134-f318-4709-a673-b01a3467d980
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 91833914-b811-4355-a97d-e1a9cb7441f1
docset: aem65
role: Admin
exl-id: 2395c895-c611-43ac-abb6-c2bc4b4a41f4
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '2448'
ht-degree: 6%

---

# 社群功能{#community-functions}

社群體驗預期的功能類型眾所周知。 社群功能可作為社群功能使用。 基本上，這些頁面是預先連線以實作社群功能的一或多個頁面，而這項功能不僅需要以製作模式將元件新增至頁面。 這些是用來定義 [社群網站範本](/help/communities/sites.md) 從哪些社區站點 [已建立](/help/communities/sites-console.md).

建立社群網站後，即可使用標準將內容新增至產生的頁面 [AEM製作模式](/help/sites-authoring/editing-content.md). 如社群功能主控台所示，提供各種社群功能。

>[!NOTE]
>
>建立 [社群網站](/help/communities/sites-console.md), [社群網站範本](/help/communities/sites.md), [社群群組範本](/help/communities/tools-groups.md)，和 [社群功能](/help/communities/functions.md) 僅供製作環境使用。

## 社區功能控制台 {#community-functions-console}

若要進入製作環境中的社群功能主控台：

* 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 社群]** > **[!UICONTROL 社群功能]**.

![社群功能](assets/community-functions.png)

## 預先建立的函式 {#pre-built-functions}

以下是隨AEM Communities提供的功能簡要說明。 每個函式都包含一或多個AEM頁面，其中包含連線在一起的功能中的Communities元件，這些元件可輕鬆整合至 [社群網站範本](/help/communities/sites.md).

社群網站範本提供社群網站的結構，包括登入、使用者設定檔、通知、傳訊、網站功能表、搜尋、貼圖和品牌推廣功能。

### 標題和URL設定 {#title-and-url-settings}

**標題** 和 **URL** 是所有社群函式的共同屬性。

當社群功能新增至社群網站範本，或在 [修改](/help/communities/sites-console.md#modifying-site-properties) 社群網站的結構中，會開啟函式的對話方塊，以便設定標題和URL。

#### 設定功能詳細資料 {#configuration-function-details}

![title-url-details](assets/title-url-details.png)

* **標題**

   (*必填*)顯示在網站功能選單中的文字

* **URL**

   (*必填*)用於生成URI的名稱。 名稱必須符合 [命名慣例](/help/sites-developing/naming-conventions.md) 由AEM和JCR強加。

例如，使用從以下項目建立的網站： [快速入門](/help/communities/getting-started.md) 教學課程，如果

* 標題=網頁
* URL =頁面

然後，頁面的URL為https://localhost:4503/content/sites/engage/en/page.html

頁面的功能表連結顯示為：

![參與頁面](assets/engage-page.png)

### 活動資料流功能 {#activity-stream-function}

活動資料流函式是具有 [活動資料流元件](/help/communities/activities.md) 已選取所有檢視（所有活動、使用者活動及後續）。 另請參閱 [活動資料流要點](/help/communities/essentials-activities.md) 供開發人員使用。

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

指配函式是定義 [啟用社群網站](/help/communities/overview.md#enablement-community). 它可為社群成員指派啟用資源。 另請參閱 [工作總攬](/help/communities/essentials-assignments.md) 供開發人員使用。

此函式是 [啟用附加元件](/help/communities/enablement.md). 啟用附加元件需要額外的授權才能在生產環境中使用。

新增至範本時，唯一的設定是 [標題和URL設定](#title-and-url-settings).

### 部落格功能 {#blog-function}

部落格功能是具有 [部落格元件](/help/communities/blog-feature.md) 已配置，用於標籤、檔案上傳、跟蹤、成員自我編輯、投票和協調。 另請參閱 [部落格要點](/help/communities/blog-developer-basics.md) 供開發人員使用。

將新增至範本時，會開啟下列對話方塊：

![部落格元件](assets/blog-component.png)

* [標題和URL設定](#title-and-url-settings)

* **允許有特殊權限的成員**

   如果選取，部落格只會允許有權限的成員透過允許選取 [特權成員組](/help/communities/users.md#privileged-members-group). 如果未選擇，則允許所有社區成員建立。 已取消選取預設值。

* **允許檔案上傳**

   如果選取，部落格將包含成員上傳檔案的功能。 已選取預設值。

* **允許執行緒式回覆**

   如果未選取，部落格會允許對文章的回覆（留言），但是不允許對留言的回覆。 已選取預設值。

* **允許主要內容**

   如果選取，則會將部落格識別為 [精選內容](/help/communities/featured.md). 已選取預設值。

### 日曆功能 {#calendar-function}

日曆函式是具有 [日曆元件](/help/communities/calendar.md) 配置為允許標籤。 另請參閱 [日曆要點](/help/communities/calendar-basics-for-developers.md) 供開發人員使用。

將新增至範本時，會開啟下列對話方塊：

![日曆 — 詳細資訊](assets/calendar-details.png)

* [標題和URL設定](#title-and-url-settings)

* **允許釘選**

   如果選中，論壇允許將主題回覆固定到評論清單的開頭。 已選取預設值。

* **允許有特殊權限的成員**

   如果選取，部落格只會允許有權限的成員透過允許選取 [特權成員組](/help/communities/users.md#privileged-members-group). 如果未選擇，則允許所有社區成員建立。 已取消選取預設值。

* **允許檔案上傳**

   如果選取，部落格將包含成員上傳檔案的功能。 已選取預設值。

* **允許執行緒式回覆**

   如果未選取，部落格會允許對文章的回覆（留言），但是不允許對留言的回覆。 已選取預設值。

* **允許主要內容**

   如果選取，則會將其內容識別為 [精選內容](/help/communities/featured.md). 已選取預設值。

### 目錄功能 {#catalog-function}

目錄函式提供 [啟用社群](/help/communities/overview.md#enablement-community) 成員以瀏覽未分配給它們的啟用資源。 請參閱 [標籤啟用資源](/help/communities/tag-resources.md) 和 [目錄要點](/help/communities/catalog-developer-essentials.md) 供開發人員使用。

社群網站的所有啟用資源和學習路徑（如果屬性為，則顯示在所有目錄中） ` [Show in Catalog](/help/communities/resources.md)`，則會設為true。 若要明確包含資源和學習路徑，必須套用 [預先篩選](/help/communities/catalog-developer-essentials.md#pre-filters) 到目錄。

新增至範本時，設定可指定用於設定向網站訪客呈現的標籤篩選器的標籤命名空間：

![目錄函式](assets/catalog-function.png)

* [標題和URL設定](#title-and-url-settings)

* **選取所有命名空間**

   選取的標籤命名空間會定義訪客可選取的標籤，以篩選目錄中所列的啟用資源清單。
如果選取，則社群網站允許的所有標籤命名空間都可用。
如果取消選取，則可以選取社群網站允許的一或多個命名空間。
已選取預設值。

### 精選內容功能 {#featured-content-function}

精選內容功能是具有 [精選內容元件](/help/communities/featured.md) 配置為允許添加和刪除注釋。

每個元件可能允許或不允許使用特徵內容(請參閱 [部落格功能](#blog-function), [日曆功能](#calendar-function), [論壇功能](#forum-function), [標識函式](#ideation-function)，和 [QnA函式](#qna-function))。

新增至範本時，唯一的設定是 [標題和URL設定](#title-and-url-settings).

### 檔案庫功能 {#file-library-function}

檔案庫函式是具有 [檔案庫元件](/help/communities/file-library.md) 配置為允許添加和刪除注釋。

新增至範本時，唯一的設定是 [標題和URL設定](#title-and-url-settings).

### 論壇功能 {#forum-function}

論壇功能是具有 [論壇元件](/help/communities/forum.md) 已配置，用於標籤、檔案上傳、跟蹤、成員自我編輯、投票和協調。

將新增至範本時，會開啟下列對話方塊：

#### 設定功能詳細資料 {#configuration-function-details-2}

![forum-component1](assets/forum-component1.png)

* [標題和URL設定](#title-and-url-settings)

* **允許釘選**

   如果選中，論壇允許將主題回覆固定到評論清單的開頭。 已選取預設值。

* **允許有特殊權限的成員**

   如果選取，論壇僅允許有權限的成員通過允許選擇 [特權成員組](/help/communities/users.md#privileged-members-group). 如果未選取，則允許所有社群成員張貼。 已取消選取預設值。

* **允許檔案上傳**

   如果選中，論壇將包括成員上傳檔案的功能。 已選取預設值。

* **允許執行緒式回覆**

   如果未選中，論壇將允許對某個主題進行評論，但不允許對這些評論進行回復。 已選取預設值。

* **允許主要內容**

   如果選取此選項，元件的內容會識別為 [精選內容](/help/communities/featured.md). 已選取預設值。

### 組函式 {#groups-function}

>[!CAUTION]
>
>組函式必須 *not* be *第一，也不是唯一* 功能（在網站結構中或社群網站範本中）。
>
>任何其他函式，例如 [頁面函式](#page-function)，必須包含在內並列出。

群組功能可讓社群成員在發佈環境的社群網站內建立子社群。

視 [設定](/help/communities/sites-console.md#groupmanagement) 當群組函式包含在 [社群網站範本](/help/communities/sites.md)，群組可以是公開或私人的，且一或多個社群群組範本可設定為在實際建立社群群組時（例如從發佈環境）提供範本選擇。 A [社群群組範本](/help/communities/tools-groups.md) 指定為組頁面（如論壇和日曆）建立的Communities功能。

建立社區組時，會為新組動態建立成員組，可將成員分配或加入到新組。 如需詳細資訊，請參閱 [管理使用者和使用者群組](/help/communities/users.md).

As of Communities [功能包1](/help/communities/deploy-communities.md#latestfeaturepack)，社群群組會使用 [Communities站點的組控制台](/help/communities/groups.md)、和時，可在啟用後於發佈環境中建立。

將新增至範本時，會開啟下列對話方塊：

![group-template-config](assets/group-template-config.png)

* [標題和URL設定](#title-and-url-settings)

* **選取群組範本**

   一個下拉式清單，可供選取一或多個已啟用的群組範本，新社群群組的未來建立者（在發佈環境中）可從中選擇。

* **允許有特殊權限的成員**

   如果選取，論壇僅允許有權限的成員通過允許選擇 [特權成員安全組](/help/communities/users.md#privileged-members-group). 如果未選取，則允許所有社群成員張貼。 已取消選取預設值。

* **允許發佈建立**

   如果選取，獲授權的社群成員可以在發佈環境中建立群組。 如果取消選取，則只能從Communities網站的群組控制台在製作環境中建立新群組（子社群）。
已選取預設值。

### 創意力功能 {#ideation-function}

識別函式是含有 [識別元件](/help/communities/ideation-feature.md).

將其添加到模板時，將開啟以下對話框，該對話框指定預設的標題和URL名稱以及模板的預設顯示設定：

![識別函式](assets/ideation-function.png)

* [標題和URL設定](#title-and-url-settings)

* **允許有特殊權限的成員**

   如果選取，論壇僅允許有權限的成員通過允許選擇 [特權成員安全組](/help/communities/users.md#privileged-members-group). 如果未選取，則允許所有社群成員張貼。 已取消選取預設值。

* **允許檔案上傳**

   如果選中，則構想包括成員上載檔案的功能。 已選取預設值。

* **允許執行緒式回覆**

   如果未選取，則建議允許對主題的回覆（留言），但不允許對留言的回覆。 已選取預設值。

* **允許主要內容**

   如果選取，則會將其內容識別為 [精選內容](/help/communities/featured.md). 已選取預設值。

### 排行榜功能 {#leaderboard-function}

排行榜功能是包含1的頁面 [排行榜元件](/help/communities/enabling-leaderboard.md).

**注意**:排行榜部分需要進一步配置 *after* 從包含「排行榜」功能的社區模板建立社區站點。 指定排行榜元件的 [規則](/help/communities/enabling-leaderboard.md#rules-tab)，取決於設定 [計分和徽章](/help/communities/implementing-scoring.md) 為社群網站。

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

頁面函式會在社群網站中新增一個空白頁面，將其連線至社群網站的功能：登入、功能表、通知、傳訊、主題和品牌推廣。 內容會使用 [標準AEM製作模式](/help/sites-authoring/editing-content.md).

新增至範本時，唯一的設定是 [標題和URL設定](#title-and-url-settings).

### QnA 功能 {#qna-function}

QnA函式是具有 [QnA元件](/help/communities/working-with-qna.md) 已配置，用於標籤、檔案上傳、跟蹤、成員自我編輯、投票和協調。

將新增至範本時，設定會允許限制有權限的成員：

![qna-dialog](assets/qna-dialog.png)

* [標題和URL設定](#title-and-url-settings)

* **允許釘選**

   如果選中，論壇允許將主題回覆固定到評論清單的開頭。 已選取預設值。

* **允許有特殊權限的成員**

   如果選中，則QnA論壇僅允許特權成員通過允許選擇 [特權成員組](/help/communities/users.md#privileged-members-group). 如果未選取，則允許所有社群成員張貼。 已取消選取預設值。

* **允許檔案上傳**

   如果選中，QnA論壇將包括成員上載檔案的功能。 已選取預設值。

* **允許執行緒式回覆**

   如果未選擇，則QnA論壇允許對已發佈的問題進行評論（回答），但不允許對答案進行答復。 已選取預設值。

* **允許主要內容**

   如果選取，則會將其內容識別為 [精選內容](/help/communities/featured.md). 已選取預設值。

## 建立社群功能 {#create-community-function}

選取 `Create Community Function` 表徵圖。 您可以建立以相同AEM Blueprint為基礎的多個函式，然後在製作編輯模式中開啟，以唯一自訂。

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

在 `AEM Blueprint` ，您可以選取作為社群功能基礎實作的blueprint。

社群功能是一個迷你網站，包含一或多個頁面，並預先連線以納入社群網站，包括登入、使用者設定檔、通知、傳訊、網站功能表、搜尋、貼圖和品牌功能。 建立函式後，即可 [開啟函式](#open-community-function) 在製作編輯模式中，並自訂頁面或元件設定。

由於社群功能是以 [即時副本](/help/sites-administering/msm.md#live-copies) a [Blueprint](/help/sites-administering/msm-livecopy.md#creatingablueprint)，則可轉出對函式所做的變更，而影響從 [社群網站範本](/help/communities/sites.md) 或 [社群群組範本](/help/communities/tools-groups.md) 包含函式。 您也可以將頁面與其上層Blueprint取消關聯，以進行頁面層級的修改。

另請參閱 [多網站管理員](/help/sites-administering/msm.md).

### 縮圖 {#thumbnail}

![函式縮圖](assets/funtion-thumbnail.png)

在縮圖面板上，可上傳影像以顯示在 [社群功能主控台](#community-functions-console).

## 開啟社群功能 {#open-community-function}

![open-function](assets/open-function.png)

選取 `Open Community Function` 圖示，以進入製作頁面內容和修改功能元件的設定的作者編輯模式。

### 配置元件 {#configuring-components}

社群函式是以AEM Blueprint的即時副本的形式實作，其詳細資訊記錄於 [多網站管理員](/help/sites-administering/msm.md).

不僅可製作頁面內容，也可設定元件。

如果在已建立的社群網站的頁面上設定元件，則可能需要取消 [繼承](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) 以設定元件。 完成設定時，應重新建立繼承。

如需設定詳細資訊，請造訪 [Communities元件](/help/communities/author-communities.md) 供作者使用。

## 編輯社群功能 {#edit-community-function}

![編輯函式](assets/edit-function.png)

選取 `Edit Community Function` 圖示，使用與 [建立社群功能](#create-community-function)，包括啟用或停用函式。
