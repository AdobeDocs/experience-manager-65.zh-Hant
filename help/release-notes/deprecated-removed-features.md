---
title: Adobe Experience Manager 6.5版中已棄用和已移除的功能。
description: Adobe Experience Manager 6.5中已棄用和已移除功能的發行說明。
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '1675'
ht-degree: 13%

---

# 過時和移除的功能 {#deprecated-and-removed-features}

Adobe 持續評估產品功能，以更新或替代的方式來改善或取代舊功能，以提升客戶享有的整體價值，且隨時謹慎考慮是否回溯相容。

為傳達AEM功能即將移除或遭取代的訊息，請套用下列規則：

1. 首先需公告功能已過時。雖然已過時，功能仍可供使用，但未進一步增強。
1. 下列主要版本最早會移除已棄用的功能。 將公佈實際的移除日期。

此程序可讓客戶在功能真正移除之前，至少還有一個發行週期，讓實作適應過時功能的新版本或後續版本。

## 過時的功能 {#deprecated-features}

本節列出AEM 6.5中已標示為過時的功能。通常，未來版本中預計移除的功能會先設為過時，並提供其他選項。

建議客戶檢閱是否在目前的部署中使用這些功能，並規劃變更實作，改用所提供的替代方案。

| 區域 | 功能 | 替代方案 | 版本 (SP) |
|---|---|---|---|
| [!DNL Sites] | **社交媒體狀態**&#x200B;的體驗片段屬性。 |  | 6.5.11.0 |
| [!DNL Sites] | 內容片段範本，用於建立簡單內容片段。 | 現在[基於模型的結構化內容片段](/help/assets/content-fragments/content-fragments-models.md)。 | 6.5.11.0 |
| Creative Cloud整合 | AEM到Creative Cloud資料夾共用於AEM 6.2中推出，作為讓創意使用者存取AEM資產的方式，以便在中開啟資產 [!DNL Creative Cloud] 應用程式和上傳新檔案，或將變更儲存至AEM。 Creative Cloud 應用程式推出的新功能 Adobe Asset Link 提供了更優異的使用者體驗，以及更強大的存取功能，可直接從 Photoshop、InDesign 和 Illustrator 中存取 AEM 的資產。Adobe不打算進一步增強AEM以Creative Cloud資料夾共用整合。 雖然AEM中包含此功能，但建議客戶使用取代解決方案。 | 建議客戶改用新的Creative Cloud整合功能，包括Adobe資產連結或AEM案頭應用程式。 |  |
| 資產 | `AssetDownloadServlet` 依預設，發佈例項會停用。 如需詳細資訊，請參閱 [AEM安全性檢查清單](/help/sites-administering/security-checklist.md). | 配置描述於 [AEM安全性檢查清單](/help/sites-administering/security-checklist.md). |  |
<!-- Search&Promote is end-of-life September 1, 2022 | Assets | If a user does not have sufficient (read and write) permissions on `/content/dam/collections`, the user cannot create a Collection. | Honor the access control setup of user and ensure appropriate permissions. ||
|Adobe Search & Promote|The integration with Adobe Search & Promote is deprecated. Adobe does not plan to make further enhancements to the Search & Promote integration. Adobe Search & Promote integration remains fully supported while being deprecated.||| -->
| DTM標籤管理 |已棄用與DTM（動態標籤管理器）的整合。 |切換為使用Adobe Experience Platform Launch作為標籤管理程式。 || |Adobe Target|新增AEM能力，透過 [!DNL Adobe I/O] AEM 6.5中以Adobe Target Standard API(Rest API)為基礎，已棄用Target Classic API(XML)方式。|將整合重新設定為 [使用新API](/help/sites-administering/target.md). || |Adobe Target|使用 `mbox.js` 不建議使用AEM中與Adobe Target的整合。|切換為使用 `at.js` 1.x.|| |商務 | [CIF休息](https://github.com/adobe/commerce-cif-api) 是於2018年以一組微服務形式提供，以啟用AEM與商務引擎之間的整合。 在Adobe於2018年年中獲得Magento後，Adobe決定改變其做法，原因有二。 Magento有其專屬的Commerce API(REST和GraphQL)，維護兩組API並非理想作法。 市場趨勢顯示客戶正轉向GraphQL，因為這是更有效的資料查詢方式。 2019年，Adobe發行了新的商務整合架構，使用Magento的GraphQL API作為真相的來源。 Adobe沒有計畫在CIF REST上再投資。 建議客戶使用更換解決方案。|針對AEM-Magento整合，請切換至 [AEM CIF原型](https://github.com/adobe/aem-cif-project-archetype) 和 [AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components). 請參閱AEM與Adobe Commerce整合 [使用Commerce Integration Framework](/help/commerce/cif/integrating/magento.md). 我們的藍圖中已列出支援與新方法整合的第三方(Magento除外)。|| |元件(AEM Sites) |Adobe不打算對儲存在 `/libs/foundation/components`. 尋找 `cq:deprecated` 和 `cq:deprecatedReason` 屬性。 AEM 6.5已包含Foundation元件，從舊版升級的客戶可繼續依原樣使用。 此外，即使已棄用，仍支援基礎元件。 |Adobe建議在未來專案中使用核心元件。 現有網站可維持原狀或使用 [AEM現代化工具套裝](https://github.com/adobe/aem-modernize-tools) 以重構網站以使用核心元件。 || |元件(AEM Sites)|設計匯入工具元件 `/libs/wcm/designimporter/components` 6.5版起已標示為已淘汰。Adobe不打算對設計匯入工具的實作進行進一步的增強。 |Adobe計畫在未來版本中提供使用案例的替代實作。 || |Foundation|Granite卸載框架。 Adobe不打算對CQ 5.6.1中推出的卸載架構進行進一步增強，將資產處理外部化。|Adobe正在開發新一代雲端原生卸載架構。||
|開發人員|`Hobbes.js`. Adobe不打算對 `hobbes.js` 用戶介面測試框架。|Adobe建議客戶使用Selenium自動化。|| |開發人員|jQuery UI客戶端庫。 Adobe不打算進一步維護和更新隨分發(Quickstart)|Adobe一起提供的jQuery UI客戶端庫，建議仍需jQuery UI的客戶將其代碼添加到其項目代碼庫中。|| |開發人員|jQuery動畫客戶端庫(`granite.jquery.animation`)。 Adobe不計畫進一步維護和更新作為分發(Quickstart)|Adobe的一部分發運的jQuery動畫客戶端庫，該庫建議仍需要jQuery動畫的客戶將其代碼添加到其項目代碼庫中。|| |開發人員|Handlebars客戶端庫。 Adobe不計畫進一步維護和更新隨分發(Quickstart)一起提供的Handlebar客戶端庫|Adobe建議仍需要Handlebars才能將其代碼添加到其項目代碼庫中的客戶。|| |開發人員|Lawnchair客戶端庫。 Adobe不計畫進一步維護和更新作為分發(Quickstart)一部分發運的Lawnchair客戶端庫|Adobe建議仍需Lawnchair才能將其代碼添加到其項目代碼庫中的客戶。|| |開發人員|`Granite.Sling.js` 用戶端程式庫。 Adobe不打算進一步增強隨發佈(Quickstart)|Adobe提供的Granite.Sling.js用戶端程式庫，建議依賴程式庫功能的客戶重新調整其程式碼，以免使用它。|| |開發人員|使用YUI來壓縮/縮小JavaScript用戶端程式庫。 Adobe不打算進一步更新YUI程式庫。 在AEM 6.4之前，YUI預設為縮小JavaScript，並提供切換至Google關閉編譯器(GCC)的選項。 從AEM 6.5開始，預設為GCC。|Adobe建議升級至AEM 6.5的客戶切換至GCC以進行實作|| |開發人員|傳統UI對話框編輯器處於CRXDE Lite。 Adobe不打算進一步增強發佈(Quickstart)時隨附的傳統UI對話框編輯器|不提供替換。 || 已棄用|Forms|AEM Forms與AEM Mobile的整合。 |無可替換。 ||開發人員|傳統UI對話方塊編輯器處於CRXDE Lite。 Adobe不打算進一步增強發佈(Quickstart)時隨附的傳統UI對話框編輯器|不提供替換。 || |開發人員|Lodash/underscore客戶端庫。 Adobe不計畫進一步維護和更新作為分發（快速入門）的Lodash/underscore客戶端庫 |Adobe建議仍需使用Lodash/底線的客戶，將其程式碼新增至其專案程式碼基底。 ||

## 移除的功能 {#removed-features}

本節列出已從AEM 6.5中移除的功能。舊版有這些功能標示為已過時。

| 區域 | 功能 | 替代方案 | 版本 (SP) |
|--- |--- |--- |--- |
|  與 [!DNL Experience Cloud] 整合 | 您可以將資產同步至 [!DNL Experience Cloud] 透過 [!DNL Adobe I/O]. [!DNL Adobe Experience Cloud] 先前稱為 [!DNL Adobe Experience Cloud]. | 如果你有任何疑問， [聯絡Adobe客戶支援](https://experienceleague.adobe.com/?support-solution=General#support). |  |
| AnalyticsActivity Map | AEM中包含的Activity Map版本。 | 由於 Adobe Analytics API 中的安全性變更，AEM 中包含的 Activity Map 版本已無法再使用。使用 [ActivityMap外掛程式由Adobe Analytics提供](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=zh-Hant). |  |
| 整合 | ExactTarget整合已從預設分發(Quickstart)中移除，現在已無法使用。 | 沒有替換。 |  |
| 整合 | Salesforce Force API整合已從預設分發(Quickstart)中刪除，現在是要從 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). | 功能仍可用。 |
| Forms | 由於不再支援Adobe中心產品，因此Adobe中心移轉橋服務的支援已遭移除。 | 沒有替換。 |  |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 沒有替換。 |  |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 無替換 |  |
| Forms | 無法在JEE上從LiveCycleES4 SP1升級至AEM 6.5 Forms的單跳升級 | 請參閱 [可用升級路徑](../forms/using/upgrade.md) 在AEM Forms升級檔案中。 |  |
| Forms | 移除JEE上AEM Forms的UPD型叢集支援 | 在JEE上的AEM Forms中，您只能使用基於TCP的群集。 如果您將UDP多播伺服器從舊版升級為JEE上的AEM 5.5 Forms ，請執行手動配置以切換到基於TCP的gemfire群集。 如需詳細指示，請參閱 [升級至JEE版AEM 6.5表單](../forms/using/upgrade-forms-jee.md) |  |
| 開發人員 | Firebug Lite已從預設分發(Quickstart)中移除 | 使用瀏覽器內建的開發人員主控台 |
| 開發人員 | 移除 `customJavaScriptPath` 支援HTML用戶端程式庫管理員。 | 無替換 |  |
| [!DNL Assets] | 資產卸載功能會移除於 [!DNL Adobe Experience Manager] 6.5。 | 無可替換。 |  |
| 快取 | `system/console/slingjsp` AEM 6.5中已不再提供移除功能。 | 類別和微快取儲存在Apache Sling Commons FileSystem ClassLoader套件組合下。 您可以在AEM Web Console中檢查套件組合編號，並直接從檔案系統移除快取資料夾(`crx-quickstart/launchpad/felix/bundle<ID>`)。 |  |

## 下一版的預發佈 {#pre-announcement-for-next-release}

本節用於預先宣佈未來版本即將進行的變更。 已宣佈的變更尚未生效，但將影響客戶。 例如，功能尚未淘汰，但會在淘汰後影響使用者。 這些更新是為規劃目的而提供的。

| 區域 | 功能 | 公告 |
|--- |--- |--- |
| Foundation | UI架構 | Adobe預計於2019年淘汰Coral UI 2元件。 AEM 6.2導入了Coral UI 3，而AEM 6.5則完全以Coral 3為基礎。 Adobe建議已使用Coral 2建立自訂UI的客戶和合作夥伴，將其重構至Coral 3。 Adobe提供工具，將Coral 2對話方塊轉換為Coral 3 - [了解詳情](/help/sites-developing/modernization-tools.md). |
