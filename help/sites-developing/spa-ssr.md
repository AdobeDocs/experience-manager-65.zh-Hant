---
title: SPA和伺服器端轉譯
description: 瞭解Adobe Experience Manager中的SPA和伺服器端轉譯。
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: a80bc883-e0f6-4714-bd28-108262f96d77
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1659'
ht-degree: 1%

---

# SPA和伺服器端轉譯{#spa-and-server-side-rendering}

>[!NOTE]
>
>對於需要以SPA框架為基礎的使用者端轉譯(例如React或Angular)專案，建議使用SPA編輯器解決方案。

>[!NOTE]
>
>如本檔案所述，需要Adobe Experience Manager (AEM) 6.5.1.0或更新版本才能使用SPA伺服器端轉譯功能。

## 概觀 {#overview}

單頁應用程式(SPA)可為使用者提供豐富的動態體驗，以熟悉的方式反應和行為，通常就像原生應用程式一樣。 [這是透過依賴使用者端先載入內容，然後進行處理使用者互動的繁重工作來達成](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work) 並藉此將使用者端與伺服器之間所需的通訊量降到最低，讓應用程式更具反應性。

不過，這可能會導致較長的初始載入時間，尤其是當SPA較大且內容豐富時。 為了最佳化載入時間，部分內容可以在伺服器端轉譯。 使用伺服器端轉譯(SSR)可以加速頁面的初始載入，然後將進一步的轉譯傳遞給使用者端。

## 何時使用SSR {#when-to-use-ssr}

並非所有專案都需要SSR。 雖然AEM完全支援適用於SPA的JS SSR，但Adobe不建議將其系統地實作到每個專案。

決定實作SSR時，您必須先估計增加SSR對專案實際代表的其他複雜性、工作量和成本，包括長期維護。 只有在增加值明顯超過預估成本時，才應選擇SSR架構。

SSR通常會在下列任一問題明確為「是」時提供某些值：

* **SEO：** 您的網站是否仍需要SSR，才能讓帶來流量的搜尋引擎正確編制索引？ 請記住，主要搜尋引擎編目程式現在會評估JS。
* **頁面速度：** SSR是否能在真實環境中提供可衡量的速度提升，並增加整體使用者體驗？

只有當這兩個問題中至少有一個問題得到明確的「是」回答時，Adobe才會建議實作SSR。 以下幾節將說明如何使用Adobe I/O Runtime執行此操作。

## Adobe I/O Runtime {#adobe-i-o-runtime}

如果您 [確信您的專案需要實作SSR](/help/sites-developing/spa-ssr.md#when-to-use-ssr)，Adobe建議的解決方案是使用Adobe I/O Runtime。

如需Adobe I/O Runtime的詳細資訊，請參閱下列內容：

* [https://developer.adobe.com/runtime/](https://developer.adobe.com/runtime/)  — 服務概述
* [https://developer.adobe.com/runtime/docs/](https://developer.adobe.com/runtime/docs/)  — 以取得平台的詳細檔案

以下章節詳細說明如何使用Adobe I/O Runtime在兩種不同的模型中為您的SPA實作SSR：

* [AEM導向的通訊流程](/help/sites-developing/spa-ssr.md#aem-driven-communication-flow)
* [Adobe I/O Runtime導向的通訊流程](/help/sites-developing/spa-ssr.md#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe建議每個環境使用個別的Adobe I/O Runtime工作區（預備、生產、測試等）。 這允許典型的系統開發生命週期(SDLC)模式，以及部署至不同環境的單一應用程式不同版本。 檢視檔案 [Project App Builder應用程式的CI/CD](https://developer.adobe.com/app-builder/docs/guides/deployment/ci_cd_for_firefly_apps/) 以取得詳細資訊。
>
>除非每個執行個體型別的執行階段實施有所差異，否則不需要為每個執行個體（作者、發佈）使用個別的工作區。

## 遠端轉譯器設定 {#remote-renderer-configuration}

AEM必須知道可在何處擷取遠端呈現的內容。 不論 [您選擇為SSR實作的模型、](#adobe-i-o-runtime)，您必須向AEM指定如何存取此遠端轉譯服務。

這可透過以下方式完成 **RemoteContentRenderer — 設定工廠OSGi服務**. 在的Web主控台設定主控台中搜尋字串「RemoteContentRenderer」 `http://<host>:<port>/system/console/configMgr`.

![轉譯器設定](assets/rendererconfig.png)

下列欄位可供設定使用：

* **內容路徑模式**  — 必要時，比對部分內容的規則運算式
* **遠端端點URL**  — 負責產生內容的端點URL
   * 若不在本機網路中，請使用安全的HTTPS通訊協定。
* **其他請求標頭**  — 要新增至傳送至遠端端點之要求的其他標頭
   * 模式： `key=value`
* **請求逾時**  — 遠端主機要求逾時（毫秒）

>[!NOTE]
>
>無論您是否選擇實施 [AEM導向的通訊流程](#aem-driven-communication-flow) 或 [Adobe I/O Runtime驅動的流量，](#adobe-i-o-runtime-driven-communication-flow) 您必須定義遠端內容轉譯器設定。
>
>如果您選擇要 [使用自訂Node.js伺服器。](#using-node-js)

>[!NOTE]
>
>此設定使用 [遠端內容轉譯器、](#remote-content-renderer) 有其他擴充功能和自訂選項。

## AEM導向的通訊流程 {#aem-driven-communication-flow}

使用SSR時， [元件互動工作流程](/help/sites-developing/spa-overview.md#workflow) AEM中的SPA包含在Adobe I/O Runtime上產生應用程式初始內容的階段。

1. 瀏覽器向AEM要求SSR內容。

1. AEM會將模型發佈至Adobe I/O Runtime。

1. Adobe I/O Runtime會傳回產生的內容。

1. AEM透過後端頁面元件的HTL範本，提供Adobe I/O Runtime傳回的HTML。

![server-side-rendering-cms-drivenaemnode-adobeio](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

## Adobe I/O Runtime導向的通訊流程 {#adobe-i-o-runtime-driven-communication-flow}

上一節將說明有關AEM中SPA之伺服器端轉譯的標準與建議實作，AEM在此會執行內容的自訂與提供。

或者，您也可以實作SSR，讓Adobe I/O Runtime負責啟動程式，有效反轉通訊流程。

這兩種模式都有效，並受到AEM支援。 不過，在實作特定模型之前，您應該先考量各別的優缺點。

<table>
 <tbody>
  <tr>
   <th><strong>Bootstrapping</strong></th>
   <th><strong>優點</strong></th>
   <th><strong>缺點</strong></th>
  </tr>
  <tr>
   <th><strong>透過AEM</strong><br /> </th>
   <td>
    <ul>
     <li>AEM會視需要管理插入程式庫</li>
     <li>僅在AEM上維護資源<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>SPA開發人員可能不熟悉<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>透過Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>SPA開發人員更熟悉<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>AEM開發人員必須透過以下方式讓應用程式所需的Clientlib資源（例如CSS和JavaScript）可供使用： <code><a href="/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet">allowProxy</a></code> 屬性<br /> </li>
     <li>資源必須在AEM和Adobe I/O Runtime之間同步<br /> </li>
     <li>若要啟用SPA的製作功能，可能需要Adobe I/O Runtime的Proxy伺服器</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 計畫SSR {#planning-for-ssr}

只有部分應用程式必須呈現在伺服器端。 常見的範例是，在頁面初始載入時，顯示在摺疊上方的內容會在伺服器端轉譯。 這可傳送給使用者端已轉譯的內容，以節省時間。 當使用者與SPA互動時，其他內容會由使用者端轉譯。

當您考慮為SPA實作伺服器端轉譯時，請檢閱應用程式的哪些部分有必要。

## 使用SSR開發SPA {#developing-an-spa-using-ssr}

SPA元件可由使用者端（在瀏覽器中）或伺服器端轉譯。 在轉譯伺服器端時，不會出現瀏覽器屬性，例如視窗大小和位置。 因此，SPA元件應同構，不對其呈現位置做任何假設。

若要使用SSR，請在AEM和Adobe I/O Runtime上部署您的程式碼，由伺服器端轉譯。 大部分的程式碼將相同，但伺服器特定的工作將有所不同。

## AEM中SPA的SSR {#ssr-for-spas-in-aem}

AEM中SPA的SSR需要Adobe I/O Runtime，此模組用於轉譯應用程式內容伺服器端。 在應用程式的HTL中，會呼叫Adobe I/O Runtime上的資源來呈現內容。

就像AEM可立即支援Angular和React SPA架構一樣，Angular和React應用程式也支援伺服器端轉譯。 如需詳細資訊，請參閱這兩個架構的NPM檔案。

* React： [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* angular： [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/angular-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/angular-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

如需簡單化的範例，請參閱 [We.Retail日誌應用程式](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal). 它會呈現整個應用程式伺服器端。 雖然這不是真實世界的範例，但它的確說明了實施SSR所需的條件。

>[!CAUTION]
>
>此 [We.Retail日誌應用程式](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) 僅供示範之用，因此使用Node.js做為簡單範例，而非建議的Adobe I/O Runtime。 請勿將此範例用於任何專案工作。

>[!NOTE]
>
>任何 AEM 專案都應使用 [AEM 專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，它支援使用 React 或 Angular 的 SPA 專案並使用 SPA SDK。

## 使用Node.js {#using-node-js}

Adobe I/O Runtime是在AEM中為SPA實作SSR的建議解決方案。

對於內部部署AEM例項，也可以使用自訂Node.js例項以上述相同方式實作SSR。 雖然Adobe支援此功能，但不建議使用。

>[!NOTE]
>
>Adobe託管的AEM執行個體不支援Node.js。

>[!NOTE]
>
>如果必須透過Node.js實作SSR，Adobe建議為每個AEM環境（作者、發佈、階段等）個別建立Node.js例項。

## 遠端內容轉譯器 {#remote-content-renderer}

此 [遠端內容轉譯器設定](#remote-content-renderer-configuration) 在AEM中，若要搭配您的SPA使用SSR，就必須採用更廣范的轉譯服務，您可依照自己的需求加以擴充與自訂。

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` 是一項OSGi服務，用於擷取遠端伺服器上呈現的內容，例如從Adobe I/O轉譯。傳送至遠端伺服器的內容是根據傳遞的請求引數。

`RemoteContentRenderingService` 當需要額外的內容操作時，可以透過相依性反轉插入自訂Sling模型或servlet中。

此服務由內部使用 [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

此 `RemoteContentRendererRequestHandlerServlet` 可用於以程式設計方式設定請求設定。 `DefaultRemoteContentRendererRequestHandlerImpl`，此為提供的預設要求處理常式實作，可讓您建立多個OSGi設定以將內容結構中的位置對應至遠端端點。

若要新增自訂請求處理常式，請實作 `RemoteContentRendererRequestHandler` 介面。 請務必設定 `Constants.SERVICE_RANKING` component屬性至大於100的整數，也就是排序方式 `DefaultRemoteContentRendererRequestHandlerImpl`.

```
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### 設定預設處理常式的OSGi設定 {#configure-default-handler}

預設處理常式的設定必須依照一節中的說明進行設定 [遠端內容轉譯器設定](#remote-content-renderer-configuration).

### 遠端內容轉譯器使用情形 {#usage}

若要讓servlet擷取並傳回部分可插入頁面的內容：

1. 確定您的遠端伺服器可以存取。
1. 將下列其中一個片段新增至AEM元件的HTL範本。
1. 選擇性地建立或修改OSGi設定。
1. 瀏覽網站內容

通常，頁面元件的HTL範本是這類功能的主要收件者。

```
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### 要求 {#requirements}

此servlet會使用Sling模型匯出工具來序列化元件資料。 根據預設，兩者皆會 `com.adobe.cq.export.json.ContainerExporter` 和 `com.adobe.cq.export.json.ComponentExporter` 支援作為Sling模型介面卡。 如有必要，您可以新增類別，讓請求適應使用 `RemoteContentRendererServlet` 並實作 `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. 其他類別必須擴充 `ComponentExporter`.
