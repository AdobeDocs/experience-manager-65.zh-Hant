---
title: 手動配置與Adobe Target的整合
seo-title: Manually Configuring the Integration with Adobe Target
description: 瞭解如何手動配置與Adobe Target的整合。
seo-description: Learn how to manually configure the integration with Adobe Target.
uuid: 0bb76a65-f981-4cc5-bee8-5feb3297137c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 20c8eb1d-5847-4902-b7d3-4c3286423b46
exl-id: 0f710685-dc4f-4333-9847-d002b2637d08
source-git-commit: 813441a61baa560c9d317a5519b9e0c0d1da7a6e
workflow-type: tm+mt
source-wordcount: '2209'
ht-degree: 0%

---

# 手動配置與Adobe Target的整合 {#manually-configuring-the-integration-with-adobe-target}

您可以修改使用嚮導時所做的選擇加入嚮導配置，也可以不使用嚮導而手動與Adobe Target整合。

## 修改「選擇加入」嚮導配置 {#modifying-the-opt-in-wizard-configurations}

的 [選擇加入嚮導](/help/sites-administering/opt-in.md) 那 [與AEMAdobe Target](/help/sites-administering/target.md) 自動建立名為「已預配的目標配置」的目標雲配置。 該嚮導還為名為「已預配的目標框架」的雲配置建立目標框架。 如果需要，您可以修改雲配置和框架的屬性。

您還可以通過配置A4TAdobe Target配置，將Adobe Target配置為目標內容時的報告源。

要定位雲配置和框架，請導航至 **Cloud Services** 通過 **工具** > **部署** > **雲**。 ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))在Adobe Target下，按一下或點擊 **顯示配置**。

### 預配的目標配置屬性 {#provisioned-target-configuration-properties}

在「選擇加入」嚮導建立的「已設定目標配置」雲配置中使用以下屬性值：

* **客戶端代碼：** 在「選擇加入」嚮導中輸入。
* **電子郵件：** 在「選擇加入」嚮導中輸入。
* **密碼：** 在「選擇加入」嚮導中輸入。
* **API類型：** 休息
* **同步來自Adobe Target的段：** 已選擇。

* **客戶端庫：** mbox.js
* **使用DTM提供客戶端庫：** 未選擇。 如果 [使用DTM](/help/sites-administering/dtm.md) 或另一個標籤管理系統來承載mbox.js或AT.js檔案。 Adobe建議您使用DTM而AEM不是交付庫。

* **自定義mbox.js:** 未指定以使用預設mbox.js檔案。 根據需要指定要使用的自定義mbox.js檔案。 僅當選擇了mbox.js時才顯示。
* **自定義AT.js:** 未指定以使用預設AT.js檔案。 指定根據需要使用的自定義AT.js檔案。 僅當選擇了AT.js時才顯示。

>[!NOTE]
>
>在AEM6.3中，可以選擇目標庫檔案， [AT.JS](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/mbox-implement/mbox-download.html)它是Adobe Target的一個新的實現庫，它既適用於典型的web實現，也適用於單頁應用程式。
>
>AT.js對mbox.js庫提供了幾項改進：
>
>* 用於Web實現的改進的頁載入時間
>* 提高安全性
>* 針對單頁應用程式的更好實施選項
>* AT.js包含target.js中包含的元件，因此不再調用target.js


### 預配的目標框架屬性 {#provisioned-target-framework-properties}

「選擇加入」嚮導建立的「已設定目標框架」配置為從配置檔案資料儲存區發送上下文資料。 預設情況下，儲存的年齡和性別資料項將發送到Target。 您的解決方案可能需要發送其他參數。

![chlimage_1-158](assets/chlimage_1-158.png)

您可以配置框架，將附加上下文資訊發送到目標，如所述 [添加目標框架](/help/sites-administering/target-configuring.md#adding-a-target-framework)。

### 配置A4TAnalytics Cloud配置 {#configuring-a-t-analytics-cloud-configuration}

您可以將Adobe Target配置為在針對內容時使用Adobe Analytics作為報告源。

>[!NOTE]
>
>用戶憑據身份驗證（舊版）不能與A4T（用於目標和分析）一起使用。 因此，客戶應使用IMS驗證而不是用戶 — 憑據驗證。

為此，您需要指定哪個A4T雲配置將Adobe Target雲配置與：

1. 導航到 **Cloud Services** 通過 **AEM徽標** > **工具** > **部署** > **Cloud Services**。
1. 在 **Adobe Target** ，按一下 **立即配置**。
1. 重新連接到您的Adobe Target配置。
1. 在 **A4TAnalytics Cloud配置** 下拉菜單，選擇框架。

   >[!NOTE]
   >
   >只有為A4T啟用的分析配置可用。
   >
   >使用配置A4T時AEM，可能會看到缺少Configuration引用條目。 要能夠選擇分析框架，請執行以下操作：
   >
   >1. 導航到 **工具** > **常規** > **CRXDE Lite**。
   1. 導航到 [A4T分析配置對話框](#a4t-analytics-config-dialog) （見下文）
   1. 設定屬性 **禁用** 至 **假**。
   1. 點擊或按一下 **全部保存**。


#### A4T分析配置對話框 {#a4t-analytics-config-dialog}

```xml
/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig
```

![AdobeTargetSettings](assets/adobe-target-settings.jpg)

按一下&#x200B;**「確定」**。當你把目標對準Adobe Target時， [選擇報表源](/help/sites-authoring/content-targeting-touch.md)。

## 手動與Adobe Target整合 {#manually-integrating-with-adobe-target}

手動與Adobe Target整合，而不是使用選擇加入嚮導。

>[!NOTE]
目標庫檔案， [AT.JS](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/mbox-implement/mbox-download.html)，是為Adobe Target設計的一個新的實現庫，它既適用於典型的web實施，也適用於單頁應用程式。 Adobe建議將AT.js而不是mbox.js用作客戶端庫。
AT.js對mbox.js庫提供了幾項改進：
* 用於Web實現的改進的頁載入時間
* 提高安全性
* 針對單頁應用程式的更好實施選項
* AT.js包含target.js中包含的元件，因此不再調用target.js
>
可以在 **客戶端庫** 的下界。

### 建立目標雲配置 {#creating-a-target-cloud-configuration}

若要AEM與Adobe Target交互，請建立目標雲配置。 要建立配置，請提供Adobe Target客戶端代碼和用戶憑據。

您僅建立一次目標雲配置，因為您可以將配置與多個市場活動AEM關聯。 如果您有多個Adobe Target客戶端代碼，請為每個客戶端代碼建立一個配置。

您可以配置雲配置以同步來自Adobe Target的段。 如果啟用同步，則在保存雲配置後，會立即從後台的Target導入段。

請按下列步驟在中建立目標雲配AEM置：

1. 導航到 **Cloud Services** 通過 **AEM徽標** > **工具** > **部署** > **Cloud Services**。 ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   的 **Adobe Marketing Cloud** 的子菜單。

1. 在 **Adobe Target** ，按一下 **立即配置**。
1. 在 **建立配置** 對話框：

   1. 給配置 **標題**。
   1. 選擇 **Adobe Target配置** 的下界。
   1. 按一下&#x200B;**建立**。

   編輯對話框開啟。

   ![AdobeTargetSettings](assets/adobe-target-settings.jpg)

   >[!NOTE]
   使用配置A4T時AEM，可能會看到缺少Configuration引用條目。 要能夠選擇分析框架，請執行以下操作：
   1. 導航到 **工具** > **常規** > **CRXDE Lite**。
   1. 導航到 **/libs/cq/analytics/components/testandargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig**
   1. 設定屬性 **禁用** 至 **假**。
   1. 點擊或按一下 **全部保存**。


1. 在對話框中，提供這些屬性的值。

   * **客戶端代碼**:目標帳戶客戶端代碼
   * **電子郵件**:目標帳戶電子郵件。
   * **密碼**:目標帳戶密碼。
   * **API類型**:REST或XML
   * **A4TAnalytics Cloud配置**:選擇用於目標活動目標和度量的分析雲配置。 如果在針對內容時使用Adobe Analytics作為報告源，則需要此選項。 如果看不到雲配置，請參閱中的注釋 [配置A4TAnalytics Cloud配置](#configuring-a-t-analytics-cloud-configuration)。

   * **使用準確的目標：** 預設情況下，此複選框處於選中狀態。 如果選中，則雲服務配置將在載入內容之前等待上下文載入。 請參閱下面的注釋。
   * **同步來自Adobe Target的段：** 選擇此選項可下載在目標中定義的段以在中使AEM用。 當API Type屬性為REST時，必須選擇此選項，因為不支援內聯段，並且您始終需要使用「目標」中的段。 (請注意，AEM「段」的術語等同於目標「受眾」。)
   * **客戶端庫：** 選擇是希望使用mbox.js還是AT.js客戶端庫。
   * **使用DTM提供客戶端庫**  — 選擇此選項可使用AT.js或DTM中的mbox.js或其他標籤管理系統。 你必須 [配置DTM整合](/help/sites-administering/dtm.md) 選項。 Adobe建議您使用DTM而AEM不是交付庫。
   * **自定義mbox.js**:如果選中DTM框或使用預設mbox.js，則保留為空。 或者上載自定義mbox.js。 僅當選擇了mbox.js時才顯示。
   * **自定義AT.js**:如果選中DTM框或使用預設AT.js，則保留為空。 或者上載自定義AT.js。 僅當選擇了AT.js時才顯示。

   >[!NOTE]
   預設情況下，當您選擇加入Adobe Target配置嚮導時，將啟用「準確定位」。
   準確定位意味著雲服務配置在載入內容之前等待上下文載入。 因此，從效能上看，準確的目標可能會在載入內容之前產生幾毫秒的延遲。
   始終在作者實例上啟用精確目標。 但是，在發佈實例上，您可以選擇在雲服務配置中清除「準確瞄準」旁邊的複選標籤，從而全局關閉準確瞄準(**http://localhost:4502/etc/cloudservices.html**)。 無論您在雲服務配置中的設定如何，您仍然可以針對各個元件開啟和關閉精確的目標。
   如果 ***已*** 建立了目標元件，並且您更改了此設定，您所做的更改不會影響這些元件。 必須直接對這些元件進行任何更改。

1. 按一下 **連接到目標** 初始化與目標的連接。 如果連接成功，則消息 **連接成功** 的上界。 按一下 **確定** 在留言上，然後 **確定** 對話框。

   如果無法連接到目標，請參閱 [故障排除](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) 的子菜單。

### 添加目標框架 {#adding-a-target-framework}

配置目標雲配置後，添加目標框架。 該框架標識從可用地址發送到Adobe Target的預設參數 [客戶端上下文](/help/sites-administering/client-context.md) 或 [上下文中心](/help/sites-developing/ch-configuring.md) 元件。 目標使用參數來確定應用於當前上下文的段。

可以為單個目標配置建立多個框架。 當您需要將一組不同的參數發送給網站不同部分的「目標」時，多個框架非常有用。 為需要發送的每組參數建立一個框架。 將網站的每個部分與相應的框架相關聯。 請注意，網頁一次只能使用一個框架。

1. 在「目標配置」頁上，按一下 **+** （加號）。
1. 在「建立框架」對話框中，指定 **標題**，選擇 **Adobe Target框架**，然後按一下 **建立**。

   ![chlimage_1-161](assets/chlimage_1-161.png)

   將開啟框架頁面。 Sidekick提供表示來自 [客戶端上下文](/help/sites-administering/client-context.md) 或 [上下文中心](/help/sites-developing/ch-configuring.md) 你可以畫地圖。

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. 拖動表示要用於映射到放置目標的資料的客戶端上下文元件。 或者，拖動&#x200B;**上下文中心儲存** 框架的元件。

   >[!NOTE]
   映射時，參數通過簡單字串傳遞到mbox。 不能從ContextHub映射陣列。

   例如，要使用 **配置檔案資料** 關於站點訪問者以控制目標市場活動，拖動 **配置檔案資料** 元件。 將顯示可用於映射到「目標」參數的配置檔案資料變數。

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. 通過選擇要使Adobe Target系統可見的變數 **共用** 的子菜單。

   ![chlimage_1-164](assets/chlimage_1-164.png)

   >[!NOTE]
   同步參數只是一種方式 — 從AEM到Adobe Target。

已建立框架。 要將框架複製到發佈實例，請使用 **激活框架** 從旁邊踢出。

### 將活動與目標雲配置關聯  {#associating-activities-with-the-target-cloud-configuration}

關聯您的 [AEM活動](/help/sites-authoring/activitylib.md) 目標雲配置，以便您能夠鏡像 [Adobe Target](https://docs.adobe.com/content/help/en/target/using/experiences/offers/manage-content.html)。

>[!NOTE]
可用的活動類型由以下各項決定：
* 如果 **xt_only** 選項在Adobe Target租戶（客戶端代碼）上啟AEM用以連接到Adobe Target，然後 **僅** 中的XT活AEM動。
* 如果 **xt_only** 選項 **不** 在Adobe Target租戶（客戶端代碼）上啟用，然後可以建立 **兩者** XT和A/B活AEM動
>
**附加說明：** **xt_only** 選項是應用於特定目標租戶（客戶端代碼）的設定，只能在Adobe Target直接修改。 您無法在AEM中啟用或停用此選項。

### 將目標框架與您的站點關聯 {#associating-the-target-framework-with-your-site}

在中建立目標框架AEM後，將網頁與框架關聯。 頁面上的目標元件將框架定義的資料發送給Adobe Target進行跟蹤。 (請參閱 [內容目標](/help/sites-authoring/content-targeting-touch.md)。)

將頁面與框架關聯時，子頁面將繼承關聯。

1. 在 **站點** 控制台，導航到要配置的站點。
1. 使用 [快速操作](/help/sites-authoring/basic-handling.md#quick-actions) 或 [選擇模式](/help/sites-authoring/basic-handling.md)選中 **查看屬性。**
1. 選擇 **Cloud Services** 頁籤。
1. 點擊/按一下 **編輯**。
1. 點擊/按一下 **添加配置** 在 **Cloud Service配置** 選擇 **Adobe Target**。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 選擇要使用的框架 **配置參考**。

   >[!NOTE]
   確保選擇特定 **框架** 建立的雲配置，而不是建立該雲配置時所依據的目標雲配置。

1. 點擊/按一下 **完成**。
1. 激活網站的根頁面，將其複製到發佈伺服器。 (請參閱 [如何發佈頁面](/help/sites-authoring/publishing-pages.md)。)

   >[!NOTE]
   如果您附加到頁面的框架尚未激活，則會開啟一個嚮導，該嚮導也允許您發佈該框架。

## 目標連接問題疑難解答 {#troubleshooting-target-connection-problems}

執行以下任務以解決連接到目標時出現的問題：

* 確保您提供的用戶憑據正確。
* 確保實例AEM可以連接到目標伺服器。 例如，確保防火牆規則不阻止出站連AEM接，或已配AEM置為使用必要的代理。
* 在錯誤日誌中查找有AEM用消息。 error.log檔案位於 **crx快速啟動/日誌** 的子AEM目錄。
* 在Adobe Target編輯活動時，URL指向localhost。 通過將外部化程式設AEM置為正確的URL來解決此問題。
