---
title: 稽核主控台
description: 瞭解管理員和社群版主如何使用「稽核」主控台來存取他們有權稽核的所有UGC。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 829da16a-4083-43c1-857d-f2666b363bfc
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2028'
ht-degree: 2%

---

# 稽核主控台 {#moderation-console}

在AEM Communities中，管理員和社群版主（指派為版主的受信任社群成員）可同時在Author和Publish環境中大量[版主社群內容](/help/communities/moderate-ugc.md)。

管理員和社群版主也可以在Publish環境中執行[內容中稽核](/help/communities/in-context.md)。

所有[社群網站](/help/communities/sites-console.md)的功能是可供具有管理許可權登入的使用者使用的`Administration`功能表專案。 `Administration`連結提供對Moderation Console的存取權。

在「調節」控制檯中，管理員和社群調節者有權存取所有他們有權調節的使用者產生內容(UGC)。 如果允許稽核多個網站，則可檢視所有網站的貼文，或依選取的社群網站進行篩選。

如需詳細資訊，請造訪[管理使用者和使用者群組](/help/communities/users.md)。

「協調」主控台支援：

* 正在大量執行稽核工作。
* 正在搜尋UGC。
* 檢視UGC詳細資料。
* 檢視UGC作者詳細資料。

只有當以管理員或具有` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`的成員身分登入時，才能執行仲裁工作。

## Publish環境存取權 {#publish-environment-access}

若要從已發佈的社群網站存取版主主控台，需先透過社群版主登入時顯示的「管理」連結進行。

![publishweretail](assets/publishweretail.png)

選取「管理」連結，會顯示「稽核」主控台：

![moderation-console-publish](assets/moderation-console-publish.png)

## 作者環境存取權 {#author-environment-access}

在製作環境中，若要存取「協調」主控台

* 從全域導覽中，選取&#x200B;**[!UICONTROL 社群]** > **[!UICONTROL 稽核]**。

只有當以系統管理員或具有[仲裁者許可權](/help/communities/in-context.md#identifyingtrustedmembers)的成員身分登入時，才能執行仲裁工作。 顯示的唯一社群內容是允許登入成員稽核的內容。

>[!NOTE]
>
>如果所選的SRP實作公用存放區，則Publish環境的UGC僅對Author可見。 例如，預設的儲存體為JSRP，這不是Author和Publish的常見儲存體。 請參閱[社群內容存放區](/help/communities/working-with-srp.md)。

![moderationconsoleauthor](assets/moderationconsoleauthor.png)

## Moderation Console UI {#moderation-console-ui}

將左側導覽邊欄放開(顯示在作者上，但不顯示在Publish上)，稽核UI有下列主要區域：

* **[頂端導覽列](#top-navigation-bar)**
* **[工具列](#toolbar)**
* **[內容區域](#content-area)**

### 頂端導覽列 {#top-navigation-bar}

所有主控台的頂端導覽列都是固定的。 如需詳細資訊，請參閱[基本處理](/help/sites-authoring/basic-handling.md)。

### 工具列 {#toolbar}

工具列位於頂端導覽列下方，在左側提供下列切換開關：

* [篩選器邊欄](/help/communities/moderation.md#filterrail)
開啟邊欄，您可在其中選取要篩選內容的屬性。

工具列位於頂端導覽列下方，在左側提供下列切換開關：

![toggleswitch](assets/toggleswitch.png)

[篩選器邊欄](/help/communities/moderation.md#filterrail)
在選取「搜尋」時開啟邊欄，允許您選取要篩選內容的屬性。

![篩選邊欄](assets/filterrail.png)

### 內容區域 {#content-area}

內容區域包含已發佈UGC的資訊：

* UGC已張貼
* 成員名稱
* 成員頭像
* 貼文的位置
* 張貼時間
* 回覆貼文的次數
* 與貼文相關的[情緒](/help/communities/moderate-ugc.md#sentiment)
* 如果核准，會顯示核取記號
* 如果有附件，則會顯示回形針

>[!NOTE]
> 
>內容區域具有&#x200B;*無限捲動*，這表示您可以繼續捲動，直到內容結束為止。 即使捲動時，工具列仍會維持在內容區域上方的固定、可見位置。

### 篩選邊欄 {#ootbfilters}

![開放式篩選邊欄](assets/open-filterrail.png)

側面板圖示會開啟篩選邊欄。 篩選器邊欄會顯示在內容區域的左側，提供不同的篩選器，每個篩選器都會立即影響內容區域中顯示的引用UGC。

每個類別中的篩選器是&#x200B;**或**&#x200B;的組合，而不同類別中的篩選器是&#x200B;**和**&#x200B;的組合。

例如，如果您同時檢查&#x200B;**問題**&#x200B;和&#x200B;**答案**，您會看到內容是&#x200B;**問題** *或* **答案**。

不過，若您檢查&#x200B;**問題**&#x200B;和&#x200B;**擱置中**，您只會看到內容是&#x200B;**問題**&#x200B;和&#x200B;**擱置中**。

>[!NOTE]
>
>社群版主可將版主主控台UI上的預先定義篩選器加入書籤。 由於這些篩選器會附加至URL的結尾（作為查詢字串引數），版主稍後可以返回書籤化篩選器，也可以共用這些連結。

![searchicon](assets/searchicon.png)

當篩選邊欄開啟時，搜尋圖示會切換關閉的側面板。 但若要關閉篩選邊欄並僅檢視使用者產生的內容，請按一下「搜尋」圖示，然後選取「僅限內容」選項。

#### 内容路徑 {#content-path}

內容路徑將顯示的參考UGC限製為放置在指定內容存放庫中的帖子。

![content-path](assets/content-path.png)

#### 測試搜尋 {#text-search}

文字搜尋會將參照的UGC顯示限製為包含輸入文字的貼文。

![文字搜尋](assets/text-search.png)

#### 網站 {#site}

網站將參照的UGC顯示限製為張貼至選取的社群網站。 如果未核取任何網站，則會顯示UGC的所有參考。

![網站面板](assets/site-panel.png)

>[!NOTE]
>
>當管理員存取大量仲裁主控台時，所有對UGC的參考都會顯示，包括不是使用[網站建立精靈](/help/communities/sites-console.md)建立的網站，例如Geometrixx範例。
>
>當信任的社群成員在Publish上存取大量仲裁主控台時，只會顯示對該成員有權仲裁的社群網站所建立的UGC參照。 此外，也可使用「網站」篩選條件來篩選。

#### 內容類型 {#content-type}

內容型別將引用的UGC顯示限製為所選資源型別的帖子。 可以選取下列一或多種型別。 如果未選取任何型別，則會顯示所有型別。

* **註解**
* **論壇主題**
* **論壇回覆**
* **QnA問題**
* **QnA答案**
* **部落格**
* **部落格註解**
* **行事曆活動**
* **行事曆註解**
* **檔案庫資料夾**
* **檔案庫檔案**
* **想法**
* **創意力註解**

![內容型別](assets/content-types.png)

#### 其他內容型別 {#additional-content-types}

若要新增其他要篩選的資源：

* 以管理員身分登入您的作者執行個體。
* 開啟[網頁主控台](https://localhost:4502/system/console/configMgr)。
* 找到`AEM Communities Moderation Dashboard Filters`。
* 選取設定，以便您可以在編輯模式中開啟。
* 輸入要篩選之元件的ResourceType：

   * 例如，若要篩選包含的投票元件，請輸入：

     `Voting=social/tally/components/hbs/voting`

  ![additional-contenttype](assets/additional-contenttype.png)

* 選取「儲存」。
* 重新整理「社群 — 稽核」主控台。

結果是`Content Type`篩選群組下`Voting`的新可選取篩選。

選取該篩選器時，控制面板的內容會顯示符合輸入之任何ResourceTypes的UGC。

#### 狀態 {#status}

狀態會將參照的UGC顯示限製為所選狀態的文章，這些狀態可能為擱置中、已核准、已拒絕或已關閉的一或多個，以及草稿或已排程的部落格，以及已回答或未回答的QnA問題。 如果未選取任何專案，則會顯示所有專案。

>[!NOTE]
>
>如果只選取「未回答」狀態，版主會看到已回答問題以外的所有內容（適用於所有內容型別）。 這是因為如果沒有已回答的問題和其他內容（例如論壇主題、部落格或評論），則負責已回答問題的屬性不存在。

![狀態](assets/statuses.png)

#### 標幟 {#flagging}

標幟會將參照的UGC顯示限製為已標幟或隱藏的貼文。

標籤內容後，該內容會維持標籤狀態，直到您再次選取&#x200B;**標幟**&#x200B;按鈕取消標籤該內容為止。 沒有標幟層級，例如重要或後續追蹤。

![標幟](assets/flagging.png)

#### 成員 {#members}

成員限制所參考的UGC顯示到由輸入的成員名稱張貼的UGC。

![個成員](assets/members.png)

#### 發佈於前一 {#posted-in-the-last}

發佈於過去將參照的UGC限製為過去小時、天、周、月或年所做的發佈。

![張貼日期](assets/posted-last.png)

#### 情緒 {#sentiment}

[情緒](/help/communities/moderate-ugc.md#sentiment)將參考的UGC顯示限製為情緒值為正面、負面或中立的貼文。

![情緒](assets/sentiment.png)

## 自訂篩選器 {#custom-filters}

除了[篩選邊欄](/help/communities/moderation.md#ootbfilters)中的現成篩選器，中繼資料上的其他自訂篩選器可以新增到稽核UI。 開發人員可以在GitHub中使用範常式式碼，擴充現有的稽核UI篩選器。

![自訂標籤篩選器](assets/custom-tag-filter.png)

GitHub上的[範例專案](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/main/aem-communities-moderation-filter)實作標籤篩選器，以根據特定標籤是否已套用至使用者產生的內容來篩選UGC清單。 您可以遵循範常式式碼，並為其他類似的UGC中繼資料欄位建立類似篩選器。

安裝「標籤」篩選器的範例：

1. 在AEM Author (`https://[aem-author]:4502/crx/packmgr/index.jsp`)執行個體和AEM Publish (`https://[aem-publish]:4503/crx/packmgr/index.jsp`)執行個體上開啟封裝管理員。
1. 從GitHub程式碼建置套件`com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip`，並安裝及啟用相同的套件。
1. 開啟AEM Author (`https://[aem-author]:4502/system/console/bundles`)執行個體和AEM Publish (`https://[aem-publish]:4503/system/console/bundles`)執行個體上的套件組合主控台。
1. 從GitHub建置套件(`[com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar`)，並安裝及啟用相同的套件。
1. 前往AEM Author (`https://[aem-author]:4502/crx/de/index.jsp#/apps/social/moderation/facets`)和AEM Publish (`https://[aem-publish]:4502/crx/de/index.jsp#/apps/social/moderation/facets`)執行個體上的&#x200B;**/apps/social/moderation/facets**&#x200B;節點。
1. 新增具有`jcr:read`許可權的技術使用者&#x200B;**communities-utility-reader**。

若要在現有社群網站上公開自訂篩選器：

1. 編輯現有稽核頁面`/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.`的`Clientlibs`

   * 新增類別`cq.social.hbs.moderation.v2.`

1. 前往`/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.`

   * 設定為新元件`sling:resourceType = social/moderation/v2/filters.`

1. 前往 `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer`。

   * 設定為新元件`sling:resourceType = social/moderation/v2/modcontainer`。

## 稽核動作 {#moderation-actions}

[在內容區域或檢視內容詳細資料時，可以針對一或多個選取專案執行稽核動作](/help/communities/moderate-ugc.md#moderation-actions)。

若要大量稽核貼文，請在內容區域中按一下貼文上的「選取（![選取](assets/selecticon.png)）」圖示，當滑鼠（案頭）將滑鼠懸停在貼文上或按住手指並按住貼文（行動裝置）時，此圖示就會顯示。 這樣，您就可以進入多選模式，現在只需按一下，即可選取後續的貼文，以進行大量稽核。 使用工具列上顯示的按鈕，以便您可以對選取的貼文執行稽核動作。 所有動作會提示確認。

若要稽核內容區域中的單一貼文，請使用滑鼠（桌上型電腦）將滑鼠游標停留在貼文上，或用手指按住貼文（行動裝置），讓按鈕顯示在貼文上。 在單一內容詳細資料上操作時，只有刪除動作會提示確認。

### 仲裁多個貼文 {#moderating-multiple-posts}

按一下貼文上的`Select`圖示，進入大量選取模式：

![select-icon](assets/select-icon.png)

若要結束大量選取模式，請選取工具列上的取消(x)圖示：

可在多個貼文上執行的稽核動作包括：

* 拒絕
* 刪除
* 關閉/重新開啟貼文

只有在選取了多個貼文時，才會在工具列上顯示允許這些動作的圖示。

![bulkmoderate](assets/bulkmoderate.png)

### 仲裁單一貼文 {#moderating-a-single-post}

在單一選取模式中，可以：

* 選取使用者名稱以檢視使用者詳細資訊。
* 選取貼文的連結，檢視內容中的貼文。
* [回覆](#reply)
* [允許](#allow)
* [拒絕](#deny)
* [刪除](#delete)
* [關閉](#close)
* 檢視[稽核歷史記錄](#moderation-history)
* [檢視詳情](#viewdetails)

在卡片檢視中，稽核動作圖示上方顯示的是貼文的文字，下方顯示的是表示下列內容的資料：

* 如果有回覆，則會在回覆前加上回複數
* 如果已標幟
* 若已核准
* 發佈UGC的時間

![singleselectmode](assets/singleselectmode.png)

#### 回覆 {#reply}

![回覆](assets/reply.png)

處理單一貼文時，如果UGC型別支援回覆，且已設定為允許回覆，則會顯示「回覆」圖示。

#### 允許 {#allow}

![允許](assets/allow.png)

處理單一貼文時，當貼文被標幟或拒絕時，允許圖示就會顯示。 如果已標幟，選取「允許」會清除所有標幟。

#### 拒絕 {#deny}

![拒絕](assets/deny.png)

**拒絕**&#x200B;仲裁動作僅適用於已仲裁的內容，且不會出現在未仲裁的內容上，除非在多重選取模式中。

未經稽核的內容一律會獲得核准。

稽核的內容最初會進入「待處理」狀態，並可在稍後修改以供核准或拒絕。

離開擱置狀態的內容永遠無法回到擱置狀態。 標示為已核准或拒絕的內容可隨時變更為其他狀態。

#### 刪除 {#delete}

![刪除](assets/delete.png)

在單一選取或大量模式中，您可以選取專案並將其刪除。 刪除動作會產生確認對話方塊。 刪除後，這些專案會立即從內容區域中消失。 **一旦刪除UGC，就會從存放庫中永久移除它，之後就無法擷取**。

#### 關閉 {#close}

![關閉](assets/close.png)

使用單一貼文時，如果UGC型別支援防止該資源再出現貼文的功能，則會顯示「關閉」圖示。

#### 審核歷史記錄 {#moderation-history}

![稽核](assets/moderation.png)

處理單一貼文時，將滑鼠懸停於其上時會顯示「稽核歷史記錄」圖示。 選取圖示會顯示一個窗格，其中包含針對UGC貼文採取的動作歷史記錄。

若要返回多個UGC貼文的內容區域顯示，請選取檢視詳細資料窗格右上角的X。

例如：

![moderation-history](assets/moderation-history.png)

#### 檢視詳細資料 {#view-detail}

![檢視](assets/view.png)

處理單一貼文時，可在詳細模式中開啟UGC，檢視更多詳細資料。

若要這麼做，請將滑鼠停留在貼文上以顯示`View Detail`圖示，並選取它以顯示包含貼文詳細資訊的面板。

若要返回多個UGC貼文的內容區域顯示，請選取檢視詳細資料窗格右上角的X。

例如：

![檢視1](assets/view1.png)
