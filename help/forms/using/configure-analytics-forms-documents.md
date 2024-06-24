---
title: 設定分析和報表
description: 瞭解如何設定Adobe Analytics以發現使用者在使用最適化表單、最適化檔案和HTML5表單時面臨的互動模式和問題。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
docset: aem65
exl-id: 72f0f8e3-e70b-4f78-aa0e-b31768b536f7
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
feature: Adaptive Forms
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 1%

---

# 使用Cloud Service框架的Analytics {#analyticsusingcloudframework}

AEM Forms與Analytics整合，可讓您擷取及追蹤已發佈表單和檔案的績效量度。 分析這些量度背後的目的是，根據使表單或檔案更易於使用所需的變更相關資料，做出明智的決定。

>[!NOTE]
>
>AEM Forms中的分析功能屬於AEM Forms附加元件套件的一部分。 如需有關安裝附加元件套件的資訊，請參閱 [安裝和設定AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).
>
>除了附加元件套件之外，您還需要Adobe Analytics帳戶和AEM執行個體的管理員許可權。 如需解決方案的相關資訊，請參閱 [Adobe Analytics](https://www.adobe.com/solutions/digital-analytics.html).

您也可以使用Analytics Launch執行Adobe。 如需如何將AEM Forms與Adobe Launch整合的詳細資訊，請參閱 [使用Analytics Launch進行Adobe](/help/forms/using/integrate-aem-forms-with-adobe-analytics.md).

## 概觀 {#overview}

您可以使用Adobe Analytics來探索使用者在使用最適化表單、HTML5表單和互動式通訊時所面臨的互動模式和問題。 Adobe分析可立即追蹤並儲存下列引數的相關資訊：

* **平均填充時間**：填寫表單所花的平均時間。
* **轉譯**：表單開啟的次數。
* **草稿**：表單以草稿狀態儲存的次數。
* **提交內容**：表單提交次數。
* **中止**：使用者未完成表單就離開的次數。

您可以自訂Adobe Analytics以新增/移除更多引數。 除了上述資訊外，此報表還包含有關HTML5每個面板和調適型表單的下列資訊：

* **時間**：面板和面板欄位逗留時間。
* **錯誤**：在面板和面板欄位上遇到的錯誤數。
* **說明**：使用者開啟面板說明及面板欄位的次數。

## 建立報表套裝 {#creating-report-suite}

Analytics資料儲存在客戶特定的存放庫，稱為報表套裝。 若要建立報表套裝並使用Adobe Analytics，您必須具備有效的Adobe Marketing Cloud帳戶。 執行以下步驟之前，請確定您擁有有效的Adobe Marketing Cloud帳戶。

執行以下步驟來建立報表套裝。

1. 登入： [https://sc.omniture.com/login/](https://sc.omniture.com/login/)
1. 在Marketing Cloud中，選取 **管理員** > **Admin Console** > **報表套裝**.
1. 選取 **新建** > **報表套裝** （位於「報表套裝管理器」）。

   ![建立新的報表套裝](assets/newreportsuite_new.png)

   建立新的報表套裝

1. 請確定第一個下拉式清單設為 **從範本建立** 然後選取 **商務**.
1. 找到 **報告套裝ID** 並新增報表套裝ID。 例如，JJEsquire。 報表套裝ID會顯示在「報表套裝ID」欄位下方。 它包含自動前置詞，通常是公司名稱。
1. 新增 **網站標題**. 例如，JJEsquire Getting Started Suite。 此標題用在Analytics UI中。 在程式碼中使用報表套裝ID。
1. 選取 **時區** 下拉式清單中的。 所有進入此報表套裝的資料都會根據定義的時區進行記錄。
1. 離開 **基礎URL** 和 **預設頁面** 欄位空白。 這兩個值只會從Adobe Marketing Cloud介面用來連結至您的網站。
1. 離開 **上線日期** 設定為今天。 上線日期是決定報表套裝啟動的時間。
1. 在 **預估每日頁面檢視次數** 欄位，輸入100。 使用此欄位來預估您預計網站每天的頁面檢視次數。 此估算可讓Adobe部署適當數量的硬體，以處理您將要收集的資料。
1. 選取 **基本貨幣** 下拉式清單中的。 所有進入此報表套裝的貨幣資料都會轉換並儲存為此貨幣格式。
1. 按一下 **建立報告** 套裝。 您應該會看到頁面重新整理並顯示訊息，指出您的報表套裝已成功建立。
1. 選取新建立的報表套裝。 瀏覽至 **編輯設定** > **一般** > **一般帳戶設定**.

   ![一般帳戶設定](assets/geographic_settings.png)

   一般帳戶設定

1. 在「一般帳戶設定」畫面中，啟用 **地理位置報表**，然後按一下 **儲存。**
1. 瀏覽至 **編輯設定** > **流量** > **流量變數**.
1. 在報表套裝中，設定並啟用以下流量變數。

   * **formName**：適用性表單的識別碼。
   * **formInstance**：最適化表單執行個體的識別碼。 啟用此變數的路徑報表。
   * **fieldName**：最適化表單欄位的識別碼。 啟用此變數的路徑報表。
   * **panelName**：最適化表單面板的識別碼。 啟用此變數的路徑報表。
   * **formTitle**：表單標題。
   * **fieldTitle**：表單欄位的標題。
   * **panelTitle**：表單面板的標題。
   * **analyticsVersion**：表單分析的版本。

1. 瀏覽至 **編輯設定** > **轉換** > **成功事件**. 定義並啟用下列成功事件：

   | 成功事件 | 類型 |
   |---|---|
   | 捨棄 | 計數器 |
   | 轉譯 | 計數器 |
   | panelVisit | 計數器 |
   | fieldVisit | 計數器 |
   | 儲存 | 計數器 |
   | 錯誤 | 計數器 |
   | 說明 | 計數器 |
   | 提交 | 計數器 |
   | 逗留時間 | 數值 |

   >[!NOTE]
   >
   >用來設定AEM Forms Analytics的事件編號和Prop編號，必須不同於中使用的事件編號和Prop編號 [AEM分析](/help/sites-administering/adobeanalytics.md) 設定。

1. 登出Adobe Marketing Cloud帳戶。

## 建立Cloud Service設定 {#creating-cloud-service-configuration}

Cloud Service設定是Adobe Analytics帳戶的相關資訊。 此設定可讓Adobe Experience Manager (AEM)連線至Adobe Analytics。 為您使用的每個Analytics帳戶建立個別設定。

1. 以管理員身分登入您的AEM作者執行個體。
1. 在左上角，按一下 **Adobe Experience Manager** > **工具** ![槌子圖示](/help/forms/using/assets/tools.png) > **Cloud Service** > **舊版Cloud Service**.
1. 尋找 **Adobe Analytics** 圖示。 按一下 **顯示設定** 然後繼續按一下 **[+]** 以新增設定。

   如果您是首次使用者，請按一下 **立即設定**.

1. 將標題新增到新設定（填寫名稱欄位是選擇性的）。 例如，我的分析設定。 按一下&#x200B;**建立**。

1. 在設定頁面上開啟「編輯」面板時，請填寫欄位：

   * **公司**：貴公司在Adobe Analytics上的主要名稱。
   * **使用者名稱**：用來登入Adobe Analytics的名稱。
   * **密碼**：上述帳戶的Adobe Analytics密碼。
   * **資料中心**：您的Adobe Analytics帳戶的資料中心。

1. 按一下 **連線至Analytics**. 會出現一個對話方塊，並顯示連線成功的訊息。 按一下&#x200B;**「確定」**。

## 建立Cloud Service架構 {#creating-cloud-service-framework}

Adobe Analytics框架是一組Adobe Analytics變數與AEM變數之間的對應。 使用框架來設定表單如何填入資料至Adobe Analytics報表。 架構與Adobe Analytics設定相關聯。 您可以為每個設定建立多個架構。

1. 在AEM雲端服務主控台上，按一下 **顯示設定**，位於Adobe Analytics下。
1. 按一下 **[+]** Analytics設定旁的連結。

   ![Adobe Analytics設定](assets/adobe-analytics-cloud-services.png)

   Adobe Analytics設定

1. 輸入a **標題** 和 **名稱** 針對框架，選取 **Adobe Analytics** 框架，然後按一下 **建立**. 隨即開啟框架進行編輯。
1. 在側邊面板的「報表套裝」區段中，按一下 **新增專案**，然後使用下拉式清單來選取與框架互動的報表套裝ID （例如JJEsquire）。
1. 在報表套裝ID旁邊，選取您要傳送資訊至報表套裝的伺服器執行個體。

   ![information_to_send_to_report_suite](assets/information_to_send_to_report_suite.png)

1. 拖曳 **Form Analytics元件** 從 **其他** 類別從Sidekick到框架。
1. 若要使用元件中定義的變數對應Analytics變數，請將變數從AEM內容尋找器拖曳至追蹤元件上的欄位。

   ![將AEM變數與Adobe Analytics變數對應](assets/analytics_new.png)

1. 使用啟動框架 **頁面索引標籤** 在sidekick中，按一下 **啟動框架**.

## 設定AEM Forms Analytics設定服務 {#configuring-aem-forms-analytics-configuration-service}

1. 在編寫執行個體上，開啟AEM Web控制檯設定管理員，位於 `https://<server>:<port>;/system/console/configMgr`.
1. 找到並開啟AEM Forms Analytics設定

   ![AEM Forms Analytics設定服務](assets/analytics_configuration.png)

   AEM Forms Analytics設定服務

1. 為下列欄位指定適當的值，然後按一下 **儲存**.

   * **SiteCatalyst框架**：選取您在「設定追蹤的架構」區段中定義的架構/設定。
   * **欄位時間追蹤基準線**：指定必須以秒為單位追蹤欄位造訪的持續時間。 預設值為 0。當值大於0 （零）時，會將兩個個別的追蹤事件傳送至Adobe Analytics伺服器。 第一個事件會指示Analytics伺服器停止追蹤退出欄位。 第二個事件會在指定的期間過後傳送。 第二個事件會指示Analytics伺服器開始追蹤造訪的欄位。 使用兩個不同的事件有助於準確測量在欄位上逗留的時間。 當值為0 （零）時，單一追蹤事件會傳送至Adobe Analytics伺服器。

   * **Analytics報表同步cron**：指定從Adobe Analytics擷取報表的cron運算式。 預設值為0 0 2 ？ &#42; &#42;.

   * **擷取報表逾時：** 指定等候伺服器回應分析報告的持續時間（以秒為單位）。 預設時間為120秒。

   >[!NOTE]
   >
   >逾時報表擷取作業最多可能需要10秒，而不是指定的秒數。

1. 在發佈執行個體上重複步驟1-3以設定Analytics。

現在，您可以為表單啟用分析並產生分析報表。

## 為表單或檔案啟用分析 {#enabling-analytics-for-a-form-or-document}

1. 登入AEM入口網站： `https://[hostname]:'port'`.
1. 按一下 **Forms > Forms與檔案**，選取表單或檔案，然後按一下 **啟用Analytics**. 已啟用Analytics。

   ![為表單或檔案啟用分析](assets/enable-analytics-1.png)

   為表單啟用分析

   **答：** 啟用Analytics按鈕 **B.** 選取的表單

   如需檢視表單分析報表的詳細資訊，請參閱 [檢視和瞭解AEM Forms analytics報表](../../forms/using/view-understand-aem-forms-analytics-reports.md).
