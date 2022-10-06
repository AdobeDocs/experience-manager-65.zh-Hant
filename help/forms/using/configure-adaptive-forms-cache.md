---
title: 設定最適化表單快取
seo-title: Configure adaptive forms cache
description: 最適化表單快取是專為最適化表單和檔案而設計。 它快取最適化表單和最適化檔案，以縮短在用戶端上轉譯最適化表單或檔案所需的時間。
seo-description: The adaptive forms cache is designed specifically for adaptive forms and documents. It caches adaptive forms and adaptive documents with the objective of reducing the time required to render an adaptive form or document on the client.
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
role: Admin
exl-id: 153986f0-b6ff-4278-8bb6-70c320a4e539
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 1%

---

# 設定最適化表單快取 {#configure-adaptive-forms-cache}

快取是一種縮短資料存取時間、減少延遲並改善輸入/輸出(I/O)速度的機制。 適用性表單快取僅儲存適用性表單的HTML內容和JSON結構，而不儲存任何預先填入的資料。 有助於縮短在用戶端上轉譯最適化表單所需的時間。 專為最適化表單而設計。

## 在製作和發佈例項時設定最適化表單快取 {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. 前往AEM Web主控台組態管理器，網址為 `https://[server]:[port]/system/console/configMgr`.
1. 按一下 **[!UICONTROL 最適化表單與互動式通訊Web通道設定]** 來編輯其配置值。
1. 在 [!UICONTROL 編輯配置值] 對話框，指定AEM實例的表單或文檔數上限 [!DNL Forms] 伺服器可在 **[!UICONTROL 適用性Forms數]** 欄位。 預設值為 100。

   >[!NOTE]
   >
   >若要停用快取，請將「適用性Forms數」欄位中的值設為 **0**. 當禁用或更改快取配置時，將重置快取，並從快取中刪除所有表單和文檔。

   ![適用性表單HTML快取的設定對話方塊](assets/cache-configuration-edit.png)

1. 按一下 **[!UICONTROL 儲存]** 以儲存設定。

您的環境已設定為使用快取最適化表單和相關資產。


## （選用）在Dispatcher設定最適化表單快取 {#configure-the-cache}

您也可以在Dispatcher設定最適化表單快取，以提升效能。

### 先決條件 {#pre-requisites}

* 啟用 [在客戶端合併或預填資料](prepopulate-adaptive-form-fields.md#prefill-at-client) 選項。 有助於合併預填表單中每個例項的唯一資料。

### 在Dispatcher上快取最適化表單的考量事項 {#considerations}

* 使用最適化表單快取時，請使用AEM [!DNL Dispatcher] 快取最適化表單的用戶端程式庫（CSS和JavaScript）。
* 開發自訂元件時，請在用於開發的伺服器上，停用最適化表單快取。
* 不會快取沒有副檔名的URL。 例如，具有模式的URL`/content/forms/[folder-structure]/[form-name].html` 會快取，而快取會忽略具有模式的URL `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. 因此，請使用具有擴充功能的URL，善用快取功能。
* 本地化適用性表單的考量事項：
   * 使用URL格式 `http://host:port/content/forms/af/<afName>.<locale>.html` 要求本地化版本的最適化表單，而非 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * [使用瀏覽器區域設定停用](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) 格式的URL `http://host:port/content/forms/af/<adaptivefName>.html`.
   * 使用URL格式時 `http://host:port/content/forms/af/<adaptivefName>.html`，和 **[!UICONTROL 使用瀏覽器地區]** 在「設定管理器」中，會停用非本地化版本的最適化表單。 非本地化語言是開發最適化表單時使用的語言。 未考慮為瀏覽器設定的地區設定（瀏覽器地區設定），且會提供最適化表單的非本地化版本。
   * 使用URL格式時 `http://host:port/content/forms/af/<adaptivefName>.html`，和 **[!UICONTROL 使用瀏覽器地區]** 在「設定管理器」中啟用時，會提供適用性表單的本地化版本（如果有）。 本地化最適化表單的語言是以為瀏覽器設定的地區（瀏覽器地區）為基礎。 這會導致 [僅快取最適化表單的第一個例項]. 若要防止問題在您的執行個體上發生，請參閱 [疑難排解](#only-first-insatnce-of-adptive-forms-is-cached).

### 在Dispatcher啟用快取

執行下列步驟，在Dispatcher上啟用和設定快取最適化表單：

1. 為您環境的每個發佈例項開啟下列URL，並 [為您的環境的發佈實例啟用刷新代理](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance):
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [將下列內容新增至您的dispatcher.any檔案](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#automatically-invalidating-cached-files):

   ```JSON
      /invalidate
      {
      /0000
      {
      /glob "*"
      /type "deny"
      }
      /0001
      {
      # Consider all HTML files stale after an activation.
      /glob "*.html"
      /type "allow"
      }
      /0002
      {
      # Exclude htmls present in AF directories
      /glob "/content/forms/**/*.html"
      /type "deny"
      }
   ```

   新增上述項目時：

   * 最適化表單會保留在快取中，直到未發佈更新後的表單版本為止。

   * 發佈最適化表單中參考的較新版本資源時，受影響的最適化表單會自動失效。 引用資源的自動失效有一些例外。 有關例外的解決方法，請參閱 [疑難排解](#troubleshooting) 區段。
1. [新增下列rules dispatcher.any或自訂規則檔案](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-documents-to-cache). 它會排除不支援快取的URL。 例如，互動式通訊。

   ```JSON
      /0000 {
            /glob "*"
            /type "allow"
      }
      ## Don't cache csrf login tokens
      /0001 {
            /glob "/libs/granite/csrf/token.json"
            /type "deny"
      }
      ## Don't cache IC - print channel
      /0002 {
            /glob "/content/forms/**/channels/print.html"
            /type "deny"
      }
      ## Don't cache IC - web channel
      /0003 {
            /glob "/content/forms/**/channels/web.html"
            /type "deny"
      }
   ```

1. [將下列參數新增至忽略URL參數清單](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#ignoring-url-parameters):

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

您的AEM環境已設定為快取最適化表單。 它會快取所有類型的最適化表單。 如果您需要在傳送快取頁面之前檢查頁面的使用者存取權限，請參閱 [快取安全內容](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/permissions-cache.html).

## 疑難排解 {#troubleshooting}

### 某些包含影像或視訊的最適化表單不會從Dispatcher快取中自動失效 {#videos-or-images-not-auto-invalidated}

#### 問題 {#issue1}

當您透過資產瀏覽器選取影像或影片並新增至最適化表單，且這些影像和影片在資產編輯器中編輯時，包含這些影像的最適化表單不會自動從Dispatcher快取中失效。

#### 解決方案 {#Solution1}

發佈影像和影片後，請明確取消發佈並發佈參考這些資產的最適化表單。

### 系統只會快取最適化表單的第一個例項 {#only-first-instance-of-adaptive-forms-is-cached}

#### 問題 {#issue3}

當適用性表單URL沒有任何本地化資訊時，以及 **[!UICONTROL 使用瀏覽器地區]** 在「設定管理器」中，會提供適用性表單的本地化版本，且系統只會快取最適化表單的第一個例項，並傳送給後續的每位使用者。

#### 解決方案 {#Solution3}

執行下列步驟以解決問題：

1. 開啟「conf.d/httpd-dispatcher.conf」或任何其他設定檔案，這些設定檔設定為在執行階段載入。

1. 將下列程式碼新增至您的檔案並儲存。 此范常式式碼會加以修改，以符合您的環境。

```XML
   <VirtualHost *:80>
        # Set log level high during development / debugging and then turn it down to whatever is appropriate
    LogLevel rewrite:trace6
        # Start Rewrite Engine
    RewriteEngine On
        # Handle actual URL convention (just pass through)
        RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
 
        # Handle selector based redirection basded on browser language
        # The Rewrite Cond(ition) is looking for the Accept-Lanague header and if found takes the first two character which most likely will be the desired language selector.
        RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
        RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
   </VirtualHost>
```
