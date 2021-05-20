---
title: 體驗已發佈的網站
seo-title: 體驗已發佈的網站
description: 瀏覽已發佈的啟用網站
seo-description: 瀏覽已發佈的啟用網站
uuid: 1bfefa8a-fd9c-4ca8-b2ff-add79776c8ae
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 26715b94-e2ea-4da7-a0e2-3e5a367ac1cd
exl-id: 801416ed-d321-45a2-8032-8935094a4d44
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 1%

---

# 體驗已發佈的網站{#experience-the-published-site}


**[⇐建立並指派啟用資源](resource.md)**

## 瀏覽到發佈時的新網站{#browse-to-new-site-on-publish}

現在，新建立的社群網站及其啟用資源和學習路徑已經發佈完畢，您就可以體驗啟用教學課程網站。

首先，瀏覽至建立網站時顯示的URL，然後在發佈伺服器上，例如

* 作者URL = [http://localhost:4502/content/sites/enable/en.html](http://localhost:4502/content/sites/enable/en.html)
* 發佈URL = [http://localhost:4503/content/sites/enable/en.html](http://localhost:4503/content/sites/enable/en.html)

若已設定[預設首頁](enablement-create-site.md#changethedefaulthomepage)，則只要瀏覽至[http://localhost:4503/](http://localhost:4503/)即應啟動網站。

首次到達已發佈的網站時，網站訪客通常尚未登入，且為匿名。

**http://localhost:4503/content/sites/enable/en.html**

![啟用登入](assets/enablement-login.png)

## 匿名網站訪客{#anonymous-site-visitor}

此私人啟用社群網站的登入頁面會立即顯示匿名網站訪客。 請注意，您無法自行註冊或登入Facebook或Twitter。

請注意，首頁顯示四個功能表項目：`Assignments, Ski Catalog, What's New`和`Discussions`，但若未登入，則無法達到。

>[!NOTE]
>
>可授予對啟用網站的匿名存取權，而不允許網站訪客自行註冊。
>
>如果啟用資源設為`show in catalog`和`allow anonymous access`，則匿名網站訪客可以在目錄中檢視資源。

### 在JCR {#prevent-anonymous-access-on-jcr}上防止匿名訪問

已知限制會透過jcr內容和json向匿名訪客公開社群網站內容，不過已針對網站內容停用&#x200B;**[!UICONTROL 允許匿名存取]**。 不過，您可以使用Sling限制來控制此行為，作為因應措施。

若要保護您的社群網站內容，不讓匿名使用者透過jcr內容和json存取，請遵循下列步驟：

1. 在AEM製作例項上，前往https://&lt;host>:&lt;port>/editor.html/content/site/&lt;sitename>.html。

   >[!NOTE]
   >
   >請勿前往本地化網站。

1. 前往&#x200B;**[!UICONTROL 頁面屬性]**。

   ![page-properties](assets/page-properties.png)

1. 前往&#x200B;**[!UICONTROL 進階]**&#x200B;標籤。
1. 啟用&#x200B;**[!UICONTROL 身份驗證要求]**。

   ![站點驗證](assets/site-authentication.png)

1. 新增登入頁面的路徑。 例如， `/content/......./GetStarted`。
1. 發佈頁面。

## 已註冊成員{#enrolled-member}

此體驗依賴於`Riley Taylor`和`Sidney Croft`正在建立的[](enablement-setup.md#publishcreateenablementmembers)和[被分配](resource.md#settings)*滑雪課程*&#x200B;學習路徑的用戶，通過其&#x200B;*社區滑雪課程*&#x200B;組的成員身份。

登入方式

* `Username: riley`
* `Password: password`

如果不是通過自註冊建立用戶配置檔案，則在成員首次登錄時，將顯示其配置檔案頁，以便他們可以根據需要驗證和修改它。

下次成員登錄時，將顯示由第一個菜單項標識的首頁。

![已註冊成員](assets/enrolled-member.png)

### 指定任務 {#assignments}

在「工作總攬」頁中，會顯示成員的所有學習路徑和專門分配給它們的啟用資源。

每個分配都提供以下基本資訊：

* 分配類型
* 是否為新分配
* 名稱
* 與分配類型相關的詳細資訊
* 工作聯繫人、專家和作者（如果提供）

「分配」類型由卡片左上角的表徵圖指示。 道路的影像用於包含啟用資源數的學習路徑。

![分配1](assets/assignment1.png)

選取&#x200B;*滑雪課程*&#x200B;將顯示學習路徑所參考的兩個啟用資源。

![assigned2](assets/assignment2.png)

選擇&#x200B;*滑雪課程1*&#x200B;將開啟啟用資源的詳細資訊頁面。

從詳細資訊頁，成員能夠學習[rate](rating.md)課程並添加[注釋](comments.md)。 任何成員活動都會反映在網站的「新增功能」區段中。

與啟用資源的互動會顯示在作者環境中可存取的「報表」區段中。

![分配3](assets/assignment3.png)

### 滑雪目錄{#ski-catalog}

「滑雪目錄」頁面是使用`Tutorial`命名空間中的標籤標籤的啟用資源目錄。 兩個&#x200B;*滑雪課程*&#x200B;資源使用`Skiing`標籤進行標籤，這樣，如果選取`All`或`Tutorial: Sports / Skiing`以外的任何標籤，則不顯示任何內容。

如果未直接或通過學習路徑為成員分配啟用資源，則可以與目錄內的啟用資源交互，並通過注釋和評級提供反饋。

![滑雪目錄](assets/ski-catalog.png)

### 討論 {#discussions}

除了對啟用資源（[當啟用](enablement-create-site.md#step33asettings)時）進行評分和評論外，建立`Enablement Tutorial`的社群網站範本還包括[論壇函式](functions.md#forum-function)(標題為`Discussions)`。

選取`Discussions`連結並張貼主題。

登出並以Sidney Croft（西德尼/密碼）的身分登入並回覆問題，以及關注主題。

請注意，除了內嵌協調，還有其他選項可在社交媒體上共用主題或透過電子郵件傳送主題。

![討論](assets/discussions.png)

### 新功能 {#what-s-new}

`What's New`功能表項目是此社群網站結構中[活動資料流函式](functions.md#activity-stream-function)的標題。

仍以Sidney登入，請選取`What's New`連結以顯示活動。

![whats-new-menu](assets/whats-new-menu.png)

## 受信任的社區成員{#trusted-community-member}

此體驗假設已指派` [Quinn Harper](enablement-setup.md#publishcreateenablementmembers)`協調者](enablement-create-site.md#moderation)和[資源連絡人](resource.md#settings)的角色。[

登入方式

* `Username: quinn`
* `Password: password`

登錄後，請注意新的菜單項`Administration`出現，因為該成員被賦予版主角色。

![trusted-member-homepage](assets/trusted-member-homepage.png)

首頁由第一個菜單項「工作總攬」標識。 Quinn是版主和培訓資源聯繫人，未註冊到任何培訓資源或學習路徑中，因此沒有任何可顯示的內容。

### 管理 {#administration}

有的是兩個學習者的活動，`Riley Taylor`和`Sidney Croft`。 選取`Administration`連結以存取協調控制台，Quinn就能使用[大量協調控制台](moderation.md)來協調其貼文。

選取側面板圖示會切換開啟用於搜尋社群內容的篩選器。

將游標暫留在留言卡上會顯示協調動作。

![管理](assets/administration.png)

## 作者報告{#reports-on-author}

存取學習者報告和培訓資源有兩種方式。

在作者上，導覽至&#x200B;**Communities, [Resources console](resources.md)**，管理啟用資源，並在選取社群網站後，便可產生報表

* 所有啟用資源和學習路徑
* 一條特定的啟用資源或學習路徑

導覽至&#x200B;**Communities, [Reports console](reports.md)**，然後根據以下項目產生報表：

* 賦予啟用資源和學習路徑
* 在特定時段內張貼至社群網站
* 特定時段內社群網站的檢視（網站造訪）

* 貼文和檢視可能屬於所有內容，或特定內容：

   * 論壇
   * 論壇主題
   * QnA
   * QnA 問題
   * 部落格
   * 部落格文章
   * 日曆
   * 日曆事件

### 資源控制台{#resources-console}

只要進行一些活動並在發佈時與資源互動，就能檢視作者的報表。

* 在作者上，以管理權限登入。
* 從主功能表導覽至&#x200B;**[!UICONTROL Communities]** > **[!UICONTROL Resources]**。
* 選擇`Enablement Tutorial`站點。
* 選擇`Report`表徵圖以查看所有資源的摘要。
* 選擇資源，然後為該資源的報表選擇`Report`表徵圖。

請注意，顯示Adobe Analytics資料可能為時過早，這可能需要1到12小時的時間才會顯示。 不過，基本的SCORM報表已可供使用。

#### 滑雪課資源報告{#ski-lessons-resource-report}

![滑雪課報告](assets/ski-lessons-report.png)

#### 滑雪課程使用者報表{#ski-lessons-user-report}

* 選擇&#x200B;**[!UICONTROL Communities >資源]**

* 開啟卡片`Enablement Tutorial`
* 開啟卡片`Ski Lessons`
* 選取 `Report > User Report`

![ski-lessions-user-report](assets/ski-lessons-user-report.png)

### 報表控制台{#reports-console}

「報表」控制台可產生

* **** 任何啟用社群網站的指派
* **** 任何社群網站的檢視
* **** 任何社群網站的貼文

對於分配報表：

* 在作者上，以管理權限登入。
* 導覽至&#x200B;**[!UICONTROL Communities]** > **[!UICONTROL Reports]** > **[!UICONTROL Assignments Report]**。
* 從下拉菜單中選擇&#x200B;**[!UICONTROL 站點]**（選擇`Enablement Tutorial`）。

* 選擇&#x200B;**[!UICONTROL 組]**（選擇`Community Ski Class`）

* 選擇&#x200B;**[!UICONTROL 分配]**（選擇`Ski Lessons`）

* 選擇&#x200B;**[!UICONTROL 生成]**

![報告分配](assets/report-assignment.png)

若是檢視報表：

* 在作者上，以管理權限登入。
* 導覽至&#x200B;**[!UICONTROL Communities]** > **[!UICONTROL Reports]** > **[!UICONTROL Views Report]**。
* 從下拉菜單中選擇&#x200B;**站點**（選擇`Enablement Tutorial`）。

* 選擇&#x200B;**[!UICONTROL 內容類型]**（選擇`all`）。

* 選擇&#x200B;**[!UICONTROL 日期範圍]**（選擇`Last 7 days`）。

* 選擇&#x200B;**[!UICONTROL 生成]**。

![報表檢視](assets/report-views.png)

**[⇐建立並指派啟用資源](resource.md)**
