---
title: 複合元SPA件
description: 瞭解如何使用單頁應用程式(AEMSingle-Page Application(SPA)Editor建立您自己的複合元件，這些元件是由其他元件組成的元件。
translation-type: tm+mt
source-git-commit: 431bed450ed5b0239d9191dcf061f01e64b8981a
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---


# &lt;a0/SPA>中的複合元件{#composite-components-in-spas}

複合元件將多個基本元件AEM結合為單一元件，以運用元件的模組化特性。 常見的複合元件使用案例是卡片元件，由影像和文字元件的組合而成。

當複合元件在「單頁應用程式(AEMSPA)編輯器」架構中正確實作時，內容作者可以像拖放任何其他元件一樣拖放這些元件，但仍能個別編輯組成複合元件的每個元件。

本文將示範如何將複合元件新增至單一頁面應用程式，以便與編輯器完AEM美搭SPA配運作。

## 使用案例{#use-case}

本文將以典型卡片元件為實例。 卡片是許多數位體驗的常用UI元素，通常由影像和相關文字或標題組成。 作者希望能夠拖放整張卡片，但可以個別編輯卡片的影像，並自訂相關文字。

## 必備條件 {#prerequisites}

以下用於支援複合元件使用案例的模型需要以下先決條件。

* 您的開AEM發實例在具有示例項目的埠4502上本地運行。
* 您已啟用正在工作的外部React應用程式[，可AEM在中編輯。](spa-edit-external.md)
* React應用程式會使用RemotePage元AEM件載入至編輯器[。](spa-remote-page.md)

## 向&lt;a0/SPA>添加複合元件{#adding-composite-components}

根據您在中的實作，實作複合元件有三種不SPA同的模AEM型。

* [您的專案中不存在元AEM件。](#component-does-not-exist)
* [元件存在於您的專AEM案中，但其必要內容不存在。](#content-does-not-exist)
* [您的專案中同時包含元件及其必要AEM內容。](#both-exist)

以下各節提供使用卡片元件來實施每個案例的範例。

### 您的專案中不存在元AEM件。{#component-does-not-exist}

首先，建立構成複合元件的元件，即影像及其文本的元件。

1. 在專案中建立文字元AEM件。
1. 在元件的`editConfig`節點中從項目添加相應的`resourceType`。

   ```text
    resourceType: 'wknd-spa/components/text' 
   ```

1. 使用`withMappable`幫助程式可啟用元件的編輯。

   ```text
   export const AEMText = withMappable(Text, TextEditConfig); 
   ```

文字元件將類似下列。

```javascript
import React from 'react';
import { withMappable } from '@adobe/aem-react-editable-components';

export const TextEditConfig = {
  emptyLabel: 'Text',
  isEmpty: function(props) {
    return !props || !props.text || props.text.trim().length < 1;
  },
  resourceType: 'wknd-spa/components/text'
};

export const Text = ({ cqPath, richText, text }) => {
  const richTextContent = () => (
    <div className="aem_text"
      id={cqPath.substr(cqPath.lastIndexOf('/') + 1)}
      data-rte-editelement
      dangerouslySetInnerHTML={{__html: text}} />
  );
  return richText ? richTextContent() : (
     <div className="aem_text">{text}</div>
  );
};

export const AEMText = withMappable(Text, TextEditConfig);
```

如果您以類似的方式建立影像元件，則可將它與`AEMText`元件結合為新的卡片元件，將影像和文字元件當成子系。

```javascript
import React from 'react';
import { AEMText } from './AEMText';
import { AEMImage } from './AEMImage';

export const AEMCard = ({ pagePath, itemPath}) => (
  <div>
    <AEMText
       pagePath={pagePath}
       itemPath={`text`} />
    <AEMImage
       pagePath={pagePath}
       itemPath={`image`} />
   </div>
);
```

現在，這個產生的複合元件可以放置在應用程式中的任何位置，而會在編輯器中新增文字和影像元件的預留位SPA置。 在以下範例中，卡片元件會新增至標題下方的首頁元件。

```javascript
function Home() {
  return (
    <div className="Home">
      <h2>Current Adventures</h2>
      <AEMCard
        pagePath='/content/wknd-spa/home' />
    </div>
  );
}
```

這會在編輯器中顯示文字和影像的空白預留位置。 當使用編輯器輸入這些值時，這些值會儲存在指定的頁面路徑（即`/content/wknd-spa/home`）的根層級，且名稱會在`itemPath`中指定。

![編輯器中的複合卡元件](assets/composite-card.png)

### 元件存在於您的專AEM案中，但其必要內容不存在。{#content-does-not-exist}

在這種情況下，卡片元件已建立在包含標題和影AEM像節點的專案中。 子節點（文本和影像）具有相應的資源類型。

![卡元件的節點結構](assets/composite-node-structure.png)

然後，您可以將它新增至SPA並擷取其內容。

1. 在中為此建立相SPA應元件。 確保子元件映射到項目中AEM的相應資源SPA類型。 在此範例中，我們使用與前例中詳細的[相同的`AEMText`和`AEMImage`元件。](#component-does-not-exist)

   ```javascript
   import React from 'react';
   import { Container, withMappable, MapTo } from '@adobe/aem-react-editable-components';
   import { Text, TextEditConfig } from './AEMText';
   import Image, { ImageEditConfig } from './AEMImage';
   
   export const AEMCard = withMappable(Container, {
     resourceType: 'wknd-spa/components/imagecard'
   });
   
   MapTo('wknd-spa/components/text')(Text, TextEditConfig);
   MapTo('wknd-spa/components/image')(Image, ImageEditConfig);
   ```

1. 由於`imagecard`元件沒有內容，請將卡片新增至頁面。 在中包含現AEM有容器SPA。
   * 如果專案中已有容器，AEM我們可將它加入SPA，並改為將元件新增至容AEM器。
   * 確保卡元件映射到中的相應資源類SPA型。

   ```javascript
   <ResponsiveGrid
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid' />
   ```

1. 將建立的`wknd-spa/components/imagecard`元件添加到頁面模板中容器元件[的允許元件中。](/help/sites-authoring/templates.md)

現在，`imagecard`元件可直接新增至編輯器中的容AEM器。

![在編輯器中合成卡片](assets/composite-card.gif)

### 您的專案中同時包含元件及其必要AEM內容。{#both-exist}

如果內容存在於AEM中，則可透過提供內容SPA路徑直接包含在中。

```javascript
<AEMCard
    pagePath='/content/wknd-spa/home'
    itemPath='root/responsivegrid/imagecard' />
```

![節點結構中的複合路徑](assets/composite-path.png)

`AEMCard`元件與上一個使用案例中定義的[元件相同。](#content-does-not-exist) 在這裡，專案中上述位置所定義AEM的內容會包含在SPA中。
