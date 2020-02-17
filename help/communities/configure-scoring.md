---
title: 計分和徽章基本工具
seo-title: 計分和徽章基本工具
description: 計分與標章功能概觀
seo-description: 計分與標章功能概觀
uuid: 6e3af071-04e8-4dc1-977a-0da711b72961
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 628b6dcd-8b1c-4166-8fc2-843baa86ac1c
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 計分和徽章基本工具{#scoring-and-badges-essentials}

AEM Communities計分和標章功能提供識別和獎勵社群成員的能力。

如需設定功能的詳細資訊，請參閱

* [社群評分和標章](/help/communities/implementing-scoring.md)

本頁包含其他技術詳細資訊：

* 如何 [將徽章顯示為影像](#displaying-badges) 或文字
* 如何開啟廣泛的除錯 [記錄功能](#debug-log-for-scoring-and-badging)
* 如何 [存取與計分](#ugc-for-scoring-and-badging) 、徽章相關的UGC

>[!CAUTION]
>
>在CRXDE Lite中可見的實作結構可能會有所變更。

## 顯示標章 {#displaying-badges}

徽章是顯示為文字或影像，會在HBS範本的用戶端進行控制。

例如，在中 `this.isAssigned` 搜 `/libs/social/forum/components/hbs/topic/list-item.hbs`尋：

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

如果為true,isAssigned表示已為角色指派徽章，且徽章應顯示為文字。

如果為false，則「已指派」表示已授與贏取分數的徽章，且徽章應顯示為影像。

對此行為所做的任何變更都應在自訂指令碼中進行（覆寫或覆蓋）。 請參 [閱用戶端自訂](/help/communities/client-customize.md)。

## 計分與簽名的除錯記錄 {#debug-log-for-scoring-and-badging}

若要協助除錯計分和標籤，可設定自訂記錄檔。 如果功能出現問題，則可將此日誌檔案的內容提供給客戶支援。

如需詳細指示，請 [造訪建立自訂記錄檔](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file)。

要快速設定slinglog檔案：

1. 存取 **Adobe Experience Manager Web Console記錄檔支援**，例如

   * https://localhost:4502/system/console/slinglog

1. select **Add new logger**

   1. 選擇 `DEBUG`日誌 **級別**

   1. 輸入日誌檔案 **的名稱**，例如

      * logs/scoring-debug.log
   1. 輸入兩個**Logger **(class)條目(使用 `+` 表徵圖)

      * `com.adobe.cq.social.scoring`
      * `com.adobe.cq.social.badging`
   1. 選擇保 **存**



![chlimage_1-193](assets/chlimage_1-193.png)

要查看日誌條目

* 從Web Console

   * 在**狀態**菜單下
   * 選擇 **日誌檔案**
   * 搜尋您的記錄檔名稱，例如 `scoring-debug`

* 在伺服器的本地磁碟上

   * 日誌檔案位於&lt;*server-install-dir*>/crx-quickstart/logs/&lt;*log-file-name*>.log

   * 例如， `.../crx-quickstart/logs/scoring-debug.log`

![chlimage_1-194](assets/chlimage_1-194.png)

## UGC的計分與簽章 {#ugc-for-scoring-and-badging}

當選擇的SRP是JSRP或MSRP，但不是ASRP時，可以查看與計分和標籤相關的UGC。 (如果不熟悉這些術語，請參 [閱社群內容儲存](/help/communities/working-with-srp.md)[和儲存資源提供者概述](/help/communities/srp.md)。)

存取計分和標籤資料的說明使用JSRP，因為UGC可使用 [CRXDE Lite輕鬆存取](/help/sites-developing/developing-with-crxde-lite.md)。

**作者JSRP** :在作者環境中進行實驗會產生只有作者環境才能看到的UGC。

**發佈時的JSRP** :同樣地，如果在發佈環境上進行測試，則必須以發佈實例的管理權限訪問CRXDE Lite。 如果發佈例項在生產模 [式](/help/sites-administering/production-ready.md) （nosamplecontent執行模式）中執行 [，則必須啟](/help/sites-administering/enabling-crxde-lite.md)用CRXDE Lite。

UGC在JSRP上的基本位置為 `/content/usergenerated/asi/jcr/`。

### 計分和標籤API {#scoring-and-badging-apis}

下列API可供使用：

* [com.adobe.cq.sosical.scoring.api](https://docs.adobe.com/content/docs/en/aem/6-3/develop/ref/javadoc/com/adobe/cq/social/scoring/api/package-summary.html)
* [com.adobe.cq.social.badging.api](https://docs.adobe.com/content/docs/en/aem/6-3/develop/ref/javadoc/com/adobe/cq/social/badging/api/package-summary.html)

Adobe儲存庫的開發人員可使用已安裝功能套件的最新Javadoc。 請參 [閱使用Maven for Communities:Javadocs](/help/communities/maven.md#javadocs)。

**UGC在儲存庫中的位置和格式可能會變更，但不會發出警告**。

### 範例設定 {#example-setup}

儲存庫資料的螢幕擷取畫面來自於在兩個不同AEM網站上設定評分和標籤論壇：

1. 具有唯一 *ID* （使用精靈建立的社群網站）的AEM網站：

* 使用在快速入門教學課程中建立的快速入門教學課程(參 [與)網站](/help/communities/getting-started.md)
* 找到論壇頁面節點

   * `/content/sites/engage/en/forum/jcr:content`

* 添加計分和標籤屬性

       &quot;
    規則= [/etc/community/rules/comments得分，
 etc/communts得分，社群／論壇……     &quot;規則=
 [/badging etc/communts/badging註解，等等——評分／評分論壇／評分規則／評分，     
    
    
    
    
    等／社群／論壇。
   
* 找到論壇元件節點

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

* 新增屬性以顯示標章

   * `allowBadges = true`

* 使用者登入、建立論壇主題，並獲得銅製徽章

1. 沒有唯一 *ID* 的AEM網站：

* 使用社 [群元件指南](/help/communities/components-guide.md)
* 找到論壇頁面節點

   * `/content/community-components/en/forum/jcr:content`

* 添加計分和標籤屬性

   ```
       scoringRules = [/etc/community/scoring/rules/comments-scoring,
        /etc/community/scoring/rules/forums-scoring]
       ```
   
       ```
       badgingRules =[/etc/community/badging/rules/comments-scoring,
        /etc/community/badging/rules/forums-scoring]
       ```
   
* 找到論壇元件節點

   * `/content/community-components/en/forum/jcr:content/content/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

* 新增屬性以顯示標章

   * `allowBadges = true`

* 使用者登入、建立論壇主題，並獲得銅製徽章

1. 使用cURL為使用者指派協調者徽章：

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/etc/community/badging/images/moderator/jcr:content/moderator.png" https://localhost:4503/home/users/community/w271OOup2Z4DjnOQrviv/profile.social.json
```

由於使用者已獲得兩枚銅製徽章，並獲得協調者徽章，因此使用者在論壇項目中的呈現方式如下：

![chlimage_1-195](assets/chlimage_1-195.png)

>[!NOTE]
>
>此範例不遵循下列最佳實務：
>
>* 計分規則名稱應全局唯一；他們不應以同名結尾。
   >  *not *to的範例：
   >  /etc/community/scoring/rules/site1/forums-scoring
   >  /etc/community/scoring/rules/site2/forums-scorning
   >
   >
* 為不同的AEM網站建立獨特的徽章影像
>



### 存取計分UGC {#access-scoring-ugc}

建議使 [用](#scoring-and-badging-apis) API。

為了調查目的，在範例中使用JSRP，包含分數的基本資料夾是

* `/content/usergenerated/asi/jcr/scoring`

的子節點 `scoring`是計分規則名稱。 因此，最佳實務是，伺服器上的計分規則名稱是全域唯一的。

對於Geometrixx Engage網站，使用者及其分數位於路徑中，路徑包含計分規則名稱、社群網站的網站ID( `engage-ba81p`)、唯一ID和使用者ID:

* `.../scoring/forums-scoring/engage-ba81p/6d179715c0e93cb2b20886aa0434ca9b5a540401/riley`

對於社群元件指南網站，使用者及其分數位於使用計分規則名稱、預設ID( `default-site`)、唯一ID和使用者ID建構的路徑中：

* `.../scoring/forums-scoring/default-site/b27a17cb4910a9b69fe81fb1b492ba672d2c086e/riley`

分數會儲存在屬性中， `scoreValue_tl` 該屬性可能僅直接包含值或間接引用atomicCounter。

![chlimage_1-196](assets/chlimage_1-196.png)

### 存取標籤UGC {#access-badging-ugc}

建議使 [用](#scoring-and-badging-apis) API。

為了調查目的，以JSRP為例，包含已指派或已授予徽章資訊的基本資料夾是

* /content/usergenerated/asi/jcr

後面是使用者描述檔的路徑，結尾為標章檔案夾，例如

* /home/users/community/w271OOup2Z4DjnOQrviv/profile/badges

#### 獎章 {#awarded-badge}

![chlimage_1-197](assets/chlimage_1-197.png)

#### 已指派徽章 {#assigned-badge}

![chlimage_1-198](assets/chlimage_1-198.png)

## 其他資訊 {#additional-information}

要根據點顯示排序的成員清單：

* [榜單功能](/help/communities/functions.md#leaderboard-function) ，可加入社群網站或群組範本。
* [Leerboard component](/help/communities/enabling-leaderboard.md), the featured component of the Leerboard function, for page authoring.

