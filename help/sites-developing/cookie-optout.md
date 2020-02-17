---
title: 設定Cookie使用情形
seo-title: 設定Cookie使用情形
description: AEM提供一項服務，可讓您設定並控制Cookie與網頁的使用方式
seo-description: AEM提供一項服務，可讓您設定並控制Cookie與網頁的使用方式
uuid: 10d95176-0a56-41f1-9d36-01dbdac757d4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 5773ec1a-f15b-462d-8f9f-54ee1d7ead44
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 設定Cookie使用情形{#configuring-cookie-usage}

AEM提供一項服務，可讓您設定並控制Cookie與網頁的使用方式：

* 可配置的伺服器端服務會維護可使用的Cookie清單。
* Javascript API可讓您的Javascript程式碼驗證Cookie是否可使用。

使用此功能可確保您的頁面符合使用者對Cookie使用的同意。

## 設定允許的Cookie {#configuring-allowed-cookies}

設定Adobe Granite選擇退出服務，以指定Cookie在您的網頁上的使用方式。 下表說明了可以配置的屬性。

要配置服務，可以使用 [Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) , [或將OSGi配置添加到儲存庫](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)。 下表說明了這兩種方法所需的屬性。 對於OSGi配置，服務PID為 `com.adobe.granite.optout`。

| 屬性名稱（Web控制台） | OSGi屬性名稱 | 說明 |
|---|---|---|
| 退出Cookie | optout.cookies | 當Cookie出現在使用者裝置上時，表示使用者未同意使用Cookie的Cookie名稱。 |
| 選擇退出HTTP標題 | optout.headers | HTTP標題的名稱，指出使用者尚未同意使用Cookie。 |
| 白名單Cookie | optout.whitelist.cookies | 對網站運作至關重要且未經使用者同意即可使用的Cookie清單。 |

## 驗證Cookie使用情形 {#validating-cookie-usage}

使用用戶端javascript呼叫Adobe Granite退出服務，以確認您可以使用Cookie。 使用Granite.OptOutUtil javascript物件來執行下列任何工作：

* 取得Cookie名稱清單，指出該使用者不同意使用Cookie進行追蹤。
* 取得可使用的Cookie清單。
* 判斷網頁瀏覽器是否包含Cookie，指出使用者不同意使用Cookie進行追蹤。
* 判斷是否可使用特定Cookie。

granite.utils用戶端 [程式庫資料夾](/help/sites-developing/clientlibs.md#referencing-client-side-libraries) ，提供Granite.OptOutUtil物件。 將下列程式碼新增至您的頁面標題JSP，以包含javascript程式庫的連結：

`<ui:includeClientLib categories="granite.utils" />`

例如，下列javascript函式會決定在寫入COOKIE之前是否允許使用COOKIE_NAME Cookie:

```
function writeCookie(value){
   if (!Granite.OptOutUtil.maySetCookie("COOKIE_NAME"))
      return;
   if (value) {
      value = encodeURIComponent(value);
      document.cookie = "COOKIE_NAME=" + value;
   }
}
```

## Granite.OptOutUtil Javascript物件 {#the-granite-optoututil-javascript-object}

Granite.OptOutUtil可讓您判斷是否允許使用Cookie。

### getCookieNames()函式 {#getcookienames-function}

傳回Cookie的名稱，當Cookie存在時，表示使用者未同意使用Cookie。

**參數**

無.

**退貨**

Cookie名稱的陣列。

#### getWhitelistCookieNames()函式 {#getwhitelistcookienames-function}

傳回不論使用者同意與否，都可使用的Cookie名稱。

**參數**

無.

**退貨**

Cookie名稱的陣列。

#### isOptedOut()函式 {#isoptedout-function}

判斷使用者的瀏覽器是否包含任何表示未同意使用Cookie的Cookie。

**參數**

無.

**退貨**

布爾值：如果 `true` 發現Cookie表示未同意，則為此值；若未發現Cookie表示 `false` 未同意，則為此值。

### maySetCookie(cookieName)函式 {#maysetcookie-cookiename-function}

判斷特定Cookie是否可用於使用者的瀏覽器。 此函式等同於搭配使用 `isOptedOut` 函式，以判斷函式傳回的清單中是否包含指定 `getWhitelsitCookieNames` 的Cookie。

**參數**

* cookieName:字串。 Cookie的名稱。

**退貨**

布爾值if `true` 可 `cookieName` 以使用，值 `false` if不 `cookieName` 能使用。
