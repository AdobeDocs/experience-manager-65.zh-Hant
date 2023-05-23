---
title: 社群功能
seo-title: Community Functions
description: 瞭解如何訪問社區功能控制台
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
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '2224'
ht-degree: 6%

---

# 社群功能{#community-functions}

社區體驗預期的功能類型眾所周知。 社區功能可作為社區功能提供。 實際上，它們是預先佈線的一個或多個頁面，以實現社區功能，該社區功能不僅要求以作者模式將元件添加到頁面。 它們是用於定義 [社區網站模板](/help/communities/sites.md) 從哪個社區站點 [建立](/help/communities/sites-console.md)。

一旦建立了社區網站，就可以使用標準將內容添加到生成的頁面 [AEM創作模式](/help/sites-authoring/editing-content.md)。 社區功能控制台中顯示了各種社區功能。

>[!NOTE]
>
>用於建立 [社區站點](/help/communities/sites-console.md)。 [社區網站模板](/help/communities/sites.md)。 [社區組模板](/help/communities/tools-groups.md), [社區功能](/help/communities/functions.md) 僅在作者環境中使用。

## 社區功能控制台 {#community-functions-console}

要在作者環境中訪問社區功能控制台：

* 導航到 **[!UICONTROL 工具]** > **[!UICONTROL 社區]** > **[!UICONTROL 社區功能]**。

![社區功能](assets/community-functions.png)

## 預構建的函式 {#pre-built-functions}

以下是與AEM Communities共同履行的職能的簡要說明。 每個功能包括一個或多個AEM頁面，這些頁面包含匯集在一起的社區元件，這些元件容易地結合到 [社區網站模板](/help/communities/sites.md)。

社區站點模板提供社區站點的結構，包括登錄、用戶配置檔案、通知、消息、站點菜單、搜索、主題和品牌特徵。

### 標題和URL設定 {#title-and-url-settings}

**標題** 和 **URL** 是所有社區函式的公用屬性。

將社區功能添加到社區網站模板或在 [修改](/help/communities/sites-console.md#modifying-site-properties) 在社區站點的結構中，將開啟函式對話框，以便可以配置標題和URL。

#### 設定功能詳細資料 {#configuration-function-details}

![標題 — url — 詳細資訊](assets/title-url-details.png)

* **標題**

   (*必需*)站點功能菜單中顯示的文本

* **URL**

   (*必需*)用於生成URI的名稱。 名稱必須符合 [命名約定](/help/sites-developing/naming-conventions.md) 和JCRAEM強加的。

例如，使用在 [入門](/help/communities/getting-started.md) 教程，如果

* 標題=網頁
* URL =頁

然後，該頁的URL為https://localhost:4503/content/sites/engage/en/page.html

頁面的菜單連結顯示為：

![「接觸」頁](assets/engage-page.png)

### 活動資料流功能 {#activity-stream-function}

活動流函式是包含 [活動流元件](/help/communities/activities.md) 已選擇所有視圖（所有活動、用戶活動和以下內容）。 另請參閱 [活動流軟體包](/help/communities/essentials-activities.md) 為開發人員準備。

添加到模板時，將開啟以下對話框：

#### 設定功能詳細資料 {#configuration-function-details-1}

![函式詳細資訊](assets/function-details.png)

* [標題和URL設定](#title-and-url-settings)

* **顯示「我的活動」檢視**

   如果選中，則「活動」頁將包含一個頁籤，該頁籤根據當前成員在社區中生成的活動篩選活動。 已選擇預設值。

* **顯示「所有活動」檢視**

   如果選中，則「活動」頁將包含一個頁籤，其中包含在當前成員有權訪問的社區中生成的所有活動。 已選擇預設值。

* **顯示「新聞資訊源」檢視**

   如果選中，則「活動」頁包含一個頁籤，該頁籤根據當前成員正在跟蹤的活動篩選活動。 已選擇預設值。

### 部落格功能 {#blog-function}

部落格功能是包含 [部落格元件](/help/communities/blog-feature.md) 配置為標籤、檔案上載、後續、成員自編、投票和審核。 另請參閱 [部落格要點](/help/communities/blog-developer-basics.md) 為開發人員準備。

添加到模板時，將開啟以下對話框：

![部落格元件](assets/blog-component.png)

* [標題和URL設定](#title-and-url-settings)

* **允許有特殊權限的成員**

   如果選中，則部落格僅允許特權成員通過允許選擇 [特權成員組](/help/communities/users.md#privileged-members-group)。 如果未選中，則允許建立所有社區成員。 取消選擇預設值。

* **允許檔案上傳**

   如果選中，則部落格包括成員上載檔案的功能。 已選擇預設值。

* **允許執行緒式回覆**

   如果未選中，部落格允許對文章的回復（注釋），但不允許對評論的回復。 已選擇預設值。

* **允許主要內容**

   如果選中，則將部落格標識為 [特色內容](/help/communities/featured.md)。 已選擇預設值。

### 日曆功能 {#calendar-function}

日曆函式是包含 [日曆元件](/help/communities/calendar.md) 配置為允許標籤。 另請參閱 [日曆要件](/help/communities/calendar-basics-for-developers.md) 為開發人員準備。

添加到模板時，將開啟以下對話框：

![日曆詳細資訊](assets/calendar-details.png)

* [標題和URL設定](#title-and-url-settings)

* **允許釘選**

   如果選中，論壇允許將主題答復固定到注釋清單的開頭。 已選擇預設值。

* **允許有特殊權限的成員**

   如果選中，則部落格僅允許特權成員通過允許選擇 [特權成員組](/help/communities/users.md#privileged-members-group)。 如果未選中，則允許建立所有社區成員。 取消選擇預設值。

* **允許檔案上傳**

   如果選中，則部落格包括成員上載檔案的功能。 已選擇預設值。

* **允許執行緒式回覆**

   如果未選中，部落格允許對文章的回復（注釋），但不允許對評論的回復。 已選擇預設值。

* **允許主要內容**

   如果選中，則其內容被標識為 [特色內容](/help/communities/featured.md)。 已選擇預設值。

### 特色內容功能 {#featured-content-function}

特色內容功能是包含 [特色內容元件](/help/communities/featured.md) 配置為允許添加和刪除注釋。

每個元件可能允許或不允許使用功能來提供內容(請參見 [部落格功能](#blog-function)。 [日曆函式](#calendar-function)。 [論壇功能](#forum-function)。 [標識函式](#ideation-function), [QnA函式](#qna-function))。

添加到模板時，唯一的配置是 [標題和URL設定](#title-and-url-settings)。

### 檔案庫功能 {#file-library-function}

檔案庫函式是包含 [檔案庫元件](/help/communities/file-library.md) 配置為允許添加和刪除注釋。

添加到模板時，唯一的配置是 [標題和URL設定](#title-and-url-settings)。

### 論壇功能 {#forum-function}

論壇功能是包含 [論壇元件](/help/communities/forum.md) 配置為標籤、檔案上載、後續、成員自編、投票和審核。

添加到模板時，將開啟以下對話框：

#### 設定功能詳細資料 {#configuration-function-details-2}

![forum-component1](assets/forum-component1.png)

* [標題和URL設定](#title-and-url-settings)

* **允許釘選**

   如果選中，論壇允許將主題答復固定到注釋清單的開頭。 已選擇預設值。

* **允許有特殊權限的成員**

   如果選中，則論壇僅允許特權成員通過允許選擇 [特權成員組](/help/communities/users.md#privileged-members-group)。 如果未選擇，則允許所有社區成員發佈。 取消選擇預設值。

* **允許檔案上傳**

   如果選中，論壇將包括成員上載檔案的功能。 已選擇預設值。

* **允許執行緒式回覆**

   如果未選擇，論壇允許對主題進行評論，但不允許對這些評論進行答復。 已選擇預設值。

* **允許主要內容**

   如果選中，則元件的內容將標識為 [特色內容](/help/communities/featured.md)。 已選擇預設值。

### 組函式 {#groups-function}

>[!CAUTION]
>
>組函式必須 *不* 是 *第一，也是唯一* 的子菜單。
>
>任何其他函式，如 [頁面函式](#page-function)，必須先包括並列出。

組功能使社區成員能夠在發佈環境中的社區站點內建立子社區。

取決於 [設定](/help/communities/sites-console.md#groupmanagement) 當「組」函式包含在 [社區網站模板](/help/communities/sites.md)，這些組可以是公共的或私有的，並且一個或多個社區組模板可配置為在實際建立社區組時（例如從發佈環境）提供模板選擇。 A [社區組模板](/help/communities/tools-groups.md) 指定為組頁面（如論壇和日曆）建立的社區功能。

建立社區組時，會為新組動態建立成員組，成員可以分配或加入到該組。 有關詳細資訊，請參見 [管理用戶和用戶組](/help/communities/users.md)。

截至社區 [功能包1](/help/communities/deploy-communities.md#latestfeaturepack)，使用 [社區站點組控制台](/help/communities/groups.md)，並且在啟用後可以在發佈環境中建立。

添加到模板時，將開啟以下對話框：

![組模板 — 配置](assets/group-template-config.png)

* [標題和URL設定](#title-and-url-settings)

* **選取群組範本**

   允許選擇一個或多個啟用的組模板的下拉清單，新社區組（在發佈環境中）的將來建立者可以從中選擇這些模板。

* **允許有特殊權限的成員**

   如果選中，則論壇僅允許特權成員通過允許選擇 [特權成員安全組](/help/communities/users.md#privileged-members-group)。 如果未選擇，則允許所有社區成員發佈。 取消選擇預設值。

* **允許發佈建立**

   如果選中，則授權的社區成員可以在發佈環境中建立組。 如果取消選擇，則只能在作者環境中從「社區站點的組」控制台建立新組（子社區）。
已選擇預設值。

### 創意力功能 {#ideation-function}

標識函式是包含 [識別元件](/help/communities/ideation-feature.md)。

添加到模板時，將開啟以下對話框，該對話框指定模板的預設標題和URL名稱以及預設顯示設定：

![理想函式](assets/ideation-function.png)

* [標題和URL設定](#title-and-url-settings)

* **允許有特殊權限的成員**

   如果選中，則論壇僅允許特權成員通過允許選擇 [特權成員安全組](/help/communities/users.md#privileged-members-group)。 如果未選擇，則允許所有社區成員發佈。 取消選擇預設值。

* **允許檔案上傳**

   如果選中，則該思想包括成員上載檔案的功能。 已選擇預設值。

* **允許執行緒式回覆**

   如果未選中，則該想法允許對主題的回復（注釋），但不允許對注釋的回復。 已選擇預設值。

* **允許主要內容**

   如果選中，則其內容被標識為 [特色內容](/help/communities/featured.md)。 已選擇預設值。

### 排行榜功能 {#leaderboard-function}

排行榜功能是包含 [排行榜元件](/help/communities/enabling-leaderboard.md)。

**注釋**:排行榜部分需要進一步配置 *後* 從包含排行榜功能的社區模板建立社區站點。 指定排行榜元件的 [規則](/help/communities/enabling-leaderboard.md#rules-tab)，這取決於配置 [得分和徽章](/help/communities/implementing-scoring.md) 社區網站。

添加到模板時，將開啟以下對話框，該對話框指定模板的預設標題和URL名稱以及預設顯示設定：

![排行榜對話](assets/leaderboard-dialog.png)

* [標題和URL設定](#title-and-url-settings)

* **顯示徽章**

   如果選中，則標籤表徵圖的列將包括在排行榜中。
取消選擇預設值。

* **顯示徽章名稱**

   如果選中，則標籤名稱的列將包括在排行榜中。
取消選擇預設值。

* **顯示頭像**

   如果選中，成員的虛擬形象影像將包含在排行榜中，位於其成員配置檔案的名稱連結旁邊。
取消選擇預設值。

### 頁面功能 {#page-function}

頁面功能將一個空白頁面添加到社區網站，該網站已連接到社區網站的功能：登錄、菜單、通知、消息、主題和品牌。 內容將使用 [標準AEM創作模式](/help/sites-authoring/editing-content.md)。

添加到模板時，唯一的配置是 [標題和URL設定](#title-and-url-settings)。

### QnA 功能 {#qna-function}

QnA函式是包含 [QnA元件](/help/communities/working-with-qna.md) 配置為標籤、檔案上載、後續、成員自編、投票和審核。

添加到模板時，配置允許對特權成員進行限制：

![QNA對話框](assets/qna-dialog.png)

* [標題和URL設定](#title-and-url-settings)

* **允許釘選**

   如果選中，論壇允許將主題答復固定到注釋清單的開頭。 已選擇預設值。

* **允許有特殊權限的成員**

   如果選中，則QnA論壇僅允許特權成員通過允許選擇 [特權成員組](/help/communities/users.md#privileged-members-group)。 如果未選擇，則允許所有社區成員發佈。 取消選擇預設值。

* **允許檔案上傳**

   如果選中，則QnA論壇包括成員上載檔案的功能。 已選擇預設值。

* **允許執行緒式回覆**

   如果未選擇，則QnA論壇允許對已發佈的問題提供評論（答案），但不允許對答案進行答復。 已選擇預設值。

* **允許主要內容**

   如果選中，則其內容被標識為 [特色內容](/help/communities/featured.md)。 已選擇預設值。

## 建立社群功能 {#create-community-function}

通過選擇 `Create Community Function` 表徵圖，位於「社區功能」控制台的頂部。 可以建立基於相同藍AEM圖的多個函式，然後通過在作者編輯模式下開啟來唯一地定制。

![建立社區功能](assets/create-community-function.png)

### 社群功能名稱 {#community-function-name}

![函式名](assets/function-name.png)

在「社區函式名稱」面板上，配置了名稱、說明以及函式是啟用還是禁用：

* **社群功能名稱**

   用於顯示和儲存的函式名稱。

* **社群功能說明**

   顯示的函式說明。

* **已禁用/已啟用**

   控制函式是否可引用的切換開關。

### AEM 藍圖 {#aem-blueprint}

![藍圖](assets/aem-blueprint.png)

在 `AEM Blueprint` 面板中，可以選擇作為社區功能底層實現的藍圖。

社區功能是一個微型站點，包括一個或多個頁面，預先連線以包括在社區站點中，包括登錄、用戶配置檔案、通知、消息、站點菜單、搜索、主題和品牌特徵。 建立函式後， [開啟函式](#open-community-function) 在作者編輯模式中，並自定義頁面或元件設定。

因為社區功能是 [即時拷貝](/help/sites-administering/msm.md#live-copies) 的 [藍圖](/help/sites-administering/msm-livecopy.md#creatingablueprint)，可以將對函式所做的更改推廣，該函式影響從 [社區網站模板](/help/communities/sites.md) 或 [社區組模板](/help/communities/tools-groups.md) 包括了功能。 也可以將頁面與其父藍圖取消關聯，以進行頁面級修改。

另請參閱 [多站點管理器](/help/sites-administering/msm.md)。

### 縮圖 {#thumbnail}

![函式縮略圖](assets/funtion-thumbnail.png)

在「縮略圖」面板上，可以上載影像以在 [社區功能控制台](#community-functions-console)。

## 開啟社群功能 {#open-community-function}

![開函式](assets/open-function.png)

選擇 `Open Community Function` 表徵圖，進入創作頁面內容和修改功能元件配置的作者編輯模式。

### 配置元件 {#configuring-components}

社區功能作為藍圖的實AEM時副本實施，詳細資訊在 [多站點管理器](/help/sites-administering/msm.md)。

不僅可以建立頁面內容，還可以配置元件。

如果在已建立的社區站點的頁面上配置元件，則可能需要取消 [繼承](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) 的子菜單。 配置完成後，應重新建立繼承。

有關配置詳細資訊，請訪問 [社區元件](/help/communities/author-communities.md) 作者。

## 編輯社群功能 {#edit-community-function}

![編輯函式](assets/edit-function.png)

選擇 `Edit Community Function` 表徵圖，使用與 [建立社區函式](#create-community-function)，包括啟用或禁用函式。
