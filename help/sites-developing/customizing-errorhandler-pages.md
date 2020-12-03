---
title: 自訂錯誤處理常式所顯示的頁面
seo-title: 自訂錯誤處理常式所顯示的頁面
description: AEM隨附標準錯誤處理常式，可處理HTTP錯誤
seo-description: AEM隨附標準錯誤處理常式，可處理HTTP錯誤
uuid: aaf940fd-e428-4c7c-af7f-88b1d02c17c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 63c94c82-ed96-4d10-b645-227fa3c09f4b
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---


# 自訂錯誤處理常式{#customizing-pages-shown-by-the-error-handler}所顯示的頁面

AEM隨附標準錯誤處理常式，可處理HTTP錯誤；例如，顯示：

![chlimage_1-67](assets/chlimage_1-67a.png)

系統提供的指令碼存在（在`/libs/sling/servlet/errorhandler`下）以響應錯誤代碼，預設情況下，標準CQ實例可使用以下指令碼：

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEM是以Apache Sling為基礎，因此請參閱[https://sling.apache.org/site/errorhandling.html](https://sling.apache.org/site/errorhandling.html)以取得Sling Error Handling的詳細資訊。

>[!NOTE]
>
>在作者實例上，預設會啟用[CQ WCM除錯篩選器](/help/sites-deploying/osgi-configuration-settings.md)。 這一律會產生回應代碼200。 預設錯誤處理程式通過將完整堆棧跟蹤寫入響應來響應。
>
>在發佈例項上，CQ WCM除錯篩選器會一律停用&#x200B;**（即使設定為已啟用）。

## 如何自訂錯誤處理常式{#how-to-customize-pages-shown-by-the-error-handler}所顯示的頁面

您可以開發自己的指令碼，以自訂在遇到錯誤時由錯誤處理常式顯示的頁面。 您的自訂頁面將建立在`/apps`下，並覆蓋預設頁面（位於`/libs`下）。

>[!NOTE]
>
>如需詳細資訊，請參閱[使用覆蓋](/help/sites-developing/overlays.md)。

1. 在儲存庫中，複製預設指令碼：

   * 從 `/libs/sling/servlet/errorhandler/`
   * 至 `/apps/sling/servlet/errorhandler/`

   由於目標路徑預設不存在，因此首次執行此操作時需要建立該路徑。

1. 導航到 `/apps/sling/servlet/errorhandler`. 您可以在這裡：

   * 編輯適當的現有指令碼，以提供所需的資訊。
   * 建立和編輯所需程式碼的新指令碼。

1. 儲存變更並進行測試。

>[!CAUTION]
>
>404.jsp和403.jsp處理常式是專為配合CQ5驗證而設計；尤其是允許在發生這些錯誤時進行系統登錄。
>
>因此，更換這兩個操縱員應該非常謹慎。

### 自定義對HTTP 500錯誤的響應{#customizing-the-response-to-http-errors}

HTTP 500錯誤是由伺服器端例外所造成。

* **[500內部伺服](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**
器錯誤伺服器遇到意外狀況，無法完成要求。

當請求處理結果產生例外時，Apache Sling架構（此AEM是內建的）:

* 記錄異常
* 傳回：

   * HTTP回應碼500
   * 異常堆棧跟蹤

   在回應本體中。

通過[自定義錯誤處理程式](#how-to-customize-pages-shown-by-the-error-handler)顯示的頁，可以建立`500.jsp`指令碼。 但是，只有在明確執行`HttpServletResponse.sendError(500)`時才使用；例如從例外捕手那裡。

否則，響應代碼設定為500，但不執行`500.jsp`指令碼。

要處理500個錯誤，錯誤處理程式指令碼的檔案名必須與異常類（或超類）相同。 要處理所有此類異常，可以建立指令碼`/apps/sling/servlet/errorhandler/Throwable.js`p或`/apps/sling/servlet/errorhandler/Exception.jsp`。

>[!CAUTION]
>
>在作者實例上，預設會啟用[CQ WCM除錯篩選器](/help/sites-deploying/osgi-configuration-settings.md)。 這一律會產生回應代碼200。 預設錯誤處理程式通過將完整堆棧跟蹤寫入響應來響應。
>
>對於自訂錯誤處理常式，需要代碼為500的回應——因此[CQ WCM除錯篩選必須停用](/help/sites-deploying/osgi-configuration-settings.md)。 這可確保傳回回回應程式碼500，這會反過來觸發正確的Sling錯誤處理常式。
>
>在發佈例項上，CQ WCM除錯篩選器會一律停用&#x200B;**（即使設定為已啟用）。

