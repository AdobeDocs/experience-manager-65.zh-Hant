---
title: 單一登入
seo-title: 單一登入
description: 瞭解如何為AEM例項設定單一登入(SSO)。
seo-description: 瞭解如何為AEM例項設定單一登入(SSO)。
uuid: b8dcb28e-4604-4da5-b8dd-4e1e2cbdda18
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
discoiquuid: 86e8dc12-608d-4aff-ba7a-5524f6b4eb0d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 單一登入 {#single-sign-on}

單一登入(SSO)可讓使用者在提供驗證憑證（例如使用者名稱和密碼）一次後，存取多個系統。 另一個系統（稱為受信任驗證器）執行驗證，並為Experience manager提供用戶憑證。 Experience manager會檢查並強制使用者的存取權限（亦即決定允許使用者存取哪些資源）。

SSO驗證處理程式服務( `com.adobe.granite.auth.sso.impl.SsoAuthenticationHandler`)會處理受信任驗證器提供的驗證結果。 SSO驗證處理程式會依此順序在下列位置中，將ssid（SSO標識符）搜索為特殊屬性的值：

1. 請求標題
1. Cookie
1. 請求參數

找到值時，搜索完成，並使用此值。

配置以下兩個服務以識別儲存ssid的屬性名稱：

* 登錄模組。
* SSO驗證服務。

您必須為兩個服務指定相同的屬性名稱。 屬性會包含在提 `SimpleCredentials` 供給的中 `Repository.login`。 屬性的值是不相關的，忽略的，僅存在就很重要。

## 設定SSO {#configuring-sso}

若要為AEM例項設定SSO，您必須設定 [SSO驗證處理常式](/help/sites-deploying/osgi-configuration-settings.md#adobegranitessoauthenticationhandler):

1. 使用AEM時，有幾種方法可管理此類服務的組態設定；如需詳 [細資訊](/help/sites-deploying/configuring-osgi.md) ，請參閱設定OSGi。

   例如，對於NTLM集：

   * **** 路徑：視需要；例如， `/`
   * **標題名稱**: `LOGON_USER`
   * **ID格式**: `^<DOMAIN>\\(.+)$`

      其中 `<*DOMAIN*>` 將由您自己的域名替換。
   針對CoSign:

   * **** 路徑：視需要；例如， `/`
   * **標題名稱**:remote_user
   * **** ID格式：現狀
   對於SiteMinder:

   * **** 路徑：視需要；例如， `/`
   * **** 標題名稱：SM_USER
   * **ID格式**:現狀



1. 確認單一登入功能是否可視需要運作；包括授權。

>[!CAUTION]
>
>請確定使用者無法在設定SSO時直接存取AEM。
>
>透過要求使用者透過執行您SSO系統代理程式的網頁伺服器，可確保使用者無法直接傳送標題、Cookie或參數，讓使用者受到AEM的信任，因為如果從外部傳送，代理程式會篩選此類資訊。
>
>任何可直接存取您AEM例項而不需透過網頁伺服器的使用者，都可以透過傳送標題、Cookie或參數（如果已知名稱），以任何使用者的身分行事。
>
>此外，請確定標題、Cookie和請求參數名稱中，您只需設定SSO設定所需的名稱。


>[!NOTE]
>
>單一登入通常與 [LDAP搭配使用](/help/sites-administering/ldap-config.md)。

>[!NOTE]
>
>如果您還將 [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) 與Microsoft Internet Information Server(IIS)一起使用，則需要在以下位置進行其他配置：
>
>* `disp_iis.ini`
>* IIS
>
>
在集 `disp_iis.ini` 合中：
>(如需完 [整的詳細資訊，請參閱安裝Dispatcher with the Microsoft Internet Information Server](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html#microsoft-internet-information-server) )
>
>* `servervariables=1` （將IIS伺服器變數轉發為請求標題至遠端例項）
>* `replaceauthorization=1` (以其「Basic」等值項取代任何名為「Authorization」（授權）以外的標題)
>
>
在IIS中：
>
>* 禁用 **匿名訪問**
   >
   >
* 啟用 **整合的Windows驗證**
>



您可以使用Felix Console的 **Authenticator** （驗證器）選項，查看哪個驗證處理器正套用至內容樹的任何區段；例如：

`http://localhost:4502/system/console/slingauth`

會先查詢最符合路徑的處理常式。 例如，如果您為路徑配置handler-A，為路 `/` 徑配置handler-B `/content`，則請求將首先 `/content/mypage.html` 查詢handler-B。

![screen_shot_2012-02-15at21006pm](assets/screen_shot_2012-02-15at21006pm.png)

### 例如 {#example}

對於Cookie請求(使用URL `http://localhost:4502/libs/wcm/content/siteadmin.html`):

```xml
GET /libs/cq/core/content/welcome.html HTTP/1.1
Host: localhost:4502
Cookie: TestCookie=admin
```

使用下列配置：

* **路徑**: `/`

* **標題名稱**: `TestHeader`

* **Cookie名稱**: `TestCookie`

* **參數名稱**: `TestParameter`

* **ID格式**: `AsIs`

回應是：

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

或者，您可以使用下列curl命令將標題 `TestHeader` 傳送至 `admin:``curl -D - -H "TestHeader: admin" http://localhost:4502/libs/cq/core/content/welcome.html`

>[!NOTE]
>
>在瀏覽器中使用請求參數時，您只會看到部分HTML —— 不含CSS。 這是因為HTML的所有請求都是在沒有請求參數的情況下提出的。

## 移除AEM登出連結 {#removing-aem-sign-out-links}

使用SSO時，登入和登出會在外部處理，因此AEM本身的登出連結不再適用，應該移除。

歡迎畫面上的登出連結可依照下列步驟移除。

1. 覆蓋 `/libs/cq/core/components/welcome/welcome.jsp` 至 `/apps/cq/core/components/welcome/welcome.jsp`
1. 從jsp中刪除以下部件。

   `<a href="#" onclick="signout('<%= request.getContextPath() %>');" class="signout"><%= i18n.get("sign out", "welcome screen") %>`

若要移除右上角使用者個人選單中可用的登出連結，請遵循下列步驟：

1. 覆蓋 `/libs/cq/ui/widgets/source/widgets/UserInfo.js` 至 `/apps/cq/ui/widgets/source/widgets/UserInfo.js`

1. 從檔案中刪除以下部件：

   ```
   menu.addMenuItem({
       "text":CQ.I18n.getMessage("Sign out"),
       "cls": "cq-userinfo-logout",
       "handler": this.logout
   });
   menu.addSeparator();
   ```

