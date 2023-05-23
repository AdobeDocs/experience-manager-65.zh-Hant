---
title: 和SPA伺服器端呈現
seo-title: SPA and Server-Side Rendering
description: "SPA和伺服器端呈現"
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

# 和SPA伺服器端呈現{#spa-and-server-side-rendering}

>[!NOTE]
>
>編輯SPA器是需要基於框架的SPA客戶端呈現(例如，反應或Angular)的項目的推薦解決方案。

>[!NOTE]
>
>AEM6.5.1.0或更高版本是使用SPA本文檔中所述的伺服器端呈現功能所必需的。

## 概觀 {#overview}

單頁應用程式(SPA)可以為用戶提供豐富的動態體驗，以熟悉的方式反應和行為，通常就像本機應用程式。 [這是通過依靠客戶端將內容預先載入，然後完成處理用戶交互的繁重工作來實現的](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work) 從而最大限度地減少客戶端與伺服器之間需要的通信量，使應用更加被動。

但是，這可能導致較長的初始載入時間，尤其是當SPA載荷較大且內容豐富時。 為了優化載入時間，可以在伺服器端呈現一些內容。 使用伺服器端渲染(SSR)可以加快頁面的初始載入，然後將進一步的渲染傳遞給客戶端。

## 何時使用SSR {#when-to-use-ssr}

並非所有項目都需要SSR。 雖然AEM完全支援聯署材料安全SPA和保障法，但Adobe並不建議對每個項目系統地實施。

在決定實施SSR時，您必須首先估計SSR的額外複雜性、工作量和成本增加實際上代表項目的哪些額外內容，包括長期維護。 只有當增加值明顯超過估計成本時，才應選擇SSR結構。

SSR通常在以下任一問題出現明確的「是」時提供一些值：

* **徐：** 是否仍然需要SSR才能讓帶來流量的搜索引擎正確索引站點？ 請記住，主搜索引擎爬網程式現在會評估JS。
* **頁面速度：** SSR是否在真實環境中提供了可衡量的速度改進，並增加了總體用戶體驗？

只有在以下兩個問題中至少有一個以明確的「是」回答您的項目時，Adobe才建議實施SSR。 以下各節介紹如何使用Adobe I/O Runtime。

## Adobe I/O Runtime {#adobe-i-o-runtime}

如果 [確信您的項目需要實施SSR](/help/sites-developing/spa-ssr.md#when-to-use-ssr),Adobe推薦的解決方案是使用Adobe I/O Runtime。

有關Adobe I/O Runtime的更多資訊，請參見

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html)  — 有關服務的概述
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html)  — 有關平台的詳細文檔

以下各節詳細介紹了如何使用Adobe I/O Runtime在兩種不SPA同型號中實施SSR:

* [AEM驅動通信流](/help/sites-developing/spa-ssr.md#aem-driven-communication-flow)
* [Adobe I/O Runtime驅動的通信流](/help/sites-developing/spa-ssr.md#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe建議每個環境（階段、生產、測試等）單獨使用Adobe I/O Runtime工作區。 這允許使用將單個應用程式的不同版本部署到不同環境的典型系統開發生命週期(SDLC)模式。 查看文檔 [Project App Builder應用程式的CI/CD](https://developer.adobe.com/app-builder/docs/guides/deployment/ci_cd_for_firefly_apps/) 的子菜單。
>
>每個實例（作者、發佈）不需要單獨的工作區，除非每個實例類型的運行時實現存在差異。

## 遠程呈現器配置 {#remote-renderer-configuration}

必AEM須知道可以在何處檢索遠程呈現的內容。 無論 [你為SSR所選擇的模型，](#adobe-i-o-runtime) 您需要指定如何訪AEM問此遠程呈現服務。

此操作通過 **RemoteContentRenderer — 配置工廠OSGi服務**。 在Web控制台配置控制台中搜索字串「RemoteContentRenderer」 `http://<host>:<port>/system/console/configMgr`。

![呈現器配置](assets/rendererconfig.png)

以下欄位可用於配置：

* **內容路徑模式**  — 規則運算式，以匹配一部分內容（如有必要）
* **遠程終結點URL**  — 負責生成內容的終結點的URL
   * 如果本地網路中沒有，則使用安全的HTTPS協定。
* **其他請求標頭**  — 要添加到發送到遠程終結點的請求的其他標頭
   * 模式: `key=value`
* **請求超時**  — 遠程主機請求超時（毫秒）

>[!NOTE]
>
>無論您是否選擇實施 [AEM驅動通信流](#aem-driven-communication-flow) 或 [Adobe I/O Runtime驅動的流，](#adobe-i-o-runtime-driven-communication-flow) 必須定義遠程內容呈現器配置。
>
>如果您選擇進行此配置，則還必須定義此配置 [使用自定義Node.js伺服器。](#using-node-js)

>[!NOTE]
>
>此配置利用 [遠程內容呈現器，](#remote-content-renderer) 有其他擴展和自定義選項。

## AEM驅動通信流 {#aem-driven-communication-flow}

使用SSR時， [元件交互工作流](/help/sites-developing/spa-overview.md#workflow) 中SPA包AEM括在Adobe I/O Runtime上生成應用程式初始內容的階段。

1. 瀏覽器從請求SSR內AEM容。

1. 把AEM模型發給Adobe I/O Runtime。

1. Adobe I/O Runtime返回生成的內容。

1. 為Adobe I/O RuntimeAEM通過後端頁面元件的HTL模板返回的HTML提供服務。

![伺服器端呈現 — cms-drivenaemnode-adobeio](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

## Adobe I/O Runtime驅動的通信流 {#adobe-i-o-runtime-driven-communication-flow}

上一節介紹了在其中執行內容引導和服務的SPA服務AEM器端呈現的AEM標準和建議實施。

或者，SSR可以實現，使得Adobe I/O Runtime負責自舉，有效地逆轉通信流。

兩種模型均有效且受支AEM持。 然而，在實施特定模式之前，應考慮每個模式的利弊。

<table>
 <tbody>
  <tr>
   <th><strong>引導</strong></th>
   <th><strong>優點</strong></th>
   <th><strong>缺點</strong></th>
  </tr>
  <tr>
   <th><strong>AEM</strong><br /> </th>
   <td>
    <ul>
     <li>AEM管理按需注入庫</li>
     <li>只需維護資AEM源<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>開發人員可能不SPA熟悉<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>開發人員更SPA熟悉<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>應用程式所需的客戶端庫資源（如CSS和JavaScript）需要由開發人員通AEM過 <code><a href="/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet">allowProxy</a></code> 屬性<br /> </li>
     <li>資源必須在與Adobe I/O RuntimeAEM之間同步<br /> </li>
     <li>要啟用對的創SPA作，可能需要Adobe I/O Runtime的代理伺服器</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## SSR規劃 {#planning-for-ssr}

通常只需要呈現應用程式的一部分。 通常的示例是呈現伺服器端的頁面初始載入時將顯示在折疊上方的內容。 這通過將已呈現的內容發送到客戶端而節省時間。 當用戶與該交互時SPA，該附加內容由該客戶端呈現。

在考慮為您的應用程式實SPA施伺服器端呈現時，您需要查看應用程式需要哪些部分。

## 利用SSRSPA開發 {#developing-an-spa-using-ssr}

可SPA由客戶端（在瀏覽器中）或伺服器端呈現元件。 呈現伺服器端時，瀏覽器屬性（如窗口大小和位置）不存在。 因SPA此，分量應是同構的，不應假設它們將在何處渲染。

要利用SSR，您需要在中和在AEMAdobe I/O Runtime部署代碼，後者負責伺服器端呈現。 大多數代碼將相同，但特定於伺服器的任務將不同。

## SSRSPA在AEM {#ssr-for-spas-in-aem}

中的SPASSRAEM需要Adobe I/O Runtime，該應用程式需要呈現應用程式內容伺服器端。 在應用的HTL中，調用Adobe I/O Runtime上的資源來呈現內容。

正如支AEM持Angular和反SPA應框架開箱即用一樣，Angular和反應應用程式也支援伺服器端呈現。 有關更多詳細資訊，請參閱這兩個框架的NPM文檔。

* 反應： [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* Angular: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/angular-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/angular-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

有關簡單化的示例，請參閱 [We.Retail Journal應用](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)。 它呈現整個應用程式伺服器端。 雖然這不是一個真實的例子，但它確實說明了實施SSR所需要的。

>[!CAUTION]
>
>的 [We.Retail Journal應用](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) 僅用於演示目的，因此使用Node.js作為簡單示例，而不是推薦的Adobe I/O Runtime。 此示例不應用於任何項目工作。

>[!NOTE]
>
>任何 AEM 專案都應利用 [AEM 專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)，它支援使用 React 或 Angular 的 SPA 專案並利用 SPA SDK。

## 使用Node.js {#using-node-js}

Adobe I/O Runtime是在中實施SSR的SPA建議解AEM決方案。

對於上預AEM習實例，也可以使用自定義Node.js實例以如上所述的相同方式實現SSR。 儘管Adobe支援此操作，但不建議這樣做。

>[!NOTE]
>
>托管的Adobe實例不支援Node.jsAEM。

>[!NOTE]
>
>如果必須通過Node.js實現SSR，則Adobe建議為每個環境（作者、發佈、階段等）AEM單獨使用Node.js實例。

## 遠程內容呈現器 {#remote-content-renderer}

的 [遠程內容呈現器配置](#remote-content-renderer-configuration) 在中使用SSR時需要SPA的AEM功能，可以針對您的需要擴展和自定義更廣泛的呈現服務。

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` 是OSGi服務，用於檢索在遠程伺服器上呈現的內容，如從Adobe I/O。發送到遠程伺服器的內容基於傳遞的請求參數。

`RemoteContentRenderingService` 當需要額外的內容操作時，可通過依賴項反轉將其注入到自定義Sling模型或servlet中。

此服務由 [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet)。

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

的 `RemoteContentRendererRequestHandlerServlet` 可用於以寫程式方式設定請求配置。 `DefaultRemoteContentRendererRequestHandlerImpl`提供的預設請求處理程式實現，允許您建立多個OSGi配置，以便將內容結構中的某個位置映射到遠程端點。

要添加自定義請求處理程式，請實現 `RemoteContentRendererRequestHandler` 。 確保設定 `Constants.SERVICE_RANKING` component屬性到大於100的整數，即 `DefaultRemoteContentRendererRequestHandlerImpl`。

```
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### 配置預設處理程式的OSGi配置 {#configure-default-handler}

預設處理程式的配置必須按照一節中所述進行配置 [遠程內容呈現器配置](#remote-content-renderer-configuration)。

### 遠程內容呈現器用法 {#usage}

要讓Servlet獲取並返回一些可以注入到頁面的內容，請執行以下操作：

1. 確保遠程伺服器可訪問。
1. 將以下片段之一添加到元件的HTL模AEM板中。
1. （可選）建立或修改OSGi配置。
1. 瀏覽網站內容

通常，頁面元件的HTL模板是此類功能的主要接收者。

```
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### 要求 {#requirements}

Servlet利用Sling模型導出器序列化元件資料。 預設情況下， `com.adobe.cq.export.json.ContainerExporter` 和 `com.adobe.cq.export.json.ComponentExporter` 支援作為Sling型號適配器。 如有必要，您可以添加請求應適用於使用的類 `RemoteContentRendererServlet` 執行 `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`。 其他類必須擴展 `ComponentExporter`。
