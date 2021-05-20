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
exl-id: aed9247c-eb81-470c-9fa4-a98c3df2dcaa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2803'
ht-degree: 1%

---

# 使用Facebook和Twitter進行社交登入{#social-login-with-facebook-and-twitter}

社交登入功能可讓網站訪客選擇以其Facebook或Twitter帳戶登入。 因此，請在其AEM成員設定檔中納入允許的Facebook或Twitter資料。

![socialloginweretail](assets/socialloginweretail.png)

## 社交登入概述{#social-login-overview}

若要包含社交登入，建立自訂Facebook和Twitter應用程式是&#x200B;*required*。

雖然we-retail範例提供範例Facebook和Twitter應用程式與雲端服務，但在[生產網站](../../help/sites-administering/production-ready.md)上無法使用。

所需步驟為：

1. [在所有AEM](#adobe-granite-oauth-authentication-handler) 發佈執行個體上啟用OAuth驗證。

   若未啟用OAuth，嘗試登入會失敗。

1. **** 建立社交應用程式和雲端服務。

   * 若要支援使用Facebook登入：

      * 建立[Facebook應用程式](#create-a-facebook-app)。
      * 建立並發佈[Facebook Connect雲端服務](#create-a-facebook-connect-cloud-service)。
   * 若要支援使用Twitter登入：

      * 建立[Twitter應用程式](#create-a-twitter-app)。
      * 建立並發佈[Twitter Connect雲端服務](#create-a-twitter-connect-cloud-service)。


1. [**** 為社](#enable-social-login) 群網站啟用Social登入。

有兩個基本概念：

1. **範圍** （權限）指定應用程式可請求的資料。

   * 依預設，Facebook和Twitter [AdobeGranite OAuth應用程式和提供者](#adobe-granite-oauth-application-and-provider)例項在其範圍內包含基本應用程式權限。

1. **欄位** (params)會指定使用URL參數請求的實際資料。

   * 這些欄位在[AEM Communities Facebook OAuth提供者](#aem-communities-facebook-oauth-provider)和[AEM Communities Twitter OAuth提供者](#aem-communities-twitter-oauth-provider)中指定。
   * 預設欄位對於大多數使用案例來說已足夠，但可以修改。

## Facebook登入{#facebook-login}

### Facebook API版本{#facebook-api-version}

facebook圖表API 1.0版時，就已開發Social登入和we-retail Facebook範例。
自AEM 6.4 GA和AEM 6.3 SP1起，社交登入已更新，可搭配較新的Facebook Graph API 2.5版使用。

>[!NOTE]
>
>若為舊版AEM，如果您在記錄&#x200B;**中遇到例外狀況，無法從此**&#x200B;擷取代號，請針對該AEM版本升級至最新的CFP。

如需Facebook圖表API版本資訊，請參閱[Facebook API變更記錄](https://developers.facebook.com/docs/apps/changelog)。

### 建立Facebook應用程式{#create-a-facebook-app}

必須有正確設定的Facebook應用程式才能啟用Facebook social登入。

若要建立Facebook應用程式，請依照Facebook的指示，網址為[https://developers.facebook.com/apps/](https://developers.facebook.com/apps/)。 下列資訊不會反映對其指示的變更。

一般而言，自Facebook API v2.7起：

* *新增Facebook應用程式*
   * 對於&#x200B;*Platform*，選擇「網站：
      * 對於&#x200B;*網站URL*，請輸入`  https://<server>:<port>.`
      * 對於&#x200B;*顯示名稱*，輸入標題以用作Facebook連接服務的標題。
      * 若為&#x200B;*類別*，建議您選擇&#x200B;*頁面應用程式*，但可以是任何項目。
      * *添加產品：Facebook登入*
      * 對於&#x200B;*有效的OAuth重定向URI*，請輸入`  https://<server>:<port>.`

>[!NOTE]
>
>對於發展，http://localhost:4503將有效。

建立應用程式後，找出&#x200B;**[!UICONTROL 應用程式ID]**&#x200B;和&#x200B;**[!UICONTROL 應用程式密碼]**&#x200B;設定。 設定[Facebook雲端服務](#createafacebookcloudservice)時需要此資訊。

### 建立Facebook連接Cloud Service{#create-a-facebook-connect-cloud-service}

透過建立雲端服務設定來具現化的[AdobeGranite OAuth應用程式和Provider](#adobe-granite-oauth-application-and-provider)例項，可識別新使用者所加入的Facebook應用程式和成員群組。

1. 在AEM製作例項上，以管理員權限登入。
1. 在全域導覽中，選取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Facebook Social登入設定]**。
1. 選擇配置&#x200B;**[!UICONTROL 上下文路徑]**。

   **[!UICONTROL 上]** 下文路徑應與建立/編輯社群網站時所選的雲配置路徑相同。

1. 檢查您的內容路徑是否已啟用，以在其下建立雲端服務。
1. 前往&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 配置瀏覽器]**。 選取您的內容並編輯屬性。 如果尚未啟用，請啟用雲端設定。

   ![config-propertyspng](assets/config-propertiespng.png)

   * 如需詳細資訊，請參閱[設定瀏覽器](/help/sites-administering/configurations.md)檔案。

1. **建立/** 編輯Facebook雲端服務設定。

   ![fbsocialloginconfigpng](assets/fbsocialloginconfigpng.png)

   * **[!UICONTROL 標題]** (*必要*)輸入可識別Facebook應用程式的顯示標題。建議您使用與為Facebook應用程式輸入的&#x200B;*顯示名稱*&#x200B;相同的名稱。
   * **[!UICONTROL 應用程式ID/API金鑰]** (*必要*)輸入Facebook ***應用*** 程式的應用程式ID。這會識別從對話方塊建立的[AdobeGranite OAuth應用程式和Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider)例項。
   * **[!UICONTROL 應用程式密碼]** (*必要*)輸入Facebook ***應用*** 程式的應用程式密碼。
   * **[!UICONTROL 建]** 立使用者如果勾選此選項，使用Facebook帳戶登入將建立AEM使用者項目，並將他們新增為所選使用者群組的成員。已勾選預設值（強烈建議）。
   * **[!UICONTROL 遮罩使用者ID]**:保持未選。
   * **[!UICONTROL 範圍電子郵件]**:應從Facebook擷取使用者的電子郵件id。
   * **[!UICONTROL 添加到用]** 戶組選擇添加用戶組，以為將添加 [用](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html) 戶的社區站點選擇一個或多個成員組。

   >[!NOTE]
   >
   >可隨時新增或移除群組。 但現有用戶的成員資格不會受到影響。 自動成員資格僅適用於此欄位更新後建立的新使用者。 對於匿名用戶被禁用的站點，選擇將用戶添加到為該封閉的社區站點而指定的相應社區成員組。

   * 選擇&#x200B;**[!UICONTROL SAVE]**。
   * **[!UICONTROL 發佈]**.



結果為[AdobeGranite OAuth應用程式和提供者](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider)例項，除非新增其他範圍（權限），否則不需要進一步修改。 預設範圍是Facebook登入的標準權限。 如果需要其他範圍，則需要直接編輯OSGI設定。 如果有直接透過系統/主控台完成的修改，請避免從觸控式UI編輯雲端服務設定，以避免覆寫。

### AEM Communities Facebook OAuth提供者{#aem-communities-facebook-oauth-provider}

AEM Communities提供者延伸[AdobeGranite OAuth應用程式和提供者](#adobe-granite-oauth-application-and-provider)例項。

此提供程式需要編輯：

* 允許用戶更新
* 在範圍](#adobe-granite-oauth-application-and-provider)內添加其他欄位[

   * 預設情況下，並非所有允許的欄位都包含在內。

如果需要編輯，請在每個AEM發佈例項上：

1. 以管理員權限登入。
1. 導覽至[Web主控台](../../help/sites-deploying/configuring-osgi.md)。 例如， http://localhost:4503/system/console/configMgr。
1. 找到AEM Communities Facebook OAuth提供者。
1. 選取要開啟以進行編輯的鉛筆圖示。

   ![fboauthprov_png](assets/fboauthprov_png.png)

   * **[!UICONTROL OAuth提供者ID]**

      （*必要*）預設值為&#x200B;*soco -facebook*。 請勿編輯。

   * **[!UICONTROL Cloud Service設定]**

      預設值為 `/etc/  cloudservices /  facebookconnect`. 請勿編輯。

   * **[!UICONTROL OAuth提供程式服務配置]**

      預設值為 `/apps/social/facebookprovider/config/`. 請勿編輯。

   * **[!UICONTROL 啟用標籤]**

      請勿編輯。

   * **[!UICONTROL 使用者路徑]**

      儲存使用者資料的存放庫位置。 對於社群網站，為確保成員能夠查看彼此的配置檔案的權限，路徑應為預設的&#x200B;*/home/users/community*。

   * **[!UICONTROL 啟用欄位]**

      若勾選此選項，系統會在向Facebook提出使用者驗證和資訊的要求時指定所列的欄位。 取消選取預設值。

   * **[!UICONTROL 欄位]**

      啟用欄位時，呼叫Facebook圖表API時會包含下列欄位。 必須允許在雲端服務設定中定義的範圍內使用欄位。 其他欄位可能需要Facebook核准。 參考Facebook檔案的Facebook登入權限區段。 新增為參數的預設欄位為：

      * id
      * 名稱
      * first_name
      * last_name
      * 連結
      * 地區設定
      * 圖片
      * 時區
      * updated_time
      * 已驗證
      * 電子郵件

   如果添加或更改了任何欄位，請更新相應的預設同步處理程式配置以更正映射。

   * **[!UICONTROL 更新用戶]**

      若勾選此選項，則會在每次登入時重新整理存放庫中的使用者資料，以反映設定檔變更或請求的其他資料。 已取消選取預設值。


#### 後續步驟{#next-steps}

facebook和Twitter的後續步驟相同：

* [發佈雲端服務設定](#publishcloudservices)
* [為社區站點啟用](#enable-social-login)

## Twitter登入{#twitter-login}

### 建立Twitter應用程式{#create-a-twitter-app}

必須有已設定的Twitter應用程式才能啟用Twitter social登入。

請依照最新指示，在[https://apps.twitter.com](https://apps.twitter.com/)建立新的Twitter應用程式。

一般而言：

1. 輸入&#x200B;*名稱* ，以識別您的網站使用者的Twitter應用程式。
1. 輸入&#x200B;*Description*。
1. 對於&#x200B;*website* — 輸入`https://<server>`。
1. 對於&#x200B;*回呼URL* — 輸入`https://server`。

   >[!NOTE]
   >
   >無需指定埠。
   >
   >對於發展，https://127.0.0.1/將有效。

1. 建立應用程式後，找出&#x200B;**[!UICONTROL 使用者(API)金鑰]**&#x200B;和&#x200B;**[!UICONTROL 使用者(API)密碼]**。 設定[Twitter雲端服務](#createatwittercloudservice)時需要此資訊。

#### 權限 {#permissions}

在Twitter應用程式管理的權限區段中：

* **[!UICONTROL 存取]**:選取 `Read only`。

   * 不支援其他選項

* **[!UICONTROL 其他權限]**:（可選） `Request email addresses from users`選擇。

   * 若未選取，AEM中的使用者設定檔將不包含其電子郵件地址。
   * Twitter的說明說明需要採取的其他步驟。

對社交登入提出的唯一REST要求是&#x200B;*[GET帳戶/驗證憑證](https://dev.twitter.com/rest/reference/get/account/verify_credentials)*。

### 建立Twitter連接Cloud Service{#create-a-twitter-connect-cloud-service}

透過建立雲端服務設定來具現化的[AdobeGranite OAuth應用程式和Provider](#adobe-granite-oauth-application-and-provider)例項，可識別新使用者所加入的Twitter應用程式和成員群組。

1. 在製作例項上，使用管理員權限登入。
1. 在全域導覽中，選取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Twitter Social登入設定]**。
1. 選擇&#x200B;**[!UICONTROL 上下文路徑]**&#x200B;配置。

   上下文路徑應與您在建立/編輯社群網站時選取的雲配置路徑相同。

1. 檢查您的內容路徑是否已啟用，以在其下建立雲端服務。
1. 前往&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 一般]** > **[!UICONTROL 配置瀏覽器]**。 選取您的內容並編輯屬性。 如果尚未啟用，請啟用雲端設定。

   ![twitterconfigpropping](assets/twitterconfigproppng.png)

   * 如需詳細資訊，請參閱[設定瀏覽器](/help/sites-administering/configurations.md)檔案。

1. 建立/編輯Twitter雲端服務設定。

   ![twittersocialloginpng](assets/twittersocialloginpng.png)

   * **[!UICONTROL 標題]**

      （*必要*）輸入識別Twitter應用程式的顯示標題。 建議您使用與為Twitter應用程式輸入的&#x200B;*顯示名稱*&#x200B;相同的名稱。

   * **[!UICONTROL 消費者金鑰]**

      （*必要*）輸入Twitter應用程式的&#x200B;**消費者(API)索引鍵**。 這會識別從對話方塊建立的[AdobeGranite OAuth應用程式和Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#AdobeGraniteOAuthApplicationandProvider)例項。

   * **[!UICONTROL 消費者機密]**

      （*必要*）輸入Twitter應用程式的&#x200B;***消費者(API)密碼***。

   * **[!UICONTROL 建立使用者]**

      若勾選此選項，使用Twitter帳戶登入將會建立AEM使用者項目，並將其新增為所選使用者群組的成員。 已勾選預設值（強烈建議）。

   * **[!UICONTROL 隱藏使用者 ID]**

      保持未選。

   * **[!UICONTROL 新增到使用者群組]**

      選擇「添加用戶組」以為將添加用戶的社區站點選擇一個或多個[成員組](https://helpx.adobe.com/experience-manager/6-3/communities/using/users.html)。
   >[!NOTE]
   >
   >可隨時新增或移除群組。 但現有使用者的會籍不會受到影響。 自動成員資格僅適用於此欄位更新後建立的新使用者。 對於匿名用戶被禁用的站點，將用戶添加到為該封閉的社區站點指定的相應社區成員組。

1. 選擇&#x200B;**[!UICONTROL SAVE]**&#x200B;和&#x200B;**[!UICONTROL Publish]**。

結果是不需要進一步修改的[AdobeGranite OAuth應用程式和Provider](https://helpx.adobe.com/experience-manager/6-3/communities/using/social-login.html#adobe-granite-oauth-application-and-provider)例項。 預設範圍是Twitter登入的標準權限。

### AEM Communities Twitter OAuth提供者{#aem-communities-twitter-oauth-provider}

AEM Communities設定會擴充[AdobeGranite OAuth應用程式和Provider](#adobe-granite-oauth-application-and-provider)例項。 此提供程式需要編輯才能允許用戶更新。

如果需要編輯，請在每個AEM發佈例項上：

1. 以管理員權限登入。
1. 導覽至[Web主控台](../../help/sites-deploying/configuring-osgi.md)。

   例如， http://localhost:4503/system/console/configMgr。

1. 找到AEM Communities Twitter OAuth提供者。
1. 選取要開啟以進行編輯的鉛筆圖示。

   ![twitteauth_png](assets/twitteroauth_png.png)

   * **[!UICONTROL OAuth提供者ID]**

   （*必要*）預設值為&#x200B;*soco -twitter*。 請勿編輯。

   * **[!UICONTROL Cloud Service設定]**

      預設值為&#x200B;*「conf」。* 請勿編輯。

   * **[!UICONTROL OAuth提供程式服務配置]**

      預設值為 `/apps/social/twitterprovider/config/`. 請勿編輯。

   * **[!UICONTROL 使用者路徑]**

      儲存使用者資料的存放庫位置。 對於社群網站，為確保成員能夠查看彼此的配置檔案的權限，路徑應為預設`/home/users/community`。

   * **[!UICONTROL 啟]** 用參數不編輯
   * **[!UICONTROL URL參]** 數不編輯
   * **[!UICONTROL 更新用戶]**

      若勾選此選項，則會在每次登入時重新整理存放庫中的使用者資料，以反映設定檔變更或請求的其他資料。 取消選取預設值。


#### 後續步驟{#next-steps-1}

facebook和Twitter的後續步驟相同：

* [發佈雲端服務設定](#publishcloudservices)
* [為社區站點啟用](#enable-social-login)

## 啟用社交登入{#enable-social-login}

### AEM Communities Sites Console {#aem-communities-sites-console}

雲端服務一旦設定完成，即可在社群網站[建立](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#SiteCreation)或[管理](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#ModifyingSiteProperties)期間，使用「[使用者管理](https://helpx.adobe.com/experience-manager/6-3/communities/using/sites-console.html#USERMANAGEMENT)設定」子面板，為社群網站啟用相關的社交登入設定。

1. 選擇您儲存社交登入設定的網站設定內容。

1. 在「一般」標籤上，設定雲配置。

   ![managesites_png](assets/managesites_png.png)

1. 在「設定」標籤上，啟用&#x200B;**[!UICONTROL 社交登入]**&#x200B;並儲存。

   ![usermgmt_png](assets/usermgmt_png.png)

## 測試社交登入{#test-social-login}

* 確認所有發佈執行個體上皆已啟用[AdobeGranite OAuth驗證處理常式](#adobe-granite-oauth-authentication-handler)。
* 確保雲端服務已發佈。
* 確保已發佈社群網站。
* 在瀏覽器中啟動已發佈的網站。
例如， http://localhost:4503/content/sites/engage/en.html
* 選擇&#x200B;**[!UICONTROL 登錄]**。
* 選取「**[!UICONTROL 使用Facebook登入]**」或「**[!UICONTROL 使用Twitter登入]**」。
* 如果尚未登入Facebook或Twitter，請使用適當的憑證登入。
* 視Facebook或Twitter應用程式顯示的對話方塊而定，可能需要授予權限。
* 請注意，頁面頂端的工具列已更新，以反映成功登入。
* 選擇&#x200B;**[!UICONTROL 配置檔案]**:設定檔頁面會顯示使用者的頭像影像、名字和姓氏。 它也會根據允許的欄位/參數顯示Facebook或Twitter設定檔的資訊。

## AEM平台OAuth設定{#aem-platform-oauth-configurations}

### AdobeGranite OAuth驗證處理常式{#adobe-granite-oauth-authentication-handler}

預設不會啟用`Adobe Granite OAuth Authentication Handler`，且必須在所有AEM發佈執行個體上啟用&#x200B;***。***

若要在發佈時啟用驗證處理常式，只需開啟OSGi設定並儲存：

* 以管理員權限登入。
* 導覽至[Web主控台](../../help/sites-deploying/configuring-osgi.md)。
例如， http://localhost:4503/system/console/configMgr
* 找到`Adobe Granite OAuth Authentication Handler`。
* 選取以開啟要編輯的設定。
* 選擇&#x200B;**[!UICONTROL 保存]**。

![graniteauth](assets/graniteoauth.png)

>[!CAUTION]
>
>請留意勿將驗證處理常式與&#x200B;*AdobeGranite OAuth應用程式和提供者*&#x200B;的Facebook或Twitter例項混淆。

![graniteauth1](assets/graniteoauth1.png)

### AdobeGranite OAuth應用程式和提供程式{#adobe-granite-oauth-application-and-provider}

建立Facebook或Twitter的雲端服務時，會建立`Adobe Granite OAuth Authentication Handler`例項。

若要找出Facebook或Twitter應用程式的已建立例項：

1. 以管理員權限登入。
1. 導覽至[Web主控台](../../help/sites-deploying/configuring-osgi.md)。

   例如， http://localhost:4503/system/console/configMgr。

1. 找出AdobeGranite OAuth應用程式和提供者。

   * 找出&#x200B;**[!UICONTROL 用戶端ID]**&#x200B;符合&#x200B;**[!UICONTROL 應用程式ID]**&#x200B;的例項。

      ![graniteoauth2](assets/graniteoauth2.png)

      除了下列屬性外，將設定的其他屬性保持未變更：

   * **[!UICONTROL 設定ID]**

      （*必要*）OAuth設定ID必須是唯一的。 建立雲端服務時自動產生。

   * **[!UICONTROL 用戶端識別碼]**

      （*必要*）建立雲端服務時提供的應用程式ID。

   * **[!UICONTROL 用戶端密碼]**

      （*必要*）建立雲端服務時提供的應用程式密碼。

   * **[!UICONTROL 範圍]**

      （*可選*）可向提供程式詢問允許的其他範圍。 預設範圍涵蓋提供社交驗證和設定檔資料所需的權限。

   * **[!UICONTROL 提供者ID]**

      （*必要*）建立雲端服務時，會設定AEM Communities的提供者ID。 請勿編輯。 若為Facebook Connect，則值為&#x200B;*soco -facebook*。 若為Twitter Connect，則值為&#x200B;*soco -twitter*。

   * **[!UICONTROL 群組]**

      （*建議*）新增已建立使用者的一或多個成員群組。 若為AEM Communities，建議列出社群網站的成員群組。

   * **[!UICONTROL 回呼 URL]**

      （*選用*）URL已透過OAuth提供者設定，以將用戶端重新導向回。 使用相對URL來使用原始請求的主機。 保留為空白，以改用原本請求的URL。 尾碼「/callback/j_security_check」會自動附加至此url。
   >[!NOTE]
   >
   >回呼的網域必須向提供者(Facebook或Twitter)註冊。

對於每個OAuth驗證處理常式設定，例項中會建立另外兩個設定：

* Apache Jackrabbit Oak Default同步處理常式(org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler) — 此處無需編輯，但您可以查看Facebook欄位對應至CQ使用者設定檔節點的使用者欄位對應。 另請注意，「同步處理常式名稱」與OAuth提供者設定的設定ID相符。
* Apache Jackrabbit Oak External登入模組(org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory) — 此處無須編輯，但您可能會注意到「身分提供者名稱」和「同步處理常式名稱」相同，並分別指向對應的OAuth和同步處理常式設定。

如需詳細資訊，請參閱[使用Apache Oak External登入模組](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)驗證。

## OAuth用戶遍歷效能{#oauth-user-traversal-performance}

針對使用Facebook或Twitter登入功能註冊的社群網站，當網站訪客使用其社交登入功能時，查詢的周遊效能會因為新增下列Oak索引而得以改善。

如果日誌中出現遍歷警告，則建議添加此索引。

在製作例項上，以管理權限登入：

1. 從全局導航：選擇&#x200B;**工具， [CRX/DE Lite](../../help/sites-developing/developing-with-crxde-lite.md)。**
1. 從ntBaseLucene的副本建立名為ntBaseLucene-oauth的索引：

   * 在節點`/oak:index`下
   * 選擇節點`ntBaseLucene`
   * 選擇&#x200B;**[!UICONTROL 複製]**
   * 選取 `/oak:index`
   * 選擇&#x200B;**[!UICONTROL 貼上]**
   * 將ntBaseLucene的副本更名為`ntBaseLucene-oauth`

1. 修改ntBaseLucene-oauth的屬性：

   * **[!UICONTROL indexPath]**:  `/oak:index/ntBaseLucene-oauth`
   * **[!UICONTROL 名稱]**:  `oauthid-123****`
   * **[!UICONTROL 重新索引]**:  `true`
   * **[!UICONTROL reindexCount]**:  `1`

1. 在節點/oak:index/ntBaseLucene-oauth/indexRules/nt:base/properties底下：

   * 刪除cqTags以外的所有子節點。
   * 將cqTags重新命名為`oauthid-123****`
   * 修改節點`oauthid-123****`的屬性

      * **[!UICONTROL 名稱]**:  `oauthid-123****`
   * 選擇&#x200B;**[!UICONTROL 保存全部]**。


* 對於&#x200B;**name** `oauthid-123`，請使用Facebook ***應用程式ID***&#x200B;或Twitter ***消費者(API)索引鍵***&#x200B;取代&#x200B;**用戶端ID** ，此為[AdobeGranite OA應用程式和提供者A12/配置中的值。**](social-login.md#adobe-granite-oauth-application-and-provider)

   ![graniteoauth-crxde](assets/graniteoauth-crxde.png)

如需其他資訊和工具，請參閱[Oak Querys and Indexing](../../help/sites-deploying/queries-and-indexing.md)。

## Dispatcher設定{#dispatcher-configuration}

請參閱[為Communities設定Dispatcher](dispatcher.md)。
