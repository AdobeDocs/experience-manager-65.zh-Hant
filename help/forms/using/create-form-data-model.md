---
title: 「教程：建立表單資料模型"
seo-title: Create Form Data Model Tutorial
description: 建立表單資料模型
seo-description: Create form data model
uuid: b9d2bb1b-90f0-44f4-b1e3-0603cdf5f5b8
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 12e6c325-ace0-4a57-8ed4-6f7ceee23099
docset: aem65
exl-id: 40bc5af6-9023-437e-95b0-f85d3df7d8aa
source-git-commit: e147605ff4d5c3d2403632285956559db235c084
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 1%

---

# 教程：建立表單資料模型 {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

本教程是 [建立第一個自適應窗體](../../forms/using/create-your-first-adaptive-form.md) 的下界。 建議按時間順序按系列進行操作，以瞭解、執行和演示完整的教程使用案例。

## 關於教程 {#about-the-tutorial}

AEM [!DNL Forms] 資料整合模組允許您從不同的後端資料源(如AEM用戶配置檔案、REST風格的Web服務、基於SOAP的Web服務、OData服務和關係資料庫)建立表單資料模型。 可以在表單資料模型中配置資料模型對象和服務，並將其與自適應表單關聯。 自適應表單域綁定到資料模型對象屬性。 這些服務使您能夠預填自適應表單並將提交的表單資料寫回資料模型對象。

有關表單資料整合和表單資料模型的詳細資訊，請參見 [AEM Forms資料整合](../../forms/using/data-integration.md)。

本教程將指導您完成準備、建立、配置表單資料模型以及將表單資料模型與自適應表單關聯的步驟。 在本教程的結束時，您將能夠：

* [將MySQL資料庫配置為資料源](#config-database)
* [使用MySQL資料庫建立表單資料模型](#create-fdm)
* [配置表單資料模型](#config-fdm)
* [Test表單資料模型](#test-fdm)

表單資料模型將類似於以下內容：

![表單資料模型_l](assets/form-data-model_l.png)

**答：** 已配置資料源 **B** 資料源架構 **C.** 可用服務 **D** 資料模型對象 **E.** 已配置的服務

## 必備條件 {#prerequisites}

在開始之前，請確保具備以下功能：

* [!DNL MySQL] 資料庫，其示例資料如Prequisets部分所述 [建立第一個自適應窗體](../../forms/using/create-your-first-adaptive-form.md)
* OSGi捆綁 [!DNL MySQL] JDBC驅動程式，如中所述 [捆綁JDBC資料庫驅動程式](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)
* 如第一教程中所述，自適應窗體 [建立自適應窗體](/help/forms/using/create-adaptive-form.md)

## 步驟1:將MySQL資料庫配置為資料源 {#config-database}

可以配置不同類型的資料源以建立表單資料模型。 在本教程中，我們將配置您配置並填充了示例資料的MySQL資料庫。 有關其他受支援的資料源以及如何配置它們的資訊，請參見 [AEM Forms資料整合](../../forms/using/data-integration.md)。

執行以下操作以配置 [!DNL MySQL] 資料庫：

1. 安裝JDBC驅動程式 [!DNL MySQL] 資料庫作為OSGi包：

   1. 下載 [!DNL MySQL] JDBC驅動程式OSGi捆綁包 `http://www.java2s.com/ref/jar/download-orgosgiservicejdbc100jar-file.html`。 <!-- This URL is an insecure link but using https is not possible -->
   1. 登錄到AEM [!DNL Forms] 以管理員身份建立實例並轉AEM到Web控制台捆綁包。 預設URL為 [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles)。

   1. 點擊 **[!UICONTROL 安裝/更新]**。 安 [!UICONTROL 上傳/安裝捆綁包] 對話框。

   1. 點擊 **[!UICONTROL 選擇檔案]** 瀏覽並選擇 [!DNL MySQL] JDBC驅動程式OSGi捆綁包。 選擇 **[!UICONTROL 啟動包]** 和 **[!UICONTROL 刷新包]**，然後點擊 **[!UICONTROL 安裝或更新]**。 確保 [!DNL Oracle Corporation's] JDBC驅動程式 [!DNL MySQL] 活動。 已安裝驅動程式。

1. 配置 [!DNL MySQL] 資料庫：

   1. 轉到AEMWeb控制台 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。
   1. 定位 **Apache Sling連接池化資料源** 配置。 按一下以在編輯模式下開啟配置。
   1. 在配置對話框中，指定以下詳細資訊：

      * **資料源名稱：** 可以指定任何名稱。 例如，指定 **WeRetailMySQL**。
      * **DataSource服務屬性名稱**:指定包含資料源名稱的服務屬性的名稱。 將資料源實例註冊為OSGi服務時指定。 比如說， **datasource.name**。
      * **JDBC驅動程式類**:指定JDBC驅動程式的Java類名。 對於 [!DNL MySQL] 資料庫，指定 **com.mysql.jdbc.驅動程式**。
      * **JDBC連接URI**:指定資料庫的連接URL。 對於 [!DNL MySQL] 運行在埠3306和schema weretail上的資料庫，URL為： `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`

      >[!NOTE]
      >
      > 當 [!DNL MySQL] 資料庫位於防火牆後，則資料庫主機名不是公共DNS。 需要在 */etc/hosts* 主機的AEM檔案。

      * **用戶名：** 資料庫的用戶名。 需要啟用JDBC驅動程式來與資料庫建立連接。
      * **密碼：** 資料庫的口令。 需要啟用JDBC驅動程式來與資料庫建立連接。

      >[!NOTE]
      >
      >AEM Forms不支援NT身份驗證 [!DNL MySQL]。 轉到AEMWeb控制台 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) 並搜索「Apache Sling連接池化資料源」。對於「JDBC連接URI」屬性集值「integratedSecurity」為False，使用建立的用戶名和密碼進行連接 [!DNL MySQL] 資料庫。

      * **Test借用：** 啟用 **[!UICONTROL Test借用]** 的雙曲餘切值。
      * **Test返回：** 啟用 **[!UICONTROL Test返回]** 的雙曲餘切值。
      * **驗證查詢：** 指定SQL SELECT查詢以驗證池中的連接。 查詢必須至少返回一行。 比如說， **選擇 &#42; 從客戶詳細資訊**。
      * **事務隔離**:將值設定為 **已提交讀取**。

         保留其他屬性為預設 [值](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) 點擊 **[!UICONTROL 保存]**。

         將建立與以下類似的配置。

         ![關係資料庫 — 資料源 — 配置](assets/relational-database-data-source-configuration.png)



## 步驟2:建立表單資料模型 {#create-fdm}

AEM [!DNL Forms] 提供直觀的用戶介面 [建立表單資料模型](data-integration.md) 從配置的資料源中。 可以在表單資料模型中使用多個資料源。 對於我們的使用案例，我們將使用 [!DNL MySQL] 資料源。

執行以下操作以建立表單資料模型：

1. 在作AEM者實例中，導航到 **[!UICONTROL Forms]** > **[!UICONTROL 資料整合]**。
1. 點擊 **[!UICONTROL 建立]** > **[!UICONTROL 窗體資料模型]**。
1. 在「建立表單資料模型」對話框中，指定 **名稱** 的子菜單。 比如說， **客戶發運 — 開單詳細資訊**。 點擊 **[!UICONTROL 下一個]**。
1. 「選擇資料源」螢幕列出所有已配置的資料源。 選擇 **WeRetailMySQL** 資料源和分路 **[!UICONTROL 建立]**。

   ![資料源選擇](assets/data-source-selection.png)

的 **客戶發運 — 開單詳細資訊** 建立窗體資料模型。

## 第3步：配置表單資料模型 {#config-fdm}

配置表單資料模型涉及：

* 添加資料模型對象和服務
* 配置資料模型對象的讀寫服務

執行以下操作以配置表單資料模型：

1. 在作AEM者實例上，導航至 **[!UICONTROL Forms]** > **[!UICONTROL 資料整合]**。 預設URL為 [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm)。
1. 的 **客戶發運 — 開單詳細資訊** 此處列出了您以前建立的表單資料模型。 在編輯模式下開啟它。

   所選資料源 **WeRetailMySQL** 在窗體資料模型中配置。

   ![預設fdm](assets/default-fdm.png)

1. 展開WeRailMySQL資料源樹。 從中選擇以下資料模型對象和服務 **零售** > **customerdetails（客戶詳細資訊）** 模式：

   * **資料模型對象**:

      * ID
      * 名稱
      * 送貨地址
      * 城市
      * 狀態
      * 郵遞區號
   * **服務:**

      * 得
      * 更新

   點擊 **添加選定項** 將所選資料模型對象和服務添加到表單資料模型。

   ![WeRetail架構](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >JDBC資料源的預設獲取、更新和插入服務是隨表單資料模型提供的。

1. 為資料模型對象配置讀和寫服務。

   1. 選擇 **customerdetails（客戶詳細資訊）** 資料模型對象和抽頭 **[!UICONTROL 編輯屬性]**。
   1. 選擇 **[!UICONTROL 得]** 從「讀取服務」下拉清單中。 的 **ID** argument（自動添加customerdetails資料模型對象中的主鍵）。 點擊 ![aem_6_3_edit](assets/aem_6_3_edit.png) 並按如下方式配置參數。

      ![讀預設](assets/read-default.png)

   1. 同樣，選擇 **[!UICONTROL 更新]** 寫入服務。 的 **customerdetails（客戶詳細資訊）** 對象會自動添加為參數。 參數的配置如下。

      ![寫預設](assets/write-default.png)

      添加和配置 **ID** 如下所示。

      ![id-arg](assets/id-arg.png)

   1. 點擊 **[!UICONTROL 完成]** 保存資料模型對象屬性。 然後，點擊 **[!UICONTROL 保存]** 來修改標籤元素的屬性。

      的 **[!UICONTROL 得]** 和 **[!UICONTROL 更新]** 服務被添加為資料模型對象的預設服務。

      ![資料模型對象](assets/data-model-object.png)

1. 轉到 **[!UICONTROL 服務]** 頁籤和配置 **[!UICONTROL 得]** 和 **[!UICONTROL 更新]** 服務。

   1. 選擇 **[!UICONTROL 得]** 服務和點擊 **[!UICONTROL 編輯屬性]**。 屬性對話框開啟。
   1. 在「編輯屬性」對話框中指定以下內容：

      * **標題**:指定服務的標題。 例如：檢索發運地址。
      * **說明**:指定包含服務詳細功能的說明。 例如：

         此服務從中檢索發運地址和其他客戶詳細資訊 [!DNL MySQL] 資料庫

      * **輸出模型對象**:選擇包含客戶資料的方案。 例如：

         customdetail架構

      * **返回陣列**:禁用 **返回陣列** 的雙曲餘切值。
      * **參數**:選擇命名的參數 **ID**。

      點擊 **[!UICONTROL 完成]**。 已配置從MySQL資料庫檢索客戶詳細資訊的服務。

      ![Shiiping地址檢索](assets/shiiping-address-retrieval.png)

   1. 選擇 **[!UICONTROL 更新]** 服務和點擊 **[!UICONTROL 編輯屬性]**。 屬性對話框開啟。

   1. 在 [!UICONTROL 編輯屬性] 對話框：

      * **標題**:指定服務的標題。 例如，更新發運地址。
      * **說明**:指定包含服務詳細功能的說明。 例如：

         此服務更新MySQL資料庫中的發運地址和相關欄位

      * **輸入模型對象**:選擇包含客戶資料的方案。 例如：

         customdetail架構

      * **輸出類型**:選擇 **布爾值**。

      * **參數**:選擇命名的參數 **ID** 和 **customerdetails（客戶詳細資訊）**。
      點擊 **[!UICONTROL 完成]**。 的 **[!UICONTROL 更新]** 更新客戶詳細資訊的服務 [!DNL MySQL] 已配置資料庫。

      ![shiiping地址更新](assets/shiiping-address-update.png)



配置表單資料模型中的資料模型對象和服務。 現在可以test表單資料模型。

## 第4步：Test表單資料模型 {#test-fdm}

您可以test資料模型對象和服務，以驗證表單資料模型是否配置正確。

執行以下操作以運行test:

1. 轉到 **[!UICONTROL 模型]** 頁籤 **customerdetails（客戶詳細資訊）** 資料模型對象和點擊 **[!UICONTROL Test模型對象]**。
1. 在 [!UICONTROL Test型號/服務] 窗口，選擇 **[!UICONTROL 讀取模型對象]** 從 **[!UICONTROL 選擇模型/服務]** 下拉。
1. 在 **customerdetails（客戶詳細資訊）** ，為 **ID** 已配置中存在的參數 [!DNL MySQL] 資料庫和點 **[!UICONTROL Test]**。

   將提取與指定ID關聯的客戶詳細資訊並在 **[!UICONTROL 輸出]** 的下界。

   ![test — 讀取模型](assets/test-read-model.png)

1. 同樣，可以testWrite模型對象和服務。

   在以下示例中，更新服務成功更新了資料庫中id 7102715的地址詳細資訊。

   ![test — 寫模型](assets/test-write-model.png)

   現在，如果您再次testid 7107215的讀取型號服務，它將獲取並顯示更新的客戶詳細資訊，如下所示。

   ![已更新](assets/read-updated.png)
