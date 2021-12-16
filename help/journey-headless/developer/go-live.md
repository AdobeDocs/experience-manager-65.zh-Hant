---
title: 如何與無頭應用程式一起運行
description: 在AEM無頭式開發人員歷程的這部分，了解如何即時部署無頭式應用程式。
source-git-commit: 20d46a7c37663dac36e6af9582d569a7f782eab7
workflow-type: tm+mt
source-wordcount: '1903'
ht-degree: 0%

---

# 如何與無頭應用程式一起運行 {#go-live}

在 [AEM Headless Developer Journey](overview.md)，了解如何即時部署無頭應用程式。

## 迄今為止的故事 {#story-so-far}

在AEM無頭歷程的上一份檔案中， [如何透過AEM Assets API更新您的內容](update-your-content.md) 您已學會如何透過API更新AEM中現有的無頭內容，現在應：

* 了解AEM Assets HTTP API。

本文以這些基本知識為基礎，讓您了解如何準備自己的AEM無頭專案以上線。

## 目標 {#objective}

本檔案可協助您了解AEM無頭發佈管道，以及在與應用程式上線前需要注意的效能考量事項。

* 了解AEM SDK及所需的開發工具
* 設定本機開發執行階段，以在上線前模擬您的內容
* 了解AEM內容復寫和快取基本知識
* 在啟動前保護並調整應用程式的規模
* 監控效能和除錯問題

## AEM SDK {#the-aem-sdk}

AEM SDK可用來建置和部署自訂程式碼。 這是您在開發和測試無頭應用程式之前所需的主要工具。 它包含下列成品：

* Quickstart jar — 可執行的jar檔案，可用於設定作者和發佈執行個體
* Dispatcher工具 — 適用於Windows和UNIX系統的Dispatcher模組及其相依性
* Java API Jar — 公開所有可用來針對AEM開發的允許Java API的Java Jar/Maven相依性
* Javadoc jar - Java API jar的javadoc

## 其他開發工具 {#additional-development-tools}

除了AEM SDK，您還需要其他工具來協助您在本機開發及測試程式碼和內容：

* Java
* Git
* 阿帕奇·馬文
* Node.js程式庫
* 您選擇的IDE

由於AEM是Java應用程式，因此您必須安裝Java和Java SDK，才能支援AEMas a Cloud Service的開發。

您可以使用Git來管理原始碼控制，以及檢查Cloud Manager的變更，然後將其部署至生產執行個體。

AEM使用Apache Maven來建置從AEM Maven專案原型產生的專案。 所有主要IDE都為Maven提供整合支援。

Node.js是JavaScript執行階段環境，用於搭配AEM專案的前端資產使用 `ui.frontend` 子專案。 Node.js與npm一起分發，npm是事實上的Node.js套件管理器，用於管理JavaScript相依性。

## AEM系統元件一覽 {#components-of-an-aem-system-at-a-glance}

接下來，讓我們看一下AEM環境的組成部分。

完整的AEM環境由製作、發佈和Dispatcher組成。 這些相同的元件會在本機開發執行階段中提供，讓您在上線前更輕鬆地預覽程式碼和內容。

* **作者服務** 是內部使用者建立、管理和預覽內容的位置。

* **發佈服務** 會視為「即時」環境，且通常是使用者與之互動的環境。 內容在Author服務上經過編輯和核准後，會分發（複製）至Publish服務。 AEM無頭式應用程式最常見的部署模式是讓生產版本的應用程式連線至AEM發佈服務。

* **Dispatcher** 是與AEM dispatcher模組增強的靜態Web伺服器。 它會快取由發佈例項產生的網頁，以提升效能。

## 本機開發工作流程 {#the-local-development-workflow}

本機開發專案以Apache Maven為基礎，且使用Git進行原始碼控制。 為了更新專案，開發人員可使用其偏好的整合開發環境，例如Eclipse、Visual Studio Code或IntelliJ等。

若要測試無頭應用程式將擷取的程式碼或內容更新，您必須將更新部署至本機AEM執行階段，其中包括AEM製作和發佈服務的本機例項。

請務必注意本機AEM執行階段中每個元件之間的差異，因為在最重要的位置測試更新非常重要。 例如，在製作上測試內容更新，或在發佈例項上測試新程式碼。

在生產系統中，Dispatcher和http Apache伺服器一律會位於AEM發佈例項之前。 它們為AEM系統提供快取和安全服務，因此也必須針對Dispatcher測試程式碼和內容更新。

## 使用本機開發環境在本機預覽您的程式碼和內容 {#previewing-your-code-and-content-locally-with-the-local-development-environment}

若要為啟動準備AEM無標題專案，您必須確定專案的所有組成部分都正常運作。

為此，您需要將所有內容整合在一起：程式碼、內容和設定，並在本機開發環境中測試，以備上線準備。

地方發展環境由三個主要領域組成：

1. AEM專案 — 這將包含AEM開發人員將要使用的所有自訂程式碼、設定和內容
1. 本機AEM執行階段 — 用於從AEM專案部署程式碼的AEM製作與發佈服務的本機版本
1. 本機Dispatcher執行階段 — 包含Dispatcher模組的Apache httpd網站伺服器的本機版本

設定本機開發環境後，您就可以在本機部署靜態節點伺服器，以模擬提供給React應用程式的內容。

若要深入了解如何設定本機開發環境，以及內容預覽所需的所有相依性，請參閱 [生產部署檔案](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/production-deployment.html?lang=en#prerequisites).

## 準備AEM Headless應用程式上線 {#prepare-your-aem-headless-application-for-golive}

<!-- Start of CDN Review -->

現在，您可以遵循以下概述的最佳實務，為您的AEM無頭應用程式做好啟動準備。

### 啟動前保護無頭應用程式 {#secure-and-scale-before-launch}

1. 準備 [驗證](/help/assets/content-fragments/graphql-authentication-content-fragments.md) GraphQL請求

### 模型結構與GraphQL輸出 {#structure-vs-output}

* 請避免建立輸出超過15kb JSON的查詢（gzip壓縮）。 長JSON檔案是需要大量資源，用戶端應用程式才能剖析。
* 避免超過五個巢狀片段階層。 額外的層級使得內容作者很難考慮其變更的影響。
* 使用多對象查詢，而不是在模型內建立具有相關性層次的模型查詢。 這可提供更長期的彈性，以重新建構JSON輸出，而無須進行大量內容變更。

### 最大化CDN快取點擊率 {#maximize-cdn}

* 請勿使用直接GraphQL查詢，除非您從表面要求即時內容。
   * 盡可能使用持續查詢。
   * 提供超過600秒的CDN TTL，讓CDN加以快取。
   * AEM可計算模型變更對現有查詢的影響。
* 在低內容和高內容變更率之間分割JSON檔案/GraphQL查詢，以減少CDN的用戶端流量並指派較高的TTL。 如此一來，CDN與來源伺服器重新驗證JSON的程度就能降到最低。
* 若要主動使CDN的內容失效，請使用「軟清除」。 這可讓CDN重新下載內容，而不會造成快取遺失。

>[!NOTE]
>
>請參閱 [其他資源](#additional-resources) 以取得CDN和快取的詳細資訊。

### 縮短下載無頭內容的時間 {#improve-download-time}

* 請確定HTTP用戶端使用HTTP/2。
* 請確定HTTP用戶端接受gzip的標題要求。
* 將用於托管JSON和參考成品的網域數減到最少。
* 運用 `Last-modified-since` 重新整理資源。
* 使用 `_reference` JSON檔案中的輸出，即可開始下載資產，而不需剖析完整的JSON檔案。

<!-- End of CDN Review -->

## 部署至生產環境 {#deploy-to-production}

部署至生產環境取決於您是否有 *傳統* 使用Maven進行部署，或位於Adobe Managed Services(AMS)上，因此使用Cloud Manager的AEM例項。

## 使用Maven部署至生產環境 {#deploy-to-production-maven}

若 *傳統* 使用Maven部署（非AMS），您可以看到 [WKND教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/project-setup.html?lang=en#build) 以取得概述。

## 使用Cloud Manager部署至生產環境 {#deploy-to-production-cloud-manager}

如果您是使用Cloud Manager的AMS客戶，則在您確定所有項目皆已測試且正常運作後，即可將程式碼更新推送至 [Cloud Manager中的集中式Git存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/setup-cloud-manager-git-integration.html).

將更新上傳至Cloud Manager後，即可使用 [Cloud Manager的CI/CD管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html).

<!-- Can't find a parallel link -->
<!--
You can start deploying your code by leveraging the Cloud Manager CI/CD pipeline, which is covered extensively [here](/help/implementing/deploying/overview.md).
-->

## 效能監控 {#performance-monitoring}

為了讓使用者在使用AEM無頭式應用程式時能有最佳體驗，請務必監控關鍵效能量度，如下所述：

* 驗證應用程式的預覽和生產版本
* 驗證AEM狀態頁以了解當前服務可用性狀態
* 訪問效能報告
   * 傳送效能
      * 來源伺服器 — 呼叫數、錯誤率、CPU負載、裝載流量
   * 作者效能
      * 檢查使用者、請求和載入數量
* 訪問特定於應用程式和空間的效能報告
   * 伺服器上線後，檢查一般量度是否為綠色/橙色/紅色，然後找出特定的應用程式問題
   * 開啟上方篩選至應用程式或空間的相同報表(例如Photoshop案頭、付費牆)
   * 使用Splunk日誌API訪問服務和應用程式效能
   * 如有其他問題，請聯絡客戶支援。

## 疑難排解 {#troubleshooting}

### 除錯 {#debugging}

請遵循下列最佳實務作為偵錯的一般方法：

* 使用應用程式的預覽版本驗證功能和效能
* 使用應用程式的生產版本驗證功能和效能
* 使用內容片段編輯器的JSON預覽進行驗證
* Inspect用戶端應用程式中的JSON，以檢查用戶端應用程式是否存在或傳送問題
* Inspect JSON使用GraphQL來檢查是否有與快取內容或AEM相關的問題

### 記錄有支援的錯誤 {#logging-a-bug-with-support}

若想透過支援有效記錄錯誤，以備您需要進一步協助時使用，請遵循下列步驟：

* 如有必要，請拍攝問題的螢幕截圖
* 記錄重現問題的方法
* 記錄問題用重制的內容
* 透過AEM支援入口網站以適當優先順序記錄問題

## 歷程結束了，還是結束了？ {#journey-ends}

恭喜！ 您已完成AEM Headless Developer Journey! 您現在應了解：

* 無頭式內容傳送與無頭式內容傳送之間的差異。
* AEM無頭功能。
* 如何組織及AEM Headless專案。
* 如何在AEM中建立無頭式內容。
* 如何在AEM中擷取和更新無標題內容。
* 如何與AEM Headless專案同時執行。
* 上線後怎麼辦。

您已啟動第一個AEM Headless專案，或現在擁有所需的所有知識。 幹得好！

### 探索單頁應用程式 {#explore-spa}

不過，AEM的無頭店不需要停在這裡。 您可能會記得 [快速入門歷程部分](getting-started.md#integration-levels) 我們簡要地討論了AEM如何不僅支援無頭式傳送和傳統的完整堆疊模型，還支援結合兩者優點的混合模型。

如果您專案需要這種彈性，請繼續前往歷程的其他選用部分， [如何使用AEM建立單頁應用程式(SPA)。](create-spa.md)

## 其他資源 {#additional-resources}

* [AEM Developing指南](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/the-basics.html?lang=en)

* [WKND教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=en)

* [適用於AEM的Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=en)

* CDN快取

   * [控制CDN快取](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html#controlling-a-cdn-cache)

   * 設定 [CDN重寫器](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/osgi-configuration-settings.html) (*搜尋CDN重寫器*)
