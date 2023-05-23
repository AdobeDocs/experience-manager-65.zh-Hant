---
title: 配置Cookie使用
seo-title: Configuring Cookie Usage
description: 提AEM供一項服務，使您能夠配置和控制Cookie與網頁的使用方式
seo-description: AEM provides a service that enables you to configure and control how cookies are used with your web pages
uuid: 10d95176-0a56-41f1-9d36-01dbdac757d4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 5773ec1a-f15b-462d-8f9f-54ee1d7ead44
exl-id: 42e8d804-6b6a-432e-a651-940b9f45db4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---

# 配置Cookie使用{#configuring-cookie-usage}

提AEM供一種服務，使您能夠配置和控制Cookie與網頁的使用方式：

* 可配置的伺服器端服務維護可使用的Cookie清單。
* Javascript API使您的Javascript代碼能夠驗證是否可以使用Cookie。

使用此功能可確保您的頁面符合用戶對cookie使用的同意。

## 配置允許的Cookie {#configuring-allowed-cookies}

配置AdobeGranite Opt-Out服務以指定Cookie在網頁上的使用方式。 下表介紹了可配置的屬性。

要配置服務，可以使用 [Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 或 [將OSGi配置添加到儲存庫](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)。 下表說明了您對任一方法所需的屬性。 對於OSGi配置，服務PID為 `com.adobe.granite.optout`。

| 屬性名稱（Web控制台） | OSGi屬性名稱 | 說明 |
|---|---|---|
| 選擇退出Cookie | optout.cookies | 當用戶設備上存在表示用戶未同意使用cookie的cookie的名稱。 |
| 選擇退出HTTP標頭 | optout.headers | HTTP標頭的名稱，當存在時，它指示用戶未同意使用cookie。 |
| 白名單Cookie | optout.whitelist.cookies | 對網站的功能至關重要的Cookie清單，在未經用戶同意的情況下可以使用。 |

## 驗證Cookie用法 {#validating-cookie-usage}

使用客戶端javascript調用AdobeGranite Opt-Out服務，以驗證是否可以使用cookie。 使用Granite.OptOutUtiljavascript對象執行以下任一任務：

* 獲取表示用戶不同意使用cookie進行跟蹤的cookie名稱清單。
* 獲取可使用的Cookie清單。
* 確定Web瀏覽器是否包含表示用戶不同意使用Cookie進行跟蹤的Cookie。
* 確定是否可以使用特定的cookie。

花崗岩.utils [客戶端庫資料夾](/help/sites-developing/clientlibs.md#referencing-client-side-libraries) 提供了Granite.OptOutUtil對象。 將以下代碼添加到頁面頭JSP中，以包括到javascript庫的連結：

`<ui:includeClientLib categories="granite.utils" />`

例如，以下javascript函式確定在寫入COOKIE_NAME cookie之前是否允許使用它：

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

## Granite.OptOutUtil Javascript對象 {#the-granite-optoututil-javascript-object}

Granite.OptOutUtil使您能夠確定是否允許使用cookie。

### getCookieNames()函式 {#getcookienames-function}

返回當存在時表示用戶未同意使用cookie的cookie的名稱。

**參數**

無。

**返回**

一組cookie名稱。

#### getWhitelistCookieNames()函式 {#getwhitelistcookienames-function}

返回可以使用的Cookie的名稱，無論用戶是否同意。

**參數**

無。

**返回**

一組cookie名稱。

#### isOpingOut()函式 {#isoptedout-function}

確定用戶的瀏覽器是否包含任何表示尚未同意使用cookie的cookie。

**參數**

無。

**返回**

布爾值 `true` 如果找到表示未同意的cookie，並且 `false` 如果沒有cookie表示未同意。

### maySetCookie(cookieName)函式 {#maysetcookie-cookiename-function}

確定是否可以在用戶的瀏覽器上使用特定的cookie。 此函式等效於使用 `isOptedOut` 與確定給定cookie是否包括在 `getWhitelistCookieNames` 函式返回。

**參數**

* cookie名稱：字串。 Cookie的名稱。

**返回**

布爾值 `true` 如果 `cookieName` 可以使用，或 `false` 如果 `cookieName` 無法使用。
