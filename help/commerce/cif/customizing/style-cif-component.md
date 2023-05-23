---
title: 樣式AEMCIF核心元件
description: 瞭解如何設AEM置CIF核心元件的樣式。 本教程介紹如何使用客戶端庫或客戶端庫為Adobe Experience Manager(AEM)Commerce實現部署和管理CSS和Javascript。 本教程還將介紹如何將ui.frontend模組和webpack項目整合到端到端構建流程中。
sub-product: Commerce
topics: Development
version: Cloud Service
doc-type: tutorial
feature: Commerce Integration Framework
kt: 3456
thumbnail: 3456-style-cif.jpg
exl-id: 04d553be-c67d-4ecb-a23f-2694c2adfc2b
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '2551'
ht-degree: 2%

---

# 樣式AEMCIF核心元件 {#style-aem-cif-core-components}

的 [CIF韋尼亞項目](https://github.com/adobe/aem-cif-guides-venia) 是用於使用的參考代碼庫 [CIF核心元件](https://github.com/adobe/aem-core-cif-components)。 在本教程中，您將檢查Venia參考項目，並瞭解CIF核心元件使用的CSSAEM和JavaScript的組織方式。 您還將使用CSS建立新樣式以更新 **產品預告** 元件。

>[!TIP]
>
>使用 [項AEM目原型](https://github.com/adobe/aem-project-archetype) 啟動您自己的商業實施。

## 您將構建的

在本教程中，將為類似於卡的產品預告元件實施新樣式。 本教程中的經驗教訓可應用於其他CIF核心元件。

![您將構建的](../assets/style-cif-component/what-you-will-build.png)

## 必備條件 {#prerequisites}

完成本教程需要本地開發環境。 這包括已配置並AEM連接到Adobe Commerce實例的運行實例。 查看 [建立地方開發AEM](../develop.md)。

## 克隆Venia項目 {#clone-venia-project}

我們將克隆 [韋尼亞計畫](https://github.com/adobe/aem-cif-guides-venia) 然後覆蓋預設樣式。

>[!NOTE]
>
>**可以自由使用現有項目** (基於包含CIFAEM的項目原型)並跳過此部分。

1. 運行以下git命令以克隆項目：

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. 將項目構建並部署到以下的本地實AEM例：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. 添加必要的OSGi配置，將實AEM例連接到Adobe Commerce實例或將配置添加到新建立的項目。

1. 此時，您應具有連接到Adobe Commerce實例的店面的工作版本。 導航到 `US` > `Home` 頁： [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

   您應看到店面當前正在使用Venia主題。 展開店面的「主菜單」，您應看到各種類別，表明與Adobe Commerce的連接正在工作。

   ![配置Venia主題的店面](../assets/style-cif-component/venia-store-configured.png)

## 客戶端庫和ui.frontend模組 {#introduction-to-client-libraries}

負責呈現庫面主題/樣式的CSS和JavaScript由AEM [客戶端庫](/help/sites-developing/clientlibs.md) 或客戶端。 客戶端庫提供一種機制，用於在項目代碼中組織CSS和Javascript，然後將其傳遞到頁面。

通過添加和覆蓋由這些客AEM戶端庫管理的CSS，可將特定品牌樣式應用於CIF核心元件。 瞭解客戶端庫的結構和包含方式至關重要。

的 [ui.frontend](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/uifrontend.html) 是 [網路包](https://webpack.js.org/) 管理項目的所有前端資產。 這允許前端開發人員使用任意數量的語言和技術，如 [類型指令碼](https://www.typescriptlang.org/)。 [薩斯](https://sass-lang.com/) 還有更多。

的 `ui.frontend` 模組也是Maven模組，通過NPM模組與大型項目整合 [aem-clientlib生成器](https://github.com/wcm-io-frontend/aem-clientlib-generator)。 在構建期間， `aem-clientlib-generator` 將編譯的CSS和JavaScript檔案複製到 `ui.apps` 中。

![ui.frontendui.apps體系結構](../assets/style-cif-component/ui-frontend-architecture.png)

*編譯後的CSS和Javascript從 `ui.frontend` 模組 `ui.apps` 模組作為Maven生成期間的客戶端庫*

## 更新預告樣式 {#ui-frontend-module}

接下來，對「預告」樣式進行小小更改，以瞭解 `ui.frontend` 模組和客戶端庫工作。 使用 [您選擇的IDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide) 來修改標籤元素的屬性。 使用的螢幕截圖來自 [Visual Studio代碼IDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code)。

1. 導航並展開 **ui.frontend** 將資料夾層次結構展開到： `ui.frontend/src/main/styles/commerce`:

   ![ui.frontend商業資料夾](../assets/style-cif-component/ui-frontend-commerce-folder.png)

   請注意有多個Sas(`.scss`)檔案。 這些是每個Commerce元件的Commerce特定樣式。

1. 開啟檔案 `_productteaser.scss`。

1. 更新 `.item__image` 規則和修改邊框規則：

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

   上述規則應在「產品預告元件」中添加一個非常粗體的粉紅色邊框。

1. 開啟新的終端窗口並導航到 `ui.frontend` 資料夾：

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

   Inspect終端輸出。 您將看到Maven命令執行了幾個NPM指令碼，包括 `npm run build`。 的 `npm run build` 命令在 `package.json` 具有編譯webpack項目和觸發客戶端庫生成的效果。

1. Inspect檔案 `ui.frontend/dist/clientlib-site/site.css`:

   ![已編譯站點CSS](../assets/style-cif-component/comiled-site-css.png)

   該檔案是項目中所有Sass檔案的編譯和精簡版本。

   >[!NOTE]
   >
   >此類檔案將從原始碼管理中忽略，因為它們應在生成時生成。

1. Inspect檔案 `ui.frontend/clientlib.config.js`。

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

   這是 [aem-clientlib生成器](https://github.com/wcm-io-frontend/aem-clientlib-generator) 並確定編譯後的CSS和JavaScript將轉換到客戶端庫的位AEM置和方式。

1. 在 `ui.apps` 模組檢查檔案： `ui.apps/src/main/content/jcr_root/apps/venia/clientlibs/clientlib-site/css/site.css`:

   ![ui.apps中已編譯的站點CSS](../assets/style-cif-component/comiled-css-ui-apps.png)

   這會複製 `site.css` 檔案 `ui.apps` 項目。 它現在是名為 `clientlib-site` 具有 `venia.site`。 一旦檔案是 `ui.apps` 模組可以部署到AEM。

   >[!NOTE]
   >
   >此類檔案也會從原始碼管理中忽略，因為它們應在生成時生成。

1. 接下來檢查項目生成的其他客戶端庫：

   ![其他客戶端庫](../assets/style-cif-component/other-clientlibs.png)

   這些客戶端庫不由 `ui.frontend` 中。 相反，這些客戶端庫包括Adobe提供的CSS和JavaScript依賴項。 這些客戶端庫的定義位於 `.content.xml` 資料夾下。

   **客戶端庫**  — 這是一個空的客戶端庫，它只是嵌入了 [核AEM心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)。 類別為 `venia.base`。

   **客戶端庫**  — 這也是一個空的客戶端庫，它只是嵌入了 [AEMCIF核心元件](https://github.com/adobe/aem-core-cif-components)。 類別為 `venia.cif`。

   **客戶機庫網格**  — 這包括啟用響應網格功AEM能所需的CSS。 使用網AEM格啟用 [佈局模式](/help/sites-authoring/responsive-layout.md) 使內容作AEM者能夠重新調整元件的大小。 類別為 `venia.grid` 嵌入 `venia.base` 的下界。

1. Inspect檔案 `customheaderlibs.html` 和 `customfooterlibs.html` 下 `ui.apps/src/main/content/jcr_root/apps/venia/components/page`:

   ![自定義頁眉和頁腳指令碼](../assets/style-cif-component/custom-header-footer-script.png)

   這些指令碼包括 **venia.base** 和 **韋尼亞語** 庫作為所有頁面的一部分。

   >[!NOTE]
   >
   >只有基庫作為頁面指令碼的一部分被「硬編碼」。 `venia.site` 不包括在這些檔案中，而是作為頁面模板的一部分包含在其中，以提高靈活性。 稍後會檢查。

1. 從終端，將整個項目構建並部署到以下的本地實AEM例：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

## 製作產品預告 {#author-product-teaser}

現在已部署了代碼更新，請使用創作工具將產品預告元件的新實例添加到站點的AEM首頁。 這將允許我們查看更新的樣式。

1. 開啟新瀏覽器頁籤並導航到 **首頁** 地址欄： [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

1. 展開中的Asset Finder（側欄） **編輯** 的子菜單。 將「資產」篩選器切換為 **產品**。

   ![展開資產查找器並按產品篩選](../assets/style-cif-component/drag-drop-product-page.png)

1. 將新產品拖放到主佈局容器的首頁上：

   ![帶粉紅色邊框的產品預告](../assets/style-cif-component/pink-border-product-teaser.png)

   您應看到「產品預告」現在具有基於先前建立的CSS規則更改的亮粉色邊框。

## 驗證頁面上的客戶端庫 {#verify-client-libraries}

接下來，驗證該頁面中是否包含客戶端庫。

1. 導航到 **首頁** 地址欄： [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

1. 選擇 **頁面資訊** 的 **查看為已發佈**:

   ![以已發佈狀態檢視](../assets/style-cif-component/view-as-published.png)

   此操作將在未載入任何作者javascriptAEM的情況下開啟該頁面，因為該頁面將顯示在發佈的站點上。 請注意，URL具有查詢參數 `?wcmmode=disabled` 已附加。 在開發CSS和Javascript時，最好使用此參數來簡化頁面，而無需作者提供任AEM何內容。

1. 查看頁面源，您應該能夠識別其中包含的幾個客戶端庫：

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

   將客戶端庫傳送到頁面時使用前置詞 `/etc.clientlibs` 通過 [代理](/help/sites-developing/clientlibs.md) 避免暴露任何敏感資訊 `/apps` 或 `/libs`。

   通知 `venia/clientlibs/clientlib-site.min.css` 和 `venia/clientlibs/clientlib-site.min.js`。 這些是從 `ui.frontend` 中。

## 包含頁面模板的客戶端庫 {#client-library-inclusion-pagetemplates}

有關如何包括客戶端庫的選項有幾個。 接下來檢查生成的項目如何包括 `clientlib-site` 庫 [頁面模板](/help/sites-developing/templates.md)。

1. 導航到 **首頁** 編輯器中的站AEM點： [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

1. 選擇 **頁面資訊** 的 **編輯模板**:

   ![編輯模板](../assets/style-cif-component/edit-template.png)

   這將開啟 **登錄頁** 模板 **首頁** 頁面。

   >[!NOTE]
   >
   >要從「開始」螢幕查看所有可用AEM模板，請導航至 **工具** > **常規** > **模板**。

1. 在左上角，選擇 **頁面資訊** 表徵圖 **頁面策略**。

   ![頁面策略菜單項](../assets/style-cif-component/page-policy-menu.png)

1. 這將開啟登錄頁模板的頁面策略：

   ![頁面策略 — 登錄頁](../assets/style-cif-component/page-policy-properties.png)

   在右側，您可以看到客戶端庫的清單 **類別** 將包含在使用此模板的所有頁面上。

   * `venia.dependencies`  — 提供任何供應商庫 `venia.site` 取決於。
   * `venia.site`  — 這是 `clientlib-site` 那個 `ui.frontend` 模組生成。

   請注意，其他模板使用相同的策略， **內容頁**。 **登錄頁**&#x200B;等等。 通過重新使用同一策略，我們可以確保所有頁面都包含相同的客戶端庫。

   使用模板和頁面策略管理包含客戶端庫的好處是您可以更改每個模板的策略。 例如，您可能在同一實例中管理兩個不同的AEM品牌。 每個品牌都有其獨特的風格或 *主題* 但基本庫和代碼是相同的。 另一個示例是，如果您有一個較大的客戶端庫，而您只想在某些頁面上顯示，則可以僅針對該模板制定一個唯一的頁面策略。

## 本地WebPack開發 {#local-webpack-development}

在上一練習中，已對 `ui.frontend` 模組，然後在執行Maven生成後，將更改部署到AEM。 接下來，我們將研究利用webpack-dev-server快速開發前端樣式。

Webpack-dev-server代理映像和來自的本地實例的某些CSS/JavaScript,AEM但允許開發人員修改 `ui.frontend` 中。

1. 在瀏覽器中導航到 **首頁** 頁面和 **查看為已發佈**: [http://localhost:4502/content/venia/us/en.html?wcmmode=disabled](http://localhost:4502/content/venia/us/en.html?wcmmode=disabled)。

1. 查看頁面的源和 **複製** 頁面的原始HTML。

1. 返回到您選擇的IDE，位於 `ui.frontend` 模組開啟檔案： `ui.frontend/src/main/static/index.html`

   ![靜態HTML檔案](../assets/style-cif-component/static-index-html.png)

1. 覆蓋 `index.html` 和 **貼上** HTML在上一步中複製。

1. 查找的包含 `clientlib-site.min.css`。 `clientlib-site.min.js` 和 **刪除** 他們。

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

   刪除這些檔案是因為它們代表由 `ui.frontend` 中。 保留其他客戶端庫，因為它們將從正在運行的實例中AEM代理。

1. 開啟新的終端窗口並導航到 `ui.frontend` 的子菜單。 運行命令 `npm start`:

   ```shell
   $ cd ui.frontend
   $ npm start
   ```

   這將在上啟動webpack-dev-server [http://localhost:8080/](http://localhost:8080/)

   >[!CAUTION]
   >
   >如果遇到與Sass相關的錯誤，請停止伺服器並運行該命令 `npm rebuild node-sass` 重複上述步驟。 如果您的 `npm` 和 `node` 在項目中指定 `aem-cif-guides-venia/pom.xml`。

1. 導航到 [http://localhost:8080/](http://localhost:8080/) 的子常式。AEM 您應通過webpack-dev-server查看Venia首頁：

   ![埠80上的Webpack Dev伺服器](../assets/style-cif-component/webpack-dev-server-port80.png)

   使webpack-dev-server保持運行。 下次演習將使用。

## 實現產品預告卡樣式 {#update-css-product-teaser}

下一步，修改 `ui.frontend` 模組，用於為產品預告器實現卡樣式。 webpack-dev-server將用於快速查看更改。

返回到IDE和生成的項目。

1. 在 **ui.frontend** 模組重新開啟檔案 `_productteaser.scss` 在 `ui.frontend/src/main/styles/commerce/_productteaser.scss`。

1. 對「產品預告」邊框進行以下更改：

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

   保存更改，webpack-dev-server應使用新樣式自動刷新。

1. 添加投影並將圓角包括到「產品預告」中。

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

1. 更新產品名稱以顯示在預告的底部，並修改文本顏色。

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

1. 更新產品的價格，使其也顯示在預告的底部，並修改文本顏色。

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

1. 更新底部的介質查詢，以將名稱和價格堆放在小於 **992px**。

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

   現在，您應看到webpack-dev-server中反映的卡式：

   ![Webpack開發伺服器預告更改](../assets/style-cif-component/webpack-dev-server-teaser-changes.png)

   但是，尚未部署更改AEM。 您可以下載 [解決方案檔案](../assets/style-cif-component/_productteaser.scss)。

1. 從命令行終AEM端將更新部署到使用Maven技能：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

   >[!NOTE]
   >還有 [IDE設定和工具](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/set-up-a-local-aem-development-environment.html#set-up-an-integrated-development-environment) 它可以直接將項目檔案同步到AEM本地實例，而無需執行完整的Maven生成。

## 查看更新的產品預告 {#view-updated-product-teaser}

在將項目代碼部署到後AEM，我們現在應該能夠看到對產品預告所做的更改。

1. 返回到瀏覽器並重新刷新首頁： [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。 您應看到已應用的更新產品預告樣式。

   ![更新的產品預告樣式](../assets/style-cif-component/product-teaser-new-style.png)

1. 通過添加附加產品預告器進行實驗。 使用佈局模式可更改元件的寬度和偏移，以便在一行中顯示多個預告。

   ![多個產品預告器](../assets/style-cif-component/multiple-teasers-final.png)

## 疑難排解 {#troubleshooting}

您可以在 [CRXDE-Lite](http://localhost:4502/crx/de/index.jsp) 已部署更新的CSS檔案： [http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css](http://localhost:4502/crx/de/index.jsp#/apps/venia/clientlibs/clientlib-site/css/site.css)

在部署新的CSS和/或JavaScript檔案時，確保瀏覽器不提供陳舊檔案也很重要。 您可以通過清除瀏覽器快取或啟動新的瀏覽器會話來消除此問題。

還嘗AEM試快取客戶端庫以獲得效能。 偶爾，在代碼部署後，會提供較舊的檔案。 可以使用 [重建客戶端庫工具](http://localhost:4502/libs/granite/ui/content/dumplibs.rebuild.html)。 *如果懷疑已快取了舊版本的客戶AEM端庫，則首選方法是無效快取。 重建庫效率低下且耗時。*

## 恭喜 {#congratulations}

您剛剛設定了第AEM一個CIF核心元件，並且使用了webpack dev伺服器！

## 獎金挑戰 {#bonus-challenge}

使用 [樣AEM式系統](/help/sites-authoring/style-system.md) 建立兩個可由內容作者開啟/關閉的樣式。 [以體制發展](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/style-system.html) 包括詳細步驟和有關如何完成此操作的資訊。

![獎金挑戰 — 樣式系統](../assets/style-cif-component/bonus-challenge.png)

## 其他資源 {#additional-resources}

* [AEM 專案原型](https://github.com/adobe/aem-project-archetype)
* [AEMCIF核心元件](https://github.com/adobe/aem-core-cif-components)
* [設定本地開發AEM環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html?lang=zh-Hant)
* [用戶端資源庫](/help/sites-developing/clientlibs.md)
* [AEM Sites入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant)
* [以體制發展](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/style-system.html)
