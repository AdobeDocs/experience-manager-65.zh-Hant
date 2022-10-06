---
title: 單一登入
seo-title: Single Sign On
description: 了解如何為AEM例項設定單一登入(SSO)。
seo-description: Learn how to configure Single Sign On (SSO) for an AEM instance.
uuid: b8dcb28e-4604-4da5-b8dd-4e1e2cbdda18
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring, Security
content-type: reference
discoiquuid: 86e8dc12-608d-4aff-ba7a-5524f6b4eb0d
feature: Configuring
exl-id: 7d2e4620-c3a5-4f5a-9eb6-42a706479d41
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 0%

---

# 單一登入 {#single-sign-on}

單一登入(SSO)允許用戶在提供一次身份驗證憑據（如用戶名和密碼）後訪問多個系統。 單獨的系統（稱為可信驗證器）執行該驗證，並提供具有用戶憑據的Experience Manager。 Experience Manager會檢查並強制使用者的存取權限（即決定允許使用者存取的資源）。

SSO驗證處理程式服務( `com.adobe.granite.auth.sso.impl.SsoAuthenticationHandler`)會處理受信任驗證器提供的驗證結果。 SSO身份驗證處理程式按以下順序在以下位置中搜索ssid（SSO標識符）作為特殊屬性的值：

1. 請求標題
1. Cookie
1. 要求參數

找到值後，搜尋即完成，並使用此值。

配置以下兩個服務以識別儲存ssid的屬性的名稱：

* 登入模組。
* SSO驗證服務。

您必須為兩個服務指定相同的屬性名稱。 屬性包含在 `SimpleCredentials` 提供給 `Repository.login`. 屬性的值不相關且被忽略，僅存在它是重要的，是經過驗證的。

## 配置SSO {#configuring-sso}

若要為AEM例項設定SSO，您必須設定 [SSO驗證處理程式](/help/sites-deploying/osgi-configuration-settings.md#adobegranitessoauthenticationhandler):

1. 使用AEM時，有數種方法可管理這類服務的組態設定；請參閱 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以取得詳細資訊和建議的實務。

   例如，對於NTLM集：

   * **路徑：** 視需要；例如， `/`
   * **標題名稱**: `LOGON_USER`
   * **ID格式**: `^<DOMAIN>\\(.+)$`

      其中 `<*DOMAIN*>` 會由您自己的網域名稱取代。
   CoSign:

   * **路徑：** 視需要；例如， `/`
   * **標題名稱**:remote_user
   * **ID格式：** 原樣

   對於SiteMinder:

   * **路徑：** 視需要；例如， `/`
   * **標題名稱：** SM_USER
   * **ID格式**:原樣



1. 確認單一登入可視需要運作；包括授權。

>[!CAUTION]
>
>請確定若已設定SSO，使用者無法直接存取AEM。
>
>通過要求用戶通過運行SSO系統代理的Web伺服器，可確保任何用戶都不能直接發送標頭、Cookie或參數，以使用戶受到AEM信任，因為如果從外部發送，代理將過濾這些資訊。
>
>任何使用者只要知道名稱，只要能直接存取您的AEM例項而不需瀏覽Web伺服器，就能透過傳送標題、Cookie或參數來擔任任何使用者。
>
>另請確定標頭、Cookie和請求參數名稱，您只需設定SSO設定所需的名稱。

>[!NOTE]
>
>單一登入通常與 [LDAP](/help/sites-administering/ldap-config.md).

>[!NOTE]
>
>如果您也使用 [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) 使用Microsoft Internet Information Server(IIS)時，以下項目將需要其他配置：
>
>* `disp_iis.ini`
>* IIS
>
>在 `disp_iis.ini` 設定：
>(請參閱 [使用Microsoft Internet Information Server安裝Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html#microsoft-internet-information-server) 如需完整詳細資訊)
>
>* `servervariables=1` （將IIS伺服器變數作為請求標頭轉發到遠程實例）
>* `replaceauthorization=1` （以「基本」等值項取代「授權」以外的任何標題）
>
>在IIS中：
>
>* disable **匿名訪問**
>
>* 啟用 **整合Windows驗證**
>


您可以使用 **驗證器** Felix Console的選項；例如：

`http://localhost:4502/system/console/slingauth`

系統會先查詢最符合路徑的處理常式。 例如，如果您為路徑配置處理常式 — A `/` 和處理程式 — B `/content`，則 `/content/mypage.html` 會先查詢處理常式B。

![screen_shot_2012-02-15at21006pm](assets/screen_shot_2012-02-15at21006pm.png)

### 範例 {#example}

Cookie請求(使用URL `http://localhost:4502/libs/wcm/content/siteadmin.html`):

```xml
GET /libs/cq/core/content/welcome.html HTTP/1.1
Host: localhost:4502
Cookie: TestCookie=admin
```

使用下列設定：

* **路徑**: `/`

* **標題名稱**: `TestHeader`

* **Cookie名稱**: `TestCookie`

* **參數名稱**: `TestParameter`

* **ID格式**: `AsIs`

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

如果您要求：
`http://localhost:4502/libs/cq/core/content/welcome.html?TestParameter=admin`

或者，您可以使用下列curl命令傳送 `TestHeader` 標題至 `admin:`
`curl -D - -H "TestHeader: admin" http://localhost:4502/libs/cq/core/content/welcome.html`

>[!NOTE]
>
>在瀏覽器中使用請求參數時，您只會看到部分HTML — 沒有CSS。 這是因為來自HTML的所有請求都是在沒有請求參數的情況下提出。

## 移除AEM登出連結 {#removing-aem-sign-out-links}

使用SSO時，系統會從外部處理登入和登出，因此AEM.自己的登出連結不再適用，應移除。

可使用下列步驟移除歡迎畫面上的登出連結。

1. 覆蓋 `/libs/cq/core/components/welcome/welcome.jsp` to `/apps/cq/core/components/welcome/welcome.jsp`
1. 從jsp中刪除以下部件。

   `<a href="#" onclick="signout('<%= request.getContextPath() %>');" class="signout"><%= i18n.get("sign out", "welcome screen") %>`

若要移除右上角使用者個人功能表中可用的登出連結，請執行下列步驟：

1. 覆蓋 `/libs/cq/ui/widgets/source/widgets/UserInfo.js` to `/apps/cq/ui/widgets/source/widgets/UserInfo.js`

1. 從檔案中刪除以下部分：

   ```
   menu.addMenuItem({
       "text":CQ.I18n.getMessage("Sign out"),
       "cls": "cq-userinfo-logout",
       "handler": this.logout
   });
   menu.addSeparator();
   ```
