---
title: Adobe Experience Manager 6.5版中已棄用和已移除的功能。
description: Adobe Experience Manager 6.5中已棄用和已移除功能的發行說明。
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
source-git-commit: a76772b8761e35a828814ffe0ac3b019266ff008
workflow-type: tm+mt
source-wordcount: '1744'
ht-degree: 11%

---

# 過時和移除的功能 {#deprecated-and-removed-features}

Adobe 持續評估產品功能，以更新或替代的方式來改善或取代舊功能，以提升客戶享有的整體價值，且隨時謹慎考慮是否回溯相容。

為傳達AEM功能即將移除或遭取代的訊息，請套用下列規則：

1. 首先需公告功能已過時。雖然已過時，功能仍可供使用，但未進一步增強。
1. 下列主要版本最早會移除已棄用的功能。 將公佈實際的移除日期。

此程序可讓客戶在功能真正移除之前，至少還有一個發行週期，讓實作適應過時功能的新版本或後續版本。

## 過時的功能 {#deprecated-features}

本節列出AEM 6.5中已標示為過時的功能。通常，未來版本中預計移除的功能會先設為過時，並提供其他選項。

建議客戶檢視是否在目前的部署中使用這些功能，並規劃變更實作，改為使用所提供的替代方案。

| 區域 | 功能 | 替代方案 |
|---|---|---|
| [!DNL Sites] | 以範本為基礎的簡單內容片段。 | [現在提供模型型結構化](/help/assets/content-fragments/content-fragments-models.md) 內容片段。 |
| Creative Cloud整合 | AEM 6.2導入了「AEM到Creative Cloud資料夾共用」功能，作為讓創意使用者存取AEM資產的方式，以便在[!DNL Creative Cloud]應用程式中開啟資產，並上傳新檔案或儲存AEM的變更。 Creative Cloud 應用程式推出的新功能 Adobe Asset Link 提供了更優異的使用者體驗，以及更強大的存取功能，可直接從 Photoshop、InDesign 和 Illustrator 中存取 AEM 的資產。Adobe不打算進一步增強AEM以Creative Cloud資料夾共用整合。 雖然AEM中包含此功能，強烈建議客戶使用取代解決方案。 | 建議客戶改用新的Creative Cloud整合功能，包括Adobe資產連結或AEM案頭應用程式。 |
| 資產 | `AssetDownloadServlet` 依預設，發佈例項會停用。如需詳細資訊，請參閱[AEM安全性檢查清單](/help/sites-administering/security-checklist.md)。 | [AEM安全性檢查清單](/help/sites-administering/security-checklist.md)中描述的配置。 |
| 資產 | 如果用戶對`/content/dam/collections`沒有足夠的（讀和寫）權限，則用戶無法建立集合。 | 遵守使用者的存取控制設定，並確保適當的權限。 |
| Adobe Search&amp;Promote | 已棄用與Adobe Search&amp;Promote的整合。 Adobe不打算進一步增強「搜尋與促銷」整合。 請注意，Search &amp; Promote整合在遭取代時仍完全受支援。 |  |
| DTM標籤管理 | 已棄用與DTM（動態標籤管理器）的整合。 | 切換為使用Adobe Experience Platform Launch作為標籤管理程式。 |
| Adobe Target | 新增AEM可使用AEM 6.5中以[!DNL Adobe I/O]為基礎的Adobe Target Standard API(Rest API)連線至Adobe Target服務的功能後，Target Classic API(XML)方式已遭取代。 | 將整合重新設定為[使用新API](https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html)。 |
| Adobe Target | 不建議在AEM中使用與Adobe Target的`mbox.js`整合。 | 切換為使用`at.js` 1.x。 |
| 商務 | [CIF ](https://github.com/adobe/commerce-cif-api) REST是在2018年提供的微服務集，可整合AEM與商務引擎。在Adobe於2018年年中獲得Magento後，Adobe決定改變其做法，原因有二。 Magento有其專屬的商務API集（REST和GraphQL），維護兩組API並非理想的作法。 市場趨勢表明，客戶正轉向GraphQL，因為這是一種更高效的資料查詢方式。 2019年，Adobe發行了新的商務整合架構，使用Magento的GraphQL API作為真相的來源。 Adobe沒有計畫在CIF REST上再投資。 強烈建議客戶使用取代解決方案。 | 針對AEM-Magento整合，請切換至[AEM CIF原型](https://github.com/adobe/aem-cif-project-archetype)和[AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components)。 請參閱使用Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)的AEM與Magento整合[。 我們的藍圖中已列出支援與新方法整合的第三方(Magento除外)。 |
| 元件(AEM Sites) | Adobe不打算對儲存在`/libs/foundation/components`中的大多數基礎元件進行進一步的增強。 查看元件資料夾中的`cq:deprecated`和`cq:deprecatedReason`屬性。 AEM 6.5已包含Foundation元件，從舊版升級的客戶可繼續依原樣使用。 此外，即使已棄用，基礎元件仍完全受支援。 | Adobe建議在未來專案中使用核心元件。 現有網站可維持原狀，或使用[AEM現代化工具套裝](https://github.com/adobe/aem-modernize-tools)重新調整網站以使用核心元件。 |
| 元件(AEM Sites) | 設計匯入工具元件`/libs/wcm/designimporter/components`自6.5起已標示為已棄用。Adobe不打算對設計匯入工具的實作進一步增強。 | Adobe計畫在未來版本中提供使用案例的替代實作。 |
| Foundation | Granite卸載框架。 Adobe不打算對CQ 5.6.1中推出的卸載架構進行進一步增強，將資產處理外部化。 | Adobe正在開發新一代雲端原生卸載架構。 |
| 開發人員 | `Hobbes.js`. Adobe不打算對`hobbes.js`使用者介面測試架構進行進一步的增強。 | Adobe建議客戶使用Selenium自動化。 |
| 開發人員 | jQuery UI用戶端程式庫。 Adobe不打算進一步維護和更新作為分發（快速入門）一部分提供的jQuery UI客戶端庫 | Adobe建議仍需jQuery UI的客戶，將其程式碼新增至其專案程式碼基底。 |
| 開發人員 | jQuery Animation客戶端庫(`granite.jquery.animation`)。 Adobe不計畫進一步維護和更新作為分發(Quickstart)一部分提供的jQuery Animation客戶端庫 | Adobe建議仍需jQuery動畫才能使用程式碼的客戶，將其新增至專案程式碼基底。 |
| 開發人員 | Handlebars客戶端庫。 Adobe不計畫進一步維護和更新作為分發的一部分發運的Handlebar客戶端庫（快速入門） | Adobe建議仍需要Handlebars才能使用其程式碼的客戶，將其新增至其專案程式碼基底。 |
| 開發人員 | Lawnchair客戶端庫。 Adobe不計畫進一步維護和更新作為分發的一部分發運的Lawnchair客戶端庫（快速入門） | Adobe建議仍需要Lawnchair才能使用程式碼的客戶，將其新增至其專案程式碼基底。 |
| 開發人員 | `Granite.Sling.js` 用戶端程式庫。Adobe不打算進一步增強隨發佈(Quickstart)提供的Granite.Sling.js用戶端程式庫 | Adobe建議依賴程式庫功能的客戶重新調整其程式碼，不再使用。 |
| 開發人員 | 使用UI來壓縮/縮小JavaScript用戶端程式庫。 Adobe不打算進一步更新YUI程式庫。 在AEM 6.4之前，YUI預設為縮小JavaScript，並提供切換至Google關閉編譯器(GCC)的選項。 從AEM 6.5開始，預設為GCC。 | Adobe建議升級至AEM 6.5的客戶切換至GCC以進行實作 |
| 開發人員 | CRXDE lite中的傳統UI對話方塊編輯器。 Adobe不打算進一步增強發佈過程中隨附的傳統UI對話框編輯器（快速入門） | 無可替換。 |
| Forms | AEM Forms與AEM Mobile的整合已淘汰。 | 無可替換。 |  | 開發人員 | CRXDE lite中的傳統UI對話方塊編輯器。 Adobe不打算進一步增強發佈過程中隨附的傳統UI對話框編輯器（快速入門） | 無可替換。 |
| 開發人員 | Lodash/underscore客戶端庫。 Adobe不計畫進一步維護和更新作為分發（快速入門）的Lodash/underscore客戶端庫 | Adobe建議仍需使用Lodash/底線的客戶，將其程式碼新增至其專案程式碼基底。 |

## 移除的功能 {#removed-features}

本節列出已從AEM 6.5中移除的功能。舊版有這些功能標示為已過時。

| 區域 | 功能 | 替代方案 |
|--- |--- |--- |
| 與[!DNL Experience Cloud]整合 | 您可以透過[!DNL Adobe I/O]使用設定，將資產與[!DNL Experience Cloud]同步。 [!DNL Adobe Experience Cloud] 先前稱為 [!DNL Adobe Marketing Cloud]。 | 若您有任何疑問，請[聯絡Adobe客戶服務](https://www.adobe.com/tw/account/sign-in.supportportal.html)。 |
| AnalyticsActivity Map | AEM中包含的Activity Map版本。 | 由於 Adobe Analytics API 中的安全性變更，AEM 中包含的 Activity Map 版本已無法再使用。使用Adobe Analytics](https://docs.adobe.com/content/help/zh-Hant/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html)提供的[ActivityMap外掛程式。 |
| Integrations | ExactTarget整合已從預設分發(Quickstart)中移除，現在已無法使用。 | 沒有替換。 |
| 整合 | Salesforce Force API整合已從預設分發(Quickstart)中刪除，現在是要從[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)安裝的額外包。 | 功能仍可用。 |
| Forms | 由於不再支援Adobe中心產品，因此Adobe中心移轉橋服務的支援已遭移除。 | 沒有替換。 |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 沒有替換。 |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 無替換 |
| Forms | 無法在JEE上從LiveCycleES4 SP1升級至AEM 6.5 Forms的單跳升級 | 請參閱AEM Forms升級檔案中的[可用升級路徑](../forms/using/upgrade.md) 。 |
| Forms | 移除JEE上AEM Forms的UPD型叢集支援 | 在JEE上的AEM Forms中，您只能使用基於TCP的群集。 如果您將UDP多播伺服器從舊版升級為JEE上的AEM 5.5 Forms ，請執行手動配置以切換到基於TCP的gemfire群集。 如需詳細指示，請參閱JEE](../forms/using/upgrade-forms-jee.md)上的[升級至AEM 6.5表單 |
| 開發人員 | Firebug Lite已從預設分發(Quickstart)中移除 | 使用瀏覽器內建的開發人員主控台 |
| 開發人員 | 移除「HTML客戶端庫管理器」中的`customJavaScriptPath`支援。 | 無替換 |
| [!DNL Assets] | [!DNL Adobe Experience Manager] 6.5中移除了資產卸載功能。 | 無可替換。 |
| 快取 | `system/console/slingjsp` AEM 6.5中已不再提供移除功能。 | 類別和微快取儲存在Apache Sling Commons FileSystem ClassLoader套件組合下。 您可以在AEM Web Console中檢查套件組合編號，並直接從檔案系統中移除快取資料夾(`crx-quickstart/launchpad/felix/bundle<ID>`)。 |

## 下一版的預發佈 {#pre-announcement-for-next-release}

本節用於預先宣佈未來版本即將進行的變更。 已宣佈的變更尚未生效，但將影響客戶。 例如，功能尚未淘汰，但會在淘汰後影響使用者。 這些更新是為規劃目的而提供的。

| 區域 | 功能 | 公告 |
|--- |--- |--- |
| Foundation | UI架構 | Adobe預計於2019年淘汰Coral UI 2元件。 AEM 6.2導入了Coral UI 3，而AEM 6.5則完全以Coral 3為基礎。 Adobe建議已使用Coral 2建立自訂UI的客戶和合作夥伴，將其重構至Coral 3。 Adobe提供工具，可將Coral 2對話方塊轉換為Coral 3 - [了解詳情](/help/sites-developing/modernization-tools.md)。 |
