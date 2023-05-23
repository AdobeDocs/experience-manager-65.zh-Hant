---
title: 如何將 Headless 應用程式上線
description: 在「無頭開發AEM者之旅」的這一部分，瞭解如何即時部署無頭應用程式。
exl-id: ec3356ef-9e60-4151-984d-3ebdab593b96
source-git-commit: 71842228dd3cb1ce3b79728912e8333d25fccefc
workflow-type: tm+mt
source-wordcount: '1846'
ht-degree: 50%

---

# 如何將 Headless 應用程式上線 {#go-live}

在 [無AEM頭開發者之旅](overview.md)，瞭解如何即時部署無頭應用程式。

## 到目前為止 {#story-so-far}

在 AEM 無周邊歷程的上一個文件「[如何透過 AEM Assets API 更新您的內容](update-your-content.md)」中，您已了解如何通過 API 更新 AEM 中現有的無周邊內容，您現在應該：

* 了解 AEM Assets HTTP API。

本文章以這些基本知識為基礎，以便您了解如何準備您自己的 AEM 無周邊專案並計畫上線。

## 目標 {#objective}

本文件可協助在將您的應用程式上線之前，應該注意的 AEM 無周邊發佈管道和效能考量事項。

* 瞭解所需AEM的SDK和開發工具
* 設定本地開發運行時以在開始運行之前模擬內容
* 瞭解內AEM容複製和快取基礎知識
* 在應用程式推出前加以保護和擴展
* 監控效能和偵錯問題

## AEM SDK {#the-aem-sdk}

AEM SDK 用於建置和部署自訂程式碼。它是您在投入使用之前必須開發和test無頭應用程式的主要工具。 它都包含下列成品：

* Quickstart jar - 這是可執行的 jar 檔案，可用於設定作者和發佈執行個體
* Dispatcher工具 — Dispatcher模組及其對基於Windows和UNIX的系統的依賴項
* Java™ API Jar - Java™ Jar/Maven 相依性公開了所有允許的 Java™ API，其可用於針對 AEM 進行開發
* Javadoc jar - Java™ API jar 的 javadoc

## 其他開發工具 {#additional-development-tools}

除了SDK，您還AEM需要其他工具來方便本地開發和測試代碼和內容：

* Java™
* Git
* Apache Maven
* Node.js 程式庫
* 您選擇的 IDE

因AEM為是Java™應用程式，必須安裝Java™和Java™ SDK以支援as a Cloud Service的開AEM發。

Git 是您用來管理原始檔控制系統和簽入對 Cloud Manager 的變更，然後將它們部署到生產執行個體的工具。

AEM 使用 Apache Maven 建置從 AEM Maven 專案原型產生的專案。所有主要的 IDE 都提供對 Maven 的整合支援。

Node.js是JavaScript運行時環境，用於處理項目的AEM前端資產 `ui.frontend` 子項目。 Node.js與npm一起分發，npm是事實上的Node.js包管理器，用於管理JavaScript依賴關係。

## AEM 系統元件一覽 {#components-of-an-aem-system-at-a-glance}

接下來，讓我們看看 AEM 環境的組成部分。

完整的 AEM 環境由作者、發佈和 Dispatcher 組成。這些相同的元件在本地開發運行時可用，以便您更輕鬆地預覽代碼和內容，然後才能投入使用。

* **作者服務**&#x200B;是內部使用者建立、管理和預覽內容的地方。

* **發佈服務** 被認為是「即時」環境，通常是最終用戶與之交互的內容。 在作者服務上編輯和批准內容後，內容將分發（複製）到發佈服務。 AEM 無周邊應用程式最常見的部署模式是讓應用程式的生產版本連接到 AEM Publish 服務。

* **Dispatcher** 是靜態 Web 伺服器，增加了 AEM Dispatcher 模組。它快取發佈執行個體產生的網頁以提升效能。

## 本機開發工作流程 {#the-local-development-workflow}

本機開發專案以 Apache Maven 為基礎建置，並使用 Git 進行原始檔控制。要更新項目，開發人員可以使用其首選的整合開發環境，如Eclipse、Visual Studio代碼或IntelliJ等。

要test由無頭應用程式接收的代碼或內容更新，請將更新部署到本地運AEM行時。 這些實例包括作者的本AEM地實例和發佈服務。

請務必注意本機 AEM 執行階段每個元件之間的區別，因為在與您的更新最有關係的地方測試它，這一點非常重要。例如，在作者執行個體測試內容更新或在發佈執行個體測試新程式碼。

在生產系統中，Dispatcher 和 http Apache 伺服器一律位於 AEM 發佈執行個體的前面。它們為 AEM 系統提供快取和安全性服務，因此針對 Dispatcher 測試程式碼和內容更新是最重要的。

## 使用本機開發環境在本機預覽程式碼和內容 {#previewing-your-code-and-content-locally-with-the-local-development-environment}

要準備AEM啟動無頭項目，請確保項目的所有組成部分都運行良好。

要做到這一點，你必須把所有東西都放在一起：代碼、內容和配置，並將其test到本地開發環境中，以便進行即時準備。

地方發展環境主要由三個方面組成：

1. 項AEM目 — 包含開發人員將要處理的所AEM有自定義代碼、配置和內容
1. 本機 AEM 執行階段 - AEM 作者和發佈服務本機版本，用於從 AEM 專案部署程式碼
1. 本機 Dispatcher 執行階段 - 包含 Dispatcher 模型的 Apache htttpd 網頁伺服器本機版本

設定本地開發環境後，您可以通過本地部署靜態節點伺服器來模擬向React應用提供的內容服務。

要更深入地瞭解設定本地開發環境以及內容預覽所需的所有相關性，請參見 [生產部署文檔](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/overview.html?lang=en)。

## 準AEM備無頭應用程式投入使用 {#prepare-your-aem-headless-application-for-golive}

<!-- Start of CDN Review -->

現在，是時候按照下面介紹的AEM最佳做法，讓您的無頭應用程式準備啟動了。

### 啟動前保護您的無頭應用程式 {#secure-and-scale-before-launch}

1. 準備 [驗證](/help/sites-developing/headless/graphql-api/graphql-authentication-content-fragments.md) 你的GraphQL請求

### 模型結構與 GraphQL 輸出 {#structure-vs-output}

* 避免建立輸出超過15 KB的JSON（gzip壓縮）的查詢。 長 JSON 檔案是資源密集型檔案，用戶端應用程式需要解析。
* 避免片段階層有超過五個巢狀層。增加層數會使內容作者難以考量變更帶來的影響。
* 使用多物件查詢，而不是在模型中使用相依性階層建立查詢模型。這樣做可以增加JSON輸出的長期靈活性，而無需進行許多內容更改。

### 最大化 CDN 快取命中比例 {#maximize-cdn}

* 不要使用直接 GraphQL 查詢，除非您從表面要求即時內容。
   * 盡可能使用持續性查詢。
   * 提供600秒以上的CDN TTL，以便CDN可以快取它們。
   * AEM 可以計算模型變更對現有查詢的影響。
* 將JSON檔案/GraphQL查詢在低和高內容更改率之間拆分，以減少客戶端到CDN的流量並分配更高的TTL。 這樣，CDN將使JSON與源伺服器重新驗證最小化。
* 要主動使CDN中的內容無效，請使用軟清除。 這樣，CDN可以重新下載內容，而不會導致快取丟失。

>[!NOTE]
>
>請參閱 [其他資源](#additional-resources) 的子菜單。

### 縮短下載 Headless 內容的時間 {#improve-download-time}

* 確保 HTTP 用戶端使用 HTTP/2。
* 確保 HTTP 用戶端接受標頭要求 gzip。
* 盡量減少用於裝載 JSON 和參考成品的網域數量。
* 使用 `Last-modified-since` 來刷新資源。
* 使用 JSON 檔案中的 `_reference` 輸出開始下載資產，而無需解析完整的 JSON 檔案。

<!-- End of CDN Review -->

## 部署至生產環境 {#deploy-to-production}

部署到生產可能取決於您是否 *傳統* 使AEM用Maven部署或位於Adobe Managed Services(AMS)上，因此使用Cloud Manager的實例。

## 使用Maven部署到生產 {#deploy-to-production-maven}

對於 *傳統* 部署（非AMS），請參閱 [WKND教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html?lang=en#build) 的雙曲餘切值。

## 使用雲管理器部署到生產 {#deploy-to-production-cloud-manager}

如果您是使用雲管理器的AMS客戶，在確保所有內容都經過測試並正常工作後，您可以將代碼更新推送到 [Cloud Manager中的集中式Git儲存庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html)。

將更新上載到雲管理器後，將其部署AEM到 [Cloud Manager的CI/CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-deployment.html)。

<!-- Can't find a parallel link -->
<!--
You can start deploying your code by leveraging the Cloud Manager CI/CD pipeline, which is covered extensively [here](/help/implementing/deploying/overview.md).
-->

## 效能監控 {#performance-monitoring}

為了讓使用者有最佳的 AEM 無周邊應用程式使用體驗，請務必監控關鍵效能量度，如下詳述：

* 驗證應用程式的預覽版本和生產版本
* 確認 AEM 狀態頁面是否有目前的服務可用性狀態
* 存取效能報告
   * 傳遞效能
      * 原始伺服器 - 呼叫次數、錯誤率、CPU 負載、負載流量
   * 作者效能
      * 檢查用戶、請求和載入的數量
* 訪問特定於應用和空間的效能報告
   * 伺服器啟動後，檢查一般量度是否為綠色/橘色/紅色，然後識別特定的應用程式問題
   * 開啟上面篩選到應用程式或空間 (例如 Photoshop 桌面、付費牆) 的相同報告
   * 使用 Splunk log API 存取服務和應用程式效能
   * 如果還有其他問題，請聯絡客戶支援。

## 疑難排解 {#troubleshooting}

### 偵錯 {#debugging}

遵循這些最佳做法做為一般偵錯方法：

* 使用應用程式的預覽版本驗證功能和效能
* 使用應用程式的生產版本驗證功能和效能
* 使用內容片段編輯器的 JSON 預覽進行驗證
* 要檢查是否存在客戶端應用程式或傳遞問題，請檢查客戶端應用程式中的JSON
* 要檢查是否存在與快取內容相關的問題，或AEM者使用GraphQL檢查JSON

### 向支援團隊記錄錯誤 {#logging-a-bug-with-support}

要通過支援高效地記錄錯誤，在需要進一步幫助時，請完成以下步驟：

* 如有必要，將問題進行螢幕截圖
* 記錄重現問題的方法
* 記錄問題重現的內容
* 透過 AEM 支援入口網站記錄問題並標註優先順序

## 歷程結束 - 還是結束了？ {#journey-ends}

恭喜！您已經完成 AEM Headless 開發人員歷程！您現在應該已經了解：

* 無周邊和有周邊內容傳遞之間的差異。
* AEM 的無周邊功能。
* 如何組織 AEM Headless 專案。
* 如何在 AEM 建立無周邊內容。
* 如何在 AEM 擷取和更新無周邊內容。
* 如何使 AEM Headless 專案上線。
* 上線完成後，該怎麼辦。

您已經啟動了第AEM一個Headless項目，或者現在已掌握了全部相關知識。 做得好！

### 探索單頁應用程式 {#explore-spa}

不過，不必停下無頭店AEM了。 在 [入門](getting-started.md#integration-levels)討論了AEM如何支援無頭遞送和傳統的全棧模型，以及如何支援結合兩者優點的混合模型。

如果這種靈活性是您項目需要的，請繼續進行可選的附加部分， [如何使用建立單頁應用SPA程式(AEM)。](create-spa.md)

## 其他資源 {#additional-resources}

* [開AEM發指南](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/the-basics.html?lang=en)

* [WKND教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en)

* [雲管理AEM器](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html?lang=zh-Hant)

* CDN快取

   * [控制CDN快取](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#controlling-a-cdn-cache)

   * 配置 [CDN重寫器](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/osgi-configuration-settings.html) (*搜索CDN重寫器*)
