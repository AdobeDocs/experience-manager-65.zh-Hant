---
title: 自訂由錯誤處理常式顯示的頁面
seo-title: Customizing Pages shown by the Error Handler
description: AEM隨附處理HTTP錯誤的標準錯誤處理常式
seo-description: AEM comes with a standard error handler for handling HTTP errors
uuid: aaf940fd-e428-4c7c-af7f-88b1d02c17c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 63c94c82-ed96-4d10-b645-227fa3c09f4b
exl-id: d6745baa-44da-45dd-b5d5-a9b218e7e8cf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 2%

---

# 自訂由錯誤處理常式顯示的頁面{#customizing-pages-shown-by-the-error-handler}

AEM隨附處理HTTP錯誤的標準錯誤處理常式；例如，透過顯示：

![chlimage_1-67](assets/chlimage_1-67a.png)

系統提供的指令碼存在(在 `/libs/sling/servlet/errorhandler`)以回應錯誤碼，標準CQ例項預設會提供下列項目：

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEM以Apache Sling為基礎，請參閱 [https://sling.apache.org/site/errorhandling.html](https://sling.apache.org/site/errorhandling.html) 以取得Sling錯誤處理的詳細資訊。

>[!NOTE]
>
>在作者例項上， [CQ WCM除錯篩選器](/help/sites-deploying/osgi-configuration-settings.md) 預設為啟用。 這一律會導致回應代碼200。 預設錯誤處理程式通過將完整堆棧跟蹤寫入響應來響應。
>
>在發佈例項上，CQ WCM除錯篩選器為 *always* 已停用（即使已設為啟用）。

## 如何自訂由錯誤處理常式顯示的頁面 {#how-to-customize-pages-shown-by-the-error-handler}

您可以開發自己的指令碼，以在發生錯誤時自訂錯誤處理常式顯示的頁面。 您的自訂頁面將在 `/apps` 並覆蓋預設頁面(位於 `/libs`)。

>[!NOTE]
>
>請參閱 [使用覆蓋](/help/sites-developing/overlays.md) 以取得更多詳細資訊。

1. 在存放庫中，複製預設指令碼：

   * 從 `/libs/sling/servlet/errorhandler/`
   * 至 `/apps/sling/servlet/errorhandler/`

   由於目的地路徑預設不存在，因此您首次執行此動作時需要建立它。

1. 導覽至 `/apps/sling/servlet/errorhandler`。您可以在此處：

   * 編輯適當的現有指令碼以提供所需資訊。
   * 建立和編輯所需代碼的新指令碼。

1. 儲存變更並測試。

>[!CAUTION]
>
>404.jsp和403.jsp處理常式經過專門設計，以滿足CQ5驗證；尤其是，允許在發生這些錯誤時進行系統登入。
>
>因此，應該非常謹慎地替換這兩個處理程式。

### 自訂對HTTP 500錯誤的回應 {#customizing-the-response-to-http-errors}

HTTP 500錯誤是由伺服器端例外所造成。

* **[500內部伺服器錯誤](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**
伺服器遇到非預期的條件，使其無法履行請求。

當請求處理導致例外時，Apache Sling架構(AEM建置於上):

* 記錄例外狀況
* 傳回：

   * HTTP回應代碼500
   * 異常堆棧跟蹤

   在回應的正文中。

依據 [自訂錯誤處理常式顯示的頁面](#how-to-customize-pages-shown-by-the-error-handler) a `500.jsp` 可建立指令碼。 不過，只有在 `HttpServletResponse.sendError(500)` 會明確執行；例如從例外捕手那裡。

否則，回應代碼會設為500，但 `500.jsp` 指令碼未執行。

要處理500錯誤，錯誤處理程式指令碼的檔案名必須與異常類（或超類）相同。 要處理所有此類例外，可以建立指令碼 `/apps/sling/servlet/errorhandler/Throwable.js`p或 `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!CAUTION]
>
>在作者例項上， [CQ WCM除錯篩選器](/help/sites-deploying/osgi-configuration-settings.md) 預設為啟用。 這一律會導致回應代碼200。 預設錯誤處理程式通過將完整堆棧跟蹤寫入響應來響應。
>
>若為自訂錯誤處理常式，則需要程式碼為500的回應，因此 [必須停用CQ WCM除錯篩選](/help/sites-deploying/osgi-configuration-settings.md). 這可確保傳回回應代碼500，進而觸發正確的Sling錯誤處理常式。
>
>在發佈例項上，CQ WCM除錯篩選器為 *always* 已停用（即使已設為啟用）。
