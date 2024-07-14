---
title: RemotePage 元件
description: RemotePage元件是自訂頁面元件，用於在AEM內編輯遠端React SPA。
exl-id: 3f015997-0d42-4241-a890-0f16a19c5e34
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 2%

---

# RemotePage 元件 {#remote-page-component}

在決定您要在外部SPA和AEM之間進行的整合層級時，您通常明顯需要能夠檢視和編輯AEM中的SPA。 RemotePage元件是僅用於此目的的自訂頁面元件。

## 概觀 {#overview}

RemotePage元件會從應用程式產生的`asset-manifest.json`擷取所有必要的資產，並用來在AEM中轉譯SPA。

* RemotePage可讓您將SPA的指令碼和樣式表插入AEM Page元件的內文中。
* 虛擬前端元件可讓您在AEM SPA編輯器中將區段標示為可編輯。
* 將託管在不同網域上的SPA放在一起，即可在AEM中編輯。

請參閱[在AEM](spa-edit-external.md)中編輯外部SPA一文，以取得有關AEM中可編輯外部SPA的更多詳細資料。

## 要求 {#requirements}

* 在開發中啟用CORS
* 在頁面屬性中設定遠端URL
* 在AEM中轉譯SPA
* Web應用程式必須使用類似下列其中一種的套件組合資產資訊清單，並在網域根目錄公開asset-manifest.json檔案，該檔案會在entrypoints屬性中列出所有要載入的CSS和JS檔案：
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest

  ![進入點](assets/asset-manifest-entrypoints.png)

* 應用程式必須能夠在body專案底下的`<div id="root"></div>`中初始化。 如果應用程式需要不同的標籤才能具現化，則必須在具有`sling:resourceSuperType="spa-project-core/components/remotepage`的Proxy元件的HTL指令碼中據以調整。

## 限制 {#limitations}

* RemotePage元件預期實作會提供資產資訊清單，就像這裡所提供的[一樣。](https://github.com/shellscape/webpack-manifest-plugin)然而，RemotePage元件僅經過測試可用於React架構（以及透過remote-page-next元件的Next.js），因此不支援從其他架構(例如Angular)從遠端載入應用程式。
* 在AEM中執行遠端轉譯時，在應用程式的根HTML檔案中定義的內部CSS以及根DOM節點上的內嵌CSS將不可用。

## 技術細節 {#technical-details}

如同其他的AEM SPA專案，RemotePage元件是開放原始碼。 如需RemotePage元件的完整技術詳細資訊，[請參閱GitHub存放庫。](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
