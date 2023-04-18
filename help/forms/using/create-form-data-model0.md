---
title: 「教學課程：在AEM Forms中建立表單資料模型」
description: 建立互動式通訊的表單資料模型
uuid: b56d3dac-be54-4812-b958-38a085686218
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5413fb3-9d50-4f4f-9db8-7e53cd5145d5
docset: aem65
feature: Interactive Communication
exl-id: c8a6037c-46bd-4058-8314-61cb925ba5a8
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '2739'
ht-degree: 0%

---

# 教學課程：在AEM Forms中建立表單資料模型{#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

本教學課程是 [建立您的第一個互動式通訊](/help/forms/using/create-your-first-interactive-communication.md) 系列。 建議您依序依序依序執行系列，以了解、執行和示範完整的教學課程使用案例。

## 關於教學課程 {#about-the-tutorial}

AEM Forms資料整合模組可讓您從不同的後端資料來源建立表單資料模型，例如AEM使用者設定檔、RESTful Web服務、SOAP型Web服務、OData服務和關係資料庫。 您可以在表單資料模型中配置資料模型對象和服務，並將其與最適化表單關聯。 適用性表單欄位會系結至資料模型物件屬性。 這些服務可讓您預填最適化表單，並將提交的表單資料寫回資料模型物件。

如需表單資料整合和表單資料模型的詳細資訊，請參閱 [AEM Forms資料整合](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html).

本教學課程會逐步引導您完成準備、建立、設定表單資料模型，以及將其與互動式通訊建立關聯的步驟。 在本教學課程結束時，您將能夠：

* [設定資料庫](../../forms/using/create-form-data-model0.md#step-set-up-the-database)
* [將MySQL資料庫配置為資料源](../../forms/using/create-form-data-model0.md#step-configure-mysql-database-as-data-source)
* [建立表單資料模型](../../forms/using/create-form-data-model0.md#step-create-form-data-model)
* [設定表單資料模型](../../forms/using/create-form-data-model0.md#step-configure-form-data-model)
* [測試表單資料模型](../../forms/using/create-form-data-model0.md#step-test-form-data-model-and-services)

表單資料模型看起來類似下列：

![表單資料模型](assets/form_data_model_callouts_new.png)

**答：** 已設定的資料來源 **B.** 資料來源結構 **C.** 可用服務 **D.** 資料模型物件 **E.** 配置的服務

## 必備條件 {#prerequisites}

開始之前，請確定您有下列項目：

* MySQL資料庫，包含示例資料，如 [設定資料庫](../../forms/using/create-form-data-model0.md#step-set-up-the-database) 區段。
* MySQL JDBC驅動程式的OSGi捆綁，如 [綁定JDBC資料庫驅動程式](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/jdbc.html#bundling-the-jdbc-database-driver)

## 步驟1:設定資料庫 {#step-set-up-the-database}

資料庫是建立互動式通信的必要條件。 本教學課程使用資料庫來顯示「表單資料模型」和「互動式通訊」的持續性功能。 設定包含客戶、帳單和呼叫表的資料庫。
下圖說明客戶表格的範例資料：

![sample_data_cust](assets/sample_data_cust.png)

使用以下DDL語句建立 **客戶** 表。

```sql
CREATE TABLE `customer` (
   `mobilenum` int(11) NOT NULL,
   `name` varchar(45) NOT NULL,
   `address` varchar(45) NOT NULL,
   `alternatemobilenumber` int(11) DEFAULT NULL,
   `relationshipnumber` int(11) DEFAULT NULL,
   `customerplan` varchar(45) DEFAULT NULL,
   PRIMARY KEY (`mobilenum`),
   UNIQUE KEY `mobilenum_UNIQUE` (`mobilenum`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

使用以下DDL語句建立 **票據** 表。

```sql
CREATE TABLE `bills` (
   `billplan` varchar(45) NOT NULL,
   `latepayment` decimal(4,2) NOT NULL,
   `monthlycharges` decimal(4,2) NOT NULL,
   `billdate` date NOT NULL,
   `billperiod` varchar(45) NOT NULL,
   `prevbal` decimal(4,2) NOT NULL,
   `callcharges` decimal(4,2) NOT NULL,
   `confcallcharges` decimal(4,2) NOT NULL,
   `smscharges` decimal(4,2) NOT NULL,
   `internetcharges` decimal(4,2) NOT NULL,
   `roamingnational` decimal(4,2) NOT NULL,
   `roamingintnl` decimal(4,2) NOT NULL,
   `vas` decimal(4,2) NOT NULL,
   `discounts` decimal(4,2) NOT NULL,
   `tax` decimal(4,2) NOT NULL,
   PRIMARY KEY (`billplan`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

使用以下DDL語句建立 **呼叫** 表。

```sql
CREATE TABLE `calls` (
   `mobilenum` int(11) DEFAULT NULL,
   `calldate` date DEFAULT NULL,
   `calltime` varchar(45) DEFAULT NULL,
   `callnumber` int(11) DEFAULT NULL,
   `callduration` varchar(45) DEFAULT NULL,
   `callcharges` decimal(4,2) DEFAULT NULL,
   `calltype` varchar(45) DEFAULT NULL
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

此 **呼叫** 表格包括呼叫日期、呼叫時間、呼叫號碼、呼叫持續時間和呼叫費用等呼叫詳細資訊。 此 **客戶** 表格會使用行動號碼(mobilenum)欄位連結至呼叫表格。 針對 **客戶** 表格中有多個記錄 **呼叫** 表格。 例如，您可以擷取 **1457892541** 行動號碼(參考 **呼叫** 表格。

此 **票據** 表包括帳單詳細資訊，如帳單日期、帳單期間、月費和通話費。 此 **客戶** 表格已連結至 **票據** 表格（使用「清單計畫」欄位）。 有一個與 **客戶** 表格。 此 **票據** 表包括所有現有計畫的定價詳細資訊。 例如，您可以檢索 **莎拉** 從 **客戶** 表格，並使用這些詳細資訊從中檢索定價詳細資訊 **票據** 表格。

## 步驟2:將MySQL資料庫配置為資料源 {#step-configure-mysql-database-as-data-source}

您可以配置不同類型的資料來源以建立表單資料模型。 在本教程中，您將配置已配置並填入示例資料的MySQL資料庫。 如需其他支援資料來源以及如何設定的相關資訊，請參閱 [AEM Forms資料整合](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html).

執行以下操作來配置MySQL資料庫：

1. 將MySQL資料庫的JDBC驅動程式作為OSGi包安裝：

   1. 以管理員身分登入AEM Forms Author Instance，並前往AEM Web主控台套件組合。 預設URL為 [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).
   1. 點選 **安裝/更新**. 安 **上傳/安裝套件組合** 對話框。

   1. 點選 **選擇檔案** 瀏覽並選擇MySQL JDBC驅動程式OSGi包。 選擇 **開始套件組合** 和 **刷新包**，然後點選 **安裝** 或 **更新**. 確保Oracle公司的MySQL JDBC驅動程式處於活動狀態。 已安裝驅動程式。

1. 將MySQL資料庫配置為資料源：

   1. 前往AEM Web主控台，網址為 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. 找出 **Apache Sling Connection Pooled DataSource** 設定。 點選以在編輯模式中開啟設定。
   1. 在設定對話方塊中，指定下列詳細資料：

      * **資料源名稱：** 您可以指定任何名稱。 例如，指定 **MySQL**.

      * **資料源服務屬性名稱**:指定包含DataSource名稱的服務屬性的名稱。 在將資料源實例註冊為OSGi服務時指定。 例如， **datasource.name**.

      * **JDBC驅動程式類**:指定JDBC驅動程式的Java類名。 對於MySQL資料庫，請指定 **com.mysql.jdbc.driver**.

      * **JDBC連接URI**:指定資料庫的連接URL。 對於在埠3306和方案Teleca上運行的MySQL資料庫，URL為： `jdbc:mysql://'server':3306/teleca?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **用戶名：** 資料庫的用戶名。 需要啟用JDBC驅動程式來建立與資料庫的連接。
      * **密碼：** 資料庫的密碼。 需要啟用JDBC驅動程式來建立與資料庫的連接。
      * **借用時測試：** 啟用 **借閱時測試** 選項。

      * **返回時測試：** 啟用 **返回時測試** 選項。

      * **驗證查詢：** 指定SQL SELECT查詢以驗證池中的連接。 查詢必須至少返回一行。 例如， **選取 &#42; 從客戶**.

      * **事務隔離**:將值設為 **READ_COMMITTED**.
   保留其他屬性為預設 [值](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) 點選 **儲存**.

   系統會建立類似下列的設定。

   ![Apache設定](assets/apache_configuration_new.png)

## 步驟3:建立表單資料模型 {#step-create-form-data-model}

AEM Forms提供直覺式的使用者介面 [建立表單資料模式](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html#main-pars_header_1524967585)l來自已設定的資料來源。 您可以在表單資料模型中使用多個資料來源。 對於本教程中的使用案例，您將使用MySQL作為資料源。

執行下列操作以建立表單資料模型：

1. 在AEM製作例項中，導覽至 **Forms** > **資料整合**.
1. 點選 **建立** > **表單資料模型**.
1. 在「建立表單資料模型」精靈中，指定 **名稱** （表單資料模型）。 例如， **FDM_Create_First_IC**. 點選 **下一個**.
1. 選擇資料源螢幕列出所有配置的資料源。 選擇 **MySQL** 資料來源及點選 **建立**.

   ![MYSQL資料源](assets/fdm_mysql_data_source_new.png)

1. 按一下 **完成**. 此 **FDM_Create_First_IC** 表單資料模型已建立。

## 步驟4:設定表單資料模型 {#step-configure-form-data-model}

配置表單資料模型包括：

* [添加資料模型對象和服務](#add-data-model-objects-and-services)
* [為資料模型對象建立計算子屬性](#create-computed-child-properties-for-data-model-object)
* [添加資料模型對象之間的關聯](#add-associations-between-data-model-objects)
* [編輯資料模型對象屬性](#edit-data-model-object-properties)
* [為資料模型對象配置服務](#configure-services)

### 添加資料模型對象和服務 {#add-data-model-objects-and-services}

1. 在AEM製作例項上，導覽至 **Forms** > **資料整合**. 預設URL為 [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. 此 **FDM_Create_First_IC** 您先前建立的表單資料模型會列在此處。 選取它並點選 **編輯**.

   所選資料源 **MySQL** 會顯示在 **資料來源** 框。

   ![FDM的MYSQL資料源](assets/mysql_fdm_new.png)

1. 展開 **MySQL** 資料源樹。 從中選擇以下資料模型對象和服務 **電影** 方案：

   * **資料模型物件**:

      * 票據
      * 呼叫
      * 客戶
   * **服務:**

      * get
      * 更新

   點選 **添加選定內容** 將所選資料模型對象和服務添加到表單資料模型。

   ![選擇資料模型對象服務](assets/select_data_model_object_services_new.png)

   清單、呼叫和客戶資料模型對象顯示在 **模型** 標籤。 取得和更新服務會顯示在 **服務** 標籤。

   ![資料模型物件](assets/data_model_objects_new.png)

### 為資料模型對象建立計算子屬性 {#create-computed-child-properties-for-data-model-object}

計算屬性是根據規則或表達式計算其值的屬性。 使用規則，可以將計算屬性的值設定為文本字串、數字、數學表達式的結果或窗體資料模型中其他屬性的值。

根據使用案例，建立 **烏薩傑查爾熱** 子計算屬性(在 **票據** 資料模型對象使用以下數學表達式：

* 使用費=呼叫費+電話會議費+簡訊費+移動網際網路費+漫遊國家+漫遊國際+ VAS（所有這些屬性均存在於賬單資料模型對象中）有關 **烏薩傑查爾熱** 子計算屬性，請參見 [規劃互動式通訊](/help/forms/using/planning-interactive-communications.md).

執行以下步驟為清單資料模型對象建立計算子屬性：

1. 選取 **票據** 資料模型物件以加以選取，並點選 **建立子屬性**.
1. 在 **建立子屬性** 窗格：

   1. 輸入 **烏薩傑查爾熱** 作為子屬性的名稱。
   1. 啟用 **計算**.
   1. 選擇 **浮點數** 作為類型並點選 **完成** 將子屬性添加到 **票據** 資料模型物件。

   ![建立子屬性](assets/create_child_property_new.png)

1. 點選 **編輯規則** 來開啟規則編輯器。
1. 點選 **建立**. 此 **設定值** 規則視窗開啟。
1. 從「選取選項」下拉式清單中，選取 **數學表達式**.

   ![使用費規則編輯器](assets/usage_charges_rule_editor_new.png)

1. 在數學表達式中，選擇 **呼叫費** 和 **concallcarches** 分別作為第一和第二對象。 選擇 **plus** 作為運算子。 在數學表達式中點選並點選 **擴充運算式** 新增 **smcharges**, **internetcargeins**, **羅明尼亞**, **羅明寧**，和 **vas** 對象。

   下圖描述規則編輯器中的數學表達式：

   ![使用費規則](assets/usage_charges_rule_all_new.png)

1. 點選 **完成**. 規則會在規則編輯器中建立。
1. 點選 **關閉** 來關閉「規則編輯器」窗口。

### 添加資料模型對象之間的關聯 {#add-associations-between-data-model-objects}

定義資料模型對象後，可以在它們之間建立關聯。 關聯可以是一對一或一對多。 例如，可以有多個與員工相關聯的家屬。 它稱為一對多關聯，在連接相關資料模型對象的線上以1:n表示。 但是，如果關聯為指定的員工ID返回唯一的員工名稱，則稱為一對一關聯。

將資料源中的關聯資料模型對象添加到表單資料模型時，它們的關聯將被保留並顯示為通過箭頭線連接。

根據使用案例，在資料模型物件之間建立下列關聯：

| 關聯 | 資料模型物件 |
|---|---|
| 1:n | customer:calls（可以在每月帳單中與一個客戶關聯多個呼叫） |
| 1:1 | 客戶：帳單（某個特定月的一個帳單與客戶關聯） |

執行以下步驟以建立資料模型對象之間的關聯：

1. 選取 **客戶** 資料模型物件以加以選取，並點選 **添加關聯**. 此 **添加關聯** 屬性窗格隨即開啟。
1. 在 **添加關聯** 窗格：

   * 指定關聯的標題。 此為選用欄位。
   * 選擇 **一對多** 從 **類型** 下拉式清單。

   * 選擇 **呼叫** 從 **模型物件** 下拉式清單。

   * 選擇 **get** 從 **服務** 下拉式清單。

   * 點選 **新增** 連結 **客戶** 資料模型對象 **呼叫** 使用屬性的資料模型物件。 根據使用案例，呼叫資料模型物件必須連結至客戶資料模型物件中的行動電話號碼屬性。 此 **新增引數** 對話框。

   ![添加關聯](assets/add_association_new.png)

1. 在 **新增引數** 對話框：

   * 選擇 **mobilenum** 從 **名稱** 下拉式清單。 行動編號屬性是客戶和呼叫資料模型物件中可用的通用屬性。 因此，它可用來建立客戶與呼叫資料模型物件之間的關聯。
對於客戶資料模型物件中可用的每個行動電話號碼，呼叫表格中有多個可用的呼叫記錄。

   * 指定引數的選用標題和說明。
   * 選擇 **客戶** 從 **綁定到** 下拉式清單。

   * 選擇 **mobilenum** 從 **綁定值** 下拉式清單。

   * 點選 **新增**.

   ![為引數新增關聯](assets/add_association_argument_new.png)

   mobilenum屬性會顯示在 **引數** 區段。

   ![添加參數關聯](assets/add_argument_association_new.png)

1. 點選 **完成** 在客戶和呼叫資料模型物件之間建立1:n關聯。

   在建立客戶和調用資料模型對象之間的關聯後，在客戶和清單資料模型對象之間建立1:1的關聯。

1. 選取 **客戶** 資料模型物件以加以選取，並點選 **添加關聯**. 此 **添加關聯** 屬性窗格隨即開啟。
1. 在 **添加關聯** 窗格：

   * 指定關聯的標題。 此為選用欄位。
   * 選擇 **一對一** 從 **類型** 下拉式清單。

   * 選擇 **票據** 從 **模型物件** 下拉式清單。

   * 選擇 **get** 從 **服務** 下拉式清單。 此 **計費計畫** 屬性是清單表的主鍵，已在 **引數** 區段。
清單和客戶資料模型對象分別使用開單計畫（清單）和客戶計畫（客戶）屬性進行連結。 在這些屬性之間建立綁定，以檢索MySQL資料庫中任何可用客戶的計畫詳細資訊。

   * 選擇 **客戶** 從 **綁定到** 下拉式清單。

   * 選擇 **customerplan** 從 **綁定值** 下拉式清單。

   * 點選 **完成** 在計費計畫和客戶計畫屬性之間建立綁定。

   ![添加客戶帳單的關聯](assets/add_association_customer_bills_new.png)

   下圖描述了資料模型對象與用於建立它們之間關聯的屬性之間的關聯：

   ![fdm_associations](assets/fdm_associations.gif)

### 編輯資料模型對象屬性 {#edit-data-model-object-properties}

在建立客戶與其他資料模型對象之間的關聯後，編輯客戶屬性以定義基於其從資料模型對象中檢索資料的屬性。 根據使用案例，行動電話號碼會作為屬性，用於從客戶資料模型物件擷取資料。

1. 選取 **客戶** 資料模型物件以加以選取，並點選 **編輯屬性**. 此 **編輯屬性** 窗格。
1. 指定 **客戶** 作為 **頂級模型對象**.
1. 選擇 **get** 從 **讀取服務** 下拉式清單。
1. 在 **引數** 小節：

   * 選擇 **請求屬性** 從 **綁定到** 下拉式清單。

   * 指定 **mobilenum** 作為捆綁值。

1. 選擇 **更新** 從 **寫入** 服務下拉式清單。
1. 在 **引數** 小節：

   * 針對 **mobilenum** 屬性，選擇 **客戶** 從 **綁定到** 下拉式清單。

   * 選擇 **mobilenum** 從 **綁定值** 下拉式清單。

1. 點選 **完成** 以儲存屬性。

   ![配置服務](assets/configure_services_customer_new.png)

1. 選取 **呼叫** 資料模型物件以加以選取，並點選 **編輯屬性**. 此 **編輯屬性** 窗格。
1. 停用 **頂級模型對象** for **呼叫** 資料模型物件。
1. 點選 **完成**.

   重複步驟8 - 10以配置 **票據** 資料模型物件。

### 配置服務 {#configure-services}

1. 前往 **服務** 標籤。
1. 選取 **get** 服務與點選 **編輯屬性**. 此 **編輯屬性** 窗格。
1. 在 **編輯屬性** 窗格：

   * 輸入可選標題和說明。
   * 選擇 **客戶** 從 **輸出模型對象** 下拉式清單。

   * 點選 **完成** 以儲存屬性。

   ![編輯屬性](assets/edit_properties_get_details_new.png)

1. 選取 **更新** 服務與點選 **編輯屬性**. 此 **編輯屬性** 窗格。
1. 在 **編輯屬性** 窗格：

   * 輸入可選標題和說明。
   * 選擇 **客戶** 從 **輸入模型對象** 下拉式清單。

   * 點選 **完成**.
   * 點選 **儲存** 保存表單資料模型。

   ![更新服務屬性](assets/update_service_properties_new.png)

## 步驟5:測試表單資料模型與服務 {#step-test-form-data-model-and-services}

您可以測試資料模型物件和服務，以驗證表單資料模型是否已正確設定。

執行下列操作以運行測試：

1. 前往 **模型** 頁簽，選擇 **客戶** 資料模型物件，並點選 **測試模型對象**.
1. 在 **測試表單資料模型** 窗口，選擇 **讀取模型對象** 從 **選擇模型/服務** 下拉式清單。
1. 在 **輸入** 區段，指定 **mobilenum** 在配置的MySQL資料庫中存在的屬性，然後點選 **測試**.

   與指定的mobilenum屬性相關聯的客戶詳細資訊會擷取並顯示在「輸出」區段中，如下所示。 關閉對話框。

   ![測試資料模型](assets/test_data_model_new.png)

1. 前往 **服務** 標籤。
1. 選取 **get** 服務與點選 **測試服務。**
1. 在 **輸入** 區段，指定 **mobilenum** 在配置的MySQL資料庫中存在的屬性，然後點選 **測試**.

   與指定的mobilenum屬性相關聯的客戶詳細資訊會擷取並顯示在「輸出」區段中，如下所示。 關閉對話框。

   ![測試服務](assets/test_service_new.png)

### 編輯和儲存範例資料 {#edit-and-save-sample-data}

表單資料模型編輯器可讓您為表單資料模型中的所有資料模型物件屬性產生範例資料，包括計算屬性。 這是一組符合為每個屬性設定的資料類型的隨機值。 您也可以編輯和儲存資料，即使重新產生範例資料，資料也會保留。

執行下列操作以生成、編輯和保存示例資料：

1. 在表單資料模型頁面上，點選 **編輯範例資料**. 它會在「編輯範例資料」視窗中產生並顯示範例資料。

   ![編輯範例資料](assets/edit_sample_data_new.png)

1. 在 **編輯範例資料** 視需要，編輯資料，然後點選 **儲存**. 關窗。
