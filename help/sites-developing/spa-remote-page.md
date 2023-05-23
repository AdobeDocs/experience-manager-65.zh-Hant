---
title: RemotePage 元件
description: RemotePage元件是一個自定義頁面元件，用於編輯遠程SPAReact在AEM中。
exl-id: 3f015997-0d42-4241-a890-0f16a19c5e34
source-git-commit: 41aac3b4ea3b100e9d927bef161929477d667a95
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 2%

---

# RemotePage 元件 {#remote-page-component}

在確定您希望在外部和之間進行何種級SPA別的集AEM成時，通常可以清楚地看到您需要能夠查看和編輯SPA內部AEM。 RemotePage元件是僅用於此目的的自定義頁面元件。

## 概觀 {#overview}

RemotePage元件從應用程式生成的所有必需資產中提取 `asset-manifest.json` 並用於在中SPA顯示AEM。

* RemotePage允許您在Page元件的正文中SPA插入指令碼和樣AEM式表。
* 虛擬前端元件允許在編輯器中將節標籤為可AEM編SPA輯。
* 同時，可SPA以在中將托管在不同域上的內容AEM編輯。

請參閱文章 [編輯SPA外部AEM](spa-edit-external.md) 的子菜單。

## 要求 {#requirements}

* 在開發中啟用CORS
* 在頁屬性中配置遠程URL
* 在SPA中呈AEM現
* Web應用程式必須使用綁定器資產清單，如下所示之一，並在域根中公開asset-manifest.json檔案，該檔案在入口點屬性中列出要載入的所有CSS和JS檔案：
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest

   ![入口點](assets/asset-manifest-entrypoints.png)

* 應用程式必須能夠在 `<div id="root"></div>` 在身體元素下。 如果應用程式需要不同的標籤來實例化，則必須在具有 `sling:resourceSuperType="spa-project-core/components/remotepage`。

## 限制 {#limitations}

* RemotePage元件期望實現提供與RemotePage元件一樣的資產清單 [中。](https://github.com/shellscape/webpack-manifest-plugin) 但是， RemotePage元件僅經過測試以與React框架（和通過remote-page-next元件的Next.js）配合使用，因此不支援從其他框架(如Angular)遠程載入應用程式。
* 在中執行遠程呈現時，應用程式的根HTML檔案中定義的內部CSS以及根DOM節點上的內聯CSS將不可AEM用。

## 技術詳細資訊 {#technical-details}

與項目的其AEM余部SPA分一樣，RemotePage元件是開源的。 有關RemotePage元件的全部技術詳細資訊， [請參閱GitHub儲存庫。](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
