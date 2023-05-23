---
title: 配置分析和報告
seo-title: Configuring analytics and reports
description: 瞭解如何配置Adobe Analytics以發現用戶在使用自適應表單、自適應文檔和HTML5表單時遇到的交互模式和問題。
seo-description: Learn how to configure Adobe Analytics to discover interaction patterns and problems users face while using adaptive forms, adaptive documents, and HTML5 forms.
uuid: ac5d1300-f303-40e8-a33e-4859a54ac10d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 96a77980-4213-4779-a540-00905ea8f7e3
docset: aem65
exl-id: 72f0f8e3-e70b-4f78-aa0e-b31768b536f7
source-git-commit: 66631fd0813f623f3321072fc00fd90f7fa33d21
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 3%

---

# 使用Cloud Service框架的分析 {#analyticsusingcloudframework}

AEM Forms與Analytics整合，使您能夠捕獲和跟蹤已發佈表單和文檔的效能指標。 分析這些指標背後的目標是根據有關使表單或文件更有用所需的變更資料做出明智的決策。

>[!NOTE]
>
>AEM Forms的分析功能是AEM Forms附加軟體包的一部分。 有關安裝附加軟體包的資訊，請參見 [安裝和配置AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md)。
>
>除了附加包外，您還需要對實例具有Adobe Analytics帳戶和管理員AEM權限。 有關解決方案的資訊，請參見 [Adobe Analytics](https://www.adobe.com/solutions/digital-analytics.html)。

您也可以使用Adobe啟動執行分析。 有關如何將AEM Forms與Adobe產品發佈整合的詳細資訊，請參見 [使用Adobe啟動的分析](/help/forms/using/integrate-aem-forms-with-adobe-analytics.md)。

## 概觀 {#overview}

您可以使用Adobe Analytics來發現用戶在使用自適應表單、HTML5表單和互動式通信時遇到的交互模式和問題。 現成Adobe分析跟蹤並儲存有關以下參數的資訊：

* **平均填充時間**:填表所花的平均時間。
* **格式副本**:開啟窗體的次數。
* **草稿**:表單在草稿狀態中保存的次數。
* **提交**:提交表單的次數。
* **中止**:用戶在未完成表單的情況下離開的次數。

可以自定義Adobe Analytics以添加/刪除更多參數。 除上述資訊外，該報告還包含有關HTML5和自適應表單的每個面板的以下資訊：

* **時間**:在面板和面板欄位上花費的時間。
* **錯誤**:在面板和面板欄位上遇到的錯誤數。
* **幫助**:用戶開啟面板幫助和面板欄位的次數。

## 建立報表套件 {#creating-report-suite}

分析資料儲存在稱為報告套件的客戶特定儲存庫中。 要建立報表套件並使用Adobe Analytics，您必須具有有效的Adobe Marketing Cloud帳戶。 在執行以下步驟之前，請確保您有有效的Adobe Marketing Cloud帳戶。

執行以下步驟建立報表套件。

1. 登錄時間： [https://sc.omniture.com/login/](https://sc.omniture.com/login/)
1. 在Marketing Cloud中，選擇 **管理** > **Admin Console** > **報表套件**。
1. 選擇 **新建** > **報表套件** 的子菜單。

   ![新建報表套件](assets/newreportsuite_new.png)

   新建報表套件

1. 確保第一個下拉清單設定為 **從模板建立** ，然後選擇 **商業**。
1. 查找 **報表套件ID** 並添加新的報表套件ID。 例如，JJEsquire。 報告套件ID顯示在「報告套件ID」欄位下。 它包括一個自動前置詞，通常是公司名稱。
1. 添加新 **網站標題**。 例如，JJEsquire入門套件。 此標題在分析UI中使用。 在代碼中使用報表套件ID。
1. 選擇 **時區** 的下界。 此報告套件中的所有資料都基於定義的時區進行記錄。
1. 離開 **基本URL** 和 **預設頁** 欄位為空。 這兩個值僅從Adobe Marketing Cloud介面用於連結到您的網站。
1. 離開 **開始即時日期** 定在今天。 「開始使用日期」確定激活報告套件的日期。
1. 在 **每天估計的頁面視圖** 鍵入100。 使用此欄位估計您每天為網站預期的頁面視圖數。 此估計允許Adobe部署適當數量的硬體來處理要收集的資料。
1. 選擇 **基本貨幣** 的下界。 此報告套件中的所有貨幣資料都將以此貨幣格式轉換和儲存。
1. 按一下 **建立報告** 套房。 您應看到頁面刷新，並顯示報告套件已成功建立的消息。
1. 選擇新建立的報告套件。 導航到 **編輯設定** > **常規** > **常規帳戶設定**。

   ![常規帳戶設定](assets/geographic_settings.png)

   常規帳戶設定

1. 在「常規帳戶設定」螢幕中，啟用 **地理位置報告**，然後按一下 **保存。**
1. 導航到 **編輯設定** > **流量** > **流量變數**。
1. 在報告套件中，配置並啟用以下通信變數。

   * **表單名稱**:自適應表單的標識符。
   * **窗體實例**:自適應窗體實例的標識符。 為此變數啟用路徑報告。
   * **欄位名稱**:自適應表單域的標識符。 為此變數啟用路徑報告。
   * **面板名稱**:自適應窗體面板的標識符。 為此變數啟用路徑報告。
   * **窗體標題**:窗體的標題。
   * **欄位標題**:窗體欄位的標題。
   * **面板標題**:窗體面板的標題。
   * **analytics版本**:窗體分析的版本。

1. 導航到 **編輯設定** > **轉換** > **成功事件**。 定義並啟用以下成功事件：

   | 成功事件 | 類型 |
   |---|---|
   | 放棄 | 計數器 |
   | 呈現 | 計數器 |
   | 面板訪問 | 計數器 |
   | 欄位訪問 | 計數器 |
   | 保存 | 計數器 |
   | 錯誤 | 計數器 |
   | 說明 | 計數器 |
   | 提交 | 計數器 |
   | 已用時間 | 數值 |

   >[!NOTE]
   >
   >用於配置AEM Forms分析的事件編號和道理編號必須與中使用的事件編號和道理編號不同 [AEM分析](/help/sites-administering/adobeanalytics.md) 配置。

1. 註銷Adobe Marketing Cloud帳戶。

## 建立Cloud Service配置 {#creating-cloud-service-configuration}

Cloud Service配置是有關Adobe Analytics帳戶的資訊。 該配置使Adobe Experience Manager(AEM)能夠連接到Adobe Analytics。 為您使用的每個分析帳戶建立單獨的配置。

1. 以管理員身AEM份登錄到作者實例。
1. 在左上角，按一下 **Adobe Experience Manager** > **工具** ![](/help/forms/using/assets/tools.png) > **Cloud Services** > **舊Cloud Services**。
1. 定位 **Adobe Analytics** 表徵圖 按一下 **顯示配置** 然後繼續按一下 **[+]** 添加新配置。

   如果您是首次用戶，請按一下 **立即配置**。

1. 將標題添加到新配置（填寫「名稱」欄位是可選的）。 例如，「我的分析」配置。 按一下&#x200B;**建立**。

1. 當「編輯」面板在配置頁面上開啟時，填寫以下欄位：

   * **公司**:你公司的名字在Adobe Analytics。
   * **用戶名**:用於登錄到Adobe Analytics的名稱。
   * **密碼**:上述帳戶的Adobe Analytics密碼。
   * **資料中心**:您的Adobe Analytics帳戶的資料中心。

1. 按一下 **連接到分析**。 出現一個對話框，其中顯示連接成功的消息。 按一下&#x200B;**「確定」**。

## 建立Cloud Service框架 {#creating-cloud-service-framework}

Adobe Analytics框架是Adobe Analytics變數和變數之間的一組映AEM射。 使用框架配置表單如何將資料填充到Adobe Analytics報表。 框架與Adobe Analytics配置相關。 可為每個配置建立多個框架。

1. 在AEM雲服務控制台上，按一下 **顯示配置**&#x200B;在Adobe Analytics。
1. 按一下 **[+]** 連結到「分析」配置旁邊。

   ![Adobe Analytics配置](assets/adobe-analytics-cloud-services.png)

   Adobe Analytics配置

1. 鍵入 **標題** 和 **名稱** 對於框架，選擇 **Adobe Analytics** 框架，然後按一下 **建立**。 該框架將開啟以進行編輯。
1. 在側麵包的「報告套件」部分，按一下 **添加項**，然後使用下拉框選擇框架與之交互的Report Suite ID（例如JJEsquire）。
1. 在報告套件ID旁，選擇要向報告套件發送資訊的伺服器實例。

   ![資訊_發送_發送_報告_套件](assets/information_to_send_to_report_suite.png)

1. 拖動 **窗體分析元件** 從 **其他** 從SideKick到框架。
1. 要將分析變數與元件中定義的變數映射，請將一個變數從AEMContent Finder拖到跟蹤元件上的欄位上。

   ![用Adobe AnalyticsAEM變數映射變數](assets/analytics_new.png)

1. 使用 **頁** 在旁邊按一下 **激活框架**。

## 配置AEM Forms分析配置服務 {#configuring-aem-forms-analytics-configuration-service}

1. 在作者實例中，開啟AEMWeb Console Configuration Manager，位於 `https://<server>:<port>;/system/console/configMgr`。
1. 查找並開啟AEM Forms分析配置

   ![AEM Forms分析配置服務](assets/analytics_configuration.png)

   AEM Forms分析配置服務

1. 為以下欄位指定相應的值，然後按一下 **保存**。

   * **SiteCatalyst框架**:選擇在設定跟蹤框架部分中定義的框架/配置。
   * **欄位時間跟蹤基線**:指定跟蹤欄位訪問的持續時間（以秒為單位）。 預設值為 0。當值大於0（零）時，兩個單獨的跟蹤事件將發送到Adobe Analytics伺服器。 第一個事件指示分析伺服器停止跟蹤退出的欄位。 第二個事件在經過指定持續時間後發送。 第二個事件指示分析伺服器開始跟蹤訪問的欄位。 使用兩個單獨的事件有助於準確測量在欄位上花費的時間。 當值為0（零）時，單個跟蹤事件將發送到Adobe Analytics伺服器。

   * **分析報表同步cron**:指定用於從Adobe Analytics提取報告的cron表達式。 預設值為0 0 2 ? &#42; &#42;。

   * **提取報告超時：** 指定等待伺服器響應分析報告的持續時間（秒）。 預設時間為120秒。
   >[!NOTE]
   >
   >超時報告提取操作和指定的秒數可能需要多10秒。

1. 在發佈實例上重複步驟1-3以配置分析。

現在，您可以啟用表單分析並生成分析報告。

## 為表單或文檔啟用分析 {#enabling-analytics-for-a-form-or-document}

1. 登錄到AEM門戶 `https://[hostname]:'port'`。
1. 按一下 **Forms>Forms和文檔**，然後按一下 **啟用分析**。 已啟用分析。

   ![為表單或文檔啟用分析](assets/enable-analytics-1.png)

   啟用窗體分析

   **答：** 啟用分析按鈕 **B** 選定窗體

   有關查看表單分析報表的詳細資訊，請參閱 [查看和瞭解AEM Forms分析報告](../../forms/using/view-understand-aem-forms-analytics-reports.md)。
