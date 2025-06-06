---
title: 教學課程：在AEM Forms中建立表單資料模型
description: 建立互動式通訊的表單資料模型
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: c8a6037c-46bd-4058-8314-61cb925ba5a8
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '2684'
ht-degree: 0%

---

# 教學課程：在AEM Forms中建立表單資料模型{#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

此教學課程是[建立您的第一個互動式通訊](/help/forms/using/create-your-first-interactive-communication.md)系列中的步驟。 建議您依照序列時間順序來瞭解、執行和示範完整的教學課程使用案例。

## 關於教學課程 {#about-the-tutorial}

AEM Forms資料整合模組可讓您從不同的後端資料來源(例如AEM使用者設定檔、RESTful Web服務、SOAP型Web服務、OData服務和關聯式資料庫)建立表單資料模型。 您可以在表單資料模型中設定資料模型物件和服務，並將其與調適型表單建立關聯。 最適化表單欄位會繫結至資料模型物件屬性。 這些服務可讓您預先填寫最適化表單，並將提交的表單資料寫入回資料模型物件。

如需表單資料整合與表單資料模型的詳細資訊，請參閱[AEM Forms資料整合](https://helpx.adobe.com/tw/experience-manager/6-3/forms/using/data-integration.html)。

本教學課程將逐步引導您準備、建立、設定表單資料模型，並將其與互動式通訊建立關聯。 在本教學課程結束時，您將能夠：

* [設定資料庫](../../forms/using/create-form-data-model0.md#step-set-up-the-database)
* [將MySQL資料庫設定為資料來源](../../forms/using/create-form-data-model0.md#step-configure-mysql-database-as-data-source)
* [建立表單資料模型](../../forms/using/create-form-data-model0.md#step-create-form-data-model)
* [設定表單資料模型](../../forms/using/create-form-data-model0.md#step-configure-form-data-model)
* [測試表單資料模型](../../forms/using/create-form-data-model0.md#step-test-form-data-model-and-services)

表單資料模型看起來類似以下畫面：

![表單資料模型](assets/form_data_model_callouts_new.png)

**A.**&#x200B;已設定的資料來源&#x200B;**B.**&#x200B;資料來源結構描述&#x200B;**C.**&#x200B;可用的服務&#x200B;**D.**&#x200B;資料模型物件&#x200B;**E.**&#x200B;已設定的服務

## 先決條件 {#prerequisites}

開始之前，請確定您具備下列條件：

* 含有範例資料的MySQL資料庫，如[設定資料庫](../../forms/using/create-form-data-model0.md#step-set-up-the-database)區段中所述。
* 適用於MySQL JDBC驅動程式的OSGi套件組合，如[套件組合JDBC資料庫驅動程式](https://helpx.adobe.com/tw/experience-manager/6-3/help/sites-developing/jdbc.html#bundling-the-jdbc-database-driver)中所述

## 步驟1：設定資料庫 {#step-set-up-the-database}

建立互動式通訊時，資料庫是必不可少的。 本教學課程使用資料庫來顯示表單資料模型和互動式通訊的持續性功能。 設定包含客戶、帳單和呼叫表格的資料庫。
下圖說明customer表格的範例資料：

![sample_data_cust](assets/sample_data_cust.png)

使用下列DDL陳述式在資料庫中建立&#x200B;**customer**&#x200B;資料表。

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

使用下列DDL陳述式在資料庫中建立&#x200B;**bills**&#x200B;資料表。

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

使用下列DDL陳述式在資料庫中建立&#x200B;**呼叫**&#x200B;資料表。

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

**通話**&#x200B;表格包含通話詳細資料，例如通話日期、通話時間、通話號碼、通話期間和通話費用。 **customer**&#x200B;資料表已使用行動電話號碼(mobilenum)欄位連結至通話資料表。 對於&#x200B;**customer**&#x200B;表格中列出的每個行動電話號碼，**通話**&#x200B;表格中有多個記錄。 例如，您可以參照&#x200B;**通話**&#x200B;資料表，擷取&#x200B;**1457892541**&#x200B;行動電話號碼的通話詳細資料。

**帳單**&#x200B;表格包含帳單詳細資訊，例如帳單日期、帳單期間、每月費用及通話費用。 **customer**&#x200B;資料表已使用[帳單計畫]欄位連結至&#x200B;**帳單**&#x200B;資料表。 **customer**&#x200B;資料表中每個客戶都有一個相關聯的計畫。 **帳單**&#x200B;表格包含所有現有計畫的定價詳細資料。 例如，您可以從&#x200B;**customer**&#x200B;資料表中擷取&#x200B;**Sarah**&#x200B;的計畫詳細資料，並使用這些詳細資料從&#x200B;**帳單**&#x200B;資料表中擷取定價詳細資料。

## 步驟2：將MySQL資料庫設定為資料來源 {#step-configure-mysql-database-as-data-source}

您可以設定不同型別的資料來源，以建立表單資料模型。 在本教學課程中，您將設定已設定並填入範例資料的MySQL資料庫。 如需其他支援的資料來源以及如何設定它們的相關資訊，請參閱[AEM Forms資料整合](https://helpx.adobe.com/tw/experience-manager/6-3/forms/using/data-integration.html)。

執行下列動作來設定您的MySQL資料庫：

1. 以OSGi套件形式安裝MySQL資料庫的JDBC驅動程式：

   1. 以管理員身分登入AEM Forms製作執行個體，並前往AEM網頁主控台套件組合。 預設URL為[https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles)。
   1. 選取&#x200B;**安裝/更新**。 出現&#x200B;**上傳/安裝組合**&#x200B;對話方塊。

   1. 選取&#x200B;**選擇檔案**&#x200B;以瀏覽並選取MySQL JDBC驅動程式OSGi套件。 選取&#x200B;**開始套件**&#x200B;和&#x200B;**重新整理套件**，然後選取&#x200B;**安裝**&#x200B;或&#x200B;**更新**。 請確定Oracle Corporation的MySQL JDBC驅動程式處於作用中狀態。 已安裝驅動程式。

1. 將MySQL資料庫設定為資料來源：

   1. 前往AEM網頁主控台，網址為[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
   1. 找到&#x200B;**Apache Sling Connection Pooled DataSource**&#x200B;設定。 選取以在編輯模式中開啟設定。
   1. 在設定對話方塊中，指定下列詳細資訊：

      * **資料來源名稱：**&#x200B;您可以指定任何名稱。 例如，指定&#x200B;**MySQL**。

      * **DataSource服務屬性名稱**：指定包含DataSource名稱的服務屬性名稱。 它是在將資料來源執行個體註冊為OSGi服務時指定。 例如，**datasource.name**。

      * **JDBC驅動程式類別**：指定JDBC驅動程式的Java類別名稱。 針對MySQL資料庫，請指定&#x200B;**com.mysql.jdbc.Driver**。

      * **JDBC連線URI**：指定資料庫的連線URL。 對於在連線埠3306和結構描述Teleca上執行的MySQL資料庫，URL是： `jdbc:mysql://'server':3306/teleca?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **使用者名稱：**&#x200B;資料庫的使用者名稱。 必須啟用JDBC驅動程式才能與資料庫建立連線。
      * **密碼：**&#x200B;資料庫的密碼。 必須啟用JDBC驅動程式才能與資料庫建立連線。
      * **借入測試：**&#x200B;啟用&#x200B;**借入測試**&#x200B;選項。

      * **回訪時測試：**&#x200B;啟用&#x200B;**回訪時測試**&#x200B;選項。

      * **驗證查詢：**&#x200B;指定SQL SELECT查詢來驗證集區的連線。 查詢至少必須傳回一列。 例如，**從客戶**&#x200B;選取&#42;。

      * **交易隔離**：將值設定為&#x200B;**READ_COMMITTED**。

   保留其他具有預設[值](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html)的屬性，並選取&#x200B;**儲存**。

   會建立類似下列的設定。

   ![Apache設定](assets/apache_configuration_new.png)

## 步驟3：建立表單資料模型 {#step-create-form-data-model}

AEM Forms提供直覺式使用者介面，可讓您從已設定的資料來源[建立表單資料模式](https://helpx.adobe.com/tw/experience-manager/6-3/forms/using/data-integration.html#main-pars_header_1524967585)l。 您可以在表單資料模型中使用多個資料來源。 在本教學課程的使用案例中，您將使用MySQL做為資料來源。

執行下列操作以建立表單資料模型：

1. 在AEM作者執行個體中，導覽至&#x200B;**Forms** > **資料整合**。
1. 選取&#x200B;**建立** > **表單資料模型**。
1. 在建立表單資料模型精靈中，指定表單資料模型的&#x200B;**名稱**。 例如，**FDM_Create_First_IC**。 選取&#x200B;**「下一步」**。
1. 選取資料來源畫面會列出所有已設定的資料來源。 選取&#x200B;**MySQL**&#x200B;資料來源並選取&#x200B;**建立**。

   ![MYSQL資料來源](assets/fdm_mysql_data_source_new.png)

1. 按一下&#x200B;**完成**。 已建立&#x200B;**FDM_Create_First_IC**&#x200B;表單資料模型。

## 步驟4：設定表單資料模型 {#step-configure-form-data-model}

設定表單資料模型包括：

* [新增資料模型物件及服務](#add-data-model-objects-and-services)
* [建立資料模型物件的計運算元屬性](#create-computed-child-properties-for-data-model-object)
* [新增資料模型物件之間的關聯](#add-associations-between-data-model-objects)
* [編輯資料模型物件屬性](#edit-data-model-object-properties)
* [為資料模型物件設定服務](#configure-services)

### 新增資料模型物件及服務 {#add-data-model-objects-and-services}

1. 在AEM作者執行個體上，導覽至&#x200B;**Forms** > **資料整合**。 預設URL為[https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm)。
1. 此處列出您先前建立的&#x200B;**FDM_Create_First_IC**&#x200B;表單資料模型。 選取它並選取&#x200B;**編輯**。

   選取的資料來源&#x200B;**MySQL**&#x200B;會顯示在&#x200B;**資料來源**&#x200B;窗格中。

   FDM的![MYSQL資料來源](assets/mysql_fdm_new.png)

1. 展開&#x200B;**MySQL**&#x200B;資料來源樹狀結構。 從&#x200B;**teleca**&#x200B;結構描述選取下列資料模型物件及服務：

   * **資料模型物件**：

      * 帳單
      * 呼叫
      * 客戶

   * **服務：**

      * get
      * 更新

   選取&#x200B;**新增選取的**&#x200B;以將選取的資料模型物件和服務新增至表單資料模型。

   ![選取資料模型物件服務](assets/select_data_model_object_services_new.png)

   帳單、呼叫和客戶資料模型物件會顯示在&#x200B;**模型**&#x200B;標籤的右窗格中。 取得和更新服務會顯示在&#x200B;**服務**&#x200B;索引標籤中。

   ![資料模型物件](assets/data_model_objects_new.png)

### 建立資料模型物件的計運算元屬性 {#create-computed-child-properties-for-data-model-object}

計算屬性是根據規則或運算式計算其值的屬性。 您可以使用規則將計算屬性的值設定為常值字串、數字、數學運算式的結果或表單資料模型中其他屬性的值。

根據使用案例，使用下列數學運算式在&#x200B;**用料表**&#x200B;資料模型物件中建立&#x200B;**usagecharges**&#x200B;子計算屬性：

* 使用費=通話費+電話會議費+ SMS費+行動網際網路費+漫遊國家+漫遊國際+ VAS （所有這些屬性都存在於帳單資料模型物件中）
如需&#x200B;**usagecharges**&#x200B;子計算屬性的詳細資訊，請參閱[規劃互動式通訊](/help/forms/using/planning-interactive-communications.md)。

執行以下步驟來建立用料表資料模型物件的計運算元屬性：

1. 選取&#x200B;**清單**&#x200B;資料模型物件頂端的核取方塊以選取它，並選取&#x200B;**建立子屬性**。
1. 在&#x200B;**建立子屬性**&#x200B;窗格中：

   1. 輸入&#x200B;**usagecharges**&#x200B;作為子屬性的名稱。
   1. 啟用&#x200B;**已計算**。
   1. 選取&#x200B;**Float**&#x200B;作為型別，並選取&#x200B;**Done**&#x200B;將子屬性新增至&#x200B;**bills**&#x200B;資料模型物件。

   ![建立子屬性](assets/create_child_property_new.png)

1. 選取&#x200B;**編輯規則**&#x200B;以開啟規則編輯器。
1. 選擇 **建立**。**設定值**&#x200B;規則視窗隨即開啟。
1. 從「選取選項」下拉式清單中，選取&#x200B;**數學運算式**。

   ![使用費用規則編輯器](assets/usage_charges_rule_editor_new.png)

1. 在數學運算式中，選取&#x200B;**callcharges**&#x200B;和&#x200B;**confcallcharges**&#x200B;分別做為第一和第二物件。 選取&#x200B;**加**&#x200B;作為運運算元。 在數學運算式中選取，並選取&#x200B;**延伸運算式**&#x200B;以將&#x200B;**smscharges**、**internetcharges**、**roamingnational**、**roamingintnl**&#x200B;和&#x200B;**vas**&#x200B;物件新增至運算式。

   下圖說明規則編輯器中的數學運算式：

   ![使用費用規則](assets/usage_charges_rule_all_new.png)

1. 選取&#x200B;**完成**。 規則會在規則編輯器中建立。
1. 選取&#x200B;**關閉**&#x200B;以關閉[規則編輯器]視窗。

### 在資料模型物件之間新增關聯 {#add-associations-between-data-model-objects}

定義資料模型物件後，您就可以建立它們之間的關聯。 關聯可以是一對一或一對多。 例如，可以有多個與員工相關聯的相依項。 它稱為一對多關聯，在連線相關資料模型物件的線上以1：n表示。 但是，如果關聯針對指定的員工ID傳回唯一員工名稱，則稱為一對一關聯。

當您將資料來源中的關聯資料模型物件新增至表單資料模型時，它們的關聯會保留並顯示為以箭頭線連線。

根據使用案例，在資料模型物件之間建立下列關聯：

| 關聯 | 資料模型物件 |
|---|---|
| 1：n | 客戶：通話（每個月帳單中可將多個通話與客戶相關聯） |
| 1:1 | customer：bills （一個帳單與特定月份的客戶相關聯） |

執行以下步驟來建立資料模型物件之間的關聯：

1. 選取&#x200B;**客戶**&#x200B;資料模型物件頂端的核取方塊以選取它，並選取&#x200B;**新增關聯**。 **新增關聯**&#x200B;屬性窗格開啟。
1. 在&#x200B;**新增關聯**&#x200B;窗格中：

   * 指定關聯的標題。 它是選用欄位。
   * 從&#x200B;**型別**&#x200B;下拉式清單中選取&#x200B;**一對多**。

   * 從&#x200B;**模型物件**&#x200B;下拉式清單中選取&#x200B;**呼叫**。

   * 從&#x200B;**服務**&#x200B;下拉式清單中選取&#x200B;**get**。

   * 選取「**新增**」以使用屬性將&#x200B;**客戶**&#x200B;資料模型物件連結至&#x200B;**呼叫**&#x200B;資料模型物件。 根據使用案例，呼叫資料模型物件必須連結至客戶資料模型物件中的行動電話號碼屬性。 **新增引數**&#x200B;對話方塊開啟。

   ![新增關聯](assets/add_association_new.png)

1. 在&#x200B;**新增引數**&#x200B;對話方塊中：

   * 從&#x200B;**名稱**&#x200B;下拉式清單中選取&#x200B;**行動裝置**。 行動號碼屬性是客戶中提供的常見屬性，可呼叫資料模型物件。 因此，它可用來建立customer與呼叫資料模型物件之間的關聯。
對於客戶資料模型物件中可用的每個行動電話號碼，呼叫表格中有多個可用的呼叫記錄。

   * 指定引數的選用標題和說明。
   * 從&#x200B;**繫結至**&#x200B;下拉式清單中選取&#x200B;**客戶**。

   * 從&#x200B;**繫結值**&#x200B;下拉式清單中選取&#x200B;**mobilenum**。

   * 選取「**新增**」。

   ![新增引數的關聯](assets/add_association_argument_new.png)

   mobilenum屬性會顯示在&#x200B;**引數**&#x200B;區段中。

   ![新增引數關聯](assets/add_argument_association_new.png)

1. 選取&#x200B;**完成**，在客戶和呼叫資料模型物件之間建立1：n關聯。

   在客戶與呼叫資料模型物件之間建立關聯後，在客戶與帳單資料模型物件之間建立1:1關聯。

1. 選取&#x200B;**客戶**&#x200B;資料模型物件頂端的核取方塊以選取它，並選取&#x200B;**新增關聯**。 **新增關聯**&#x200B;屬性窗格開啟。
1. 在&#x200B;**新增關聯**&#x200B;窗格中：

   * 指定關聯的標題。 它是選用欄位。
   * 從&#x200B;**Type**&#x200B;下拉式清單中選取&#x200B;**One to One**。

   * 從&#x200B;**模型物件**&#x200B;下拉式清單中選取&#x200B;**清單**。

   * 從&#x200B;**服務**&#x200B;下拉式清單中選取&#x200B;**get**。 **billplan**&#x200B;屬性是清單資料表的主索引鍵，已在&#x200B;**引數**&#x200B;區段中可用。
帳單和客戶資料模型物件分別使用帳單計畫(bills)和客戶計畫(customerplan) (customer)屬性連結。 在這些屬性之間建立繫結，以擷取MySQL資料庫中任何可用客戶的計畫詳細資訊。

   * 從&#x200B;**繫結至**&#x200B;下拉式清單中選取&#x200B;**客戶**。

   * 從&#x200B;**繫結值**&#x200B;下拉式清單中選取&#x200B;**customerplan**。

   * 選取&#x200B;**完成**&#x200B;以在billplan和customerplan屬性之間建立繫結。

   ![新增客戶帳單的關聯](assets/add_association_customer_bills_new.png)

   下列影像說明資料模型物件與用來建立它們之間關聯的屬性之間的關聯：

   ![fdm_associations](assets/fdm_associations.gif)

### 編輯資料模型物件屬性 {#edit-data-model-object-properties}

在客戶與其他資料模型物件之間建立關聯後，編輯客戶屬性以定義屬性，系統會根據此屬性從資料模型物件中擷取資料。 根據使用案例，行動電話號碼會當作屬性使用，以從客戶資料模型物件中擷取資料。

1. 選取&#x200B;**customer**&#x200B;資料模型物件頂端的核取方塊以選取它，並選取&#x200B;**編輯屬性**。 **編輯屬性**&#x200B;窗格開啟。
1. 指定&#x200B;**客戶**&#x200B;為&#x200B;**最上層模型物件**。
1. 從&#x200B;**讀取服務**&#x200B;下拉式清單中選取&#x200B;**get**。
1. 在&#x200B;**引數**&#x200B;區段中：

   * 從&#x200B;**繫結至**&#x200B;下拉式清單中選取&#x200B;**要求屬性**。

   * 指定&#x200B;**mobilenum**&#x200B;做為繫結值。

1. 從&#x200B;**寫入**&#x200B;服務下拉式清單中選取&#x200B;**更新**。
1. 在&#x200B;**引數**&#x200B;區段中：

   * 針對&#x200B;**mobilenum**&#x200B;屬性，從&#x200B;**繫結至**&#x200B;下拉式清單中選取&#x200B;**客戶**。

   * 從&#x200B;**繫結值**&#x200B;下拉式清單中選取&#x200B;**mobilenum**。

1. 選取&#x200B;**完成**&#x200B;以儲存屬性。

   ![設定服務](assets/configure_services_customer_new.png)

1. 選取&#x200B;**呼叫**&#x200B;資料模型物件頂端的核取方塊以選取它，並選取&#x200B;**編輯屬性**。 **編輯屬性**&#x200B;窗格開啟。
1. 停用&#x200B;**呼叫**&#x200B;資料模型物件的&#x200B;**最上層模型物件**。
1. 選取「**完成**」。

   重複步驟8至10，設定&#x200B;**用料表**&#x200B;資料模型物件的屬性。

### 設定服務 {#configure-services}

1. 移至&#x200B;**服務**&#x200B;標籤。
1. 選取&#x200B;**get**&#x200B;服務並選取&#x200B;**編輯屬性**。 **編輯屬性**&#x200B;窗格開啟。
1. 在&#x200B;**編輯屬性**&#x200B;窗格中：

   * 輸入選用的標題和說明。
   * 從&#x200B;**輸出模型物件**&#x200B;下拉式清單中選取&#x200B;**客戶**。

   * 選取&#x200B;**完成**&#x200B;以儲存屬性。

   ![編輯屬性](assets/edit_properties_get_details_new.png)

1. 選取&#x200B;**更新**&#x200B;服務並選取&#x200B;**編輯屬性**。 **編輯屬性**&#x200B;窗格開啟。
1. 在&#x200B;**編輯屬性**&#x200B;窗格中：

   * 輸入選用的標題和說明。
   * 從&#x200B;**輸入模型物件**&#x200B;下拉式清單中選取&#x200B;**客戶**。

   * 選取「**完成**」。
   * 選取&#x200B;**儲存**&#x200B;以儲存表單資料模型。

   ![更新服務屬性](assets/update_service_properties_new.png)

## 步驟5：測試表單資料模型和服務 {#step-test-form-data-model-and-services}

您可以測試資料模型物件與服務，以確認表單資料模型已正確設定。

執行下列操作以執行測試：

1. 移至&#x200B;**模型**&#x200B;標籤，選取&#x200B;**客戶**&#x200B;資料模型物件，然後選取&#x200B;**測試模型物件**。
1. 在&#x200B;**測試表單資料模型**&#x200B;視窗中，從&#x200B;**選取模型/服務**&#x200B;下拉式清單中選取&#x200B;**讀取模型物件**。
1. 在&#x200B;**Input**&#x200B;區段中，為已設定之MySQL資料庫中存在的&#x200B;**mobilenum**&#x200B;屬性指定值，並選取&#x200B;**測試**。

   系統會擷取與指定mobilenum屬性相關聯的客戶詳細資訊，並顯示在「輸出」區段中，如下所示。 關閉對話方塊。

   ![測試資料模型](assets/test_data_model_new.png)

1. 移至&#x200B;**服務**&#x200B;標籤。
1. 選取&#x200B;**get**&#x200B;服務並選取&#x200B;**測試服務。**
1. 在&#x200B;**Input**&#x200B;區段中，為已設定之MySQL資料庫中存在的&#x200B;**mobilenum**&#x200B;屬性指定值，並選取&#x200B;**測試**。

   系統會擷取與指定mobilenum屬性相關聯的客戶詳細資訊，並顯示在「輸出」區段中，如下所示。 關閉對話方塊。

   ![測試服務](assets/test_service_new.png)

### 編輯並儲存範例資料 {#edit-and-save-sample-data}

表單資料模型編輯器可讓您為表單資料模型中的所有資料模型物件屬性（包括計算屬性）產生範例資料。 這是一組隨機值，符合為每個屬性設定的資料型別。 您也可以編輯並儲存資料，即使您重新產生範例資料，資料仍會保留。

執行下列操作來產生、編輯和儲存範例資料：

1. 在表單資料模型頁面上，選取&#x200B;**編輯範例資料**。 它會在「編輯範例資料」視窗中產生並顯示範例資料。

   ![編輯範例資料](assets/edit_sample_data_new.png)

1. 在&#x200B;**編輯範例資料**&#x200B;視窗中，視需要編輯資料，並選取&#x200B;**儲存**。 關閉視窗。
