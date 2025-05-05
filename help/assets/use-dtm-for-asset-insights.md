---
title: 透過DTM啟用Assets深入分析
description: 瞭解如何使用AdobeDynamic Tag Management (DTM)來啟用Assets Insights。
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 80e8f84e-3235-4212-9dcd-6acdb9067893
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 2%

---

# 透過DTM啟用Assets深入分析 {#enable-asset-insights-through-dtm}

AdobeDynamic Tag Management是可啟用您的數位行銷工具的工具。 Adobe Analytics客戶可免費使用此功能。 您可以自訂追蹤代碼，讓協力廠商CMS解決方案能夠使用Assets Insights，或使用DTM插入Assets Insights標籤。 僅支援並為影像提供深入分析。

>[!CAUTION]
>
>AdobeDTM已遭取代而支援[!DNL Adobe Experience Platform]，且即將結束[生命週期](https://medium.com/launch-by-adobe/dtm-plans-for-a-sunset-3c6aab003a6f)。 Adobe建議您[使用 [!DNL Adobe Experience Platform] 進行資產分析](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/asset-insights-launch-tutorial.html?lang=zh-Hant)。

執行這些步驟，透過DTM啟用Assets Insights。

1. 按一下Experience Manager標誌，然後前往&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 深入分析設定]**。
1. [使用DTMCloud Service設定Experience Manager部署](/help/sites-administering/dtm.md)

   在您登入[https://dtm.adobe.com](https://dtm.adobe.com/)並造訪使用者設定檔中的&#x200B;**[!UICONTROL 帳戶設定]**&#x200B;後，應該就能使用API權杖。 從Assets Insights的角度來看，不需要執行此步驟，因為仍在進行Experience Manager Sites與Assets Insights的整合。

1. 登入[https://dtm.adobe.com](https://dtm.adobe.com/)，並視需要選取公司。
1. 建立或開啟現有的Web屬性

   * 選取&#x200B;**[!UICONTROL Web屬性]**&#x200B;標籤，然後按一下&#x200B;**[!UICONTROL 新增屬性]**。

   * 視需要更新欄位，然後按一下&#x200B;**[!UICONTROL 建立屬性]**。 請參閱[文件](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant)。

   ![建立編輯Web屬性](assets/Create-edit-web-property.png)

1. 在&#x200B;**[!UICONTROL 規則]**&#x200B;標籤中，從瀏覽窗格選取&#x200B;**[!UICONTROL 頁面載入規則]**，然後按一下&#x200B;**[!UICONTROL 建立新規則]**。

   ![chlimage_1-58](assets/chlimage_1-194.png)

1. 展開&#x200B;**[!UICONTROL JavaScript /第三方標籤]**。 然後按一下&#x200B;**[!UICONTROL 循序HTML]**&#x200B;索引標籤中的&#x200B;**[!UICONTROL 新增指令碼]**&#x200B;以開啟指令碼對話方塊。

   ![chlimage_1-59](assets/chlimage_1-195.png)

1. 按一下Experience Manager標誌，然後前往&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]**。
1. 按一下&#x200B;**[!UICONTROL 前瞻分析頁面追蹤器]**，複製追蹤器程式碼，然後將其貼到您在步驟6中開啟的指令碼對話方塊中。 儲存變更。

   >[!NOTE]
   >
   >* `AppMeasurement.js`已移除。 應透過DTM的Adobe Analytics工具提供。
   >* 對`assetAnalytics.dispatcher.init()`的呼叫已移除。 DTM的Adobe Analytics工具載入完成後，應該會呼叫函式。
   >* 根據Assets前瞻分析頁面追蹤器的託管位置(例如，Experience Manager、CDN等)，指令碼來源的來源可能需要變更。
   >* 對於Experience Manager託管的頁面追蹤器，來源應使用Dispatcher執行個體的主機名稱指向發佈執行個體。

1. 存取`https://dtm.adobe.com`。 在Web屬性中按一下&#x200B;**[!UICONTROL 概觀]**，然後按一下&#x200B;**[!UICONTROL 新增工具]**&#x200B;或開啟現有的Adobe Analytics工具。 建立工具時，您可以將&#x200B;**[!UICONTROL 組態方法]**&#x200B;設定為&#x200B;**[!UICONTROL 自動]**。

   ![新增Adobe Analytics工具](assets/Add-Adobe-Analytics-Tool.png)

   視需要選取測試/生產報表套裝。

1. 展開&#x200B;**[!UICONTROL 程式庫管理]**，並確定&#x200B;**[!UICONTROL 在]**&#x200B;載入程式庫&#x200B;**[!UICONTROL 頁面頂端]**。

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
             "",  /** listVar to put comma-separated-list of Asset IDs for Asset Impression Events in tracking-call, for example, 'listVar1' */
             "",  /** eVar to put Asset ID for Asset Click Events in, for example, 'eVar3' */
             "",  /** event to include in tracking-calls for Asset Impression Events, for example, 'event8' */
             "",  /** event to include in tracking-calls for Asset Click Events, for example, 'event7' */
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

   * DTM中的頁面載入規則僅包含`pagetracker.js`程式碼。 任何`assetAnalytics`欄位都視為預設值的覆寫。 預設不需要。
   * 程式碼在確定`_satellite.getToolsByType('sc')[0].getS()`已初始化且`assetAnalytics,dispatcher.init`可用之後呼叫`assetAnalytics.dispatcher.init()`。 因此，您可以略過在步驟11中新增。
   * 如前瞻分析頁面追蹤器程式碼(**[!UICONTROL 工具> Assets >前瞻分析頁面追蹤器]**)中的評論所指示，當頁面追蹤器未建立`AppMeasurement`物件時，前三個引數（RSID、追蹤伺服器和訪客名稱空間）無關。 傳遞空字串而非醒目提示此專案。\
     其餘引數對應至見解設定頁面(**[!UICONTROL 工具> Assets >見解設定]**)中的設定內容。
   * 透過查詢所有可用AppMeasurement引擎的`satelliteLib`來擷取SiteCatalyst物件。 如果設定了多個標籤，請適當的變更陣列選擇器的索引。 陣列中的專案會根據DTM介面中可用的SiteCatalyst工具排序。

1. 儲存並關閉程式碼編輯器視窗，然後將變更儲存在工具設定中。
1. 在&#x200B;**[!UICONTROL 核准]**&#x200B;索引標籤中，核准兩個擱置的核准。 DTM標籤已可插入您的網頁。
