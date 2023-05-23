---
title: 通過DTM啟用Assets Insights
description: 瞭解如何使用Adobe動態Tag Management(DTM)啟用Assets Insights。
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 80e8f84e-3235-4212-9dcd-6acdb9067893
source-git-commit: afc72fb6b324cf2e0ad8168f783d9c1a6f96c614
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 2%

---

# 通過DTM啟用Assets Insights {#enable-asset-insights-through-dtm}

Adobe動態Tag Management是激活您的數字營銷工具的工具。 酒店為Adobe Analytics客戶免費提供。 您可以自定義跟蹤代碼以啟用第三方CMS解決方案以使用Assets Insights，也可以使用DTM插入Assets Insights標籤。 只支援和提供影像的見解。

>[!CAUTION]
>
>AdobeDTM已棄用， [!DNL Adobe Experience Platform] 很快就會 [生命結束](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f)。 Adobe建議您 [使用 [!DNL Adobe Experience Platform] 為assets insigns](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html)。

執行這些步驟以通過DTM啟用Assets Insights。

1. 按一下Experience Manager徽標，然後轉到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 洞察力配置]**。
1. [使用DTMExperience Manager配置Cloud Service](/help/sites-administering/dtm.md)

   登錄後，API令牌應可用 [https://dtm.adobe.com](https://dtm.adobe.com/) 訪問 **[!UICONTROL 帳戶設定]** 的子菜單。 從Assets Insights的角度來看，不需要執行此步驟，因為Experience Manager Sites與Assets Insights的整合仍在進行中。

1. 登錄到 [https://dtm.adobe.com](https://dtm.adobe.com/)，然後選擇一個公司（如適用）。
1. 建立或開啟現有Web屬性

   * 選擇 **[!UICONTROL Web屬性]** ，然後按一下 **[!UICONTROL 添加屬性]**。

   * 根據需要更新欄位，然後按一下 **[!UICONTROL 建立屬性]**。 請參閱 [文檔](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant)。

   ![建立編輯Web屬性](assets/Create-edit-web-property.png)

1. 在 **[!UICONTROL 規則]** 頁籤 **[!UICONTROL 頁面載入規則]** 按一下 **[!UICONTROL 建立新規則]**。

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. 展開 **[!UICONTROL JavaScript /第三方標籤]**。 然後按一下 **[!UICONTROL 添加新指令碼]** 的 **[!UICONTROL 順序HTML]** 頁籤。

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. 按一下Experience Manager徽標，然後轉到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]**。
1. 按一下 **[!UICONTROL Insights頁跟蹤器]**，複製跟蹤程式碼，然後將其貼上到步驟6中開啟的「指令碼」對話框中。 儲存變更。

   >[!NOTE]
   >
   >* `AppMeasurement.js` 的子菜單。 預計可通過DTM的Adobe Analytics工具獲得。
   >* 呼叫 `assetAnalytics.dispatcher.init()` 的子菜單。 當DTM的Adobe Analytics工具完成載入後，將調用該函式。
   >* 根據Assets Insights Page Tracker的托管位置(例如Experience Manager、CDN等)，指令碼源的來源可能需要更改。
   >* 對於承載Experience Manager的頁面跟蹤器，源應使用調度程式實例的主機名指向發佈實例。


1. 存取 `https://dtm.adobe.com`. 按一下 **[!UICONTROL 概述]** 在web屬性中，按一下 **[!UICONTROL 添加工具]** 或者開啟現有的Adobe Analytics工具。 建立工具時，可以 **[!UICONTROL 配置方法]** 至 **[!UICONTROL 自動]**。

   ![添加Adobe Analytics工具](assets/Add-Adobe-Analytics-Tool.png)

   根據需要選擇「暫存/生產」報表套件。

1. 展開 **[!UICONTROL 庫管理]**，並確保 **[!UICONTROL 在載入庫]** 設定為 **[!UICONTROL 頁首]**。

   ![chlimage_1-61](assets/chlimage_1-197.png)

1. 展開 **[!UICONTROL 自定義頁碼]**，然後按一下 **[!UICONTROL 開啟編輯器]**。

   ![chlimage_1-62](assets/chlimage_1-198.png)

1. 在窗口中貼上以下代碼：

   ```Java
   var sObj;
   
   if (arguments.length > 0) {
     sObj = arguments[0];
   } else {
     sObj = _satellite.getToolsByType('sc')[0].getS();
   }
   _satellite.notify('in assetAnalytics customInit');
   (function initializeAssetAnalytics() {
     if ((!!window.assetAnalytics) && (!!assetAnalytics.dispatcher)) {
       _satellite.notify('assetAnalytics ready');
       /** NOTE:
           Copy over the call to 'assetAnalytics.dispatcher.init()' from Assets Pagetracker
           Be mindful about changing the AppMeasurement object as retrieved above.
       */
       assetAnalytics.dispatcher.init(
             "",  /** RSID to send tracking-call to */
             "",  /** Tracking Server to send tracking-call to */
             "",  /** Visitor Namespace to send tracking-call to */
             "",  /** listVar to put comma-separated-list of Asset IDs for Asset Impression Events in tracking-call, e.g. 'listVar1' */
             "",  /** eVar to put Asset ID for Asset Click Events in, e.g. 'eVar3' */
             "",  /** event to include in tracking-calls for Asset Impression Events, e.g. 'event8' */
             "",  /** event to include in tracking-calls for Asset Click Events, e.g. 'event7' */
             sObj  /** [OPTIONAL] if the webpage already has an AppMeasurement object, include the object here. If unspecified, Pagetracker Core shall create its own AppMeasurement object */
             );
       sObj.usePlugins = true;
       sObj.doPlugins = assetAnalytics.core.updateContextData;
       assetAnalytics.core.optimizedAssetInsights();
     }
     else {
       _satellite.notify('assetAnalytics not available. Consider updating the Custom Page Code', 4);
     }
   })();
   ```

   * DTM中的頁面載入規則僅包括 `pagetracker.js` 代碼。 任意 `assetAnalytics` 欄位被視為預設值的替代。 預設情況下不需要這些。
   * 代碼調用 `assetAnalytics.dispatcher.init()` 在確保 `_satellite.getToolsByType('sc')[0].getS()` 已初始化 `assetAnalytics,dispatcher.init` 的子菜單。 因此，您可以跳過在步驟11中添加它。
   * 如Insights頁跟蹤程式碼中的注釋(**[!UICONTROL 「工具」>「資產」>「透視」頁跟蹤器]**)，當頁面跟蹤器未建立 `AppMeasurement` 對象，前三個參數（RSID、跟蹤伺服器和訪問者命名空間）無關。 將傳遞空字串以突出顯示此項。\
      其餘參數與「洞察力配置」頁中配置的參數(**[!UICONTROL 「工具」>「資產」>「洞察力配置」]**)。
   * 通過查詢檢索AppMeasurement對象 `satelliteLib` 所有可用SiteCatalyst引擎。 如果配置了多個標籤，請相應更改陣列選擇器的索引。 陣列中的條目按DTM介面中可用的SiteCatalyst工具排序。

1. 保存並關閉「代碼編輯器」窗口，然後在「工具」配置中保存更改。
1. 在 **[!UICONTROL 批准]** 頁籤，審批兩個待定審批。 DTM標籤已準備好插入您的網頁。
