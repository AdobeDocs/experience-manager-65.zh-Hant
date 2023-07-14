---
title: Adobe Experience Manager 6.5版本中已過時和已移除的功能。
description: 特定於Adobe Experience Manager 6.5中已過時和已移除功能的發行說明。
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
source-git-commit: 11e848d93964b5f8e45ccd7388a48953a3148e35
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 12%

---

# 過時和移除的功能 {#deprecated-and-removed-features}

Adobe 持續評估產品功能，以更新或替代的方式來改善或取代舊功能，以提升客戶享有的整體價值，且隨時謹慎考慮是否回溯相容。

若要傳達AEM功能即將移除或取代的訊息，請套用下列規則：

1. 首先需公告功能已過時。雖然已棄用，但功能仍可使用，但不會進一步增強。
1. 下列主要發行版本最先會移除已棄用的功能。 將會宣佈實際的目標移除日期。

此程序可讓客戶在功能真正移除之前，至少還有一個發行週期，讓實作適應過時功能的新版本或後續版本。

## 過時的功能 {#deprecated-features}

本節列出AEM 6.5中標示為過時的功能。通常，未來新版本預計移除的功能，將先設為棄用，並提供其他選項。

建議客戶檢閱是否在目前的部署中使用這些功能，並規劃變更實作，改用所提供的替代方案。

| 區域 | 功能 | 替代方案 | 版本 (SP) |
|---|---|---|---|
| [!DNL Sites] | **社交媒體狀態**&#x200B;的體驗片段屬性。 |   | 6.5.11.0 |
| [!DNL Sites] | 內容片段範本，用於建立簡單內容片段。 | 現在[基於模型的結構化內容片段](/help/assets/content-fragments/content-fragments-models.md)。 | 6.5.11.0 |
| Creative Cloud整合 | AEM 6.2引入了AEM到Creative Cloud資料夾共用功能，作為讓創意使用者存取AEM中的資產以便他們可以在中開啟資產的方式 [!DNL Creative Cloud] 應用程式並上傳新檔案或儲存變更至AEM。 Creative Cloud 應用程式推出的新功能 Adobe Asset Link 提供了更優異的使用者體驗，以及更強大的存取功能，可直接從 Photoshop、InDesign 和 Illustrator 中存取 AEM 的資產。Adobe不打算進一步增強AEM的「Creative Cloud資料夾共用」整合。 雖然此功能包含在AEM中，但建議客戶使用替代解決方案。 | 建議客戶改用新的Creative Cloud整合功能，包括Adobe資產連結或AEM案頭應用程式。 |  |
| Assets | `AssetDownloadServlet` 發佈執行個體預設為停用。 如需詳細資訊，請參閱 [AEM安全性檢查清單](/help/sites-administering/security-checklist.md). | 設定說明於 [AEM安全性檢查清單](/help/sites-administering/security-checklist.md). |  |
<!-- Search&Promote is end-of-life September 1, 2022 | Assets | If a user does not have sufficient (read and write) permissions on `/content/dam/collections`, the user cannot create a Collection. | Honor the access control setup of user and ensure appropriate permissions. ||
|Adobe Search & Promote|The integration with Adobe Search & Promote is deprecated. Adobe does not plan to make further enhancements to the Search & Promote integration. Adobe Search & Promote integration remains fully supported while being deprecated.||| -->
| DTM標籤管理員 |不建議使用DTM (Dynamic Tag Manager)整合。 |切換以使用Adobe Experience Platform Launch作為標籤管理員。 || |Adobe Target|新增AEMAdobe Target的功能，以使用 [!DNL Adobe I/O] 以AEM 6.5中的Adobe Target Standard API (Rest API)為基礎，Target Classic API (XML)方式已過時。|將整合重新設定為 [使用新API](/help/sites-administering/target.md). || |Adobe Target|使用 `mbox.js` 不建議使用AEM中與Adobe Target的整合。|切換以使用 `at.js` 1.x.|| |商務 | [CIF REST](https://github.com/adobe/commerce-cif-api) 在2018年提供了一系列微服務，以啟用AEM與商務引擎之間的整合。 Adobe在2018年年中取得Magento後，Adobe決定變更其方法，原因有二。 Magento有自己的Commerce API集(REST和GraphQL)，維護兩組API是不好的做法。 市場趨勢顯示客戶正轉向GraphQL，因為這是查詢資料的更有效率。 2019年，Adobe發行了新的Commerce Integration Framework，使用Magento的GraphQL API作為真相來源。 Adobe不打算進一步投資CIF REST。 建議客戶使用替代解決方案。|若為AEMMagento整合，請切換至 [AEM CIF原型](https://github.com/adobe/aem-cif-project-archetype) 和 [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components). 請參閱AEM與Adobe Commerce整合 [使用Commerce Integration Frame](/help/commerce/cif/integrating/magento.md). 新方法支援協力廠商(Magento除外)整合，具體內容已列入我們的藍圖中。|| |元件(AEM Sites) |Adobe不打算進一步增強中儲存的大部分基礎元件 `/libs/foundation/components`. 尋找 `cq:deprecated` 和 `cq:deprecatedReason` 屬性。 AEM 6.5已包含基礎元件，而從舊版升級的客戶可繼續依原樣使用這些元件。 此外，即使已棄用，亦支援基礎元件。 | Adobe建議將核心元件用於未來的專案。 現有網站可維持原狀，或使用 [AEM Modernize Tools Suite](https://github.com/adobe/aem-modernize-tools) 以重構網站以使用核心元件。 || |元件(AEM Sites)|Design Importer元件 `/libs/wcm/designimporter/components` 從6.5開始標籤為已棄用。Adobe不打算進一步增強「設計匯入工具」實作。 |Adobe計畫在未來版本中提供使用案例的替代實施。 || |Foundation|Granite解除安裝架構。 Adobe不打算進一步增強CQ 5.6.1中推出的解除安裝架構，以將資產處理外部化。|Adobe正在開發新一代的雲端原生解除安裝架構。||
|開發人員|`Hobbes.js`. Adobe不打算進一步增強 `hobbes.js` 使用者介面測試架構。|Adobe建議客戶使用Selenium自動化。|| |開發人員|jQuery UI使用者端程式庫。 Adobe不打算進一步維護和更新隨散發提供的jQuery UI使用者端程式庫（快速入門）|Adobe建議仍需要jQuery UI才能使用程式碼的客戶，將其新增至專案程式碼基底。|| |開發人員|jQuery Animation使用者端程式庫(`granite.jquery.animation`)。 Adobe不打算進一步維護及更新隨附於發行的jQuery Animation使用者端程式庫（快速入門）|Adobe建議仍然需要jQuery Animations程式碼的客戶將其新增到專案程式碼庫中。|| |開發人員|Handlebars使用者端程式庫。 Adobe不打算進一步維護和更新隨散發提供的Handlebar使用者端程式庫（快速入門）|Adobe建議仍需要Handlebars程式碼的客戶將其新增至專案程式碼基底。|| |開發人員|Lawnchair使用者端資料庫。 Adobe不打算進一步維護和更新隨散發功能提供的Lawnchair使用者端程式庫（快速入門）|Adobe建議仍需要Lawnchair程式碼的客戶將其新增至專案程式碼基底。|| |開發人員|`Granite.Sling.js` 使用者端資源庫。 Adobe不打算進一步增強隨附於散發的Granite.Sling.js使用者端程式庫（快速入門）|Adobe建議依賴程式庫功能的客戶重構其程式碼，不再使用。|| |開發人員|使用YUI壓縮/縮制JavaScript使用者端程式庫。 Adobe不打算進一步更新YUI程式庫。 直到AEM 6.4之前，YUI預設會使用切換至Google Closure Compiler (GCC)的選項來縮制JavaScript。 從AEM 6.5開始，GCC為預設值。|Adobe建議客戶升級至AEM 6.5，以切換至GCC進行實作|| |開發人員|傳統UI對話方塊編輯器(CRXDE Lite)。 Adobe不打算進一步增強散發隨附的Classic UI對話方塊編輯器（快速入門）|沒有可用的替代。 || |Forms|AEM Forms與AEM Mobile的整合已過時。 |沒有可用的替代專案。 CRXDE Lite中的開發人員Classic UI對話方塊編輯器。 Adobe不打算進一步增強散發隨附的Classic UI對話方塊編輯器（快速入門）|沒有可用的替代。 || |開發人員|Lodash/Underscore使用者端資源庫。 Adobe不打算進一步維護和更新隨分送（快速入門）提供的Lodash/underscore使用者端程式庫 | Adobe建議仍需將程式碼加到底線的客戶，將其新增至專案程式碼基底。 || |Screens|Adobe不打算進一步維護和更新2Publishers設定所使用的com.adobe.cq.screens.mq.activemq套件組合和相關設定。| Adobe建議仍需要2Publishers設定的客戶可使用 [負載平衡器](https://wiki.corp.adobe.com/pages/viewpage.action?spaceKey=screens&amp;title=AEM+Screens+publish+environment+horizontal+scaling+through+Load+Balancer+session+stickiness) 方法。 ||

## 移除的功能 {#removed-features}

本節列出已從AEM 6.5移除的功能。舊版將這些功能標籤為已過時。

| 區域 | 功能 | 替代方案 | 版本 (SP) |
|--- |--- |--- |--- |
|  與 [!DNL Experience Cloud] 整合 | 您可以將資產與同步 [!DNL Experience Cloud] 透過使用設定 [!DNL Adobe I/O]. [!DNL Adobe Experience Cloud] 之前稱為 [!DNL Adobe Experience Cloud]. | 如果您有任何查詢， [聯絡Adobe客戶支援](https://experienceleague.adobe.com/?support-solution=General#support). |  |
| AnalyticsActivity Map | AEM中包含的Activity Map版本。 | 由於 Adobe Analytics API 中的安全性變更，AEM 中包含的 Activity Map 版本已無法再使用。使用 [Adobe Analytics提供的ActivityMap外掛程式](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=zh-Hant). |  |
| 整合 | ExactTarget整合已從預設發佈（快速入門）中移除，且不再可用。 | 無替代方案。 |  |
| 整合 | Salesforce Force API整合已從預設發佈（快速入門）中移除，現在是一個額外的套件，可從此處安裝 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). | 此功能仍然可用。 |
| Forms | 對Adobe Central Migration Bridge服務的支援已移除，因為已不再支援Adobe Central產品。 | 無替代方案。 |  |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 無替代方案。 |  |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 無替代 |  |
| Forms | JEE版不提供從LiveCycleES4 SP1到AEM 6.5 Forms的單躍點升級 | 另請參閱 [可用的升級路徑](../forms/using/upgrade.md) 在AEM Forms升級檔案中。 |  |
| Forms | 從AEM Forms on JEE移除UPD型叢集支援 | 您只能在AEM Forms on JEE中使用TCP型叢集。 如果您將UDP多點傳送伺服器從舊版升級至JEE上的AEM 5.5 Forms，請執行手動設定，以切換至以TCP為基礎的Gemfire叢集。 如需詳細指示，請參閱 [在JEE上升級至AEM 6.5 forms](../forms/using/upgrade-forms-jee.md) |  |
| 開發人員 | Firebug Lite已從預設散發中移除（快速入門） | 使用瀏覽器內建的開發人員主控台 |
| 開發人員 | 移除 `customJavaScriptPath` HTML使用者端資源庫管理員的支援。 | 無替代 |  |
| [!DNL Assets] | 資產解除安裝功能在中移除 [!DNL Adobe Experience Manager] 6.5. | 沒有可用的替代專案。 |  |
| 快取 | `system/console/slingjsp` 「 」已移除「 」在AEM 6.5中不再提供。 | 類別和Slightly快取儲存在Apache Sling Commons FileSystem ClassLoader套件組合下。 您可以在AEM Web Console中檢查套件組合編號，並直接從檔案系統移除快取資料夾(`crx-quickstart/launchpad/felix/bundle<ID>`)。 |  |

## 下一版本的預先公告 {#pre-announcement-for-next-release}

本節用於預先宣佈未來版本中的即將變更。 已宣佈的變更尚未生效，但將影響客戶。 例如，功能尚未棄用，但會在棄用後影響使用者。 提供這些更新是為了規劃目的。

| 區域 | 功能 | 宣告 |
|--- |--- |--- |
| Foundation | UI框架 | Adobe計畫在2019年淘汰Coral UI 2元件。 AEM 6.2引入了Coral UI 3，而AEM 6.5完全以Coral 3為基礎。 Adobe建議已使用Coral 2建立自訂UI的客戶和合作夥伴，將其重構為Coral 3。 Adobe提供將Coral 2對話方塊轉換為Coral 3的工具 —  [瞭解詳情](/help/sites-developing/modernization-tools.md). |
