---
title: 「教學課程：建立表單資料模型「
seo-title: 建立表單資料模型教學課程
description: 建立表單資料模型
seo-description: 建立表單資料模型
uuid: b9d2bb1b-90f0-44f4-b1e3-0603cdf5f5b8
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 12e6c325-ace0-4a57-8ed4-6f7ceee23099
docset: aem65
exl-id: 40bc5af6-9023-437e-95b0-f85d3df7d8aa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 1%

---

# 教學課程：建立表單資料模型{#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

本教學課程是[建立第一個最適化表單](../../forms/using/create-your-first-adaptive-form.md)系列中的步驟。 建議您依序依序依序執行系列，以了解、執行和示範完整的教學課程使用案例。

## 關於教學課程{#about-the-tutorial}

AEM [!DNL Forms]資料整合模組可讓您從不同的後端資料來源建立表單資料模型，例如AEM使用者設定檔、RESTful Web服務、SOAP型Web服務、OData服務和關係資料庫。 您可以在表單資料模型中配置資料模型對象和服務，並將其與最適化表單關聯。 適用性表單欄位會系結至資料模型物件屬性。 這些服務可讓您預填最適化表單，並將提交的表單資料寫回資料模型物件。

如需表單資料整合與表單資料模型的詳細資訊，請參閱[AEM Forms資料整合](../../forms/using/data-integration.md)。

本教學課程會逐步引導您完成準備、建立、設定表單資料模型與最適化表單的相關步驟。 在本教學課程結束時，您將能夠：

* [將MySQL資料庫配置為資料源](#config-database)
* [使用MySQL資料庫建立表單資料模型](#create-fdm)
* [設定表單資料模型](#config-fdm)
* [測試表單資料模型](#test-fdm)

表單資料模型看起來類似下列：

![form-data-model_l](assets/form-data-model_l.png)

**A.** 設定的資 **料來源B.** 資料來源結 **構C.** 可用服務 **D.** 資料模型物件 **E.** 設定的服務

## 必備條件 {#prerequisites}

開始之前，請確定您有下列項目：

* [!DNL MySQL] 資料庫，如建立第一個最適化表單的「必要條件」 [一節中所述，含有範例資料](../../forms/using/create-your-first-adaptive-form.md)
* [綁定JDBC資料庫驅動程式](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)中所述[!DNL MySQL] JDBC驅動程式的OSGi綁定
* 如第一個教學課程[建立最適化表單](/help/forms/using/create-adaptive-form.md)中所述

## 步驟1:將MySQL資料庫配置為資料源{#config-database}

您可以配置不同類型的資料來源以建立表單資料模型。 在本教程中，我們將配置您配置的MySQL資料庫並填入示例資料。 如需其他支援資料來源的相關資訊及如何設定，請參閱[AEM Forms資料整合](../../forms/using/data-integration.md)。

執行以下操作來配置[!DNL MySQL]資料庫：

1. 將[!DNL MySQL]資料庫的JDBC驅動程式作為OSGi包安裝：

   1. 以管理員身分登入AEM [!DNL Forms]製作執行個體，並前往AEM Web主控台套件組合。 預設URL為[https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles)。

   1. 點選&#x200B;**[!UICONTROL 安裝/更新]**。 此時將顯示[!UICONTROL 上載/安裝套件組合]對話框。

   1. 點選&#x200B;**[!UICONTROL 選擇檔案]**&#x200B;以瀏覽並選擇[!DNL MySQL] JDBC驅動程式OSGi捆綁包。 選擇「**[!UICONTROL 啟動套件組合]**」和「**[!UICONTROL 刷新套件]**」，然後點選「**[!UICONTROL 安裝或更新]**」。 確保[!DNL MySQL]的[!DNL Oracle Corporation's] JDBC驅動程式處於活動狀態。 已安裝驅動程式。

1. 將[!DNL MySQL]資料庫配置為資料源：

   1. 前往AEM Web主控台，網址為[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
   1. 找出&#x200B;**Apache Sling Connection Pooled DataSource**&#x200B;設定。 點選以在編輯模式中開啟設定。
   1. 在設定對話方塊中，指定下列詳細資料：

      * **資料來源名稱：** 您可以指定任何名稱。例如，指定&#x200B;**WeRetailMySQL**。
      * **資料源服務屬性名稱**:指定包含DataSource名稱的服務屬性的名稱。在將資料源實例註冊為OSGi服務時指定。 例如， **資料源.name**。
      * **JDBC驅動程式類**:指定JDBC驅動程式的Java類名。對於[!DNL MySQL]資料庫，請指定&#x200B;**com.mysql.jdbc.Driver**。
      * **JDBC連接URI**:指定資料庫的連接URL。對於在埠3306和架構weretail上運行的[!DNL MySQL]資料庫，URL為：`jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **用戶名：** 資料庫的用戶名。需要啟用JDBC驅動程式來建立與資料庫的連接。
      * **密碼：** 資料庫的密碼。需要啟用JDBC驅動程式來建立與資料庫的連接。
      * **借貸時測試：** 啟用「借 **[!UICONTROL 貸時測]** 試」選項。
      * **傳回時測試：** 啟用傳 **[!UICONTROL 回時測]** 試。
      * **驗證查詢：** 指定SQL SELECT查詢以驗證池中的連接。查詢必須至少返回一行。 例如， **從customerdetails**&#x200B;中選擇*。
      * **事務隔離**:將值設定為 **READ_COMMITTED**。

         保留其他屬性，其預設值為[values](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html)，然後點選&#x200B;**[!UICONTROL Save]**。

         系統會建立類似下列的設定。

         ![relational-database-data-source-configuration](assets/relational-database-data-source-configuration.png)

## 步驟2:建立表單資料模型{#create-fdm}

AEM [!DNL Forms]提供直觀的用戶介面，用於從配置的資料源建立表單資料模型](data-integration.md)。 [您可以在表單資料模型中使用多個資料來源。 對於我們的使用案例，我們將使用配置的[!DNL MySQL]資料源。

執行下列操作以建立表單資料模型：

1. 在AEM製作例項中，導覽至&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 資料整合]**。
1. 點選「**[!UICONTROL 建立]** > **[!UICONTROL 表單資料模型]**」。
1. 在「建立表單資料模型」對話方塊中，為表單資料模型指定&#x200B;**名稱**。 例如， **customer-shipping-billing-details**。 點選&#x200B;**[!UICONTROL Next]**。
1. 選擇資料源螢幕列出所有配置的資料源。 選擇&#x200B;**WeRetailMySQL**&#x200B;資料源並點選&#x200B;**[!UICONTROL Create]**。

   ![資料源選擇](assets/data-source-selection.png)

已建立&#x200B;**customer-shipping-billing-details**&#x200B;表單資料模型。

## 步驟3:配置表單資料模型{#config-fdm}

配置表單資料模型涉及：

* 添加資料模型對象和服務
* 配置資料模型對象的讀寫服務

執行下列操作來配置表單資料模型：

1. 在AEM製作例項上，導覽至&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 資料整合]**。 預設URL為[https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm)。
1. 您先前建立的&#x200B;**customer-shipping-billing-details**&#x200B;表單資料模型列於此處。 在編輯模式中開啟它。

   所選資料源&#x200B;**WeRetailMySQL**&#x200B;是在表單資料模型中配置的。

   ![default-fdm](assets/default-fdm.png)

1. 展開WeRailMySQL資料源樹。 從&#x200B;**weretail** > **customerdetails**&#x200B;架構中選擇以下資料模型對象和服務以形成資料模型：

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

   點選「**新增選取的** 」，將選取的資料模型物件和服務新增至表單資料模型。

   ![WeRetail結構](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >JDBC資料源的預設獲取、更新和插入服務是隨表單資料模型提供的。

1. 為資料模型對象配置讀寫服務。

   1. 選擇&#x200B;**customerdetails**&#x200B;資料模型對象，然後點選&#x200B;**[!UICONTROL Edit Properties]**。
   1. 從「讀取服務」下拉清單中選擇&#x200B;**[!UICONTROL get]**。 系統會自動新增&#x200B;**id**&#x200B;引數，該引數是customerdetails資料模型物件中的主要索引鍵。 點選![aem_6_3_edit](assets/aem_6_3_edit.png)並依下列方式設定引數。

      ![read-default](assets/read-default.png)

   1. 同樣，選擇&#x200B;**[!UICONTROL update]**&#x200B;作為寫入服務。 會自動將&#x200B;**customerdetails**&#x200B;物件新增為引數。 引數的設定如下。

      ![write-default](assets/write-default.png)

      新增並設定&#x200B;**id**&#x200B;引數，如下所示。

      ![id-arg](assets/id-arg.png)

   1. 點選&#x200B;**[!UICONTROL Done]**&#x200B;以儲存資料模型物件屬性。 然後，點選&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存表單資料模型。

      將&#x200B;**[!UICONTROL get]**&#x200B;和&#x200B;**[!UICONTROL update]**&#x200B;服務新增為資料模型物件的預設服務。

      ![data-model-object](assets/data-model-object.png)

1. 前往&#x200B;**[!UICONTROL Services]**&#x200B;標籤，並設定&#x200B;**[!UICONTROL get]**&#x200B;和&#x200B;**[!UICONTROL update]**&#x200B;服務。

   1. 選取&#x200B;**[!UICONTROL get]**&#x200B;服務，然後點選&#x200B;**[!UICONTROL 編輯屬性]**。 屬性對話框開啟。
   1. 在「編輯屬性」對話方塊中指定下列項目：

      * **標題**:指定服務的標題。例如：檢索發運地址。
      * **說明**:指定包含服務詳細功能的說明。例如：

         此服務從[!DNL MySQL]資料庫中檢索發運地址和其他客戶詳細資訊

      * **輸出模型物件**:選取包含客戶資料的結構。例如：

         customerdetail結構

      * **傳回陣列**:停用「傳 **回** 陣列」選項。
      * **引數**:選取名為 **ID**&#x200B;的引數。

      點選&#x200B;**[!UICONTROL Done]**。 已配置從MySQL資料庫檢索客戶詳細資訊的服務。

      ![shiiping-address-retrieval](assets/shiiping-address-retrieval.png)

   1. 選擇&#x200B;**[!UICONTROL update]**&#x200B;服務，然後點選&#x200B;**[!UICONTROL Edit Properties]**。 屬性對話框開啟。

   1. 在[!UICONTROL 編輯屬性]對話方塊中指定下列項目：

      * **標題**:指定服務的標題。例如，更新發運地址。
      * **說明**:指定包含服務詳細功能的說明。例如：

         此服務更新MySQL資料庫中的發運地址和相關欄位

      * **輸入模型物件**:選取包含客戶資料的結構。例如：

         customerdetail結構

      * **輸出類型**:選取 **布林值**。

      * **引數**:選取名為ID **** 和customerdetails **的引數**。
      點選&#x200B;**[!UICONTROL Done]**。 已配置&#x200B;**[!UICONTROL update]**&#x200B;服務以更新[!DNL MySQL]資料庫中的客戶詳細資訊。

      ![shiiping-address-update](assets/shiiping-address-update.png)



配置表單資料模型中的資料模型對象和服務。 您現在可以測試表單資料模型。

## 步驟4:測試表單資料模型{#test-fdm}

您可以測試資料模型物件和服務，以驗證表單資料模型是否已正確設定。

執行下列操作以運行測試：

1. 轉至&#x200B;**[!UICONTROL Model]**&#x200B;頁簽，選擇&#x200B;**customerdetails**&#x200B;資料模型對象，然後點選&#x200B;**[!UICONTROL Test Model Object]**。
1. 在[!UICONTROL 測試模型/服務]窗口中，從&#x200B;**[!UICONTROL 選擇模型/服務]**&#x200B;下拉清單中選擇&#x200B;**[!UICONTROL 讀取模型對象]**。
1. 在&#x200B;**customerdetails**&#x200B;部分中，為配置的[!DNL MySQL]資料庫中存在的&#x200B;**id**&#x200B;參數指定值，然後點選&#x200B;**[!UICONTROL Test]**。

   與指定ID相關聯的客戶詳細資訊會擷取並顯示在&#x200B;**[!UICONTROL Output]**&#x200B;區段中，如下所示。

   ![測試讀取模型](assets/test-read-model.png)

1. 同樣，您也可以測試寫入模型物件和服務。

   在以下示例中，更新服務成功更新了資料庫中ID 7102715的地址詳細資訊。

   ![測試 — 寫模型](assets/test-write-model.png)

   現在，如果您再次測試id 7107215的讀取模型服務，它將擷取並顯示更新後的客戶詳細資料，如下所示。

   ![已更新](assets/read-updated.png)
