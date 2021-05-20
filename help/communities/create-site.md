---
title: 製作新的社群網站
seo-title: 製作新的社群網站
description: 如何製作新的AEM Communities網站
seo-description: 如何製作新的AEM Communities網站
uuid: 4f609f5f-ef07-44fc-aeb3-1c616e120d46
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8ae324ea-8b84-47a3-aabf-1fee2a3bd46d
docset: aem65
exl-id: d4c1895f-421c-4146-b94a-8d11065ef9e3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 1%

---

# 製作新的社群網站{#author-a-new-community-site}

## 建立社區站點{#create-a-community-site}

使用製作例項來建立社群網站。 在AEM Author例項上：

1. 以管理員權限登入。
1. 從全局導航，轉至&#x200B;**[!UICONTROL Communities]** > **[!UICONTROL Sites]**。

Communities Sites控制台提供嚮導，引導用戶完成建立社區站點的步驟。 在最終步驟中提交站點之前，可以前進到`Next`步驟或`Back`到上一步。

要開始建立新的社區站點，請執行以下操作：

* 選擇`Create`按鈕。

![createcommunitysite](assets/createcommunitysite.png)

### 步驟1:站點模板{#step-site-template}

![建立網站的範本](assets/create-site.png)

在[網站範本步驟](/help/communities/sites-console.md#step2013asitetemplate)中，輸入標題、說明、URL名稱，並選取社群網站範本，例如：

* **社群網站標題**: `Getting Started Tutorial`
* **社群網站說明**: `A site for engaging with the community.`
* **社區站點根**:(預設根保留空白 `/content/sites`)
* **雲端設定**:（若未指定雲端設定，則保留空白）提供指定雲端設定的路徑。
* **社區站點基語言**:(單一語言不受影響：英文)使用下拉式清單，從可 *用* 的語言中選擇一或多種基本語言 — 德文、義大利文、法文、日文、西班牙文、葡萄牙文（巴西）、中文（繁體）和中文（簡體）。系統會針對每個新增的語言建立一個社群網站，並依照[多語言網站轉譯內容](/help/sites-administering/translation.md)中所述的最佳作法，存在於相同的網站資料夾中。 每個網站的根頁面都會包含一個子頁面，其名稱是所選語言之一的語言代碼，例如英文為「en」，法文為「fr」。

* **社群網站名稱**:參與

   * 仔細檢查名稱，因為建立網站後不易變更
   * 初始URL將顯示在「社群網站名稱」下方
   * 為了有效的URL，請附加基本語言代碼+ &quot;。html&quot;
   * *例如*, https://localhost:4502/content/sites/  `engage/en.html`

* **範本**:下拉式選擇  `Reference Site`

* 選擇&#x200B;**Next**。

### 步驟2:設計{#step-design}

「設計」步驟會分兩節顯示，用於選取主題和品牌橫幅：

#### 社區站點主題{#community-site-theme}

選取要套用至範本的所需樣式。 選取後，主題將用複選標籤覆蓋。

#### 社區站點品牌{#community-site-branding}

（選用）上傳橫幅影像以在網站頁面間顯示。 橫幅會釘在瀏覽器的左側邊緣、社群網站標題和導覽連結之間。 橫幅高度會裁切為120像素。 橫幅沒有調整大小以符合瀏覽器寬度和120像素高度。

![社群網站品牌化](assets/community-site-branding.png)

![上傳 — 影像 — 網站](assets/upload-image-site.png)

選擇&#x200B;**Next**。

### 步驟3:設定{#step-settings}

在「設定」步驟中，在選取`Next`之前，請注意，有七個區段提供對設定的存取，包括使用者管理、標籤、協調、群組管理、分析、翻譯和啟用。

請參閱[啟用AEM Communities快速入門](/help/communities/getting-started-enablement.md)教學課程，體驗如何使用啟用功能。

#### 使用者管理 {#user-management}

選中[用戶管理](/help/communities/sites-console.md#user-management)的所有複選框

* 允許網站訪客自行註冊
* 允許網站訪客檢視網站而不登入
* 允許成員發送和接收來自其他社區成員的消息
* 允許使用Facebook登入，而非註冊和建立設定檔
* 允許使用Twitter登入，而非註冊和建立設定檔

>[!NOTE]
>
>針對生產環境，需建立自訂Facebook和Twitter應用程式。 請參閱[使用Facebook和Twitter進行社交登入](/help/communities/social-login.md)。

![社群網站設定](assets/site-settings.png)

#### 標籤 {#tagging}

可套用至社群內容的標籤，是透過選取先前透過[標籤控制台](/help/sites-administering/tags.md#tagging-console)（例如[教學課程命名空間](/help/communities/setup.md#create-tutorial-tags)）定義的AEM命名空間來控制。

使用預先輸入搜尋可輕鬆找到命名空間。 例如，

* 類型 `tut`
* 選取 `Tutorial`

![標籤](assets/tagging.png)

#### 角色 {#roles}

[社群成](/help/communities/users.md) 員角色是透過「角色」區段中的設定來指派。

若要讓社區成員（或成員組）以社區管理員的身份體驗站點，請使用「預先鍵入」搜索並從下拉清單中的選項中選擇成員或組名稱。

例如，

* 類型 `q`
* 選擇[Quinn Harper](/help/communities/enablement-setup.md#publishcreateenablementmembers)

>[!NOTE]
>
>[通道](https://helpx.adobe.com/experience-manager/6-3/help/communities/deploy-communities.html#tunnel-service-on-author) 服務允許選擇僅存在於發佈環境中的成員和組。

![新網站中的使用者角色](assets/site-admin-1.png)

#### 協調 {#moderation}

接受[調節](/help/communities/sites-console.md#moderation)用戶生成內容(UGC)的預設全局設定。

![審核](assets/moderation1.png)

#### ANALYTICS {#analytics}

如果Adobe Analytics已授權，且已設定Analytics雲端服務和架構，則可啟用Analytics並選取架構。

請參閱[Analytics For Communities](/help/communities/analytics.md)。

![分析](assets/analytics.png)

#### 翻譯 {#translation}

[翻譯設定](/help/communities/sites-console.md#translation)指定網站的基本語言，以及UGC是否可被翻譯以及如果是，可以翻譯成哪種語言。

* 檢查&#x200B;**允許機器翻譯**
* 預設機器翻譯服務將預設語言保留為要翻譯的語言
* 保留預設翻譯提供者並設定
* 不需要全球商店，因為沒有語言副本
* 選擇&#x200B;**翻譯整個頁**
* 保留預設持久性選項

![翻譯設定](assets/translation-settings.png)

#### 啟用 {#enablement}

建立參與社群時，請保留空白。

如需快速建立[啟用社群](/help/communities/overview.md#enablement-community)的類似教學課程，請參閱[啟用AEM Communities快速入門](/help/communities/getting-started-enablement.md)。

選擇&#x200B;**Next**。

![啟用](assets/enablement.png)

### 步驟4:建立社區站點{#step-create-communities-site}

選擇&#x200B;**建立。**

![建立網站](assets/create-site2.png)

過程完成後，新站點的資料夾將顯示在Communities - Sites控制台中。

![通信sitesconsole](assets/communitiessitesconsole.png)

## 發佈社群網站{#publish-the-community-site}

應從Communities - Sites控制台管理建立的站點，該控制台與可建立新站點的控制台相同。

選取社群網站的資料夾以開啟後，將滑鼠指標暫留在網站圖示上，以便顯示四個動作圖示：

![Siteactionicons-1](assets/siteactionicons-1.png)

選取第四個點圖示（更多動作）時，會顯示「匯出網站」和「刪除網站」選項。

![Siteactionsnew-1](assets/siteactionsnew-1.png)

從左到右為：

* **開啟網站**

   選取鉛筆圖示，以在作者編輯模式中開啟社群網站，以新增和/或設定頁面元件

* **編輯網站**

   選取屬性圖示以開啟社群網站以修改屬性，例如標題或變更主題

* **發佈網站**

   選取發佈社群網站的世界圖示（例如，如果您的發佈伺服器在本機電腦上執行，則預設會發佈至localhost:4503）

* **匯出網站**

   選擇導出表徵圖可建立同時儲存在[包管理器](/help/sites-administering/package-manager.md)中和下載的社區站點的包。
請注意，網站套件中未包含UGC。

* **刪除網站**

   選擇刪除表徵圖以從&#x200B;**[!UICONTROL Communities > Sites控制台]**&#x200B;中刪除社區站點。 此動作會移除與網站相關聯的所有項目，例如UGC、使用者群組、資產和資料庫記錄。

![網站動作](assets/siteactions.png)

>[!NOTE]
>
>如果未使用發佈實例的預設埠4503，請編輯預設複製代理以將埠號設定為正確的值。
>
>在製作例項上，從主功能表：
>
>1. 導覽至「**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 復寫]**」功能表。
>1. 選擇&#x200B;**[!UICONTROL Agent on author]**。
>1. 選擇&#x200B;**[!UICONTROL 預設代理（發佈）]**。
>1. 在&#x200B;**[!UICONTROL Settings]**&#x200B;旁，選擇&#x200B;**[!UICONTROL Edit]**。
>1. 在「代理設定」的彈出式對話框中，選擇&#x200B;**[!UICONTROL Transport]**&#x200B;頁簽。
>1. 在URI中，將埠號4503更改為所需的埠號。 例如，要使用埠6103:https://localhost:6103/bin/receive?sling:authRequestLogin=1
>1. 選擇&#x200B;**[!UICONTROL OK]**。
>1. （可選）選擇&#x200B;**[!UICONTROL Clear]**&#x200B;或&#x200B;**[!UICONTROL 強制重試]**&#x200B;以重置複製隊列。


### 選擇發佈{#select-publish}

確保發佈伺服器正在運行後，選擇「世界」表徵圖以發佈社區站點。

![發佈網站](assets/publish-site.png)

成功發佈社群網站後，會短暫顯示「已發佈網站」訊息。

### 新社區用戶組{#new-community-user-groups}

除了新的社群網站外，還會建立新的使用者群組，這些使用者群組具有針對各種管理功能所設定的適當權限。 如需詳細資訊，請造訪[社群網站的使用者群組](/help/communities/users.md#usergroupsforcommunitysites)。

對於這個新的社群網站，如果在步驟1中指定網站名稱「engage」，則可從[群組控制台](/help/communities/members.md)(全域導覽：社區、組):

* 社群參與社群經理
* 社群參與群組管理員
* 社群參與成員
* 社群參與協調者
* 社群互動特權成員
* 社群參與網站內容管理員

請注意，[Aaron McDonald](/help/communities/tutorials.md#demo-users)是

* 社群參與社群經理
* 社群參與協調者
* 社群參與成員（間接作為協調者群組的成員）

![使用者群組](assets/user-group.png)

#### https://localhost:4503/content/sites/engage/en.html {#http-localhost-content-sites-engage-en-html}

![參與](assets/engage.png)

## 配置身份驗證錯誤{#configure-for-authentication-error}

將網站設定並推送至發佈後，請在發佈執行個體上設定登入對應](/help/communities/sites-console.md#configure-for-authentication-error)(`Adobe Granite Login Selector Authentication Handler`)。 [好處是當未正確輸入登入憑證時，驗證錯誤將會以錯誤訊息重新顯示社群網站的登入頁面。

將`Login Page Mapping`新增為

* `/content/sites/engage/en/signin:/content/sites/engage/en`

## 可選步驟{#optional-steps}

### 更改預設首頁{#change-the-default-home-page}

使用發佈網站以進行示範時，將預設首頁變更為新網站可能會很實用。

要執行此操作，需要使用[CRXDE](https://localhost:4503/crx/de) Lite來編輯發佈時的[resource-mapping](/help/sites-deploying/resource-mapping.md)表。

若要開始：

1. 在發佈執行個體上，使用管理員權限登入。
1. 瀏覽至[https://localhost:4503/crx/de](https://localhost:4503/crx/de)。
1. 在專案瀏覽器中，展開`/etc/map.`
1. 選擇`http`節點：

   * 選擇&#x200B;**建立節點：**

      * **** Namelocalhost.4503(不 ** 要使用「：」)

      * **** [類型：映射](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)

1. 已選擇新建立的`localhost.4503`節點：

   * 添加屬性：

   * **** 命名：match
      * **** TypeString
      * **** Valuelocalhost.4503/$（必須以「$」字元結尾）
   * 添加屬性：

      * **** 命名：internalRedirect
      * **** TypeString
      * **值** /content/sites/engage/en.html


1. 選擇&#x200B;**全部保存。**
1. （選用）刪除瀏覽歷史記錄。
1. 瀏覽至https://localhost:4503/。

   * 到達https://localhost:4503/content/sites/engage/en.html

>[!NOTE]
>
>若要停用，只需為`sling:match`屬性值加上前置詞&#39;x&#39; - `xlocalhost.4503/$` — 和&#x200B;**Save All**&#x200B;即可。

![可選步驟](assets/optional-steps.png)

#### 疑難排解：保存映射{#troubleshooting-error-saving-map}時出錯

如果無法保存更改，請確保節點名稱為`localhost.4503`（帶有「點」分隔符），而不是帶有「冒號」分隔符的`localhost:4503`，因為`localhost`不是有效的命名空間前置詞。

![錯誤訊息](assets/error-message.png)

#### 疑難排解：無法重定向{#troubleshooting-fail-to-redirect}

規則運算式`sling:match`字串結尾的「**$**」很重要，因此只有`https://localhost:4503/`已完全對應，否則重新導向值會前置詞至URL中server:port之後可能存在的任何路徑。 因此，當AEM嘗試重新導向至登入頁面時，會失敗。

### 修改站點{#modify-the-site}

網站初次建立後，作者可使用[開啟網站圖示](/help/communities/sites-console.md#authoring-site-content)執行標準AEM製作活動。

此外，管理員可以使用[編輯站點表徵圖](/help/communities/sites-console.md#modifying-site-properties)來修改站點的屬性，如標題。

進行任何修改後，請記得&#x200B;**Save**&#x200B;並重新&#x200B;**Publish**&#x200B;網站。

>[!NOTE]
>
>若不熟悉AEM，請檢視[basic handling](/help/sites-authoring/basic-handling.md)和[製作頁面快速指南](/help/sites-authoring/qg-page-authoring.md)的相關檔案。
