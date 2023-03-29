---
title: 如何將 Headless 應用程式上線
description: 在AEM無頭式開發人員歷程的這部分，了解如何即時部署無頭式應用程式。
exl-id: ec3356ef-9e60-4151-984d-3ebdab593b96
source-git-commit: ad0f0bd8b0c230e002c734adca87da22bfa3a7cd
workflow-type: tm+mt
source-wordcount: '1903'
ht-degree: 54%

---

# 如何將 Headless 應用程式上線 {#go-live}

在 [AEM Headless Developer Journey](overview.md)，了解如何即時部署無頭應用程式。

## 到目前為止 {#story-so-far}

在 AEM 無周邊歷程的上一個文件「[如何透過 AEM Assets API 更新您的內容](update-your-content.md)」中，您已了解如何通過 API 更新 AEM 中現有的無周邊內容，您現在應該：

* 了解 AEM Assets HTTP API。

本文章以這些基本知識為基礎，以便您了解如何準備您自己的 AEM 無周邊專案並計畫上線。

## 目標 {#objective}

本檔案可協助您了解AEM無頭發佈管道，以及在與應用程式上線前需要注意的效能考量事項。

* 了解AEM SDK及所需的開發工具
* 設定本機開發執行階段，以在上線前模擬您的內容
* 了解AEM內容復寫和快取基本知識
* 在應用程式推出前加以保護和擴展
* 監控效能和偵錯問題

## AEM SDK {#the-aem-sdk}

AEM SDK 用於建置和部署自訂程式碼。這是您在開發和測試無頭應用程式之前所需的主要工具。 它都包含下列成品：

* Quickstart jar - 這是可執行的 jar 檔案，可用於設定作者和發佈執行個體
* Dispatcher工具 — 適用於Windows和UNIX系統的Dispatcher模組及其相依性
* Java API Jar — 公開所有可用來針對AEM開發的允許Java API的Java Jar/Maven相依性
* Javadoc jar - Java API jar的javadoc

## 其他開發工具 {#additional-development-tools}

除了AEM SDK，您還需要其他工具來協助您在本機開發及測試程式碼和內容：

* Java
* Git
* Apache Maven
* Node.js 程式庫
* 您選擇的 IDE

由於AEM是Java應用程式，因此您必須安裝Java和Java SDK，才能支援AEMas a Cloud Service的開發。

您可以使用Git來管理原始碼控制，以及檢查Cloud Manager的變更，然後將其部署至生產執行個體。

AEM使用Apache Maven來建置從AEM Maven專案原型產生的專案。 所有主要的 IDE 都提供對 Maven 的整合支援。

Node.js 是 JavaScript 執行階段環境，用於處理 AEM 專案 `ui.frontend`子專案的前端資產。Node.js與npm一起分發，npm是事實上的Node.js套件管理器，用於管理JavaScript相依性。

## AEM 系統元件一覽 {#components-of-an-aem-system-at-a-glance}

接下來，讓我們看一下AEM環境的組成部分。

完整的 AEM 環境由作者、發佈和 Dispatcher 組成。這些相同的元件會在本機開發執行階段中提供，讓您在上線前更輕鬆地預覽程式碼和內容。

* **作者服務**&#x200B;是內部使用者建立、管理和預覽內容的地方。

* **發佈服務**&#x200B;被認為是「即時」環境，通常是一般使用者與其互動。內容在Author服務上經過編輯和核准後，會分發（複製）至Publish服務。 AEM 無周邊應用程式最常見的部署模式是讓應用程式的生產版本連接到 AEM Publish 服務。

* **Dispatcher** 是靜態 Web 伺服器，增加了 AEM Dispatcher 模組。它快取發佈執行個體產生的網頁以提升效能。

## 本機開發工作流程 {#the-local-development-workflow}

本機開發專案以 Apache Maven 為基礎建置，並使用 Git 進行原始檔控制。為了更新專案，開發人員可使用其偏好的整合開發環境，例如Eclipse、Visual Studio Code或IntelliJ等。

若要測試無頭應用程式將擷取的程式碼或內容更新，您必須將更新部署至本機AEM執行階段，其中包括AEM製作和發佈服務的本機例項。

請務必注意本機 AEM 執行階段每個元件之間的區別，因為在與您的更新最有關係的地方測試它，這一點非常重要。例如，在作者執行個體測試內容更新或在發佈執行個體測試新程式碼。

在生產系統中，Dispatcher和http Apache伺服器一律會位於AEM發佈例項之前。 它們為AEM系統提供快取和安全服務，因此也必須針對Dispatcher測試程式碼和內容更新。

## 使用本機開發環境在本機預覽程式碼和內容 {#previewing-your-code-and-content-locally-with-the-local-development-environment}

若要為啟動準備AEM無標題專案，您必須確定專案的所有組成部分都正常運作。

為此，您需要將所有內容整合在一起：程式碼、內容和設定，並在本機開發環境中測試，以備上線準備。

本機開發環境由三個主要區域組成：

1. AEM專案 — 這將包含AEM開發人員將要使用的所有自訂程式碼、設定和內容
1. 本機AEM執行階段 — 用於從AEM專案部署程式碼的AEM製作與發佈服務的本機版本
1. 本機 Dispatcher 執行階段 - 包含 Dispatcher 模型的 Apache htttpd 網頁伺服器本機版本

設定好本機開發環境後，您可以透過在本機部署靜態節點伺服器來模擬提供給 React 應用程式的內容。

若要深入了解如何設定本機開發環境，以及內容預覽所需的所有相依性，請參閱 [生產部署檔案](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/production-deployment.html?lang=en#prerequisites).

## 準備AEM Headless應用程式上線 {#prepare-your-aem-headless-application-for-golive}

<!-- Start of CDN Review -->

現在，您可以遵循以下概述的最佳實務，為您的AEM無頭應用程式做好啟動準備。

### 啟動前保護無頭應用程式 {#secure-and-scale-before-launch}

1. 準備 [驗證](/help/sites-developing/headless/graphql-api/graphql-authentication-content-fragments.md) 針對GraphQL請求

### 模型結構與 GraphQL 輸出 {#structure-vs-output}

* 避免建立輸出超過 15kb JSON (gzip 格式壓縮) 的查詢。長 JSON 檔案是資源密集型檔案，用戶端應用程式需要解析。
* 避免片段階層有超過五個巢狀層。增加層數會使內容作者難以考量變更帶來的影響。
* 使用多物件查詢，而不是在模型中使用相依性階層建立查詢模型。這允許更長期的靈活性來重新建構 JSON 輸出，而無需進行大量內容變更。

### 最大化 CDN 快取命中比例 {#maximize-cdn}

* 不要使用直接 GraphQL 查詢，除非您從表面要求即時內容。
   * 盡可能使用持續性查詢。
   * 提供 600 秒以上的 CDN TTL，以便 CDN 可以快取。
   * AEM 可以計算模型變更對現有查詢的影響。
* 在低內容更改率和高內容變更改率之間分割 JSON 檔案/GraphQL 查詢，以減少流到 CDN 的用戶端流量並指派更高的 TTL。這將 CDN 使用原始伺服器重新驗證 JSON 的需要降至最低。
* 要主動使來自 CDN 的內容無效，請使用軟清除 (Soft Purge)。這可讓CDN重新下載內容，而不會造成快取遺失。

>[!NOTE]
>
>請參閱 [其他資源](#additional-resources) 以取得CDN和快取的詳細資訊。

### 縮短下載 Headless 內容的時間 {#improve-download-time}

* 確保 HTTP 用戶端使用 HTTP/2。
* 確保 HTTP 用戶端接受標頭要求 gzip。
* 盡量減少用於裝載 JSON 和參考成品的網域數量。
* 利用 `Last-modified-since` 重新整理資源。
* 使用 JSON 檔案中的 `_reference` 輸出開始下載資產，而無需解析完整的 JSON 檔案。

<!-- End of CDN Review -->

## 部署至生產環境 {#deploy-to-production}

部署至生產環境取決於您是否有 *傳統* 使用Maven進行部署，或位於Adobe Managed Services(AMS)上，因此使用Cloud Manager的AEM例項。

## 使用Maven部署至生產環境 {#deploy-to-production-maven}

若 *傳統* 使用Maven部署（非AMS），您可以看到 [WKND教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html?lang=en#build) 以取得概述。

## 使用Cloud Manager部署至生產環境 {#deploy-to-production-cloud-manager}

如果您是使用Cloud Manager的AMS客戶，則在您確定所有項目皆已測試且正常運作後，即可將程式碼更新推送至 [Cloud Manager中的集中式Git存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html).

將更新上傳到 Cloud Manager 後，可以使用 [Cloud Manager 的 CI/CD 管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)部署到 AEM 

<!-- Can't find a parallel link -->
<!--
You can start deploying your code by leveraging the Cloud Manager CI/CD pipeline, which is covered extensively [here](/help/implementing/deploying/overview.md).
-->

## 效能監控 {#performance-monitoring}

為了讓使用者在使用AEM無頭式應用程式時能有最佳體驗，請務必監控關鍵效能量度，如下所述：

* 驗證應用程式的預覽版本和生產版本
* 確認 AEM 狀態頁面是否有目前的服務可用性狀態
* 存取效能報告
   * 傳遞效能
      * 原始伺服器 - 呼叫次數、錯誤率、CPU 負載、負載流量
   * 作者效能
      * 檢查使用者、要求和負載的數量
* 訪問特定於應用程式和空間的效能報告
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
* 檢查用戶端應用程式中的 JSON 以檢查是否存在用戶端應用程式或傳遞問題
* 使用 GraphQL 檢查 JSON 以檢查是否存在與快取內容或 AEM 相關的問題

### 向支援團隊記錄錯誤 {#logging-a-bug-with-support}

為了在需要進一步協助時，可以有效率地向支援團隊記錄錯誤，請按照以下步驟操作：

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
* 上線後怎麼辦。

您已經推出您的第一個 AEM Headless 專案，或是現在已經掌握完成此作業的所有必要知識。做得好！

### 探索單頁應用程式 {#explore-spa}

不過，AEM 無周邊商店不需要就此停止。您可能會記得 [快速入門歷程部分](getting-started.md#integration-levels) 我們簡要地討論了AEM如何不僅支援無頭式傳送和傳統的完整堆疊模型，還支援結合兩者優點的混合模型。

如果您的專案需要這種靈活性，請繼續學習此歷程的額外部分 (選用)：[如何使用 AEM 建立單頁應用程式 (SPA)。](create-spa.md)

## 其他資源 {#additional-resources}

* [AEM Developing指南](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/the-basics.html?lang=en)

* [WKND教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en)

* [適用於AEM的Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=en)

* CDN快取

   * [控制CDN快取](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#controlling-a-cdn-cache)

   * 設定 [CDN重寫器](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/osgi-configuration-settings.html) (*搜尋CDN重寫器*)
