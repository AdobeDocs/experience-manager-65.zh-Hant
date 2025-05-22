---
title: Adobe Experience Manager 6.5版中已過時和已移除的功能。
description: 特定於Adobe Experience Manager 6.5中已過時和已移除功能的發行說明。
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: bd29ae46ead836e16362ad3a9a63bb31548415ff
workflow-type: tm+mt
source-wordcount: '1765'
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
| Sites | [SPA 編輯器](/help/sites-developing/spa-editor-deprecation.md) | 針對Headless使用案例，請善用[通用編輯器](/help/sites-developing/universal-editor/introduction.md)進行視覺化編輯，或善用[內容片段編輯器](/help/sites-developing/universal-editor/introduction.md)進行表單式編輯。 | 6.5.23 |
| Sites | **Adobe AEM受管理的輪詢設定**&#x200B;服務： `com.day.cq.polling.importer.impl.ManagedPollConfigImpl` | **Adobe AEM Analytics報表Sling匯入工具**&#x200B;服務。 請參閱連線到Adobe Analytics和建立架構 — [設定匯入間隔](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval) | 6.5.19.0 |
| Screens | Adobe Experience Manager (AEM)中的ActiveMQ。 ActiveMQ用於兩個AEM Publish執行個體之間的通訊。 | Adobe建議客戶現在使用負載平衡器。 | 6.5.18.0 |
| **社交媒體狀態**&#x200B;的體驗片段屬性。 |   | 6.5.11.0 |
| [!DNL Sites] | 內容片段範本，用於建立簡單的內容片段。 | 現在[基於模型的結構化內容片段](/help/assets/content-fragments/content-fragments-models.md)。 | 6.5.11.0 |
| Creative Cloud整合 | AEM 6.2已匯入AEM至Creative Cloud資料夾共用。這可讓創意使用者存取AEM中的資產，以便在[!DNL Creative Cloud]應用程式中開啟資產，以及上傳新檔案或儲存變更至AEM。 Creative Cloud應用程式推出的新功能Adobe Asset Link提供了更優異的使用者體驗，以及更強大的存取功能，可直接從Photoshop、InDesign和Illustrator存取AEM的資產。 Adobe不打算進一步增強AEM與Creative Cloud資料夾共用整合的功能。 雖然此功能包含在AEM中，但建議使用替代解決方案。 | 建議客戶改用新的Creative Cloud整合功能，包括Adobe Asset Link或AEM案頭應用程式。 |  |
| Assets | 發佈執行個體預設會停用`AssetDownloadServlet`。 如需詳細資訊，請參閱[AEM安全性檢查清單](/help/sites-administering/security-checklist.md)。 | 在[AEM安全性檢查清單](/help/sites-administering/security-checklist.md)中說明的設定。 |  |
| 整合 | 畫面&#x200B;**[!UICONTROL Experience Manager Cloud Services選擇加入]**&#x200B;已過時，因為[!DNL Experience Manager]和[!DNL Adobe Target]整合已在[!DNL Experience Manager] 6.5中更新。整合支援Adobe Target Standard API。 API透過Adobe IMS和[!DNL Adobe I/O Runtime]使用驗證。 它支援Adobe Launch成長中的角色，以檢測[!DNL Experience Manager]頁面的分析和個人化，而選擇加入精靈在功能上無關。 | 透過各自的[!DNL Experience Manager]雲端服務設定系統連線、Adobe IMS驗證和[!DNL Adobe I/O Runtime]整合。 | 6.5.7.0 |
| 連接器 | 適用於Microsoft®SharePoint 2010和Microsoft® SharePoint 2013的Adobe JCR聯結器已針對[!DNL Experience Manager] 6.5淘汰。 | 不適用 |  |
| 動態標籤管理員(DTM) | 不建議使用DTM整合。 | 切換以使用Adobe Experience Platform Launch作為標籤管理員。 |   |
| Adobe Target | 在AEM 6.5中新增使用[!DNL Adobe I/O]型Adobe Target Standard API (Rest API)連線Adobe Target服務的功能後，AEM Classic API (XML)方式已過時。 | 重新設定整合以[使用新的API](/help/sites-administering/target.md)。 |  |
| Adobe Target | 不建議在AEM中使用`mbox.js`型與Adobe Target的整合。 | 切換為使用`at.js` 1.x。 |  |
| Commerce | [CIF REST](https://github.com/adobe/commerce-cif-api)在2018年以一組微服務的形式提供，以啟用AEM與商務引擎之間的整合。 在Adobe於2018年年中收購Adobe Commerce (前身為Magento)後，Adobe決定變更其作法，原因有二。 Commerce有自己的Commerce API集(REST和GraphQL)，維護兩組API是不好的做法。 市場趨勢顯示客戶正轉向GraphQL，因為這是查詢資料的更有效率。 2019年，Adobe已使用Commerce的GraphQL API作為真實來源發行了新的Commerce integration framework。 Adobe不打算進一步投資CIF REST。 建議客戶使用替代解決方案。 | 若為AEM-Commerce整合，請切換至[AEM CIF Archetype](https://github.com/adobe/aem-cif-project-archetype)和[AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components)。 請參閱AEM與Adobe Commerce整合[使用Commerce integration framework](/help/commerce/cif/integrating/magento.md)。 Adobe的藍圖支援新方法的協力廠商(Commerce除外)整合。 |  |
| 元件(AEM Sites) | Adobe不打算進一步增強儲存在`/libs/foundation/components`中的大部分Foundation元件。 在元件資料夾中尋找`cq:deprecated`和`cq:deprecatedReason`屬性。 AEM 6.5包含基礎元件，而從舊版升級的客戶可繼續依原樣使用。 此外，即使已棄用，亦支援基礎元件。 | Adobe建議將核心元件用於未來的專案。 現有網站可以維持原狀，或使用[AEM Modernize Tools Suite](https://github.com/adobe/aem-modernize-tools)來重構網站以使用核心元件。 |  |
| 元件(AEM Sites) | 從6.5版開始，Design Importer元件`/libs/wcm/designimporter/components`已標示為已棄用。Adobe不打算進一步增強「設計匯入工具」的實作。 | Adobe計畫於未來版本中提供使用案例的替代實作。 |  |
| Foundation | Granite解除安裝架構。 Adobe不打算進一步增強CQ 5.6.1中匯入的解除安裝架構，將資產處理外部化。 | Adobe正在開發新一代的雲端原生解除安裝架構。 |  |
| 開發人員 | `Hobbes.js`。Adobe不打算進一步增強`hobbes.js`使用者介面測試架構。 | Adobe建議客戶使用Selenium自動化。 |  |
| 開發人員 | jQuery UI使用者端資源庫。 Adobe不打算進一步維護和更新隨分送（快速入門）提供的jQuery UI使用者端程式庫。 | Adobe建議仍需使用jQuery UI來輸入程式碼的客戶，將其新增至專案程式碼基底。 |  |
| 開發人員 | jQuery動畫使用者端程式庫(`granite.jquery.animation`)。 Adobe不打算進一步維護和更新隨配送（快速入門）提供的jQuery Animation使用者端程式庫。 | Adobe建議仍需使用jQuery動畫來製作程式碼的客戶，將其新增至專案程式碼基底。 |  |
| 開發人員 | Handlebars使用者端程式庫。 Adobe不打算進一步維護和更新隨分送（快速入門）提供的Handlebar使用者端程式庫。 | Adobe建議仍然需要`Handlebars`程式碼的客戶，將其新增至專案程式碼基底。 |  |
| 開發人員 | 草坪椅使用者端資源庫。 Adobe不打算進一步維護和更新隨分送（快速入門）提供的Lawnchair使用者端程式庫。 | Adobe建議仍需使用Lawnchair程式碼的客戶，將其新增至專案程式碼基底。 |  |
| 開發人員 | `Granite.Sling.js`使用者端資料庫。 Adobe不打算進一步增強隨分送（快速入門）提供的Granite.Sling.js使用者端資料庫。 | Adobe建議依賴程式庫功能的客戶將其程式碼重構為不再使用。 |  |
| 開發人員 | 使用YUI壓縮/縮制JavaScript使用者端程式庫。 Adobe不打算進一步更新YUI資料庫。 直到AEM 6.4之前，YUI預設會透過切換至Google Closure Compiler (GCC)的選項來縮制JavaScript。 從AEM 6.5開始，預設為GCC。 | Adobe建議客戶升級至AEM 6.5，以切換至GCC進行實作 |  |
| 開發人員 | CRXDE Lite中的傳統UI對話方塊編輯器。 Adobe不打算進一步增強傳統UI對話方塊編輯器(隨附於分送（快速入門）) | 沒有可用的替代專案。 |  |
| Forms | AEM Forms與AEM Mobile的整合已過時。 | 沒有可用的替代專案。 |
| 開發人員 | CRXDE Lite中的傳統UI對話方塊編輯器。 Adobe不打算進一步增強傳統UI對話方塊編輯器(隨附於分送（快速入門）) | 沒有可用的替代專案。 |  |
| 開發人員 | Lodash/underscore使用者端資源庫。 Adobe不打算進一步維護和更新隨分送（快速入門）提供的Lodash/underscore使用者端程式庫。 | Adobe建議仍需將程式碼加到底線的客戶，將其新增至專案程式碼基底。 |  |

## 已移除的功能 {#removed-features}

本節列出已從AEM 6.5移除的功能。舊版將這些功能標籤為已過時。

| 區域 | 功能 | 替代方案 | 版本(SP) |
|--- |--- |--- |--- |
| Commerce | AEM CIF Classic已移除。 | 您應該移轉至[AEM CIF](/help/commerce/cif/migration.md)。 如果您仍然需要CIF Classic，已建立相容性套件，請[聯絡Adobe客戶支援](https://experienceleague.adobe.com/?support-solution=General#support)。 | 6.5.22.0 |
| 與[!DNL Experience Cloud]整合 | 您可以透過[!DNL Adobe I/O]使用設定，將您的資產與[!DNL Experience Cloud]同步化。 [!DNL Adobe Experience Cloud]先前稱為[!DNL Adobe Experience Cloud]。 | 若您有任何疑問，請[聯絡Adobe客戶支援](https://experienceleague.adobe.com/?support-solution=General#support)。 |  |
| Analytics Activity Map | AEM中包含的Activity Map版本。 | 由於 Adobe Analytics API 中的安全性變更，AEM 中包含的 Activity Map 版本已無法再使用。使用Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html)提供的[ActivityMap外掛程式。 |  |
| 整合 | ExactTarget整合已從預設分送（快速入門）中移除，且不再提供。 | 沒有替代專案。 |  |
| 整合 | Salesforce Force API整合已從預設發佈(Quickstart)中移除，現在是一個要從[軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)安裝的額外套件。 | 此功能仍可使用。 |
| Forms | 已移除對Adobe中央移轉Bridge服務的支援，因為已不再支援Adobe中央產品。 | 沒有替代專案。 |  |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 沒有替代專案。 |  |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 無替代專案 |  |
| Forms | 無法在JEE上從LiveCycle ES4 SP1升級至AEM 6.5 Forms的單跳升級功能 | 請參閱AEM Forms升級檔案中的[可用升級路徑](../forms/using/upgrade.md)。 |  |
| Forms | 移除JEE版AEM Forms中的UPD型叢集支援 | 在JEE上的AEM Forms中，您只能使用TCP型叢集。 如果您將UDP多點傳送伺服器從舊版升級至JEE上的AEM 5.5 Forms，請執行手動設定，以切換至以TCP為基礎的Gemfire叢集。 如需詳細指示，請參閱[在JEE上升級至AEM 6.5表單](../forms/using/upgrade-forms-jee.md) |  |
| 開發人員 | Firebug Lite已從預設散發中移除（快速入門） | 使用瀏覽器內建的開發人員主控台 |
| 開發人員 | 移除HTML Client Library Manager中的`customJavaScriptPath`支援。 | 無替代專案 |  |
| [!DNL Assets] | 資產解除安裝功能已在[!DNL Adobe Experience Manager] 6.5中移除。 | 沒有可用的替代專案。 |  |
| 快取 | `system/console/slingjsp`已移除，不再於AEM 6.5中使用。 | 類別和Slightly快取儲存在Apache Sling Commons FileSystem ClassLoader套件組合下。 您可以在AEM網頁主控台中檢查套件組合編號，並直接從檔案系統(`crx-quickstart/launchpad/felix/bundle<ID>`)移除快取資料夾。 |  |
| Screens | 移除activemq套件組合支援及其相關設定。 |  |  |

<!-- ## Pre-announcement for next release {#pre-announcement-for-next-release}

This section is used to pre-announce the upcoming changes in the future releases. The announced changes are not yet effective but will impact customers. For example, the features are not yet deprecated but impacts the users after deprecation. These updates are provided for planning purpose.

|Area|Feature|Announcement|
|--- |--- |--- |
|Foundation|UI Framework|Adobe is planning to deprecate the Coral UI 2 components in 2019. Coral UI 3 was introduced with AEM 6.2, and AEM 6.5 is fully based on Coral 3. Adobe recommends customers and partners that have build custom UIs with Coral 2 to refactored them to Coral 3. Adobe is providing a tool to convert Coral 2 dialogs to Coral 3 - [Read more](/help/sites-developing/modernization-tools.md).|
-->
