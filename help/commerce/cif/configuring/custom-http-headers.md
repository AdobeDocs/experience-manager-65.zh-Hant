---
title: 自訂 HTTP 標頭
description: 配置自定義HTTP標頭
exl-id: 834aadac-c3be-4e7a-a3cb-349608810b40
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 5%

---

# 自訂 HTTP 標頭 {#custom-http-headers}

## 概觀 {#overview}

為了獲得對其後端的更多控制，作者可以配置將發送到商務引擎的自定義HTTP報頭以及CIF已發送的報頭。 常見使用案例包括多儲存設定，在這些設定中，您可以使用HTTP標頭來控制商務後端的響應。

>[!NOTE]
>
>開發人員始終可以使用GraphQL客戶端配置配置自定義HTTP標頭。

## 設定 {#configuration}

要配置自定義HTTP標頭，必須先定義它們。 必須先將自定義HTTP標頭添加到 `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` 使用OSGi配置進行服務配置。

可以在項目的「Cloud Service配置」頁中配置HTTP標頭的值：

1. 轉至「工具」 — >「Cloud Service」 — >「CIF配置」中的「Cloud Services配置」頁
1. 開啟現有配置或建立新配置
1. 轉到「高級」頁籤並查找「自定義HTTP標頭」多欄位。 您可以選擇先前定義的題頭，並為其分配值。

使用上述雲服務配置的元件將隨每個GraphQL請求發送這些HTTP頭。

## 限制 {#restrictions}

雖然該服務允許定義任何標頭名稱，包括標準標頭名稱，但它們將不可用於配置。 換句話說，不能使用此功能覆蓋標準HTTP標頭。 可以找到受限制的標題名稱清單 [這裡](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)。 除了這些標題外，還有兩個無法使用的標題：

* 「商店」 — CIF用於識別Adobe Commerce商店
* &quot;預覽版&quot;- CIF用於檢索已提貨產品
