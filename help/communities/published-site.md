---
title: 體驗已發佈的網站
seo-title: 體驗已發佈的網站
description: 瀏覽到已發佈的站點
seo-description: 瀏覽到已發佈的站點
uuid: 44594e9e-27ad-475d-953d-3611b04f0df8
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: dd0cbc05-a361-46bc-b9f1-d045f8f23890
docset: aem65
exl-id: ebc4e1e7-34f0-4f4e-9f00-178dfda23ce4
source-git-commit: 840ea373537799af995c3b8ce0c8bf575752775b
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 1%

---

# 體驗已發佈的網站 {#experience-the-published-site}

## 在發佈時瀏覽到新站點 {#browse-to-new-site-on-publish}

現在新建立的社群網站已發佈完畢，請瀏覽至建立網站時顯示的URL，但在發佈伺服器上，例如：

* 作者URL = https://localhost:4502/content/sites/engage/en.html
* 發佈URL = https://localhost:4503/content/sites/engage/en.html

為了盡可能避免使用者對哪個成員在製作和發佈上登入的混淆，建議對每個例項使用不同的瀏覽器。

首次到達已發佈的網站時，網站訪客通常尚未登入，且為匿名。

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![已發佈](assets/authorpublished.png)

## 匿名網站訪客 {#anonymous-site-visitor}

匿名網站訪客在UI中看到下列內容：

* 網站標題（快速入門教學課程）
* 無個人資料連結
* 無消息連結
* 無通知連結
* 搜尋欄位
* 登入連結
* 品牌橫幅
* 「參考站點模板」中包含的元件的菜單連結。

如果您選取各種連結，您會發現這些連結處於唯讀模式。

### 在JCR上防止匿名訪問 {#prevent-anonymous-access-on-jcr}

已知限制會透過jcr內容和json向匿名訪客公開社群網站內容，不過已針對網站內容停用&#x200B;**允許匿名存取**。 不過，您可以使用Sling限制來控制此行為，作為因應措施。

若要保護您的社群網站內容，不讓匿名使用者透過jcr內容和json存取，請遵循下列步驟：

1. 在AEM Author例項上，前往https://主機名稱：port/editor.html/content/site/sitename.html。

   >[!NOTE]
   >
   >請勿前往本地化網站。

1. 前往&#x200B;**頁面屬性**。

   ![page-properties](assets/page-properties.png)

1. 前往&#x200B;**進階**&#x200B;標籤。

1. 啟用&#x200B;**身份驗證要求**。

   ![站點驗證](assets/site-authentication.png)

1. 新增登入頁面的路徑。 例如， **/content/......./GetStarted**。
1. 發佈頁面。

## 受信任的社區成員 {#trusted-community-member}

此體驗假設[Aaron McDonald](/help/communities/tutorials.md#demo-users)已獲派[社群經理和主持人](/help/communities/create-site.md#roles)的角色。 若未包含，請返回作者環境以[修改網站設定](/help/communities/sites-console.md#modifying-site-properties)，並選取Aaron McDonald作為社群經理和協調者。

在右上角，選擇`Log in`，並使用用戶名(aaron.mcdonald@mailinator.com)和密碼（密碼）進行簽名。 請注意使用Twitter或Facebook憑證登入的功能。

![登入](assets/login.png)

以註冊的社群成員身份登錄後，請注意以下菜單項，以點擊並瀏覽您的社群站點：

* **** 設定檔選項可讓您檢視和編輯您的設定檔。
* [](/help/communities/configure-messaging.md) 訊息選項會將您導向直接傳訊區段，您可在此處：

   1. 檢視您收到的直接訊息（收件匣）、已傳送（已傳送項目）和已刪除（清除）。
   1. 撰寫新的直接訊息以傳送至個人和群組。

* [](/help/communities/notifications.md) 通知選項會將您導向通知區段，您可在此檢視所關心的事件並編輯通知設定。
* [](/help/communities/published-site.md#moderationlink) 如果您有協調權限，管理會將您導向至AEM Communities協調頁面。

![adminscreen](assets/adminscreen.png)

請注意，「日曆」頁面是首頁，因為選擇的「參考網站範本」會先包含「日曆」功能，接著是「活動資料流」功能、「論壇」功能等。 此結構可從[網站範本](/help/communities/sites.md#edit-site-template)控制台或在製作環境中修改網站屬性時顯示：

![網站範本](assets/sitetemplate.png)

>[!NOTE]
>
>如需Communities元件和功能的詳細資訊，請造訪：
>
>* [Communities元件](/help/communities/author-communities.md) （適用於作者）
>* [元件、函式和功能要點](/help/communities/essentials.md) （適用於開發人員）


### 論壇連結 {#forum-link}

通過選擇「論壇」連結查看基本論壇功能。

成員可以發佈新主題或關注主題。

網站訪客可檢視貼文，並以各種方式加以排序。

![forumlink](assets/forumlink.png)

### 群組連結 {#groups-link}

由於Aaron是組管理員，因此選擇「組」連結將允許Aaron通過選擇組模板、影像、組是開啟還是秘密以及邀請成員來建立新的社區組。

這是在發佈環境中建立群組的範例。

群組也可在製作環境中建立，並在製作環境的社群網站內進行管理（[社群群組主控台](/help/communities/groups.md)）。 本教學課程的下一個體驗是在作者](/help/communities/nested-groups.md)上建立群組。[

![groupling](assets/grouplink.png)

建立參考群組：

1. 選擇&#x200B;**新組**
1. **設定標籤**

   * 群組名稱 : `Sports`
   * 說明 : `A parent group for various sporting groups`.
   * 群組 URL 名稱 : `sports`
   * 選擇`Open Group`（允許任何社區成員通過加入來參與）

1. **範本索引標籤**

   * 選擇`Reference Group`（在其結構中包含允許嵌套組的組函式）

1. 選擇&#x200B;**建立組**

   ![creategroup](assets/creategroup.png)

建立新組後，選擇新的運動組&#x200B;**以在其中建立兩個組（嵌套）。**&#x200B;由於網站結構不能以群組功能開頭，因此在開啟「運動」群組後，必須選取「群組」連結：

![grouplink1](assets/grouplink1.png)

從`Blog`開始的第二組連結屬於當前選擇的組`Sports`組。 選取「運動」`Groups`連結，即可在「運動」群組內巢狀內嵌兩個群組。

例如，新增兩個`new groups`。

* 名為`Baseball`的

   * 將其設為`Open Group`（必要的成員資格）。
   * 在「模板」頁簽上，選擇`Conversational Group`。

* 名為`Gymnastics`的

   * 將其設定變更為`Member Only Group`（限製成員資格）。
   * 在「模板」頁簽上，選擇`Conversational Group`。

**注意**:

* 在顯示兩個群組之前，可能需要重新整理頁面。
* 此範本&#x200B;*不*&#x200B;包含群組函式，因此無法進一步巢狀群組。
* 在作者上，[群組主控台](/help/communities/groups.md)提供第三個選項 — `Public Group`（選用成員資格）。

建立兩個群組後，請選取「棒球」群組、一個開啟的群組，並注意其連結：

`Discussions` `What's New` `Members`

群組的連結會顯示在主要網站的連結下方，並產生下列顯示結果：

![grouplink2](assets/grouplink2.png)

在作者上 — 具有管理權限，導覽至[Communities Groups主控台](/help/communities/members.md)，並將Weston McCall新增至`Community Engage Gymnastics <uid> Members`群組。

繼續發佈，登出Aaron McDonald，並以匿名網站訪客的身分檢視運動群組：

* 從首頁
* 選擇`Groups`連結
* 選擇`Sports`連結
* 選取「運動」 `Groups`連結

只有棒球群組會顯示。

以Weston McCall(weston.mccall@dodgit.com /密碼)登入，並導覽至相同位置。 請注意，Weston能夠`Join`開啟的`Baseball`組和`enter or Leave`專用`Gymnastics`組。

![grouplink3](assets/grouplink3.png)

### 網頁連結 {#web-page-link}

通過選擇「網頁」連結查看網站中包含的基本網頁。 標準AEM製作工具可用來在製作環境中將內容新增至此頁面。

例如，前往&#x200B;**author**&#x200B;例項，在[Communities Sites主控台](/help/communities/sites-console.md)中開啟`engage`資料夾，選取&#x200B;**Open Site**&#x200B;圖示以進入作者編輯模式。 然後，選擇預覽模式以選擇`Web Page`連結，然後選擇編輯模式以添加標題和文本元件。 最後，只重新發佈頁面或整個網站。

![webpagelink](assets/webpagelink.png)

### 協調連結 {#moderationlink}

當社群成員擁有協調權限時，則會顯示「協調」連結，並選取該連結時，會顯示已張貼的社群內容，並允許其以類似於製作環境中[協調控制台](/help/communities/moderation.md)的方式來協調](/help/communities/moderate-ugc.md)。[

使用瀏覽器的返回按鈕返回已發佈的網站。 發佈環境中無法從全域導覽存取大部分的主控台。

![協調連結](assets/moderationlink.png)

## 自註冊 {#self-registration}

登出後，可以建立新的使用者註冊。

* 選取 `Log In`
* 選取 `Sign up for a new account`

![註冊](assets/registration.png)

![註冊](assets/signup.png)

依預設，電子郵件地址為登入ID。 如果取消勾選，訪客可以輸入自己的登入id（使用者名稱）。 使用者名稱在發佈環境中必須是唯一的。

指定用戶名、電子郵件和密碼後，選擇`Sign Up`將建立用戶並使用戶能夠簽名。

登入後，顯示的第一個頁面就是其`Profile`頁面，可供個人化。

![側面像](assets/profile.png)

如果成員忘記了其登錄ID，則可以使用其電子郵件地址進行恢復。

![forgotusername](assets/forgotusername.png)
