---
title: Communities Sites Console
seo-title: Communities Sites Console
description: 如何訪問Communities Sites控制台
seo-description: 如何訪問Communities Sites控制台
uuid: 74134281-244c-40da-a941-7f2f3e706d4b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 4130f952-5bb5-4e32-91d6-47b2885b30a4
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Communities Sites控制台{#communities-sites-console}

Communities Sites控制台可讓您存取：

* 網站建立
* 網站編輯
* 網站管理
* [建立和編輯巢狀群組](/help/communities/groups.md) （子社群）

請參閱[AEM Communities快速入門(Getting Started with Moginal](/help/communities/getting-started.md))，瞭解在作者環境中建立社群網站的速度，以及如何從作者和發佈環境建立社群群組。

>[!NOTE]
>
>用於建立[社區站點](/help/communities/sites-console.md)、[社區站點模板](/help/communities/sites.md)、[社區組模板](/help/communities/tools-groups.md)和[社區功能](/help/communities/functions.md)的主要社區菜單僅用於作者環境。

## 必備條件 {#prerequisites}

在建立社區站點之前，它&#x200B;*required*&#x200B;要：

* 請確定有一或多個發佈例項正在執行。
* 啟用[隧道服務](/help/communities/deploy-communities.md#tunnel-service-on-author)來管理成員和成員組。
* 識別[主要發行者](/help/communities/deploy-communities.md#primary-publisher)。
* [當主發](/help/communities/deploy-communities.md#replication-agents-on-author) 布者埠不是預設值時，設定複製(4503)。

最佳實務是，為確保網站已準備好支援許多功能，請採取下列步驟：

* 安裝[最新的功能套件](/help/communities/deploy-communities.md#latestfeaturepack)。
* 為AEM Communities啟用[Adobe Analytics](/help/communities/analytics.md)。
* 配置[email](/help/communities/email.md)
* 確定[社區管理員](/help/communities/users.md#creating-community-members)。
* [啟用OAuth掌](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler) 上型電腦以進行社交登入。

## 訪問社區站點控制台{#accessing-communities-sites-console}

在作者環境中，要訪問Communities Sites控制台：

* 從全域導覽：**[!UICONTROL 社群]** > **[!UICONTROL 網站]**

「社群網站」主控台會顯示任何現有的社群網站。 在此控制台中，可以建立、編輯、管理和刪除社區站點。

要建立新社區站點，請選擇&#x200B;**建立**&#x200B;表徵圖。

若要存取現有社群網站，為了製作、修改、發佈、匯出或新增巢狀群組，請選取網站的檔案夾圖示。

例如，下圖顯示主Communities Sites控制台，顯示兩個社群站點的資料夾：[enable](/help/communities/getting-started-enablement.md)和[engage](/help/communities/getting-started.md):

![site-console](assets/site-console.png)

## 站點建立{#site-creation}

站點建立控制台提供了根據選定的[社區站點模板](/help/communities/sites.md)和設定來組合站點功能的逐步方法。

每個建立的網站都包含登入功能，因為網站訪客必須先登入才能張貼內容、傳送訊息或參與群組。 其他包含的功能包括使用者設定檔、訊息、通知、網站選單、搜尋、主題和品牌。

通過選擇位於Communities Sites控制台頂部的`Create`按鈕啟動進程。

建立過程是一系列步驟，這些步驟顯示為包含要配置的一組特徵的面板（顯示為子面板）。 在最後步驟中提交站點之前，可以前移到&#x200B;**Next**&#x200B;步驟或&#x200B;**Back**&#x200B;到前一個步驟。

### 步驟1:網站範本{#step-site-template}

![新網站範本](assets/newsitetemplate.png)

在「網站範本」面板上，會指定「標題」、「說明」、「網站根」、「基本語言」、「名稱」和「網站範本」:

* **社群網站標題**

   網站的顯示標題。

   標題會出現在已發佈的網站上，也會出現在網站管理員UI中。

* **社群網站說明**

   網站的說明。

   說明不會出現在發佈的網站上。

* **社群網站根目錄**

   網站的根路徑。

   預設根目錄為`/content/sites`，但根目錄可以移動到網站中的任何位置。

* **社群網站基本語言**

   (單一語言不受影響：英文)使用下拉式選單，從可用語言(德文、義大利文、法文、日文、西班牙文、葡萄牙文（巴西）、中文（繁體）和簡體中文)選擇一種或多種&#x200B;*或多種*&#x200B;基本語言。 會針對新增的每種語言建立一個社群網站，並依照[多語言網站轉譯內容](/help/sites-administering/translation.md)中所述的最佳實務，存在於相同的網站資料夾中。 每個網站的根頁面將包含一個子頁面，該子頁面由其中一種語言的語言代碼命名，例如英文的&#39;en&#39;或法文的&#39;fr&#39;。

* **社群網站名稱**:

   顯示在URL中的網站根頁面名稱。

   * 請連按兩下名稱，因為在建立網站後不易變更。
   * 基本URL(`https://server:port/site root/site name)`)將顯示在`Community Site Name`的下方。

   * 若為有效的URL，請附加基本語言代碼+ &quot;。html&quot;

      *例如*,  `https://localhost:4502/content/sites/mysight/en.html`

* **社群網站範本** 功能表

   使用下拉菜單選擇可用的[社區站點模板](/help/communities/tools.md)。

* 選擇&#x200B;**Next**。

### 步驟2:設計{#step-design}

「設計」面板包含2個子面板，用於選取主題和品牌橫幅：

#### 社群網站主題{#community-site-theme}

![sitetheme](assets/sitetheme.png)

此架構使用[TwitterBootstrap](https://twitterbootstrap.org/)為網站提供回應式、有彈性的設計。 可以選擇多個預先載入的Bootstrap主題之一以對所選社區站點模板進行樣式化，或者可以上載Bootstrap主題。

選取後，主題將會以不透明的藍色核取標籤覆蓋。

社群網站發佈後，[可編輯屬性](#modifying-site-properties)並選取不同的主題。

#### 社群網站品牌{#community-site-branding}

![網站品牌](assets/site-branding.png)

社群網站品牌是顯示為每個頁面上方標題的影像。

影像的大小應與預期的頁面在瀏覽器中顯示的大小相同，高度應為120像素。

建立或選取影像時，請記住：

* 影像高度會裁切為120像素，從影像的上邊緣測量。
* 影像會固定在瀏覽器視窗的左邊緣。
* 影像沒有調整大小，因此當影像寬度為……

   * 小於瀏覽器的寬度，影像會水準重複。
   * 大於瀏覽器的寬度，影像會看起來被裁切。

* 選擇&#x200B;**Next**。

### 步驟3:設定{#step-settings}

「設定」面板包含數個子面板，這些子面板會先顯示要設定的功能，然後再移至建立網站的最後一個步驟。

* [使用者管理](#user-management)
* [標籤](#tagging)
* [角色](#roles)
* [協調](#moderation)
* [ANALYTICS](#analytics)
* [翻譯](#translation)
* [啟用](#enablement)

>[!NOTE]
>
>**啟用隧道服務**
>
>數個「設定」子面板可讓受信任成員在發佈環境中協調UGC、管理群組或成為啟用資源的聯絡人。
>
>此約定適用於發佈端[使用者和使用者群組](/help/communities/users.md)（成員和成員群組）在作者環境中不複製。
>
>因此，在作者環境中建立社區站點並將受信任成員分配給各種角色時，必須從發佈環境中檢索成員資料。
>
>這是通過為作者環境啟用` [AEM Communities Publish Tunnel Service](/help/communities/deploy-communities.md#tunnel-service-on-author)`來實現的。

#### 用戶管理{#user-management}

![createsitesettings](assets/createsitesettings.png)

>[!NOTE]
>
>建議[啟用社群網站](/help/communities/overview.md#enablement-community)為私用（如需詳細資訊，請連絡您的帳戶代表）。
>
>當匿名網站訪客被拒絕存取、無法自行註冊且不能使用社交登入時，社群網站是私密的。

* **允許使用者註冊**

   如果勾選，網站訪客可能會透過自行註冊成為社群成員。
如果未勾選，則社群網站為*restricted*，且必須將網站訪客指派給社群網站的成員群組、提出請求或透過電子郵件傳送邀請。 如果未勾選，則不允許匿名存取。
對*private*&#x200B;社區站點取消選中。 已勾選預設值。

* **允許匿名存取**

   如果勾選，社群網站會*開啟*任何網站訪客都可存取網站。
若未勾選，則只有登入會員可存取網站。
取消勾選*private *community站點。 已勾選預設值。

* **允許傳訊**

   如果選中此選項，成員可以向彼此發送消息，也可以向社區站點中的組發送消息。
如果未選中，則不會為社區設定消息。
預設為未勾選。

* **允許社交登入: Facebook**

   如果勾選，允許網站訪客使用其Facebook帳戶認證登入。 選取的[Facebook雲端設定](/help/communities/social-login.md#create-a-facebook-connect-cloud-service)應設定為在建立社群網站後，新增使用者至社群網站的成員群組。
如果未勾選，則不會顯示Facebook登入。
對*private*&#x200B;社區站點不選中。 預設為未勾選。

* **允許社交登入: Twitter**

   如果勾選，允許網站訪客使用其Twitter帳戶認證登入。 選取的[Twitter雲端設定](/help/communities/social-login.md#create-a-twitter-connect-cloud-service)應設定為在社群網站建立後，將使用者新增至社群網站的成員群組。
如果取消勾選，則不會顯示Twitter登入。
對*private*&#x200B;社區站點不選中。 預設為未勾選。

>[!NOTE]
>
>**允許社交登入**
>
>雖然範例Facebook和Twitter組態可能存在且可供選取，但對於[生產環境](/help/sites-administering/production-ready.md)，則必須建立自訂Facebook和Twitter應用程式。 請參閱[使用Facebook和Twitter進行社交登入](/help/communities/social-login.md)。

#### 標籤{#tagging}

![網站標籤](assets/site-tagging.png)

可以應用於社區內容的標籤通過選擇以前通過[標籤控制台](/help/sites-administering/tags.md#tagging-console)定義的標籤名稱空間來控制。

此外，為社群網站選取標籤名稱空間會限制在定義目錄和資源時顯示的選擇。 如需重要資訊，請參閱[標籤啟用資源](/help/communities/tag-resources.md)。

* 文字搜尋方塊：開始輸入以識別允許在網站上使用的標籤。

#### 角色{#roles}

![社群角色](assets/site-admin-2.png)

社區成員的[角色將分配這些設定。](/help/communities/users.md)

使用預先輸入搜尋，尋找社群成員十分簡單。

* **社群管理員**

   開始鍵入以選擇一個或多個可管理社區成員和成員組的社區成員或成員組。

* **社群版主**

   開始鍵入以選擇一個或多個要作為用戶生成內容的協調者信任的社區成員或成員組。

* **社群有特殊權限的成員**

   開始鍵入以選擇一個或多個社區成員或成員組，以便在[社區函式](/help/communities/functions.md)選擇了`Allow Privileged Member`時，使其能夠建立新內容。

* **社群管理員**

   開始鍵入以選擇一個或多個站點管理員，這些管理員可以處理獨立於其他站點管理員和預設社區管理員的站點結構。 他們可以在階層的任何層級建立群組，並成為巢狀群組的預設管理員（但稍後可從巢狀群組的管理員角色中移除這些群組）。

#### 協調{#moderation}

![網站協調](assets/site-moderation.png)

協調使用者產生內容(UGC)的全域設定由這些設定控制。 個別元件有其他設定可控制協調。

* **內容已預先審核**

   如果勾選，則張貼的社群內容在協調者核准後才會顯示。 預設為未勾選。 如需詳細資訊，請參閱[協調社群內容](/help/communities/moderate-ugc.md#premoderation)。

* **隱藏內容之前的標幟臨界值**

   如果大於0，則主題或貼文在隱藏於公開檢視之前必須加以標幟的次數。 如果設為-1，則標籤的主題或貼文永遠不會隱藏在公開檢視中。 預設值為5。

#### ANALYTICS {#analytics}

![網站分析](assets/site-analytics.png)

* **啟動 Analytics**

   只有在Adobe Analytics已為Communities功能配置[](/help/communities/analytics.md)時才可用。
預設為未勾選。 勾選後，會出現其他選擇功能表：

![site-analytics-enable](assets/site-analytics-enable.png)

* **雲端設定框架引用**

   從下拉式選單中，選取為此社群網站設定的Analytics雲端服務架構。
   `Communities` 是Analytics Configuration for Communities  [Features檔案的架](/help/communities/analytics.md#aem-analytics-framework-configuration) 構範例。

#### TRANSLATION {#translation}

![站點轉換](assets/site-translation.png)

* **允許機器翻譯**

   勾選後（預設為未勾選），網站內的UGC就會啟用機器轉譯。 這不會影響任何其他內容，例如頁面內容，即使網站設定為多語言網站亦然。 有關為AEM Communities配置許可翻譯服務的資訊，請參見[翻譯用戶生成的內容](/help/communities/translate-ugc.md)。 如需完整概觀，請參閱[多語言網站翻譯內容](/help/sites-administering/translation.md)。

![允許機器翻譯](assets/allow-machine-translation.png)

* **為選取的語言啟用機器翻譯**

   啟用機器翻譯的語言預設為[翻譯整合配置](/help/communities/translate-ugc.md#translation-integration-configuration)指定的系統設定。 透過刪除預設值及／或從下拉式選單選取其他語言，可覆寫此網站的這些預設設定。

* **選擇翻譯提供者**

   預設情況下，服務提供商是僅用於演示的試用服務。 `microsoft`如果未許可翻譯服務提供商，應取消選中「允許機器翻譯」。****

* **選擇全域共用存放區**

   對於具有多個語言副本的網站，全域共用商店會提供單一對話串，每個語言副本都可看到。 這是通過選擇其中一種語言作為語言副本來實現的。 預設值為&#x200B;*無全局共用儲存*。

* **選擇翻譯提供者設定**

   選擇為許可翻譯提供者建立的[翻譯整合框架](/help/sites-administering/tc-tic.md)。

* **選取您社群網站的翻譯選項**

   * **翻譯整個頁面**

      如果選取此選項，頁面上的所有UGC都會轉譯為頁面的基本語言。

      預設值為&#x200B;*未選取*。

   * **只翻譯選取項目**

      如果選取此選項，每個貼文旁會出現一個翻譯選項，允許將個別貼文翻譯為頁面的基本語言。
預設值為*selected*。

* **選取保留選項**

   * **翻譯使用者要求的稿件，**
然後保留如果選取，則內容在提出要求前不會翻譯。翻譯完成後，翻譯將儲存在儲存庫中。

      預設值為&#x200B;*未選取*。

   * **不保留翻譯**

      如果選中此選項，則翻譯不會儲存在儲存庫中。

      如果未選擇，則保留翻譯。

      預設值為&#x200B;*未選取*。

* **智慧型轉譯**

   選擇以下選項之一：

   * `Always show contributions in the original language` (預設)
   * `Always show contributions in user preferred language`
   * `Show contributions in user preferred language for only logged-in users`

#### 啟用{#enablement}

![網站啟用](assets/site-enablement.png)

當選擇的社區站點模板包括[分配函式](/help/communities/functions.md#assignments-function)時，`ENABLEMENT`設定適用，當啟用功能獲得許可並且[配置](/help/communities/enablement.md)時，設定可用。 包含分配函式的參考站點模板為`Reference Structured Learning Site Template.`

* **啟用管理員**
（必要）只有群組的 `Community Enablementmanagers` 成員可供選取以管理此啟用社群。啟用經理負責指派成員至資源。 另請參閱[管理用戶和用戶組](/help/communities/users.md)。

* **Marketing Cloud 組織 ID**

   （可選）[視訊心率分析](/help/communities/analytics.md#video-heartbeat-analytics)授權的ID。

* 選擇&#x200B;**Next**。

### 步驟4:建立社區站點{#step-create-communities-site}

如果需要調整，請使用&#x200B;**Back**&#x200B;按鈕進行調整。

一旦選擇並啟動&#x200B;**Create**&#x200B;後，建立站點的過程就無法中斷。

建立網站後：

* 不支援變更URL（節點名稱）。
* 未來對社群網站範本所做的變更，將不會影響已建立的社群網站。
* 禁用社區站點模板不會影響建立的社區站點。
* 通過修改社區站點的屬性，可以編輯社區站點的[STRUCTURE](#modify-structure)。

![create-site](assets/create-site1.png)

當程式完成時，新站點的資料夾將顯示在「社群站點」控制台中，作者可以從中添加頁面內容，或者管理員可以修改站點的屬性。

![modify-site-property](assets/modify-site-property.png)

要修改社區站點，請選擇其項目資料夾以將其開啟：

![site-project](assets/site-project.png)

當用滑鼠暫留在網站上，或觸碰網站資訊卡時，會出現允許[以作者模式](#authoring-site-content)、[開啟網站屬性以進行修改](#modifying-site-properties)、[、[匯出網站](#exporting-the-site)和[刪除網站](#deleting-the-site)的圖示。](#publishing-the-site)

## 編寫網站內容{#authoring-site-content}

網站的內容可能與任何其他網站使用相同的工具AEM製作。 若要開啟網站以進行製作，請選取在滑鼠暫留網站時顯示的`Open Site`圖示。 該站點將在新頁籤中開啟，以便Communities Sites控制台仍可訪問。

![網站內容](assets/site-content.png)

>[!NOTE]
>
>如果不熟AEM悉，請檢視[基本處理](/help/sites-authoring/basic-handling.md)和[頁面編寫快速指南的說明檔案。](/help/sites-authoring/qg-page-authoring.md)

## 修改站點屬性{#modifying-site-properties}

![edit-site](assets/edit-site.png)

在站點建立過程中指定的現有站點的屬性可通過選擇`Edit Site`表徵圖來修改，該表徵圖顯示在滑鼠懸停站點上。

`Details of the following properties match the descriptions provided in the` [網站建](#site-creation) 立區段。

![modify-site-basicinfo](assets/modify-site-basicinfo.png)

### 修改基本{#modify-basic}

BASIC面板允許修改：

* 社群網站標題
* 社群網站說明

不得修改社群網站名稱。

選擇不同的社群網站範本對現有社群網站不會有任何影響，因為範本和網站之間沒有任何連接。

可以改進社區站點的[STRUCTURE](#modify-structure)。

### 修改結構{#modify-structure}

「結構」(STRUCTURE)面板允許修改最初從所選社區站點模板建立的結構。 從面板，您可以：

* 將其他[社群函式](/help/communities/functions.md)拖放至網站結構中。
* 在網站結構中的社群功能例項上：

   * **`gear icon`**

      編輯設定，包括顯示標題和URL名稱*，以及[特權成員群組](/help/communities/users.md#privilegedmembersgroups)。

   * **`trashcan icon`**

      從網站結構移除（刪除）函式。

   * **`grid icon`**

      修改網站頂層導覽列中顯示的功能順序。

>[!NOTE]
>
>您可以變更「網站結構」中除頂部函式外的所有函式順序。 因此，無法變更社群網站的首頁。

>[!CAUTION]
>
>* 雖然顯示標題可以不產生副作用而變更，但不建議編輯屬於社群網站之社群函式的URL名稱。
>
>
例如，重新命名URL不會移動現有的UGC，因此會產生「遺失」UGC的效果。

>[!CAUTION]
>
>群組函式必須&#x200B;*not*&#x200B;是&#x200B;*的第一個函式，也不是站點結構中唯一的*&#x200B;函式。
>
>任何其他函式（例如[page函式](/help/communities/functions.md#page-function)）必須先包含並列出。

#### 範例：將目錄函式添加到社區站點結構{#example-adding-a-catalog-function-to-a-community-site-structure}

![add-catalog-site](assets/add-catalog-site.png)

### 修改設計{#modify-design}

DESIGN面板可套用新主題：

* [社群網站主題](#community-site-theme)
* [社群網站品牌](#community-site-branding)

   * 捲動至面板底部以變更品牌影像。

### 修改設定{#modify-settings}

「設定」面板可讓您存取「社群網站建立步驟3」子面板下的大部分設定：

* [使用者管理](#user-management)
* [標記](#tagging)
* [審核](#moderation)
* [會員角色](#roles)
* [分析](#analytics)
* [轉換](#translation)

### 修改縮圖{#modify-thumbnail}

THUMBNAIL面板允許上傳影像，以在Communities Sites主控台中呈現網站。

### 修改啟用{#modify-enablement}

ENABLEMENT面板可讓您存取社群網站建立期間提供的設定。

請參閱[ENABLEMENT](#enablement)說明。

## 發佈網站{#publishing-the-site}

社群網站新建或修改後，可以選取`Publish Site`圖示來發佈（啟用）網站，此圖示會在滑鼠暫留在網站上。

![publish-site](assets/publish-site.png)

網站成功發佈後，將會出現指示。

![site-published](assets/site-published.png)

### 使用巢狀群組發佈{#publishing-with-nested-groups}

發佈社群網站後，必須個別發佈使用[群組控制台](/help/communities/groups.md)建立的每個子社群（巢狀群組）。

## 導出站點{#exporting-the-site}

![導出站點](assets/export-site.png)

選擇將滑鼠懸停在站點上的導出表徵圖，以建立同時儲存在[軟體包管理器](/help/sites-administering/package-manager.md)中並下載的社區站點的軟體包。

請注意，網站套件中不包含UGC。

## 刪除站點{#deleting-the-site}

![deleteicon](assets/deleteicon.png)

要刪除社區站點，請選擇「刪除站點」表徵圖，該表徵圖將滑鼠懸停在「社區站點控制台」中的站點上。 此動作會移除與網站相關的所有項目，例如UGC、使用者群組、資產和資料庫記錄。

## 已建立社區用戶組{#created-community-user-groups}

發佈新社群網站後，新成員群組（使用者群組是在發佈環境中建立的）會針對各種管理和成員角色設定適當的權限。

為成員組建立的名稱包括&#x200B;*站點名*（在[步驟1](#step13asitetemplate)中指定站點）以及唯一ID，以避免與社區站點和組衝突，這些站點和組具有不同社區站點根目錄的相同站點名。

例如，如果名稱為「Getting Started Tutorial」（快速入門教學課程）的網站名稱為「engage」，則協調者的使用者群組為：

* 標題：社群參與協調者
* 名稱：community-*engage-uid*-moderator

請注意，在建立站點時，任何分配角色作為協調者或組管理員的成員都將被分配給相應的組，並被分配給成員組。 發佈新網站時，會在發佈時建立這些群組和成員指派。

如需詳細資訊，請參閱[管理使用者和使用者群組](/help/communities/users.md)。

>[!NOTE]
>
>如果[允許社交登入：一旦使用者群組啟用Facebook](#user-management)
>
>* `community-<site-name>-<uid>-members`
>
>
建立後，應將已套用的[Facebook雲端服務](/help/communities/social-login.md#createafacebookcloudservice)設定為新增使用者至此群組。

## 配置驗證錯誤{#configure-for-authentication-error}

依預設，當使用者輸入錯誤的認證且無法登入時，社群網站會重新導向至範例登入頁面。 此樣例登錄不存在於[生產伺服器](/help/sites-administering/production-ready.md)上。

若要正確重新導向，在設定網站並推送至發佈後，請完成下列步驟，以取得重新導向至社群網站的驗證失敗：

* 在每個AEM發佈例項上。
* 以管理員權限登入。
* 訪問[Web控制台](/help/sites-deploying/configuring-osgi.md)。

   * 例如，[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)。

* 找到`Adobe Granite Login Selector Authentication Handler`。
* 選擇`pencil`表徵圖以開啟要編輯的配置。
* 輸入&#x200B;**登錄頁映射** ，如下所示：

   `/content/sites/<site-name>/path/to/login/page:/content/sites/<site-name>`

   例如：
   `/content/sites/engage/en/signin:/content/sites/engage/en`

* 選擇&#x200B;**保存**。

![驗證錯誤](assets/auth-error.png)

### 測試驗證重定向{#test-authentication-redirection}

在為社AEM群網站設定登入頁面對應的相同發佈例項上：

* 瀏覽至社群網站首頁。

   * 例如，[https://localhost:4503/content/sites/engage/en.html](https://localhost:4503/content/sites/engage/en.html)

* 選擇「註銷」。
* 選擇「登入」。
* 輸入明顯不正確的憑證，例如使用者名稱&quot;x&quot;和密碼&quot;x&quot;。
* 登入頁面應顯示「無效登入」錯誤。

![測試認證](assets/test-authentication.png)

## 從主站點控制台{#accessing-community-sites-from-main-sites-console}訪問社區站點

在全局導航站點控制台中，社區站點位於`Community Sites`資料夾中。

雖然可以通過這種方式訪問社區站點，但對於管理任務，應從「社區站點」控制台訪問社區站點。

![存取網站](assets/access-site.png)



