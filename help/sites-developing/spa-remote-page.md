---
title: RemotePage元件
description: RemotePage元件是用於編輯遠程React的自定義頁面組SPA件AEM。
translation-type: tm+mt
source-git-commit: 431bed450ed5b0239d9191dcf061f01e64b8981a
workflow-type: tm+mt
source-wordcount: '261'
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

## 限制 {#limitations}

* RemotePage元件的當前實施僅支援遠程React應用程式。
* 在中執行遠端演算時，無法使用應用程式根HTML檔案中定義的內部CSS以及根DOM節點上的內嵌CSSAEM。

## 技術詳細資訊{#technical-details}

與項目的其餘部AEM分SPA一樣，RemotePage元件是開源的。 有關RemotePage元件的完整技術詳細資訊，請參見GitHub儲存庫。](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)[
