---
title: 自訂 HTTP 標頭
description: 瞭解如何在Adobe Experience Manager Commerce中設定自訂HTTP標題。
exl-id: 834aadac-c3be-4e7a-a3cb-349608810b40
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 5%

---

# 自訂 HTTP 標頭 {#custom-http-headers}

## 概觀 {#overview}

為了更能掌控其後端，作者可以設定會傳送至商務引擎的自訂HTTP標頭，以及CIF已傳送的標頭。 常見的使用案例包括多商店設定，您可以在其中使用HTTP標頭控制商務後端的回應。

>[!NOTE]
>
>開發人員一律可以使用GraphQL使用者端設定來設定自訂HTTP標頭。
>

## 設定 {#configuration}

為了設定自訂HTTP標頭，首先必須定義它們。 自訂HTTP標頭必須先透過將其新增到以下專案來定義： `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` 使用OSGi設定的服務設定。

您可以在專案的「Cloud Service設定」頁面中設定HTTP標頭的值：

1. 前往「工具 — >Cloud Service-> CIF設定」中的「Cloud Services設定」頁面
1. 開啟現有設定或建立新設定
1. 前往「進階」索引標籤，尋找「自訂HTTP標題」多欄位。 您可以選取先前定義的標頭，並為其指派值。

使用上述雲端服務設定的元件將會隨著每個GraphQL請求傳送這些HTTP標頭。

## 限制 {#restrictions}

雖然此服務可定義任何標頭名稱，包括標準名稱，但無法加以設定。 換言之，您無法使用此功能覆寫標準HTTP標頭。 可以找到受限制的標頭名稱清單 [此處](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers). 除了這些以外，還有兩個標頭無法使用：

* &quot;Store&quot; - CIF用來識別Adobe Commerce存放區
* &quot;Preview-Version&quot; — 由CIF用於擷取分階段產品
