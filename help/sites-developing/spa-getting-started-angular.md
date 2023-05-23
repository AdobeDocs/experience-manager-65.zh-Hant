---
title: 入門 — SPAAngular
seo-title: Getting Started with SPAs in AEM - Angular
description: 本文介紹了一SPA個示例應用程式，說明了它的組合方式，並允許您使用Angular框架快速啟動和運SPA行自己的應用程式。
seo-description: This article presents a sample SPA application, explains how it is put together, and allows you to get up-and-running with your own SPA quickly using the Angular framework.
uuid: d3d2fa63-68c8-4a48-8c8d-045f4f8db937
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9cdd7648-d67e-414d-aedf-a5687da39326
docset: aem65
exl-id: 9528d92b-0989-4e2d-83be-ba6c07c845e2
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 5%

---

# 入門 — SPAAngular{#getting-started-with-spas-in-aem-angular}

單頁應用程式 (SPA) 可為網站使用者提供引人入勝的體驗。開發人員希望能夠使用框架構建站SPA點，而作者希望無縫地編輯AEM使用框架構建的站SPA點的內容。

創SPA作功能提供了全面的解決方案，SPA支援AEM內。 本文介紹了一SPA個簡化的Angular框架應用程式，並說明了它的組合方式，使您能夠快速啟動並運行自己的運SPA行。

>[!NOTE]
>
>本文基於Angular框架。 有關React框架的相應文檔，請參見 [入門 — SPA反AEM應](/help/sites-developing/spa-getting-started-react.md)。

>[!NOTE]
>
>編輯SPA器是需要基於框架的SPA客戶端呈現(例如，反應或Angular)的項目的推薦解決方案。

## 簡介 {#introduction}

本文概括了簡單功能的基本功SPA能，以及使您的運行所需要知道的最低值。

有關如何工作的SPA詳細AEM資訊，請參閱以下文檔：

* [SPA 簡介和逐步解說](/help/sites-developing/spa-walkthrough.md)
* [創SPA作簡介](/help/sites-developing/spa-overview.md)
* [SPA 藍圖](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>為了能夠在內部創作內容SPA，內容必須儲存在內AEM容模型中並由內容模型公開。
>
>如SPA果不遵守內AEM容模型合同，外部開發的將無法授權。

本文檔將介紹簡化的結構，SPA並說明其工作原理，以便您可以將此理解應用到您自己的SPA結構。

## 依賴項、配置和構建 {#dependencies-configuration-and-building}

除了預期的Angular相關性外，該示例SPA還可以利用附加庫，使建立更SPA加高效。

### 相依性 {#dependencies}

的 `package.json` 檔案定義了整個包的SPA要求。 此處列出了AEM所需的最低依賴項。

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
```

的 `aem-clientlib-generator` 可使建立客戶端庫成為生成過程的一部分。

`"aem-clientlib-generator": "^1.4.1",`

有關此項的進一步詳細資訊，請參閱 [在GitHub上](https://github.com/wcm-io-frontend/aem-clientlib-generator)。

>[!CAUTION]
>
>的最低版本 `aem-clientlib-generator` 必填項為1.4.1。

的 `aem-clientlib-generator` 在 `clientlib.config.js` 的下界。

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-angular-app/clientlibs",

    libs: {
        name: "my-angular-app",
        allowProxy: true,
        categories: ["my-angular-app"],
        embed: ["my-angular-app.responsivegrid"],
        jsProcessor: ["min:gcc"],
        serializationFormat: "xml",
        assets: {
            js: [
                "dist/**/*.js"
            ],
            css: [
                "dist/**/*.css"
            ]
        }
    }
};
```

### 正在建置 {#building}

實際構建應用可利用 [Webpack](https://webpack.js.org/) 除aem-clientlib-generator外，還用於自動建立客戶端庫。 因此，build命令將類似於：

`"build": "ng build --build-optimizer=false && clientlib",`

生成後，可以將包上載到實AEM例。

### AEM 專案原型 {#aem-project-archetype}

任何 AEM 專案都應利用 [AEM 專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)，它支援使用 React 或 Angular 的 SPA 專案並利用 SPA SDK。

## 應用程式結構 {#application-structure}

包括依賴項和生成應用程式（如前所述）將為您留SPA下一個工作包，您可以將其上載到AEM實例。

本文檔的下一節將介紹如何SPA構AEM建中的檔案、驅動應用程式的重要檔案以及它們如何協同工作。

以簡化的影像元件為例，但應用程式的所有元件都基於相同的概念。

### app.module.ts {#app-module-ts}

入口SPA是 `app.module.ts` 此處顯示的檔案經過簡化，可以專注於重要內容。

```
// app.module.ts
import { BrowserModule, BrowserTransferStateModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { SpaAngularEditableComponentsModule } from '@adobe/aem-angular-editable-components';
import { AppRoutingModule } from './app-routing.module';

@NgModule({
  imports: [ BrowserModule.withServerTransition({ appId: 'my-angular-app' }),
    SpaAngularEditableComponentsModule,
    AppRoutingModule,
    BrowserTransferStateModule ],
  providers: ...,
  declarations: [ ... ],
  entryComponents: [ ... ],
  bootstrap: [ AppComponent ]
})
export class AppModule {}
```

的 `app.module.ts` 檔案是應用程式的起點，包含初始項目配置和使用 `AppComponent` 引導應用程式。

#### 靜態實例化 {#static-instantiation}

使用元件模板靜態實例化元件時，必須將值從模型傳遞到元件的屬性。 模型中的值作為屬性傳遞，以便以後作為元件屬性可用。

### app.component.ts {#app-component-ts}

一次 `app.module.ts` 引導 `AppComponent`然後，它可以初始化應用程式，該應用程式將以簡化版本顯示在此處，以專注於重要內容。

```
// app.component.ts
import { Component } from '@angular/core';
import { ModelManager } from '@adobe/aem-spa-page-model-manager';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-root',
  template: `
    <router-outlet></router-outlet>
  `
})

export class AppComponent {
  items;
  itemsOrder;
  path;

  constructor() {
    ModelManager.initialize().then(this.updateData.bind(this));
  }

  private updateData(model) {
    this.path = model[Constants.PATH_PROP];
    this.items = model[Constants.ITEMS_PROP];
    this.itemsOrder = model[Constants.ITEMS_ORDER_PROP];
  }
}
```

### main-content.component.ts {#main-content-component-ts}

通過處理頁面， `app.component.ts` 呼叫 `main-content.component.ts` 以簡化版本列出。

```
import { Component } from '@angular/core';
import { ModelManagerService }     from '../model-manager.service';
import { ActivatedRoute } from '@angular/router';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-main',
  template: `
    <aem-page class="structure-page" [attr.data-cq-page-path]="path" [cqPath]="path" [cqItems]="items" [cqItemsOrder]="itemsOrder" ></aem-page>
  `
})

export class MainContentComponent {
  items;
  itemsOrder;
  path;

  constructor( private route: ActivatedRoute,
    private modelManagerService: ModelManagerService) {
    this.modelManagerService.getData({ path: this.route.snapshot.data.path }).then((data) => {
      this.path = data[Constants.PATH_PROP];
      this.items = data[Constants.ITEMS_PROP];
      this.itemsOrder = data[Constants.ITEMS_ORDER_PROP];
    });
  }
}
```

的 `MainComponent` 接收頁面模型的JSON表示，並處理內容以包裝/裝飾頁面的每個元素。 有關 `Page` 可在文檔中找到 [藍SPA圖](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501)。

### image.component.ts {#image-component-ts}

的 `Page` 是由元件組成的。 JSON接收後， `Page` 可以處理這些元件，如 `image.component.ts` 如圖所示。

```
/// image.component.ts
import { Component, Input } from '@angular/core';

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function(cqModel) {
        return !cqModel || !cqModel.src || cqModel.src.trim().length < 1;
    }
};

@Component({
  selector: 'app-image',
  templateUrl: './image.component.html',
})

export class ImageComponent {
  @Input() src: string;
  @Input() alt: string;
  @Input() title: string;
}

MapTo('my-angular-app/components/image')(ImageComponent, ImageEditConfig);
```

中的核心SPA思想AEM是將元件映射SPA到元件AEM，並在修改內容時更新元件（反之亦然）。 查看文檔 [編SPA輯器概述](/help/sites-developing/spa-overview.md) 獲取此通信模型的摘要。

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

的 `MapTo` 方法將組SPA件映射到AEM元件。 它支援使用單個字串或字串陣列。

`ImageEditConfig` 是配置對象，它通過為編輯器提供生成佔位符所需的元資料來幫助啟用元件的創作功能

如果沒有內容，則將標籤作為佔位符提供以表示空內容。

#### 動態傳遞的屬性 {#dynamically-passed-properties}

來自模型的資料作為元件的屬性動態傳遞。

### image.component.html {#image-component-html}

最後，可在 `image.component.html`。

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## 元件之間共用信SPA息 {#sharing-information-between-spa-components}

對於單頁應用程式中的元件來說，經常需要共用資訊。 有幾種建議的方法來執行此操作，其複雜程度的增加順序如下所列。

* **選項1:** 將邏輯集中並廣播到必要的元件，例如，使用util類作為純物件導向的解決方案。
* **選項2:** 使用狀態庫（如NgRx）共用元件狀態。
* **備選3:** 通過自定義和擴展容器元件來利用對象層次結構。

## 後續步驟 {#next-steps}

有關建立自己的逐步指南的SPA資訊，請參閱 [編輯器入AEM門SPA- WKND事件教程](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)。

有關如何組織您開發以查看文章SPA的AEM詳細資訊 [開SPA發AEM](/help/sites-developing/spa-architecture.md)。

有關動態模型到元件映射及其在中的工作方式的詳細SPA信AEM息，請參閱文章 [動態模型到元件的映SPA射](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)。

如果您希望在SPAReact或AEMAngular之外的框架中實施，或只是希望深入瞭解SDK的工SPA作方AEM式，請參閱 [藍SPA圖](/help/sites-developing/spa-blueprint.md) 文章。
