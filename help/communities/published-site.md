---
title: 體驗發佈網站
seo-title: 體驗發佈網站
description: 瀏覽至已發佈的網站
seo-description: 瀏覽至已發佈的網站
uuid: 44594e9e-27ad-475d-953d-3611b04f0df8
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: dd0cbc05-a361-46bc-b9f1-d045f8f23890
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 體驗發佈網站 {#experience-the-published-site}

## 瀏覽至發佈時的新網站 {#browse-to-new-site-on-publish}

現在新建立的社群網站已經發佈，請瀏覽至建立網站時顯示的URL，但瀏覽至發佈伺服器，例如

* 作者URL = https://localhost:4502/content/sites/engage/en.html
* 發佈URL = https://localhost:4503/content/sites/engage/en.html

為了盡量避免使用者在作者和發佈上登入哪些會員的混淆，建議針對每個例項使用不同的瀏覽器。

首次到達發佈網站時，網站訪客通常尚未登入，且是匿名的。

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![chlimage_1-31](assets/chlimage_1-31.png)

## 匿名網站訪客 {#anonymous-site-visitor}

匿名網站訪客在UI中會看到下列內容：

* 網站的標題。 哪些是快速入門教學課程
* 無描述檔連結
* 無消息連結
* 無通知連結
* 搜尋欄位
* 登入連結
* 品牌橫幅
* 「參考站點模板」中包含的元件的菜單連結

如果您選取各種連結，您會發現這些連結是唯讀模式。

### 防止對JCR的匿名訪問 {#prevent-anonymous-access-on-jcr}

已知限制會透過jcr內容和json將社群網站內容公開給匿名訪客， **但允許匿名存取** ，網站內容則會停用。 不過，這個行為可以使用Sling Restrictions做為因應措施加以控制。

若要保護您的社群網站內容不受匿名使用者透過jcr內容和json存取，請遵循下列步驟：

1. 在「AEM作者」例項上，請前往https://&lt;host>:&lt;port>/editor.html/content/site/&lt;sitename>.html。

   >[!NOTE]
   >
   >請勿前往本地化網站。

1. 前往「頁 **面屬性」**。

   ![站點驗證](assets/site-authentication.png)

1. 前往**進階**標籤。

   ![page-properties](assets/page-properties.png)

1. 啟用 **驗證要求**。
1. 新增登入頁面的路徑。 例如，**/content/......./GetStarted**.
1. 發佈頁面。

## 受信任的社群成員 {#trusted-community-member}

本體驗假設 [Aaron mcDonald](/help/communities/tutorials.md#demo-users) 被指派為社群經 [理和協調者的角色](/help/communities/create-site.md#roles)。 如果沒有，請返回作者環境以修 [改網站設定](/help/communities/sites-console.md#modifying-site-properties) ，並選擇Aaron mcDonald擔任社群經理和協調者。

在右上角，選取並 `Log in`使用使用者名稱「aaron.mcdonald@mailinator.com」和密碼「password」簽署。 請注意，使用Twitter或Facebook認證登入的能力。

![chlimage_1-32](assets/chlimage_1-32.png)

以註冊社群成員身分登入後，請注意下列功能表項目，以點選並探索您的社群網站：

* **設定檔** 選項可讓您檢視和編輯您的設定檔。
* [消息](/help/communities/configure-messaging.md) 選項將引導您到直接消息傳送部分，您可以在其中：

1. 檢視您收到的直接訊息（收件匣）、傳送的訊息（已傳送的項目）和刪除的訊息（垃圾桶）。
1. 編寫新的直接訊息，以傳送給個人和群組。

* [通知](/help/communities/notifications.md) (Notifications)選項會引導您前往通知區段，您可在此處檢視感興趣的事件並編輯通知設定。
* [管理](/help/communities/published-site.md#moderationlink) （如果您有協調權限）可將您導向「AEM Communities協調頁面」。

![chlimage_1-33](assets/chlimage_1-33.png)

請注意，「日曆」頁面是首頁，因為選擇的「參考網站範本」會先包含「日曆」功能，接著是「活動串流」功能、「論壇」功能等。 此結構可從「網站範本」 [控制台](/help/communities/sites.md#edit-site-template) ，或在作者環境中修改網站屬性時顯示：

![chlimage_1-34](assets/chlimage_1-34.png)

>[!NOTE]
>
>有關Communities元件和功能的詳細資訊，請造訪
>
>* [社群元件](/help/communities/author-communities.md) （適用於作者）
>* [元件、功能和功能基本工具](/help/communities/essentials.md) （適用於開發人員）
>



### 論壇連結 {#forum-link}

選擇「論壇」連結，以檢視基本論壇功能。

成員可以發佈新主題或關注主題。

網站訪客可以檢視貼文，並以多種方式加以排序。

![chlimage_1-35](assets/chlimage_1-35.png)

### 群組連結 {#groups-link}

由於Aaron是群組管理員，選擇「群組」連結可讓Aaron透過選擇群組範本、影像、群組是開啟還是機密，以及邀請成員來建立新的社群群組。

這是在發佈環境中建立群組的範例。

群組也可以在作者環境中建立，並在作者環境的社群網站(社群群組主控台 [](/help/communities/groups.md))中管理。 本教學課程 [提供在作者上建立群組](/help/communities/nested-groups.md) 的後續經驗。

![chlimage_1-36](assets/chlimage_1-36.png)

建立參考群組：

1. 選擇 **新群組**
1. **「設定」頁籤**

   * 群組名稱 : `Sports`
   * 說明 : `A parent group for various sporting groups`
   * 群組 URL 名稱 : `sports`
   * 選擇 `Open Group` （允許任何社區成員通過加入參與）

1. **範本標籤**

   * 選擇 `Reference Group` （在其結構中包含組函式以允許嵌套組）

1. 選擇 **建立群組**

![chlimage_1-37](assets/chlimage_1-37.png)

建立新群組後，請選 **取新的「運動」群組** ，以便在其中建立兩個群組（巢狀）。 由於網站結構不能以群組功能開始，在開啟「運動」群組後，必須選取「群組」連結：

![chlimage_1-38](assets/chlimage_1-38.png)

第二組連結(從開 `Blog`始)屬於目前選取的群 `Sports`組。 選取「運動」(Sports) `Groups` 連結後，就可在「運動」(Sports)群組內巢狀內嵌兩個群組。

例如，新增兩個n `ew groups.`

* 一個 `Baseball`

   * 保留為(必要 `Open Group` 會籍)
   * 在「模板」頁籤上，選擇 `Conversational Group`

* 一個 `Gymnastics`

   * 將其設定變更為 `Member Only Group` （受限制會籍）
   * 在「模板」頁籤上，選擇 `Conversational Group`

**注意 **:

* 在顯示兩個群組之前，可能需要重新整理頁面
* 此範本不*not *include groups function，因此不可能再建立群組巢狀結構
* 在作者上，「群 [組控制台](/help/communities/groups.md) 」提供第三種選擇- `Public Group` （選用會籍）

建立兩個群組後，請選取「棒球」群組、開啟的群組，並注意其連結：

`Discussions` `What's New` `Members`

群組的連結會顯示在主網站的連結下方，並產生下列顯示：

![chlimage_1-39](assets/chlimage_1-39.png)

在作者上——具有管理權限，導覽至 [Communities Groups主控台](/help/communities/members.md) ，並將Weston mcCall新增至 `Community Engage Gymnastics <uid> Members` 群組。

繼續發佈時，以Aaron mcDonald的身分登出，並以匿名網站訪客的身分檢視運動群組：

* 從首頁開始
* 選取連 `Groups`結
* 選取連 `Sports`結
* 選擇「運動」(Sports) `Groups`連結

只會顯示棒球群組。

以Weston mcCall(weston.mccall@dodgit.com /密碼)的身分登入，並導覽至相同的位置。 請注意，Weston可以使用 `Join` 開啟的 `Baseball` 群組和 `enter or Leave` 私人 `Gymnastics`群組。

![chlimage_1-40](assets/chlimage_1-40.png)

### 網頁連結 {#web-page-link}

選取「網頁」連結，即可檢視網站所包含的基本網頁。 標準的AEM製作工具可用來在作者環境中將內容新增至此頁面。

例如，前往作 **者例項** ，在 `engage` Communities Sites主控台中開啟資料夾 [，選取「開啟網站](/help/communities/sites-console.md)**** 」圖示以進入作者編輯模式。 然後選取預覽模式以選取連 `Web Page`結，然後選取編輯模式以新增標題和文字元件。 最後，只重新發佈頁面或整個網站。

![chlimage_1-41](assets/chlimage_1-41.png)

### 協調連結 {#moderationlink}

當社群成員擁有協調權限時，「協調」連結就會顯示，選取該連結將顯示已張貼的社群內容，並允許其以類似於作者環境中的 [協調控制台的方式協調](/help/communities/moderate-ugc.md)[](/help/communities/moderation.md) 。

使用瀏覽器的「上一步」按鈕可返回已發佈的網站。 在發佈環境中，大多數控制台都無法從全局導航訪問。 [](/help/communities/moderate-ugc.md)

![chlimage_1-42](assets/chlimage_1-42.png)

## 自助註冊 {#self-registration}

登出後，可建立新的使用者註冊。

* select `Log In`
* select `Sign up for a new account`

![chlimage_1-43](assets/chlimage_1-43.png) ![chlimage_1-44](assets/chlimage_1-44.png)

依預設，電子郵件地址為登入ID。 若未勾選，訪客可輸入其專屬的登入ID（使用者名稱）。 使用者名稱在發佈環境中必須是唯一的。

在指定使用者名稱、電子郵件和密碼後，選取會 `Sign Up`建立使用者並讓他們簽名。

登入後，第一頁即為其頁面， `Profile`可供他們個人化。

![chlimage_1-45](assets/chlimage_1-45.png)

如果成員忘記其登錄ID，則可以使用其電子郵件地址進行恢復。

![chlimage_1-46](assets/chlimage_1-46.png)

