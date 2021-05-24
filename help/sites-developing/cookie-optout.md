---
title: 設定Cookie使用情形
seo-title: 設定Cookie使用情形
description: AEM提供的服務可讓您設定及控制如何在您的網頁中使用cookie
seo-description: AEM提供的服務可讓您設定及控制如何在您的網頁中使用cookie
uuid: 10d95176-0a56-41f1-9d36-01dbdac757d4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 5773ec1a-f15b-462d-8f9f-54ee1d7ead44
exl-id: 42e8d804-6b6a-432e-a651-940b9f45db4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 1%

---

# 設定Cookie使用狀況{#configuring-cookie-usage}

AEM提供的服務可讓您設定及控制如何在您的網頁中使用cookie:

* 可設定的伺服器端服務會維護可使用的Cookie清單。
* Javascript API可讓您的Javascript程式碼驗證是否可使用Cookie。

使用此功能可確保您的頁面符合使用者對Cookie使用方式的同意。

## 配置允許的Cookie {#configuring-allowed-cookies}

設定AdobeGranite選擇退出服務，以指定在您的網頁上使用Cookie的方式。 下表說明了可配置的屬性。

要配置服務，可以使用[Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)或[將OSGi配置添加到儲存庫](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)。 下表說明了任何一種方法所需的屬性。 對於OSGi配置，服務PID為`com.adobe.granite.optout`。

| 屬性名稱（Web主控台） | OSGi屬性名稱 | 說明 |
|---|---|---|
| 退出Cookie | optout.cookies | 當Cookie出現在使用者裝置上時，表示使用者未同意使用Cookie的Cookie名稱。 |
| 退出HTTP標題 | optout.headers | HTTP標題的名稱，在出現時指出使用者未同意使用Cookie。 |
| 白名單Cookie | optout.whitelist.cookies | 對網站運作至關重要且未經使用者同意即可使用的Cookie清單。 |

## 驗證Cookie使用{#validating-cookie-usage}

使用用戶端javascript來呼叫AdobeGranite選擇退出服務，以確認您可以使用Cookie。 使用Granite.OptOutUtil Javascript物件執行下列任一作業：

* 取得Cookie名稱清單，指出該使用者不同意將Cookie用於追蹤用途。
* 取得可使用的Cookie清單。
* 判斷網頁瀏覽器是否包含指出使用者不同意使用Cookie進行追蹤的Cookie。
* 判斷是否可使用特定Cookie。

granite.utils [client library資料夾](/help/sites-developing/clientlibs.md#referencing-client-side-libraries)提供Granite.OptOutUtil物件。 將下列程式碼新增至您的頁面標題JSP，以包含javascript程式庫的連結：

`<ui:includeClientLib categories="granite.utils" />`

例如，下列javascript函式會決定在寫入COOKIE_NAME Cookie之前，是否允許使用COOKIE_NAME Cookie:

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

## Granite.OptOutUtil Javascript物件{#the-granite-optoututil-javascript-object}

Granite.OptOutUtil可讓您判斷是否允許使用Cookie。

### getCookieNames()函式{#getcookienames-function}

傳回Cookie的名稱，若存在，即表示使用者未同意使用Cookie。

**參數**

無.

**傳回**

Cookie名稱的陣列。

#### getWhitelistCookieNames()函式{#getwhitelistcookienames-function}

傳回無論使用者同意為何皆可使用的Cookie名稱。

**參數**

無.

**傳回**

Cookie名稱的陣列。

#### isOptedOut()函式{#isoptedout-function}

判斷使用者的瀏覽器是否包含任何表示尚未同意使用Cookie的Cookie。

**參數**

無.

**傳回**

如果找到未指示同意的Cookie，則布林值為`true`；如果沒有Cookie表示未同意，則布林值為`false`。

### maySetCookie(cookieName)函式{#maysetcookie-cookiename-function}

判斷是否可在使用者的瀏覽器上使用特定Cookie。 此函式等同於使用`isOptedOut`函式，並結合判斷指定的Cookie是否包含在`getWhitelistCookieNames`函式傳回的清單中。

**參數**

* cookieName:字串。 Cookie的名稱。

**傳回**

若可使用`cookieName`，則布林值為`true`，若無法使用`cookieName`，則布林值為`false`。
