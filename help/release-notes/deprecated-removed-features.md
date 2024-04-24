---
title: Adobe Experience Manager 6.5版中已過時和已移除的功能。
description: 特定於Adobe Experience Manager 6.5中已過時和已移除功能的發行說明。
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 10%

---

# 過時和移除的功能 {#deprecated-and-removed-features}

<!-- Search&Promote is end-of-life September 1, 2022 | Assets | If a user does not have sufficient (read and write) permissions on `/content/dam/collections`, the user cannot create a Collection. | Honor the access control setup of user and ensure appropriate permissions. ||
|Adobe Search & Promote|The integration with Adobe Search & Promote is deprecated. Adobe does not plan to make further enhancements to the Search & Promote integration. Adobe Search & Promote integration remains fully supported while being deprecated.||| -->

Adobe 持續評估產品功能，以更新或替代的方式來改善或取代舊功能，以提升客戶享有的整體價值，且隨時謹慎考慮是否回溯相容。

若要傳達Adobe Experience Manager (AEM)功能即將移除或取代的訊息，請套用下列規則：

1. 首先需公告功能已過時。雖然已棄用，功能仍可使用，但不會進一步增強。
1. 後續最新主要發行版本，則將最先移除已棄用的功能。 實際的目標移除日期將於稍後宣佈。

此程序可讓客戶在功能真正移除之前，至少還有一個發行週期，讓實作適應過時功能的新版本或後續版本。

## 已棄用的功能 {#deprecated-features}

本節提供AEM 6.5中標示為過時的功能。通常，未來新發行版本預計移除的功能，將先設為過時並提供其他選項。

建議客戶檢閱是否在目前的部署中使用這些功能，並規劃變更實作，改用所提供的替代方案。

| 區域 | 功能 | 替代方案 | 版本(SP) |
|---|---|---|---|
|   |   |   |   |
| Sites | 此 **AdobeAEM受管理的輪詢設定** 服務： `com.day.cq.polling.importer.impl.ManagedPollConfigImpl` | 此 **AdobeAEM Analytics報表Sling匯入工具** 服務。 請參閱連線Adobe Analytics與建立框架 —  [設定匯入間隔](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval) | 6.5.19.0 |
| Screens | Adobe Experience Manager (AEM)中的ActiveMQ。 ActiveMQ用於兩個AEM Publish執行個體之間的通訊。 | Adobe建議客戶現在使用負載平衡器。 | 6.5.18.0 |
| **社交媒體狀態**&#x200B;的體驗片段屬性。 |   | 6.5.11.0 |
| [!DNL Sites] | 內容片段範本，用於建立簡單的內容片段。 | 現在[基於模型的結構化內容片段](/help/assets/content-fragments/content-fragments-models.md)。 | 6.5.11.0 |
| Creative Cloud整合 | AEM 6.2引入了AEM至Creative Cloud資料夾共用功能。它提供一種方法，讓創意使用者可以存取AEM中的資產，以便在中開啟它們 [!DNL Creative Cloud] 應用程式並上傳新檔案或儲存變更至AEM。 Creative Cloud應用程式推出的新功能Adobe Asset Link提供更優異的使用者體驗，以及更強大的存取功能，可直接從Photoshop、InDesign和Illustrator內從AEM存取資產。 Adobe不打算進一步增強AEM的「Creative Cloud資料夾共用」整合。 雖然此功能包含在AEM中，但建議使用替代解決方案。 | 建議客戶改用新的Creative Cloud整合功能，包括Adobe資產連結或AEM案頭應用程式。 |  |
| Assets | `AssetDownloadServlet` 發佈執行個體預設為停用。 如需詳細資訊，請參閱 [AEM安全性檢查清單](/help/sites-administering/security-checklist.md). | 設定說明於 [AEM安全性檢查清單](/help/sites-administering/security-checklist.md). |  |
| 整合 | 畫面 **[!UICONTROL Experience Manager Cloud Service選擇加入]** 已過時，因為 [!DNL Experience Manager] 和 [!DNL Adobe Target] 整合已更新於 [!DNL Experience Manager] 6.5.整合支援Adobe Target Standard API。 API透過Adobe IMS和以下方式使用驗證 [!DNL Adobe I/O Runtime]. 它可支援AdobeLaunch在樂器方面日益增加的作用 [!DNL Experience Manager] 頁面對於analytics和個人化，選擇加入精靈在功能上無關。 | 設定系統連線、Adobe IMS驗證和 [!DNL Adobe I/O Runtime] 透過個別 [!DNL Experience Manager] 雲端服務。 | 6.5.7.0 |
| 聯結器 | Microsoft®SharePoint 2010和Microsoft® SharePoint 2013的JCR ConnectorAdobe已遭取代 [!DNL Experience Manager] 6.5. | 不適用 |  |
| 動態標籤管理員(DTM) | 不建議使用DTM整合。 | 切換以使用Adobe Experience Platform Launch作為標籤管理員。 |   |
| Adobe Target | 新增AEM連線Adobe Target服務的功能，使用 [!DNL Adobe I/O] 以AEM 6.5中的Adobe Target Standard API (Rest API)為基礎，Target Classic API (XML)方式已過時。 | 將整合重新設定至 [使用新API](/help/sites-administering/target.md). |  |
| Adobe Target | 使用 `mbox.js` 不建議使用AEM中與Adobe Target的整合方式。 | 切換以使用 `at.js` 1.x. |  |
| 商務 | [CIF REST](https://github.com/adobe/commerce-cif-api) 在2018年提供的一組微服務，用於啟用AEM與商務引擎之間的整合。 在Adobe於2018年年中收購Adobe Commerce (前身為Magento)後，Adobe決定變更其作法，原因有二。 Commerce有自己的Commerce API集(REST和GraphQL)，維護兩組API是不好的做法。 市場趨勢顯示客戶正轉向GraphQL，因為這是查詢資料的更有效率。 2019年，Adobe已使用Commerce的GraphQL API作為真相來源發佈新Commerce integration framework。 Adobe不打算進一步投資CIF REST。 建議客戶使用替代解決方案。 | 若為AEM-Commerce整合，請切換至 [AEM CIF原型](https://github.com/adobe/aem-cif-project-archetype) 和 [AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components). 請參閱AEM與Adobe Commerce整合 [使用Commerce integration framework](/help/commerce/cif/integrating/magento.md). Adobe的藍圖支援第三方(Commerce除外)與新方法整合。 |  |
| 元件(AEM Sites) | Adobe不打算進一步增強中儲存的大部分基礎元件 `/libs/foundation/components`. 尋找 `cq:deprecated` 和 `cq:deprecatedReason` 屬性。 AEM 6.5包含基礎元件，而從舊版升級的客戶可繼續依原樣使用。 此外，即使已棄用，亦支援基礎元件。 | Adobe建議將核心元件用於未來的專案。 現有網站可維持原狀，或使用 [AEM Modernize Tools Suite](https://github.com/adobe/aem-modernize-tools) 以使用核心元件來重構網站。 |  |
| 元件(AEM Sites) | Design Importer元件 `/libs/wcm/designimporter/components` 從6.5開始標籤為已過時。Adobe不打算進一步增強「設計匯入工具」的實作。 | Adobe計畫在未來版本中提供使用案例的替代實施。 |  |
| Foundation | Granite解除安裝架構。 Adobe不打算進一步增強CQ 5.6.1中匯入的解除安裝架構，以將資產處理外部化。 | Adobe正在開發新一代的雲端原生解除安裝架構。 |  |
| 開發人員 | `Hobbes.js`。Adobe不打算進一步增強 `hobbes.js` 使用者介面測試架構。 | Adobe建議客戶使用Selenium自動化。 |  |
| 開發人員 | jQuery UI使用者端資源庫。 Adobe不打算進一步維護和更新隨分送（快速入門）提供的jQuery UI使用者端程式庫。 | Adobe建議仍需使用jQuery UI來取得程式碼的客戶，將其新增至專案程式碼基底。 |  |
| 開發人員 | jQuery Animation使用者端程式庫(`granite.jquery.animation`)。 Adobe不打算進一步維護及更新隨配送（快速入門）提供的jQuery Animation使用者端程式庫。 | Adobe建議仍然需要jQuery動畫才能讓程式碼加入專案程式碼基底的客戶。 |  |
| 開發人員 | Handlebars使用者端程式庫。 Adobe不打算進一步維護和更新隨分送（快速入門）提供的Handlebar使用者端程式庫。 | Adobe建議客戶仍然需要 `Handlebars` 將程式碼新增至專案程式碼庫中。 |  |
| 開發人員 | 草坪椅使用者端資源庫。 Adobe不打算進一步維護及更新隨分送（快速入門）提供的Lawnchair使用者端程式庫。 | Adobe建議仍在要求程式碼使用Lawnchair的客戶將其新增至專案程式碼基底。 |  |
| 開發人員 | `Granite.Sling.js` 使用者端資源庫。 Adobe不打算進一步增強做為發佈(Quickstart)一部分所提供的Granite.Sling.js使用者端資料庫。 | Adobe建議依賴程式庫功能的客戶將其程式碼重構為不再使用。 |  |
| 開發人員 | 使用YUI壓縮/縮制JavaScript使用者端程式庫。 Adobe不打算進一步更新YUI資料庫。 直到AEM 6.4之前，YUI預設會使用切換至Google Closure Compiler (GCC)的選項來縮制JavaScript。 從AEM 6.5開始，預設為GCC。 | Adobe建議客戶升級至AEM 6.5，以切換至GCC進行實作 |  |
| 開發人員 | CRXDE Lite中的傳統UI對話方塊編輯器。 Adobe不打算進一步增強傳統UI對話方塊編輯器(隨附於分送（快速入門）) | 沒有可用的替代專案。 |  |
| 表單 | AEM Forms與AEM Mobile的整合已過時。 | 沒有可用的替代專案。 |
| 開發人員 | CRXDE Lite中的傳統UI對話方塊編輯器。 Adobe不打算進一步增強傳統UI對話方塊編輯器(隨附於分送（快速入門）) | 沒有可用的替代專案。 |  |
| 開發人員 | Lodash/underscore使用者端資源庫。 Adobe不打算進一步維護和更新隨分送（快速入門）提供的Lodash/underscore使用者端程式庫。 | Adobe建議仍需將程式碼加到底線的客戶，將其新增至專案程式碼基底。 |  |

## 已移除的功能 {#removed-features}

本節列出已從AEM 6.5移除的功能。舊版將這些功能標籤為已過時。

| 區域 | 功能 | 替代方案 | 版本(SP) |
|--- |--- |--- |--- |
| 與整合 [!DNL Experience Cloud] | 您可以將資產與同步 [!DNL Experience Cloud] 使用設定管道 [!DNL Adobe I/O]. [!DNL Adobe Experience Cloud] 之前稱為 [!DNL Adobe Experience Cloud]. | 如果您有任何查詢， [聯絡Adobe客戶支援](https://experienceleague.adobe.com/?support-solution=General#support). |  |
| AnalyticsActivity Map | AEM中包含的Activity Map版本。 | 由於 Adobe Analytics API 中的安全性變更，AEM 中包含的 Activity Map 版本已無法再使用。使用 [Adobe Analytics提供的ActivityMap外掛程式](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html). |  |
| 整合 | ExactTarget整合已從預設分送（快速入門）中移除，且不再提供。 | 沒有替代專案。 |  |
| 整合 | Salesforce API整合已從預設的分發（快速入門）中移除，現在是可供安裝的額外套件 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). | 此功能仍可使用。 |
| 表單 | 已移除對Adobe Central Migration Bridge服務的支援，因為已不再支援Adobe Central產品。 | 沒有替代專案。 |  |
| 表單 | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 沒有替代專案。 |  |
| 表單 | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 無替代專案 |  |
| 表單 | JEE版不提供從LiveCycleES4 SP1到AEM 6.5 Forms的單點躍點升級 | 另請參閱 [可用的升級路徑](../forms/using/upgrade.md) 在AEM Forms升級檔案中。 |  |
| 表單 | 移除JEE版AEM Forms中的UPD型叢集支援 | 在JEE上的AEM Forms中，您只能使用TCP型叢集。 如果您將UDP多點傳送伺服器從舊版升級至JEE上的AEM 5.5 Forms，請執行手動設定，以切換至以TCP為基礎的Gemfire叢集。 如需詳細指示，請參閱 [在JEE上升級至AEM 6.5表單](../forms/using/upgrade-forms-jee.md) |  |
| 開發人員 | Firebug Lite已從預設散發中移除（快速入門） | 使用瀏覽器內建的開發人員主控台 |
| 開發人員 | 移除 `customJavaScriptPath` 支援HTML Client Library Manager。 | 無替代專案 |  |
| [!DNL Assets] | 資產解除安裝功能在中移除 [!DNL Adobe Experience Manager] 6.5. | 沒有可用的替代專案。 |  |
| 快取 | `system/console/slingjsp` 「 」已移除，不再於AEM 6.5中使用。 | 類別和Slightly快取儲存在Apache Sling Commons FileSystem ClassLoader套件組合下。 您可以在AEM網頁主控台中檢查該套件組合編號，並直接從檔案系統移除快取資料夾(`crx-quickstart/launchpad/felix/bundle<ID>`)。 |  |
| Screens | 移除activemq套件組合支援及其相關設定。 |  |  |

<!-- ## Pre-announcement for next release {#pre-announcement-for-next-release}

This section is used to pre-announce the upcoming changes in the future releases. The announced changes are not yet effective but will impact customers. For example, the features are not yet deprecated but impacts the users after deprecation. These updates are provided for planning purpose.

|Area|Feature|Announcement|
|--- |--- |--- |
|Foundation|UI Framework|Adobe is planning to deprecate the Coral UI 2 components in 2019. Coral UI 3 was introduced with AEM 6.2, and AEM 6.5 is fully based on Coral 3. Adobe recommends customers and partners that have build custom UIs with Coral 2 to refactored them to Coral 3. Adobe is providing a tool to convert Coral 2 dialogs to Coral 3 - [Read more](/help/sites-developing/modernization-tools.md).|
-->
