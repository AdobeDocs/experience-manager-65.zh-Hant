---
title: 設定分析和報表
seo-title: 設定分析和報表
description: 了解如何設定Adobe Analytics，以探索使用者使用最適化表單、最適化檔案和HTML5表單時所面臨的互動模式和問題。
seo-description: 了解如何設定Adobe Analytics，以探索使用者使用最適化表單、最適化檔案和HTML5表單時所面臨的互動模式和問題。
uuid: ac5d1300-f303-40e8-a33e-4859a54ac10d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 96a77980-4213-4779-a540-00905ea8f7e3
docset: aem65
exl-id: 72f0f8e3-e70b-4f78-aa0e-b31768b536f7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1533'
ht-degree: 1%

---

# 設定分析和報表{#configuring-analytics-and-reports}

AEM Forms與Adobe Analytics整合，可讓您擷取及追蹤已發佈表單和檔案的效能量度。 分析這些量度的目的，是根據讓表單或檔案更實用所需的變更資料，做出明智的決策。

>[!NOTE]
>
>AEM Forms中的分析功能屬於AEM Forms附加套件的一部分。 有關安裝附加軟體包的資訊，請參閱[安裝和配置AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md)。
>
>除了附加套件之外，您還需要AEM例項的Adobe Analytics帳戶和管理員權限。 如需解決方案的相關資訊，請參閱[Adobe Analytics](https://www.adobe.com/solutions/digital-analytics.html)。

## 概覽 {#overview}

您可以使用Adobe Analytics來探索使用者在使用最適化表單、HTML5表單和互動式通訊時所面臨的互動模式和問題。 Adobe分析會立即追蹤並儲存下列參數的相關資訊：

* **平均填充時間**:填寫表單的平均逗留時間。
* **轉譯**:表單開啟的次數。
* **草稿**:表單保存為草稿狀態的次數。
* **提交**:表單的提交次數。
* **中止**:使用者未填妥表單就離開的次數。

您可以自訂Adobe Analytics以新增/移除更多參數。 除了上述資訊外，報表還包含下列HTML5和最適化表單每個面板的相關資訊：

* **時間**:面板和面板欄位的逗留時間。
* **錯誤**:在面板和面板欄位上遇到的錯誤數。
* **說明**:使用者開啟面板說明和面板欄位的次數。

## 建立報表套裝{#creating-report-suite}

Analytics資料會儲存在稱為報表套裝的客戶專屬存放庫中。 若要建立報表套裝並使用Adobe Analytics，您必須具備有效的Adobe Marketing Cloud帳戶。 執行下列步驟之前，請確定您擁有有效的Adobe Marketing Cloud帳戶。

執行下列步驟來建立報表套裝。

1. 登入[https://sc.omniture.com/login/](https://sc.omniture.com/login/)
1. 在Marketing Cloud中，選取「**管理** > **Admin Console** > **報表套裝**」。
1. 在「報表套裝管理器」中，選取「**建立新** > **報表套裝**」。

   ![建立新的報表套裝](assets/newreportsuite_new.png)

   建立新的報表套裝

1. 請確定第一個下拉式清單設為「從範本&#x200B;**建立」，然後選取「**&#x200B;商務&#x200B;**」。**
1. 找出「**報表套裝ID**」欄位，然後新增報表套裝ID。 例如，JJEsquire。 報表套裝ID會顯示在「報表套裝ID」欄位下方。 其中包含自動首碼，通常是公司名稱。
1. 新增&#x200B;**網站標題**。 例如，JJEsquire Getting Started Suite。 此標題用於Analytics UI。 在程式碼中使用報表套裝ID。
1. 從下拉式清單中選取&#x200B;**時區**。 此報表套裝中的所有資料都會根據定義的時區記錄。
1. 將「**基本URL**」和「**預設頁面**」欄位保留為空白。 這兩個值只會從Adobe Marketing Cloud介面用來連結至您的網站。
1. 將&#x200B;**上線日期**&#x200B;設為今天。 「上線日期」決定報表套裝啟動的日期。
1. 在「**預估每日頁面檢視次數**」欄位中，輸入100。 使用此欄位可預估您預計的每日網站頁面檢視次數。 此估計值可讓Adobe配置適當數量的硬體，以處理您要收集的資料。
1. 從下拉式清單中選取&#x200B;**基本貨幣**。 此報表套裝中的所有貨幣資料都會以此貨幣格式轉換和儲存。
1. 按一下「**建立報表**&#x200B;套裝」。 您應該會看到頁面重新整理，並顯示報表套裝已成功建立的訊息。
1. 選取新建立的報表套裝。 導覽至&#x200B;**編輯設定** > **一般** > **一般帳戶設定**。

   ![一般帳戶設定](assets/geographic_settings.png)

   一般帳戶設定

1. 在「一般帳戶設定」螢幕中，啟用&#x200B;**Geography Reporting**，然後按一下&#x200B;**Save.**
1. 導覽至&#x200B;**編輯設定** > **流量** > **流量變數**。
1. 在報表套裝中，設定並啟用下列流量變數。

   * **formName**:最適化表單的識別碼。
   * **formInstance**:適用性表單例項的識別碼。啟用此變數的路徑報表。
   * **fieldName**:最適化表單欄位的識別碼。啟用此變數的路徑報表。
   * **panelName**:最適化表單面板的識別碼。啟用此變數的路徑報表。
   * **formTitle**:表單的標題。
   * **fieldTitle**:表單欄位的標題。
   * **panelTitle**:表單面板的標題。
   * **analytics版本**:表單分析的版本。

1. 導覽至&#x200B;**編輯設定** > **轉換** > **成功事件**。 定義並啟用下列成功事件：

   | 成功事件 | 類型 |
   |---|---|
   | 放棄 | 計數器 |
   | 轉譯 | 計數器 |
   | panelVisit | 計數器 |
   | fieldVisit | 計數器 |
   | 儲存 | 計數器 |
   | 錯誤 | 計數器 |
   | 說明 | 計數器 |
   | 提交 | 計數器 |
   | timeSpent | 數值 |

   >[!NOTE]
   >
   >用來設定AEM Forms analytics的事件編號和prop編號必須與[AEM analytics](/help/sites-administering/adobeanalytics.md)設定中使用的事件編號和prop編號不同。

1. 登出Adobe Marketing Cloud帳戶。

## 建立Cloud Service配置{#creating-cloud-service-configuration}

Cloud Service設定是Adobe Analytics帳戶的相關資訊。 此設定可讓Adobe Experience Manager(AEM)連線至Adobe Analytics。 為您使用的每個Analytics帳戶建立個別的設定。

1. 以管理員身分登入您的AEM製作例項。
1. 在左上角，按一下「**Adobe Experience Manager** > **工具** ![](/help/forms/using/assets/tools.png) > **Cloud Services** > **舊Cloud Services**」。
1. 找到&#x200B;**Adobe Analytics**&#x200B;圖示。 按一下「**顯示配置**」，然後繼續按一下「**[+]**」以添加新配置。

   如果您是首次使用者，請按一下&#x200B;**立即配置**。

1. 將標題新增至新設定（填寫「名稱」欄位為選填）。 例如，我的分析設定。 按一下&#x200B;**建立**。

1. 在設定頁面上開啟「編輯」面板時，請填入下列欄位：

   * **公司**:貴公司的名字在Adobe Analytics上。
   * **使用者名稱**:用來登入Adobe Analytics的名稱。
   * **密碼**:上述帳戶的Adobe Analytics密碼。
   * **資料中心**:Adobe Analytics帳戶的資料中心。

1. 按一下「**連線至Analytics**」。 出現對話方塊，其中顯示連線成功的訊息。 按一下&#x200B;**「確定」**。

## 建立Cloud Service框架{#creating-cloud-service-framework}

Adobe Analytics架構是Adobe Analytics變數和AEM變數之間的一組對應。 使用架構設定表單填入資料至Adobe Analytics報表的方式。 架構與Adobe Analytics設定相關聯。 您可以為每個設定建立多個架構。

1. 在AEM雲端服務主控台上，按一下Adobe Analytics下方的&#x200B;**顯示設定**。
1. 按一下Analytics設定旁的&#x200B;**[+]**&#x200B;連結。

   ![Adobe Analytics組態](assets/adobe-analytics-cloud-services.png)

   Adobe Analytics組態

1. 鍵入框架的&#x200B;**Title**&#x200B;和&#x200B;**Name**，選擇&#x200B;**Adobe Analytics**&#x200B;框架，然後按一下&#x200B;**Create**。 架構隨即開啟供編輯。
1. 在側面Pod的「報表套裝」區段中，按一下「**新增項目**」，然後使用下拉式清單來選取框架將與其互動的報表套裝ID（例如JJEsquire）。
1. 在報表套裝ID旁，選取您要傳送資訊至報表套裝的伺服器例項。

   ![information_to_send_to_report_suite](assets/information_to_send_to_report_suite.png)

1. 從&#x200B;**其他**&#x200B;類別從SideKick拖曳&#x200B;**表單分析元件**&#x200B;至架構。
1. 若要將AEM變數與元件中定義的變數對應，請將變數從Analytics內容尋找器拖曳至追蹤元件上的欄位。

   ![將AEM變數與Adobe Analytics變數對應](assets/analytics_new.png)

1. 使用sidekick中的&#x200B;**page tab**&#x200B;啟動架構，按一下&#x200B;**啟動架構**。

## 設定AEM Forms Analytics設定服務{#configuring-aem-forms-analytics-configuration-service}

1. 在製作執行個體上，開啟位於`https://<server>:<port>;/system/console/configMgr`的AEM Web Console Configuration Manager。
1. 找出並開啟AEM Forms Analytics設定

   ![AEM Forms Analytics設定服務](assets/analytics_configuration.png)

   AEM Forms Analytics設定服務

1. 為下列欄位指定適當的值，然後按一下「**儲存**」。

   * **SiteCatalyst框架**:選取您在「設定追蹤架構」區段中定義的架構/設定。
   * **欄位時間追蹤基線**:指定必須追蹤欄位造訪的持續時間（以秒為單位）。預設值為 0。當值大於0（零）時，會傳送兩個不同的追蹤事件至Adobe Analytics伺服器。 第一個事件會指示Analytics伺服器停止追蹤已退出欄位。 第二個事件會在經過指定的持續時間後傳送。 第二個事件會指示Analytics伺服器開始追蹤已造訪的欄位。 使用兩個不同的事件有助於準確測量欄位逗留時間。 當值為0（零）時，會將單一追蹤事件傳送至Adobe Analytics伺服器。

   * **Analytics報表同步程式**:指定從Adobe Analytics擷取報表的cron運算式。預設值為0 0 2 ?* *.

   * **擷取報表逾時：** 指定等待伺服器回應分析報表的持續時間（以秒為單位）。預設時間為120秒。
   >[!NOTE]
   >
   >逾時報表擷取作業，然後是指定的秒數，最多可能需要10秒。

1. 在發佈例項上重複步驟1至3以設定分析。

現在，您可以啟用表單分析並產生分析報表。

## 啟用表單或文檔{#enabling-analytics-for-a-form-or-document}的分析

1. 在`https://[hostname]:'port'`登入AEM入口網站。
1. 按一下「**Forms > Forms與檔案**」，選取表單或檔案，然後按一下「**啟用Analytics**」。 分析已啟用。

   ![為表單或檔案啟用分析](assets/enable-analytics-1.png)

   為表單啟用分析

   **A.** 啟用Analytics按鈕 **B.選** 取的表單

   如需檢視表單分析報表的詳細資訊，請參閱[檢視及了解AEM Forms分析報表](../../forms/using/view-understand-aem-forms-analytics-reports.md)
