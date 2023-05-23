---
title: 「教程：在AEM Forms建立表單資料模型」
description: 為交互通信建立表單資料模型
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

# 教程：在AEM Forms建立表單資料模型{#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

本教程是 [建立您的第一個互動式通信](/help/forms/using/create-your-first-interactive-communication.md) 的下界。 建議按時間順序按系列進行操作，以瞭解、執行和演示完整的教程使用案例。

## 關於教程 {#about-the-tutorial}

AEM Forms資料整合模組允許您從不同的後端資料源(如AEM用戶配置檔案、REST風格的Web服務、基於SOAP的Web服務、OData服務和關係資料庫)建立表單資料模型。 可以在表單資料模型中配置資料模型對象和服務，並將其與自適應表單關聯。 自適應表單域綁定到資料模型對象屬性。 這些服務使您能夠預填自適應表單並將提交的表單資料寫回資料模型對象。

有關表單資料整合和表單資料模型的詳細資訊，請參見 [AEM Forms資料整合](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html)。

本教程將指導您完成準備、建立、配置表單資料模型以及將表單資料模型與互動式通信關聯的步驟。 在本教程的結束時，您將能夠：

* [設定資料庫](../../forms/using/create-form-data-model0.md#step-set-up-the-database)
* [將MySQL資料庫配置為資料源](../../forms/using/create-form-data-model0.md#step-configure-mysql-database-as-data-source)
* [建立表單資料模型](../../forms/using/create-form-data-model0.md#step-create-form-data-model)
* [配置表單資料模型](../../forms/using/create-form-data-model0.md#step-configure-form-data-model)
* [Test表單資料模型](../../forms/using/create-form-data-model0.md#step-test-form-data-model-and-services)

表單資料模型類似於以下內容：

![窗體資料模型](assets/form_data_model_callouts_new.png)

**答：** 已配置資料源 **B** 資料源架構 **C.** 可用服務 **D** 資料模型對象 **E.** 已配置的服務

## 必備條件 {#prerequisites}

在開始之前，請確保具備以下功能：

* MySQL資料庫，其示例資料如 [設定資料庫](../../forms/using/create-form-data-model0.md#step-set-up-the-database) 的子菜單。
* MySQL JDBC驅動程式的OSGi捆綁包，如中所述 [捆綁JDBC資料庫驅動程式](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/jdbc.html#bundling-the-jdbc-database-driver)

## 步驟1:設定資料庫 {#step-set-up-the-database}

資料庫是建立互動式通信的關鍵。 本教程使用資料庫來顯示Interactive Communications的表單資料模型和持久性功能。 設定包含客戶、帳單和呼叫表的資料庫。
下圖說明了客戶表的示例資料：

![示例_data_cust](assets/sample_data_cust.png)

使用以下DDL語句建立 **客戶** 表格。

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

使用以下DDL語句建立 **票據** 表格。

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

使用以下DDL語句建立 **呼叫** 表格。

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

的 **呼叫** 表包括呼叫詳細資訊，如呼叫日期、呼叫時間、呼叫號碼、呼叫持續時間和呼叫費用。 的 **客戶** 表使用「移動號碼」(mobilenum)欄位連結到呼叫表。 對於列在 **客戶** 表中有多個記錄 **呼叫** 的子菜單。 例如，您可以檢索 **1457892541** 通過引用 **呼叫** 的子菜單。

的 **票據** 表包括帳單詳細資訊，如帳單日期、帳單期間、每月費用和呼叫費用。 的 **客戶** 表連結到 **票據** 表。 有一個計畫與中的每個客戶關聯 **客戶** 的子菜單。 的 **票據** 表包括所有現有計畫的定價詳細資訊。 例如，您可以檢索計畫詳細資訊 **莎拉** 從 **客戶** 並使用這些詳細資訊從中檢索定價詳細資訊 **票據** 的子菜單。

## 步驟2:將MySQL資料庫配置為資料源 {#step-configure-mysql-database-as-data-source}

可以配置不同類型的資料源以建立表單資料模型。 在本教程中，您將配置已配置並填充示例資料的MySQL資料庫。 有關其他受支援的資料源以及如何配置它們的資訊，請參見 [AEM Forms資料整合](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html)。

執行以下操作以配置MySQL資料庫：

1. 將MySQL資料庫的JDBC驅動程式作為OSGi包安裝：

   1. 以管理員身份登錄到AEM Forms作者實例，然後轉AEM到Web控制台捆綁包。 預設URL為 [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles)。
   1. 點擊 **安裝/更新**。 安 **上傳/安裝捆綁包** 對話框。

   1. 點擊 **選擇檔案** 瀏覽並選擇MySQL JDBC驅動程式OSGi包。 選擇 **啟動包** 和 **刷新包**，然後點擊 **安裝** 或 **更新**。 確保Oracle公司的MySQL JDBC驅動程式處於活動狀態。 已安裝驅動程式。

1. 將MySQL資料庫配置為資料源：

   1. 轉到AEMWeb控制台 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
   1. 定位 **Apache Sling連接池化資料源** 配置。 按一下以在編輯模式下開啟配置。
   1. 在配置對話框中，指定以下詳細資訊：

      * **資料源名稱：** 可以指定任何名稱。 例如，指定 **MySQL**。

      * **DataSource服務屬性名稱**:指定包含資料源名稱的服務屬性的名稱。 將資料源實例註冊為OSGi服務時指定。 比如說， **datasource.name**。

      * **JDBC驅動程式類**:指定JDBC驅動程式的Java類名。 對於MySQL資料庫，請指定 **com.mysql.jdbc.驅動程式**。

      * **JDBC連接URI**:指定資料庫的連接URL。 對於在埠3306和架構teleca上運行的MySQL資料庫，URL為： `jdbc:mysql://'server':3306/teleca?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **用戶名：** 資料庫的用戶名。 需要啟用JDBC驅動程式來與資料庫建立連接。
      * **密碼：** 資料庫的口令。 需要啟用JDBC驅動程式來與資料庫建立連接。
      * **Test借用：** 啟用 **Test借用** 的雙曲餘切值。

      * **Test返回：** 啟用 **Test返回** 的雙曲餘切值。

      * **驗證查詢：** 指定SQL SELECT查詢以驗證池中的連接。 查詢必須至少返回一行。 比如說， **選擇 &#42; 從客戶**。

      * **事務隔離**:將值設定為 **已提交讀取**。
   保留其他屬性為預設 [值](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) 點擊 **保存**。

   將建立與以下類似的配置。

   ![Apache配置](assets/apache_configuration_new.png)

## 第3步：建立表單資料模型 {#step-create-form-data-model}

AEM Forms提供直觀的用戶介面 [建立表單資料模式](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html#main-pars_header_1524967585)l來自已配置的資料源。 可以在表單資料模型中使用多個資料源。 對於本教程中的用例，您將使用MySQL作為資料源。

執行以下操作以建立表單資料模型：

1. 在作AEM者實例中，導航到 **Forms** > **資料整合**。
1. 點擊 **建立** > **窗體資料模型**。
1. 在「建立表單資料模型」嚮導中，指定 **名稱** 的子菜單。 比如說， **FDM_Create_First_IC**。 點擊 **下一個**。
1. 「選擇資料源」螢幕列出所有已配置的資料源。 選擇 **MySQL** 資料源和分路 **建立**。

   ![MYSQL資料源](assets/fdm_mysql_data_source_new.png)

1. 按一下 **完成**。 的 **FDM_Create_First_IC** 建立窗體資料模型。

## 第4步：配置表單資料模型 {#step-configure-form-data-model}

配置表單資料模型包括：

* [添加資料模型對象和服務](#add-data-model-objects-and-services)
* [建立資料模型對象的計算子屬性](#create-computed-child-properties-for-data-model-object)
* [添加資料模型對象之間的關聯](#add-associations-between-data-model-objects)
* [編輯資料模型對象屬性](#edit-data-model-object-properties)
* [為資料模型對象配置服務](#configure-services)

### 添加資料模型對象和服務 {#add-data-model-objects-and-services}

1. 在作AEM者實例上，導航至 **Forms** > **資料整合**。 預設URL為 [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm)。
1. 的 **FDM_Create_First_IC** 此處列出了您以前建立的表單資料模型。 選擇它並點擊 **編輯**。

   所選資料源 **MySQL** 中 **資料源** 的子菜單。

   ![FDM的MYSQL資料源](assets/mysql_fdm_new.png)

1. 展開 **MySQL** 資料源樹。 從中選擇以下資料模型對象和服務 **電視** 架構：

   * **資料模型對象**:

      * 票據
      * 呼叫
      * 客戶
   * **服務:**

      * 得
      * 更新

   點擊 **添加選定項** 將所選資料模型對象和服務添加到表單資料模型。

   ![選擇資料模型對象服務](assets/select_data_model_object_services_new.png)

   清單、呼叫和客戶資料模型對象顯示在右側窗格中 **模型** 頁籤。 獲取和更新服務顯示在 **服務** 頁籤。

   ![資料模型對象](assets/data_model_objects_new.png)

### 為資料模型對象建立計算子屬性 {#create-computed-child-properties-for-data-model-object}

computed屬性是基於規則或表達式計算其值的屬性。 使用規則，可以將計算屬性的值設定為文本字串、數字、數學表達式的結果或窗體資料模型中另一個屬性的值。

根據使用案例，建立 **烏薩傑查爾** 子計算屬性 **票據** 資料模型對象使用以下數學表達式：

* 使用費=呼叫費+電話會議費+ SMS費+移動網際網路費+漫遊國家+漫遊國際+ VAS（所有這些屬性都存在於票據資料模型對象中）有關 **烏薩傑查爾** 子計算屬性，請參見 [規劃互動式通信](/help/forms/using/planning-interactive-communications.md)。

執行以下步驟為清單資料模型對象建立計算子屬性：

1. 選中位於 **票據** 資料模型對象選擇並點擊 **建立子屬性**。
1. 在 **建立子屬性** 窗格：

   1. 輸入 **烏薩傑查爾** 作為子屬性的名稱。
   1. 啟用 **計算**。
   1. 選擇 **浮動** 鍵入和點擊 **完成** 將子屬性添加到 **票據** 資料模型對象。

   ![建立子屬性](assets/create_child_property_new.png)

1. 點擊 **編輯規則** 開啟規則編輯器。
1. 點擊 **建立**。 的 **設定值** 的下界。
1. 從「選擇選項」(Select Option)下拉清單中，選擇 **數學表達式**。

   ![使用費用規則編輯器](assets/usage_charges_rule_editor_new.png)

1. 在數學表達式中，選擇 **催繳費** 和 **指控** 分別作為第一及第二對象。 選擇 **加** 作為運算子。 在數學表達式中點擊並點擊 **擴展表達式** 添加 **smc費用**。 **網際網路收費**。 **羅阿曼族**。 **羅曼寧**, **增值服務** 對象。

   下圖描述了規則編輯器中的數學表達式：

   ![使用費用規則](assets/usage_charges_rule_all_new.png)

1. 點擊 **完成**。 規則將在規則編輯器中建立。
1. 點擊 **關閉** 按鈕。

### 添加資料模型對象之間的關聯 {#add-associations-between-data-model-objects}

定義資料模型對象後，可在它們之間建立關聯。 關聯可以是一對一或一對多。 例如，可以有多個與員工關聯的家屬。 它稱為一對多關聯，在連接相關資料模型對象的線上以1:n表示。 但是，如果關聯為給定的員工ID返回唯一的員工名稱，則它稱為一對一關聯。

將資料源中的關聯資料模型對象添加到表單資料模型時，它們的關聯將保留並顯示為通過箭頭線連接。

根據使用案例，在資料模型對象之間建立以下關聯：

| 關聯 | 資料模型對象 |
|---|---|
| 1:n | 客戶：呼叫（在每月帳單中可以將多個呼叫與客戶關聯） |
| 1:1 | 客戶：帳單（一個帳單與某個特定月份的客戶關聯） |

執行以下步驟以建立資料模型對象之間的關聯：

1. 選中位於 **客戶** 資料模型對象選擇並點擊 **添加關聯**。 的 **添加關聯** 屬性窗格。
1. 在 **添加關聯** 窗格：

   * 指定關聯的標題。 它是一個可選欄位。
   * 選擇 **一對多** 從 **類型** 的子菜單。

   * 選擇 **呼叫** 從 **模型對象** 的子菜單。

   * 選擇 **得** 從 **服務** 的子菜單。

   * 點擊 **添加** 連結 **客戶** 資料模型對象 **呼叫** 使用屬性的資料模型對象。 根據使用情況，調用資料模型對象必須連結到客戶資料模型對象中的移動號碼屬性。 的 **添加參數** 對話框。

   ![添加關聯](assets/add_association_new.png)

1. 在 **添加參數** 對話框：

   * 選擇 **移動枚舉** 從 **名稱** 的子菜單。 移動號碼屬性是客戶和調用資料模型對象中可用的公用屬性。 結果，它用於在客戶和調用資料模型對象之間建立關聯。
對於客戶資料模型對象中可用的每個移動號碼，呼叫表中有多個可用呼叫記錄。

   * 指定參數的可選標題和說明。
   * 選擇 **客戶** 從 **綁定到** 的子菜單。

   * 選擇 **移動枚舉** 從 **綁定值** 的子菜單。

   * 點擊 **添加**。

   ![為參數添加關聯](assets/add_association_argument_new.png)

   mobilenum屬性顯示在 **參數** 的子菜單。

   ![添加參數關聯](assets/add_argument_association_new.png)

1. 點擊 **完成** 建立客戶和調用資料模型對象之間的1:n關聯。

   在客戶和調用資料模型對象之間建立關聯後，請在客戶和清單資料模型對象之間建立1:1關聯。

1. 選中位於 **客戶** 資料模型對象選擇並點擊 **添加關聯**。 的 **添加關聯** 屬性窗格。
1. 在 **添加關聯** 窗格：

   * 指定關聯的標題。 它是一個可選欄位。
   * 選擇 **一對一** 從 **類型** 的子菜單。

   * 選擇 **票據** 從 **模型對象** 的子菜單。

   * 選擇 **得** 從 **服務** 的子菜單。 的 **計費計畫** 屬性（是清單表的主鍵）已在 **參數** 的子菜單。
清單和客戶資料模型對象分別使用開單計畫（清單）和客戶計畫（客戶）屬性進行連結。 在這些屬性之間建立綁定，以檢索MySQL資料庫中任何可用客戶的計畫詳細資訊。

   * 選擇 **客戶** 從 **綁定到** 的子菜單。

   * 選擇 **客戶計畫** 從 **綁定值** 的子菜單。

   * 點擊 **完成** 在billplan和customerplan屬性之間建立綁定。

   ![添加客戶帳單的關聯](assets/add_association_customer_bills_new.png)

   下圖描述了資料模型對象與用於建立它們之間關聯的屬性之間的關聯：

   ![fdm_associations](assets/fdm_associations.gif)

### 編輯資料模型對象屬性 {#edit-data-model-object-properties}

在建立客戶與其他資料模型對象之間的關聯後，編輯客戶屬性以定義從資料模型對象檢索資料的屬性。 根據使用案例，使用移動號碼作為屬性從客戶資料模型對象檢索資料。

1. 選中位於 **客戶** 資料模型對象選擇並點擊 **編輯屬性**。 的 **編輯屬性** 的子菜單。
1. 指定 **客戶** 的 **頂級模型對象**。
1. 選擇 **得** 從 **讀取服務** 的子菜單。
1. 在 **參數** 部分：

   * 選擇 **請求屬性** 從 **綁定到** 的子菜單。

   * 指定 **移動枚舉** 作為綁定值。

1. 選擇 **更新** 從 **寫入** 服務下拉清單。
1. 在 **參數** 部分：

   * 對於 **移動枚舉** 屬性，選擇 **客戶** 從 **綁定到** 的子菜單。

   * 選擇 **移動枚舉** 從 **綁定值** 的子菜單。

1. 點擊 **完成** 的子菜單。

   ![配置服務](assets/configure_services_customer_new.png)

1. 選中位於 **呼叫** 資料模型對象選擇並點擊 **編輯屬性**。 的 **編輯屬性** 的子菜單。
1. 禁用 **頂級模型對象** 為 **呼叫** 資料模型對象。
1. 點擊 **完成**。

   重複步驟8 - 10以配置 **票據** 資料模型對象。

### 配置服務 {#configure-services}

1. 轉到 **服務** 頁籤。
1. 選擇 **得** 服務和點擊 **編輯屬性**。 的 **編輯屬性** 的子菜單。
1. 在 **編輯屬性** 窗格：

   * 輸入可選標題和說明。
   * 選擇 **客戶** 從 **輸出模型對象** 的子菜單。

   * 點擊 **完成** 的子菜單。

   ![編輯屬性](assets/edit_properties_get_details_new.png)

1. 選擇 **更新** 服務和點擊 **編輯屬性**。 的 **編輯屬性** 的子菜單。
1. 在 **編輯屬性** 窗格：

   * 輸入可選標題和說明。
   * 選擇 **客戶** 從 **輸入模型對象** 的子菜單。

   * 點擊 **完成**。
   * 點擊 **保存** 來修改標籤元素的屬性。

   ![更新服務屬性](assets/update_service_properties_new.png)

## 第5步：Test表單資料模型和服務 {#step-test-form-data-model-and-services}

您可以test資料模型對象和服務，以驗證表單資料模型是否配置正確。

執行以下操作以運行test:

1. 轉到 **模型** 頁籤 **客戶** 資料模型對象和點擊 **Test模型對象**。
1. 在 **Test表單資料模型** 窗口，選擇 **讀取模型對象** 從 **選擇模型/服務** 的子菜單。
1. 在 **輸入** ，為 **移動枚舉** 配置的MySQL資料庫中存在的屬性，然後點擊 **Test**。

   與指定的mobilenum屬性關聯的客戶詳細資訊將被提取並顯示在「輸出」部分，如下所示。 關閉對話框。

   ![Test資料模型](assets/test_data_model_new.png)

1. 轉到 **服務** 頁籤。
1. 選擇 **得** 服務和點擊 **Test服務。**
1. 在 **輸入** ，為 **移動枚舉** 配置的MySQL資料庫中存在的屬性，然後點擊 **Test**。

   與指定的mobilenum屬性關聯的客戶詳細資訊將被提取並顯示在「輸出」部分，如下所示。 關閉對話框。

   ![Test服務](assets/test_service_new.png)

### 編輯和保存示例資料 {#edit-and-save-sample-data}

表單資料模型編輯器允許您為表單資料模型中的所有資料模型對象屬性（包括計算屬性）生成示例資料。 它是一組隨機值，與為每個屬性配置的資料類型一致。 也可以編輯和保存資料，即使重新生成示例資料也會保留這些資料。

執行以下操作以生成、編輯和保存示例資料：

1. 在表單資料模型頁上，點擊 **編輯示例資料**。 它在「編輯示例資料」窗口中生成並顯示示例資料。

   ![編輯示例資料](assets/edit_sample_data_new.png)

1. 在 **編輯示例資料** 窗口，根據需要編輯資料，然後點擊 **保存**。 關閉窗口。
