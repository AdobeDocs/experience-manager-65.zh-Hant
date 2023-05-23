---
title: 自定義錯誤處理程式顯示的頁
seo-title: Customizing Pages shown by the Error Handler
description: 帶AEM有處理HTTP錯誤的標準錯誤處理程式
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

# 自定義錯誤處理程式顯示的頁{#customizing-pages-shown-by-the-error-handler}

帶AEM有處理HTTP錯誤的標準錯誤處理程式；例如，通過顯示：

![chlimage_1-67](assets/chlimage_1-67a.png)

系統提供的指令碼存在(在 `/libs/sling/servlet/errorhandler`)響應錯誤代碼，預設情況下，標準CQ實例提供以下內容：

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEM基於Apache Sling，請參閱 [https://sling.apache.org/site/errorhandling.html](https://sling.apache.org/site/errorhandling.html) 有關Sling錯誤處理的詳細資訊。

>[!NOTE]
>
>在作者案中， [CQ WCM調試篩選器](/help/sites-deploying/osgi-configuration-settings.md) 預設情況下啟用。 這始終導致響應代碼200。 預設錯誤處理程式通過將完整堆棧跟蹤寫入響應來響應。
>
>在發佈實例上，CQ WCM調試篩選器為 *總是* 已禁用（即使配置為已啟用）。

## 如何自定義錯誤處理程式顯示的頁 {#how-to-customize-pages-shown-by-the-error-handler}

您可以開發自己的指令碼，以便在遇到錯誤時自定義錯誤處理程式顯示的頁。 將在下面建立您的自定義頁面 `/apps` 並覆蓋預設頁面(位於 `/libs`)。

>[!NOTE]
>
>請參閱 [使用疊加](/help/sites-developing/overlays.md) 的子菜單。

1. 在儲存庫中，複製預設指令碼：

   * 從 `/libs/sling/servlet/errorhandler/`
   * 至 `/apps/sling/servlet/errorhandler/`

   由於預設情況下目標路徑不存在，因此在首次執行此操作時需要建立它。

1. 導覽至 `/apps/sling/servlet/errorhandler`。在此，您可以：

   * 編輯相應的現有指令碼以提供所需的資訊。
   * 建立和編輯所需代碼的新指令碼。

1. 保存更改和test。

>[!CAUTION]
>
>404.jsp和403.jsp處理程式是專門設計用於滿足CQ5驗證的；特別是，在出現這些錯誤時允許系統登錄。
>
>因此，更換這兩個操縱員應十分謹慎。

### 自定義對HTTP 500錯誤的響應 {#customizing-the-response-to-http-errors}

HTTP 500錯誤是由伺服器端異常引起的。

* **[500內部伺服器錯誤](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**
伺服器遇到意外情況，無法完成請求。

當請求處理導致異常時，Apache Sling框架(基於AEM此框架構建):

* 記錄異常
* 返回：

   * HTTP響應代碼500
   * 異常堆棧跟蹤

   在反應體中。

按 [自定義錯誤處理程式顯示的頁](#how-to-customize-pages-shown-by-the-error-handler) a `500.jsp` 可以建立指令碼。 但是，僅當 `HttpServletResponse.sendError(500)` 明確執行；也就是從例外捕手那裡。

否則，響應代碼設定為500，但 `500.jsp` 指令碼未執行。

要處理500個錯誤，錯誤處理程式指令碼的檔案名必須與異常類（或超類）相同。 要處理所有此類異常，可以建立指令碼 `/apps/sling/servlet/errorhandler/Throwable.js`p或 `/apps/sling/servlet/errorhandler/Exception.jsp`。

>[!CAUTION]
>
>在作者案中， [CQ WCM調試篩選器](/help/sites-deploying/osgi-configuration-settings.md) 預設情況下啟用。 這始終導致響應代碼200。 預設錯誤處理程式通過將完整堆棧跟蹤寫入響應來響應。
>
>對於自定義錯誤處理程式，需要代碼為500的響應 — 因此 [需要禁用CQ WCM調試篩選器](/help/sites-deploying/osgi-configuration-settings.md)。 這確保返迴響應代碼500，這反過來觸發正確的Sling錯誤處理程式。
>
>在發佈實例上，CQ WCM調試篩選器為 *總是* 已禁用（即使配置為已啟用）。
