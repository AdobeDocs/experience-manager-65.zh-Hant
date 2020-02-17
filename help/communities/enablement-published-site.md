---
title: 體驗發佈網站
seo-title: 體驗發佈網站
description: 瀏覽至發佈網站以啟用
seo-description: 瀏覽至發佈網站以啟用
uuid: 1bfefa8a-fd9c-4ca8-b2ff-add79776c8ae
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 26715b94-e2ea-4da7-a0e2-3e5a367ac1cd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---



# 體驗發佈網站 {#experience-the-published-site}


**[‹建立和分配啟用資源](resource.md)**

## 瀏覽至發佈時的新網站 {#browse-to-new-site-on-publish}

現在，新建立的社群網站及其啟用資源和學習路徑已經發佈，您就可以體驗「啟用教學課程」網站。

首先，瀏覽至建立網站時顯示的URL，但是在發佈伺服器上，例如

* 作者URL = [http://localhost:4502/content/sites/enable/en.html](http://localhost:4502/content/sites/enable/en.html)
* 發佈URL = [http://localhost:4503/content/sites/enable/en.html](http://localhost:4503/content/sites/enable/en.html)

如果設 [定了預設首頁](enablement-create-site.md#changethedefaulthomepage)，則只要瀏覽至 [http://localhost:4503/](http://localhost:4503/) ，就應該啟動網站。

首次到達發佈網站時，網站訪客通常尚未登入，且是匿名的。

**http://localhost:4503/content/sites/enable/en.html**

![chlimage_1-433](assets/chlimage_1-433.png)

## 匿名網站訪客 {#anonymous-site-visitor}

匿名網站訪客會立即看到此私人啟用社群網站的登入頁面。 請注意，您沒有選擇自行註冊或登入Facebook或Twitter。

請注意，此首頁顯示四個功能表項目：而 `Assignments, Ski Catalog, What's New` 且， `Discussions`但若未登入，則無法達成任何目標。

>[!NOTE]
>
>不允許網站訪客自行註冊，就可授予對啟用網站的匿名存取權。
>如果啟用資源設 `show in catalog` 為 `allow anonymous access`且，匿名網站訪客將可檢視目錄中的資源。

### 防止對JCR的匿名訪問 {#prevent-anonymous-access-on-jcr}

已知限制會透過jcr內容和json將社群網站內容公開給匿名訪客， **[!UICONTROL 但允許匿名存取]** ，網站內容則會停用。 不過，這個行為可以使用Sling Restrictions做為因應措施加以控制。

若要保護您的社群網站內容不受匿名使用者透過jcr內容和json存取，請遵循下列步驟：

1. 在「AEM作者」例項上，請前往https://&lt;host>:&lt;port>/editor.html/content/site/&lt;sitename>.html。

   >[!NOTE]
   >
   >請勿前往本地化網站。

1. 前往「頁 **[!UICONTROL 面屬性」]**。

   ![page-properties-1](assets/page-properties-1.png)

1. 前往「進 **[!UICONTROL 階]** 」標籤。
1. 啟用 **[!UICONTROL 驗證要求]**。

   ![站點驗證-1](assets/site-authentication-1.png)

1. 新增登入頁面的路徑。 例如， `/content/......./GetStarted`。
1. 發佈頁面。

## 已註冊會員 {#enrolled-member}

這一經驗依賴於 `Riley Taylor` Ski Slik Sloyss Group `Sidney Croft` 的建立 [和被指派的Ski Lessons Learning Path(Ski Lessons Learning Path)的使用者，](enablement-setup.md#publishcreateenablementmembers) 通過其 [](resource.md#settings)**** 成為Ski Class Ski group的成員。

使用

* `Username: riley`
* `Password: password`

如果用戶配置檔案不是通過自註冊建立的，則會在成員首次登錄時顯示其「配置檔案」頁，以便他們可以根據需要驗證和修改該配置檔案。

下次成員登入時，會顯示由第一個功能表項目所識別的首頁。

![chlimage_1-434](assets/chlimage_1-434.png)

### 指定任務 {#assignments}

在「工作」頁面中，會顯示成員所有專門分配給他們的學習路徑和啟用資源。

每項指派都提供基本資訊

* 指派類型
* 是否為新任務
* 名稱
* 與分配類型相關的詳細資訊
* 指派聯絡人、專家和作者（如果提供）

指派類型由卡片左上角的圖示指示。 道路的影像是用於學習路徑，其中包含的支援資源數量。

![chlimage_1-435](assets/chlimage_1-435.png)

選取 *滑雪課程* ，將會顯示學習路徑所參照的兩個啟用資源。

![chlimage_1-436](assets/chlimage_1-436.png)

選擇 *滑雪課程1* 將開啟啟用資源的詳細資訊頁面。

在詳細資訊頁面中，會員可以學習、評 [分課](rating.md) ，並新增注 [釋](comments.md)。 任何會員活動都會反映在網站的「新增功能」區段中。

與啟用資源的互動將記錄在作者環境中可存取的「報表」區段中。

![chlimage_1-437](assets/chlimage_1-437.png)

### 滑雪目錄 {#ski-catalog}

「滑雪目錄」頁面是使用命名空間標籤的啟用資源 `Tutorial` 目錄。 這兩個 *滑雪課程資源都使用標* 記加上標籤，如果選取了或以外的任何標籤，則不 `Skiing` 會顯示任 `All``Tutorial: Sports / Skiing` 何內容。

如果沒有直接或通過學習路徑為成員分配啟用資源，則可以與位於目錄內的啟用資源交互，並通過注釋和分級提供反饋。

![chlimage_1-438](assets/chlimage_1-438.png)

### 討論 {#discussions}

除了對啟用資源評分和加上註解([啟用](enablement-create-site.md#step33asettings))外，從中建立的社群網站范 `Enablement Tutorial` 本還包含論壇 [功能](functions.md#forum-function) (標題為 `Discussions)`。

選取連 `Discussions`結並張貼主題。

以Sidney Croft（sidney /密碼）的身分登出並登入並回覆問題，以及關注主題。

注意，除了內嵌協調外，還有選項可供您在社交媒體上分享主題或以電子郵件傳送主題。

![chlimage_1-439](assets/chlimage_1-439.png)

### 新功能 {#what-s-new}

功 `What's New` 能表項目是此社群網站 [結構中指定活動串流功能](functions.md#activity-stream-function) 的標題。

仍以Sidney的身分登入，請選取 `What's New` 連結以顯示活動。

![chlimage_1-440](assets/chlimage_1-440.png)

## 受信任的社群成員 {#trusted-community-member}

此體驗假設 ` [Quinn Harper](enablement-setup.md#publishcreateenablementmembers)` 已指派協調者和資 [源](enablement-create-site.md#moderation)[聯絡人角色](resource.md#settings)。

使用

* `Username: quinn`
* `Password: password`

登入後，請注意會出現新的功能表項目， `Administration`因為會員被賦予協調者的角色。

![chlimage_1-441](assets/chlimage_1-441.png)

首頁由第一個菜單項「工作總攬」標識。 Quinn是協調者和啟用資源聯絡人，未註冊任何啟用資源或學習路徑，因此無需顯示任何內容。

### 管理 {#administration}

現在，兩位學員的活動， `Riley Taylor` 並選 `Sidney Croft. By s`擇 `Administration`連結以存取「協調控制台」,Quinn可以使用大量 [](moderation.md) 協調控制台來協調其貼文。

選取側面板圖示可切換開啟用於搜尋社群內容的篩選器。

將滑鼠指標暫留在留言卡上會顯示協調動作。

![chlimage_1-442](assets/chlimage_1-442.png)

## 作者報告 {#reports-on-author}

存取學員報告和啟用資源有兩種方式。

在作者上，導覽至「社 **群」、「[資源」主控台](resources.md)**，其中管理啟用資源，在選取社群網站後，就可產生報表

* 所有啟用資源和學習途徑
* 一種特定的啟用資源或學習途徑

導覽至「社 **群」、「報[告」主控台](reports.md)**，並根據

* 指派至啟用資源和學習路徑
* 在特定時段內張貼至社群網站
* 特定時段內社群網站的檢視（網站瀏覽）

* 貼文和檢視可能針對所有內容，或特定內容：

   * 論壇
   * 論壇主題
   * QnA
   * QnA 問題
   * 部落格
   * 部落格文章
   * 日曆
   * 日曆事件

### 資源控制台 {#resources-console}

只要進行一些活動，並與發佈時的「資源」互動，檢視作者的報表就值得一看。

* 論作者
* 使用管理權限登入
* 從主功能表導覽至「社群> **[!UICONTROL 資源」]**
* 選擇網 `Enablement Tutorial` 站
* 選擇所 `Report`有資源摘要的表徵圖
* 選擇資源，然後為該資 `Report`源上的報表選擇表徵圖

請注意，顯示Adobe Analytics的資料可能還為時太早，Adobe Analytics可能需要1到12小時才會顯示。 不過，基本的SCORM報表已可供使用。

#### 滑雪課程資源報告 {#ski-lessons-resource-report}

![chlimage_1-443](assets/chlimage_1-443.png)

#### 滑雪課程使用者報表 {#ski-lessons-user-report}

* 選擇 **[!UICONTROL 社群>資源]**

* 開放卡 `Enablement Tutorial`
* 開放卡 `Ski Lessons`
* `select Report, User Report`

![chlimage_1-444](assets/chlimage_1-444.png)

### 報表主控台 {#reports-console}

「報表控制台」可讓您在

* **任何啟用** 、社群網站的指派
* **任何社群網站的檢視** ,
* **任何社群網站的貼文** ,

對於分配報告：

* 論作者
* 使用管理權限登入
* 導覽至「社 **[!UICONTROL 群>報表>工作分配報表」]**
* 從下 **[!UICONTROL 拉式功能表]** (選取 `Enablement Tutorial`)中選取網站

* 選擇 **[!UICONTROL 群組]** (選擇 `Community Ski Class`)

* 選擇分 **[!UICONTROL 配]** (選擇 `Ski Lessons`)

* 選擇生 **[!UICONTROL 成]**

![chlimage_1-445](assets/chlimage_1-445.png)

若是檢視報表：

* 論作者
* 使用管理權限登入
* 導覽至「 **[!UICONTROL 社群>報表>檢視報表」]**
* 從下 **拉式功能表&#x200B;**(選取`Enablement Tutorial`)中選取網站

* 選擇 **[!UICONTROL 內容類型]** (選擇 `all`)

* 選擇日 **[!UICONTROL 期範圍]** (選擇 `Last 7 days`)

* 選擇生 **[!UICONTROL 成]**

![chlimage_1-446](assets/chlimage_1-446.png)

**[‹建立和分配啟用資源](resource.md)**
