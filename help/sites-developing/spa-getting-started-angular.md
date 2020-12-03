---
title: AEM中的SPA快速入門- Angular
seo-title: AEM中的SPA快速入門- Angular
description: 本文介紹了一個示例SPA應用程式，並說明了它的組合方式，並允許您使用Angular框架快速啟動並運行自己的SPA。
seo-description: 本文介紹了一個示例SPA應用程式，並說明了它的組合方式，並允許您使用Angular框架快速啟動並運行自己的SPA。
uuid: d3d2fa63-68c8-4a48-8c8d-045f4f8db937
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9cdd7648-d67e-414d-aedf-a5687da39326
docset: aem65
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 0%

---


# AEM中的SPA快速入門- Angular{#getting-started-with-spas-in-aem-angular}

單頁應用程式(SPA)可為網站使用者提供引人入勝的體驗。 開發人員希望能夠使用SPA架構建立網站，而作者則想在AEM中為使用SPA架構建立的網站順暢地編輯內容。

SPA製作功能提供完整的解決方案，以支援AEM中的SPA。 本文介紹Angular架構上的簡化SPA應用程式，並說明其組合方式，讓您快速啟動並執行自己的SPA。

>[!NOTE]
>
>本文基於Angular框架。 如需React架構的對應檔案，請參閱[AEM中SPA快速入門- React](/help/sites-developing/spa-getting-started-react.md)。

>[!NOTE]
>
>SPA編輯器是建議的解決方案，適用於需要以SPA架構為基礎的用戶端轉換（例如React或Angular）的專案。

## 簡介 {#introduction}

本文摘述了簡單SPA的基本功能，以及您需要瞭解的最低功能，以便讓您的SPA運作。

如需SPA在AEM中運作的詳細資訊，請參閱下列檔案：

* [SPA簡介與逐步說明](/help/sites-developing/spa-walkthrough.md)
* [SPA製作簡介](/help/sites-developing/spa-overview.md)
* [SPA藍圖](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>為了能夠在SPA中製作內容，內容必須儲存在AEM中，並由內容模型公開。
>
>如果AEM以外開發的SPA不遵守內容模型合約，則無法授權。

本檔案將逐步介紹簡化的SPA結構，並說明其運作方式，讓您將此理解套用至您自己的SPA。

## 相依性、配置和構建{#dependencies-configuration-and-building}

除了預期的Angular相依性外，範例SPA還可運用其他程式庫，讓建立SPA更有效率。

### 相依關係 {#dependencies}

`package.json`檔案定義了整個SPA包的要求。 此處列出最低需要的AEM相依性。

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
```

`aem-clientlib-generator`可讓建立用戶端程式庫的作業自動化，做為建立程式的一部分。

`"aem-clientlib-generator": "^1.4.1",`

有關它的詳細資訊，請在GitHub上[這裡](https://github.com/wcm-io-frontend/aem-clientlib-generator)找到。

>[!CAUTION]
>
>所需的`aem-clientlib-generator`最低版本為1.4.1。

`aem-clientlib-generator`在`clientlib.config.js`檔案中的配置如下。

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

實際建立應用程式時，除了aem-clientlib-generator以外，還運用[Webpack](https://webpack.js.org/)進行轉譯，以建立自動用戶端程式庫。 因此，build命令將類似：

`"build": "ng build --build-optimizer=false && clientlib",`

建立後，套件就可以上傳至AEM例項。

### AEM Project Archetype {#aem-project-archetype}

任何AEM專案都應運用[AEM Project Archetype](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html)，它支援使用React或Angular的SPA專案，並運用SPA SDK。

## 應用程式結構{#application-structure}

納入相依性並依照先前所述建立應用程式，將會留下您可上傳至AEM例項的正常SPA套件。

本檔案的下一節將帶您瞭解AEM中的SPA結構、驅動應用程式的重要檔案，以及它們如何搭配運作。

以簡化的影像元件為例，但應用程式的所有元件都是以相同的概念為基礎。

### app.module.ts {#app-module-ts}

進入SPA的入口點是此處顯示的`app.module.ts`檔案，此處已簡化，以著重於重要內容。

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

`app.module.ts`檔案是應用程式的起點，包含初始專案設定，並使用`AppComponent`引導應用程式。

#### 靜態實例化{#static-instantiation}

使用元件模板靜態實例化元件時，必須將值從模型傳遞到元件的屬性。 模型中的值作為屬性傳遞，以便以後作為元件屬性使用。

### app.component.ts {#app-component-ts}

在`app.module.ts`啟動`AppComponent`後，它就可以初始化應用程式，此應用程式會以簡化版本顯示，以專注於重要內容。

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

透過處理頁面，`app.component.ts`會呼叫此處列於簡化版本的`main-content.component.ts`。

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

`MainComponent`會擷取頁面模型的JSON表示法，並處理內容以包覆／裝飾頁面的每個元素。 有關`Page`的詳細資訊，請參見文檔[SPA Blueprint](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501)。

### image.component.ts {#image-component-ts}

`Page`由元件組成。 透過內嵌JSON,`Page`可處理這些元件，例如`image.component.ts`，如此處所示。

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

AEM中SPA的核心理念是將SPA元件對應至AEM元件，並在修改內容時更新元件（反之亦然）。 有關此通信模型的摘要，請參見文檔[SPA編輯器概述](/help/sites-developing/spa-overview.md)。

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

`MapTo`方法將SPA元件對應至AEM元件。 它支援使用單一字串或字串陣列。

`ImageEditConfig` 是配置對象，通過為編輯器提供生成佔位符所需的元資料來啟用元件的編寫功能

如果沒有內容，則會提供標籤作為預留位置來表示空內容。

#### 動態傳遞的屬性{#dynamically-passed-properties}

來自模型的資料會動態傳遞為元件的屬性。

### image.component.html {#image-component-html}

最後，影像可在`image.component.html`中轉譯。

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## 在SPA元件之間共用資訊{#sharing-information-between-spa-components}

單頁應用程式中的元件必須定期共用資訊。 有幾種建議的方法可做到，如下列出，增加了複雜性。

* **選項1:** 將邏輯集中化，並廣播到必要的元件，例如，將util類用作純物件導向的解決方案。
* **選項2：使** 用狀態庫（如NgRx）共用元件狀態。
* **選項3：自** 訂和擴充容器元件，以運用物件階層。

## 後續步驟{#next-steps}

如需建立您自己SPA的逐步指南，請參閱[AEM SPA編輯器快速入門- WKND事件教學課程](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)。

如需如何組織您自己為AEM開發SPA的詳細資訊，請參閱文章[「為AEM開發SPA」](/help/sites-developing/spa-architecture.md)。

如需動態模型至元件對應的詳細資訊，以及它在AEM中SPA中的運作方式，請參閱文章[SPA的動態模型至元件對應](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)。

如果您想要在AEM中實作React或Angular以外的架構的SPA，或只想深入瞭解AEM的SPA SDK的運作方式，請參閱[SPA Blueprint](/help/sites-developing/spa-blueprint.md)文章。
