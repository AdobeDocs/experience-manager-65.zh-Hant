---
title: 「教學課程：建立表單資料模型"
seo-title: 建立表單資料模型教學課程
description: 建立表單資料模型
seo-description: 建立表單資料模型
uuid: b9d2bb1b-90f0-44f4-b1e3-0603cdf5f5b8
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 12e6c325-ace0-4a57-8ed4-6f7ceee23099
docset: aem65
translation-type: tm+mt
source-git-commit: 78768e6eab65f452421d8809384500c6eab6b97f
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 1%

---


# 教學課程：建立表單資料模型{#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

本教程是[建立第一個自適應表單](../../forms/using/create-your-first-adaptive-form.md)系列中的一個步驟。 建議依序依序依序排列，以瞭解、執行和展示完整的教學課程使用案例。

## 關於教學課程{#about-the-tutorial}

AEM [!DNL Forms]資料整合模組可讓您從不同的後端資料來源建立表單資料模型，例如AEM使用者設定檔、REST風格的Web服務、SOAP架構的Web服務、OData服務和關係式資料庫。 您可以在表單資料模型中配置資料模型對象和服務，並將其與自適應表單關聯。 最適化表單欄位會系結至資料模型物件屬性。 這些服務可讓您預先填寫最適化表單，並將提交的表單資料寫回資料模型物件。

如需表單資料整合與表單資料模型的詳細資訊，請參閱[AEM Forms Data Integration](../../forms/using/data-integration.md)。

本教學課程將逐步帶您準備、建立、設定表單資料模型，並將表單資料模型與最適化表單建立關聯。 在本教學課程結束時，您將能夠：

* [將MySQL資料庫配置為資料源](#config-database)
* [使用MySQL資料庫建立表單資料模型](#create-fdm)
* [設定表單資料模型](#config-fdm)
* [測試表單資料模型](#test-fdm)

表單資料模型看起來類似下列：

![form-data-model-l](assets/form-data-model_l.png)

**A.** Configured data sources  **B.** Data sources結構 **C.** Available services  **D.** D. **** Dobjects configured E.E.D.D.D.D.D.D.D.Services服務

## 必備條件 {#prerequisites}

開始之前，請確定您有下列項目：

* [!DNL MySQL] 資料庫，其示例資料如建立第一個自適應表單的「必 [備條件」部分中所述](../../forms/using/create-your-first-adaptive-form.md)
* [捆綁JDBC資料庫驅動程式](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)中介紹的[!DNL MySQL] JDBC驅動程式的OSGi捆綁包
* 如第一個教程[中所述的自適應表單建立自適應表單](/help/forms/using/create-adaptive-form.md)

## 步驟1:將MySQL資料庫配置為資料源{#config-database}

您可以設定不同類型的資料來源以建立表單資料模型。 在本教程中，我們將配置您配置的MySQL資料庫，並用示例資料填充該資料庫。 如需其他支援資料來源的詳細資訊以及如何設定這些資料來源，請參閱[AEM Forms Data Integration](../../forms/using/data-integration.md)。

執行下列操作以配置[!DNL MySQL]資料庫：

1. 將[!DNL MySQL]資料庫的JDBC驅動程式作為OSGi包安裝：

   1. 以管理員身分登入「AEM [!DNL Forms]作者例項」，並前往AEM網頁主控台組合。 預設URL為[https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles)。

   1. 點選&#x200B;**[!UICONTROL 安裝／更新]**。 出現[!UICONTROL 上傳／安裝包]對話框。

   1. 點選&#x200B;**[!UICONTROL 選擇檔案]**&#x200B;以瀏覽並選擇[!DNL MySQL] JDBC驅動程式OSGi包。 選擇&#x200B;**[!UICONTROL 啟動Bundle]**&#x200B;和&#x200B;**[!UICONTROL 重新整理套件]**，然後點選&#x200B;**[!UICONTROL 安裝或更新]**。 確保[!DNL MySQL]的[!DNL Oracle Corporation's] JDBC驅動程式處於活動狀態。 已安裝驅動程式。

1. 將[!DNL MySQL]資料庫配置為資料源：

   1. 前往[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)的AEM網頁主控台。
   1. 找到&#x200B;**Apache Sling Connection Pooled DataSource**&#x200B;組態。 點選以在編輯模式中開啟設定。
   1. 在設定對話方塊中，指定下列詳細資訊：

      * **資料來源名稱：** 您可以指定任何名稱。例如，指定&#x200B;**WeRetailMySQL**。
      * **DataSource服務屬性名稱**:指定包含DataSource名稱的服務屬性名稱。在將資料源實例註冊為OSGi服務時指定。 例如，**datasource.name**。
      * **JDBC驅動程式類**:指定JDBC驅動程式的Java類名。對於[!DNL MySQL]資料庫，請指定&#x200B;**com.mysql.jdbc.Driver**。
      * **JDBC連接URI**:指定資料庫的連線URL。對於在埠3306和模式weretail上運行的[!DNL MySQL]資料庫，URL為：`jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **用戶名：** 資料庫的用戶名。必須啟用JDBC驅動程式才能與資料庫建立連接。
      * **密碼：** 資料庫的密碼。必須啟用JDBC驅動程式才能與資料庫建立連接。
      * **借閱時測試：** 啟用 **[!UICONTROL Test on]** Borrow選項。
      * **Test on Return:** Enable the  **[!UICONTROL Test on]** Returnoption.
      * **驗證查詢：** 指定SQL SELECT查詢以驗證池中的連接。查詢至少必須返回一行。 例如，**從customerdetails**&#x200B;中選擇*。
      * **事務隔離**:將值設定為 **READ_COMMITTED**。

         將其他屬性保留為預設值[值](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html)並點選&#x200B;**[!UICONTROL 保存]**。

         系統會建立類似下列的設定。

         ![關係——資料庫——資料源——配置](assets/relational-database-data-source-configuration.png)

## 步驟2:建立表單資料模型{#create-fdm}

AEM [!DNL Forms]提供直覺式使用者介面，以從設定的資料來源建立表單資料模型](data-integration.md)。 [您可以在表單資料模型中使用多個資料來源。 對於我們的使用案例，我們將使用已配置的[!DNL MySQL]資料源。

執行下列動作以建立表單資料模型：

1. 在AEM作者例項中，導覽至&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Data Integrations]**。
1. 點選「**[!UICONTROL 建立]** > **[!UICONTROL 表單資料模型]**」。
1. 在「建立表單資料模型」對話框中，為表單資料模型指定&#x200B;**name**。 例如，**customer-shipping-billing-details**。 點選&#x200B;**[!UICONTROL Next]**。
1. 選取資料來源畫面會列出所有已設定的資料來源。 選擇&#x200B;**WeRetailMySQL**&#x200B;資料源並按一下&#x200B;**[!UICONTROL 建立]**。

   ![資料源選擇](assets/data-source-selection.png)

建立&#x200B;**customer-shipping-billing-details**&#x200B;表單資料模型。

## 步驟3:配置表單資料模型{#config-fdm}

配置表單資料模型涉及：

* 添加資料模型對象和服務
* 為資料模型對象配置讀寫服務

執行下列動作以設定表單資料模型：

1. 在AEM作者例項上，導覽至&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Data Integrations]**。 預設URL為[https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm)。
1. 此處列出您先前建立的&#x200B;**customer-shipping-billing-details**&#x200B;表單資料模型。 在編輯模式中開啟。

   選定的資料源&#x200B;**WeRetailMySQL**&#x200B;以表單資料模型配置。

   ![default-fdm](assets/default-fdm.png)

1. 展開WeRailMySQL資料源樹。 從&#x200B;**weretail** > **customerdetails**&#x200B;模式選擇以下資料模型對象和服務以形成資料模型：

   * **資料模型物件**:

      * id
      * 名稱
      * shippingAddress
      * 城市
      * 狀態
      * zipcode
   * **服務:**

      * get
      * 更新

   點選「**新增選取的**」，將選取的資料模型物件和服務新增至表單資料模型。

   ![WeRetail架構](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >JDBC資料來源的預設get、update和insert服務是隨附表單資料模型的現成可用功能。

1. 為資料模型對象配置讀和寫服務。

   1. 選擇&#x200B;**customerdetails**&#x200B;資料模型對象，然後按一下&#x200B;**[!UICONTROL 編輯屬性]**。
   1. 從「讀取服務」下拉式清單中選擇&#x200B;**[!UICONTROL get]**。 會自動添加&#x200B;**id**&#x200B;引數，該引數是customerdetails資料模型對象中的主鍵。 點選![aem_6_3_edit](assets/aem_6_3_edit.png)並依如下方式設定引數。

      ![read-default](assets/read-default.png)

   1. 同樣，選擇&#x200B;**[!UICONTROL update]**&#x200B;作為寫服務。 **customerdetails**&#x200B;物件會自動新增為引數。 參數的配置如下。

      ![write-default](assets/write-default.png)

      按如下方式添加和配置&#x200B;**id**&#x200B;參數。

      ![id-arg](assets/id-arg.png)

   1. 點選&#x200B;**[!UICONTROL Done]**&#x200B;以儲存資料模型物件屬性。 然後，點選「**[!UICONTROL 儲存]**」以儲存表單資料模型。

      **[!UICONTROL get]**&#x200B;和&#x200B;**[!UICONTROL update]**&#x200B;服務被添加為資料模型對象的預設服務。

      ![資料模型——對象](assets/data-model-object.png)

1. 前往&#x200B;**[!UICONTROL Services]**&#x200B;標籤，並設定&#x200B;**[!UICONTROL get]**&#x200B;和&#x200B;**[!UICONTROL update]**&#x200B;服務。

   1. 選擇&#x200B;**[!UICONTROL get]**&#x200B;服務，然後點選&#x200B;**[!UICONTROL 編輯屬性]**。 屬性對話框開啟。
   1. 在「編輯屬性」對話方塊中指定下列項目：

      * **標題**:指定服務的標題。例如：檢索發運地址。
      * **說明**:指定包含服務詳細功能的說明。例如：

         此服務從[!DNL MySQL]資料庫中檢索發運地址和其他客戶詳細資訊

      * **輸出模型對象**:選擇包含客戶資料的結構。例如：

         customerdetail架構

      * **返回陣列**:停用 **Return** Arrayoption。
      * **引數**:選擇名為 **ID的參數**。

      點選&#x200B;**[!UICONTROL Done]**。 已配置從MySQL資料庫檢索客戶詳細資訊的服務。

      ![Shiiping-address-retrieval](assets/shiiping-address-retrieval.png)

   1. 選擇&#x200B;**[!UICONTROL update]**&#x200B;服務並點選&#x200B;**[!UICONTROL 編輯屬性]**。 屬性對話框開啟。

   1. 在[!UICONTROL 編輯屬性]對話方塊中指定下列項目：

      * **標題**:指定服務的標題。例如，更新發運地址。
      * **說明**:指定包含服務詳細功能的說明。例如：

         此服務會更新MySQL資料庫中的送貨地址和相關欄位

      * **輸入模型物件**:選擇包含客戶資料的結構。例如：

         customerdetail架構

      * **輸出類型**:選擇 **布爾**。

      * **引數**:選擇名為 **** ID和 **customerdetails的參數**。
      點選&#x200B;**[!UICONTROL Done]**。 **[!UICONTROL update]**&#x200B;服務用於更新[!DNL MySQL]資料庫中的客戶詳細資訊。

      ![shiiping-address-update](assets/shiiping-address-update.png)



配置表單資料模型對象和服務。 您現在可以測試表單資料模型。

## 步驟4:測試表單資料模型{#test-fdm}

您可以測試資料模型物件和服務，以驗證表單資料模型已正確設定。

執行下列動作以執行測試：

1. 轉至&#x200B;**[!UICONTROL Model]**&#x200B;標籤，選擇&#x200B;**customerdetails**&#x200B;資料模型物件，並點選&#x200B;**[!UICONTROL Test Model Object]**。
1. 在[!UICONTROL Test Model/Service]窗口中，從&#x200B;**[!UICONTROL Select Model/Service]**&#x200B;下拉式清單中選擇&#x200B;**[!UICONTROL Read model object]**。
1. 在&#x200B;**customerdetails**&#x200B;區段中，為&#x200B;**id**&#x200B;參數指定值，該參數存在於已配置的[!DNL MySQL]資料庫中，然後點選&#x200B;**[!UICONTROL Test]**。

   與指定ID相關的客戶詳細資訊將被提取並顯示在&#x200B;**[!UICONTROL Output]**&#x200B;部分中，如下所示。

   ![測試讀模型](assets/test-read-model.png)

1. 同樣地，您也可以測試Write模型對象和服務。

   在以下示例中，更新服務成功更新資料庫中id 7102715的地址詳細資訊。

   ![測試——寫模型](assets/test-write-model.png)

   現在，如果您再次測試id 7107215的讀取型號服務，它會擷取並顯示更新的客戶詳細資訊，如下所示。

   ![read-updated](assets/read-updated.png)
