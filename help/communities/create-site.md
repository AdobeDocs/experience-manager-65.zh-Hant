---
title: 製作新社群網站
seo-title: 製作新社群網站
description: 如何製作新的AEM Communities網站
seo-description: 如何製作新的AEM Communities網站
uuid: 4f609f5f-ef07-44fc-aeb3-1c616e120d46
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8ae324ea-8b84-47a3-aabf-1fee2a3bd46d
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# 製作新社群網站{#author-a-new-community-site}

## 建立社群網站 {#create-a-community-site}

使用作者例項建立社群網站。 在AEM Author例項上：

1. 以管理員權限登入。
1. 從全域導覽，前往導 **覽、社群、網站。**

Communities Sites控制台提供了嚮導，可引導用戶完成建立社區站點的步驟。 在最後一步中提 `Next`交站 `Back`點之前，可以前進到步驟或上一步。

要開始建立新的社區站點，請執行以下操作：

* 選擇按 `Create`鈕。

![createcommunitysite](assets/createcommunitysite.png)

### 步驟1:網站範本 {#step-site-template}

![建立網站的範本](assets/create-site.png)

在「網 [站範本」步驟中](/help/communities/sites-console.md#step2013asitetemplate)，輸入標題、說明、URL名稱，並選取社群網站範本，例如：

* **社群網站標題**: `Getting Started Tutorial`
* **社群網站說明**: `A site for engaging with the community.`
* **社群網站根**:(對於預設根，保留空白 `/content/sites`)
* **雲端設定**:（若未指定雲端設定，請留空）提供指定雲端設定的路徑。
* **社群網站基本語言**:（單語言不受影響）英文)使用下拉式清單，從 *可用語言* (德文、義大利文、法文、日文、西班牙文、葡萄牙文（巴西）、中文（繁體）和簡體中文)選擇一或多種基本語言。 會針對新增的每種語言建立一個社群網站，並依照多語言網站翻譯內容中所述的最佳實務，存在於相 [同的網站資料夾中](/help/sites-administering/translation.md)。 每個網站的根頁面將包含一個子頁面，該子頁面由其中一種語言的語言代碼命名，例如英文的&#39;en&#39;或法文的&#39;fr&#39;。

* **社群網站名稱**:參與

   * 重複檢查名稱，因為在建立網站後不易變更
   * 初始URL將顯示在「社群網站名稱」下方
   * 若為有效的URL，請附加基本語言代碼+ &quot;。html&quot;
   * *例如*,https://localhost:4502/content/sites/ `engage/en.html`

* **範本**:向下拉選擇 `Reference Site`

選擇下 **一步**

### 步驟2:設計 {#step-design}

「設計」步驟會分兩節顯示，供您選取主題和品牌橫幅：

#### COMMUNITY SITE THEME {#community-site-theme}

選擇要套用至範本的樣式。 選取後，主題將覆蓋勾選標籤。

#### COMMUNITY SITE BRANDING {#community-site-branding}

（選用）上傳橫幅影像以顯示在網站頁面上。 橫幅會釘在瀏覽器的左邊，位於社群網站標題和導覽連結之間。 橫幅高度會裁切為120像素。 橫幅的大小不會調整為適合瀏覽器寬度和120像素高度。

![chlimage_1-58](assets/chlimage_1-58.png) ![chlimage_1-59](assets/chlimage_1-59.png)

選擇 **下一步**。

### 步驟3:設定 {#step-settings}

在「設定」步驟中，在選取 `Next`之前，請注意有7個區段可提供使用者管理、標籤、協調、群組管理、分析、翻譯和啟用等組態的存取權。

請造訪 [AEM Communities快速入門啟用教學課程](/help/communities/getting-started-enablement.md) ，以體驗使用啟用功能的經驗。

#### 使用者管理 {#user-management}

勾選「用戶管理」的所 [有複選框](/help/communities/sites-console.md#user-management)

* 允許網站訪客自行註冊
* 允許網站訪客檢視網站，而不需登入
* 允許成員從其他社區成員發送和接收消息
* 允許使用Facebook登入，而不是註冊和建立個人檔案
* 允許使用Twitter登入，而不是註冊和建立設定檔

>[!NOTE]
>
>對於生產環境，必須建立自訂的Facebook和Twitter應用程式。 請參 [閱使用Facebook和Twitter的社交登入](/help/communities/social-login.md)。

![社群網站設定](assets/site-settings.png)

#### TAGGING {#tagging}

可套用至社群內容的標籤是透過選取先前透過「標籤控制台」( [Tagging Console](/help/sites-administering/tags.md#tagging-console) )定義的AEM名稱空間(例如 [Tutorial namespace](/help/communities/setup.md#create-tutorial-tags))來控制。

使用預先輸入搜尋功能，尋找名稱空間十分簡單。 例如，

* 鍵入&#39;tut&#39;
* select `Tutorial`

![chlimage_1-60](assets/chlimage_1-60.png)

#### ROLES {#roles}

[社區成員角色](/help/communities/users.md) ，通過「角色」部分中的設定進行分配。

若要讓社群成員（或成員群組）以社群管理員的身分體驗網站，請使用預先輸入搜尋，並從下拉式清單的選項中選取成員或群組名稱。

例如，

* 類型&quot;q&quot;
* 選擇奎 [恩·哈珀](/help/communities/enablement-setup.md#publishcreateenablementmembers)

>[!NOTE]
>
>[隧道服務](https://helpx.adobe.com/experience-manager/6-3/help/communities/deploy-communities.html#tunnel-service-on-author) ，允許選擇僅存在於發佈環境中的成員和組。

![新站點中的用戶角色](assets/site-admin-1.png)

#### MODERATION {#moderation}

接受預設的全域設 [定](/help/communities/sites-console.md#moderation) ，以協調使用者產生的內容(UGC)。

![chlimage_1-61](assets/chlimage_1-61.png)

#### ANALYTICS {#analytics}

如果Adobe Analytics已取得授權，且已設定Analytics雲端服務和架構，則可啟用Analytics並選取架構。

請參閱 [社群功能的Analytics設定](/help/communities/analytics.md)。

![chlimage_1-62](assets/chlimage_1-62.png)

#### TRANSLATION {#translation}

「轉 [譯」設定](/help/communities/sites-console.md#translation) ，可指定網站的基本語言，以及UGC是否可轉譯，以及是否可轉譯為哪種語言。

* 檢查允 **許機器翻譯**
* 保留預設的「機器翻譯」服務為翻譯選擇的預設語言
* 保留預設翻譯提供器和配置
* 不需要全球商店，因為沒有語言復本
* 選擇 **翻譯整個頁面**
* 保留預設持久性選項

![chlimage_1-63](assets/chlimage_1-63.png)

#### ENABLEMENT {#enablement}

建立參與社群時留空。

如需快速建立啟用社群的類似教 [學課程](/help/communities/overview.md#enablement-community)，請 [參閱「啟用AEM社群快速入門」](/help/communities/getting-started-enablement.md)。

選擇 **下一步**。

### 步驟4:建立社群網站 {#step-create-communities-site}

選擇 **建立。**

![chlimage_1-64](assets/chlimage_1-64.png)

當流程完成時，新站點的資料夾將顯示在「社區——站點」控制台中。

![通信Sitesconsole](assets/communitiessitesconsole.png)

## 發佈社群網站 {#publish-the-community-site}

建立的站點應從Communities - Sites控制台進行管理，該控制台與建立新站點的控制台相同。

在選取社群網站的檔案夾以開啟檔案夾後，將滑鼠指標暫留在網站圖示上，以便顯示4個動作圖示：

![siteactionicons-1](assets/siteactionicons-1.png)

在選取第四個省略號圖示（更多操作）時，會顯示「匯出網站」和「刪除網站」選項。

![siteactionsnew-1](assets/siteactionsnew-1.png)

從左到右依次為：

* **「開啟網**&#x200B;站」選取鉛筆圖示，以作者編輯模式開啟社群網站，以新增及／或設定頁面元件

* **「編輯網**&#x200B;站」選擇屬性圖示，以開啟社群網站以修改屬性，例如標題或變更主題

* **「發佈網**&#x200B;站」選取全球圖示以發佈社群網站（例如，如果您的發佈伺服器正在本機電腦上執行，則預設為localhost:4503）

* **「匯出網**&#x200B;站」選取匯出圖示，以建立儲存在封裝管理員中及已下載之社群網站 [的封裝](/help/sites-administering/package-manager.md) 。
請注意，網站套件中不包含UGC。

* **刪除站點**選擇刪除表徵圖，從「社區」>「站點」控制台中刪除社區站點。 此動作會移除與網站相關的所有項目，例如UGC、使用者群組、資產和資料庫記錄。

![siteactions](assets/siteactions.png)

>[!NOTE]
>
>如果未對發佈實例使用預設埠4503，請編輯預設複製代理，將埠號設定為正確值。
>
>在作者實例上，從主菜單：
>
>1. 導航至「工具」>「操作」>「複製」菜單。
1. 選擇「作者上的代理」。
1. 選擇「預設代理（發佈）」。
1. 在「設定」旁選擇「編輯」。
1. 在「代理設定」的彈出對話框中，選擇「傳輸」頁籤。
1. 在URI中，將埠號4503更改為所需的埠號>
   * 例如，要使用埠6103:https://localhost:6103/bin/receive?sling:authRequestLogin=1
1. 選擇「確定」。
1. （可選）選擇「清除」或「強制重試」以重置複製隊列。




### 選擇發佈 {#select-publish}

在確保發佈伺服器正在執行後，選取要發佈社群網站的世界圖示。

![chlimage_1-65](assets/chlimage_1-65.png)

成功發佈社群網站後，會短暫出現訊息：

![chlimage_1-66](assets/chlimage_1-66.png)

### 新社群使用者群組 {#new-community-user-groups}

除了新社群網站外，還會建立新的使用者群組，其中已針對各種管理功能設定適當的權限。 如需詳細資訊，請 [造訪社群網站的使用者群組](/help/communities/users.md#usergroupsforcommunitysites)。

對於這個新社群網站，若在步驟1中指定網站名稱「參與」，則可從「群組」主控台(全域導覽 [](/help/communities/members.md) :社群、群組):

* 社群互動社群經理
* 社群參與群組管理員
* 社群參與會員
* 社群參與協調者
* 社群參與特權會員
* 社群參與網站內容管理員

請注意， [Aaron mcDonald](/help/communities/tutorials.md#demo-users) 是

* 社群互動社群經理
* 社群參與協調者
* 社群參與會員（間接地以協調者群組成員的身分）

![chlimage_1-67](assets/chlimage_1-67.png)

#### https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![chlimage_1-68](assets/chlimage_1-68.png)

## 配置驗證錯誤 {#configure-for-authentication-error}

在設定網站並推送至發佈後，在 [發佈例項上設定登入對應](/help/communities/sites-console.md#configure-for-authentication-error) ( `Adobe Granite Login Selector Authentication Handler`)。 優點是，當未正確輸入登入憑證時，驗證錯誤會重新顯示社群網站的登入頁面，並顯示錯誤訊息。

新增為 `Login Page Mapping`

* /content/sites/engage/tw/signin:/content/sites/engage/tw

## 可選步驟 {#optional-steps}

### 變更預設首頁 {#change-the-default-home-page}

使用發佈網站進行展示時，將預設首頁變更為新網站可能會很有用。

若要這麼做，必須使 [用CRXDE](https://localhost:4503/crx/de) Lite來編輯 [發佈上的資源對應表](/help/sites-deploying/resource-mapping.md) 。

若要開始：

1. 在發佈例項上，以管理員權限登入。
1. 瀏覽至 [https://localhost:4503/crx/de](https://localhost:4503/crx/de)。
1. 在專案瀏覽器中，展開 `/etc/map.`
1. 選擇節 `http` 點：

   * 選擇 **建立節點：**

      * **名稱** localhost.4503(不 *要* 使用&#39;:&#39;)

      * **Type** [sling:Mapping](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. 選中新建立 `localhost.4503` 的節點時：

   * 新增屬性：

      * **Name** sling:match
      * **類型字串**
      * **值** localhost.4503/$（必須以&#39;$&#39;字元結尾）
   * 新增屬性：

      * **Name** sling:internalRedirect
      * **類型字串**
      * **值** /content/sites/engage/en.html


1. 選擇「 **全部保存」。**
1. （可選）刪除瀏覽歷史記錄。
1. 瀏覽至https://localhost:4503/。

   * https://localhost:4503/content/sites/engage/en.html

>[!NOTE]
若要停用，只需在屬 `sling:match` 性值前加上&#39;x&#39; - `xlocalhost.4503/$` —— 和 **全部儲存**。

![chlimage_1-69](assets/chlimage_1-69.png)

#### 疑難排解：保存映射時出錯 {#troubleshooting-error-saving-map}

如果無法保存更改，請確保節點名稱為 `localhost.4503`，使用「dot」分隔符，而不使用「冒號」 `localhost:4503` 分隔符，因為 `localhost`它不是有效的命名空間前置詞。

![chlimage_1-70](assets/chlimage_1-70.png)

#### 疑難排解：無法重新導向 {#troubleshooting-fail-to-redirect}

規則運算式字&#x200B;**串結尾的&#39;**`sling:match``https://localhost:4503/` $&#39;至關重要，因此只會正確映射，否則重新導向值會前置詞至URL中server:port之後可能存在的任何路徑。 因此，當AEM嘗試重新導向至登入頁面時，它會失敗。

### 修改網站 {#modify-the-site}

在初次建立網站後，作者可以使用「開啟網站」 [圖示](/help/communities/sites-console.md#authoring-site-content) ，執行標準的AEM製作活動。

此外，管理員可使用「編 [輯網站」圖示](/help/communities/sites-console.md#modifying-site-properties) ，修改網站的屬性，例如標題。

在進行任何修改後，請記 **得儲存** ，然後重&#x200B;**新發佈網站** 。

>[!NOTE]
如果不熟悉AEM，請檢視基本處理 [相關檔案](/help/sites-authoring/basic-handling.md) ，以 [及製作頁面的快速指南](/help/sites-authoring/qg-page-authoring.md)。

