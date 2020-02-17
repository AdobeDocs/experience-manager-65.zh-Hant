---
title: 設定資料來源
seo-title: 設定資料來源
description: 瞭解如何設定不同類型的資料來源並運用來建立表單資料模型。
seo-description: 瞭解如何設定不同類型的資料來源並運用來建立表單資料模型。
uuid: 12360c8c-b596-4f9b-837a-10a8ff5c7448
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9d78a6dc-fc9c-415b-b817-164fe6648b30
docset: aem65
translation-type: tm+mt
source-git-commit: 43780682ba27d9c7d578393df04267ed8be4f1de

---


# 設定資料來源{#configure-data-sources}

![](do-not-localize/data-integeration.png)

AEM Forms Data Integration可讓您設定並連線至不同的資料來源。 下列類型是現成可用的支援。 不過，只需少量自訂，您也可以整合其他資料來源。

* 關係資料庫- mySQL、Microsoft SQL Server、IBM DB2和Oracle RDBMS。
* AEM使用者設定檔
* REST風格的Web服務
* 基於SOAP的web services
* OData服務

資料整合支援OAuth2.0、基本驗證和API金鑰驗證類型立即可用，並可實作自訂驗證以存取網站服務。 雖然RESTful、SOAP架構和OData服務已在AEM Cloud services中設定，但AEM web主控台中已設定關係式資料庫的JDBC和AEM使用者設定檔的連接器。

## 配置關係資料庫 {#configure-relational-database}

您可以使用AEM Web Console Configuration來設定關係式資料庫。 執行下列動作：

1. 前往AEM網頁主控台([https:// server]:[host]/system/console/configMgr)。
1. 尋找 **[!UICONTROL Apache Sling Connection Pooled DataSource組態]** 。 點選以在編輯模式中開啟設定。
1. 在配置對話框中，指定要配置的資料庫的詳細資訊，例如：

   * 資料來源的名稱
   * 儲存資料源名稱的資料源服務屬性
   * JDBC驅動程式的Java類名
   * JDBC連接URI
   * 用於與JDBC驅動程式建立連接的用戶名和密碼
   >[!NOTE] {graybox=&quot;true&quot;}
   >
   >在設定資料來源之前，請務必先加密機密資訊，例如密碼。 要加密：
   >
   >    
   >    
   >    1. 轉至https://[server]:[port]/system/console/crypto。
   >    1. 在「純 **[!UICONTROL 文本]** 」欄位中，指定要加密的口令或任何字串，然後按一下「保 **[!UICONTROL 護」]**。
   >    
   >    
   >    
   >加密的文字會出現在「受保護的文字」欄位中，您可在設定中指定。

1. 啟 **[!UICONTROL 用「借用時測試]** 」或「返回時測 **** 試」，指定在分別從池借用或返回或返回到池之前驗證對象。
1. 在「驗證查詢」欄位中指定SQL **[!UICONTROL SELECT查詢]** ，以驗證池中的連接。 查詢至少必須返回一行。 根據您的資料庫，指定下列其中一項：

   * 選擇1（MySQL和MS SQL）
   * 從雙(Oracle)中選擇1

1. 點選「 **[!UICONTROL 儲存]** 」以儲存設定。

## 設定AEM使用者設定檔 {#configure-aem-user-profile}

您可以在AEM Web Console中使用「使用者描述檔連接器」設定來設定AEM使用者描述檔。 執行下列動作：

1. 前往AEM網頁主控台([https:// server]:[host]/system/console/configMgr)。
1. 尋找 **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]** ，然後點選以在編輯模式中開啟設定。
1. 在「用戶配置檔案連接器配置」對話框中，可以添加、刪除或更新用戶配置檔案屬性。 指定的屬性將可用於表單資料模型中。 使用以下格式指定用戶配置檔案屬性：

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   範例：

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`
   >[!NOTE] {graybox=&quot;true&quot;}
   >
   >上例 **中的*** ，表示AEM使用者設定檔中，CRXDE `profile/empLocation/` 結構中節點下的所有節點。 表單資料模型可以訪問節點下 `city` 任何節點 `string` 中的類型屬 `profile/empLocation/` 性。 但是，包含指定屬性的節點必須遵循一致的結構。

1. 點選「 **[!UICONTROL 儲存]** 」以儲存設定。

## 為雲端服務設定資料夾 {#cloud-folder}

**注意**:為RESTful、SOAP和OData服務配置雲端服務時，需要配置雲端服務資料夾。

AEM中的所有雲端服務設定都會整合在AEM `/conf` 儲存庫的資料夾中。 依預設，檔 `conf` 案夾包含您 `global` 可建立雲端服務組態的檔案夾。 不過，您必須針對雲端組態手動啟用它。 您也可以在中建立其他資料夾， `conf` 以建立並組織雲端服務組態。

要為雲端服務配置配置資料夾：

1. 前往「工 **[!UICONTROL 具>一般>設定瀏覽器]**」。
1. 請執行下列動作，為雲端設定啟用全域資料夾，或略過此步驟，為雲端服務設定建立並設定另一個資料夾。

   1. 在配置瀏 **[!UICONTROL 覽器中]**，選擇檔案 `global` 夾並點選 **[!UICONTROL 屬性]**。

   1. 在「設 **[!UICONTROL 定屬性]** 」對話方 **[!UICONTROL 塊中，啟用Cloud Configurations]**。

   1. 點選 **[!UICONTROL 「儲存並關閉]** 」以儲存設定並退出對話方塊。

1. 在設定瀏 **[!UICONTROL 覽器中]**，點選 **[!UICONTROL 建立]**。
1. 在「建 **[!UICONTROL 立設定]** 」對話方塊中，指定資料夾的標題並啟用「雲 **[!UICONTROL 端設定」]**。
1. 點選 **[!UICONTROL 「建立]** 」以建立適用於雲端服務設定的資料夾。

## 配置REST風格的Web服務 {#configure-restful-web-services}

REST風格的Web服務可在Swagger定義檔 [案中使用](https://swagger.io/specification/) JSON或YAML格式的Swagger規格加以說明。 若要在AEM雲端服務中設定REST風格的網站服務，請確定您的檔案系統上有Swagger檔案，或是檔案所在的URL。

執行以下操作以配置REST風格的服務：

1. 前往「 **[!UICONTROL 工具>雲端服務>資料來源」]**。 點選以選取您要建立雲端設定的檔案夾。

   如需 [建立和設定雲端服務組態資料夾的相關資訊](../../forms/using/configure-data-sources.md#cloud-folder) ，請參閱雲端服務組態設定資料夾。

1. 點選「 **[!UICONTROL 建立]** 」以開啟「 **[!UICONTROL 建立資料來源設定」精靈]**。 指定配置的名稱和（可選）標題，從「服務類型」下拉式清單中選擇 **[!UICONTROL RESTful Service]** ，或者瀏覽並選擇該配置的縮略圖，然後點選「 **[!UICONTROL 下一步]******」。
1. 為RESTful服務指定以下詳細資訊：

   * 從「Swagger來源」下拉式清單中選取「URL」或「檔案」，並據以指定Swagger定義檔案的Swagger URL，或從本機檔案系統上傳Swagger檔案。
   * 根據Swagger來源輸入，下列欄位會預先填入值：

      * 方案：REST API使用的傳輸通訊協定。 下拉式清單中顯示的方案類型數目取決於Swagger來源中定義的方案。
      * 主機：提供REST API的主機的域名或IP地址。 這是一個強制欄位。
      * 基本路徑：所有API路徑的URL首碼。 此欄位為選擇性欄位。\
         如有必要，請編輯這些欄位的預先填入值。
   * 選擇驗證類型— 無、OAuth2.0、基本驗證、API金鑰或自訂驗證— 訪問REST風格的服務，並相應地提供驗證的詳細資訊。
   如果您選 **[!UICONTROL 取API金鑰]** ，則請指定API金鑰的值。 API金鑰可以以請求標題或查詢參數的形式傳送。 從「位置」( **[!UICONTROL Location]** )下拉式清單中選取其中一個選項，並在「參數名稱」(Parameter Name)欄位中指定標題或查詢 **[!UICONTROL 參數的名稱]** 。

1. 點選 **[!UICONTROL 「建立]** 」以建立REST風格服務的雲端設定。

## 配置SOAP web services {#configure-soap-web-services}

使用網站服務描述語言( [WSDL)規格說明以SOAP為基礎的網站服務](https://www.w3.org/TR/wsdl)。 若要在AEM雲端服務中設定以SOAP為基礎的Web服務，請確定您擁有Web服務的WSDL URL，並執行下列動作：

1. 前往「 **[!UICONTROL 工具>雲端服務>資料來源」]**。 點選以選取您要建立雲端設定的檔案夾。

   如需 [建立和設定雲端服務組態資料夾的相關資訊](../../forms/using/configure-data-sources.md#cloud-folder) ，請參閱雲端服務組態設定資料夾。

1. 點選「 **[!UICONTROL 建立]** 」以開啟「 **[!UICONTROL 建立資料來源設定」精靈]**。 指定配置的名稱和標題（可選），從「服務類型」下拉式清單中選擇 **[!UICONTROL SOAP Web Service]** ，或者瀏覽並選擇配置的縮圖影像，然後點選「 **[!UICONTROL 下一步]******」。
1. 為SOAP web服務指定以下內容：

   * Web服務的WSDL URL。
   * 服務端點. 在此欄位中指定一個值，以覆蓋WSDL中提及的服務端點。
   * 選擇驗證類型— 無、OAuth2.0、基本驗證或自訂驗證— 存取SOAP服務，並據以提供驗證的詳細資訊。

1. 點選 **[!UICONTROL 「建立]** 」以建立SOAP網站服務的雲端設定。

## 配置OData服務 {#config-odata}

OData服務由其服務根URL標識。 若要在AEM雲端服務中設定OData服務，請確定您有服務的服務根URL，並執行下列動作：

>[!NOTE]
如需設定Microsoft Dynamics 365的逐步指南（線上或內部），請參閱 [Microsoft Dynamics OData設定](/help/forms/using/ms-dynamics-odata-configuration.md)。

1. 前往「 **[!UICONTROL 工具>雲端服務>資料來源」]**。 點選以選取您要建立雲端設定的檔案夾。

   如需 [建立和設定雲端服務組態資料夾的相關資訊](../../forms/using/configure-data-sources.md#cloud-folder) ，請參閱雲端服務組態設定資料夾。

1. 點選「 **[!UICONTROL 建立]** 」以開啟「 **[!UICONTROL 建立資料來源設定」精靈]**。 指定配置的名稱和（可選）標題，從「服務類型」下拉式清單中選擇 **[!UICONTROL OData Service]** ，或者瀏覽並選取該配置的縮圖影像，然後點選「 **[!UICONTROL 下一步]******」。
1. 為OData服務指定以下詳細資訊：

   * 要配置的OData服務的服務根URL。
   * 選擇驗證類型— 無、OAuth2.0、基本驗證或自訂驗證— 訪問OData服務，並相應地提供驗證的詳細資訊。
   >[!NOTE]
   您必須選擇OAuth 2.0驗證類型，以OData端點作為服務根目錄與Microsoft Dynamics服務連接。

1. 點選 **「建立** 」以建立OData服務的雲端設定。

## 後續步驟 {#next-steps}

您已設定資料來源。 接下來，您可以建立表單資料模型，或如果您已建立不含資料來源的表單資料模型，則可將其與您剛設定的資料來源建立關聯。 如需詳 [細資訊，請參閱建立表單資料模型](/help/forms/using/create-form-data-models.md) 。
