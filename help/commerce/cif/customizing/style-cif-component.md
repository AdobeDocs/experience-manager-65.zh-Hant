---
title: 樣式AEMCIF核心元件
description: 瞭解如何設AEM定CIF核心元件的樣式。 本教學課程涵蓋如何使用用戶端資料庫或clientlibs來部署及管理Adobe Experience Manager(AEM)商務實作的CSS和Javascript。 本教學課程也將涵蓋ui.frontend模組和webpack專案如何整合到端對端建置程式。
sub-product: 商務
topics: Development
version: cloud-service
doc-type: tutorial
feature: 商務整合框架
kt: 3456
thumbnail: 3456-style-cif.jpg
translation-type: tm+mt
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '2562'
ht-degree: 1%

---

# 樣式AEMCIF核心元件{#style-aem-cif-core-components}

[CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia)是使用[CIF核心元件](https://github.com/adobe/aem-core-cif-components)的參考代碼庫。 在本教學課程中，您將檢視Venia參考專案，並瞭解CIF核心元件所使用的CSSAEM和JavaScript的組織方式。 您也將使用CSS建立新樣式，以更新&#x200B;**Product Teaser**&#x200B;元件的預設樣式。

>[!TIP]
>
> 啟動您自己的商務實AEM施時，請使用[Project archetype](https://github.com/adobe/aem-project-archetype)。

## 您將建立的

在本教學課程中，類似卡片的產品摘要元件將會建置新樣式。 本教學課程可套用至其他CIF核心元件。

![您將建立的](../assets/style-cif-component/what-you-will-build.png)

## 必備條件 {#prerequisites}

完成本教學課程時，需要有本機開發環境。 這包括已配置並連AEM接到Magento實例的運行實例。 檢視[設定使用](../develop.md)進行本機開發的AEM需求和步驟。

## 克隆Venia Project {#clone-venia-project}

我們將仿製[Venia Project](https://github.com/adobe/aem-cif-guides-venia)，然後覆寫預設樣式。

>[!NOTE]
>
> **您可以隨意使用現有專案** (根據包含CIF的AEM「專案原型」)，並略過本節。

1. 執行下列git命令以複製專案：

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. 將專案建立並部署至下列的本機例AEM項：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. 添加必要的OSGi配置，將實AEM例連接到Magento實例，或將配置添加到新建的項目。

1. 此時，您應該擁有連接至Magento實例的店面的工作版本。 導覽至`US` > `Home`頁面，網址為：[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

   您應該會看到，店面目前使用的是Venia主題。 展開店面的「主功能表」時，您應該會看到各種類別，指出連線Magento正在運作。

   ![使用Venia Theme配置的店面](../assets/style-cif-component/venia-store-configured.png)

## 客戶端庫和ui.frontend模組{#introduction-to-client-libraries}

負責呈現店面主題／樣式的CSS和JavaScript，由[Client libraryAEM](/help/sites-developing/clientlibs.md)或clientlibs來管理。 用戶端程式庫提供一種機制，可在專案程式碼中組織CSS和Javascript，然後傳送至頁面。

您可新增並覆寫由AEM這些用戶端程式庫管理的CSS，將品牌特定樣式套用至CIF核心元件。 瞭解用戶端程式庫的結構化及包含在頁面上，是十分重要的。

[ui.frontend](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/uifrontend.html)是專用的[webpack](https://webpack.js.org/)專案，用來管理專案的所有前端資產。 這可讓前端開發人員使用任何語言和技術，例如[TypeScript](https://www.typescriptlang.org/)、[Sass](https://sass-lang.com/)等。

`ui.frontend`模組也是Maven模組，通過使用[aem-clientlib-generator](https://github.com/wcm-io-frontend/aem-clientlib-generator)的NPM模組與較大的項目整合。 在構建過程中，`aem-clientlib-generator`將編譯的CSS和JavaScript檔案複製到`ui.apps`模組中的客戶端庫中。

![ui.frontend ui.apps架構](../assets/style-cif-component/ui-frontend-architecture.png)

*在Maven建置期間，編譯的CSS `ui.frontend` 和Javascript會 `ui.apps` 從模組複製到模組中做為用戶端程式庫*

## 更新摘要樣式{#ui-frontend-module}

接著，對摘要樣式進行小幅變更，以瞭解`ui.frontend`模組和用戶端程式庫的運作方式。 使用您選擇的[IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide)來導入Venia項目。 使用的截屏來自[Visual Studio代碼IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code)。

1. 導覽並展開&#x200B;**ui.frontend**&#x200B;模組，並將資料夾階層展開為：`ui.frontend/src/main/styles/commerce`:

   ![ui.frontend商務資料夾](../assets/style-cif-component/ui-frontend-commerce-folder.png)

   請注意，資料夾下有多個Sass(`.scss`)檔案。 這些是每個「商務」元件的「商務」特定樣式。

1. 開啟檔案`_productteaser.scss`。

1. 更新`.item__image`規則並修改邊框規則：

   ```scss
   .item__image {
       border: #ea00ff 8px solid; /* <-- modify this rule */
       display: block;
       grid-area: main;
       height: auto;
       opacity: 1;
       transition-duration: 512ms;
       transition-property: opacity, visibility;
       transition-timing-function: ease-out;
       visibility: visible;
       width: 100%;
   }
   ```

   上述規則應在「產品摘要元件」中新增非常粗體的粉紅色邊框。

1. 開啟新的終端機視窗並導覽至`ui.frontend`資料夾：

   ```shell
   $ cd <project-location>/aem-cif-guides-venia/ui.frontend
   ```

1. 運行以下Maven命令：

   ```shell
   $ mvn clean install
   ...
   [INFO] ------------------------------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ------------------------------------------------------------------------
   [INFO] Total time:  29.497 s
   [INFO] Finished at: 2020-08-25T14:30:44-07:00
   [INFO] ------------------------------------------------------------------------
   ```

   Inspect終端輸出。 您將看到Maven命令執行了包括`npm run build`在內的多個NPM指令碼。 `npm run build`命令定義在`package.json`檔案中，具有編譯webpack項目和觸發客戶端庫生成的效果。

1. Inspect檔案`ui.frontend/dist/clientlib-site/site.css`:

   ![編譯網站CSS](../assets/style-cif-component/comiled-site-css.png)

   該檔案是項目中所有Sass檔案的編譯和精簡版本。

   >[!NOTE]
   >
   > 這類檔案會從來源控制項中忽略，因為它們應在建立時產生。

1. Inspect檔案`ui.frontend/clientlib.config.js`。

   ```js
   /* clientlib.config.js*/
   ...
   // Config for `aem-clientlib-generator`
   module.exports = {
       context: BUILD_DIR,
       clientLibRoot: CLIENTLIB_DIR,
       libs: [
           {
               ...libsBaseConfig,
               name: 'clientlib-site',
               categories: ['venia.site'],
               dependencies: ['venia.dependencies', 'aem-core-cif-react-components'],
               assets: {
   ...
   ```

   這是[aem-clientlib-generator](https://github.com/wcm-io-frontend/aem-clientlib-generator)的設定檔案，並決定編譯的CSS和JavaScript將轉換為用戶端程式庫的位AEM置和方式。

1. 在`ui.apps`模組中檢查檔案：`ui.apps/src/main/content/jcr_root/apps/venia/clientlibs/clientlib-site/css/site.css`:

   ![在ui.apps中編譯網站CSS](../assets/style-cif-component/comiled-css-ui-apps.png)

   這會將複製的`site.css`檔案複製到`ui.apps`專案中。 它現在是名為`clientlib-site`且類別為`venia.site`的clientlibrary的一部分。 一旦檔案屬於`ui.apps`模組的一部分，就可將其部署到該模AEM塊。

   >[!NOTE]
   >
   > 類似的檔案也會從來源控制項中忽略，因為它們應在建立時產生。

1. 接下來，檢查項目生成的其他客戶端庫：

   ![其他用戶端程式庫](../assets/style-cif-component/other-clientlibs.png)

   這些客戶端庫不由`ui.frontend`模組管理。 這些用戶端程式庫包含Adobe提供的CSS和JavaScript相依性。 這些clientlibraries的定義位於每個資料夾下方的`.content.xml`檔案中。

   **clientlib-base**  —— 此為空的客戶端庫，僅嵌入核心元件中所需的 [AEM依賴項](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html)。類別為`venia.base`。

   **clientlib-cif**  —— 這也是一個空的客戶端庫，它只嵌入了 [AEM CIF核心元件中的必要相關性](https://github.com/adobe/aem-core-cif-components)。類別為`venia.cif`。

   **clientlib-grid**  —— 這包括啟用「自適應格線」功能AEM所需的CSS。使用格AEM線可在編輯器中啟用「版面模式」([ Layout Mode](/help/sites-authoring/responsive-layout.md))AEM，讓內容作者能夠重新調整元件大小。 類別為`venia.grid`，並內嵌在`venia.base`程式庫中。

1. Inspect`customheaderlibs.html`和`customfooterlibs.html`下方的檔案：`ui.apps/src/main/content/jcr_root/apps/venia/components/page`

   ![自訂頁首和頁尾指令碼](../assets/style-cif-component/custom-header-footer-script.png)

   這些指令碼包含作為所有頁面一部分的&#x200B;**venia.base**&#x200B;和&#x200B;**venia.cif**&#x200B;程式庫。

   >[!NOTE]
   >
   > 只有基本庫會「硬式編碼」為頁面指令碼的一部分。 `venia.site` 未包含在這些檔案中，而是包含在頁面範本中，以獲得更大的彈性。稍後會檢查。

1. 從終端，建立並部署整個專案至本機執行個AEM體：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

## 製作產品摘要{#author-product-teaser}

現在已部署程式碼更新，請使用編寫工具將新的產品摘要元件例項新增至網站的AEM首頁。 這可讓我們檢視更新的樣式。

1. 開啟新的瀏覽器標籤，並導覽至網站的&#x200B;**首頁**:[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

1. 在&#x200B;**編輯**&#x200B;模式中展開資產搜尋器（側欄）。 將「資產」篩選器切換為&#x200B;**Products**。

   ![展開資產搜尋器並依產品篩選](../assets/style-cif-component/drag-drop-product-page.png)

1. 將新產品拖放至主版面容器的首頁：

   ![帶粉色邊框的產品摘要](../assets/style-cif-component/pink-border-product-teaser.png)

   您應該會看到「產品摘要」現在會根據先前建立的CSS規則變更，顯示亮粉色邊框。

## 驗證頁面{#verify-client-libraries}上的客戶端庫

接下來驗證頁面上是否包含用戶端程式庫。

1. 導覽至網站的&#x200B;**首頁**:[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

1. 選擇&#x200B;**頁面資訊**&#x200B;功能表，然後按一下&#x200B;**檢視為已發佈**:

   ![以已發佈狀態檢視](../assets/style-cif-component/view-as-published.png)

   如此會開啟未載入任何作AEM者javascript的頁面，因為它會顯示在發佈的網站上。 請注意，URL已附加查詢參數`?wcmmode=disabled`。 在開發CSS和Javascript時，最好使用此參數來簡化頁面，而不需任何作者的AEM協助。

1. 檢視頁面來源，您應該能夠識別包含的數個用戶端程式庫：

   ```html
   <!DOCTYPE html>
   <html lang="en-US">
   <head>
       ...
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-base.min.css" type="text/css">
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-site.min.css" type="text/css">
   </head>
   ...
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-site.min.js"></script>
       <script type="text/javascript" src="/etc.clientlibs/core/wcm/components/commons/site/clientlibs/container.min.js"></script>
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-base.min.js"></script>
   <script type="text/javascript" src="/etc.clientlibs/core/cif/clientlibs/common.min.js"></script>
   <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-cif.min.js"></script>
   </body>
   </html>
   ```

   傳送至頁面的用戶端程式庫會加上`/etc.clientlibs`前置詞，並透過[proxy](/help/sites-developing/clientlibs.md)提供，以避免暴露`/apps`或`/libs`中任何敏感內容。

   注意`venia/clientlibs/clientlib-site.min.css`和`venia/clientlibs/clientlib-site.min.js`。 這些是從`ui.frontend`模組衍生的已編譯CSS和Javascript檔案。

## 包含頁面範本的客戶端庫包含{#client-library-inclusion-pagetemplates}

如何包含用戶端程式庫有幾個選項。 接下來，請透過[頁面範本](/help/sites-developing/templates.md)檢查產生的專案如何包含`clientlib-site`程式庫。

1. 導覽至編輯器中網站的&#x200B;**首頁&lt;a1/AEM>:[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。**

1. 選擇&#x200B;**頁面資訊**&#x200B;功能表，然後按一下&#x200B;**編輯範本**:

   ![編輯範本](../assets/style-cif-component/edit-template.png)

   這將開啟&#x200B;**著陸頁面**&#x200B;範本，**首頁**&#x200B;頁面是基於此範本。

   >[!NOTE]
   >
   > 要從「開始」螢幕查看所有可用模板，請導航至「工具」**「工具」>「**&#x200B;一般」**>「模板」**。****

1. 在左上角，選擇&#x200B;**頁面資訊**&#x200B;圖示，然後按一下&#x200B;**頁面政策**。

   ![頁面原則功能表項目](../assets/style-cif-component/page-policy-menu.png)

1. 這會開啟「著陸頁面」範本的頁面政策：

   ![頁面政策——登陸頁面](../assets/style-cif-component/page-policy-properties.png)

   在右側，您可以看到將包含在使用此模板的所有頁面上的客戶端庫&#x200B;**類別**&#x200B;的清單。

   * `venia.dependencies` -提供任何依賴的供 `venia.site` 應商庫。
   * `venia.site` -這是模組生 `clientlib-site` 成的 `ui.frontend` 類別。

   請注意，其他範本使用相同的原則：**內容頁面**、**著陸頁面**&#x200B;等……透過重新使用相同的原則，我們可以確保所有頁面上都包含相同的用戶端程式庫。

   使用「範本」和「頁面」原則管理包含用戶端程式庫的好處是，您可以依範本變更原則。 例如，您可能在同一個實例中管理兩個不同的AEM品牌。 每個品牌都有其獨特的樣式或&#x200B;*theme*，但基本資料庫和程式碼會相同。 另一個範例是，如果您有較大的用戶端程式庫，而您只想要顯示在特定頁面上，則可針對該範本建立唯一的頁面原則。

## 本地Webpack開發{#local-webpack-development}

在上一練習中，對`ui.frontend`模組中的Sass檔案進行了更新，然後在執行Maven構建後，將更改部署到AEM。 接下來，我們將探討如何運用webpack-dev-server來快速開發前端樣式。

webpack-dev-server proxy影像和本機例項中的部分CSS/JavaScriptAEM，但可讓開發人員修改`ui.frontend`模組中的樣式和JavaScript。

1. 在瀏覽器中，瀏覽至&#x200B;**首頁**&#x200B;頁面和&#x200B;**檢視為發佈**:[http://localhost:4502/content/venia/us/en.html?wcmmode=disabled](http://localhost:4502/content/venia/us/en.html?wcmmode=disabled)。

1. 檢視頁面的來源，以及頁面的&#x200B;**copy**&#x200B;原始HTML。

1. 返回到`ui.frontend`模組下選擇的IDE，開啟檔案：`ui.frontend/src/main/static/index.html`

   ![靜態HTML檔案](../assets/style-cif-component/static-index-html.png)

1. 覆寫在前一步驟中複製的`index.html`和&#x200B;**paste**&#x200B;的內容。

1. 查找`clientlib-site.min.css`、`clientlib-site.min.js`和&#x200B;**remove**&#x200B;的包含。

   ```html
   <head>
       <!-- remove this link -->
       <link rel="stylesheet" href="/etc.clientlibs/venia/clientlibs/clientlib-base.min.css" type="text/css">
       ...
   </head>
   <body>
       ...
        <!-- remove this link -->
       <script type="text/javascript" src="/etc.clientlibs/venia/clientlibs/clientlib-site.min.js"></script>
   </body>
   ```

   這些值會移除，因為它們代表由`ui.frontend`模組產生的CSS和JavaScript編譯版本。 保留其他用戶端程式庫，因為它們將會從執行中的例項AEM中複製。

1. 開啟新的終端視窗並導覽至`ui.frontend`資料夾。 運行命令`npm start` :

   ```shell
   $ cd ui.frontend
   $ npm start
   ```

   這將啟動[http://localhost:8080/](http://localhost:8080/)上的webpack-dev-server

   >[!CAUTION]
   >
   > 如果出現與Sass相關的錯誤，請停止伺服器並運行命令`npm rebuild node-sass` ，然後重複上述步驟。 如果項目`aem-cif-guides-venia/pom.xml`中指定了不同版本的`npm`和`node`，則可能會發生這種情況。

1. 使用與登入的例項相同的瀏覽器，在新標籤中導覽至[http://localhost:8080/](http://localhost:8080/)AEM。 您應透過webpack-dev-server查看Venia首頁：

   ![埠80上的Webpack開發伺服器](../assets/style-cif-component/webpack-dev-server-port80.png)

   讓webpack-dev-server繼續運作。 它將用於下次練習。

## 實施產品摘要的資訊卡樣式{#update-css-product-teaser}

接著，修改`ui.frontend`模組中的Sass檔案，為「產品摘要」實作類似卡片的樣式。 webpack-dev-server將用於快速查看更改。

返回到IDE和生成的項目。

1. 在&#x200B;**ui.frontend**&#x200B;模組中，在`ui.frontend/src/main/styles/commerce/_productteaser.scss`重新開啟檔案`_productteaser.scss`。

1. 對「產品摘要」邊框進行下列變更：

   ```diff
       .item__image {
   -       border: #ea00ff 8px solid;
   +       border-bottom: 1px solid #c0c0c0;
           display: block;
           grid-area: main;
           height: auto;
           opacity: 1;
           transition-duration: 512ms;
           transition-property: opacity, visibility;
           transition-timing-function: ease-out;
           visibility: visible;
           width: 100%;
       }
   ```

   儲存變更，webpack-dev-server就會自動重新整理新樣式。

1. 新增下垂式陰影並將圓角加入「產品摘要」中。

   ```scss
    .item__root {
        position: relative;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
        transition: 0.3s;
        border-radius: 5px;
        float: left;
        margin-left: 12px;
        margin-right: 12px;
   }
   
   .item__root:hover {
      box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
   }
   ```

1. 更新產品名稱以顯示在摘要底部，並修改文字顏色。

   ```css
   .item__name {
       color: #000;
       display: block;
       float: left;
       font-size: 22px;
       font-weight: 900;
       line-height: 1em;
       padding: 0.75em;
       text-transform: uppercase;
       width: 75%;
   }
   ```

1. 更新產品價格，以便也顯示在摘要底部，並修改文字顏色。

   ```css
   .price {
       color: #000;
       display: block;
       float: left;
       font-size: 18px;
       font-weight: 900;
       padding: 0.75em;
       padding-bottom: 2em;
       width: 25%;
   
       ...
   ```

1. 更新底部的媒體查詢，將名稱和價格堆疊在小於&#x200B;**992px**&#x200B;的畫面中。

   ```css
   @media (max-width: 992px) {
       .productteaser .item__name {
           font-size: 18px;
           width: 100%;
       }
       .productteaser .item__price {
           font-size: 14px;
           width: 100%;
       }
   }
   ```

   您現在應該會看到webpack-dev-server中反映的卡片式：

   ![Webpack Dev Server摘要變更](../assets/style-cif-component/webpack-dev-server-teaser-changes.png)

   但是，尚未部署這些變AEM更。 您可以在此處下載[解決方案檔案](../assets/style-cif-component/_productteaser.scss)。

1. 從命令列終端AEM部署更新，以使用您的Maven技能：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

   >[!NOTE]
   >另外還有[IDE設定和工具](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment)，它們可以直接將項目檔案同步到本地實例，而AEM無需執行完整的Maven生成。

## 檢視更新的產品摘要{#view-updated-product-teaser}

將專案的程式碼部署至之後AEM，我們現在應該可以看到產品摘要的變更。

1. 返回瀏覽器並重新整理首頁：[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。 您應該會看到已套用更新的產品摘要樣式。

   ![更新的產品摘要樣式](../assets/style-cif-component/product-teaser-new-style.png)

1. 加入額外的產品預告來嘗試。 使用「版面模式」變更元件的寬度和偏移，以一列顯示多個預告。

   ![多種產品預告](../assets/style-cif-component/multiple-teasers-final.png)

## 疑難排解 {#troubleshooting}

您可以在[CRXDE-Lite](http://localhost:4502/crx/de/index.jsp)中確認已部署更新的CSS檔案：[http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css](http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css)

部署新的CSS和／或JavaScript檔案時，請務必確保瀏覽器不提供舊檔。 您可以清除瀏覽器快取或啟動新的瀏覽器工作階段，以消除這種情況。

還嘗AEM試快取客戶端庫以提高效能。 有時，在程式碼部署後，會提供舊版檔案。 可以使用[AEM重建客戶端庫工具](http://localhost:4502/libs/granite/ui/content/dumplibs.rebuild.html)手動使客戶端庫快取失效。 *如果您懷疑已快取舊版用戶端程式庫，AEM則偏好使用「使快取無效」方法。重建庫效率低下且耗時。*

## 恭喜{#congratulations}

您剛設計了第AEM一個CIF核心元件，並使用了webpack開發伺服器！

## 獎金競賽{#bonus-challenge}

使用[AEM Style system](/help/sites-authoring/style-system.md)來建立兩個樣式，供內容作者開啟／關閉。 [使用樣式系統開](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html) 發包含詳細步驟和資訊，說明如何完成。

![獎金挑戰——樣式系統](../assets/style-cif-component/bonus-challenge.png)

## 其他資源 {#additional-resources}

* [AEM 專案原型](https://github.com/adobe/aem-project-archetype)
* [AEMCIF核心元件](https://github.com/adobe/aem-core-cif-components)
* [建立當地開發AEM環境](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)
* [用戶端資源庫](/help/sites-developing/clientlibs.md)
* [開始使用AEM Sites](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)
* [用體制發展](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html)
