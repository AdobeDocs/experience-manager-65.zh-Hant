---
title: 編寫社群網站
description: 瞭解如何撰寫Adobe Experience Manager Communities網站。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: d4c1895f-421c-4146-b94a-8d11065ef9e3
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 0%

---

# 編寫社群網站{#author-a-new-community-site}

## 建立社群網站 {#create-a-community-site}

使用作者例項建立社群網站。 在AEM編寫執行個體上：

1. 以系統管理員許可權登入。
1. 從全域導覽，前往&#x200B;**[!UICONTROL 社群]** > **[!UICONTROL 網站]**。

Communities Sites主控台會提供精靈，引導使用者完成建立社群網站的步驟。 在認可最後一個步驟中的網站之前，可以前進到`Next`步驟或`Back`到上一個步驟。

若要開始建立社群網站：

* 選取`Create`按鈕。

![createcommunitysite](assets/createcommunitysite.png)

### 步驟1：網站範本 {#step-site-template}

![要建立網站的範本](assets/create-site.png)

在[網站範本步驟](/help/communities/sites-console.md#step2013asitetemplate)中，輸入標題、說明、URL的名稱，然後選取社群網站範本，例如：

* **社群網站標題**： `Getting Started Tutorial`
* **社群網站描述**： `A site for engaging with the community.`
* **社群網站根目錄**： （預設根目錄`/content/sites`保留空白）
* **雲端設定**： （若未指定雲端設定，則保留空白）提供指定雲端設定的路徑。
* **社群網站基本語言**： （單一語言則保持原樣：英文）使用下拉式清單，從可用的語言(德文、義大利文、法文、日文、西班牙文、葡萄牙文（巴西）、中文（繁體）及中文（簡體）)中選擇一種&#x200B;*或更多*&#x200B;種基本語言。 已針對新增的每種語言建立一個社群網站，並遵循[翻譯多語言網站的內容](/help/sites-administering/translation.md)中所述的最佳實務，存在於相同的網站資料夾中。 每個網站的根頁面都包含一個子頁面，該子頁面是以其中一個選取語言的語言代碼來命名，例如「en」代表英文，「fr」代表法文。

* **社群網站名稱**：參與

   * 請仔細檢查名稱，因為網站建立後不易變更
   * 初始URL會顯示在社群網站名稱下方
   * 若要取得有效的URL，請附加基本語言代碼+ &quot;。html&quot;
   * *例如*，https://localhost:4502/content/sites/ `engage/en.html`

* **範本**：下拉式以選擇`Reference Site`

* 選取&#x200B;**「下一步」**。

### 步驟2：設計 {#step-design}

「設計」步驟顯示在兩個區段中，用於選取主題和品牌化橫幅：

#### 社群網站主題 {#community-site-theme}

選取要套用至範本的所需樣式。 選取時，佈景主題上會覆蓋一個核取記號。

#### 社群網站品牌 {#community-site-branding}

（選用）上傳橫幅影像，以在網站頁面上顯示。 橫幅會釘選至瀏覽器左邊緣，位於社群網站標題與導覽連結之間。 橫幅高度會裁剪為120畫素。 橫幅不會調整大小以符合瀏覽器的寬度和120畫素的高度。

![社群網站品牌](assets/community-site-branding.png)

![upload-image-site](assets/upload-image-site.png)

選取&#x200B;**「下一步」**。

### 步驟3：設定 {#step-settings}

在「設定」步驟中，在選取`Next`之前，有7個區段可存取涉及使用者管理、標籤、稽核、群組管理、分析和翻譯的設定。

#### 使用者管理 {#user-management}

勾選[使用者管理](/help/communities/sites-console.md#user-management)的所有核取方塊

* 允許網站訪客自行註冊
* 允許網站訪客在不登入的情況下檢視網站
* 允許成員傳送和接收來自其他社群成員的訊息
* 允許使用Facebook登入，而非註冊和建立設定檔
* 允許使用Twitter登入，而不是註冊和建立設定檔

>[!NOTE]
>
>對於生產環境，必須建立自訂Facebook和Twitter應用程式。 請參閱[使用Facebook和Twitter的社交登入](/help/communities/social-login.md)。

![社群網站設定](assets/site-settings.png)

#### 標籤 {#tagging}

套用至社群內容的標籤是透過選取先前透過[標籤主控台](/help/sites-administering/tags.md#tagging-console)定義的AEM名稱空間（例如[教學課程名稱空間](/help/communities/setup.md#create-tutorial-tags)）來控制。

使用預先輸入搜尋可輕鬆尋找名稱空間。 例如，

* 型別`tut`
* 選取`Tutorial`

![標籤](assets/tagging.png)

#### 角色 {#roles}

已透過[角色]區段中的設定指派[社群成員角色](/help/communities/users.md)。

若要讓社群成員（或成員群組）以社群管理員身分體驗網站，請使用預先輸入搜尋，並從下拉式清單中的選項中選取成員或群組名稱。

例如，

* 型別`q`
* 選取Quinn Harper

>[!NOTE]
>
>[通道服務](https://helpx.adobe.com/tw/experience-manager/6-3/help/communities/deploy-communities.html#tunnel-service-on-author)允許選取僅存在於發佈環境中的成員和群組。

新網站中的![個使用者角色](assets/site-admin-1.png)

#### 稽核 {#moderation}

接受[仲裁](/help/communities/sites-console.md#moderation)使用者產生的內容(UGC)的預設全域設定。

![稽核](assets/moderation1.png)

#### ANALYTICS {#analytics}

如果Adobe Analytics已獲得授權，且已設定Analytics Cloud服務和架構，則您可以啟用Analytics並選取架構。

請參閱[社群功能的Analytics設定](/help/communities/analytics.md)。

![分析](assets/analytics.png)

#### 翻譯 {#translation}

[翻譯設定](/help/communities/sites-console.md#translation)會指定網站的基本語言，以及是否可翻譯UGC及翻譯成何種語言（如果可以）。

* 檢查&#x200B;**允許機器翻譯**
* 保留預設機器翻譯服務選取的預設翻譯語言
* 保留預設翻譯提供者和設定
* 不需要全域存放區，因為沒有語言副本
* 選取&#x200B;**翻譯整個頁面**
* 保留預設持續性選項

![翻譯設定](assets/translation-settings.png)

### 步驟4：建立社群網站 {#step-create-communities-site}

選取&#x200B;**建立。**

![create-site](assets/create-site2.png)

程式完成後，新網站的資料夾會顯示在Communities - Sites主控台中。

![communitiessitesconsole](assets/communitiessitesconsole.png)

## Publish社群網站 {#publish-the-community-site}

建立的網站應從「社群 — 網站」主控台進行管理，該主控台與可建立新網站的主控台相同。

選取社群網站的資料夾以開啟後，將滑鼠指標暫留在網站圖示上，便會顯示四個動作圖示：

![siteactionicons-1](assets/siteactionicons-1.png)

選取第四個橢圓圖示（「更多動作」）時，會顯示「匯出網站」和「刪除網站」選項。

![siteactionsnew-1](assets/siteactionsnew-1.png)

從左到右分別是：

* **開啟網站**

  選取鉛筆圖示會以作者編輯模式開啟社群網站，您可在此新增或設定頁面元件。

* **編輯網站**

  選取屬性圖示會開啟社群網站以修改屬性，例如標題或變更主題。

* **Publish網站**

  選取世界圖示會發佈社群網站（例如，如果您的發佈伺服器在本機電腦上執行，則預設會發佈至localhost：4503）。

* **匯出網站**

  選取匯出圖示會建立社群網站的封裝，此封裝儲存在[封裝管理員](/help/sites-administering/package-manager.md)中並下載。 UGC未包含在網站套件中。

* **刪除網站**

  選取刪除圖示會從&#x200B;**[!UICONTROL 社群>網站主控台]**&#x200B;內刪除社群網站。 此動作會移除與網站相關聯的所有專案，例如UGC、使用者群組、資產和資料庫記錄。

![siteactions](assets/siteactions.png)

>[!NOTE]
>
>如果未使用發佈執行個體的預設連線埠4503，請編輯預設的復寫代理程式，以將連線埠號碼設定為正確的值。
>
>在作者執行個體上，從主功能表：
>
>1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 復寫]**&#x200B;功能表。
>1. 選取作者&#x200B;**上的**&#x200B;代理程式。
>1. 選取&#x200B;**[!UICONTROL 預設代理程式（發佈）]**。
>1. 在&#x200B;**[!UICONTROL 設定]**&#x200B;旁邊，選取&#x200B;**[!UICONTROL 編輯]**。
>1. 在[代理程式設定]的快顯對話方塊中，選取&#x200B;**[!UICONTROL 傳輸]**&#x200B;索引標籤。
>1. 在URI中，將連線埠號碼4503變更為所需的連線埠號碼。 例如，使用連線埠6103： https://localhost:6103/bin/receive?sling:authRequestLogin=1
>1. 選取&#x200B;**[!UICONTROL 確定]**。
>1. （選擇性）選取&#x200B;**[!UICONTROL 清除]**&#x200B;或&#x200B;**[!UICONTROL 強制重試]**&#x200B;以重設復寫佇列。

### 選取Publish {#select-publish}

確認發佈伺服器執行後，選取世界圖示以發佈社群網站。

![publish-site](assets/publish-site.png)

成功發佈社群網站後，訊息會短暫出現「網站已發佈」。

### 新增社群使用者群組 {#new-community-user-groups}

隨著新社群網站的建立，新的使用者群組會針對各種管理功能設定適當的許可權。 如需詳細資訊，請造訪[社群網站的使用者群組](/help/communities/users.md#usergroupsforcommunitysites)。

對於這個新的社群網站，在步驟1中指定網站名稱「engage」，可能會從[群組主控台](/help/communities/members.md) （全域導覽：社群、群組）看到四個新的使用者群組：

* 社群參與社群管理員
* 社群參與群組管理員
* 社群參與成員
* 社群參與版主
* 社群參與有特殊許可權的成員
* 社群參與網站內容管理員

[Aaron McDonald](/help/communities/tutorials.md#demo-users)是

* 社群參與社群管理員
* 社群參與版主
* Community Engage成員（間接身為版主群組的成員）

![使用者群組](assets/user-group.png)

#### https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![參與](assets/engage.png)

## 設定驗證錯誤 {#configure-for-authentication-error}

設定網站並推送至發佈後，請在發佈執行個體上[設定登入對應](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`)。 優點在於，當登入認證未正確輸入時，驗證錯誤會重新顯示社群網站的登入頁面，並顯示錯誤訊息。

將`Login Page Mapping`新增為

* `/content/sites/engage/en/signin:/content/sites/engage/en`

## 可選步驟 {#optional-steps}

### 變更預設首頁 {#change-the-default-home-page}

使用發佈網站進行示範時，將預設首頁變更為新網站可能會有幫助。

若要這麼做，需要使用[CRXDE](https://localhost:4503/crx/de) Lite來編輯發佈上的[資源對應](/help/sites-deploying/resource-mapping.md)資料表。

若要開始使用：

1. 在發佈執行個體上，使用管理員許可權登入。
1. 瀏覽至[https://localhost:4503/crx/de](https://localhost:4503/crx/de)。
1. 在專案瀏覽器中，展開`/etc/map.`
1. 選取`http`節點：

   * 選取&#x200B;**建立節點：**

      * **名稱** localhost.4503
（請*不*&#x200B;使用&#39;：&#39;）

      * **型別** [sling：Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. 選取新建立的`localhost.4503`節點：

   * 新增屬性：

   * **名稱** sling：match
      * **型別**&#x200B;字串
      * **值** localhost.4503/$
（結尾必須是「$」字元）

   * 新增屬性：

      * **名稱** sling：internalRedirect
      * **型別**&#x200B;字串
      * **值** /content/sites/engage/en.html

1. 選取&#x200B;**全部儲存。**
1. （選用）刪除瀏覽記錄。
1. 瀏覽至https://localhost:4503/。

   * 送達https://localhost:4503/content/sites/engage/en.html

>[!NOTE]
>
>若要停用，只要在`sling:match`屬性值前面加上&#39;x&#39; - `xlocalhost.4503/$` — 和&#x200B;**全部儲存**&#x200B;即可。

![optional-steps](assets/optional-steps.png)

#### 疑難排解：儲存地圖時發生錯誤 {#troubleshooting-error-saving-map}

如果無法儲存變更，請確定節點名稱為`localhost.4503` （帶有&#39;dot&#39;分隔符號），而不是`localhost:4503` （帶有&#39;colon&#39;分隔符號），因為`localhost`不是有效的名稱空間前置詞。

![錯誤訊息](assets/error-message.png)

#### 疑難排解：無法重新導向 {#troubleshooting-fail-to-redirect}

規則運算式`sling:match`字串結尾的&#39;**$**&#39;很關鍵，因此只有`https://localhost:4503/`會進行對應，否則重新導向值會以URL中server：port後面可能存在的任何路徑為前置詞。 因此，當AEM嘗試重新導向到登入頁面時，它會失敗。

### 修改網站 {#modify-the-site}

網站初次建立後，作者可使用[開啟網站圖示](/help/communities/sites-console.md#authoring-site-content)執行標準的AEM編寫活動。

此外，管理員可以使用[編輯網站圖示](/help/communities/sites-console.md#modifying-site-properties)來修改網站的內容，例如標題。

進行任何修改之後，請記得將&#x200B;**儲存**&#x200B;並重新&#x200B;**Publish**&#x200B;網站。

>[!NOTE]
>
>如果不熟悉AEM，請檢視有關[基本處理](/help/sites-authoring/basic-handling.md)的檔案和[編寫頁面的快速指南](/help/sites-authoring/qg-page-authoring.md)。
