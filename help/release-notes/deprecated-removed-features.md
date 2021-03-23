---
title: Adobe Experience Manager6.5版中已過時和已移除的功能。
description: 針對Adobe Experience Manager6.5中已過時和已移除功能的發行說明。
translation-type: tm+mt
source-git-commit: 7035c19a109ff67655ee0419aa37d1723e2189cc
workflow-type: tm+mt
source-wordcount: '1719'
ht-degree: 11%

---


# 過時和移除的功能 {#deprecated-and-removed-features}

Adobe 持續評估產品功能，以更新或替代的方式來改善或取代舊功能，以提升客戶享有的整體價值，且隨時謹慎考慮是否回溯相容。

要通知即將拆除或替換功能AEM，請遵守以下規則：

1. 首先需公告功能已過時。雖然已過時，但功能仍可用，但未進一步增強。
1. 最早會在下列主要版本中移除已過時的功能。 將公佈實際的移除目標日期。

此程序可讓客戶在功能真正移除之前，至少還有一個發行週期，讓實作適應過時功能的新版本或後續版本。

## 過時的功能 {#deprecated-features}

本節列出已標示為已停用6.5的功AEM能和功能。通常，計畫在未來版本中移除的功能會先設為不建議使用，並提供其他選項。

建議客戶檢視是否在目前的部署中使用這些功能，並規劃變更實作，改為使用所提供的替代方案。

| 區域 | 功能 | 替代方案 |
|---|---|---|
| Creative Cloud整合 | 在AEMAEM6.2中引入「Creative Cloud資料夾共用」，讓創意使用者可存取其中的資產AEM，以便在CC應用程式中開啟資產，並上傳新檔案或儲存變更AEM。 Creative Cloud 應用程式推出的新功能 Adobe Asset Link 提供了更優異的使用者體驗，以及更強大的存取功能，可直接從 Photoshop、InDesign 和 Illustrator 中存取 AEM 的資產。Adobe不打算對「Creative Cloud資料夾共用」集AEM成進行進一步的增強。 雖然功能已包含在內，AEM但強烈建議客戶使用取代解決方案。 | 建議客戶改用新的Creative Cloud整合功能，包括Adobe資產連結或案頭應AEM用程式。 檢閱和AEMCreative Cloud整合最佳實務，以取得詳細資訊。 |
| 資產 | `AssetDownloadServlet` 預設會停用發佈例項。如需詳細資訊，請參閱[AEM安全性檢查清單](/help/sites-administering/security-checklist.md)。 | [安全檢查清單AEM](/help/sites-administering/security-checklist.md)中說明的配置。 |
| 資產 | 如果使用者對`/content/dam/collections`沒有足夠的（讀取和寫入）權限，則使用者無法建立系列。 | 遵循使用者的存取控制設定，並確保適當的權限。 |
| Adobe Search&amp;Promote | 與Adobe Search&amp;Promote的整合已過時。 Adobe不打算對「搜尋與促銷」整合做進一步的增強。 請注意，Search &amp; Promote整合仍完全受支援，但不建議使用。 |  |
| DTM標籤管理器 | 不再支援與DTM（動態標籤管理器）的整合。 | 切換使用Adobe Experience Platform Launch做標籤管理程式。 |
| Adobe Target | 在6.5中新AEM增使用[!DNL Adobe I/O]架構的Adobe Target標準API(Rest API)連線至Adobe Target服務的能力AEM,Target Classic API(XML)方式已不再使用。 | 將整合重新設定為[使用新的API](https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html)。 |
| Adobe Target | 不建議在中使用以`mbox.js`為基礎的與Adobe TargetAEM的整合。 | 切換為使用`at.js` 1.x。 |
| 商務 | [CIF ](https://github.com/adobe/commerce-cif-api) REST是於2018年提供的一套微型服務，以整合商務引AEM擎。在Adobe於2018年年中獲得Magento後，Adobe決定改變其做法，原因有二。 Magento有自己的一組商務API（REST和GraphQL），維護兩組API並不是很好的做法。 市場趨勢表明，客戶正在向GraphQL靠攏，因為GraphQL是一種更高效的資料查詢方式。 2019年，Adobe以Magento的GraphQL API作為真相來源，發佈了新的商務整合框架。 Adobe不打算在CIF REST公司做進一步投資。 強烈建議客戶使用更換解決方案。 | 對於AEMMagento整合，請切換到&lt;a0/AEM>CIF Archetype](https://github.com/adobe/aem-cif-project-archetype)和[AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components)。 [請參AEM閱使用Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)Magento整合[。 我們的規劃藍圖中已列出支援協力廠商(Magento除外)與新方法整合的方案。 |
| 元件(AEM Sites) | Adobe不打算對儲存在`/libs/foundation/components`中的大多數基礎元件進行進一步的增強。 在元件資料夾中查找`cq:deprecated`和`cq:deprecatedReason`屬性。 AEM6.5包含Foundation Components，而舊版升級的客戶可依現狀繼續使用。 此外，即使已停用，Foundation Components仍完全受支援。 | Adobe建議將核心元件用於未來的專案。 現有網站可維持原狀，或使用[最新化工具套AEM件](https://github.com/adobe/aem-modernize-tools)重新調整網站以使用核心元件。 |
| 元件(AEM Sites) | Design Importer元件`/libs/wcm/designimporter/components`已標示為6.5起已停用。Adobe不打算對設計匯入工具的實施進行進一步的增強。 | Adobe計畫在未來版本中提供使用案例的替代實作。 |
| Foundation | 花崗岩卸載架構。 Adobe不打算對CQ 5.6.1中引入的卸載框架做進一步的改進，以將資產處理外部化。 | Adobe正在開發新一代雲端原生卸載架構。 |
| 開發人員 | `Hobbes.js`. Adobe不打算對`hobbes.js`使用者介面測試架構做進一步的增強。 | Adobe建議客戶使用Selenium自動化。 |
| 開發人員 | jQuery UI用戶端程式庫。 Adobe不打算進一步維護和更新作為分發的一部分發運的jQuery UI客戶端庫（快速啟動） | Adobe建議仍需要jQuery UI才能使用其程式碼的客戶，將其新增至專案程式碼庫。 |
| 開發人員 | jQuery Animation用戶端程式庫(`granite.jquery.animation`)。 Adobe不打算進一步維護和更新作為分發的一部分發運的jQuery Animation客戶端庫（快速啟動） | Adobe建議仍需要jQuery動畫做為程式碼的客戶，將其新增至專案程式碼庫。 |
| 開發人員 | Handlebars客戶程式庫。 Adobe不打算進一步維護和更新作為分發的一部分發運的Handlebar客戶端庫（快速入門） | Adobe建議仍需要Handlebars代碼的客戶，將其加入專案程式碼庫。 |
| 開發人員 | Lawnchair客戶資料庫。 Adobe不打算進一步維護和更新作為分發的一部分發運的Lawnshair客戶端庫（快速入門） | Adobe建議仍需Lawnchair才能使用程式碼的客戶，將程式碼加入其專案程式碼庫。 |
| 開發人員 | `Granite.Sling.js` 用戶端程式庫。Adobe不打算進一步增強Granite.Sling.js用戶端程式庫，此程式庫會隨散發(Quickstart)一起出貨 | Adobe建議依賴程式庫功能的客戶重新調整其程式碼，以便不再使用它。 |
| 開發人員 | 使用UI來壓縮／精簡JavaScript用戶端程式庫。 Adobe不打算進一步更新UI程式庫。 在6.AEM4之前，UYI預設為使用切換至Google Closure Compiler(GCC)的選項來精簡JavaScript。 從AEM6.5開始，GCC為預設值。 | Adobe建議升級至AEM6.5的客戶改用GCC進行實作 |
| 開發人員 | CRXDE lite中的傳統UI對話框編輯器。 Adobe不打算進一步增強作為分發的一部分附帶的傳統UI對話框編輯器（快速入門） | 沒有可替換的。 |
| 表單 | AEM Forms與AEM Mobile的整合已過時。 | 沒有可用的替換。 |  | 開發人員 | CRXDE lite中的傳統UI對話框編輯器。 Adobe不打算進一步增強作為分發的一部分附帶的傳統UI對話框編輯器（快速入門） | 沒有可替換的。 |
| 開發人員 | Lodash/下划線客戶端庫。 Adobe不打算進一步維護和更新作為分發的一部分附帶的Lodash/下划線客戶端庫（快速入門） | Adobe建議仍需使用Lodash/底線的客戶將程式碼新增至其專案程式碼庫。 |

## 移除的功能 {#removed-features}

本節列出已從6.5移除的AEM功能。舊版的這些功能已標示為已過時。

| 區域 | 功能 | 替代方案 |
|--- |--- |--- |
| 分析Activity Map | 包含在中的Activity Map版本AEM。 | 由於 Adobe Analytics API 中的安全性變更，AEM 中包含的 Activity Map 版本已無法再使用。使用Adobe Analytics提供的[ActivityMap外掛程式。](https://docs.adobe.com/content/help/zh-Hant/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) |
| Integrations | ExactTarget整合已從預設分發（快速入門）中移除，現已不再提供。 | 沒有替換。 |
| 整合 | Salesforce Force API整合已從預設散發(Quickstart)中移除，現在是從[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)安裝的額外套件。 | 此功能仍然可用。 |
| 表單 | 已刪除對Adobe中央遷移橋服務的支援，因為不再支援Adobe中心產品。 | 沒有替換。 |
| 表單 | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 沒有替換。 |
| 表單 | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 無取代 |
| 表單 | JEE上的單跳從LiveCycleES4 SP1升級AEM到6.5Forms | 請參閱AEM Forms升級檔案中的[可用升級路徑](../forms/using/upgrade.md)。 |
| 表單 | 在JEE上從AEM Forms移除基於UPD的聚類支援 | 在JEE上，您只能在AEM Forms使用基於TCP的群集。 如果您將JEE上的UDP組播伺服器從舊版升級到AEM5.5Forms，請執行手動配置以切換到基於TCP的gemfire群集。 如需詳細指示，請參閱JEE上的[升AEM級至6.5表單](../forms/using/upgrade-forms-jee.md) |
| 開發人員 | Firebug Lite已從預設散發中移除（快速入門） | 使用瀏覽器內建的開發人員主控台 |
| 開發人員 | 移除HTML Client Library Manager中的`customJavaScriptPath`支援。 | 無取代 |
| [!DNL Assets] | [!DNL Adobe Experience Manager] 6.5會移除資產卸載功能。 | 沒有可替換的。 |
| 快取 | `system/console/slingjsp` 在6.5中已不再AEM提供。 | Classes and Lightly cache會儲存在Apache Sling Commons FileSystem ClassLoader套件下。 您可以在Web控制台中檢查包號AEM，並直接從檔案系統(`crx-quickstart/launchpad/felix/bundle<ID>`)中刪除快取資料夾。 |

## 下一版的預發佈{#pre-announcement-for-next-release}

本節用於預先宣佈未來發行中即將進行的變更。 宣佈的變更尚未生效，但會影響客戶。 例如，功能尚未過時，但淘汰後會影響使用者。 這些更新是為了規劃目的而提供的。

| 區域 | 功能 | 公告 |
|--- |--- |--- |
| 基礎 | UI架構 | Adobe計畫在2019年淘汰Coral UI 2元件。 Coral UI 3隨附於AEM6.2,AEM6.5完全以Coral 3為基礎。 Adobe建議已使用Coral 2建立自訂UI的客戶和合作夥伴，將它們重新分解至Coral 3。 Adobe提供將Coral 2對話方塊轉換為Coral 3 - [閱讀更多資訊](/help/sites-developing/modernization-tools.md)的工具。 |
