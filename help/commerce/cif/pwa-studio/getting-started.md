---
title: 擴展AEMPWA Studio入門
description: 瞭解如何部署AEM具有PWA Studio的無頭內容和商務項目。
topics: Commerce
feature: Commerce Integration Framework
thumbnail: 37843.jpg
exl-id: de7b8f05-b6b7-4105-84a5-940c16ebf2b4
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---

# 擴展AEMPWA Studio入門 {#getting-started-pwa}

開箱即用後，PWA Studio通過GraphQL與Adobe Commerce無縫整合，為創造創新和吸引人的店面和其他數字型驗提供無限選擇。

內容片段是具有預定義結構的內容片段，它允許以不同格式（例如JSON、Markdown）和獨立呈現的API以無頭方式使用這些內容。 內容片段包括GraphQL所需的所有資料類型和欄位，以確保您的應用程式僅請求可用內容並接收預期內容。 它們在結構方面提供的靈活性使其非常適合在多個地點和多個渠道中使用。

在Adobe Experience Manager的內容片段模型編輯器中，設計所需的結構很容易。 將Adobe Experience Manager內容片段（或任何其他資料）與您的PWA Studio應用程式整合的主要挑戰是從多個GraphQL端點提取資料。 這是因為PWA Studio在開箱即用，可以與單個Adobe CommerceGraphQL端點配合使用。

## 架構 {#architecture}

![PWA無頭架構](/help/commerce/cif/assets/pwa-studio/PWA-Studio_Architecture.png)

## 設定PWA Studio {#setup-pwa}

關注Adobe Commerce [PWA Studio文檔](https://developer.adobe.com/commerce/pwa-studio/tutorials/) 設定PWA Studio應用。

要將PWA Studio與的GraphQL終結點連AEM接，可以使用 [擴AEM展PWA Studio](https://github.com/adobe/aem-pwa-studio-extensions)。

1. 簽出儲存庫

1. 在PWA Studio應用程式中，將擴展添加為開發依賴項。

   ```javascript
   yarn add --dev file:{path-to-extension}/extension
   ```

1. 將阿波羅連結包裝添加到您的PWA Studio應用程式。 在pwa-root/src/index.js中，進行以下更改：

   ```javascript
     import { linkWrapper } from '@adobe/pwa-studio-aem-cfm-blog-extension';
   
   // ...
   
   <Adapter apiBase={apiBase} apollo={{ link: linkWrapper(apolloLink) }} store={store}>
   ```

   您可以在中找到有關Apollo Client自定義項的詳細資訊 [linkWrapper.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/linkWrapper.js)。

1. 要使用部落格條目擴展導航元件，請將以下適應添加到pwa-root/local-intercept.js:

   ```javascript
   const addBlogToNavigation = require('@adobe/pwa-studio-aem-cfm-blog-extension/src/addBlogToNavigation');
   
   function localIntercept(targets) {
       addBlogToNavigation(targets);
   }    
   ```

   您可以在中查找有關自定義導航元件的詳細資訊 [addBlogToNavigation.js](https://github.com/adobe/aem-pwa-studio-extensions/blob/master/aem-cfm-blog-extension/extension/src/addBlogToNavigation.js) 在 [擴展性框架](https://developer.adobe.com/commerce/pwa-studio/guides/general-concepts/extensibility/) PWA Studio。

1. Apollo客戶端將期望AEMGraphQL端點位於 <https://pwa-studio/endpoint.js>。 要將端點映射到此位置，您需要自定義PWA Studio應用程式的UPPROWD配置：a.將AEM_CFM_GRAPHQL變數添加到pwa-root/.env，並將其調整為指向您的內AEM容片段GraphQL終結點。

   示例：AEM_CFM_GRAPHQL=<http://localhost:4503/content/graphql/global>

   b.將代理解析程式添加到OWPRAM配置。 OWPRAMD配置示例可能如下所示：

```json
   response:
     resolver: conditional
     when:
       - matches: request.url.pathname
         pattern: ^/endpoint.json(/|$)
         use: aemProxy
     default: veniaResponse

   aemProxy:
     resolver: proxy
     target: env.AEM_CFM_GRAPHQL
     ignoreSSLErrors: true

   status: response.status
   headers: response.headers
   body: response.body
```

## 設定AEM {#setup-aem}

按照「內AEM容片段」文檔為項目設定GraphQL終AEM點。 此外，在項AEM目中，添加以下配置以允許PWA Studio應用程式訪問GraphQL終結點：

* Adobe花崗岩跨源資源共用策略(com.adobe.granite.cors.impl.CORSPolicyImpl)

   將allowedorigin屬性設定為PWA應用程式的完整主機名。

   範例:  <https://pwa-studio-test-vflyn.local.pwadev:9366>

* Apache Sling引用過濾器(org.apache.sling.security.impl.ReferrerFilter.cfg.json)

   將allow.hosts屬性設定為PWA應用程式的主機名。

   示例：pwa-studio-test-vflyn.local.pwadev

您可以在此處找到兩種配置的完整示例： <https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension/aem/config/src/main/content/jcr_root/apps/blog-demo/config>。

為了展示GraphQL端點，我們通過內容包準備了一些內容片段模型和資料示例。 這些功能與提供PWA Studio擴展的React Components配合使用。

## 使用方式 {#how-to-use}

此擴展被視為一個示例性實現，該示例說明如何將PWA Studio應用程式AEM與連接，以通過GraphQL檢索和呈現內容。

根據您的使用案例，您希望建立自己的自定義內容片段模型，這些模型會生成一個自定義GraphQL架構，然後該架構可由您自己的React元件使用。

生產設定可以在多個方面有所不同。

* 您可以有單個聯合GraphQL終結點，該終結點組合AEM了和Adobe CommerceGraphQL資料，而不是自定義Apollo客戶端。
* 您的PWA Studio應用程式可以AEM直接使用GraphQL終結點URL，而不使用帶有OWPRAMD的代理。 該代理也可以移動到不同的層（例如CDN）。
* 哪種方法最適合您，這還主要取決於您如何將PWA Studio應用程式交付給最終用戶。

這個擴展包含兩個示例。

### 部落格 {#blog}

根據某些內容片段模型顯示部落格帖子。 此外，它還包含如何配置Apollo客戶端以與AEMGraphQL端點一起工作以及如何在PWA Studio中擴展導航元件的示例。 請參閱 [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cfm-blog-extension) 的子菜單。

### PDP富集 {#pdp-enrichment}

使營銷人員能夠方便地使用作為內容片段管理的附加內容來豐富PDP。  請參閱 [GitHub](https://github.com/adobe/aem-pwa-studio-extensions/tree/master/aem-cif-product-page-extension) 的子菜單。
