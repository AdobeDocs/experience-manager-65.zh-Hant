---
title: SPA和伺服器端轉譯
seo-title: SPA and Server-Side Rendering
description: "SPA與伺服器端轉譯"
seo-description: null
uuid: 27e26e3f-65d4-4069-b570-58b8b9e2a1ae
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 844e5c96-2a18-4869-b4c8-2fb9efe0332a
docset: aem65
exl-id: a80bc883-e0f6-4714-bd28-108262f96d77
source-git-commit: f923a3b7d6821f63d059f310de783b11bf3e8ec3
workflow-type: tm+mt
source-wordcount: '1751'
ht-degree: 2%

---

# SPA和伺服器端轉譯{#spa-and-server-side-rendering}

>[!NOTE]
>
>若專案需要SPA架構的用戶端轉譯(例如React或Angular),SPA Editor是建議的解決方案。

>[!NOTE]
>
>AEM 6.5.1.0或更新版本是使用SPA伺服器端轉譯功能的必要條件，如本檔案所述。

## 概觀 {#overview}

單頁應用程式(SPA)可為使用者提供豐富的動態體驗，以熟悉的方式回應和運作，通常就像原生應用程式。 [這是通過依靠客戶端將內容預先載入，然後進行用戶交互的繁重提升來實現的](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work) 從而將客戶端與伺服器之間所需的通訊量降至最低，使應用程式更具反應性。

不過，這可能會導致較長的初始載入時間，尤其是如果SPA很大且內容豐富。 為了最佳化載入時間，某些內容可在伺服器端轉譯。 使用伺服器端轉譯(SSR)可以加速頁面的初始載入，然後將轉譯傳遞給用戶端。

## 何時使用SSR {#when-to-use-ssr}

並非所有項目都需要SSR。 雖然AEM完全支援SPA適用的JS SSR，但Adobe不建議針對每個專案系統實作。

在決定實施SSR時，首先必須估計SSR的實際代表是什麼額外的複雜性、工作量和成本增加，包括長期維護。 只有當增值明顯超過估計成本時，才應選擇SSR架構。

SSR通常在下列任一問題都有明確的「是」時提供一些值：

* **SEO:** 您的網站是否仍需要SSR才能由帶來流量的搜尋引擎正確編列索引？ 請記住，主要搜尋引擎編目程式現在會評估JS。
* **頁面速度：** SSR是否在真實環境中提供了可衡量的速度改進，並增加了總體用戶體驗？

只有在這兩個問題中至少有一個以明確的「是」回答，您的專案才會Adobe建議實作SSR。 以下各節將說明如何使用Adobe I/O Runtime執行此作業。

## Adobe I/O Runtime {#adobe-i-o-runtime}

若您 [確信您的項目需要實施SSR](/help/sites-developing/spa-ssr.md#when-to-use-ssr),Adobe的建議解決方案是使用Adobe I/O Runtime。

如需Adobe I/O Runtime的詳細資訊，請參閱

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html)  — 服務概觀
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html)  — 如需有關平台的詳細檔案

以下幾節將詳細說明如何使用Adobe I/O Runtime，在兩種不同的模型中為SPA實作SSR:

* [AEM導向的通訊流程](/help/sites-developing/spa-ssr.md#aem-driven-communication-flow)
* [Adobe I/O Runtime驅動的通訊流](/help/sites-developing/spa-ssr.md#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe建議每個環境（預備、生產、測試等）分別使用Adobe I/O Runtime工作區。 這允許典型的系統開發生命週期(SDLC)模式，將不同版本的單個應用程式部署到不同的環境。 請參閱檔案 [專案應用程式產生器應用程式的CI/CD](https://developer.adobe.com/app-builder/docs/guides/deployment/ci_cd_for_firefly_apps/) 以取得更多資訊。
>
>每個例項（製作、發佈）不需要個別的工作區，除非每個例項類型在執行階段實施中有差異。

## 遠程轉譯器配置 {#remote-renderer-configuration}

AEM必須知道可在何處擷取遠端轉譯的內容。 無論 [您選擇對SSR實施的模型，](#adobe-i-o-runtime) 您需要指定AEM如何存取此遠端呈現服務。

這是透過 **RemoteContentRenderer — 配置工廠OSGi服務**. 在Web控制台配置控制台中搜索字串&quot;RemoteContentRenderer&quot;(位於 `http://<host>:<port>/system/console/configMgr`.

![轉譯器配置](assets/rendererconfig.png)

下列欄位適用於設定：

* **內容路徑模式**  — 必要的規則運算式，以匹配部分內容
* **遠端端點URL**  — 負責產生內容的端點URL
   * 如果本地網路中沒有，請使用安全的HTTPS協定。
* **其他請求標題**  — 要新增至傳送至遠端端點之請求的其他標題
   * 模式: `key=value`
* **請求逾時**  — 遠程主機請求超時（毫秒）

>[!NOTE]
>
>無論您是否選擇實作 [AEM驅動的通信流](#aem-driven-communication-flow) 或 [Adobe I/O Runtime驅動的流，](#adobe-i-o-runtime-driven-communication-flow) 您必須定義遠端內容轉譯器設定。
>
>如果您選擇 [使用自訂Node.js伺服器。](#using-node-js)

>[!NOTE]
>
>此設定會利用 [遠端內容轉譯器、](#remote-content-renderer) 其他擴充功能和自訂選項可供使用。

## AEM導向的通訊流程 {#aem-driven-communication-flow}

使用SSR時， [元件交互工作流](/help/sites-developing/spa-overview.md#workflow) 的SPA包含在Adobe I/O Runtime上產生應用程式初始內容的階段。

1. 瀏覽器會向AEM要求SSR內容。

1. AEM會將模型發佈至Adobe I/O Runtime。

1. Adobe I/O Runtime會傳回產生的內容。

1. AEM會透過後端頁面元件的HTL範本，提供Adobe I/O Runtime傳回的HTML。

![伺服器端轉譯 — cms-drivenaemnode-adobeio](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

## Adobe I/O Runtime驅動的通訊流 {#adobe-i-o-runtime-driven-communication-flow}

上一節將說明針對AEM中的SPA而執行伺服器端轉譯的標準和建議實作，AEM會執行內容的引導及服務。

或者，SSR可以實現，使Adobe I/O Runtime負責引導，有效地逆轉通信流。

這兩種模型均有效，且受AEM支援。 然而，在實施特定模式之前，應考慮每種模式的利弊。

<table>
 <tbody>
  <tr>
   <th><strong>引導</strong></th>
   <th><strong>優點</strong></th>
   <th><strong>缺點</strong></th>
  </tr>
  <tr>
   <th><strong>透過AEM</strong><br /> </th>
   <td>
    <ul>
     <li>AEM會視需要管理注入程式庫</li>
     <li>只需在AEM上維護資源<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>可能不熟悉SPA開發人員<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>透過Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>更熟悉SPA開發人員<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>應用程式所需的Clientlib資源（例如CSS和JavaScript）將需要由AEM開發人員透過 <code><a href="/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet">allowProxy</a></code> 屬性<br /> </li>
     <li>必須在AEM和Adobe I/O Runtime之間同步資源<br /> </li>
     <li>若要啟用SPA的編寫功能，可能需要Adobe I/O Runtime的代理伺服器</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## SSR規劃 {#planning-for-ssr}

通常，只有應用程式的一部分需要呈現在伺服器端。 常見的範例是，在頁面初始載入時，會在折頁上方顯示的內容會呈現在伺服器端。 這樣可將已呈現的內容傳送給用戶端，節省時間。 當使用者與SPA互動時，用戶端會轉譯其他內容。

當您考慮為SPA實作伺服器端轉譯時，需要檢閱應用程式的哪些部分是必要的。

## 用SSR開發SPA {#developing-an-spa-using-ssr}

SPA元件可由用戶端（在瀏覽器中）或伺服器端轉譯。 呈現伺服器端時，瀏覽器屬性（例如視窗大小和位置）不存在。 因此，SPA元件應為同構，不須假設其轉譯位置。

若要運用SSR，您必須在AEM和Adobe I/O Runtime中部署程式碼，後者負責伺服器端轉譯。 大部分的程式碼會相同，但伺服器特定的工作會有所不同。

## AEM中SPA的SSR {#ssr-for-spas-in-aem}

AEM中的SPA適用的SSR需要Adobe I/O Runtime，這是轉譯應用程式內容伺服器端所呼叫的功能。 在應用程式的HTL內，會呼叫Adobe I/O Runtime上的資源來呈現內容。

正如AEM可立即支援Angular和React SPA架構，Angular和React應用程式也支援伺服器端轉譯。 如需詳細資訊，請參閱這兩個架構的NPM檔案。

* React: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* Angular: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/angular-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/angular-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

如需簡單化的範例，請參閱 [We.Retail Journal應用程式](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal). 它會呈現整個應用程式伺服器端。 雖然這不是現實中的例子，但它確實說明了實施SSR需要什麼。

>[!CAUTION]
>
>此 [We.Retail Journal應用程式](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) 僅供展示之用，因此會使用Node.js作為簡單範例，而非建議的Adobe I/O Runtime。 此範例不應用於任何專案工作。

>[!NOTE]
>
>任何 AEM 專案都應利用 [AEM 專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)，它支援使用 React 或 Angular 的 SPA 專案並利用 SPA SDK。

## 使用Node.js {#using-node-js}

Adobe I/O Runtime是在AEM中實作SPA SSR的建議解決方案。

若為內部部署的AEM例項，您也可以使用與上述相同的方式，使用自訂Node.js例項來實作SSR。 雖然Adobe支援此功能，但不建議使用。

>[!NOTE]
>
>托管於Adobe的AEM例項不支援Node.js。

>[!NOTE]
>
>如果SSR必須透過Node.js實作，Adobe建議為每個AEM環境（製作、發佈、預備等）使用個別的Node.js例項。

## 遠端內容轉譯器 {#remote-content-renderer}

此 [遠端內容轉譯器設定](#remote-content-renderer-configuration) 在AEM中搭配SPA使用SSR時，需要點選更廣泛的轉譯服務，這些服務可擴充及自訂，以符合您的需求。

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` 是OSGi服務，用於擷取在遠端伺服器上轉譯的內容，例如從Adobe I/O。傳送至遠端伺服器的內容是根據所傳遞的要求參數。

`RemoteContentRenderingService` 可在需要進行其他內容操作時，透過相依性反轉插入自訂Sling模型或servlet中。

此服務由 [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

此 `RemoteContentRendererRequestHandlerServlet` 可用來以程式設計方式設定要求設定。 `DefaultRemoteContentRendererRequestHandlerImpl`，提供預設請求處理常式實作，可讓您建立多個OSGi設定，以將內容結構中的位置對應至遠端端點。

若要新增自訂請求處理常式，請實作 `RemoteContentRendererRequestHandler` 介面。 請務必將 `Constants.SERVICE_RANKING` 元件屬性轉換為高於100的整數，這是 `DefaultRemoteContentRendererRequestHandlerImpl`.

```
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### 配置預設處理程式的OSGi配置 {#configure-default-handler}

預設處理常式的設定必須依照一節所述進行設定 [遠端內容轉譯器設定](#remote-content-renderer-configuration).

### 遠端內容轉譯器用途 {#usage}

若要讓servlet擷取並傳回可插入頁面的某些內容：

1. 確保您的遠程伺服器可訪問。
1. 將下列其中一個程式片段新增至AEM元件的HTL範本。
1. （可選）建立或修改OSGi設定。
1. 瀏覽您網站的內容

頁面元件的HTL範本通常是此類功能的主要收件者。

```
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### 要求 {#requirements}

servlet會利用Sling模型匯出工具來序列化元件資料。 依預設， `com.adobe.cq.export.json.ContainerExporter` 和 `com.adobe.cq.export.json.ComponentExporter` 支援作為Sling型號轉接器。 如有必要，您可以新增類，讓要求適應使用 `RemoteContentRendererServlet` 和 `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. 其他類必須擴展 `ComponentExporter`.
