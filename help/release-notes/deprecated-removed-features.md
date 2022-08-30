---
title: Adobe Experience Manager6.5版中的已棄用和已刪除功能。
description: 特定於Adobe Experience Manager6.5中已棄用和已刪除功能的發行說明。
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
source-git-commit: e3caa3e3067cf5e29cfcdf4286047eb346aefa23
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 10%

---

# 過時和移除的功能 {#deprecated-and-removed-features}

Adobe 持續評估產品功能，以更新或替代的方式來改善或取代舊功能，以提升客戶享有的整體價值，且隨時謹慎考慮是否回溯相容。

要傳達即將刪除或替換權AEM能，應用以下規則：

1. 首先需公告功能已過時。雖然已棄用，但功能仍可用，但未進一步增強。
1. 最早在以下主發行版中刪除過時的功能。 將公佈實際刪除目標日期。

此程序可讓客戶在功能真正移除之前，至少還有一個發行週期，讓實作適應過時功能的新版本或後續版本。

## 過時的功能 {#deprecated-features}

本節列出了已標籤為不建議使用的6.5AEM功能。通常，計畫在將來版本中刪除的功能會先設定為不建議使用，並提供替代選項。

建議客戶檢查其當前部署中是否使用了該功能/功能，並制定計畫更改其實施以使用提供的替代方案。

| 區域 | 功能 | 替代方案 | 版本 (SP) |
|---|---|---|---|
| [!DNL Sites] | 體驗片段屬性 **社交媒體狀態**。 |  | 6.5.11.0 |
| [!DNL Sites] | 內容片段模板，用於建立簡單內容片段。 | [基於模型的結構化內容片段](/help/assets/content-fragments/content-fragments-models.md) 現在。 | 6.5.11.0 |
| Creative Cloud整合 | 在6AEM.2中引入了「Creative Cloud資料夾共用」AEM，以便讓創意用戶能夠訪問來自的資AEM產，這樣他們就可以在 [!DNL Creative Cloud] 應用程式和上載新檔案或將更改保存到AEM。 Creative Cloud 應用程式推出的新功能 Adobe Asset Link 提供了更優異的使用者體驗，以及更強大的存取功能，可直接從 Photoshop、InDesign 和 Illustrator 中存取 AEM 的資產。Adobe不打算對Creative Cloud資料夾共用集AEM成進行進一步增強。 儘管該功能已包含在AEM中，但建議客戶使用更換解決方案。 | 建議客戶切換到新的Creative Cloud整合功能，包括Adobe資產連結或AEM案頭應用。 |  |
| Assets | `AssetDownloadServlet` 預設情況下，對於發佈實例禁用。 有關詳細資訊，請參閱 [AEM安全檢查表](/help/sites-administering/security-checklist.md)。 | 配置描述於 [安AEM全核對表](/help/sites-administering/security-checklist.md)。 |  |
| 資產 | 如果用戶沒有足夠的（讀和寫）權限 `/content/dam/collections`，用戶無法建立集合。 | 執行用戶的訪問控制設定並確保相應的權限。 |  |
| Adobe Search&amp;Promote | 已棄用與Adobe Search&amp;Promote的整合。 Adobe不打算對搜索和升級整合進行進一步的增強。 Adobe Search&amp;Promote整合在被棄用時仍完全受支援。 |  |  |
| DTM標籤管理器 | 不建議使用與DTM（動態標籤管理器）的整合。 | 切換為將Adobe Experience Platform Launch用作標籤管理器。 |  |
| Adobe Target | 通過添加連接AEM到Adobe Target服務的功能， [!DNL Adobe I/O] 基於6.5中的Adobe Target標準API(Rest API)AEM，不建議使用目標經典API(XML)方法。 | 將整合重新配置為 [使用新API](/help/sites-administering/target.md)。 |  |
| Adobe Target | 使用 `mbox.js` 已棄用與Adobe Target的AEM基本整合。 | 切換到使用 `at.js` 1.x |  |
| 商務 | [CIF余料](https://github.com/adobe/commerce-cif-api) 於2018年提供為一組微服務，以實現與商業引擎AEM的整合。 Adobe在2018年年中獲得Magento後，Adobe決定改變其做法，原因有二。 Magento有其自己的Commerce API（REST和GraphQL）集，維護兩組API並不是好做法。 市場趨勢表明，客戶正在向GraphQL轉移，因為GraphQL是一種更高效的資料查詢方法。 2019年，Adobe發佈了新的Commerce Integration Framework ，使用Magento的GraphQL API作為真相的來源。 Adobe不計畫進一步投資CIF REST. 建議客戶使用更換解決方案。 | 對於AEMMagento整合，切換到 [CIF原AEM型](https://github.com/adobe/aem-cif-project-archetype) 和 [AEMCIF核心元件](https://github.com/adobe/aem-core-cif-components)。 見AEM和Adobe Commerce [使用Commerce Integration Framework](/help/commerce/cif/integrating/magento.md)。 支援第三方(除Magento外)與新方法的整合已列在我們的路線圖中。 |  |
| 部件(AEM Sites) | Adobe不打算對儲存在 `/libs/foundation/components`。 查找 `cq:deprecated` 和 `cq:deprecatedReason` 屬性。 AEM6.5包含了Foundation Components，從早期版本升級的客戶可以繼續按原樣使用它們。 此外，即使已棄用，也支援Foundation Components。 | Adobe建議將核心元件用於未來項目。 現有站點可以保持原樣或使用 [現代化AEM工具套件](https://github.com/adobe/aem-modernize-tools) 重新構建站點以使用核心元件。 |  |
| 部件(AEM Sites) | 設計導入程式元件 `/libs/wcm/designimporter/components` 從6.5開始已標籤為不建議使用。Adobe沒有計畫對設計進口商的實施做進一步的改進。 | Adobe計畫在今後的版本中提供使用案例的替代實施。 |  |
| Foundation | 花崗岩卸載框架。 Adobe不打算對CQ 5.6.1中為將資產處理外部化而引入的卸載框架進行進一步的增強。 | Adobe正在開發新一代雲本地卸載框架。 |  |
| 開發人員 | `Hobbes.js`。 Adobe不打算對 `hobbes.js` 用戶介面測試框架。 | Adobe建議客戶使用Selenium自動化。 |  |
| 開發人員 | jQuery UI客戶端庫。 Adobe不計畫進一步維護和更新作為分發的一部分發運的jQuery UI客戶端庫（快速啟動） | Adobe建議仍需要jQuery UI的客戶將其代碼添加到項目代碼庫中。 |  |
| 開發人員 | jQuery動畫客戶端庫(`granite.jquery.animation`)。 Adobe不計畫進一步維護和更新作為分發的一部分發運的jQuery動畫客戶端庫（快速啟動） | Adobe建議仍需要jQuery動畫的客戶將其代碼添加到項目代碼庫中。 |  |
| 開發人員 | 車把客戶端庫。 Adobe不打算進一步維護和更新作為分發的一部分而發運的Handlebar客戶端庫（快速啟動） | Adobe建議仍需要Handlebar代碼的客戶將其添加到項目代碼庫。 |  |
| 開發人員 | Lawnchair客戶端庫。 Adobe不計畫進一步維護和更新作為分發的一部分發運的Lawnshair客戶端庫（快速啟動） | Adobe建議仍需要Lawnchaird進行代碼添加到項目代碼庫的客戶。 |  |
| 開發人員 | `Granite.Sling.js` 客戶端庫。 Adobe不打算進一步增強作為分發(Quickstart)一部分發貨的Granite.Sling.js客戶端庫 | Adobe建議依賴庫功能的客戶重新調整其代碼，使其不再使用。 |  |
| 開發人員 | 使用YUI壓縮/縮小JavaScript客戶端庫。 Adobe不計畫進一步更新YUI庫。 在6.4AEM之前，YUI預設為JavaScript最小化，並具有切換到Google關閉編譯器(GCC)的選項。 從AEM6.5開始，GCC為預設值。 | Adobe建議升級到AEM6.5的客戶切換到GCC以實施 |  |
| 開發人員 | CRXDE Lite中的經典UI對話框編輯器。 Adobe不計畫進一步增強作為分發（快速入門）一部分提供的經典用戶介面對話框編輯器 | 沒有可用的更換。 |  |
| Forms | AEM Forms與AEM Mobile的整合已過時。 | 沒有可用的更換。 |  | 開發人員 | CRXDE Lite中的經典UI對話框編輯器。 Adobe不計畫進一步增強作為分發（快速入門）一部分提供的經典用戶介面對話框編輯器 | 沒有可用的更換。 |  |
| 開發人員 | Lodash/下划線客戶端庫。 Adobe不計畫進一步維護和更新作為分發的一部分發運的Lodash/下划線客戶端庫（快速啟動） | Adobe建議仍需要Lodash/下划線的客戶將其代碼添加到其項目代碼庫中。 |  |

## 移除的功能 {#removed-features}

本節列出了已從6.5中刪除的功AEM能和功能。以前的版本將這些功能標籤為不建議使用。

| 區域 | 功能 | 替代方案 | 版本 (SP) |
|--- |--- |--- |--- |
|  與 [!DNL Experience Cloud] 整合 | 您可以將資產與 [!DNL Experience Cloud] 使用配置 [!DNL Adobe I/O]。 [!DNL Adobe Experience Cloud] 以前叫 [!DNL Adobe Experience Cloud]。 | 如果你有任何疑問， [聯繫Adobe客戶支援](https://experienceleague.adobe.com/?support-solution=General#support)。 |  |
| 分析Activity Map | 包含在中的Activity Map版本AEM。 | 由於 Adobe Analytics API 中的安全性變更，AEM 中包含的 Activity Map 版本已無法再使用。使用 [ActivityMap插件由Adobe Analytics提供](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=zh-Hant)。 |  |
| Integrations | ExactTarget整合已從預設分發（快速啟動）中刪除，並且不再可用。 | 沒有替換。 |  |
| 整合 | Salesforce Force API整合已從預設分發(Quickstart)中刪除，現在是要從中安裝的額外包 [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)。 | 該功能仍然可用。 |
| Forms | 已取消對Adobe中央遷移橋服務的支援，因為不再支援Adobe中央產品。 | 沒有替換。 |  |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 沒有替換。 |  |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 無替換 |  |
| Forms | 無法在JEE上從LiveCycleES4 SP1升級到AEM6.5Forms的單跳升級 | 請參閱 [可用升級路徑](../forms/using/upgrade.md) AEM Forms升級文檔。 |  |
| Forms | 已從AEM Forms刪除基於UPD的JEE群集支援 | 您只能在JEE上在AEM Forms使用基於TCP的群集。 如果在JEE上將UDP多播伺服器從以前版本升級到AEM5.5Forms，請執行手動配置以切換到基於TCP的gemfire群集。 有關詳細說明，請參見 [升級到AEMJEE上的6.5表單](../forms/using/upgrade-forms-jee.md) |  |
| 開發人員 | Firebug Lite已從預設分發（快速啟動）中刪除 | 使用瀏覽器內置的開發人員控制台 |
| 開發人員 | 刪除 `customJavaScriptPath` 在HTML客戶端庫管理器中提供支援。 | 無替換 |  |
| [!DNL Assets] | 資產卸載功能將在 [!DNL Adobe Experience Manager] 6.5 | 沒有可用的更換。 |  |
| 快取 | `system/console/slingjsp` 在6.5中不AEM再可用。 | 類和輕微快取儲存在Apache Sling Commons FileSystem ClassLoader包下。 您可以在Web控制台中檢查捆綁AEM包編號，並直接從檔案系統中刪除快取資料夾(`crx-quickstart/launchpad/felix/bundle<ID>`)。 |  |

## 下一版本的預發佈 {#pre-announcement-for-next-release}

本部分用於預先宣佈未來版本中即將進行的更改。 已宣佈的更改尚未生效，但將影響客戶。 例如，這些功能尚未過時，但會在棄用後影響用戶。 這些更新是為了規劃而提供的。

| 區域 | 功能 | 公告 |
|--- |--- |--- |
| 基礎 | UI框架 | Adobe計畫在2019年棄用Coral UI 2元件。 Coral UI 3採用AEM6.2,AEM6.5完全基於Coral 3。 Adobe建議已使用Coral 2構建自定義用戶介面的客戶和合作夥伴將這些用戶介面重新分解為Coral 3。 Adobe提供了一種工具，將Coral 2對話框轉換為Coral 3 - [閱讀更多內容](/help/sites-developing/modernization-tools.md)。 |
