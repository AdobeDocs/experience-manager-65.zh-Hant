---
title: Adobe Experience Manager 6.5版本中已停用和移除的功能。
description: Adobe Experience Manager 6.5中已過時和已移除功能的發行說明。
translation-type: tm+mt
source-git-commit: 0560eb8e3c127964920827609a9982acf07b515f
workflow-type: tm+mt
source-wordcount: '1719'
ht-degree: 7%

---


# 過時和移除的功能 {#deprecated-and-removed-features}

Adobe 持續評估產品功能，以更新或替代的方式來改善或取代舊功能，以提升客戶享有的整體價值，且隨時謹慎考慮是否回溯相容。

若要傳達即將移除或取代AEM功能，請套用下列規則：

1. 首先需公告功能已過時。雖然已過時，但功能仍可用，但未進一步增強。
1. 最早會在下列主要版本中移除已過時的功能。 將公佈實際的移除目標日期。

此程序可讓客戶在功能真正移除之前，至少還有一個發行週期，讓實作適應過時功能的新版本或後續版本。

## 過時的功能 {#deprecated-features}

本節列出已標示為不再提倡的AEM 6.5功能。通常，計畫在未來版本中移除的功能會先設為不建議使用，並提供其他選項。

建議客戶檢視是否在目前的部署中使用這些功能，並規劃變更實作，改為使用所提供的替代方案。

| 區域 | 功能 | 替代方案 |
|---|---|---|
| Creative Cloud整合 | AEM到Creative Cloud資料夾共用功能已在AEM 6.2中推出，讓創意使用者可存取AEM的資產，如此他們就可以在CC應用程式中開啟資產，並上傳新檔案或儲存對AEM所做的變更。 Creative Cloud應用程式中發行的新功能Adobe Asset Link提供更佳的使用者體驗，並可直接從Photoshop、InDesign和Illustrator內部，以更強大的方式存取AEM中的資產。 Adobe不打算對AEM做進一步的增強，以整合Creative Cloud資料夾共用。 雖然AEM中包含此功能，但強烈建議客戶使用取代解決方案。 | 建議客戶改用新的Creative Cloud整合功能，包括Adobe Asset Link或AEM案頭應用程式。 請參閱AEM和Creative Cloud整合最佳實務，以取得詳細資訊。 |
| 資產 | `AssetDownloadServlet` 預設會停用發佈例項。如需詳細資訊，請參閱[AEM安全性檢查清單](/help/sites-administering/security-checklist.md)。 | [AEM安全性檢查清單](/help/sites-administering/security-checklist.md)中說明的設定。 |
| 資產 | 如果使用者對`/content/dam/collections`沒有足夠的（讀取和寫入）權限，則使用者無法建立系列。 | 遵循使用者的存取控制設定，並確保適當的權限。 |
| Adobe Search &amp; Promote | 不再提倡與Adobe Search &amp; Promote的整合。 Adobe不打算對「搜尋與促銷」整合做進一步的增強。 請注意，Search &amp; Promote整合仍完全受支援，但不建議使用。 |  |
| DTM標籤管理器 | 不再支援與DTM（動態標籤管理器）的整合。 | 切換使用Adobe Experience Platform Launch做為標籤管理程式。 |
| Adobe Target | 在AEM 6.5中新增AEM使用[!DNL Adobe I/O]架構的Adobe Target Standard API(Rest API)連線至Adobe Target服務的功能後，Target Classic API(XML)方式即不再提供。 | 將整合重新設定為[使用新的API](https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html)。 |
| Adobe Target | 不建議在AEM中使用與Adobe Target的`mbox.js`整合。 | 切換為使用`at.js` 1.x。 |
| 商務 | [CIF ](https://github.com/adobe/commerce-cif-api) REST是在2018年提供的一套微型服務，可讓AEM與商務引擎整合。在Adobe於2018年年中收購Magento後，Adobe決定改變其方式，原因有二。 Magento有自己的一組商務API（REST和GraphQL），維護兩組API並不是很好的做法。 市場趨勢表明，客戶正在向GraphQL靠攏，因為GraphQL是一種更高效的資料查詢方式。 在2019年，Adobe已推出新的商務整合架構，使用Magento的GraphQL API作為真相來源。 Adobe並不打算進一步投資CIF REST。 強烈建議客戶使用更換解決方案。 | 對於AEM-Magento整合，請切換至[AEM CIF Archetype](https://github.com/adobe/aem-cif-project-archetype)和[AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components)。 請參閱「使用商務整合架構」的AEM和Magento整合[。 ](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)我們的規劃藍圖中已列出支援協力廠商（Magento除外）與新方法整合的功能。 |
| 元件(AEM Sites) | Adobe不打算對儲存在`/libs/foundation/components`中的大部分Foundation Components進行進一步的增強。 在元件資料夾中查找`cq:deprecated`和`cq:deprecatedReason`屬性。 AEM 6.5包含Foundation Components，而從舊版升級的客戶可依現狀繼續使用這些元件。 此外，即使已停用，Foundation Components仍完全受支援。 | Adobe建議未來專案使用核心元件。 現有網站可維持原狀，或使用[AEM最新化工具套件](https://github.com/adobe/aem-modernize-tools)重新調整網站以使用核心元件。 |
| 元件(AEM Sites) | Design Importer元件`/libs/wcm/designimporter/components`已標示為6.5起已停用。Adobe不打算對該設計匯入工具的實作進行進一步的增強。 | Adobe計畫在未來版本中提供使用案例的替代實作。 |
| 基礎 | 花崗岩卸載架構。 Adobe不打算對CQ 5.6.1中引進的卸載架構做進一步的增強，以將資產處理外部化。 | Adobe正在研發新一代雲端原生卸載架構。 |
| 開發人員 | `Hobbes.js`. Adobe不打算對`hobbes.js`使用者介面測試架構做進一步的增強。 | Adobe建議客戶使用Selenium自動化。 |
| 開發人員 | jQuery UI用戶端程式庫。 Adobe不打算進一步維護和更新發佈時隨附的jQuery UI用戶端程式庫（快速入門） | Adobe建議仍需要jQuery UI才能使用其程式碼的客戶，將其新增至專案程式碼庫。 |
| 開發人員 | jQuery Animation用戶端程式庫(`granite.jquery.animation`)。 Adobe不打算進一步維護和更新作為散發一部分而隨附的jQuery Animation用戶端程式庫(Quickstart) | Adobe建議仍需jQuery Animations才能使用其程式碼的客戶，將其新增至專案程式碼庫。 |
| 開發人員 | Handlebars客戶程式庫。 Adobe不打算進一步維護和更新Handlebar用戶端程式庫，此程式庫是做為散發的一部份(Quickstart) | Adobe建議仍需要Handlebars代碼的客戶，將其加入專案代碼庫。 |
| 開發人員 | Lawnchair客戶資料庫。 Adobe不打算進一步維護和更新Lawnshair用戶端程式庫(Quickstart)，此程式庫會隨散發一起運送 | Adobe建議仍需Lawnchair才能使用程式碼的客戶，將其新增至專案程式碼庫。 |
| 開發人員 | `Granite.Sling.js` 用戶端程式庫。Adobe不打算進一步增強Granite.Sling.js用戶端程式庫，此程式庫會隨散發(Quickstart)一起出貨 | Adobe建議依賴程式庫功能的客戶重新調整其程式碼，以便不再使用。 |
| 開發人員 | 使用UI來壓縮／精簡JavaScript用戶端程式庫。 Adobe不打算進一步更新UYI程式庫。 在AEM 6.4之前，UYI預設為使用切換至Google Closure Compiler(GCC)的選項來精簡JavaScript。 從AEM 6.5開始，GCC為預設值。 | Adobe建議升級至AEM 6.5的客戶切換至GCC以進行實作 |
| 開發人員 | CRXDE lite中的傳統UI對話框編輯器。 Adobe不打算進一步增強散發時隨附的Classic UI Dialog Editor（快速入門） | 沒有可替換的。 |
| 表單 | AEM Forms與AEM Mobile的整合已過時。 | 沒有可用的替換。 |  | 開發人員 | CRXDE lite中的傳統UI對話框編輯器。 Adobe不打算進一步增強散發時隨附的Classic UI Dialog Editor（快速入門） | 沒有可替換的。 |
| 開發人員 | Lodash/下划線客戶端庫。 Adobe不打算進一步維護和更新Lodash/底線用戶端程式庫，此程式庫會隨散發（快速入門）一起出貨 | Adobe建議仍需使用Lodash/底線的客戶將程式碼新增至其專案程式碼庫。 |

## 移除的功能 {#removed-features}

本節列出已從AEM 6.5移除的功能。舊版的這些功能已標示為已過時。

| 區域 | 功能 | 替代方案 |
|--- |--- |--- |
| Analytics Activity Map | AEM中包含的Activity Map版本。 | 由於Adobe Analytics API中的安全性變更，無法再使用AEM中包含的Activity Map版本。 使用Adobe Analytics](https://docs.adobe.com/content/help/en/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html)提供的[ActivityMap外掛程式。 |
| 整合 | ExactTarget整合已從預設分發（快速入門）中移除，現已不再提供。 | 沒有替換。 |
| 整合 | Salesforce Force API整合已從預設散發(Quickstart)中移除，現在是從[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)安裝的額外套件。 | 此功能仍然可用。 |
| 表單 | Adobe Central Migration Bridge服務的支援已移除，因為不再支援Adobe Central產品。 | 沒有替換。 |
| 表單 | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 沒有替換。 |
| 表單 | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 無取代 |
| 表單 | JEE上不提供從LiveCycle ES4 SP1升級至AEM 6.5 Forms的單跳升級 | 請參閱AEM Forms升級檔案中的[可用升級路徑](../forms/using/upgrade.md)。 |
| 表單 | 從JEE上的AEM Forms移除以UPD為基礎的叢集支援 | 在JEE上的AEM Forms中，您只能使用TCP叢集。 如果您將UDP多點傳播伺服器從舊版升級至JEE上的AEM 5.5 Forms，請執行手動組態，以切換至以TCP為基礎的gemfire叢集。 如需詳細指示，請參閱JEE上的[升級至AEM 6.5表格](../forms/using/upgrade-forms-jee.md) |
| 開發人員 | Firebug Lite已從預設散發中移除（快速入門） | 使用瀏覽器內建的開發人員主控台 |
| 開發人員 | 移除HTML Client Library Manager中的`customJavaScriptPath`支援。 | 無取代 |
| [!DNL Assets] | [!DNL Adobe Experience Manager] 6.5會移除資產卸載功能。 | 沒有可替換的。 |
| 快取 | `system/console/slingjsp` is removed is nore available in AEM 6.5. | Classes and Lightly cache會儲存在Apache Sling Commons FileSystem ClassLoader套件下。 您可以在AEM Web Console中檢查套件編號，並直接從檔案系統(`crx-quickstart/launchpad/felix/bundle<ID>`)移除快取資料夾。 |

## 下一版的預發佈{#pre-announcement-for-next-release}

本節用於預先宣佈未來發行中即將進行的變更。 宣佈的變更尚未生效，但會影響客戶。 例如，功能尚未過時，但淘汰後會影響使用者。 這些更新是為了規劃目的而提供的。

| 區域 | 功能 | 公告 |
|--- |--- |--- |
| 基礎 | UI架構 | Adobe計畫在2019年淘汰Coral UI 2元件。 AEM 6.2已推出Coral UI 3，而AEM 6.5則完全以Coral 3為基礎。 Adobe建議已使用Coral 2建立自訂UI的客戶和合作夥伴，將它們重新分解至Coral 3。 Adobe提供工具，將Coral 2對話方塊轉換為Coral 3 - [閱讀更多資訊](/help/sites-developing/dialog-conversion.md)。 |
