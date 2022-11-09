---
title: AEM中SPA快速入門 — Angular
seo-title: Getting Started with SPAs in AEM - Angular
description: 本文提供範例SPA應用程式，說明其組合方式，並可讓您使用Angular架構快速上手並執行自己的SPA。
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
ht-degree: 2%

---

# AEM中SPA快速入門 — Angular{#getting-started-with-spas-in-aem-angular}

單頁應用程式 (SPA) 可為網站使用者提供引人入勝的體驗。開發人員希望能使用SPA架構建立網站，而作者則想在AEM中為使用SPA架構建立的網站順暢地編輯內容。

SPA製作功能提供全方位的解決方案，可支援AEM中的SPA。 本文在Angular架構上示範簡化的SPA應用程式，並說明其組合方式，讓您能夠快速上手並執行自己的SPA。

>[!NOTE]
>
>本文是基於Angular框架。 如需React架構的對應檔案，請參閱 [AEM中的SPA快速入門 — React](/help/sites-developing/spa-getting-started-react.md).

>[!NOTE]
>
>若專案需要SPA架構的用戶端轉譯(例如React或Angular),SPA Editor是建議的解決方案。

## 簡介 {#introduction}

本文概述簡單SPA的基本功能，以及您執行作業所需了解的最低限度。

如需SPA在AEM中如何運作的詳細資訊，請參閱下列檔案：

* [SPA簡介和逐步說明](/help/sites-developing/spa-walkthrough.md)
* [SPA製作簡介](/help/sites-developing/spa-overview.md)
* [SPA Blueprint](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>為了能在SPA內製作內容，內容必須儲存在AEM中，並由內容模型公開。
>
>若SPA不遵守內容模型合約，則在AEM外部開發的Analytics將無法授權。

本檔案將逐步說明簡化SPA的結構，並說明其運作方式，以便您將此了解套用至您自己的SPA。

## 相依性、配置和構建 {#dependencies-configuration-and-building}

除了預期的Angular相依性外，範例SPA還可運用其他程式庫，讓SPA的建立更有效率。

### 相依性 {#dependencies}

此 `package.json` 檔案會定義整體SPA套件的需求。 此處列出所需的最低AEM相依性。

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
```

此 `aem-clientlib-generator` 可用來讓建立用戶端程式庫的作業在建立過程中自動執行。

`"aem-clientlib-generator": "^1.4.1",`

有關該檔案的更多詳細資訊，請參見 [在GitHub上](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>的最低版本 `aem-clientlib-generator` 必填為1.4.1。

此 `aem-clientlib-generator` 在 `clientlib.config.js` 檔案，如下所示。

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

實際建置應用程式可運用 [Webpack](https://webpack.js.org/) 除了自動建立用戶端程式庫的aem-clientlib-generator外，還可進行轉譯。 因此，build命令將類似於：

`"build": "ng build --build-optimizer=false && clientlib",`

建置後，可將套件上傳至AEM例項。

### AEM 專案原型 {#aem-project-archetype}

任何AEM專案皆應運用 [AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)，可支援使用React或Angular的SPA專案，並運用SPA SDK。

## 應用程式結構 {#application-structure}

如先前所述，包括相依性和建立應用程式，讓您得到可上傳至AEM例項的有效SPA套件。

本檔案的下一節將帶您了解AEM中SPA的結構、驅動應用程式的重要檔案，以及它們如何共同運作。

以簡化的影像元件為例，但應用程式的所有元件都以相同的概念為基礎。

### app.module.ts {#app-module-ts}

進入SPA的入口點為 `app.module.ts` 此處顯示的檔案已簡化，以著重於重要內容。

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

此 `app.module.ts` 檔案是應用程式的起點，包含初始專案設定，並使用 `AppComponent` 引導應用程式。

#### 靜態實例化 {#static-instantiation}

使用元件模板靜態實例化元件時，必須將值從模型傳遞到元件的屬性。 模型中的值作為屬性傳遞，以後可作為元件屬性使用。

### app.component.ts {#app-component-ts}

一次 `app.module.ts` 引導 `AppComponent`，接著便可初始化應用程式，此處以簡化版本顯示，著重於重要內容。

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

處理頁面後， `app.component.ts` 呼叫 `main-content.component.ts` 以簡化版本列出。

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

此 `MainComponent` 擷取頁面模型的JSON表示，並處理內容以包裝/裝飾頁面的每個元素。 有關 `Page` 可在文檔中找到 [SPA Blueprint](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### image.component.ts {#image-component-ts}

此 `Page` 由元件組成。 擷取JSON後， `Page` 可以處理這些元件，例如 `image.component.ts` 如下所示。

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

AEM中SPA的核心思想是將SPA元件對應至AEM元件，以及在修改內容時更新元件（反之亦然）。 請參閱檔案 [SPA編輯器概述](/help/sites-developing/spa-overview.md) 以取得此通訊模型的摘要。

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

此 `MapTo` 方法會將SPA元件對應至AEM元件。 支援使用單一字串或字串陣列。

`ImageEditConfig` 是配置對象，通過為編輯器提供必要的元資料來生成佔位符，有助於啟用元件的創作功能

如果沒有內容，則會提供標籤作為預留位置來表示空白內容。

#### 動態傳遞的屬性 {#dynamically-passed-properties}

來自模型的資料會以元件屬性的形式動態傳遞。

### image.component.html {#image-component-html}

最後，影像可呈現於 `image.component.html`.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## 在SPA元件之間共用資訊 {#sharing-information-between-spa-components}

單頁應用程式中的元件必須經常共用資訊。 執行此作業有數種建議方法，如下所列，其複雜度會隨之增加。

* **選項1:** 將邏輯和廣播集中到必要的元件，例如，將util類用作純物件導向的解決方案。
* **選項2:** 使用狀態庫（如NgRx）共用元件狀態。
* **選項3:** 透過自訂和擴充容器元件，善用物件階層。

## 後續步驟 {#next-steps}

如需建立自己的SPA的逐步指南，請參閱 [AEM SPA Editor - WKND Events教學課程快速入門](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

如需如何組織您自己以開發SPA for AEM的詳細資訊，請參閱文章 [開發SPA for AEM](/help/sites-developing/spa-architecture.md).

如需動態模型與元件對應，以及其在AEM中於SPA內如何運作的詳細資訊，請參閱文章 [SPA的動態模型與元件對應](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

若您想在AEM中針對React或Angular以外的架構實作SPA，或只想深入探討SPA SDK for AEM的運作方式，請參閱 [SPA Blueprint](/help/sites-developing/spa-blueprint.md) 文章。
