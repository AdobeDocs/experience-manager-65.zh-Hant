---
title: 「教學課程：建立表單資料模型「
seo-title: Create Form Data Model Tutorial
description: 建立表單資料模型
seo-description: Create form data model
uuid: b9d2bb1b-90f0-44f4-b1e3-0603cdf5f5b8
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 12e6c325-ace0-4a57-8ed4-6f7ceee23099
docset: aem65
exl-id: 40bc5af6-9023-437e-95b0-f85d3df7d8aa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1421'
ht-degree: 1%

---

# 教學課程：建立表單資料模型 {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

本教學課程是 [建立第一個最適化表單](../../forms/using/create-your-first-adaptive-form.md) 系列。 建議您依序依序依序執行系列，以了解、執行和示範完整的教學課程使用案例。

## 關於教學課程 {#about-the-tutorial}

AEM [!DNL Forms] 資料整合模組允許您從不同的後端資料源(如AEM用戶配置檔案、RESTful Web服務、基於SOAP的Web服務、OData服務和關係資料庫)建立表單資料模型。 您可以在表單資料模型中配置資料模型對象和服務，並將其與最適化表單關聯。 適用性表單欄位會系結至資料模型物件屬性。 這些服務可讓您預填最適化表單，並將提交的表單資料寫回資料模型物件。

如需表單資料整合和表單資料模型的詳細資訊，請參閱 [AEM Forms資料整合](../../forms/using/data-integration.md).

本教學課程會逐步引導您完成準備、建立、設定表單資料模型與最適化表單的相關步驟。 在本教學課程結束時，您將能夠：

* [將MySQL資料庫配置為資料源](#config-database)
* [使用MySQL資料庫建立表單資料模型](#create-fdm)
* [設定表單資料模型](#config-fdm)
* [測試表單資料模型](#test-fdm)

表單資料模型看起來類似下列：

![form-data-model_l](assets/form-data-model_l.png)

**答：** 已設定的資料來源 **B.** 資料來源結構 **C.** 可用服務 **D.** 資料模型物件 **E.** 配置的服務

## 必備條件 {#prerequisites}

開始之前，請確定您有下列項目：

* [!DNL MySQL] 資料庫，如 [建立第一個最適化表單](../../forms/using/create-your-first-adaptive-form.md)
* 用於的OSGi捆綁 [!DNL MySQL] JDBC驅動程式，如 [綁定JDBC資料庫驅動程式](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)
* 第一個教學課程中說明的最適化表單 [建立最適化表單](/help/forms/using/create-adaptive-form.md)

## 步驟1:將MySQL資料庫配置為資料源 {#config-database}

您可以配置不同類型的資料來源以建立表單資料模型。 在本教程中，我們將配置您配置的MySQL資料庫並填入示例資料。 如需其他支援資料來源以及如何設定的相關資訊，請參閱 [AEM Forms資料整合](../../forms/using/data-integration.md).

請執行下列動作來設定 [!DNL MySQL] 資料庫：

1. 為安裝JDBC驅動程式 [!DNL MySQL] 資料庫作為OSGi捆綁包：

   1. 登入AEM [!DNL Forms] 以管理員身分製作執行個體，並前往AEM Web主控台套件組合。 預設URL為 [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).

   1. 點選 **[!UICONTROL 安裝/更新]**. 安 [!UICONTROL 上傳/安裝套件組合] 對話框。

   1. 點選 **[!UICONTROL 選擇檔案]** 瀏覽並選取 [!DNL MySQL] JDBC驅動程式OSGi捆綁包。 選擇 **[!UICONTROL 開始套件組合]** 和 **[!UICONTROL 刷新包]**，然後點選 **[!UICONTROL 安裝或更新]**. 確保 [!DNL Oracle Corporation's] JDBC驅動程式 [!DNL MySQL] 活動。 已安裝驅動程式。

1. 設定 [!DNL MySQL] 資料庫作為資料源：

   1. 前往AEM Web主控台，網址為 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. 找出 **Apache Sling Connection Pooled DataSource** 設定。 點選以在編輯模式中開啟設定。
   1. 在設定對話方塊中，指定下列詳細資料：

      * **資料源名稱：** 您可以指定任何名稱。 例如，指定 **WeRetailMySQL**.
      * **資料源服務屬性名稱**:指定包含DataSource名稱的服務屬性的名稱。 在將資料源實例註冊為OSGi服務時指定。 例如， **datasource.name**.
      * **JDBC驅動程式類**:指定JDBC驅動程式的Java類名。 針對 [!DNL MySQL] 資料庫，指定 **com.mysql.jdbc.driver**.
      * **JDBC連接URI**:指定資料庫的連接URL。 針對 [!DNL MySQL] 在埠3306和架構weretail上運行的資料庫，URL為： `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **用戶名：** 資料庫的用戶名。 需要啟用JDBC驅動程式來建立與資料庫的連接。
      * **密碼：** 資料庫的密碼。 需要啟用JDBC驅動程式來建立與資料庫的連接。
      * **借用時測試：** 啟用 **[!UICONTROL 借閱時測試]** 選項。
      * **返回時測試：** 啟用 **[!UICONTROL 返回時測試]** 選項。
      * **驗證查詢：** 指定SQL SELECT查詢以驗證池中的連接。 查詢必須至少返回一行。 例如， **選取 &#42; 來自customerdetails**.
      * **事務隔離**:將值設為 **READ_COMMITTED**.

         保留其他屬性為預設 [值](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) 點選 **[!UICONTROL 儲存]**.

         系統會建立類似下列的設定。

         ![relational-database-data-source-configuration](assets/relational-database-data-source-configuration.png)

## 步驟2:建立表單資料模型 {#create-fdm}

AEM [!DNL Forms] 提供直觀的使用者介面 [建立表單資料模型](data-integration.md) 從設定的資料來源。 您可以在表單資料模型中使用多個資料來源。 針對我們的使用案例，我們將使用已設定的 [!DNL MySQL] 資料來源。

執行下列操作以建立表單資料模型：

1. 在AEM製作例項中，導覽至 **[!UICONTROL Forms]** > **[!UICONTROL 資料整合]**.
1. 點選 **[!UICONTROL 建立]** > **[!UICONTROL 表單資料模型]**.
1. 在「建立表單資料模型」對話方塊中，指定 **名稱** （表單資料模型）。 例如， **customer-shipping-billing-details**. 點選 **[!UICONTROL 下一個]**.
1. 選擇資料源螢幕列出所有配置的資料源。 選擇 **WeRetailMySQL** 資料來源及點選 **[!UICONTROL 建立]**.

   ![資料源選擇](assets/data-source-selection.png)

此 **customer-shipping-billing-details** 表單資料模型已建立。

## 步驟3:設定表單資料模型 {#config-fdm}

配置表單資料模型涉及：

* 添加資料模型對象和服務
* 配置資料模型對象的讀寫服務

執行下列操作來配置表單資料模型：

1. 在AEM製作例項上，導覽至 **[!UICONTROL Forms]** > **[!UICONTROL 資料整合]**. 預設URL為 [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. 此 **customer-shipping-billing-details** 您先前建立的表單資料模型會列在此處。 在編輯模式中開啟它。

   所選資料源 **WeRetailMySQL** 是在表單資料模型中設定。

   ![default-fdm](assets/default-fdm.png)

1. 展開WeRailMySQL資料源樹。 從中選擇以下資料模型對象和服務 **weretail** > **customerdetails** 表單資料模型的結構：

   * **資料模型物件**:

      * id
      * 名稱
      * shippingAddress
      * 城市
      * 狀態
      * 郵遞區號
   * **服務:**

      * get
      * 更新

   點選 **添加選定內容** 將所選資料模型對象和服務添加到表單資料模型。

   ![WeRetail結構](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >JDBC資料源的預設獲取、更新和插入服務是隨表單資料模型提供的。

1. 為資料模型對象配置讀寫服務。

   1. 選取 **customerdetails** 資料模型物件及點選 **[!UICONTROL 編輯屬性]**.
   1. 選擇 **[!UICONTROL get]** 從「讀取服務」下拉式清單中。 此 **id** 引數，即customerdetails資料模型物件中的主要索引鍵會自動新增。 點選 ![aem_6_3_edit](assets/aem_6_3_edit.png) 並依下列方式設定引數。

      ![read-default](assets/read-default.png)

   1. 同樣地，請選取 **[!UICONTROL 更新]** 作為寫入服務。 此 **customerdetails** 物件會自動新增為引數。 引數的設定如下。

      ![write-default](assets/write-default.png)

      新增及設定 **id** 引數，如下所示。

      ![id-arg](assets/id-arg.png)

   1. 點選 **[!UICONTROL 完成]** 保存資料模型對象屬性。 然後，點選 **[!UICONTROL 儲存]** 保存表單資料模型。

      此 **[!UICONTROL get]** 和 **[!UICONTROL 更新]** 服務會新增為資料模型物件的預設服務。

      ![data-model-object](assets/data-model-object.png)

1. 前往 **[!UICONTROL 服務]** 標籤和設定 **[!UICONTROL get]** 和 **[!UICONTROL 更新]** 服務。

   1. 選取 **[!UICONTROL get]** 服務與點選 **[!UICONTROL 編輯屬性]**. 屬性對話框開啟。
   1. 在「編輯屬性」對話方塊中指定下列項目：

      * **標題**:指定服務的標題。 例如：檢索發運地址。
      * **說明**:指定包含服務詳細功能的說明。 例如：

         此服務會從中檢索發運地址和其他客戶詳細資訊 [!DNL MySQL] 資料庫

      * **輸出模型對象**:選取包含客戶資料的結構。 例如：

         customerdetail結構

      * **傳回陣列**:停用 **傳回陣列** 選項。
      * **引數**:選擇名為的參數 **ID**.

      點選 **[!UICONTROL 完成]**. 已配置從MySQL資料庫檢索客戶詳細資訊的服務。

      ![shiiping-address-retrieval](assets/shiiping-address-retrieval.png)

   1. 選取 **[!UICONTROL 更新]** 服務與點選 **[!UICONTROL 編輯屬性]**. 屬性對話框開啟。

   1. 在 [!UICONTROL 編輯屬性] 對話框：

      * **標題**:指定服務的標題。 例如，更新發運地址。
      * **說明**:指定包含服務詳細功能的說明。 例如：

         此服務更新MySQL資料庫中的發運地址和相關欄位

      * **輸入模型對象**:選取包含客戶資料的結構。 例如：

         customerdetail結構

      * **輸出類型**:選擇 **布林值**.

      * **引數**:選擇名為的參數 **ID** 和 **customerdetails**.
      點選 **[!UICONTROL 完成]**. 此 **[!UICONTROL 更新]** 更新客戶詳細資訊的服務，請參閱 [!DNL MySQL] 資料庫已配置。

      ![shiiping-address-update](assets/shiiping-address-update.png)



配置表單資料模型中的資料模型對象和服務。 您現在可以測試表單資料模型。

## 步驟4:測試表單資料模型 {#test-fdm}

您可以測試資料模型物件和服務，以驗證表單資料模型是否已正確設定。

執行下列操作以運行測試：

1. 前往 **[!UICONTROL 模型]** 頁簽，選擇 **customerdetails** 資料模型物件，並點選 **[!UICONTROL 測試模型對象]**.
1. 在 [!UICONTROL 測試模型/服務] 窗口，選擇 **[!UICONTROL 讀取模型對象]** 從 **[!UICONTROL 選擇模型/服務]** 下拉式清單。
1. 在 **customerdetails** 區段，指定 **id** 已配置的參數中存在的參數 [!DNL MySQL] 資料庫和點選 **[!UICONTROL 測試]**.

   系統會擷取與指定ID相關聯的客戶詳細資料，並顯示在 **[!UICONTROL 輸出]** 區段，如下所示。

   ![測試讀取模型](assets/test-read-model.png)

1. 同樣，您也可以測試寫入模型物件和服務。

   在以下示例中，更新服務成功更新了資料庫中ID 7102715的地址詳細資訊。

   ![測試 — 寫模型](assets/test-write-model.png)

   現在，如果您再次測試id 7107215的讀取模型服務，它將擷取並顯示更新後的客戶詳細資料，如下所示。

   ![已更新](assets/read-updated.png)
