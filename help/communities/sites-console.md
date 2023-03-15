---
title: Communities Sites主控台
seo-title: Communities Sites Console
description: 如何存取Communities Sites主控台
seo-description: How to access the Communities Sites console
uuid: 74134281-244c-40da-a941-7f2f3e706d4b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 4130f952-5bb5-4e32-91d6-47b2885b30a4
docset: aem65
role: Admin
exl-id: 426e3adf-3723-4d17-a988-6eb050939e68
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '3278'
ht-degree: 3%

---

# Communities Sites主控台 {#communities-sites-console}

Communities Sites控制台提供對以下內容的訪問：

* 網站建立
* 網站編輯
* 網站管理
* [建立和編輯巢狀群組](/help/communities/groups.md) （子社區）

請參閱 [開始使用AEM Communities](/help/communities/getting-started.md) 若要體驗在製作環境中建立社群網站的速度，以及如何從製作和發佈環境建立社群群組。

>[!NOTE]
>
>用於建立的 [社群網站](/help/communities/sites-console.md), [社群網站範本](/help/communities/sites.md), [社群群組範本](/help/communities/tools-groups.md) 和 [社群功能](/help/communities/functions.md) 僅供製作環境使用。

## 必備條件 {#prerequisites}

在建立社群網站之前，請先 *必填* 至：

* 確定一或多個發佈執行個體執行中。
* 啟用 [隧道服務](/help/communities/deploy-communities.md#tunnel-service-on-author) 管理成員和成員組。
* 識別 [主要發佈者](/help/communities/deploy-communities.md#primary-publisher).
* [配置複製](/help/communities/deploy-communities.md#replication-agents-on-author) 當主發佈器埠不是預設埠時(4503)。

最佳實務是，為確保網站已準備好支援許多功能，請採取下列步驟：

* 安裝 [最新功能套件](/help/communities/deploy-communities.md#latestfeaturepack).
* 啟用 [Adobe Analytics](/help/communities/analytics.md) AEM Communities。
* 設定 [電子郵件](/help/communities/email.md)
* 識別 [社群管理員](/help/communities/users.md#creating-community-members).
* [啟用OAuth處理常式](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler) 用於社交登入。

## 訪問Communities Sites控制台 {#accessing-communities-sites-console}

在製作環境中，若要存取Communities Sites主控台：

* 從全局導航： **[!UICONTROL 社群]** > **[!UICONTROL 網站]**

Communities Sites控制台顯示任何現有的社區站點。 在此控制台中，可以建立、編輯、管理和刪除社區站點。

要建立新的社區站點，請選擇 **建立** 表徵圖。

若要存取現有的社群網站，為了製作、修改、發佈、匯出或新增巢狀群組，請選取網站的資料夾圖示。

例如，下圖顯示主要的Communities Sites控制台，顯示兩個社群網站的資料夾： [啟用](/help/communities/getting-started-enablement.md) 和 [參與](/help/communities/getting-started.md):

![網站主控台](assets/site-console.png)

## 建立網站 {#site-creation}

網站建立主控台提供逐步方法，以根據選取的 [社群網站範本](/help/communities/sites.md) 和設定。

所建立的每個網站都包含登入功能，因為網站訪客必須先登入，才能張貼內容、傳送訊息或參與群組。 其他包含的功能包括使用者設定檔、傳訊、通知、網站功能表、搜尋、主題和品牌推廣。

程式會透過選取 `Create` 按鈕（位於Communities Sites控制台的頂部）。

建立過程是一系列步驟，以面板的形式呈現，其中包含要配置的一組特徵（以子面板的形式呈現）。 您可以前往 **下一個** 步驟或 **返回** 前一步，再在最後一步中提交網站。

### 步驟1 :網站範本 {#step-site-template}

![newsitetemplate](assets/newsitetemplate.png)

在「網站範本」面板中，會指定「標題」、「說明」、「網站根」、「基本語言」、「名稱」和「網站範本」：

* **社群網站標題**

   網站的顯示標題。

   標題會顯示在已發佈的網站上，以及網站管理員UI中。

* **社群網站說明**

   網站的說明。

   說明不會出現在已發佈的網站上。

* **社區站點根**

   網站的根路徑。

   預設根為 `/content/sites`，但根可移至網站內的任何位置。

* **社群網站基本語言**

   (單一語言不受影響：英文)使用下拉式功能表來選擇 *或更多* 可用語言的基本語言 — 德語、義大利語、法語、日語、西班牙語、葡萄牙語（巴西）、中文（繁體）和簡體中文。 系統會為每個新增的語言建立一個社群網站，並依照 [轉譯多語言網站的內容](/help/sites-administering/translation.md). 每個網站的根頁面都會包含一個子頁面，其名稱是所選語言之一的語言代碼，例如英文為「en」，法文為「fr」。

* **社群網站名稱**:

   顯示在URL中的網站根頁面名稱。

   * 仔細檢查名稱，因為建立網站後不易變更。
   * 基本URL( `https://server:port/site root/site name)` 會顯示在 `Community Site Name`.

   * 為了有效的URL，請附加基本語言代碼+ &quot;。html&quot;

      *例如*, `https://localhost:4502/content/sites/mysight/en.html`

* **社群網站範本** 功能表

   使用下拉式功能表來選擇可用 [社群網站範本](/help/communities/tools.md).

* 選擇 **下一個**.

### 步驟2 :設計 {#step-design}

「設計」面板包含2個子面板，用於選取主題和品牌橫幅：

#### 社群網站主題 {#community-site-theme}

![Sitetheme](assets/sitetheme.png)

框架使用 `Twitter Bootstrap` 為網站帶來回應式、彈性的設計。 可以選擇多個預載的Bootstrap主題之一來設定所選社區站點模板的樣式，或者可以上傳Bootstrap主題。

選取時，主題將會以不透明的藍色核取記號覆蓋。

發佈社群網站後，您可以 [編輯屬性](#modifying-site-properties) 並選取不同的主題。

#### 社群網站品牌推廣 {#community-site-branding}

![網站品牌化](assets/site-branding.png)

社群網站品牌化是顯示為頁首的影像，橫跨每個頁面。

影像的大小應與瀏覽器中頁面的預期顯示大小一樣寬，高度應為120像素。

建立或選取影像時，請記住：

* 影像高度會裁切為120個像素，從影像的上邊緣測量。
* 影像會固定至瀏覽器視窗的左側邊緣。
* 影像沒有大小調整，因此當影像寬度為……

   * 小於瀏覽器的寬度，影像會水準重複。
   * 大於瀏覽器的寬度，影像就會看起來被裁切。

* 選擇 **下一個**.

### 步驟3 :設定 {#step-settings}

「設定」面板包含數個子面板，顯示在移至建立網站的最後一個步驟之前要設定的功能。

* [使用者管理](#user-management)
* [標籤](#tagging)
* [角色](#roles)
* [協調](#moderation)
* [ANALYTICS](#analytics)
* [翻譯](#translation)
* [啟用](#enablement)

>[!NOTE]
>
>**啟用通道服務**
>
>數個「設定」子面板可指派受信任的成員來協調UGC、管理群組，或成為發佈環境中啟用資源的連絡人。
>
>此公約適用於發佈端 [使用者和使用者群組](/help/communities/users.md) （成員和成員群組），不會在製作環境中重複。
>
>因此，在製作環境中建立社群網站並指派受信任成員至各種角色時，必須從發佈環境中擷取成員資料。
>
>這是透過啟用 ` [AEM Communities Publish Tunnel Service](/help/communities/deploy-communities.md#tunnel-service-on-author)` 供作者使用。

#### 使用者管理 {#user-management}

![createsitesettings](assets/createsitesettings.png)

>[!NOTE]
>
>建議 [啟用社群網站](/help/communities/overview.md#enablement-community) 設為私人（如需詳細資訊，請連絡您的帳戶代表）。
>
>當匿名網站訪客被拒絕訪問、不能自行註冊，以及不能使用社交登錄時，社群網站是私有的。

* **允許使用者註冊**

   若勾選此選項，網站訪客可透過自行註冊成為社群成員。
如果未勾選，則社群網站為 *受限* 和網站訪客必須指派給社群網站的成員群組、提出要求或透過電子郵件傳送邀請。 如果取消勾選，則不允許匿名存取。
取消核取 *私人* 社群網站。 已勾選預設值。

* **允許匿名存取**

   若勾選此選項，社群網站會*開啟*且任何網站訪客都可存取該網站。
如果未選中，則只有登錄成員才能訪問該站點。
取消選中*私有*社區站點。 已勾選預設值。

* **允許傳訊**

   如果選中此選項，成員可以相互發送消息，併發送到社區站點內的組。
如果未勾選，則不會為社群設定傳訊。
預設為未勾選。

* **允許社交登入: Facebook**

   若勾選此選項，允許網站訪客以其Facebook帳戶憑證登入。 選取的 [Facebook雲端組態](/help/communities/social-login.md#create-a-facebook-connect-cloud-service) 應配置為在建立社區站點後將用戶添加到社區站點的成員組。
如果未勾選，則不會顯示Facebook登入。
不勾選 *私人* 社群網站。 預設為未勾選。

* **允許社交登入: Twitter**

   若勾選此選項，允許網站訪客以其Twitter帳戶憑證登入。 選取的 [Twitter雲端組態](/help/communities/social-login.md#create-a-twitter-connect-cloud-service) 應配置為在建立社區站點後將用戶添加到社區站點的成員組。
如果未勾選，則不會顯示Twitter登入。
不勾選 *私人* 社群網站。 預設為未勾選。

>[!NOTE]
>
>**允許社交登入**
>
>雖然範例Facebook和Twitter設定可能存在，且可供選取， [生產環境](/help/sites-administering/production-ready.md)，則必須建立自訂Facebook和Twitter應用程式。 請參閱 [使用Facebook和Twitter進行社交登入](/help/communities/social-login.md).

#### 標籤 {#tagging}

![網站標籤](assets/site-tagging.png)

可套用至社群內容的標籤，是透過選取先前透過 [標籤主控台](/help/sites-administering/tags.md#tagging-console).

此外，為社群網站選取標籤命名空間會限制定義目錄和資源時顯示的選取範圍。 請參閱 [標籤啟用資源](/help/communities/tag-resources.md) 以了解重要資訊。

* 文字搜尋方塊：開始輸入以識別允許在網站上使用的標籤。

#### 角色 {#roles}

![社群角色](assets/site-admin-2.png)

此 [社群成員的角色](/help/communities/users.md) 會隨這些設定指派。

使用預先輸入搜尋可輕鬆找到社群成員。

* **社群管理員**

   開始鍵入以選擇一個或多個可以管理社區成員和成員組的社區成員或成員組。

* **社群版主**

   開始鍵入以選擇一個或多個社區成員或成員組，這些成員或組將作為用戶生成內容的協調者受信任。

* **社群有特殊權限的成員**

   開始鍵入以選擇一個或多個社區成員或成員組，以便在 `Allow Privileged Member` 已為 [社群功能](/help/communities/functions.md).

* **社群管理員**

   開始鍵入以選擇一個或多個站點管理員，這些管理員可以獨立於其他站點管理員和預設社區管理員處理站點結構。 他們可以在階層的任何層級建立群組，並成為巢狀群組的預設管理員（但稍後可從巢狀群組的管理員角色中移除）。

#### 協調 {#moderation}

![網站協調](assets/site-moderation.png)

協調使用者產生的內容(UGC)的全域設定是由這些設定所控制。 個別元件有其他可控制協調的設定。

* **內容已預先審核**

   如果勾選「 」，張貼的社群內容要等到協調者核准後才會顯示。 預設為未勾選。 如需詳細資訊，請參閱 [調節社群內容](/help/communities/moderate-ugc.md#premoderation).

* **隱藏內容之前的標幟臨界值**

   如果大於0，則必須標籤主題或貼文，之後才能從公開檢視中隱藏該主題或貼文的次數。 如果設為–1，則標籤的主題或貼文永遠不會在公開檢視中隱藏。 預設為5。

#### ANALYTICS {#analytics}

![site-analytics](assets/site-analytics.png)

* **啟動 Analytics**

   僅限Adobe Analytics [已配置](/help/communities/analytics.md) （適用於社群功能）。
預設為未勾選。 勾選後，會出現其他選取功能表：

![site-analytics-enable](assets/site-analytics-enable.png)

* **雲端設定框架引用**

   從下拉式功能表中，選取為此社群網站設定的Analytics雲端服務架構。
   `Communities` 是來自的架構範例 [Communities功能的Analytics設定](/help/communities/analytics.md#aem-analytics-framework-configuration) 檔案。

#### 翻譯 {#translation}

![網站翻譯](assets/site-translation.png)

* **允許機器翻譯**

   若勾選（預設為未勾選），網站內的UGC就會啟用機器翻譯。 這不會影響任何其他內容，例如頁面內容，即使網站設定為多語言網站亦然。 請參閱 [轉譯使用者產生的內容](/help/communities/translate-ugc.md) 以取得有關為AEM Communities設定授權翻譯服務的資訊。 請參閱 [轉譯多語言網站的內容](/help/sites-administering/translation.md) 以取得完整概述。

![允許 — 機器 — 翻譯](assets/allow-machine-translation.png)

* **為選取的語言啟用機器翻譯**

   為機器翻譯啟用的語言預設為 [翻譯整合設定](/help/communities/translate-ugc.md#translation-integration-configuration). 通過刪除預設值和/或從下拉菜單中選擇其他語言，可以覆蓋此站點的這些預設設定。

* **選擇翻譯提供者**

   依預設，服務提供者是試用服務，使用 `microsoft` 僅供展示。 如果未授權翻譯服務提供商， **允許機器翻譯** 應取消勾選。

* **選擇全域共用存放區**

   對於具有多個語言副本的網站，全域共用存放區會提供單一對話執行緒，可從每個語言副本中看到。 這是通過選擇其中一種語言作為語言副本來實現的。 預設為 *無全局共用儲存*.

* **選擇翻譯提供者設定**

   選擇 [翻譯整合框架](/help/sites-administering/tc-tic.md) 為授權翻譯提供者建立。

* **選取您社群網站的翻譯選項**

   * **翻譯整個頁面**

      如果選取，則頁面上的所有UGC都會翻譯成頁面的基本語言。

      預設為 *未選取*.

   * **只翻譯選取項目**

      如果選取「 」，則每個貼文旁會出現一個翻譯選項，允許將個別貼文翻譯成頁面的基本語言。
預設為 *已選取*.

* **選取保留選項**

   * **根據使用者要求轉譯貢獻內容，並在之後保留**
如果選取此選項，則在提出要求前，內容不會翻譯。 翻譯後，翻譯會儲存在存放庫中。

      預設為 *未選取*.

   * **不保留翻譯**

      如果選中，翻譯不會儲存在儲存庫中。

      如果未選取，則會保存翻譯。

      預設為 *未選取*.

* **智慧型轉譯**

   選擇以下選項之一：

   * `Always show contributions in the original language` (預設)
   * `Always show contributions in user preferred language`
   * `Show contributions in user preferred language for only logged-in users`

#### 啟用 {#enablement}

![網站啟用](assets/site-enablement.png)

此 `ENABLEMENT`選擇的社區站點模板包括 [指派函式](/help/communities/functions.md#assignments-function)，啟用功能授權後即可使用， [已配置](/help/communities/enablement.md). 包括分配功能的參考站點模板為 `Reference Structured Learning Site Template.`

* **啟用管理員**
（必要）僅限 `Community Enablementmanagers` 可選擇組以管理此啟用社區。 啟用管理員負責將成員指派給資源。 另請參閱 [管理使用者和使用者群組](/help/communities/users.md).

* **Marketing Cloud 組織 ID**

   （選用） [視訊心率分析](/help/communities/analytics.md#video-heartbeat-analytics) 授權。

* 選擇 **下一個**.

### 步驟4 :建立社區網站 {#step-create-communities-site}

如果需要任何調整，請使用 **返回** 按鈕來製作。

一次 **建立** 若選取並啟動，則建立網站的程式將無法中斷。

建立網站後：

* 不支援變更url（節點名稱）。
* 未來對社群網站範本所做的變更不會影響已建立的社群網站。
* 禁用社區站點模板不會影響已建立的社區站點。
* 您可以編輯 [結構](#modify-structure) 來修改其屬性。

![建立網站](assets/create-site1.png)

過程完成後，新站點的資料夾將顯示在Communities Sites控制台中，供作者添加頁面內容或管理員修改站點的屬性。

![modify-site-property](assets/modify-site-property.png)

要修改社區站點，請選擇其項目資料夾以開啟它：

![網站專案](assets/site-project.png)

使用滑鼠暫留在網站上，或觸及網站資訊卡時，會出現圖示， [在製作模式中編輯網站](#authoring-site-content), [開啟站點屬性以進行修改](#modifying-site-properties), [發佈網站](#publishing-the-site), [匯出網站](#exporting-the-site)，和 [刪除網站](#deleting-the-site).

## 製作網站內容 {#authoring-site-content}

網站的內容可使用與任何其他AEM網站相同的工具製作。 若要開啟網站進行製作，請選取 `Open Site` 表徵圖，用滑鼠懸停在站點上。 該站點將在新頁簽中開啟，以便Communities Sites控制台仍可訪問。

![網站內容](assets/site-content.png)

>[!NOTE]
>
>如果不熟悉AEM，請在 [基本處理](/help/sites-authoring/basic-handling.md) 和 [製作頁面的快速指南](/help/sites-authoring/qg-page-authoring.md).

## 修改網站屬性 {#modifying-site-properties}

![編輯網站](assets/edit-site.png)

現有網站的屬性（在網站建立程式期間指定）可透過選取 `Edit Site`表徵圖，用滑鼠懸停在站點上。

`Details of the following properties match the descriptions provided in the` [網站建立](#site-creation) 區段。

![modify-site-basicinfo](assets/modify-site-basicinfo.png)

### 修改基本 {#modify-basic}

BASIC面板允許修改：

* 社群網站標題
* 社群網站說明

不能修改社區站點名稱。

選擇不同的社區站點模板對現有的社區站點沒有影響，因為模板和站點之間沒有連接。

反之， [結構](#modify-structure) 可以修改社區站點的。

### 修改結構 {#modify-structure}

「結構」面板允許修改最初從所選社區站點模板建立的結構。 從面板，您可以：

* 拖放其他 [社群功能](/help/communities/functions.md) 進入網站結構。
* 在網站結構中的社群函式例項上：

   * **`gear icon`**

      編輯設定，包括顯示標題和URL名稱*，以及 [特權成員組](/help/communities/users.md#privilegedmembersgroups).

   * **`trashcan icon`**

      從網站結構中移除（刪除）函式。

   * **`grid icon`**

      修改網站頂層導覽列中顯示的函式順序。

>[!NOTE]
>
>您可以變更「網站結構」中除頂端函式外所有函式的順序。 因此，無法變更社群網站的首頁。

>[!CAUTION]
>
>* 雖然顯示標題可以不產生副作用而變更，但不建議編輯屬於社群網站之社群函式的URL名稱。
>
>例如，重新命名URL不會移動現有的UGC，因此會產生「遺失」UGC的效果。

>[!CAUTION]
>
>組函式必須 *not* be *第一，也不是唯一* 功能。
>
>任何其他函式，例如 [頁面函式](/help/communities/functions.md#page-function)，必須包含在內並列出。

#### 範例：將目錄函式添加到社區站點結構 {#example-adding-a-catalog-function-to-a-community-site-structure}

![add-catalog-site](assets/add-catalog-site.png)

### 修改設計 {#modify-design}

「設計」面板允許應用新主題：

* [社群網站主題](#community-site-theme)
* [社群網站品牌](#community-site-branding)

   * 捲動至面板底部以變更品牌影像。

### 修改設定 {#modify-settings}

「設定」面板可讓您存取社群網站建立步驟3之子面板下的大部分設定：

* [使用者管理](#user-management)
* [標記](#tagging)
* [審核](#moderation)
* [會員角色](#roles)
* [分析](#analytics)
* [轉換](#translation)

### 修改縮圖 {#modify-thumbnail}

「縮圖」面板允許上傳影像以在Communities Sites控制台中表示站點。

### 修改啟用 {#modify-enablement}

「啟用」面板可讓您存取建立社群網站期間提供的設定。

請參閱 [啟用](#enablement) 說明。

## 發佈網站 {#publishing-the-site}

社群網站經過新建立或修改後，即可透過選取 `Publish Site` 表徵圖，滑鼠將滑鼠懸停在站點上。

![發佈網站](assets/publish-site.png)

網站成功發佈後，會出現指示。

![網站發佈](assets/site-published.png)

### 使用巢狀群組發佈 {#publishing-with-nested-groups}

發佈社群網站後，必須個別發佈使用 [群組主控台](/help/communities/groups.md).

## 匯出網站 {#exporting-the-site}

![匯出網站](assets/export-site.png)

選取將滑鼠移至網站上的匯出圖示，以建立同時儲存於 [封裝管理員](/help/sites-administering/package-manager.md) 和下載。

請注意，網站套件中未包含UGC。

## 刪除網站 {#deleting-the-site}

![deleteicon](assets/deleteicon.png)

要刪除社區站點，請選擇「社區站點控制台」中滑鼠懸停在站點上時顯示的「刪除站點」表徵圖。 此動作會移除與網站相關聯的所有項目，例如UGC、使用者群組、資產和資料庫記錄。

## 建立的社區用戶組 {#created-community-user-groups}

發佈新社群網站後，新成員群組（在發佈環境中建立使用者群組）會對各種管理和成員角色設定適當的權限。

為成員組建立的名稱包括 *網站名稱* 在 [步驟1](#step13asitetemplate) （顯示在URL中的名稱）和唯一ID，以避免與不同社群網站根具有相同網站名稱的社群網站和群組產生衝突。

例如，如果標題為「快速入門教學課程」的網站名稱為「參與」，則協調者的使用者群組將是：

* 標題：社群參與協調者
* 名稱：社群 — *engage-uid* — 協調者

請注意，在建立網站時，任何成員都會將角色指派為協調者或群組管理員，並指派給適當的群組以及成員群組。 這些組和成員分配是在發佈新站點時在發佈時建立的。

如需詳細資訊，請參閱 [管理使用者和使用者群組](/help/communities/users.md).

>[!NOTE]
>
>若 [允許Social登入：Facebook](#user-management) 啟用後，使用者群組
>
>* `community-<site-name>-<uid>-members`
>
>建立，則會套用 [Facebook雲端服務](/help/communities/social-login.md#createafacebookcloudservice) 應已設定為將使用者新增至此群組。

## 配置身份驗證錯誤 {#configure-for-authentication-error}

依預設，當使用者輸入錯誤的憑證且無法登入時，社群網站會重新導向至範例登入頁面。 此範例登入不會顯示在 [生產伺服器](/help/sites-administering/production-ready.md).

若要正確重新導向，當網站經設定並推送至發佈後，請完成下列步驟以取得驗證失敗，而無法重新導向至社群網站：

* 在每個AEM發佈例項上。
* 以管理員權限登入。
* 存取 [Web主控台](/help/sites-deploying/configuring-osgi.md).

   * 例如， [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr).

* 找出 `Adobe Granite Login Selector Authentication Handler`.
* 選取 `pencil` 圖示以開啟要編輯的設定。
* 輸入 **登入頁面對應** 如下所示：

   `/content/sites/<site-name>/path/to/login/page:/content/sites/<site-name>`

   例如：
   `/content/sites/engage/en/signin:/content/sites/engage/en`

* 選取&#x200B;**儲存**。

![auth-error](assets/auth-error.png)

### 測試驗證重定向 {#test-authentication-redirection}

在相同的AEM發佈執行個體上，使用社群網站的登入頁面對應進行設定：

* 瀏覽到社區站點首頁。

   * 例如， [https://localhost:4503/content/sites/engage/en.html](https://localhost:4503/content/sites/engage/en.html)

* 選擇註銷。
* 選擇「登錄」。
* 輸入明顯不正確的憑據，例如用戶名&quot;x&quot;和密碼&quot;x&quot;。
* 登入頁面應顯示「無效登入」錯誤。

![測試驗證](assets/test-authentication.png)

## 從主站點控制台訪問社區站點 {#accessing-community-sites-from-main-sites-console}

從全域導覽網站控制台，社群網站位於 `Community Sites` 檔案夾。

雖然可以以此方式訪問社區站點，但對於管理任務，應從社區站點控制台訪問社區站點。

![存取網站](assets/access-site.png)
