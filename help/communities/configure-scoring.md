---
title: 評分和徽章要點
description: 瞭解Adobe Experience Manager社群評分和徽章功能如何識別和獎勵社群成員。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 470a382a-2aa7-449e-bf48-b5a804c5b114
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# 評分和徽章要點 {#scoring-and-badges-essentials}

AEM Communities評分和徽章功能可識別和獎勵社群成員。

有關設定功能的詳細資訊，請參閱

* [社群評分和預算](/help/communities/implementing-scoring.md)

此頁面包含其他技術詳細資訊：

* 操作說明 [顯示徽章](#displaying-badges) 做為影像或文字
* 如何開啟廣泛功能 [偵錯記錄](#debug-log-for-scoring-and-badging)
* 操作說明 [存取UGC](#ugc-for-scoring-and-badging) 與評分和徽章相關

>[!CAUTION]
>
>CRXDE Lite中顯示的實作結構可能會有所變更。

## 顯示徽章 {#displaying-badges}

徽章是以文字還是影像的形式顯示，需在HBS範本的使用者端加以控制。

例如，搜尋 `this.isAssigned` 在 `/libs/social/forum/components/hbs/topic/list-item.hbs`：

```
{{#each author.badges}}

  {{#if this.isAssigned}}

    <div class="scf-badge-text">

      {{this.title}}

    </div>

  {{/if}}

{{/each}}

{{#each author.badges}}

  {{#unless this.isAssigned}}

    <img class="scf-badge-image" alt="{{this.title}}" title="{{this.title}}" src="{{this.imageUrl}}" />

  {{/unless}}

{{/each}}
```

如果為True， `isAssigned` 表示此徽章已指派給角色，且此徽章應顯示為文字。

如果為false， `isAssigned` 表示該徽章已獲得贏取分數，且應顯示為影像。

對此行為的任何變更都應在自訂指令碼中進行（覆寫或覆蓋）。 另請參閱 [使用者端自訂](/help/communities/client-customize.md).

## 評分和徽章的偵錯記錄 {#debug-log-for-scoring-and-badging}

為協助偵錯評分和徽章，可以設定自訂記錄檔。 如果功能發生問題，可將此記錄檔的內容提供給客戶支援。

如需詳細指示，請造訪 [建立自訂記錄檔](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).

若要快速設定slinglog檔案：

1. 存取 **Adobe Experience Manager網頁主控台記錄檔支援**，例如

   * https://localhost:4502/system/console/slinglog

1. 選取 **新增記錄器**

   1. 選取 `DEBUG` 的 **記錄層級**

   1. 輸入名稱 **記錄檔**，例如

      * logs/scoring-debug.log

   1. 輸入兩個 **Logger** （類別）專案(使用 `+` 圖示)

      * `com.adobe.cq.social.scoring`
      * `com.adobe.cq.social.badging`

   1. 選取 **儲存**

![debug-scoring-log](assets/debug-scoring-log.png)

若要檢視記錄專案，請執行下列動作：

* 從Web控制檯

   * 在 **狀態** 功能表
   * 選取 **記錄檔**
   * 搜尋您的記錄檔名稱，例如 `scoring-debug`

* 在伺服器的本機磁碟上

   * 記錄檔位於&lt;*server-install-dir*>/crx-quickstart/logs/&lt;*log-file-name*>.log

   * 例如 `.../crx-quickstart/logs/scoring-debug.log`

![scoring-log](assets/scoring-log.png)

## 評分和徽章的UGC {#ugc-for-scoring-and-badging}

當所選的SRP是JSRP或MSRP，而不是ASRP時，可以檢視與評分和徽章相關的UGC。 (若不熟悉這些詞語，請參閱 [社群內容儲存](/help/communities/working-with-srp.md) 和 [儲存資源提供者概觀](/help/communities/srp.md).)

使用JSRP存取評分和徽章資料的說明，因為使用UGC可輕鬆存取 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

**作者上的JSRP**：在製作環境中實驗會產生只可從製作環境看到的UGC。

**發佈上的JSRP**：同樣地，如果在發佈環境中測試，必須在發佈執行個體上使用管理許可權存取CRXDE Lite。 如果發佈執行個體執行於 [生產模式](/help/sites-administering/production-ready.md) （nosamplecontent執行模式），必須 [啟用CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

JSRP上UGC的基本位置為 `/content/usergenerated/asi/jcr/`.

### 評分和徽章API {#scoring-and-badging-apis}

以下API可供使用：

* [6.3中的com.adobe.cq.social.scoring.api](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html)
* [6.3中的com.adobe.cq.social.badging.api](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html)

已安裝Feature Pack的最新Javadoc可供Adobe存放庫中的開發人員使用。 另請參閱 [使用Maven for Communities ：Javadocs](/help/communities/maven.md#javadocs).

**UGC在存放庫中的位置和格式可能會有所變更，恕不另行警告**.

### 範例設定 {#example-setup}

存放庫資料的熒幕擷取畫面來自於為兩個不同AEM網站上的論壇設定評分和徽章：

1. AEM網站 *替換為* 唯一id （使用精靈建立的社群網站） ：

   * 使用期間建立的快速入門教學課程（參與）網站 [快速入門教學課程](/help/communities/getting-started.md)
   * 找出論壇頁面節點

     `/content/sites/engage/en/forum/jcr:content`

   * 新增評分和徽章屬性

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-scoring,
   /libs/settings/community/badging/rules/forums-scoring]
   ```

   * 找出論壇元件節點

     `/content/sites/engage/en/forum/jcr:content/content/primary/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * 若要顯示徽章，請新增屬性

     `allowBadges = true`

   * 使用者登入、建立論壇主題，並獲頒銅級徽章

1. AEM網站 *不含* 唯一識別碼：

   * 使用 [社群元件指南](/help/communities/components-guide.md)
   * 找出論壇頁面節點

     `/content/community-components/en/forum/jcr:content`

   * 新增評分和徽章屬性

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-badging,
   /libs/settings/community/badging/rules/forums-badging]
   ```

   * 找出論壇元件節點

     `/content/community-components/en/forum/jcr:content/content/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * 若要顯示徽章，請新增屬性

     `allowBadges = true`

   * 使用者登入、建立論壇主題，並獲頒銅級徽章

1. 已使用cURL為使用者指派版主徽章：

   ```shell
   curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" https://localhost:4503/home/users/community/w271OOup2Z4DjnOQrviv/profile.social.json
   ```

   由於使用者已獲得兩個銅級徽章並獲得了版主徽章，因此該使用者與其論壇條目一起出現如下：

   ![版主](assets/moderator.png)

>[!NOTE]
>
>此範例未遵循下列最佳實務：
>
>* 評分規則名稱應為全域唯一名稱，且不得以相同名稱結尾。
>
>  的範例 *非* 待辦事項：
>
>  /libs/settings/community/scoring/rules/site1/forums-scoring
>  /libs/settings/community/scoring/rules/site2/forums-scoring
>
>* 為不同的AEM網站建立唯一的徽章影像

### 存取評分UGC {#access-scoring-ugc}

使用 [API](#scoring-and-badging-apis) 建議使用。

在調查用途中，以JSRP為例，包含分數的基本資料夾為

* `/content/usergenerated/asi/jcr/scoring`

的子節點： `scoring` 是評分規則名稱。 因此，最佳做法是伺服器上的評分規則名稱是全球唯一的。

對於Geometrixx參與網站，使用者和他們的分數在使用評分規則名稱，社群網站的網站ID ( `engage-ba81p`)、唯一id和使用者id ：

* `.../scoring/forums-scoring/engage-ba81p/6d179715c0e93cb2b20886aa0434ca9b5a540401/riley`

對於社群元件指南網站，使用者及其分數位於以評分規則名稱(預設ID ( `default-site`)、唯一id和使用者id ：

* `.../scoring/forums-scoring/default-site/b27a17cb4910a9b69fe81fb1b492ba672d2c086e/riley`

分數會儲存在屬性中 `scoreValue_tl` 只能包含值，或間接參照atomicCounter。

![access-scoring-ugc](assets/access-scoring-ugc.png)

### 存取徽章UGC {#access-badging-ugc}

使用 [API](#scoring-and-badging-apis) 建議使用。

在調查用途中，以JSRP為例，包含指派或獎勵徽章相關資訊的基本資料夾為

* `/content/usergenerated/asi/jcr`

後面接著使用者設定檔的路徑，結尾是徽章資料夾，例如：

* `/home/users/community/w271OOup2Z4DjnOQrviv/profile/badges`

#### 已授與的徽章 {#awarded-badge}

![awerated-badging-ugc](assets/access-badging-ugc.png)

#### 已指派的徽章 {#assigned-badge}

![assigned-badge](assets/assigned-badge.png)

## 其他資訊 {#additional-information}

若要根據點顯示已排序的成員清單，請執行下列動作：

* [排行榜功能](/help/communities/functions.md#leaderboard-function) 包含在社群網站或群組範本中。
* [排行榜元件](/help/communities/enabling-leaderboard.md)，排行榜功能的精選元件，用於頁面製作。
