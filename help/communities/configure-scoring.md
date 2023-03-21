---
title: 計分和徽章要點
seo-title: Scoring and Badges Essentials
description: 計分與徽章功能概觀
seo-description: Scoring and Badges feature overview
uuid: 6e3af071-04e8-4dc1-977a-0da711b72961
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 628b6dcd-8b1c-4166-8fc2-843baa86ac1c
docset: aem65
exl-id: 470a382a-2aa7-449e-bf48-b5a804c5b114
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 1%

---

# 計分和徽章要點 {#scoring-and-badges-essentials}

AEM Communities計分和徽章功能可識別並獎勵社群成員。

如需設定功能的詳細資訊，請參閱

* [社群計分和徽章](/help/communities/implementing-scoring.md)

本頁包含其他技術詳細資訊：

* 如何 [顯示徽章](#displaying-badges) 為影像或文字
* 如何開啟廣泛 [偵錯記錄](#debug-log-for-scoring-and-badging)
* 如何 [訪問UGC](#ugc-for-scoring-and-badging) 與打分和徽章有關

>[!CAUTION]
>
>CRXDE Lite中可見的實作結構可能會有所變更。

## 顯示徽章 {#displaying-badges}

徽章是否顯示為文字或影像，在HBS範本的用戶端進行控制。

例如，搜尋 `this.isAssigned` in `/libs/social/forum/components/hbs/topic/list-item.hbs`:

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

如果為true, isAssigned表示已為角色分配徽章，且徽章應顯示為文本。

如果為false, isAssigned表示已為已獲得分數授予徽章，且徽章應顯示為影像。

對此行為所做的任何變更都應在自訂指令碼中進行（覆寫或覆蓋）。 請參閱 [用戶端自訂](/help/communities/client-customize.md).

## 計分和簽名的調試日誌 {#debug-log-for-scoring-and-badging}

若要協助除錯計分和標籤，可設定自訂記錄檔。 如果此功能出現問題，則此日誌檔案的內容將提供給客戶支援。

如需詳細指示，請造訪 [建立自訂記錄檔](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).

若要快速設定slinglog檔案：

1. 存取 **Adobe Experience Manager Web主控台記錄支援**，例如

   * https://localhost:4502/system/console/slinglog

1. 選擇 **添加新記錄器**

   1. 選擇 `DEBUG` for **記錄層級**

   1. 輸入 **記錄檔**，例如

      * logs/scoring-debug.log
   1. 輸入2 **記錄器** （類）條目(使用 `+` 圖示)

      * `com.adobe.cq.social.scoring`
      * `com.adobe.cq.social.badging`
   1. 選擇 **儲存**



![debug-scoring-log](assets/debug-scoring-log.png)

要查看日誌條目，請執行以下操作：

* 從Web控制台

   * 在 **狀態** 功能表
   * 選擇 **記錄檔**
   * 搜尋您的記錄檔檔案名稱，例如 `scoring-debug`

* 在伺服器的本地磁碟上

   * 日誌檔案為&lt;*server-install-dir*>/crx-quickstart/logs/&lt;*log-file-name*>.log

   * 例如, `.../crx-quickstart/logs/scoring-debug.log`

![計分日誌](assets/scoring-log.png)

## UGC用於計分和簽名 {#ugc-for-scoring-and-badging}

當選擇的SRP是JSRP或MSRP，但不是ASRP時，可以查看與計分和徽章相關的UGC。 (如果不熟悉這些術語，請參閱 [社群內容儲存](/help/communities/working-with-srp.md) 和 [儲存資源提供程式概述](/help/communities/srp.md).)

存取計分和加註資料的說明使用JSRP，因為UGC可透過 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

**JSRP關於作者**:在製作環境中實驗會導致UGC，而此UGC僅可從製作環境中看到。

**發佈JSRP**:同樣地，如果在發佈環境上進行測試，則需要以發佈例項的管理權限存取CRXDE Lite。 如果發佈執行個體在 [生產模式](/help/sites-administering/production-ready.md) (nosamplecontent runmode)，則必須 [啟用CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

UGC在JSRP上的基地位置為 `/content/usergenerated/asi/jcr/`.

### 計分與加號API {#scoring-and-badging-apis}

下列API可供使用：

* [6.3中的com.adobe.cq.social.scorin.api](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html)
* [6.3中的com.adobe.cq.social.badging.api](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html)

已安裝Feature Pack的最新Javadoc可供Adobe存放庫的開發人員使用。 請參閱 [將Maven用於社群：Javadocs](/help/communities/maven.md#javadocs).

**UGC在存放庫中的位置和格式可能會變更，恕不另行警告**.

### 範例設定 {#example-setup}

存放庫資料的螢幕擷取畫面來自為兩個不同AEM網站上的論壇設定計分和標籤：

1. AEM網站 *with* 唯一id（使用精靈建立的社群網站）:

   * 使用在 [快速入門教學課程](/help/communities/getting-started.md)
   * 找到論壇頁面節點

      `/content/sites/engage/en/forum/jcr:content`

   * 添加計分和標籤屬性

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-scoring,
   /libs/settings/community/badging/rules/forums-scoring]
   ```

   * 找到論壇元件節點

      `/content/sites/engage/en/forum/jcr:content/content/primary/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * 若要顯示徽章，請新增屬性

      `allowBadges = true`

   * 使用者登入、建立論壇主題，並獲得銅牌


1. AEM網站 *無* 唯一id:

   * 使用 [社群元件指南](/help/communities/components-guide.md)
   * 找到論壇頁面節點

      `/content/community-components/en/forum/jcr:content`

   * 添加計分和標籤屬性

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-badging,
   /libs/settings/community/badging/rules/forums-badging]
   ```

   * 找到論壇元件節點

      `/content/community-components/en/forum/jcr:content/content/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * 若要顯示徽章，請新增屬性

      `allowBadges = true`

   * 使用者登入、建立論壇主題，並獲得銅牌


1. 使用cURL為使用者指派協調者徽章：

   ```shell
   curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" https://localhost:4503/home/users/community/w271OOup2Z4DjnOQrviv/profile.social.json
   ```

   由於用戶已獲得兩個銅牌並且已獲得版主徽章，因此用戶將顯示其論壇條目，如下所示：

   ![版主](assets/moderator.png)

>[!NOTE]
>
>此範例不遵循下列最佳實務：
>
>* 計分規則名稱應為全域唯一；它們的結尾不應該是同一個名稱。
>
>  以下範例 *not* 要執行：
>
>  /libs/settings/community/scoring/rules/site1/forums計分
>  /libs/settings/community/scoring/rules/site2/forums計分
>
>* 為不同的AEM網站建立不重複徽章影像


### 訪問計分UGC {#access-scoring-ugc}

使用 [API](#scoring-and-badging-apis) 為偏好設定。

為了調查目的，以JSRP為例，包含分數的基本資料夾為

* `/content/usergenerated/asi/jcr/scoring`

的子節點 `scoring` 是計分規則名稱。 因此，最佳實務是，伺服器上的計分規則名稱是全域唯一的。

對於Geometrixx參與網站、使用者及其分數，位於以計分規則名稱、社群網站網站ID( `engage-ba81p`)、唯一id和使用者id :

* `.../scoring/forums-scoring/engage-ba81p/6d179715c0e93cb2b20886aa0434ca9b5a540401/riley`

對於社群元件指南網站，使用者及其分數位於以計分規則名稱（預設ID）建構的路徑中( `default-site`)、唯一id和使用者id :

* `.../scoring/forums-scoring/default-site/b27a17cb4910a9b69fe81fb1b492ba672d2c086e/riley`

分數會儲存在屬性中 `scoreValue_tl` 其中只能包含值，或間接引用atomicCounter。

![access-scoring-ugc](assets/access-scoring-ugc.png)

### 訪問標籤UGC {#access-badging-ugc}

使用 [API](#scoring-and-badging-apis) 為偏好設定。

為了調查目的，以JSRP為例，包含已指派或已授予徽章之資訊的基本資料夾為

* `/content/usergenerated/asi/jcr`

後接使用者設定檔的路徑，結尾為徽章資料夾，例如：

* `/home/users/community/w271OOup2Z4DjnOQrviv/profile/badges`

#### 獎章 {#awarded-badge}

![獎授 — 加丁 — ugc](assets/access-badging-ugc.png)

#### 指派的徽章 {#assigned-badge}

![指派徽章](assets/assigned-badge.png)

## 其他資訊 {#additional-information}

要根據點顯示按排序的成員清單，請執行以下操作：

* [排行榜功能](/help/communities/functions.md#leaderboard-function) 以包含在社群網站或群組範本中。
* [排行榜元件](/help/communities/enabling-leaderboard.md)，此元件為排行榜功能的精選元件，用於頁面編寫。
