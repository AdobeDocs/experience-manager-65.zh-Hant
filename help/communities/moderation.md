---
title: 協調控制台
seo-title: Moderation Console
description: 如何存取「協調」主控台
seo-description: How to access the Moderation console
uuid: d3b8a160-85b2-43f4-9891-5fafa8c48c5f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 404582ab-bb4c-4775-9ae3-17356d376dca
docset: aem65
role: Admin
exl-id: 829da16a-4083-43c1-857d-f2666b363bfc
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '2042'
ht-degree: 4%

---

# 協調控制台 {#moderation-console}

在AEM Communities，大量 [協調社群內容](/help/communities/moderate-ugc.md) 管理員和社群協調者（指派為協調者的受信任社群成員）皆可從製作和發佈環境中使用。

管理員和社群協調者也可以執行 [內容內協調](/help/communities/in-context.md) 在發佈環境中。

所有功能 [社群網站](/help/communities/sites-console.md) 是 `Administration` 功能表項目。 此 `Administration` 連結可讓您存取「協調」主控台。

從「協調」控制台，管理員和社群協調者將有權存取所有使用者產生的內容(UGC)，且他們有權協調這些內容。 如果允許協調多個網站，則可以檢視所有網站的貼文，或依所選社群網站進行篩選。

如需更多詳細資訊，請造訪 [管理使用者和使用者群組](/help/communities/users.md).

「協調」控制台支援：

* 大量執行協調工作。
* 正在搜索UGC。
* 查看UGC詳細資訊。
* 檢視UGC作者詳細資訊。

僅當以管理員或具有的成員身份登錄時 ` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`，即可執行協調工作。

## 發佈環境存取 {#publish-environment-access}

從已發佈的社群網站存取「協調」主控台是透過管理連結，此連結會在社群協調者登入時顯示。

![publishweretail](assets/publishweretail.png)

選取「管理」連結後，會顯示「協調」主控台：

![moderation-console-publish](assets/moderation-console-publish.png)

## 製作環境存取 {#author-environment-access}

在製作環境中，若要進入「協調」主控台

* 在全局導航中，選擇 **[!UICONTROL 社群]** > **[!UICONTROL 協調]**.

僅在以管理員身分登入，或以 [版主權限](/help/communities/in-context.md#identifyingtrustedmembers)，則可執行協調工作。 顯示的唯一社區內容是允許登錄的成員協調的社區內容。

>[!NOTE]
>
>只有當選擇的SRP實作通用商店時，發佈環境中的UGC才會顯示於作者。 例如，預設情況下，儲存為JSRP，這不是製作和發佈的常見存放區。 請參閱 [社群內容儲存](/help/communities/working-with-srp.md).

![moderationconsoleauthor](assets/moderationconsoleauthor.png)

## 協調控制台UI {#moderation-console-ui}

除了左側導覽邊欄（顯示在作者上，但不顯示在發佈上）之外，協調UI有下列主要區域：

* **[頂端導覽列](#top-navigation-bar)**
* **[工具列](#toolbar)**
* **[內容區域](#content-area)**

### 頂端導覽列 {#top-navigation-bar}

所有主控台的頂端導覽列都為常數。 如需詳細資訊，請參閱 [基本處理](/help/sites-authoring/basic-handling.md).

### 工具列 {#toolbar}

工具列位於頂端導覽列下方，在左側提供下列切換開關：

* [篩選邊欄](/help/communities/moderation.md#filterrail)
開啟邊欄，供您選擇要篩選內容的屬性。

工具列位於頂端導覽列下方，在左側提供下列切換開關：

![小巫](assets/toggleswitch.png)

[篩選邊欄](/help/communities/moderation.md#filterrail)
在選取「搜尋」時開啟邊欄，供您選擇要篩選內容的屬性。

![filterrail](assets/filterrail.png)

### 內容區域 {#content-area}

內容區域包含已發佈UGC的資訊：

* UGC已發佈
* 成員名稱
* 成員頭像
* 貼文的位置。
* 發佈時。
* 貼文的回覆次數。
* [情緒](/help/communities/moderate-ugc.md#sentiment) 與貼文相關聯
* 如果已核准，則會顯示核取記號。
* 如果有附件，則顯示回形針。

>[!NOTE]
> 
>內容區域具有 *無限滾動*，這表示在您到達內容結尾之前，它可讓您繼續捲動。 即使在捲動時，工具列仍停留在內容區域上方的固定可見位置。

### 篩選邊欄 {#ootbfilters}

![開啟欄位](assets/open-filterrail.png)

側面板圖示會開啟篩選邊欄。 顯示在內容區域左側的篩選欄會提供不同的篩選器，每個篩選器都對顯示在內容區域中的參考UGC有立竿見影的效果。

每個類別中的篩選器包括 **或**「d」結合在一起，而不同類別中的篩選器 **和** d一起。

例如，如果您同時檢查 **問題** 和 **回答**，您會看到 **問題** *或* an **回答**.

不過，如果您檢查 **問題** 和 **待定**，您只會看到 **問題** 和 **待定**.

>[!NOTE]
>
>社群協調者可在協調控制台UI上將預先定義的篩選器加入書籤。 當這些篩選器附加至URL的結尾時（作為查詢字串參數），協調者稍後可以返回已建立書籤的篩選器，也可以共用這些連結。

![searchicon](assets/searchicon.png)

當篩選邊欄開啟時，「搜尋」圖示會切換側面板關閉。 不過，若要關閉篩選邊欄並僅檢視使用者產生的內容，請按一下「搜尋」圖示並選取「僅限內容」選項。

#### 內容路徑 {#content-path}

「內容路徑」會限制顯示給放置在指定內容存放庫之貼文的參考UGC。

![內容路徑](assets/content-path.png)

#### 測試搜尋 {#text-search}

文字搜尋會限制對包含輸入文字之貼文顯示的參考UGC。

![文字搜尋](assets/text-search.png)

#### 網站 {#site}

網站會限制所選社群網站貼文所顯示的參考UGC。 如果未核取任何網站，則會顯示所有UGC的參考。

![網站面板](assets/site-panel.png)

>[!NOTE]
>
>當管理員存取大量協調控制台時，會顯示對UGC的所有參考，包括未以 [網站建立精靈](/help/communities/sites-console.md)，例如Geometrixx範例。
>
>當受信任的社群成員在發佈時存取大量協調主控台時，系統只會顯示針對該成員獲授權協調之社群網站所建立之UGC的參考，並可使用網站篩選器加以篩選。

#### 內容類型 {#content-type}

內容類型會限制所選資源類型之貼文所顯示的參考UGC。 可以選擇以下一種或多種類型。 如果未選取任何類型，則會顯示所有類型。

* **評論**
* **論壇主題**
* **論壇回覆**
* **QnA 問題**
* **QnA 答案**
* **部落格文章**
* **部落格評論**
* **日曆事件**
* **行事曆評論**
* **檔案資料庫資料夾**
* **檔案資料庫文件**
* **創意**
* **創意力評論**

![內容類型](assets/content-types.png)

#### 其他內容類型 {#additional-content-types}

若要新增要篩選的其他資源：

* 以管理員身分登入您的製作執行個體。
* 開啟 [Web主控台](https://localhost:4502/system/console/configMgr).
* 找出 `AEM Communities Moderation Dashboard Filters`.
* 選取要在編輯模式中開啟的設定。
* 輸入要對其進行篩選的元件的ResourceType:

   * 例如，要篩選包含的投票元件，請輸入：

      `Voting=social/tally/components/hbs/voting`
   ![additional-contenttype](assets/additional-contenttype.png)

* 選取儲存。
* 重新整理Communities — 協調主控台。

結果是新的可選過濾器，用於 `Voting` 在 `Content Type` 篩選群組。

選取該篩選器時，控制面板的內容將顯示UGC，該UGC符合任何輸入的ResourceType。

#### 狀態 {#status}

狀態限制所引用的UGC顯示給選定狀態的帖子，這些帖子可能是「待定」、「已批准」、「拒絕」或「已關閉」中的一個或多個，以及「為部落格文章草稿」或「已排程」、「QnA問題已回答」或「未回答」中的一個。 如果未選取任何項目，則會顯示所有項目。

>[!NOTE]
>
>如果僅選擇「未應答」狀態，則版主將看到除已應答問題之外的所有內容（適用於所有內容類型）。 這是因為，在未回答的問題和其他內容（如論壇主題、部落格文章或評論）中，不存在負責「已答問題」的屬性。

![狀態](assets/statuses.png)

#### 標幟 {#flagging}

標幟會限制所顯示的參考UGC會被標幟或隱藏的貼文。

標籤內容後，會持續標籤該內容，直到您借由選取 **標幟** 按鈕。 請注意，沒有標幟層級，例如重要或後續動作。

![衰落](assets/flagging.png)

#### 成員 {#members}

成員限制所輸入的成員名稱所過帳的被引用的UGC顯示為UGC。

![成員](assets/members.png)

#### 發佈於前一 {#posted-in-the-last}

「在上次發佈」限制會將參考的UGC顯示於在最後一小時、一天、一週、一個月或一年內發佈的貼文。

![已張貼 — 上次](assets/posted-last.png)

#### 情緒 {#sentiment}

[情緒](/help/communities/moderate-ugc.md#sentiment) 以正面、負面或中性的情緒值，限制對貼文顯示的參考UGC。

![情緒](assets/sentiment.png)

## 自訂篩選器 {#custom-filters}

除了 [篩選邊欄](/help/communities/moderation.md#ootbfilters)，則可將中繼資料的其他自訂篩選器新增至協調UI。 開發人員可使用Github中的范常式式碼，以擴充現有的協調UI篩選條件。

![自訂標籤篩選](assets/custom-tag-filter.png)

此 [範例專案](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/main/aem-communities-moderation-filter) 在Github上實作「標籤」篩選，以根據特定標籤是否套用至使用者產生的內容來篩選UGC清單。 您可以遵循范常式式碼，並為其他類似的UGC中繼資料欄位建立類似的篩選器。

若要安裝標籤篩選器的範例：

1. 在AEM製作上開啟套件管理器(`https://[aem-author]:4502/crx/packmgr/index.jsp`)例項和AEM發佈(`https://[aem-publish]:4503/crx/packmgr/index.jsp`)例項。
1. 建立套件 `com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip` 從GitHub程式碼，並安裝及啟用相同功能。
1. 在AEM製作上開啟套件組合主控台( `https://[aem-author]:4502/system/console/bundles`)例項和AEM發佈( `https://[aem-publish]:4503/system/console/bundles`)例項。
1. 建立套件(`[com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar`)，並安裝及啟用相同功能。
1. 前往 **/apps/social/moderation/facets** AEM作者上的節點(`https://[aem-author]:4502/crx/de/index.jsp#/apps/social/moderation/facets`)和AEM發佈(`https://[aem-publish]:4502/crx/de/index.jsp#/apps/social/moderation/facets`)例項。
1. 新增技術使用者 **communities-utility-reader** with `jcr:read` 權限。

要公開現有社群網站上的自訂篩選器：

1. 編輯 `Clientlibs` 現有協調頁面 `/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.`

   * 新增類別 `cq.social.hbs.moderation.v2.`

1. 前往 `/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.`

   * 設為新元件 `sling:resourceType = social/moderation/v2/filters.`

1. 前往 `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer`.

   * 設為新元件 `sling:resourceType = social/moderation/v2/modcontainer`.

## 協調動作 {#moderation-actions}

[協調動作](/help/communities/moderate-ugc.md#moderation-actions) 可在內容區域中或檢視內容詳細資料時，執行一或多個選取項目。

若要大量協調貼文，請在內容區域中按一下「選取」(![選擇](assets/selecticon.png))圖示，此圖示會顯示在透過滑鼠（案頭）暫留在貼文上，或按住手指（行動）。 這樣，您就會進入多選模式，現在只要按一下，即可選取要大量協調的後續貼文。 使用工具列上顯示的按鈕，對選取的貼文執行協調動作。 所有動作都會提示進行確認。

若要協調內容區域中的單一貼文，請用滑鼠（案頭）將滑鼠移到貼文上，或按住貼文（行動）上的手指，使貼文上顯示按鈕。 對單一內容詳細資料執行作業時，只有刪除動作會提示進行確認。

### 協調多個貼文 {#moderating-multiple-posts}

按一下 `Select` 圖示（在貼文中）:

![select-icon](assets/select-icon.png)

若要退出大量選取模式，請選取工具列上的取消(x)圖示：

可對多則貼文執行的協調動作為：

* 拒絕
* 刪除
* 關閉/重新開啟貼文

只有選取多個貼文時，工具列才會顯示允許這些動作的圖示。

![bulk審核](assets/bulkmoderate.png)

### 協調單一貼文 {#moderating-a-single-post}

在單選模式中，可以：

* 通過選擇用戶名查看用戶詳細資訊。
* 選取貼文的連結，即可在內容中檢視貼文。
* [回覆](#reply)
* [允許](#allow)
* [拒絕](#deny)
* [刪除](#delete)
* [關閉](#close)
* 檢視 [協調歷史記錄](#moderation-history)
* [檢視詳情](#viewdetails)

仲裁動作圖示上方的卡片檢視上顯示的是貼文的文字，下方則是指出：

* 如果它有答復，如果有，則前面加上答複數。
* 如果已標籤。
* 如果已核准。
* UGC發佈時。

![單電模式](assets/singleselectmode.png)

#### 回覆 {#reply}

![回覆](assets/reply.png)

處理單一貼文時，如果UGC類型支援回覆，且設定為允許回覆，則會顯示回覆圖示。

#### 允許 {#allow}

![允許](assets/allow.png)

使用單一貼文時，當貼文遭到標籤或拒絕時，「允許」圖示會出現。 如果已標籤，選取「允許」將會清除所有標幟。

#### 拒絕 {#deny}

![拒絕](assets/deny.png)

此 **拒絕** 協調動作僅適用於已協調的內容，除了在多選模式中，不會出現在未協調的內容上。

未協調的內容一律會獲核准。

經協調的內容最初進入「待定」狀態，之後可修改為核准或拒絕。

離開擱置狀態的內容永遠無法傳回擱置狀態。 標示為已核准或拒絕的內容可隨時變更為不同狀態。

#### 刪除 {#delete}

![刪除](assets/delete.png)

在單一選取或大量模式中，您可以選取項目並加以刪除。 刪除動作會產生確認對話方塊。 刪除後，這些項目會立即從內容區域中消失。 **UGC一旦刪除，就會從存放庫中永久移除，之後將無法擷取**.

#### 關閉 {#close}

![關閉](assets/close.png)

使用單一貼文時，如果UGC類型支援防止該資源進一步貼文的功能，則會顯示「關閉」圖示。

#### 審核歷史記錄 {#moderation-history}

![審核](assets/moderation.png)

處理單一貼文時，將滑鼠游標暫留在該貼文上時，會顯示「協調歷程記錄」圖示。 選取圖示會顯示一個窗格，其中包含針對UGC貼文所採取動作的歷史記錄。

若要返回顯示多個UGC貼文的內容區域，請在檢視詳細資料窗格右上角選取X。

例如：

![調節歷史記錄](assets/moderation-history.png)

#### 檢視詳細資料 {#view-detail}

![檢視](assets/view.png)

使用單一貼文時，可以以詳細模式開啟UGC來檢視更多詳細資訊。

若要這麼做，請將滑鼠指標暫留在貼文上以顯示 `View Detail` 圖示，然後選取該圖示，以顯示包含貼文詳細資料的面板。

若要返回顯示多個UGC貼文的內容區域，請在檢視詳細資料窗格右上角選取X。

例如：

![view1](assets/view1.png)
