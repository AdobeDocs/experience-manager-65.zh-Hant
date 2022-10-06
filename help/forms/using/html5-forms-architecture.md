---
title: HTML5表單架構
seo-title: Architecture of HTML5 forms
description: HTML5表單在內嵌AEM例項內部署為套件，且會使用RESTful Apache Sling架構，以REST端點OVER HTTP/S的形式公開功能。
seo-description: HTML5 forms is deployed as a package within the embedded AEM instance and exposes the functionality as REST end point over HTTP/S using RESTful Apache Sling architecture.
uuid: 7f515cea-1447-4fc7-82ba-17f2e3f9f80c
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a644978e-5736-4771-918a-dfefe350a4a1
docset: aem65
feature: Mobile Forms
exl-id: ed8349a1-f761-483f-9186-bf435899df7d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2011'
ht-degree: 0%

---

# HTML5表單架構{#architecture-of-html-forms}

## 架構 {#architecture}

HTML5表單功能在內嵌AEM例項中部署為套件，且會使用RESTful透過HTTP/S公開為REST端點 [Apache Sling Architecture](https://sling.apache.org/).

![02-aem-forms-architecture_large](assets/02-aem-forms-architecture_large.jpg)

### 使用Sling Framework {#using-sling-framework}

[Apache Sling](https://sling.apache.org/) 以資源為中心。 它會使用請求URL來先解析資源。 每個資源都有 **sling:resourceType** (或 **sling:resourceSuperType**)屬性。 接著會根據此屬性、要求方法和要求URL的屬性，選取Sling指令碼來處理要求。 此Sling指令碼可以是JSP或Servlet。 HTML5表單， **設定檔** 節點可做為sling資源和 **描述檔轉譯器** 可做為sling指令碼，處理使用特定設定檔轉譯行動表單的請求。 A **描述檔轉譯器** 是JSP，可從要求讀取參數並呼叫Forms OSGi服務。

如需REST端點和支援請求參數的詳細資訊，請參閱 [轉譯表單範本](/help/forms/using/rendering-form-template.md).

當使用者從用戶端裝置(例如iOS或Android瀏覽器)提出請求時，Sling會先根據請求URL解析設定檔節點。 從此配置檔案節點，它讀取 **sling:resourceSuperType** 和 **sling:resourceType** 確定可處理此表單呈現請求的所有可用指令碼。 接著會使用Sling要求選取器搭配要求方法來識別最適合處理此要求的指令碼。 一旦請求達到設定檔轉譯器JSP,JSP就會呼叫Forms OSGi服務。

如需Sling指令碼解析度的詳細資訊，請參閱 [AEM Sling速查表](https://docs.adobe.com/content/docs/en/cq/current/developing/sling_cheatsheet.html) 或 [Apache Sling Url分解](https://sling.apache.org/site/url-decomposition.html).

#### 典型表單處理呼叫流程 {#typical-form-processing-call-flow}

HTML5表單會快取第一個請求處理表單（轉譯或提交）所需的所有中間物件。 它不會快取與資料相關的對象，因為這些對象可能會更改。

Mobile Form會維護兩個不同層級的快取，即PreRender快取和Render快取。 preRender快取包含解析的模板的所有片段和影像，而Render快取包含已呈現的內容，如HTML。

![HTML5表單工作流程](assets/cacheworkflow.png)

HTML5表單工作流程

HTML5表單不會快取缺少片段和影像參考的範本。 如果HTML5表單所花的時間超過正常時間，請檢查伺服器記錄檔中是否有遺漏的參考和警告。 另請確保未達到對象的最大大小。

Forms OSGi服務會以兩個步驟處理請求：

* **佈局和初始表單狀態生成**:Forms OSGi轉譯服務會呼叫Forms快取元件，判斷表單是否已快取且未失效。 如果表單已快取且有效，則會從快取中提供產生的HTML。 如果表單失效，Forms OSGi轉譯服務會以XML格式產生「初始表單配置」和「表單狀態」。 此XML會由Forms OSGi服務轉換為HTML配置和初始JSON表單狀態，然後快取以供後續請求使用。
* **預先填入的Forms**:轉譯時，如果使用者以預先填入的資料請求表單，Forms OSGi轉譯服務會呼叫Forms服務容器，並透過合併的資料產生新的表單狀態。 不過，由於配置已在上述步驟中產生，因此此呼叫比首次呼叫更快。 此呼叫只會執行資料合併，並對資料執行指令碼。

如果表單內有任何更新或使用的任何資產，表單快取元件會偵測到該更新，而該特定表單的快取失效。 Forms OSGi服務完成處理後，設定檔轉譯器jsp會將JavaScript程式庫參考和樣式新增至此表單，並將回應傳回給用戶端。 典型的Web伺服器，如 [Apache](https://httpd.apache.org/) 可在此處搭配HTML壓縮使用。 Web伺服器將顯著減少伺服器和客戶端電腦之間的資料流所需的響應大小、網路流量和時間。

使用者提交表單時，瀏覽器會將表單狀態以JSON格式傳送至 [提交服務代理](../../forms/using/service-proxy.md);然後，提交服務代理使用JSON資料生成資料XML，並提交該資料XML以提交端點。

## 元件 {#components}

您需要AEM Forms附加套件才能啟用HTML5表單。 如需安裝AEM Forms附加元件套件的詳細資訊，請參閱 [安裝和設定AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).

### OSGi元件(adobe-lc-forms-core.jar) {#osgi-components-adobe-lc-forms-core-jar}

**AdobeXFA Forms轉譯器(com.adobe.livecycle.adobe-lc-forms-core)** 是從Felix Admin Console的「套件檢視」(https://)檢視時，HTML5 forms OSGi套件組合的顯示名稱[主機]:[埠]/system/console/bundles)。

此元件包含用於呈現、快取管理和配置設定的OSGi元件。

#### Forms OSGi服務 {#forms-osgi-service}

此OSGi服務包含邏輯，可將XDP轉譯為HTML，並處理表單提交以產生資料XML。 此服務使用Forms服務容器。 Forms服務容器內部呼叫原生元件 `XMLFormService.exe` 執行處理。

如果收到轉譯請求，此元件會呼叫Forms服務容器，以產生配置和狀態資訊，並進一步處理以產生HTML和JSON表單DOM狀態。

此元件也負責從提交的表單狀態JSON產生資料XML。

#### 快取元件 {#cache-component}

HTML5表單使用快取來最佳化吞吐量和回應時間。 您可以配置快取服務的級別，以微調效能和空間利用率之間的權衡。

<table>
 <tbody>
  <tr>
   <th>快取策略</th>
   <th>說明</th>
  </tr>
  <tr>
   <td>無</td>
   <td>不快取對象<br /> </td>
  </tr>
  <tr>
   <td>保守</td>
   <td>僅快取在表單呈現前產生的中間成品，如包含內嵌片段和影像的範本</td>
  </tr>
  <tr>
   <td>攻擊性</td>
   <td>快取呈現的HTML內容<br /> 快取保守級別中快取的所有對象。<br /> <strong>附註</strong>:此策略會產生最佳效能，但會耗用更多記憶體來儲存快取的成品。</td>
  </tr>
 </tbody>
</table>

HTML5表單會使用LRU策略執行記憶體內快取。 如果快取策略設定為「無快取」，則不會建立快取，且現有快取資料（如果有）將被清除。 除快取策略外，您還可以配置記憶體內快取總大小，這有助於最大限制快取大小，如果超出限制範圍，則它將使用LRU模式釋放快取資源。

>[!NOTE]
>
>記憶體內快取在群集節點之間不共用。

#### 配置服務 {#configuration-service}

Configuration Service可調整HTML5表單的配置參數和快取設定。

若要更新這些設定，請前往CQ FelixAdmin Console(可於https://&lt;&#39;取得)[伺服器]:[埠]「/system/console/configMgr)，搜索並選擇「移動Forms配置」。

您可以使用配置服務配置快取大小或禁用快取。 您也可以使用「除錯選項」參數來啟用除錯功能。 如需對表單進行除錯的詳細資訊，請參閱 [調試HTML5表單](/help/forms/using/debug.md).

### 執行階段元件(adobe-lc-forms-runtime-pkg.zip) {#runtime-components-adobe-lc-forms-runtime-pkg-zip}

執行階段套件包含用於轉譯HTML表單的用戶端程式庫。

**運行時程式包提供的重要元件：**

#### 指令碼引擎 {#scripting-engine}

AdobeXFA實作支援兩種指令碼語言，以在表單中啟用使用者定義的邏輯執行：JavaScript和FormCalc。

HTMLForms的指令碼引擎是以JavaScript編寫，以支援這兩種語言的XFA指令碼API。

在呈現時，FormCalc指令碼會在伺服器上轉換為（和快取）JavaScript，對用戶或設計人員而言是透明的。

此指令碼引擎使用ECMAScript5的某些功能，如Object.defineProperty。 引擎/程式庫會以類別名稱的CQ用戶端程式庫傳送 **xfaforms.profile**. 也提供 **FormBridge API** 使外部門戶或應用能夠與表單交互。 使用FormBridge，外部應用程式可以以寫程式方式隱藏某些元素、獲取或設定其值，或更改其屬性。

如需詳細資訊，請參閱 [表單網橋](/help/forms/using/form-bridge-apis.md) 文章。

#### 版面引擎 {#layout-engine}

HTML5表單的版面配置和視覺方面以SVG1.1、jQuery、BackBone和CSS3功能為基礎。 在伺服器上生成並快取表單的初始外觀。 在客戶端上管理初始佈局的調整以及對表單佈局的任何進一步增量更改。 為此，Runtime套件包含以JavaScript撰寫且以jQuery/Backbone為基礎的版面引擎。 此引擎處理所有動態行為，如添加/刪除可重複實例、可增長對象佈局。 此版面引擎一次呈現一個表單。 最初，用戶僅查看一個頁面，水準捲動條僅佔第一頁。 不過，當使用者向下捲動時，下一頁會開始呈現。 此逐頁轉譯可縮短在瀏覽器中轉譯第一個頁面所需的時間，並增強可感知的表單效能。 此引擎/程式庫是CQ用戶端程式庫（具有類別名稱）的一部分 **xfaforms.profile**.

版面引擎也包含一組小工具集，用來從使用者擷取表單欄位的值。 這些小部件模型為 [jQuery UI介面工具集](https://api.jqueryui.com/jQuery.widget/) 執行某些額外合約，以便與版面引擎順暢地搭配運作。

有關Widget和相應合同的詳細資訊，請參閱 [HTML5表單的自訂介面工具集](/help/forms/using/introduction-widgets.md).

#### 樣式 {#styling}

與HTML元素相關聯的樣式會內嵌或根據內嵌的CSS區塊新增。 某些不依賴表單的常見樣式屬於CQ用戶端程式庫的一部分，其類別名稱為xfaforms.profile。

除了預設樣式屬性外，每個表單元素也包含根據元素類型、名稱和其他屬性的特定CSS類別。 使用這些類，您可以通過指定自己的CSS來重新設定元素的樣式。

有關預設樣式和類的詳細資訊，請參閱 [樣式簡介](/help/forms/using/css-styles.md).

#### 伺服器端指令碼和網站服務 {#server-side-script-and-web-services}

任何標籤為在伺服器上運行或標籤為調用Web服務（無論其標籤為執行的位置）的指令碼始終在伺服器上執行。

客戶端指令碼引擎：

1. 以JSON形式同步呼叫傳遞目前表單狀態的伺服器
1. 在伺服器上執行指令碼或Web服務
1. 產生新的JSON狀態
1. 傳回回應時，合併用戶端上的新JSON狀態。

#### 本地化資源包 {#localization-resource-bundles}

HTML5表單支援義大利文(it)、西班牙文(es)、巴西葡萄牙文(pt_BR)、簡體中文(zh_CN)、繁體中文（僅支援）(zh_TW)、韓文(ko_KR)、英語(en_US)、法語(fr_FR)、德語(de_DE)和日語(ja)語言。 根據在請求標題中收到的區域設定，將相應的資源包發送到客戶端。 此資源包將作為CQ客戶端庫（具有類別名稱）添加到配置檔案JSP中 **xfaforms.I18N**. 您可以覆蓋在配置檔案中提取地區包的邏輯。

### Sling元件(adobe-lc-forms-content-pkg.zip) {#sling-components-adobe-lc-forms-content-pkg-zip}

Sling套件包含與設定檔和設定檔轉譯器相關的內容。

#### 設定檔 {#profiles}

設定檔是Sling中代表表單或Forms系列的資源節點。 在CQ層級，這些設定檔是JCR節點。 節點位於 **/content** 資料夾（位於JCR存放庫中），且可位於 **/content** 檔案夾。

#### 設定檔轉譯者 {#profile-renderers}

「配置檔案」節點具有屬性 **sling:resourceSuperType** 值 **xfaforms/設定檔**. 此屬性會內部傳送轉送要求至位於 **/libs/xfaforms/profile** 檔案夾。 這些指令碼是JSP頁，它們是將HTML表單和所需的JS/CSS對象放在一起的容器。 這些頁面包含下列項目的參考：

* **xfaforms.I18N。&lt;locale>**:此程式庫包含本地化資料。
* **xfaforms.profile**:此程式庫包含XFA指令碼和版面引擎的實作。

這些程式庫會模型化為CQ用戶端程式庫，其優點是可自動串連、縮制及壓縮CQ架構JavaScript程式庫。
如需CQ用戶端Lib的詳細資訊，請參閱 [CQ Clientlib檔案](https://docs.adobe.com/docs/en/cq/current/developing/components/clientlibs.html).

如上所述，設定檔轉譯器JSP會透過sling include呼叫Forms服務。 此JSP還根據管理員配置或請求參數設定各種調試選項。

HTML5表單可讓開發人員建立設定檔和描述檔轉譯器，以自訂表單的外觀。 例如，HTML表單可讓開發人員將表單整合至面板或 &lt;div> 區段(位於現有HTML入口網站的區段)。
如需建立自訂設定檔的詳細資訊，請參閱 [建立自訂設定檔](/help/forms/using/custom-profile.md).
