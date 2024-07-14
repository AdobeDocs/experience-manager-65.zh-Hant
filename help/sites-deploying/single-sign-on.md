---
title: 單一登入
description: 瞭解如何為Adobe Experience Manager (AEM)的執行個體設定單一登入(SSO)。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring, Security
content-type: reference
feature: Security
exl-id: 7d2e4620-c3a5-4f5a-9eb6-42a706479d41
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---

# 單一登入 {#single-sign-on}

單一登入(SSO)可讓使用者在提供一次驗證認證（例如使用者名稱和密碼）之後存取多個系統。 另一個系統（稱為受信任的驗證者）會執行驗證並提供使用者認證的Experience Manager。 Experience Manager會檢查並強制使用者的存取許可權（即決定允許使用者存取哪些資源）。

SSO驗證處理常式服務( `com.adobe.granite.auth.sso.impl.SsoAuthenticationHandler`)會處理受信任的驗證器所提供的驗證結果。 SSO驗證處理常式會依此順序在下列位置搜尋SSO識別碼(SSID)作為特殊屬性的值：

1. 請求標頭
1. Cookie
1. 要求引數

找到值時，即完成搜尋並使用此值。

設定以下兩個服務來識別儲存SSID的屬性名稱：

* 登入模組。
* SSO驗證服務。

為兩個服務指定相同的屬性名稱。 屬性包含在提供給`Repository.login`的`SimpleCredentials`中。 屬性的值不相關且會被忽略，只要存在就很重要且經過驗證。

## 設定SSO {#configuring-sso}

若要設定AEM執行個體的SSO，請設定[SSO驗證處理常式](/help/sites-deploying/osgi-configuration-settings.md#adobegranitessoauthenticationhandler)：

1. 使用AEM時，有數種方法可管理此類服務的組態設定；請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)以取得詳細資訊和建議的作法。

   例如，對於NTLM集：

   * **路徑：**&#x200B;為必要；例如，`/`
   * **標頭名稱**： `LOGON_USER`
   * **ID格式**： `^<DOMAIN>\\(.+)$`

     其中`<*DOMAIN*>`會由您自己的網域名稱取代。

   對於CoSign：

   * **路徑：**&#x200B;為必要；例如，`/`
   * **標頭名稱**： remote_user
   * **ID格式：** AsIs

   對於SiteMinder：

   * **路徑：**&#x200B;為必要；例如，`/`
   * **標頭名稱：** SM_USER
   * **ID格式**： AsIs

1. 確認單一登入已視需要運作；包括授權。

>[!CAUTION]
>
>如果設定了SSO，請確定使用者無法直接存取AEM。
>
>透過要求使用者通過執行SSO系統代理程式的網頁伺服器，可確保沒有任何使用者能夠直接傳送標頭、Cookie或引數來將使用者授予AEM信任，因為代理程式會篩選從外部傳送的此類資訊。
>
>任何使用者只要不透過網頁伺服器直接存取您的AEM執行個體，便可傳送標頭、Cookie或引數（若名稱已知），擔任任何使用者。
>
>另外也請確定在標頭、Cookie和請求引數名稱中，您只設定SSO設定所需的名稱。
>

>[!NOTE]
>
>單一登入常搭配[LDAP](/help/sites-administering/ldap-config.md)使用。

>[!NOTE]
>
>如果您也使用[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)搭配Microsoft® Internet Information Server (IIS)，則需要在下列專案中進行其他設定：
>
>* `disp_iis.ini`
>* IIS
>
>在`disp_iis.ini`集合中：
>(如需完整詳細資訊，請參閱[使用Microsoft® Internet Information Server安裝Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/dispatcher-install.html#microsoft-internet-information-server))
>
>* `servervariables=1` （將IIS伺服器變數作為要求標頭轉送給遠端執行個體）
>* `replaceauthorization=1` (將任何名為「Authorization」的標頭（「Basic」以外的標頭取代為「Basic」的對等標頭）
>
>在IIS中：
>
>* 停用&#x200B;**匿名存取**
>
>* 啟用&#x200B;**整合式Windows驗證**
>

您可以使用Felix主控台的&#x200B;**Authenticator**&#x200B;選項，檢視哪個驗證處理常式正在套用至內容樹狀結構的任何區段；例如：

`http://localhost:4502/system/console/slingauth`

系統會先查詢最符合路徑的處理常式。 例如，如果您為路徑`/`設定處理常式A，為路徑`/content`設定處理常式B，則對`/content/mypage.html`的請求將先查詢處理常式B。

![screen_shot_2012-02-15at21006pm](assets/screen_shot_2012-02-15at21006pm.png)

### 範例 {#example}

針對Cookie要求（使用URL `http://localhost:4502/libs/wcm/content/siteadmin.html`）：

```xml
GET /libs/cq/core/content/welcome.html HTTP/1.1
Host: localhost:4502
Cookie: TestCookie=admin
```

使用以下設定：

* **路徑**： `/`

* **標頭名稱**： `TestHeader`

* **Cookie名稱**： `TestCookie`

* **引數名稱**： `TestParameter`

* **ID格式**： `AsIs`

回應會是：

```xml
HTTP/1.1 200 OK
Connection: Keep-Alive
Server: Day-Servlet-Engine/4.1.24
Content-Type: text/html;charset=utf-8
Date: Thu, 23 Aug 2012 09:58:39 GMT
Transfer-Encoding: chunked

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "https://www.w3.org/TR/html4/strict.dtd">
<html>
<head>
    <meta http-equiv="content-type" content="text/html; charset=UTF-8">
    <title>Welcome to Adobe&reg; CQ5</title>
....
```

如果您請求：
`http://localhost:4502/libs/cq/core/content/welcome.html?TestParameter=admin`

或者，您可以使用以下curl命令將`TestHeader`標頭傳送至`admin:`
`curl -D - -H "TestHeader: admin" http://localhost:4502/libs/cq/core/content/welcome.html`

>[!NOTE]
>
>在瀏覽器中使用請求引數時，您只會看到部分HTML — 沒有CSS。 這是因為來自HTML的所有請求都是在沒有請求引數的情況下進行的。

## 移除AEM登出連結 {#removing-aem-sign-out-links}

使用SSO時，登入和登出會在外部處理，因此AEM自己的登出連結已不再適用且應移除。

您可使用下列步驟移除歡迎畫面上的登出連結。

1. 覆蓋`/libs/cq/core/components/welcome/welcome.jsp`到`/apps/cq/core/components/welcome/welcome.jsp`
1. 從jsp中移除下列零件。

   `<a href="#" onclick="signout('<%= request.getContextPath() %>');" class="signout"><%= i18n.get("sign out", "welcome screen") %>`

若要移除使用者右上角個人功能表中可用的登出連結，請執行下列步驟：

1. 覆蓋`/libs/cq/ui/widgets/source/widgets/UserInfo.js`到`/apps/cq/ui/widgets/source/widgets/UserInfo.js`

1. 從檔案中移除下列部分：

   ```
   menu.addMenuItem({
       "text":CQ.I18n.getMessage("Sign out"),
       "cls": "cq-userinfo-logout",
       "handler": this.logout
   });
   menu.addSeparator();
   ```
