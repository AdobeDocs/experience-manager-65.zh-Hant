---
title: 如何將 Headless 應用程式上線
description: 在AEM Headless開發人員歷程的這一部分，瞭解如何即時部署Headless應用程式。
exl-id: ec3356ef-9e60-4151-984d-3ebdab593b96
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin, Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '1803'
ht-degree: 53%

---

# 如何將 Headless 應用程式上線 {#go-live}

在[AEM Headless開發人員歷程](overview.md)的這一部分，瞭解如何即時部署Headless應用程式。

## 到目前為止 {#story-so-far}

在 AEM Headless 歷程的上一個文件「[如何透過 AEM Assets API 更新您的內容](update-your-content.md)」中，您已了解如何通過 API 更新 AEM 中現有的 Headless 內容，您現在應該：

* 了解 AEM Assets HTTP API。

本文章以這些基本知識為基礎，以便您了解如何準備您自己的 AEM Headless 專案並方案上線。

## 目標 {#objective}

本文件可協助在將您的應用程式上線之前，應該注意的 AEM Headless 發佈管道和效能考量事項。

* 瞭解AEM SDK和所需的開發工具
* 設定本機開發執行階段以在上線之前模擬您的內容
* 瞭解AEM內容復寫和快取基本概念
* 在應用程式推出前加以保護和擴展
* 監控效能和偵錯問題

## AEM SDK {#the-aem-sdk}

AEM SDK 用於建置和部署自訂程式碼。這是您在啟用Headless應用程式之前，必須開發和測試的主要工具。 它都包含下列成品：

* Quickstart jar - 這是可執行的 jar 檔案，可用於設定編寫和發佈執行個體
* Dispatcher工具 — Windows和UNIX系統的Dispatcher模組及其相依性
* Java™ API Jar - Java™ Jar/Maven 相依性公開了所有允許的 Java™ API，其可用於針對 AEM 進行開發
* Javadoc jar - Java™ API jar 的 javadoc

## 其他開發工具 {#additional-development-tools}

除了AEM SDK，您還需要其他工具，協助您在本機開發和測試程式碼和內容：

* Java™
* Git
* Apache Maven
* Node.js 程式庫
* 您選擇的 IDE

由於AEM是Java™應用程式，因此您必須安裝Java™和Java™ SDK以支援AEM as a Cloud Service的開發。

Git 是您用來管理原始檔控制系統和簽入對 Cloud Manager 的變更，然後將它們部署到生產執行個體的工具。

AEM 使用 Apache Maven 建置從 AEM Maven 專案原型產生的專案。所有主要的 IDE 都提供對 Maven 的整合支援。

Node.js是JavaScript執行階段環境，用來處理AEM專案`ui.frontend`子專案的前端資產。 Node.js隨npm分佈，後者是實際的Node.js Package Manager，用於管理JavaScript相依性。

## AEM 系統元件一覽 {#components-of-an-aem-system-at-a-glance}

接下來，讓我們看看 AEM 環境的組成部分。

完整的 AEM 環境由編寫、發佈和 Dispatcher 組成。這些相同的元件在本機開發執行階段中可供使用，讓您更輕鬆地在上線之前預覽程式碼和內容。

* **編寫服務**&#x200B;是內部使用者建立、管理和預覽內容的地方。

* **Publish服務**&#x200B;被視為「即時」環境，通常是使用者互動的對象。 在Author服務上編輯及核准後的內容，會分配（復寫）至Publish服務。 AEM Headless 應用程式最常見的部署模式是讓應用程式的生產版本連接到 AEM Publish 服務。

* **Dispatcher** 是靜態 Web 伺服器，增加了 AEM Dispatcher 模組。它快取發佈執行個體產生的網頁以提升效能。

## 本機開發工作流程 {#the-local-development-workflow}

本機開發專案以 Apache Maven 為基礎建置，並使用 Git 進行原始檔控制。若要更新專案，開發人員可以使用偏好的整合式開發環境，例如 Eclipse、Visual Studio Code 或 IntelliJ 等。

若要測試Headless應用程式擷取的程式碼或內容更新，請將更新部署至本機AEM執行階段。 其中包括AEM作者和發佈服務的本機執行個體。

請務必注意本機 AEM 執行階段每個元件之間的區別，因為在與您的更新最有關係的地方測試它，這一點非常重要。例如，在編寫執行個體測試內容更新或在發佈執行個體測試新程式碼。

在生產系統中，Dispatcher 和 http Apache 伺服器一律位於 AEM 發佈執行個體的前面。它們為 AEM 系統提供快取和安全性服務，因此針對 Dispatcher 測試程式碼和內容更新是最重要的。

## 使用本機開發環境在本機預覽程式碼和內容 {#previewing-your-code-and-content-locally-with-the-local-development-environment}

若要準備AEM Headless專案以準備啟動，請確定專案的所有組成部分皆正常運作。

為此，您必須將所有內容（程式碼、內容和設定）整合在一起，並在本機開發環境中測試其上線整備。

本機開發環境由三個主要區域組成：

1. AEM專案 — 包含AEM開發人員將處理的所有自訂程式碼、設定和內容
1. 本機 AEM 執行階段 - AEM 編寫和發佈服務本機版本，用於從 AEM 專案部署程式碼
1. 本機 Dispatcher 執行階段 - 包含 Dispatcher 模型的 Apache htttpd 網頁伺服器本機版本

設定本機開發環境後，您可以透過在本機部署靜態Node伺服器來模擬提供給React應用程式的內容。

若要更深入瞭解如何設定本機開發環境以及內容預覽所需的所有相依性，請參閱[生產部署檔案](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/overview.html)。

## 準備您的AEM Headless應用程式以供上線 {#prepare-your-aem-headless-application-for-golive}

<!-- Start of CDN Review -->

現在，您可以依照下列最佳作法，讓AEM Headless應用程式準備好要啟動。

### 啟動前保護您的Headless應用程式 {#secure-and-scale-before-launch}

1. 為您的GraphQL請求準備[驗證](/help/sites-developing/headless/graphql-api/graphql-authentication-content-fragments.md)

### 模型結構與 GraphQL 輸出 {#structure-vs-output}

* 避免建立輸出超過15 KB JSON （gzip壓縮）的查詢。 長 JSON 檔案是資源密集型檔案，用戶端應用程式需要解析。
* 避免片段階層有超過五個巢狀層。增加層數會使內容作者難以考量變更帶來的影響。
* 使用多物件查詢，而不是在模型中使用相依性階層建立查詢模型。如此可讓您在重新建構JSON輸出時擁有更長遠的彈性，而不需進行許多內容變更。

### 最大化 CDN 快取命中比例 {#maximize-cdn}

* 不要使用直接 GraphQL 查詢，除非您從表面要求即時內容。
   * 盡可能使用持續性查詢。
   * 提供600秒以上的CDN TTL，讓CDN可以快取它們。
   * AEM 可以計算模型變更對現有查詢的影響。
* 在低和高內容變更率之間分割JSON檔案/GraphQL查詢，以減少對CDN的使用者端流量並指派較高的TTL。 如此可將CDN使用原始伺服器重新驗證JSON的情況降至最低。
* 若要讓CDN的內容主動失效，請使用「軟清除」。 這麼做可讓CDN重新下載內容，而不會造成快取遺失。

>[!NOTE]
>
>如需有關CDN和快取的詳細資訊，請參閱[其他資源](#additional-resources)。

### 縮短下載 Headless 內容的時間 {#improve-download-time}

* 確保 HTTP 用戶端使用 HTTP/2。
* 確保 HTTP 用戶端接受標頭要求 gzip。
* 盡量減少用於裝載 JSON 和參考成品的網域數量。
* 使用`Last-modified-since`重新整理資源。
* 使用 JSON 檔案中的 `_reference` 輸出開始下載資產，而無需解析完整的 JSON 檔案。

<!-- End of CDN Review -->

## 部署至生產環境 {#deploy-to-production}

部署到生產環境取決於您是使用Maven部署的&#x200B;*傳統* AEM執行個體，還是使用Managed Services (AMS)Adobe並因此使用Cloud Manager。

## 使用Maven部署至生產環境 {#deploy-to-production-maven}

如需使用Maven的&#x200B;*傳統*&#x200B;部署（非AMS），請參閱[WKND教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html#build)以取得概覽。

## 使用Cloud Manager部署至生產環境 {#deploy-to-production-cloud-manager}

如果您是使用Cloud Manager的AMS客戶，在確認一切都經過測試且正常運作後，您可以將程式碼更新推送到Cloud Manager中的[集中式Git存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/git-integration.html)。

將更新上傳到Cloud Manager後，使用[Cloud Manager的CI/CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-deployment.html)將它們部署到AEM。

<!-- Cannot find a parallel link -->
<!--
You can start deploying your code by using the Cloud Manager CI/CD pipeline, which is covered extensively - see the [Overview](/help/implementing/deploying/overview.md) to start.
-->

## 效能監控 {#performance-monitoring}

為了讓使用者有最佳的 AEM Headless 應用程式使用體驗，請務必監控關鍵效能量度，如下詳述：

* 驗證應用程式的預覽版本和生產版本
* 確認 AEM 狀態頁面是否有目前的服務可用性狀態
* 存取效能報告
   * 傳遞效能
      * 原始伺服器 - 呼叫次數、錯誤率、CPU 負載、負載流量
   * 作者效能
      * 檢查使用者、請求和載入的數量
* 存取應用程式和空間特定的效能報表
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
* 若要檢查使用者端應用程式是否存在或傳送問題，請在使用者端應用程式中檢查JSON
* 若要檢查是否存在與快取內容或AEM相關的問題，請使用GraphQL檢查JSON

### 向支援團隊記錄錯誤 {#logging-a-bug-with-support}

若您需要進一步協助，請完成下列步驟，以有效率地向「支援」記錄錯誤：

* 如有必要，將問題進行螢幕截圖
* 記錄重現問題的方法
* 記錄問題重現的內容
* 透過 AEM 支援入口網站記錄問題並標註優先順序

## 歷程結束 - 還是結束了？ {#journey-ends}

恭喜！您已經完成 AEM Headless 開發人員歷程！您現在應該已經了解：

* Headless 和 Headful 內容傳遞之間的差異。
* AEM 的 Headless 功能。
* 如何組織 AEM Headless 專案。
* 如何在 AEM 建立 Headless 內容。
* 如何在 AEM 擷取和更新 Headless 內容。
* 如何使 AEM Headless 專案上線。
* 上線完成後該做什麼。

您已經啟動第一個AEM Headless專案，或已經掌握執行此工作的所有知識。 做得好！

### 探索單頁應用程式 {#explore-spa}

不過，不需要停止AEM中的Headless商店。 在歷程[&#128279;](getting-started.md#integration-levels)的快速入門部分中，它討論了AEM如何不僅支援Headless傳送和傳統的全棧疊模型，還支援結合兩者優勢的混合模型。

如果您的專案需要這種彈性，請繼續進行[如何使用AEM建立單頁應用程式(SPA) ](create-spa.md)歷程的其他選擇性部分。

## 其他資源 {#additional-resources}

* [AEM開發指南](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/the-basics.html)

* [WKND教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)

* 適用於AEM的[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html)

* CDN快取

   * [控制CDN快取](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#controlling-a-cdn-cache)

   * 正在設定[CDN重寫程式](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/osgi-configuration-settings.html) （*搜尋CDN重寫程式*）

* [AEM as a Headless CMS 簡介](/help/sites-developing/headless/introduction.md)
* [AEM 開發人員入口網站](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html)
* [AEM 中的 Headless 教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)
