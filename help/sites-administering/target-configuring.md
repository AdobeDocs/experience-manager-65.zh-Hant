---
title: 手動設定與Adobe Target的整合
seo-title: 手動設定與Adobe Target的整合
description: 瞭解如何手動設定與Adobe target的整合。
seo-description: 瞭解如何手動設定與Adobe target的整合。
uuid: 0bb76a65-f981-4cc5-bee8-5feb3297137c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 20c8eb1d-5847-4902-b7d3-4c3286423b46
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# 手動設定與Adobe Target的整合 {#manually-configuring-the-integration-with-adobe-target}

您可以修改使用精靈時所做的選擇加入精靈設定，也可以手動與Adobe Target整合，而不需使用精靈。

## 修改加入嚮導配置 {#modifying-the-opt-in-wizard-configurations}

整合 [AEM與Adobe Target](/help/sites-administering/opt-in.md)[](/help/sites-administering/target.md) 的「選擇加入」精靈會自動建立名為「已布建的目標設定」的Target雲端設定。 該嚮導還為名為「已布建的目標框架」的雲配置建立Target框架。 您可以視需要修改雲端組態和架構的屬性。

您也可以設定A4T Analytics雲端設定，將Adobe Target設定為在定位內容時，將Adobe Target用作報告來源。

若要找到雲端設定和架構，請導覽至 **Cloud Services** ( **透過工具** > **部署** > **** Cloud)。 ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))在Adobe Target下方，按一下或點選「顯 **示設定」**。

### 已布建的目標配置屬性 {#provisioned-target-configuration-properties}

下列屬性值用於「選擇加入」精靈所建立的「布建目標設定」雲端設定：

* **** 用戶端代碼：在選擇加入精靈中輸入。
* **** 電子郵件：在選擇加入精靈中輸入。
* **** 密碼：在選擇加入精靈中輸入。
* **** API類型：REST
* **** 從Adobe target同步區段：已選取。

* **** 用戶端程式庫：mbox.js。
* **** 使用DTM來傳送用戶端程式庫：未選取。 如果您使用DTM [](/help/sites-administering/dtm.md) 或其他標籤管理系統來代管mbox.js或AT.js檔案，請選取此選項。 Adobe建議您使用DTM而非AEM來傳送程式庫。

* **** 自訂mbox.js:未指定預設mbox.js檔案。 指定自訂mbox.js檔案，視需要使用。 只有在您選取了mbox.js時才會顯示。
* **** 自訂AT.js:未指定預設AT.js檔案。 指定自訂AT.js檔案以視需要使用。 只有在您選取了AT.js時才會顯示。

>[!NOTE]
>
>在AEM 6.3中，您可以選取Target Library檔案 [AT.JS](https://marketing.adobe.com/resources/help/en_US/target/ov2/c_target-atjs-implementation.html)，這是Adobe Target的新實作庫，專為一般Web實作和單頁應用程式而設計。
>
>AT.js提供多項mbox.js程式庫的改進：
>
>* 改善網頁建置的頁面載入時間
>* 改善的安全性
>* 針對單頁應用程式提供更佳的實作選項
>* AT.js包含target.js中包含的元件，因此不再有對target.js的呼叫
>
>
如需詳 [細資訊，請參閱](https://marketing.adobe.com/resources/help/en_US/target/rn/201604.html) 「Target發行說明」。

### 已布建的目標框架屬性 {#provisioned-target-framework-properties}

「選擇加入」精靈建立的「已布建的目標架構」已設定為從「設定檔資料儲存區」傳送上下文資料。 預設會將商店的年齡和性別資料項目傳送至Target。 您的解決方案可能需要傳送其他參數。

![chlimage_1-158](assets/chlimage_1-158.png)

您可以設定框架，依新增Target架構中所述，將其他上下文 [資訊傳送至Target](/help/sites-administering/target-configuring.md#adding-a-target-framework)。

### Configuring A4T Analytics Cloud Configuration {#configuring-a-t-analytics-cloud-configuration}

您可以設定Adobe Target，以在定位內容時使用Adobe Analytics作為報告來源。

若要這麼做，您必須指定要將Adobe Target雲端設定與下列項目連接的A4T雲端設定：

1. 透過 **AEM logo** > **Deployment** Tools **> Cloud Services**********，導覽至Cloud Services。
1. 在「 **Adobe Target」區段中** ，按一下「 **立即設定」**。
1. 重新連線至您的Adobe Target設定。
1. 在 **A4T Analytics cloud設定下拉式選單中** ，選取架構。

   >[!NOTE]
   >
   >只有為A4T啟用的分析設定可用。
   >
   >使用AEM設定A4T時，您可能會看到「設定參考」遺失項目。 若要能夠選取分析架構，請執行下列動作：
   >
   >1. 導覽至「 **工具** >一 **般** > **CRXDE Lite**」。
   1. 導覽至 **/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig**
   1. 將屬性disable **設為****false**。
   1. 點選或按一下「 **全部儲存**」。


   ![chlimage_1-159](assets/chlimage_1-159.png)

   按一下 **確定**。 當您使用Adobe Target定位內容時，可以選 [取報表來源](/help/sites-authoring/content-targeting-touch.md)。

## 手動與Adobe target整合 {#manually-integrating-with-adobe-target}

手動與Adobe Target整合，而非使用選擇加入精靈。

>[!NOTE]
Target Library檔案 [AT.JS](https://marketing.adobe.com/resources/help/en_US/target/ov2/c_target-atjs-implementation.html)，是Adobe Target的全新實作庫，專為一般Web實作和單頁應用程式而設計。 Adobe建議您使用AT.js而非mbox.js做為用戶端程式庫。
AT.js提供多項mbox.js程式庫的改進：
* 改善網頁建置的頁面載入時間
* 改善的安全性
* 針對單頁應用程式提供更佳的實作選項
* AT.js包含target.js中包含的元件，因此不再有對target.js的呼叫

如需詳 [細資訊，請參閱](https://marketing.adobe.com/resources/help/en_US/target/rn/201604.html) 「Target發行說明」。
您可以在「用戶端程式庫」下拉式選單中選 **取** AT.js或mbox.js。

### 建立Target cloud設定 {#creating-a-target-cloud-configuration}

若要讓AEM與Adobe Target互動，請建立Target雲端設定。 若要建立設定，請提供Adobe target用戶端程式碼和使用者認證。

您只需建立一次Target雲端設定，因為您可以將設定與多個AEM促銷活動建立關聯。 如果您有數個Adobe target用戶端代碼，請為每個用戶端代碼建立一個組態。

您可以設定雲端設定，以同步來自Adobe Target的區段。 如果您啟用同步，當儲存雲端設定時，就會從背景的Target匯入區段。

請依照下列步驟，在AEM中建立Target雲端設定：

1. 透過 **AEM logo** > **Deployment** Tools **> Cloud Services**********，導覽至Cloud Services。 ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   隨即 **會開啟Adobe Marketing Cloud** 總覽頁面。

1. 在「 **Adobe Target」區段中** ，按一下「 **立即設定」**。
1. 在「建立 **配置** 」對話框中：

   1. 為配置指定 **標題**。
   1. 選取 **Adobe Target設定範本** 。
   1. 按一下&#x200B;**「建立」**。
   編輯對話框隨即開啟。

   ![chlimage_1-160](assets/chlimage_1-160.png)

   >[!NOTE]
   使用AEM設定A4T時，您可能會看到「設定參考」遺失項目。 若要能夠選取分析架構，請執行下列動作：
   1. 導覽至「 **工具** >一 **般** > **CRXDE Lite**」。
   1. 導覽至 **/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig**
   1. 將屬性disable **設為****false**。
   1. 點選或按一下「 **全部儲存**」。


1. 在對話框中，提供這些屬性的值。

   * **用戶端代碼**:目標帳戶用戶端代碼
   * **電子郵件**:目標帳戶電子郵件。
   * **密碼**:目標帳戶密碼。
   * **API類型**:REST或XML
   * **A4T Analytics雲端設定**:選取用於目標活動目標和度量的Analytics雲端設定。 如果您在定位內容時使用Adobe Analytics做為報告來源，則需要此功能。 如果您看不到雲端設定，請參閱「設定 [A4T Analytics雲端設定」中的附註](#configuring-a-t-analytics-cloud-configuration)。

   * **** 使用精確的定位：預設情況下，此複選框處於選中狀態。 如果選取此選項，雲端服務設定會等待載入內容後再載入內容。 請參閱以下附註。
   * **** 從Adobe target同步區段：選取這個選項可下載在Target中定義的區段，以便在AEM中使用。 當「API類型」屬性為REST時，您必須選取此選項，因為不支援內嵌區段，而且您一律需要使用Target中的區段。 （請注意，「區段」的AEM詞語等同於「目標對象」。）
   * **** 用戶端程式庫：選取您要mbox.js或AT.js用戶端程式庫。
   * **使用DTM來傳送用戶端程式庫** -選取此選項，以使用DTM或其他標籤管理系統的AT.js或mbox.js。 您必須 [設定DTM整合](/help/sites-administering/dtm.md) ，才能使用此選項。 Adobe建議您使用DTM而非AEM來傳送程式庫。
   * **自訂mbox.js**:如果您勾選DTM方塊或使用預設mbox.js，請留空。 或者，上傳您的自訂mbox.js。 只有在您選取了mbox.js時才會顯示。
   * **自訂AT.js**:如果您勾選DTM方塊或使用預設AT.js，請留空。 或者，上傳您的自訂AT.js。 只有在您選取了AT.js時才會顯示。
   >[!NOTE]
   在您選擇加入Adobe target設定精靈時，預設會啟用「精確定位」。
   精確定位意味著雲端服務設定會在載入內容之前等待載入內容。 因此，在效能方面，精確定位可能會在載入內容前造成毫秒數的延遲。
   作者例項一律會啟用正確定位。 不過，在發佈例項中，您可以透過清除雲端服務設定中「精確定位」旁的核取標籤(**http://localhost:4502/etc/cloudservices.html**)，選擇全域關閉精確定位。 您也可以針對個別元件開啟或關閉精確定位，不論您在雲端服務組態中的設定為何。
   如果您已建 ***立目標元件*** ，而且您變更了此設定，則您所做的變更不會影響這些元件。 您必須直接對這些元件進行任何變更。

1. 按一 **下「連線至Target** 」以初始化與Target的連線。 如果連接成功，則顯示「 **Connection successful** （連接成功）」消息。 按一 **下訊息上** 「確定」，然後 **在對話方塊上** 按「確定」。

   如果您無法連線至Target，請參閱疑難 [排解](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) 一節。

### 新增Target架構 {#adding-a-target-framework}

設定Target雲端設定後，請新增Target架構。 此架構可識別從可用的 [Client Context](/help/sites-administering/client-context.md) 或 [ContextHub元件傳送至Adobe Target的預設參](/help/sites-administering/contexthub-config.md) 數。 Target會使用參數來決定套用至目前上下文的區段。

您可以為單一Target設定建立多個架構。 當您需要針對網站的不同區段傳送不同的參數集至Target時，多個架構非常實用。 為需要傳送的每組參數建立架構。 將網站的每個區段與適當的架構建立關聯。 請注意，網頁一次只能使用一個架構。

1. 在您的Target設定頁面上，按一 **下** 「可用架構」旁的+（加號）。
1. 在「建立架構」對話方塊中，指 **定標題**，選取 **Adobe Target Framework**，然後按一下「 **建立**」。

   ![chlimage_1-161](assets/chlimage_1-161.png)

   框架頁面隨即開啟。 Sidekick提供代表您可映射之 [Client Context](/help/sites-administering/client-context.md)[或ContextHub](/help/sites-administering/contexthub-config.md) 資訊的元件。

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. 拖曳代表您要用來對應至拖放目標之資料的「用戶端內容」元件。 或者，將&#x200B;**ContextHub Store** 元件拖曳至架構。

   >[!NOTE]
   映射時，參數會透過簡單字串傳遞至mbox。 您無法從ContextHub映射陣列。

   例如，若要使用網站訪 **客的「描述檔資料** 」來控制Target促銷活動，請將「描述檔資料 **** 」元件拖曳至頁面。 此時會顯示可映射至Target參數的描述檔資料變數。

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. 選取適當欄中的「共用」核取方塊，以選取您要讓Adobe Target系統可見的 **變數** 。

   ![chlimage_1-164](assets/chlimage_1-164.png)

   >[!NOTE]
   同步參數只有一種方式——從AEM到Adobe Target。

系統會建立您的架構。 若要將架構複製至發佈例項，請使用側 **點中的「啟用架構** 」選項。

### 將活動與Target cloud設定關聯 {#associating-activities-with-the-target-cloud-configuration}

將 [AEM活動與Target雲端設定關聯](/help/sites-authoring/activitylib.md) ，以便您能夠在 [Adobe Target中鏡像活動](https://marketing.adobe.com/resources/help/en_US/target/target/c_manage_content.html)。

>[!NOTE]
可用的活動類型由以下各項決定：
* 如果 **AEM端使用的Adobe Target租用戶(clientcode)上啟用** xt_only **選項以連線至Adobe Target，則您只能在AEM中建立** XT活動。

* 如果 **Adobe Target租用戶(clientcode)** 未啟用xt_only **** 選項 **，則您可以在AEM中建立** XT和A/B活動。

**** 其他附註： **xt_only** options是套用在特定Target租用戶（客戶代碼）上的設定，只能在Adobe Target中直接修改。 您無法在AEM中啟用或停用此選項。

### 將Target架構與您的網站建立關聯 {#associating-the-target-framework-with-your-site}

在AEM中建立Target架構後，請將網頁與架構建立關聯。 頁面上的目標元件會將架構定義的資料傳送至Adobe Target以進行追蹤。 (請參閱 [內容定位](/help/sites-authoring/content-targeting-touch.md)。)

將頁面與框架關聯時，子頁面繼承關聯。

1. 在「 **Sites** 」主控台中，導覽至您要設定的網站。
1. 使用快速 [動作](/help/sites-authoring/basic-handling.md#quick-actions) 或選 [擇模式](/help/sites-authoring/basic-handling.md)，選 **取「檢視屬性」。**
1. 選擇「 **雲端服務** 」標籤。
1. 點選／按一下「 **編輯**」。
1. 點選／按一 **下「雲端服務****設定」下的「新增設定」** ，然後選 **取「Adobe Target**」。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 在「配置參考」( **Configuration Reference)下選擇要的框架**。

   >[!NOTE]
   請確定您選取您建立的 **特定架構** ，而非建立該架構時所依據的Target雲端設定。

1. 點選／按一下「 **完成**」。
1. 啟動網站的根頁面，將其複製至發佈伺服器。 (請參 [閱如何發佈頁面](/help/sites-authoring/publishing-pages.md)。)

   >[!NOTE]
   如果您附加至頁面的架構尚未啟動，則會開啟精靈，讓您也能發佈它。

## 疑難排解Target連線問題 {#troubleshooting-target-connection-problems}

執行下列工作以疑難排解連線至Target時發生的問題：

* 請確定您提供的使用者憑證正確無誤。
* 請確定AEM例項可以連線至Target伺服器。 例如，請確定防火牆規則未封鎖傳出AEM連線，或AEM已設定為使用必要的Proxy。
* 在AEM錯誤記錄中尋找有用的訊息。 error.log檔案位於安裝AEM **的crx-quickstart/logs** 目錄中。
* 在Adobe target中編輯活動時，URL會指向localhost。 請將AEM外部化設定為正確的URL，以解決此問題。

