---
title: 體驗已發佈站點
seo-title: Experience the Published Site
description: 瀏覽到已發佈的站點
seo-description: Browse to a published site
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
source-wordcount: '1193'
ht-degree: 1%

---

# 體驗已發佈站點 {#experience-the-published-site}

## 瀏覽到發佈時的新網站 {#browse-to-new-site-on-publish}

現在新建立的社區網站已發佈，請瀏覽到建立網站時顯示的URL，但是在發佈伺服器上，例如：

* 作者URL = https://localhost:4502/content/sites/engage/en.html
* 發佈URL = https://localhost:4503/content/sites/engage/en.html

為了盡量減少關於哪個成員在作者上登錄和發佈的混亂，建議對每個實例使用不同的瀏覽器。

首次到達已發佈的站點時，站點訪問者通常不會登錄，並且是匿名的。

`https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}`

![署名](assets/authorpublished.png)

## 匿名站點訪問者 {#anonymous-site-visitor}

匿名站點訪問者在UI中看到以下內容：

* 網站標題（入門教程）
* 無配置檔案連結
* 無消息連結
* 無通知連結
* 搜索欄位
* 登錄連結
* 品牌標語
* 「參考站點模板」中包括的元件的菜單連結。

如果選擇了各種連結，則會發現它們處於只讀模式。

### 阻止對JCR的匿名訪問 {#prevent-anonymous-access-on-jcr}

已知限制通過jcr內容和json向匿名訪問者公開社區網站內容，但 **允許匿名訪問** 已為站點內容禁用。 但是，可以使用Sling Restrictions作為變通方法來控制此行為。

要保護社區網站的內容免受匿名用戶通過jcr內容和json的訪問，請執行以下步驟：

1. 在AEM Author實例上，轉到https:// hostname:port/editor.html/content/site/sitename.html。

   >[!NOTE]
   >
   >不要轉到本地化網站。

1. 轉到 **頁面屬性**。

   ![頁屬性](assets/page-properties.png)

1. 轉到 **高級** 頁籤。

1. 啟用 **身份驗證要求**。

   ![站點驗證](assets/site-authentication.png)

1. 添加登錄頁的路徑。 比如說， **/content/......。/GetStarted**。
1. 發佈頁面。

## 受信任的社區成員 {#trusted-community-member}

此經驗假定 [亞倫·麥克唐納](/help/communities/tutorials.md#demo-users) 已分配角色 [社區經理和主持人](/help/communities/create-site.md#roles)。 否則，返回作者環境以 [修改站點設定](/help/communities/sites-console.md#modifying-site-properties) 選擇艾倫·麥克唐納為社區經理和主持人。

在右上角，選擇 `Log in`，並使用用戶名(aaron.mcdonald@mailinator.com)和密碼（密碼）登錄。 請注意使用Twitter或Facebook憑據登錄的能力。

![登錄](assets/login.png)

以註冊的社區成員身份登錄後，請注意以下菜單項以按一下並瀏覽您的社區站點：

* **配置檔案** 頁籤。
* [消息](/help/communities/configure-messaging.md) 選項可指導您直接發送消息，您可以在其中：

   1. 查看您收到的直接郵件（收件箱）、發送的郵件（已發送的郵件）和刪除的郵件（垃圾）。
   1. 編寫要發送到個人和組的新直接消息。

* [通知](/help/communities/notifications.md) 選項將引導您進入「通知」部分，在該部分中可以查看您關心的事件並編輯通知設定。
* [管理](/help/communities/published-site.md#moderationlink) 如果您具有審核權限，則將引導您到AEM Communities審核頁。

![管理螢幕](assets/adminscreen.png)

請注意，「日曆」頁是首頁，因為所選的「參考站點模板」首先包含「日曆」功能，然後是「活動流」功能、「論壇」功能等。 此結構可從 [站點模板](/help/communities/sites.md#edit-site-template) 控制台或修改作者環境中的站點屬性時：

![站點模板](assets/sitetemplate.png)

>[!NOTE]
>
>有關社區組成部分和功能的詳細資訊，請訪問：
>
>* [社區元件](/help/communities/author-communities.md) （供作者使用）
>* [元件、函式和功能要素](/help/communities/essentials.md) （對於開發人員）


### 論壇連結 {#forum-link}

通過選擇「論壇」連結查看基本論壇功能。

成員可以發佈新主題或關注主題。

站點訪問者可以查看帖子並以各種方式對其進行排序。

![forumlink](assets/forumlink.png)

### 組連結 {#groups-link}

由於Aaron是組管理員，選擇「組」連結將允許Aaron通過選擇組模板、影像、組是開啟還是保密以及邀請成員來建立新的社區組。

這是在發佈環境中建立組的示例。

也可以在作者環境中建立組並在作者環境中的社區站點中進行管理([團體組控制台](/help/communities/groups.md))。 A. [建立作者組](/help/communities/nested-groups.md) 是本教程的下一個。

![粗鏈](assets/grouplink.png)

建立引用組：

1. 選擇 **新建組**
1. **「設定」頁籤**

   * 群組名稱 : `Sports`
   * 說明 : `A parent group for various sporting groups`.
   * 群組 URL 名稱 : `sports`
   * 選擇 `Open Group` (允許任何社區成員通過加入參與

1. **「模板」頁籤**

   * 選擇 `Reference Group` （在其結構中包含允許嵌套組的組函式）

1. 選擇 **建立組**

   ![建立組](assets/creategroup.png)

建立新組後， **選擇新的「體育」組** 以便在其中建立兩個組（嵌套）。 由於網站結構不能從組功能開始，開啟體育組後，需要選擇「組」連結：

![grouplink1](assets/grouplink1.png)

第二組連結，以 `Blog`，屬於當前選定的組， `Sports` 組。 通過選擇體育 `Groups` 連結，可以在運動組內嵌套兩個組。

例如，添加兩個 `new groups`。

* 一個名為 `Baseball`

   * 將其設定為 `Open Group` （必需的成員資格）。
   * 在「模板」頁籤上，選擇 `Conversational Group`。

* 一個名為 `Gymnastics`

   * 將其設定更改為 `Member Only Group` （限製成員）。
   * 在「模板」頁籤上，選擇 `Conversational Group`。

**注意**:

* 在顯示兩個組之前可能需要刷新頁面。
* 此模板可 *不* 包括組函式，因此不可能再進行組嵌套。
* 作者， [組控制台](/help/communities/groups.md) 提供了第三個選擇 — a `Public Group` （可選成員）。

建立兩個組後，選擇開啟的組「棒球」組，並注意其連結：

`Discussions` `What's New` `Members`

組的連結顯示在主站點的連結下方，並導致以下顯示：

![grouplink2](assets/grouplink2.png)

作者 — 具有管理權限，導航至 [社區組控制台](/help/communities/members.md) 然後把韋斯頓·麥考爾 `Community Engage Gymnastics <uid> Members` 組。

繼續發佈，以Aaron McDonald的身份註銷，並以匿名網站訪問者的身份查看體育組中的組：

* 從首頁
* 選擇 `Groups` 連結
* 選擇 `Sports` 連結
* 選擇體育 `Groups` 連結

只有棒球組才可見。

以Weston McCall(weston.mccall@dodgit.com /密碼)身份登錄，並導航到相同位置。 注意威斯頓能 `Join` 開啟 `Baseball` 組 `enter or Leave` 私人 `Gymnastics` 組。

![grouplink3](assets/grouplink3.png)

### 網頁連結 {#web-page-link}

通過選擇「網頁」連結查看網站中包含的基本網頁。 標準創AEM作工具可用於在作者環境中將內容添加到此頁面。

例如，轉到 **作者** 實例，開啟 `engage` 資料夾 [社區站點控制台](/help/communities/sites-console.md)，選擇 **開啟網站** 表徵圖以進入作者編輯模式。 然後選擇預覽模式以選擇 `Web Page` 連結，然後選擇編輯模式以添加標題和文本元件。 最後，只發佈頁面或整個網站。

![網頁連結](assets/webpagelink.png)

### 審核連結 {#moderationlink}

當社區成員具有審核權限時，「審核」連結將可見，選擇該連結將顯示已發佈的社區內容，並允許它 [已](/help/communities/moderate-ugc.md) 與 [調節控制台](/help/communities/moderation.md) 在作者環境中。

使用瀏覽器的「後退」按鈕返回到已發佈的站點。 大多數控制台無法從發佈環境中的全局導航訪問。

![現代化連結](assets/moderationlink.png)

## 自註冊 {#self-registration}

註銷後，可以建立新用戶註冊。

* 選取 `Log In`
* 選取 `Sign up for a new account`

![登記](assets/registration.png)

![註冊](assets/signup.png)

預設情況下，電子郵件地址為登錄ID。 如果未選中，訪問者可以輸入自己的登錄ID（用戶名）。 用戶名在發佈環境中必須唯一。

指定用戶名、電子郵件和密碼後，選擇 `Sign Up` 將建立用戶並使其能夠簽名。

登錄後，顯示的第一頁是 `Profile` 頁面，他們可以個性化。

![側面像](assets/profile.png)

如果成員忘記了其登錄ID，則可能使用其電子郵件地址進行恢復。

![forgotusername](assets/forgotusername.png)
