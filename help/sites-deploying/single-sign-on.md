---
title: 單一登錄
seo-title: Single Sign On
description: 瞭解如何為實例配置單一登錄(SSO)AEM。
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

# 單一登錄 {#single-sign-on}

單一登錄(SSO)允許用戶在提供一次身份驗證憑據（如用戶名和密碼）後訪問多個系統。 單獨的系統（稱為受信任驗證器）執行該驗證並提供與用戶憑據的Experience Manager。 Experience Manager檢查並強制用戶的訪問權限（即確定允許用戶訪問哪些資源）。

SSO身份驗證處理程式服務( `com.adobe.granite.auth.sso.impl.SsoAuthenticationHandler`)處理受信任驗證器提供的驗證結果。 SSO驗證處理程式將ssid（SSO標識符）作為以下位置中特殊屬性的值按順序搜索：

1. 請求標題
1. Cookie
1. 請求參數

找到值後，將完成搜索並使用此值。

配置以下兩個服務以識別儲存ssid的屬性的名稱：

* 登錄模組。
* SSO身份驗證服務。

必須為兩個服務指定相同的屬性名。 該屬性包含在 `SimpleCredentials` 提供給 `Repository.login`。 屬性的值是無關的和忽略的，僅存在屬性是重要的和經過驗證的。

## 配置SSO {#configuring-sso}

要為實例配AEM置SSO，您需要 [SSO身份驗證處理程式](/help/sites-deploying/osgi-configuration-settings.md#adobegranitessoauthenticationhandler):

1. 使用時，AEM有幾種方法管理此類服務的配置設定；見 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 的子菜單。

   例如，對於NTLM集：

   * **路徑：** 按要求；比如說， `/`
   * **標題名稱**: `LOGON_USER`
   * **ID格式**: `^<DOMAIN>\\(.+)$`

      位置 `<*DOMAIN*>` 替換為您自己的域名。
   對於CoSign:

   * **路徑：** 按要求；比如說， `/`
   * **標題名稱**:遠程用戶
   * **ID格式：** 原樣

   對於SiteMinder:

   * **路徑：** 按要求；比如說， `/`
   * **標題名稱：** SM用戶
   * **ID格式**:原樣



1. 確認單點登錄是否按要求工作；包括授權。

>[!CAUTION]
>
>確保在配置SSO時AEM用戶無法直接訪問。
>
>通過要求用戶通過運行SSO系統代理的Web伺服器，可確保任何用戶都不能直接發送會使用戶受信任的頭、cookie或參數AEM，因為如果從外部發送，代理將過濾此類資訊。
>
>如果知道名稱，AEM則任何可以直接訪問實例而無需通過Web伺服器的用戶都可以通過發送標頭、cookie或參數來充當任何用戶。
>
>另外，確保頭、cookie和請求參數名稱的名稱，您只配置SSO設定所需的名稱。

>[!NOTE]
>
>單一登錄通常與 [LDAP](/help/sites-administering/ldap-config.md)。

>[!NOTE]
>
>如果您還使用 [調度程式](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) 使用MicrosoftInternet Information Server(IIS)，則需要在以下位置進行其他配置：
>
>* `disp_iis.ini`
>* IIS
>
>在 `disp_iis.ini` 設定：
>（請參見） [使用MicrosoftInternet Information Server安裝Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html#microsoft-internet-information-server) 有關完整詳細資訊)
>
>* `servervariables=1` （將IIS伺服器變數作為請求標頭轉發到遠程實例）
>* `replaceauthorization=1` （用「Basic」等效的標題替換「Basic」以外的任何名為「Authorization」的標題）
>
>在IIS中：
>
>* 禁用 **匿名訪問**
>
>* 啟用 **整合Windows驗證**
>


通過使用 **驗證器** Felix Console的選項；例如：

`http://localhost:4502/system/console/slingauth`

首先查詢與路徑最匹配的處理程式。 例如，如果為路徑配置handler-A `/` 路徑和handler-B `/content`，然後請求 `/content/mypage.html` 將首先查詢handler-B。

![screen_shot_2012-02-15at21006pm](assets/screen_shot_2012-02-15at21006pm.png)

### 範例 {#example}

對於Cookie請求（使用URL） `http://localhost:4502/libs/wcm/content/siteadmin.html`):

```xml
GET /libs/cq/core/content/welcome.html HTTP/1.1
Host: localhost:4502
Cookie: TestCookie=admin
```

使用以下配置：

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

如果您請求：
`http://localhost:4502/libs/cq/core/content/welcome.html?TestParameter=admin`

或者，可以使用以下curl命令發送 `TestHeader` 標題 `admin:`
`curl -D - -H "TestHeader: admin" http://localhost:4502/libs/cq/core/content/welcome.html`

>[!NOTE]
>
>在瀏覽器中使用請求參數時，您只能看到某些HTML — 沒有CSS。 這是因為來自HTML的所有請求都是在沒有request參數的情況下發出的。

## 刪除AEM註銷連結 {#removing-aem-sign-out-links}

使用SSO時，外部會處理登錄和註銷，AEM這樣。自己的註銷連結不再適用，應刪除。

可使用以下步驟刪除歡迎螢幕上的註銷連結。

1. 覆蓋 `/libs/cq/core/components/welcome/welcome.jsp` 至 `/apps/cq/core/components/welcome/welcome.jsp`
1. 從jsp中刪除以下部件。

   `<a href="#" onclick="signout('<%= request.getContextPath() %>');" class="signout"><%= i18n.get("sign out", "welcome screen") %>`

要刪除右上角用戶個人菜單中可用的註銷連結，請執行以下步驟：

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
