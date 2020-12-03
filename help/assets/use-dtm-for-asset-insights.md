---
title: 透過DTM啟用資產見解
description: 瞭解如何使用Adobe動態標籤管理(DTM)來啟用資產分析。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---


# 透過DTM {#enable-asset-insights-through-dtm}啟用資產分析

Adobe動態標籤管理是可啟動數位行銷工具的工具。 Adobe Analytics客戶可免費取得。 您可以自訂追蹤代碼，讓協力廠商CMS解決方案使用「資產前瞻分析」，或使用DTM插入「資產前瞻分析」標籤。 只有影像才支援並提供見解。

>[!CAUTION]
>
>Adobe DTM已過時，改用[!DNL Adobe Experience Platform Launch]，即將到達[生命週期結束](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f)。 Adobe建議您[使用 [!DNL Launch] 來取得資產見解](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html)。

執行這些步驟，以透過DTM啟用資產分析。

1. 按一下Experience Manager標誌，並前往&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 前瞻分析設定]**。
1. [使用DTM Cloud服務配置Experience Manager部署](/help/sites-administering/dtm.md)

   當您登入[https://dtm.adobe.com](https://dtm.adobe.com/)並造訪使用者設定檔中的&#x200B;**[!UICONTROL 帳戶設定]**&#x200B;時，API Token就應可用。 從資產前瞻分析的角度來看，此步驟不是必需的，因為Experience Manager Sites與資產前瞻分析的整合仍在進行中。

1. 登入[https://dtm.adobe.com](https://dtm.adobe.com/)，並視需要選擇公司。
1. 建立或開啟現有的Web屬性

   * 選擇&#x200B;**[!UICONTROL Web屬性]**&#x200B;頁籤，然後按一下&#x200B;**[!UICONTROL 添加屬性]**。

   * 視需要更新欄位，然後按一下「建立屬性」。 ****&#x200B;請參閱[documentation](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)。

   ![建立編輯Web屬性](assets/Create-edit-web-property.png)

1. 在&#x200B;**[!UICONTROL Rules]**&#x200B;標籤中，從導覽窗格中選擇&#x200B;**[!UICONTROL Page Load Rules]**，然後按一下&#x200B;**[!UICONTROL Create New Rule]**。

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. 展開&#x200B;**[!UICONTROL JavaScript /第三方標籤]**。 然後，在&#x200B;**[!UICONTROL 循序HTML]**&#x200B;標籤中按一下「新增指令碼&#x200B;****」以開啟「指令碼」對話方塊。

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. 按一下Experience Manager標誌，並前往&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 資產]**。
1. 按一下「**[!UICONTROL 前瞻分析頁面追蹤器]**」，複製追蹤器代碼，然後貼到您在步驟6中開啟的「指令碼」對話方塊中。 儲存變更。

   >[!NOTE]
   >
   >* `AppMeasurement.js` 中。預計可透過DTM的Adobe Analytics工具取得。
   >* 將刪除對`assetAnalytics.dispatcher.init()`的調用。 當DTM的Adobe Analytics工具載入完成時，預期會呼叫此函式。
   >* 視資產前瞻分析頁面追蹤器的托管位置（例如Experience Manager、CDN等）而定，指令碼來源的來源可能需要變更。
   >* 對於Experience Manager代管的頁面追蹤器，來源應使用分派程式例項的主機名稱指向發佈例項。


1. 存取 `https://dtm.adobe.com`. 按一下Web屬性中的&#x200B;**[!UICONTROL 概述]**，然後按一下「新增工具」，或開啟現有的Adobe Analytics工具。 ****&#x200B;在建立工具時，可以將&#x200B;**[!UICONTROL 配置方法]**&#x200B;設定為&#x200B;**[!UICONTROL 自動]**。

   ![新增Adobe Analytics工具](assets/Add-Adobe-Analytics-Tool.png)

   視需要選取「測試／生產」報表套裝。

1. 展開「庫管理」**[!UICONTROL ，並確保****的「載入庫」設定為「頁首」]**。]****[!UICONTROL 

   ![chlimage_1-61](assets/chlimage_1-197.png)

1. 展開&#x200B;**[!UICONTROL 自訂頁面程式碼]**，然後按一下&#x200B;**[!UICONTROL 開啟編輯器]**。

   ![chlimage_1-62](assets/chlimage_1-198.png)

1. 在視窗中貼上下列程式碼：

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

   * DTM中的頁面載入規則僅包含`pagetracker.js`程式碼。 任何`assetAnalytics`欄位皆視為預設值的覆寫。 預設不需要這些字元。
   * 在確定`_satellite.getToolsByType('sc')[0].getS()`已初始化且`assetAnalytics,dispatcher.init`可用後，代碼會呼叫`assetAnalytics.dispatcher.init()`。 因此，您可以略過在步驟11中加入。
   * 如前瞻分析頁面追蹤器程式碼（**[!UICONTROL 工具>資產>前瞻分析頁面追蹤器]**）中的注釋所示，當頁面追蹤器未建立`AppMeasurement`物件時，前三個引數（RSID、追蹤伺服器和訪客命名空間）並不相關。 會改為傳遞空字串以反白標示此值。\
      其餘引數對應於「前瞻分析設定」頁面（**[!UICONTROL 工具>資產>前瞻分析設定]**）中設定的值。
   * AppMeasurement物件是透過查詢`satelliteLib`所有可用的SiteCatalyst引擎來擷取。 如果已設定多個標籤，請適當變更陣列選擇器的索引。 依據DTM介面中可用的SiteCatalyst工具，陣列中的項目排序。

1. 儲存並關閉「程式碼編輯器」視窗，然後儲存「工具」設定中的變更。
1. 在&#x200B;**[!UICONTROL Approvals]**&#x200B;標籤中，批准兩個待審批。 DTM標籤已準備好可插入網頁。 如需如何在網頁中插入DTM標籤的詳細資訊，請參閱[將DTM整合在自訂頁面範本中](https://blogs.adobe.com/experiencedelivers/experience-management/integrating-dtm-custom-aem6-page-template/)。
