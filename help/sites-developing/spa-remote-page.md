---
title: RemotePage元件
description: RemotePage元件是用於編輯遠程React的自定義頁面組SPA件AEM。
exl-id: 3f015997-0d42-4241-a890-0f16a19c5e34
translation-type: tm+mt
source-git-commit: a92358d187aa78e05dd9b5a7bd4ae14bf0972f62
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# RemotePage元件{#remote-page-component}

在決定您要在外部和之間進行何種SPA整AEM合時，您通常需要能夠在中檢視和編SPA輯AEM。 RemotePage元件是專門用於此目的的自定義頁面元件。

## 概覽 {#overview}

RemotePage元件從應用程式生成的`asset-manifest.json`中提取所有必要的資產，並使用它來呈現SPA內AEM。

* RemotePage允許您在Page元件主體中插入SPA指令碼和樣AEM式表。
* 虛擬前端元件允許在編輯器中將節標籤為可AEM編SPA輯。
* 搭配使用，SPA可讓位於不同網域的代管網域在AEM中編輯。

有關可編輯、外部的詳細資訊，請參SPA閱AEM[在](spa-edit-external.md)中編輯外部的SPA文AEM章。

## 要求{#requirements}

* 讓CORS可進行開發
* 在頁面屬性中設定遠端URL
* 在中SPA演算AEM
* Web應用程式必須使用Bundler資產資訊清單，如下列其中一項，並在網域根目錄中公開asset-manifest.json檔案，其中會列出要載入的所有CSS和JS檔案：
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest

   ![入口點](assets/asset-manifest-entrypoints.png)

* 應用程式必須能夠在主體元素下方的`<div id="root"></div>`中初始化。 如果應用程式需要不同的標籤來執行個體化，則必須在具有`sling:resourceSuperType="spa-project-core/components/remotepage`的proxy元件的HTL指令碼中相應調整。

## 限制 {#limitations}

* RemotePage元件的當前實施僅支援遠程React應用程式。
* 在中執行遠端演算時，無法使用應用程式根HTML檔案中定義的內部CSS以及根DOM節點上的內嵌CSSAEM。

## 技術詳細資訊{#technical-details}

與項目的其餘部AEM分SPA一樣，RemotePage元件是開源的。 有關RemotePage元件的完整技術詳細資訊，請參見GitHub儲存庫。](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)[
