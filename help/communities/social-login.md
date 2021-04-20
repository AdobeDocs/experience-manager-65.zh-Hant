---
title: 使用Facebook和Twitter進行社交登入
seo-title: 使用Facebook和Twitter進行社交登入
description: 社交登入可讓網站訪客使用其Facebook或Twitter帳戶登入。
seo-description: 社交登入可讓網站訪客使用其Facebook或Twitter帳戶登入。
uuid: f70e346e-0d8c-41a0-a100-206a420088dc
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c0a71870-8f95-40c8-9ffd-b7af49723288
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2804'
ht-degree: 1%

---


# 使用Facebook和Twitter {#social-login-with-facebook-and-twitter}進行社交登入

社交登入是一種功能，可讓網站訪客選擇使用其Facebook或Twitter帳戶登入。 因此，在其會員個人檔案中加入允許的FacebookAEM或Twitter資料。

![socialloginweretail](assets/socialloginweretail.png)

## 社交登入概述{#social-login-overview}

若要包含社交登入，建立自訂Facebook和Twitter應用程式時需&#x200B;**。

雖然我們零售的範例提供範例Facebook和Twitter應用程式與雲端服務，但無法在生產網站[](../../help/sites-administering/production-ready.md)上使用。

所需步驟包括：

1. [對所有發](#adobe-granite-oauth-authentication-handler) 布例項啟AEM用OAuth驗證。

   未啟用OAuth時，嘗試登入失敗。

1. **建立** 社交應用程式和雲端服務。

   * 若要支援使用Facebook登入：

      * 建立[Facebook應用程式](#create-a-facebook-app)。
      * 建立並發佈[Facebook Connect雲端服務](#create-a-facebook-connect-cloud-service)。
   * 若要支援使用Twitter登入：

      * 建立[Twitter應用程式](#create-a-twitter-app)。
      * 建立並發佈[Twitter Connect雲端服務](#create-a-twitter-connect-cloud-service)。


1. [**啟** 用社](#enable-social-login) 群網站的社交登入。

有兩個基本概念：

1. **Scope** （權限）會指定應用程式可請求的資料。

   * 依預設，Facebook和Twitter [AdobeGranite OAuth應用程式和Provider](#adobe-granite-oauth-application-and-provider)例項會在其範圍內包含基本應用程式權限。

1. **Fields** (params)指定使用URL參數請求的實際資料。

   * 這些欄位在[AEM CommunitiesFacebook OAuth提供者](#aem-communities-facebook-oauth-provider)和[AEM CommunitiesTwitter OAuth提供者](#aem-communities-twitter-oauth-provider)中指定。
   * 預設欄位適用於大多數使用案例，但可加以修改。

## Facebook登入{#facebook-login}

### Facebook API版本{#facebook-api-version}

社交登入和we-retail Facebook範例是在Facebook Graph API 1.0版時開發的。
自6.AEM4 GA和6.3 SP1的社交登入已更新，可搭配較新的Facebook Graph API 2.5版本使用。

>[!NOTE]
>
>對於舊AEM版，如果您在記錄&#x200B;**中遇到例外情況無法從此**&#x200B;擷取Token，請升級至該版本的最新CFPAEM。

如需Facebook圖形API版本資訊，請參閱[Facebook API changelog](https://developers.facebook.com/docs/apps/changelog)。

### 建立Facebook應用程式{#create-a-facebook-app}

必須有正確設定的Facebook應用程式，才能啟用Facebook社交登入。

若要建立Facebook應用程式，請依照Facebook在[https://developers.facebook.com/apps/](https://developers.facebook.com/apps/)的指示進行。 下列資訊不會反映對其指示的變更。

一般而言，自Facebook API v2.7起：

* *新增Facebook應用程式*
   * 對於&#x200B;*Platform*，選擇「Website:
      * 對於&#x200B;*網站URL*，請輸入`  https://<server>:<port>.`
      * 對於&#x200B;*顯示名稱*，輸入標題以用作Facebook連線服務的標題。
      * 對於&#x200B;*Category*，建議選擇&#x200B;*頁面應用程式*，但可以是任何內容。
      * *新增產品：Facebook登入*
      * 對於&#x200B;*有效的OAuth重定向URI*，請輸入`  https://<server>:<port>.`

>[!NOTE]
>
>若要開發，http://localhost:4503將有效。

建立應用程式後，請找出&#x200B;**[!UICONTROL App ID]**&#x200B;和&#x200B;**[!UICONTROL App Secret]**&#x200B;設定。 此資訊是設定[Facebook雲端服務](#createafacebookcloudservice)時的必要資訊。

### 建立Facebook ConnectCloud Service{#create-a-facebook-connect-cloud-service}

[AdobeGranite OAuth應用程式和Provider](#adobe-granite-oauth-application-and-provider)例項會透過建立雲端服務設定實例化，以識別新增使用者的Facebook應用程式和成員群組。

1. 在作AEM者例項上，以管理員權限登入。
1. 在全域導覽中，選取「工具&#x200B;**** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Facebook Social登入設定]**」。
1. 選擇配置&#x200B;**[!UICONTROL 上下文路徑]**。

   **[!UICONTROL 上]** 下文路徑應與您在建立／編輯社群網站時選取的雲端設定路徑相同。

1. 檢查您的上下文路徑是否已啟用，以在其下方建立雲端服務。
1. 前往「**[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 配置瀏覽器]**」。 選取您的上下文並編輯屬性。 如果尚未啟用，請啟用雲端設定。

   ![config-propertiespng](assets/config-propertiespng.png)

   * 如需詳細資訊，請參閱[Configuration Browser](/help/sites-administering/configurations.md)檔案。

1. **建立／編** 輯Facebook雲端服務設定。

   ![fbsocialloginconfigpng](assets/fbsocialloginconfigpng.png)

   * **[!UICONTROL Title]** (*必要*)輸入識別Facebook應用程式的顯示標題。建議您為Facebook應用程式使用與&#x200B;*顯示名稱*&#x200B;輸入的相同名稱。
   * **[!UICONTROL 應用程式ID/API金鑰]** (必&#x200B;*要*)輸入 ***Facebook應*** 用程式的應用程式ID。這會識別從對話方塊建立的[AdobeGranite OAuth應用程式和Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider)例項。
   * **[!UICONTROL App Secret]** (必&#x200B;*要*)輸入 ***Facebook應*** 用程式的App Secret。
   * **[!UICONTROL 建]** 立使用者若勾選，使用Facebook帳戶登入將會建立AEM使用者項目，並將其新增為所選使用者群組的成員。已勾選預設值（強烈建議）。
   * **[!UICONTROL 遮色片使用者ID]**:保持未選定狀態。
   * **[!UICONTROL 範圍電子郵件]**:應從Facebook擷取使用者的電子郵件ID。
   * **[!UICONTROL 添加到用]** 戶組選擇添加用戶組，以為將添加 [用](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) 戶的社區站點選擇一個或多個成員組。

   >[!NOTE]
   >
   >您可隨時新增或移除群組。 但現有使用者的會籍不會受到影響。 自動會籍僅適用於在此欄位更新後建立的新使用者。 對於匿名用戶被禁用的站點，選擇將用戶添加到為該封閉社區站點指定的相應社區成員組。

   * 選擇&#x200B;**[!UICONTROL SAVE]**。
   * **[!UICONTROL 發佈]**.



結果是[AdobeGranite OAuth應用程式和Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider)執行個體，除非新增其他範圍（權限），否則不需要進一步修改。 預設範圍是Facebook登入的標準權限。 如果需要其他範圍，則需要直接編輯OSGI配置。 如果有修改是透過系統／主控台直接完成，請避免從觸控式使用者介面編輯您的雲端服務設定，以避免覆寫。

### AEM CommunitiesFacebook OAuth提供者{#aem-communities-facebook-oauth-provider}

AEM Communities提供者會擴充[AdobeGranite OAuth應用程式和提供者](#adobe-granite-oauth-application-and-provider)例項。

此提供者需要編輯才能：

* 允許使用者更新
* 在範圍](#adobe-granite-oauth-application-and-provider)內添加其他欄位[

   * 並非預設允許的所有欄位都包含在內。

如果需要編輯，請在每個發佈例AEM項上：

1. 以管理員權限登入。
1. 導航至[Web控制台](../../help/sites-deploying/configuring-osgi.md)。 例如，http://localhost:4503/system/console/configMgr。
1. 找到AEM CommunitiesFacebook OAuth提供者。
1. 選取要開啟以進行編輯的鉛筆圖示。

   ![fboauthprov_png](assets/fboauthprov_png.png)

   * **[!UICONTROL OAuth提供者ID]**

      (*Required*)預設值為&#x200B;*soco -facebook*。 不要編輯。

   * **[!UICONTROL Cloud Service設定]**

      預設值為 `/etc/  cloudservices /  facebookconnect`. 不要編輯。

   * **[!UICONTROL OAuth提供者服務設定]**

      預設值為 `/apps/social/facebookprovider/config/`. 不要編輯。

   * **[!UICONTROL 啟用標籤]**

      不要編輯。

   * **[!UICONTROL 使用者路徑]**

      儲存用戶資料的儲存庫中的位置。 對於社群網站，為確保成員有權查看彼此的配置檔案，路徑應為預設的&#x200B;*/home/users/community*。

   * **[!UICONTROL 啟用欄位]**

      勾選後，列出的欄位會在向Facebook要求使用者驗證和資訊時指定。 預設值為取消選中。

   * **[!UICONTROL 欄位]**

      啟用「欄位」後，呼叫Facebook圖形API時會包含下列欄位。 這些欄位必須允許在雲端服務設定中定義的範圍內。 其他欄位可能需要Facebook核准。 參考Facebook檔案的「Facebook登入權限」區段。 新增為參數的預設欄位為：

      * id
      * 名稱
      * first_name
      * last_name
      * link
      * 地區設定
      * 圖片
      * 時區
      * updated_time
      * 已驗證
      * 電子郵件

   如果添加或更改了任何欄位，請更新相應的預設同步處理程式配置以更正映射。

   * **[!UICONTROL 更新使用者]**

      如果選中此選項，則每次登錄時都會刷新儲存庫中的用戶資料，以反映配置檔案更改或請求的其他資料。 已取消選取預設值。


#### 後續步驟{#next-steps}

Facebook和Twitter的後續步驟相同：

* [發佈雲端服務設定](#publishcloudservices)
* [為社群網站啟用](#enable-social-login)

## Twitter登入{#twitter-login}

### 建立Twitter應用程式{#create-a-twitter-app}

必須有已設定的Twitter應用程式才能啟用Twitter社交登入。

請依照最新指示，在[https://apps.twitter.com](https://apps.twitter.com/)建立新的Twitter應用程式。

一般而言：

1. 輸入&#x200B;*名稱*，以識別您網站使用者的Twitter應用程式。
1. 輸入&#x200B;*說明*。
1. 對於&#x200B;*website* —— 輸入`https://<server>`。
1. 對於&#x200B;*回呼URL* —— 輸入`https://server`。

   >[!NOTE]
   >
   >無需指定埠。
   >
   >若要開發，https://127.0.0.1/將有效。

1. 建立應用程式後，請找出&#x200B;**[!UICONTROL 消費者(API)金鑰]**&#x200B;和&#x200B;**[!UICONTROL 消費者(API)密碼]**。 設定[Twitter雲端服務](#createatwittercloudservice)時，將需要此資訊。

#### 權限 {#permissions}

在Twitter應用程式管理的權限區段中：

* **[!UICONTROL 存取]**:選擇 `Read only`。

   * 不支援其他選項

* **[!UICONTROL 其他權限]**:（可選）選 `Request email addresses from users`擇。

   * 如果未選取此選項，中的使用者設定AEM檔將不包含其電子郵件地址。
   * Twitter的指示說明需要採取的其他步驟。

僅對&#x200B;*[GET帳戶/verify credentials](https://dev.twitter.com/rest/reference/get/account/verify_credentials)*&#x200B;提出REST登入要求。

### 建立Twitter連線Cloud Service{#create-a-twitter-connect-cloud-service}

[AdobeGranite OAuth應用程式和Provider](#adobe-granite-oauth-application-and-provider)例項會透過建立雲端服務設定來執行個體化，以識別新增使用者的Twitter應用程式和成員群組。

1. 在作者例項上，以管理員權限登入。
1. 在全域導覽中，選擇&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Twitter Social登入設定]**。
1. 選擇&#x200B;**[!UICONTROL 上下文路徑]**&#x200B;配置。

   上下文路徑應與您在建立／編輯社群網站時選取的雲端設定路徑相同。

1. 檢查您的上下文路徑是否已啟用，以在其下方建立雲端服務。
1. 前往「**[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 配置瀏覽器]**」。 選取您的上下文並編輯屬性。 如果尚未啟用，請啟用雲端設定。

   ![twitterconfigpropping](assets/twitterconfigproppng.png)

   * 如需詳細資訊，請參閱[Configuration Browser](/help/sites-administering/configurations.md)檔案。

1. 建立／編輯Twitter雲端服務設定。

   ![twittersocialloginpng](assets/twittersocialloginpng.png)

   * **[!UICONTROL 標題]**

      （*必要*）輸入識別Twitter應用程式的顯示標題。 建議您為Twitter應用程式使用與&#x200B;*顯示名稱*&#x200B;所輸入的相同名稱。

   * **[!UICONTROL 消費者金鑰]**

      （*必要*）輸入Twitter應用程式的&#x200B;**消費者(API)金鑰**。 這會識別從對話方塊建立的[AdobeGranite OAuth應用程式和Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider)例項。

   * **[!UICONTROL 消費者機密]**

      （*必要*）輸入Twitter應用程式的&#x200B;***消費者(API)密碼***。

   * **[!UICONTROL 建立使用者]**

      如果勾選，使用Twitter帳戶登入將會建立AEM使用者項目，並將其新增為所選使用者群組的成員。 已勾選預設值（強烈建議）。

   * **[!UICONTROL 隱藏使用者 ID]**

      保持未選定狀態。

   * **[!UICONTROL 新增到使用者群組]**

      選擇「添加用戶組」，為將添加用戶的社區站點選擇一個或多個[成員組](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html)。
   >[!NOTE]
   >
   >您可隨時新增或移除群組。 但現有使用者的會籍不會受到影響。 自動會籍僅適用於在此欄位更新後建立的新使用者。 對於匿名使用者被停用的網站，請將使用者新增至該封閉社群網站的對應社群成員群組。

1. 選擇&#x200B;**[!UICONTROL SAVE]**&#x200B;和&#x200B;**[!UICONTROL Publish]**。

結果是不需要進一步修改的[AdobeGranite OAuth應用程式和Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider)例項。 預設範圍是Twitter登入的標準權限。

### AEM CommunitiesTwitter OAuth提供者{#aem-communities-twitter-oauth-provider}

AEM Communities配置擴展了[AdobeGranite OAuth應用程式和Provider](#adobe-granite-oauth-application-and-provider)實例。 此提供者需要編輯才能允許使用者更新。

如果需要編輯，請在每個發佈例AEM項上：

1. 以管理員權限登入。
1. 導航至[Web控制台](../../help/sites-deploying/configuring-osgi.md)。

   例如，http://localhost:4503/system/console/configMgr。

1. 尋找AEM CommunitiesTwitter OAuth提供者。
1. 選取要開啟以進行編輯的鉛筆圖示。

   ![twitteroauth_png](assets/twitteroauth_png.png)

   * **[!UICONTROL OAuth提供者ID]**

   （*必要*）預設值為&#x200B;*soco -twitter*。 不要編輯。

   * **[!UICONTROL Cloud Service設定]**

      預設值為&#x200B;*conf。* 不要編輯。

   * **[!UICONTROL OAuth提供者服務設定]**

      預設值為 `/apps/social/twitterprovider/config/`. 不要編輯。

   * **[!UICONTROL 使用者路徑]**

      儲存用戶資料的儲存庫中的位置。 對於社群站點，為確保成員有權查看彼此的配置檔案，路徑應為預設`/home/users/community`。

   * **[!UICONTROL 啟用]** 參數不編輯
   * **[!UICONTROL URL參]** 數不編輯
   * **[!UICONTROL 更新使用者]**

      如果選中此選項，則每次登錄時都會刷新儲存庫中的用戶資料，以反映配置檔案更改或請求的其他資料。 預設值為取消選中。


#### 後續步驟{#next-steps-1}

Facebook和Twitter的後續步驟相同：

* [發佈雲端服務設定](#publishcloudservices)
* [為社群網站啟用](#enable-social-login)

## 啟用社交登入{#enable-social-login}

### AEM Communities站台控制台{#aem-communities-sites-console}

一旦配置了雲服務，在社區站點建立[或[管理](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#ModifyingSiteProperties)期間，可使用[用戶管理](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#USERMANAGEMENT)設定子面板為社區站點啟用相關的社交登錄設定。](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#SiteCreation)

1. 選擇您儲存社交登入設定的網站設定內容。

1. 在「一般」標籤上，設定雲端設定。

   ![managesites_png](assets/managesites_png.png)

1. 在「設定」標籤上，啟用&#x200B;**[!UICONTROL 社交登入]**&#x200B;並儲存。

   ![usermgmt_png](assets/usermgmt_png.png)

## 測試社交登入{#test-social-login}

* 請確定所有發佈例項上已啟用[AdobeGranite OAuth驗證處理常式](#adobe-granite-oauth-authentication-handler)。
* 確保已發佈雲端服務。
* 確定社群網站已發佈。
* 在瀏覽器中啟動發佈的網站。
例如，http://localhost:4503/content/sites/engage/en.html
* 選擇&#x200B;**[!UICONTROL 登入]**。
* 選擇「使用Facebook登入」或「使用Twitter登入」。********
* 如果尚未登入Facebook或Twitter，請使用適當的認證登入。
* 視Facebook或Twitter應用程式顯示的對話方塊而定，可能需要授與權限。
* 請注意，頁面頂端的工具列已更新，以反映成功登入。
* 選擇&#x200B;**[!UICONTROL 配置檔案]**:「設定檔」頁面會顯示使用者的頭像、名字和姓氏。 它也會根據允許的欄位／參數，顯示來自Facebook或Twitter設定檔的資訊。

## AEM平台OAuth配置{#aem-platform-oauth-configurations}

### AdobeGranite OAuth驗證處理常式{#adobe-granite-oauth-authentication-handler}

`Adobe Granite OAuth Authentication Handler`預設未啟用，且&#x200B;***必須在所有發佈例AEM項上啟用。***

若要在發佈時啟用驗證處理常式，只要開啟OSGi組態並儲存它：

* 以管理員權限登入。
* 導航至[Web控制台](../../help/sites-deploying/configuring-osgi.md)。
例如，http://localhost:4503/system/console/configMgr
* 找到`Adobe Granite OAuth Authentication Handler`。
* 選擇以開啟要編輯的配置。
* 選擇&#x200B;**[!UICONTROL 保存]**。

![graniteauth](assets/graniteoauth.png)

>[!CAUTION]
>
>請注意，請勿將驗證處理常式與&#x200B;*AdobeGranite OAuth應用程式與Provider*&#x200B;的Facebook或Twitter例項混淆。

![graniteauth1](assets/graniteoauth1.png)

### AdobeGranite OAuth應用程式和提供者{#adobe-granite-oauth-application-and-provider}

建立Facebook或Twitter的雲端服務時，會建立`Adobe Granite OAuth Authentication Handler`例項。

若要尋找Facebook或Twitter應用程式的已建立例項：

1. 以管理員權限登入。
1. 導航至[Web控制台](../../help/sites-deploying/configuring-osgi.md)。

   例如，http://localhost:4503/system/console/configMgr。

1. 找到AdobeGranite OAuth應用程式和提供者。

   * 找到&#x200B;**[!UICONTROL Client ID]**&#x200B;符合&#x200B;**[!UICONTROL App ID]**&#x200B;的例項。

      ![graniteauth2](assets/graniteoauth2.png)

      除了下列屬性外，請保留組態的其他屬性不變：

   * **[!UICONTROL 設定ID]**

      （*必要*）OAuth組態ID必須是唯一的。 在建立雲端服務時自動產生。

   * **[!UICONTROL 用戶端識別碼]**

      （*必要*）建立雲端服務時提供的應用程式ID。

   * **[!UICONTROL 用戶端密碼]**

      （*必要*）建立雲端服務時提供的應用程式密碼。

   * **[!UICONTROL 範圍]**

      （*可選*）供應商可詢問允許的額外範圍。 預設範圍涵蓋提供社交驗證和個人檔案資料的必要權限。

   * **[!UICONTROL 提供者ID]**

      （*必要*）建立雲端服務時，會設定AEM Communities的提供者ID。 不要編輯。 對於Facebook Connect，值為&#x200B;*soco -facebook*。 對於Twitter Connect，該值為&#x200B;*soco -twitter*。

   * **[!UICONTROL 群組]**

      (*Recommended*)新增已建立使用者的一或多個成員群組。 對於AEM Communities，建議列出社區站點的成員組。

   * **[!UICONTROL 回呼 URL]**

      （*可選*）URL,OAuth提供者已設定為將用戶端重新導向回原始位置。 使用相對URL來使用原始請求的主機。 留空可改用原本要求的URL。 尾碼&quot;/callback/j_security_check&quot;會自動附加到此URL。
   >[!NOTE]
   >
   >回呼的網域必須向提供者（Facebook或Twitter）註冊。

對於每個OAuth驗證處理常式設定，例項中會另外建立兩個組態：

* Apache Jackrabbit Oak預設同步處理常式(org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler)-不需要進行編輯，但您可以檢視使用者欄位對應，Facebook欄位如何對應至CQ使用者描述檔節點。 另請注意，「同步處理常式名稱」與OAuth提供者設定的設定ID相符。
* Apache Jackrabbit Oak外部登入模組(org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory)-不需要進行編輯，但您可能會注意到「身分提供者名稱」和「同步處理常式名稱」分別指向對應的OA和同步處理常式uth組態。

如需詳細資訊，請參閱[Authentication with Apache Oak External Login Module](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)。

## OAuth使用者遍歷效能{#oauth-user-traversal-performance}

對於使用Facebook或Twitter登入功能註冊的社群網站，當網站訪客使用其社交登入功能時，可新增下列Oak索引來改善查詢的周遊效能。

如果日誌中出現遍歷警告，建議添加此索引。

在作者例項上，以管理權限登入：

1. 從全域導覽：選擇&#x200B;**工具， [CRX/DE Lite](../../help/sites-developing/developing-with-crxde-lite.md)。**
1. 從ntBaseLucene的副本建立名為ntBaseLucene-oauth的索引：

   * 在節點`/oak:index`下
   * 選擇節點`ntBaseLucene`
   * 選擇&#x200B;**[!UICONTROL Copy]**
   * 選取 `/oak:index`
   * 選擇&#x200B;**[!UICONTROL 貼上]**
   * 將ntBaseLucene的副本更名為`ntBaseLucene-oauth`

1. 修改node ntBaseLucene-oauth的屬性：

   * **[!UICONTROL indexPath]**:  `/oak:index/ntBaseLucene-oauth`
   * **[!UICONTROL 名稱]**:  `oauthid-123****`
   * **[!UICONTROL reindex]**:  `true`
   * **[!UICONTROL reindexCount]**:  `1`

1. 在node /oak:index/ntBaseLucene-oauth/indexRules/nt:base/properties下：

   * 刪除所有子節點，cqTags除外。
   * 將cqTags重新命名為`oauthid-123****`
   * 修改節點`oauthid-123****`的屬性

      * **[!UICONTROL 名稱]**:  `oauthid-123****`
   * 選擇&#x200B;**[!UICONTROL 全部保存]**。


* 對於&#x200B;**名稱** `oauthid-123`，請將&#x200B;*123*&#x200B;取代為Facebook ***應用程式ID***&#x200B;或Twitter ***消費者(API)金鑰***，此金鑰是&#x200B;**客戶ID**&#x200B;在[AdobeGranite OAuth應用程式和提供者](social-login.md#adobe-granite-oauth-application-and-provider)組態中。

   ![graniteauth-crxde](assets/graniteoauth-crxde.png)

有關其他資訊和工具，請參閱[Oak Queries and Indexing](../../help/sites-deploying/queries-and-indexing.md)。

## Dispatcher Configuration {#dispatcher-configuration}

請參閱[配置Dispatcher for Communities](dispatcher.md)。
