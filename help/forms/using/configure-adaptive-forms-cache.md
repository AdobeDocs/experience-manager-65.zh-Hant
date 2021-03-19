---
title: 配置自適應表單快取
seo-title: 配置自適應表單快取
description: '最適化表單快取是專為最適化表單和檔案而設計。 它快取最適化表單和最適化檔案，以縮短在用戶端上轉換最適化表單或檔案所需的時間。 '
seo-description: '最適化表單快取是專為最適化表單和檔案而設計。 它快取最適化表單和最適化檔案，以縮短在用戶端上轉換最適化表單或檔案所需的時間。 '
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 0%

---


# 配置自適應表單快取{#configure-adaptive-forms-cache}

快取是縮短資料存取時間、減少延遲並改善輸入／輸出(I/O)速度的機制。 最適化表單快取只儲存最適化表單的HTML內容和JSON結構，而不儲存任何預先填入的資料。 它有助於縮短在用戶端上轉換最適化表單所需的時間。 它專為最適化表單而設計。

## 在作者處配置自適應表單快取和發佈例項{#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. 轉至AEM`https://[server]:[port]/system/console/configMgr`的Web控制台配置管理器。
1. 按一下&#x200B;**[!UICONTROL 自適應表單和互動式通信Web通道配置]**&#x200B;以編輯其配置值。
1. 在[!UICONTROL 編輯配置值]對話框中，在&#x200B;**[!UICONTROL 最適化Forms]**&#x200B;欄位中指定[!DNL Forms]伺服器實例可快取的表單或文檔的最大數量。 預設值為 100。

   >[!NOTE]
   >
   >要禁用快取，請將「Number of AdaptiveForms」（自適應性資料）欄位中的值設定為&#x200B;**0**。 當禁用或更改快取配置時，將重置快取，並從快取中刪除所有表單和文檔。

   ![最適化表單HTML快取的設定對話方塊](assets/cache-configuration-edit.png)

1. 按一下&#x200B;**[!UICONTROL 保存]**&#x200B;保存配置。

您的環境已配置為使用快取自適應表單和相關資產。


## （可選）在Dispatcher {#configure-the-cache}配置自適應表單快取

您也可以在Dispatcher中設定自適應表單快取，以進一步提升效能。

### 先決條件{#pre-requisites}

* 啟用[合併或預填充客戶端的資料選項。 ](prepopulate-adaptive-form-fields.md#prefill-at-client)它有助於合併每個預先填入表單實例的唯一資料。

### 在調度程式{#considerations}上快取自適應表單的注意事項

* 使用最適化表單快取時，請使AEM用[!DNL Dispatcher]快取最適化表單的用戶端程式庫（CSS和JavaScript）。
* 在開發自訂元件時，在用於開發的伺服器上，請停用最適化表單快取。
* 不會快取無副檔名的URL。 例如，會快取模式為pattern`/content/forms/[folder-structure]/[form-name].html`的URL，並忽略模式為`/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`的URL快取。 因此，請搭配使用URL和擴充功能，以充份運用快取功能。
* 本地化最適化表單的考量事項：
   * 使用URL格式`http://host:port/content/forms/af/<afName>.<locale>.html`來請求本地化版本的自適應表單，而非`http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * [針對格式化](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) 的URL停用瀏覽器本 `http://host:port/content/forms/af/<adaptivefName>.html`位。
   * 當您使用URL格式`http://host:port/content/forms/af/<adaptivefName>.html`，且在配置管理器中禁用了「使用瀏覽器語言環境&#x200B;]**」時，將提供自適應表單的非本地化版本。**[!UICONTROL &#x200B;非本地化語言是開發自適應表單時使用的語言。 不會考慮為瀏覽器設定的地區設定（瀏覽器地區設定），而且會提供最適化表單的非本地化版本。
   * 當您使用URL格式`http://host:port/content/forms/af/<adaptivefName>.html`，並且在配置管理器中啟用了「使用瀏覽器區域設定」(Use Browser Locale)時，如果可用，則會提供最適化表單的本地化版本。 ****&#x200B;本地化的最適化表單語言是以您瀏覽器所設定的地區（瀏覽器地區）為基礎。 它只能導致[自適應表單]的第一個實例快取。 若要防止問題在實例上發生，請參閱[疑難排解](#only-first-insatnce-of-adptive-forms-is-cached)。

### 在調度程式中啟用快取

執行下列步驟，以啟用和配置分發程式上的快取自適應表單：

1. 為您環境的每個發佈實例開啟以下URL，並[為您環境的發佈實例啟用刷新代理](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance):
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [將以下內容添加到dispatcher.any檔案中](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#automatically-invalidating-cached-files):

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

   當您新增上述項目時：

   * 最適化表單會保留在快取中，直到未發佈更新的表單版本為止。

   * 當發佈自適應表單中引用的較新版本資源時，受影響的自適應表單會自動失效。 引用資源的自動失效有一些例外。 有關例外的解決方法，請參閱[疑難排解](#troubleshooting)一節。
1. [新增下列rules dispatcher.any或自訂規則檔案](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-documents-to-cache)。它會排除不支援快取的URL。 例如，互動式通訊。

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

您的環AEM境已配置為快取自適應表單。 它會快取所有類型的調適性表單。 如果您需要在傳送快取頁面之前檢查頁面的使用者存取權限，請參閱[快取保護內容](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/permissions-cache.html)。

## 疑難排解 {#troubleshooting}

### 某些包含影像或視頻的自適應表單不會自動從調度器快取中失效{#videos-or-images-not-auto-invalidated}

#### 問題 {#issue1}

當您透過資產瀏覽器選取影像或視訊並新增至最適化表單，而且這些影像和視訊是在資產編輯器中編輯時，包含這些影像的最適化表單不會自動從分派器快取中失效。

#### 解決方案{#Solution1}

發佈影像和視訊後，請明確取消發佈並發佈參照這些資產的最適化表單。

### 僅快取自適應表單的第一個實例{#only-first-instance-of-adaptive-forms-is-cached}

#### 問題 {#issue3}

當最適化表單URL沒有任何本地化資訊，並且在配置管理器中啟用「使用瀏覽器區域設定」(**[!UICONTROL Use Browser Locale]**)時，就會提供最適化表單的本地化版本，並且只會快取並傳送最適化表單的第一個實例給每個後續使用者。

#### 解決方案{#Solution3}

執行下列步驟以解決問題：

1. 開啟conf.d/httpd-dispatcher.conf或任何其他設定檔，設定為在執行時期載入。

1. 將下列程式碼新增至您的檔案並儲存。 它是一個范常式式碼，可依您的環境加以修改。

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
