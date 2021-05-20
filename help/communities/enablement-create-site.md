---
title: 製作新的社群網站以進行培訓
seo-title: 製作新的社群網站以進行培訓
description: 建立社群網站以進行啟用
seo-description: 建立社群網站以進行啟用
uuid: a75fa566-a570-45fd-aabc-23651ef819cc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: b9333558-6af9-46b2-9f03-3722645c69a6
docset: aem65
exl-id: 812bbf7b-c49f-4c34-a47d-636b0468e0ba
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1728'
ht-degree: 2%

---

# 製作新的啟用社群網站{#author-a-new-community-site-for-enablement}

## 建立社群網站 {#create-community-site}

[社區站](/help/communities/sites-console.md) 點建立採用嚮導，引導您完成建立社區站點的步驟。在最終步驟中提交站點之前，可以前進到`Next`步驟或`Back`到上一步。

若要開始建立新的社群網站：

使用[author例項](https://localhost:4502/)

* 以管理員權限登錄，並導航至&#x200B;**[!UICONTROL Communities]** > **[!UICONTROL Sites]**。

* 選擇 **建立**。

### 步驟1 :站點模板{#step-site-template}

![啟用網站範本](assets/enablement-site-template.png)

在&#x200B;**網站範本**&#x200B;步驟中，輸入標題、說明、URL名稱，並選取社群網站範本，例如：

* **社群網站標題**: `Enablement Tutorial`.

* **社群網站說明**: `A site for enabling the community to learn.`

* **社區站點根**:(預設根保留空白 `/content/sites`)

* **雲端設定**:（若未指定雲端設定，則保留空白）提供指定雲端設定的路徑。
* **社區站點基語言**:(單一語言不受影響：英文)使用下拉式清單，從 *可用* 的語言中選擇一或多種基本語言 — 德文、義大利文、法文、日文、西班牙文、葡萄牙文（巴西）、中文（繁體）和中文（簡體）。系統會針對每個新增的語言建立一個社群網站，並依照[多語言網站轉譯內容](/help/sites-administering/translation.md)中所述的最佳作法，存在於相同的網站資料夾中。 每個網站的根頁面都會包含一個子頁面，其名稱是所選語言之一的語言代碼，例如英文為「en」，法文為「fr」。

* **社群網站名稱**: `enable`

   * 初始URL將顯示在「社群網站名稱」下方
   * 為了有效的URL，請附加基本語言代碼+ &quot;。html&quot;
      *例如*, https://localhost:4502/content/sites/  `enable/en.html`

* **參考網站範本**:下拉式選擇  `Reference Structured Learning Site Template`

選擇&#x200B;**Next**。

### 步驟2 :設計{#step-design}

「設計」步驟會分兩節顯示，用於選取主題和品牌橫幅：

#### 社區站點主題{#community-site-theme}

選取要套用至範本的所需樣式。 選取後，主題將會以勾號覆蓋。

#### 社區站點品牌{#community-site-branding}

（選用）上傳橫幅影像以在網站頁面間顯示。 橫幅會釘在瀏覽器的左側邊緣、社群網站標題和功能表（導覽連結）之間。 橫幅高度會裁切為120像素。 橫幅沒有調整大小以符合瀏覽器寬度和120像素高度。

![站點品牌1](assets/site-branding1.png)

![網站品牌推廣2](assets/site-branding2.png)

選擇&#x200B;**Next**。

### 步驟3 :設定{#step-settings}

在「設定」步驟中，在選取`Next`之前，請注意有七個區段提供存取設定的功能，包括使用者管理、標籤、角色、協調、分析、翻譯和啟用。

#### 用戶管理{#user-management}

建議將[啟用社群](/help/communities/overview.md#enablement-community)設為私人。

當匿名網站訪客被拒絕訪問、不能自行註冊，以及不能使用社交登錄時，社群網站是私有的。

確保為[User Management](/help/communities/sites-console.md#user-management)取消選中大多數複選框：

* 請勿允許網站訪客自行註冊。
* 不允許匿名網站訪客檢視網站。
* 是否允許社群成員之間傳送訊息為選用。
* 不允許使用Facebook登入。
* 不允許使用Twitter登入。

![user-mgmt](assets/user-mgmt.png)

#### 標籤 {#tagging}

可套用至社群內容的標籤，是透過選取先前透過[標籤控制台](/help/sites-administering/tags.md#tagging-console)（例如[教學課程命名空間](/help/communities/enablement-setup.md#create-tutorial-tags)）定義的AEM命名空間來控制。

此外，為社群網站選取「標籤命名空間」，會限制定義目錄和啟用資源時顯示的選取項目。 如需重要資訊，請參閱[標籤啟用資源](/help/communities/tag-resources.md) 。

使用預先輸入搜尋可輕鬆找到命名空間。 例如，

* 類型 `tut`
* 選取 `Tutorial`

![啟用標籤](assets/enablement-tagging.png)

### 角色 {#roles}

[社群成](/help/communities/users.md) 員角色是透過「角色」區段中的設定來指派。

若要讓社區成員（或成員組）以社區管理員的身份體驗站點，請使用「預先鍵入」搜索並從下拉清單中的選項中選擇成員或組名稱。

例如，

* 類型 `q`
* 選擇[Quinn Harper](/help/communities/enablement-setup.md#publishcreateenablementmembers)

>[!NOTE]
>
>[通道](/help/communities/deploy-communities.md#tunnel-service-on-author) 服務允許選擇僅存在於發佈環境中的成員和組。

![啟用角色](assets/site-admin.png)

#### 協調 {#moderation}

接受[調節](/help/communities/sites-console.md#moderation)用戶生成內容(UGC)的預設全局設定。

![moderation1](assets/moderation1.png)

#### ANALYTICS {#analytics}

從下拉式清單中，選取為此社群網站設定的Analytics雲端服務架構。

螢幕截圖中顯示的選項`Communities`是[配置文檔中的框架示例。](/help/communities/analytics.md#aem-analytics-framework-configuration)

![分析](assets/analytics.png)

#### 翻譯 {#translation}

[翻譯設定](/help/communities/sites-console.md#translation)指定UGC是否可翻譯，如果可以，則可以翻譯到哪種語言。

* 檢查&#x200B;**允許機器翻譯**
* 使用預設設定

![轉換](assets/translation.png)

#### 啟用 {#enablement}

對於啟用社群，您必須識別一或多個社群啟用管理員。

* **啟用管理員**
（必要） 
`Community Enablement Managers` 可選擇組以管理此社區站點。

   * 類型 `s`
   * 選取 `Sirius Nilson`

* **Marketing Cloud組織Id**
（選用）Adobe Analytics帳戶的ID，在啟用報表中加入視訊心 [率分](/help/communities/analytics.md#video-heartbeat-analytics) 析時必需。

![啟用](assets/enablement.png)

選擇&#x200B;**Next**。

### 步驟4 :建立社區站點{#step-create-community-site}

選擇&#x200B;**建立。**

![預覽](assets/preview.png)

過程完成後，新站點的資料夾將顯示在「社區」>「站點」控制台中。

![enablementsitecreated](assets/enablementsitecreated.png)

### 發佈新社區站點{#publish-the-new-community-site}

應從Communities - Sites控制台管理建立的站點，該控制台與可建立新站點的控制台相同。

選取社群網站的資料夾後，將滑鼠指標暫留在網站圖示上，以便顯示四個動作圖示：

![Siteactionicons](assets/siteactionicons.png)

選取點圖示（更多動作圖示）時，會顯示「匯出網站」和「刪除網站」選項。

![網站活動新](assets/siteactionsnew.png)

從左到右為：

* **開啟網站**

   選取鉛筆圖示以在作者編輯模式中開啟社群網站，以新增和/或設定頁面元件。

* **編輯網站**

   選取屬性圖示以開啟社群網站以修改屬性，例如標題或以變更主題。

* **發佈網站**

   選取要發佈社群網站的世界圖示（預設為localhost:4503）。

* **匯出網站**

   選擇導出表徵圖可建立同時儲存在[包管理器](/help/sites-administering/package-manager.md)中和下載的社區站點的包。
請注意，網站套件中未包含UGC。

* **刪除網站**

   要刪除社區站點，請選擇「社區站點控制台」中滑鼠懸停在站點上時顯示的「刪除站點」表徵圖。 此動作會移除與網站相關聯的所有項目，例如UGC、使用者群組、資產和資料庫記錄。

   ![enablesiteactions](assets/enablesiteactions.png)

#### 選擇發佈{#select-publish}

選取發佈社群網站的世界圖示。

![發佈網站](assets/publish-site.png)

網站已發佈的跡象。

![網站發佈](assets/site-published.png)

## 社群使用者和使用者群組{#community-users-user-groups}

### 注意新社區用戶組{#notice-new-community-user-groups}

除了新的社群網站外，還會建立新的使用者群組，這些使用者群組具有針對各種管理功能所設定的適當權限。 如需詳細資訊，請造訪[社群網站的使用者群組](/help/communities/users.md#usergroupsforcommunitysites)。

對於這個新的社群網站，在步驟1中指定網站名稱「enable」時，可從[社群成員和群組控制台](/help/communities/members.md#groups-console)中看到發佈環境中存在的新使用者群組：

![community_usergroup](assets/community_usergroup.png)

### 將成員分配給社區啟用成員組{#assign-members-to-community-enable-members-group}

在作者上，啟用通道服務後，可將在初始設定期間建立的[使用者指派給新建立社群網站的社群成員群組。](/help/communities/enablement-setup.md#publishcreateenablementmembers)

使用「社群群組」主控台，可以個別新增成員，或透過群組的成員資格新增成員。

在此示例中，組`Community Ski Class`被添加為組`Community Enable Members`的成員以及成員`Quinn Harper`。

* 導覽至&#x200B;**社群、群組**&#x200B;主控台
* 選擇&#x200B;*社區啟用成員*&#x200B;組
* 在&#x200B;**向組添加成員**&#x200B;搜索框中輸入&#39;ski&#39;
* 選擇&#x200B;*社區滑雪課*（學習者組）
* 在搜索框中輸入&#39;quinn&#39;
* 選擇&#x200B;*Quinn Harper*（啟用資源聯繫人）

* 選擇&#x200B;**保存**

![編輯組設定](assets/edit-group-settings.png)

## 發佈時的配置{#configurations-on-publish}

`https://localhost:4503/content/sites/enable/en.html {#http-localhost-content-sites-enable-en-html}`

![啟用登入](assets/enablement-login.png)

### 配置身份驗證錯誤{#configure-for-authentication-error}

將網站設定並推送至發佈後，請在發佈執行個體上設定登入對應](/help/communities/sites-console.md#configure-for-authentication-error)(`Adobe Granite Login Selector Authentication Handler`)。 [好處是當未正確輸入登入憑證時，驗證錯誤將會以錯誤訊息重新顯示社群網站的登入頁面。

將`Login Page Mapping`新增為：

* `/content/sites/enable/en/signin:/content/sites/enable/en`

### （選用）變更預設首頁{#optional-change-the-default-home-page}

使用發佈網站以進行示範時，將預設首頁變更為新網站可能會很實用。

要執行此操作，需要使用[CRX|DE](https://localhost:4503/crx/de) Lite來編輯發佈時的[資源映射](/help/sites-deploying/resource-mapping.md)表。

若要開始：

1. 發佈時，請存取CRXDE並使用管理員權限登入

   * 例如，瀏覽至[https://localhost:4503/crx/de](https://localhost:4503/crx/de)並使用`admin/admin`登入

1. 在專案瀏覽器中，展開`/etc/map`
1. 選擇`http`節點

   * 選擇&#x200B;**建立節點**

      * **** Namelocalhost.4503

         （do *not*&#x200B;使用「：」）

      * **** [類型：映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. 已選擇新建立的`localhost.4503`節點

   * 新增屬性

      * **** 命名：match
      * **** TypeString
      * **** Valuelocalhost.4503/$

   （必須以「$」字元結尾）

   * 新增屬性

      * **** 命名：internalRedirect
      * **** TypeString
      * **值** /content/sites/enable/en.html


1. 選擇&#x200B;**保存全部**
1. （選用）刪除瀏覽歷史記錄
1. 瀏覽至https://localhost:4503/

   * 到達https://localhost:4503/content/sites/enable/en.html

>[!NOTE]
>
>若要停用，只需在`sling:match`屬性值的前面加上「x」 — `xlocalhost.4503/$` — 和&#x200B;**儲存全部**&#x200B;即可。

![change-default-homepage](assets/change-default-homepage.png)

#### 疑難排解：保存映射{#troubleshooting-error-saving-map}時出錯

如果無法保存更改，請確保節點名稱為`localhost.4503`（帶有「點」分隔符），而不是帶有「冒號」分隔符的`localhost:4503`，因為`localhost`不是有效的命名空間前置詞。

![error-map](assets/error-map.png)

#### 疑難排解：無法重定向{#troubleshooting-fail-to-redirect}

規則運算式`sling:match`字串結尾的「**$**」很重要，因此只有`https://localhost:4503/`已完全對應，否則重新導向值會加在URL中server:port之後可能存在的任何路徑前面。 因此，當AEM嘗試重新導向至登入頁面時，會失敗。

## 修改社區站點{#modifying-the-community-site}

網站初次建立後，作者可使用[開啟網站圖示](/help/communities/sites-console.md#authoring-site-content)執行標準AEM製作活動。

此外，管理員可以使用[編輯站點表徵圖](/help/communities/sites-console.md#modifying-site-properties)來修改站點的屬性，如標題。

進行任何修改後，請記得&#x200B;**Save**&#x200B;並重新&#x200B;**Publish**&#x200B;網站。

>[!NOTE]
>
>若不熟悉AEM，請檢視[basic handling](/help/sites-authoring/basic-handling.md)和[製作頁面快速指南](/help/sites-authoring/qg-page-authoring.md)的相關檔案。

### 添加目錄{#add-a-catalog}

為此社區站點選擇的社區站點模板應包含目錄功能。

若未包含，則可輕鬆新增目錄功能。 這可讓社群的其他成員（未指派給啟用資源或學習路徑）從目錄中選取啟用資源。

如果網站結構已包含目錄功能，則可變更其標題。

要修改站點的結構，請導航到&#x200B;**[!UICONTROL Communities]** > **[!UICONTROL Sites]**&#x200B;控制台，開啟`enable`資料夾，並選擇&#x200B;**Edit Site**&#x200B;表徵圖以訪問`Enablement Tutorial`的屬性。

選取「結構」面板以新增目錄或修改現有目錄：

* **標題**: `Ski Catalog`

* **URL**:  `catalog`

* **選取所有命名空間**:保留為預設值。

* 選擇&#x200B;**保存**。

![modify-site-structure](assets/modify-site-structure.png)

使用「位置」表徵圖將「目錄」函式移動到「工作總攬」後的第二個位置。

![move-catalog-func](assets/move-catalog-func.png)

選擇右上角的&#x200B;**Save**&#x200B;以保存對社區站點的更改。

然後重新發佈網站&#x200B;**。**
