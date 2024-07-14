---
title: 社群網站主控台
description: 瞭解如何存取Communities Sites主控台，以進行網站建立、編輯和管理。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 426e3adf-3723-4d17-a988-6eb050939e68
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '3084'
ht-degree: 0%

---

# 社群網站主控台 {#communities-sites-console}

社群網站主控台提供下列存取權：

* 網站建立
* 網站編輯
* 網站管理
* [建立和編輯巢狀群組](/help/communities/groups.md) （子社群）

請參閱[AEM Communities快速入門](/help/communities/getting-started.md)，您可以在其中體驗如何在作者環境中快速建立社群網站，以及如何從作者和發佈環境建立社群群組。

>[!NOTE]
>
>建立[社群網站](/help/communities/sites-console.md)、[社群網站範本](/help/communities/sites.md)、[社群群組範本](/help/communities/tools-groups.md)和[社群功能](/help/communities/functions.md)的主社群功能表僅供作者環境使用。

## 先決條件 {#prerequisites}

建立社群網站之前，*必須*&#x200B;才能：

* 確認一或多個Publish執行個體在執行中。
* 啟用[通道服務](/help/communities/deploy-communities.md#tunnel-service-on-author)以管理成員和成員群組。
* 識別[主要發行者](/help/communities/deploy-communities.md#primary-publisher)。
* [當主要發行者連線埠不是預設值(4503)時設定復寫](/help/communities/deploy-communities.md#replication-agents-on-author)。

為確保網站準備好支援許多功能，最佳實務是採取下列步驟：

* 安裝[最新功能套件](/help/communities/deploy-communities.md#latestfeaturepack)。
* 為AEM Communities啟用[Adobe Analytics](/help/communities/analytics.md)。
* 設定[電子郵件](/help/communities/email.md)
* 識別[社群管理員](/help/communities/users.md#creating-community-members)。
* [為社交登入啟用OAuth處理常式](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)。

## 存取社群網站主控台 {#accessing-communities-sites-console}

在製作環境中，若要存取Communities Sites主控台：

* 從全域導覽： **[!UICONTROL 社群]** > **[!UICONTROL 網站]**

社群網站主控台會顯示任何現有的社群網站。 在此主控台中，可以建立、編輯、管理和刪除社群網站。

若要建立社群網站，請選取&#x200B;**建立**&#x200B;圖示。

若要存取現有的社群網站以編寫、修改、發佈、匯出或新增巢狀群組，請選取網站的資料夾圖示。

## 網站建立 {#site-creation}

網站建立主控台提供根據所選[社群網站範本](/help/communities/sites.md)和設定來組合網站功能的逐步方法。

每個建立的網站都包含登入功能，因為網站訪客必須先登入，才能發佈內容、傳送訊息或參與群組。 包含的其他功能包括使用者設定檔、訊息、通知、網站功能表、搜尋、主題設定和品牌推廣。

選取社群網站主控台頂端的`Create`按鈕，即可啟動程式。

建立過程是作為面板顯示的一系列步驟，其中包含要配置的一組特徵（顯示為子面板）。 在認可最後步驟中的網站之前，可以前進到&#x200B;**下一步**&#x200B;步驟或&#x200B;**上一步**。

### 步驟1：網站範本 {#step-site-template}

![newsitetemplate](assets/newsitetemplate.png)

在「網站範本」面板上，會指定「標題」、「說明」、「網站根目錄」、「基本語言」、「名稱」和「網站範本」：

* **社群網站標題**

  網站的顯示標題。

  標題會顯示在已發佈的網站與網站管理員UI中。

* **社群網站描述**

  網站說明。

  說明未出現在已發佈的網站上。

* **社群網站根目錄**

  網站的根路徑。

  預設根目錄為`/content/sites`，但根目錄可移至網站內的任何位置。

* **社群網站基本語言**

  （單一語言則保持原樣：英文）使用下拉式功能表，從可用的語言中選擇一種&#x200B;*或更多*&#x200B;種基本語言 — 德文、義大利文、法文、日文、西班牙文、葡萄牙文（巴西）、繁體中文，以及簡體中文。 已針對新增的每種語言建立一個社群網站，並遵循[翻譯多語言網站的內容](/help/sites-administering/translation.md)中所述的最佳實務，存在於相同的網站資料夾中。 每個網站的根頁面都包含一個子頁面，該子頁面是以其中一個選取語言的語言代碼來命名，例如「en」代表英文，「fr」代表法文。

* **社群網站名稱**：

  顯示在URL中的網站根頁面名稱。

   * 請仔細檢查名稱，因為網站建立後不易變更。
   * 基底URL ( `https://server:port/site root/site name)`顯示在`Community Site Name`下方。

   * 若要取得有效的URL，請附加基本語言代碼+ &quot;。html&quot;

     *例如*，`https://localhost:4502/content/sites/mysight/en.html`

* **社群網站範本**&#x200B;功能表

  使用下拉式功能表選擇可用的[社群網站範本](/help/communities/tools.md)。

* 選取&#x200B;**「下一步」**。

### 步驟2 ：設計 {#step-design}

「設計」面板包含兩個子面板，用於選取主題和品牌化橫幅：

#### 社群網站主題 {#community-site-theme}

![網站佈景主題](assets/sitetheme.png)

架構使用`Twitter Bootstrap`為網站提供回應式彈性設計。 可以選擇預先載入的Bootstrap主題之一來設定所選社群網站範本的樣式，也可以上傳Bootstrap主題。

選取時，主題會以不透明的藍色核取記號覆蓋。

發佈社群網站之後，可以[編輯屬性](#modifying-site-properties)並選取不同的主題。

#### 社群網站品牌 {#community-site-branding}

![網站品牌](assets/site-branding.png)

社群網站品牌化是在每個頁面頂端以標題顯示的影像。

影像大小應如瀏覽器中頁面的預期顯示一樣寬，且高度應為120畫素。

建立或選取影像時，請記住：

* 影像高度會裁剪成從影像上邊緣測量的120畫素。
* 影像會釘選至瀏覽器視窗的左邊緣。
* 不會調整影像大小，因此當影像寬度為……

   * 小於瀏覽器的寬度，影像會水準重複。
   * 大於瀏覽器的寬度，影像看起來會遭到裁切。

* 選取&#x200B;**「下一步」**。

### 步驟3：設定 {#step-settings}

「設定」面板包含數個子面板，顯示了在移至建立網站的最後一步之前要設定的功能。

* [USER MANAGEMENT](#user-management)
* [標籤](#tagging)
* [角色](#roles)
* [稽核](#moderation)
* [ANALYTICS](#analytics)
* [翻譯](#translation)

>[!NOTE]
>
>**啟用通道服務**
>
>有幾個「設定」子面板允許指派受信任的成員來稽核UGC、管理群組或成為發佈環境中啟用資源的聯絡人。
>
>慣例適用於發佈端[使用者與使用者群組](/help/communities/users.md) （成員與成員群組），在製作環境中不可重複。
>
>因此，在製作環境中建立社群網站，並將受信任的成員指派給各種角色時，必須從發佈環境中擷取成員資料。
>
>這是透過為作者環境啟用` [AEM Communities Publish Tunnel Service](/help/communities/deploy-communities.md#tunnel-service-on-author)`來完成的。

#### USER MANAGEMENT {#user-management}

![createsitesettings](assets/createsitesettings.png)

* **允許使用者註冊**

  若勾選，網站訪客可透過自助註冊成為社群成員。
如果取消勾選，社群網站是*受限制的*，且網站訪客必須指派給社群網站的成員群組、提出要求或透過電子郵件傳送邀請。 如果未勾選，則不應允許匿名存取。
取消核取*私人*&#x200B;社群網站。 預設為已核取。

* **允許匿名存取**

  如果勾選，社群網站是&#x200B;*開啟*，任何網站訪客都可以存取該網站。
如果未勾選，則只有已登入的成員才能存取該網站。
取消核取*私人*&#x200B;社群網站。 預設為已核取。

* **允許傳訊**

  如果勾選，成員可以相互傳送訊息，並傳送給社群網站內的群組。
如果未勾選，則不會為社群設定訊息。
預設為未勾選。

* **允許社交登入： Facebook**

  如果勾選，可允許網站訪客使用其Facebook帳戶憑證登入。 選取的[Facebook雲端設定](/help/communities/social-login.md#create-a-facebook-connect-cloud-service)應設定為在建立社群網站後，將使用者新增至社群網站的成員群組。
如果未勾選，則不會顯示任何Facebook登入。
保留*私人*&#x200B;社群網站未勾選。 預設為未勾選。

* **允許社交登入：Twitter**

  如果勾選，可允許網站訪客使用其Twitter帳戶憑證登入。 選取的[Twitter雲端設定](/help/communities/social-login.md#create-a-twitter-connect-cloud-service)應設定為在建立社群網站後，將使用者新增至社群網站的成員群組。
如果未勾選，則不會顯示Twitter登入。
保留*私人*&#x200B;社群網站未勾選。 預設為未勾選。

>[!NOTE]
>
>**允許社交登入**
>
>雖然範例Facebook和Twitter設定可能存在，並且可供[生產環境](/help/sites-administering/production-ready.md)選擇，但必須建立自訂Facebook和Twitter應用程式。 請參閱[使用Facebook和Twitter的社交登入](/help/communities/social-login.md)。

#### 標籤 {#tagging}

![網站標籤](assets/site-tagging.png)

可套用至社群內容的標籤，可藉由選取先前透過[標籤主控台](/help/sites-administering/tags.md#tagging-console)定義的標籤名稱空間，加以控制。

此外，為社群網站選取標籤名稱空間會限制定義目錄和資源時顯示的選取範圍。

* 文字搜尋方塊：開始輸入以識別允許用於網站上的標籤。

#### 角色 {#roles}

![社群角色](assets/site-admin-2.png)

已指派這些設定給社群成員](/help/communities/users.md)的[角色。

使用預先輸入搜尋可輕鬆尋找社群成員。

* **社群管理員**

  開始輸入以選取一或多個可管理社群成員和成員群組的社群成員或成員群組。

* **社群版主**

  開始輸入以選取一或多個要信任為使用者產生內容之版主的社群成員或成員群組。

* **社群有特殊許可權的成員**

  開始輸入以選取一個或多個社群成員或成員群組，以便在已針對[社群功能](/help/communities/functions.md)選取`Allow Privileged Member`時，提供建立內容的能力。

* **社群管理員**

  開始輸入以選取一個或多個可以獨立於其他網站管理員和預設社群管理員來處理網站結構的網站管理員。 他們可以在階層架構的任何層級建立群組，並成為巢狀群組的預設管理員（但他們稍後可以從巢狀群組的管理員角色中移除）。

#### 稽核 {#moderation}

![網站稽核](assets/site-moderation.png)

用於仲裁使用者產生內容(UGC)的全域設定是由這些設定所控制。 個別元件有其他設定可控制調節。

* **內容已預先稽核**

  如果勾選，張貼的社群內容在版主核准前不會顯示。 預設為未勾選。 如需詳細資訊，請參閱[仲裁社群內容](/help/communities/moderate-ugc.md#premoderation)。

* **隱藏內容前的標幟臨界值**

  如果大於0，則在主題或貼文隱藏於公眾檢視之前必須加以標幟的次數。 如果設為–1，則已標幟的主題或貼文絕不會從公開檢視中隱藏。 預設值為5。

#### ANALYTICS {#analytics}

![網站分析](assets/site-analytics.png)

* **啟用Analytics**

  僅當[已針對Communities功能](/help/communities/analytics.md)設定Adobe Analytics時可用。
預設為未勾選。 勾選後，會出現另一個選取功能表：

![網站分析 — 啟用](assets/site-analytics-enable.png)

* **雲端設定框架參考**

  從下拉式功能表中，選取為此社群網站設定的Analytics Cloud服務架構。
  `Communities`是來自[Analytics Configuration for Communities Features](/help/communities/analytics.md#aem-analytics-framework-configuration)檔案的架構範例。

#### 翻譯 {#translation}

![網站翻譯](assets/site-translation.png)

* **允許機器翻譯**

  核取後（預設為未核取），網站內的UGC會啟用機器翻譯。 這不會影響任何其他內容，例如頁面內容，即使網站設定為多語言網站亦然。 如需設定AEM Communities授權翻譯服務的相關資訊，請參閱[翻譯使用者產生的內容](/help/communities/translate-ugc.md)。 請參閱[翻譯多語言網站的內容](/help/sites-administering/translation.md)，以取得完整的總覽。

![允許機器翻譯](assets/allow-machine-translation.png)

* **啟用所選語言的機器翻譯**

  為機器翻譯啟用的語言預設為[翻譯整合組態](/help/communities/translate-ugc.md#translation-integration-configuration)所指定的系統設定。 您可以刪除預設值和/或從下拉式功能表中選取其他語言，來覆寫此網站的預設設定。

* **選擇翻譯提供者**

  依預設，服務提供者為僅使用`microsoft`進行示範的試用服務。 如果沒有授權翻譯服務提供者，**應該取消勾選「允許機器翻譯」**。

* **選擇全域共用存放區**

  對於有多個語言副本的網站，全域共用存放區會提供單一對話對話串，從每個語言副本中可見。 若要這麼做，請選取其中一個語言作為語言副本。 預設值為&#x200B;*沒有全域共用存放區*。

* **選擇翻譯提供者設定**

  選擇為授權翻譯提供者建立的[翻譯整合架構](/help/sites-administering/tc-tic.md)。

* **選取您社群網站的翻譯選項**

   * **翻譯整個頁面**

     如果選取，頁面上的所有UGC都會轉譯為頁面的基本語言。

     預設為&#x200B;*未選取*。

   * **僅翻譯選取專案**

     如果選取，每個貼文旁都會顯示翻譯選項，可將個別貼文翻譯成頁面的基本語言。
預設為*已選取*。

* **選取持續性選項**

   * **翻譯使用者要求上的貢獻並於之後保留**
如果選取，內容在提出請求之前不會翻譯。 翻譯後，翻譯會儲存在存放庫中。

     預設為&#x200B;*未選取*。

   * **不要保留翻譯**

     如果選取，翻譯將不會儲存在存放庫中。

     如果未選取，則會持續翻譯。

     預設為&#x200B;*未選取*。

* **智慧型轉譯器**

  選取下列其中一項：

   * `Always show contributions in the original language` (預設)
   * `Always show contributions in user preferred language`
   * `Show contributions in user preferred language for only logged-in users`

### 步驟4 ：建立社群網站 {#step-create-communities-site}

如果需要任何調整，請使用&#x200B;**上一步**&#x200B;按鈕進行調整。

選取&#x200B;**建立**&#x200B;並啟動後，建立網站的程式便無法中斷。

網站建立後：

* 不支援變更url （節點名稱）。
* 社群網站範本的未來變更不會影響已建立的社群網站。
* 停用社群網站範本不會影響已建立的社群網站。
* 您可以修改社群網站的內容，以編輯社群網站的[結構](#modify-structure)。

![create-site](assets/create-site1.png)

程式完成時，新網站的資料夾會顯示在Communities Sites主控台中，作者可在其中新增頁面內容，或管理員可修改網站的屬性。

![modify-site-property](assets/modify-site-property.png)

若要編輯社群網站，請選取其專案資料夾以開啟它：

![網站專案](assets/site-project.png)

使用滑鼠將滑鼠游標停留在網站上或接觸網站卡片時，會出現允許下列專案的圖示：

* [在作者模式下編輯網站](#authoring-site-content)
* [開啟網站屬性以進行修改](#modifying-site-properties)
* [發佈網站](#publishing-the-site)
* [匯出網站](#exporting-the-site)
* [刪除網站](#deleting-the-site)

## 製作網站內容 {#authoring-site-content}

您可以使用與任何其他AEM網站相同的工具來編寫網站內容。 若要開啟網站進行製作，請選取滑鼠將網站懸停時顯示的`Open Site`圖示。 網站會在新標籤中開啟，社群網站主控台維持可供存取。

![網站內容](assets/site-content.png)

>[!NOTE]
>
>如果不熟悉AEM，請檢視有關[基本處理](/help/sites-authoring/basic-handling.md)的檔案和[編寫頁面的快速指南](/help/sites-authoring/qg-page-authoring.md)。

## 修改場地屬性 {#modifying-site-properties}

![編輯網站](assets/edit-site.png)

透過選取滑鼠將網站懸停時顯示的`Edit Site`圖示，可以修改網站建立過程中所指定的現有網站屬性。

`Details of the following properties match the descriptions provided in the` [網站建立](#site-creation)區段。

![modify-site-basicinfo](assets/modify-site-basicinfo.png)

### 修改基本 {#modify-basic}

「基本」面板允許修改：

* 社群網站標題
* 社群網站說明

社群網站名稱不可修改。

選擇不同的社群網站範本並不會對現有社群網站造成影響，因為範本和網站之間沒有連線。

相反地，可以修改社群網站的[結構](#modify-structure)。

### 修改結構 {#modify-structure}

「結構」面板允許修改最初從所選社群網站範本建立的結構。 您可以從面板執行下列作業：

* 將其他[社群功能](/help/communities/functions.md)拖放至網站結構。
* 在網站結構中的社群功能例項上：

   * **`gear icon`**

     編輯設定，包括顯示標題和URL名稱，以及[有特殊許可權的成員群組](/help/communities/users.md#privilegedmembersgroups)。

   * **`trashcan icon`**

     從網站結構中移除（刪除）函式。

   * **`grid icon`**

     修改網站最上層導覽列中顯示的函式順序。

>[!NOTE]
>
>您可以變更「場地結構」中所有函式的順序，但頂端的函式除外。 因此，無法變更社群網站的首頁。

>[!CAUTION]
>
>* 雖然顯示標題可能會變更而不會產生副作用，但建議您不要編輯屬於社群網站的社群功能的URL名稱。
>
>例如，重新命名URL不會移動現有UGC，因此「遺失」UGC。

>[!CAUTION]
>
>群組函式必須&#x200B;*不是*&#x200B;網站結構中的&#x200B;*第一個，也不是唯一的*&#x200B;函式。
>
>必須包含其他任何函式，例如[頁面函式](/help/communities/functions.md#page-function)，並先列出。

#### 範例：新增目錄函式至社群網站結構 {#example-adding-a-catalog-function-to-a-community-site-structure}

![add-catalog-site](assets/add-catalog-site.png)

### 修改設計 {#modify-design}

DESIGN面板允許套用新的主題：

* [社群網站主題](#community-site-theme)
* [社群網站品牌](#community-site-branding)

   * 捲動至面板底部，以便變更品牌影像。

### 修改設定 {#modify-settings}

「設定」面板可讓您存取子面板下的大部分設定，以用於建立社群網站的步驟3：

* [使用者管理](#user-management)
* [標記](#tagging)
* [審核](#moderation)
* [會員角色](#roles)
* [分析](#analytics)
* [轉換](#translation)

### 修改縮圖 {#modify-thumbnail}

「縮圖」面板可讓您上傳影像，以便在Communities Sites主控台中代表網站。

## 發佈網站 {#publishing-the-site}

建立或修改社群網站後，可以選取滑鼠停留在網站上方時顯示的`Publish Site`圖示來發佈（啟動）網站。

![publish-site](assets/publish-site.png)

成功發佈網站後會有提示。

![網站已發佈](assets/site-published.png)

### 使用巢狀群組發佈 {#publishing-with-nested-groups}

發佈社群網站後，必須個別發佈使用[群組主控台](/help/communities/groups.md)建立的每個子社群（巢狀群組）。

## 匯出網站 {#exporting-the-site}

![export-site](assets/export-site.png)

選取匯出圖示，將滑鼠停留在網站上，即可建立社群網站的套件，該套件同時儲存在[套件管理員](/help/sites-administering/package-manager.md)中並下載。

UGC未包含在網站套件中。

## 刪除網站 {#deleting-the-site}

![deleteicon](assets/deleteicon.png)

若要刪除社群網站，請選取將滑鼠游標停留在Communities網站主控台的網站上方時顯示的刪除網站圖示。 此動作會移除與網站相關聯的所有專案，例如UGC、使用者群組、資產和資料庫記錄。

## 已建立的社群使用者群組 {#created-community-user-groups}

發佈新的社群網站後，新的成員群組（在發佈環境中建立使用者群組）會擁有針對各種管理和成員角色設定的適當許可權。

為成員群組建立的名稱包含[步驟1](#step13asitetemplate)中指定的&#x200B;*site-name* （出現在URL中的名稱）。 它也包括唯一ID，以避免與不同社群網站根目錄具有相同網站名稱的社群網站和群組發生衝突。

例如，如果標題為「快速入門教學課程」的網站名稱為「engage」，則版主的使用者群組為：

* title：社群參與版主
* 名稱： community-*engage-uid*-moderators

任何在建立場地時，被指派為版主或群組管理員角色的成員，都會被指派給適當的群組並指派給成員群組。 發佈新網站時，會在發佈上建立這些群組和成員指派。

如需詳細資訊，請參閱[管理使用者和使用者群組](/help/communities/users.md)。

>[!NOTE]
>
>如果[允許社交登入： Facebook](#user-management)已啟用，則使用者群組`community-<site-name>-<uid>-members`後
>已建立，套用的[Facebook雲端服務](/help/communities/social-login.md#createafacebookcloudservice)應設定為新增使用者至此群組。

## 設定驗證錯誤 {#configure-for-authentication-error}

依預設，當使用者輸入錯誤的憑證而無法登入時，社群網站會重新導向至範例登入頁面。 此範例登入不存在於[生產伺服器](/help/sites-administering/production-ready.md)上。

若要正確重新導向，在設定網站並推送至發佈後，請完成下列步驟，以取得驗證失敗，重新導向至社群網站：

* 在每個AEM發佈執行個體上。
* 以系統管理員許可權登入。
* 存取[網頁主控台](/help/sites-deploying/configuring-osgi.md)。

   * 例如，[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)。

* 找到`Adobe Granite Login Selector Authentication Handler`。
* 選取`pencil`圖示，以開啟設定進行編輯。
* 請依照下列方式輸入&#x200B;**登入頁面對應**：

  `/content/sites/<site-name>/path/to/login/page:/content/sites/<site-name>`

  例如：
  `/content/sites/engage/en/signin:/content/sites/engage/en`

* 選取「**儲存**」。

![auth-error](assets/auth-error.png)

### 測試驗證重新導向 {#test-authentication-redirection}

在設定了社群網站登入頁面對應的相同AEM發佈執行個體上：

* 瀏覽至社群網站首頁。

   * 例如，[https://localhost:4503/content/sites/engage/en.html](https://localhost:4503/content/sites/engage/en.html)

* 選取「登出」。
* 選取「登入」。
* 輸入不正確的認證，例如使用者名稱&quot;x&quot;和密碼&quot;x&quot;。
* 登入頁面應顯示「無效登入」錯誤。

![測試驗證](assets/test-authentication.png)

## 從主要網站主控台存取社群網站 {#accessing-community-sites-from-main-sites-console}

從全域導覽Sites主控台，社群網站位於`Community Sites`資料夾。

雖然以此方式存取社群網站是可行的，但針對管理任務，社群網站應從「社群網站」主控台存取。

![存取網站](assets/access-site.png)
