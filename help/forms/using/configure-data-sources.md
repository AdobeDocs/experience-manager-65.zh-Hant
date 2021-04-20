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
feature: Form Data Model
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2023'
ht-degree: 0%

---


# 設定資料來源{#configure-data-sources}

![](do-not-localize/data-integeration.png)

AEM Forms資料整合可讓您設定並連線至不同的資料來源。 下列類型是現成可用的支援。 不過，只需少量自訂，您也可以整合其他資料來源。

* 關係資料庫- MySQL、Microsoft SQL Server、IBM DB2和OracleRDBMS。
* AEM用戶配置檔案
* REST風格的Web服務
* 基於SOAP的web services
* OData服務

資料整合支援OAuth2.0、基本驗證和API金鑰驗證類型立即可用，並可實作自訂驗證以存取網站服務。 雖然RESTful、SOAP架構和OData服務已在AEM Cloud Services中設定，但Web主控台中會設定關係資料庫的JDBC和AEM使用者設定檔的連AEM接器。

## 配置關係資料庫{#configure-relational-database}

您可以使用Web控制台配置AEM配置關係資料庫。 請執行下列動作：

1. 請前往AEMhttps://server:host/system/console/configMgr的Web主控台。
1. 尋找&#x200B;**[!UICONTROL Apache Sling Connection Pooled DataSource]**&#x200B;組態。 點選以在編輯模式中開啟設定。
1. 在配置對話框中，指定要配置的資料庫的詳細資訊，例如：

   * 資料來源的名稱
   * 儲存資料源名稱的資料源服務屬性
   * JDBC驅動程式的Java類名
   * JDBC連接URI
   * 用於與JDBC驅動程式建立連接的用戶名和密碼

   >[!NOTE]
   >
   >在設定資料來源之前，請務必先加密機密資訊，例如密碼。 要加密：
   >
   >    
   >    
   >    1. 轉到https://&#39;[server]:[port]&#39;/system/console/crypto。
   >    1. 在&#x200B;**[!UICONTROL 純文字檔案]**&#x200B;欄位中，指定要加密的口令或任何字串，並點選&#x200B;**[!UICONTROL Protect]**。

   >    
   >    
   >    
   >加密的文字會出現在「受保護的文字」欄位中，您可在設定中指定。

1. 啟用「借用時測試」或「返回時測試」，以指定在分別從池借用或返回對象之前先驗證對象。********
1. 在&#x200B;**[!UICONTROL 驗證查詢]**&#x200B;欄位中指定SQL SELECT查詢，以驗證池中的連接。 查詢至少必須返回一行。 根據您的資料庫，指定下列其中一項：

   * 選擇1（MySQL和MS SQL）
   * 從雙(Oracle)中選擇1

1. 點選「**[!UICONTROL 儲存]**」以儲存設定。

## 配置AEM用戶配置檔案{#configure-aem-user-profile}

您可以使用AEMWeb Console中的「使用者描述檔連接器」設定來AEM設定使用者描述檔。 請執行下列動作：

1. 轉至AEMhttps://&#39;[server]的Web控制台：[port]&#39;system/console/configMgr。
1. 尋找&#x200B;**[!UICONTROL AEM Forms資料整合——使用者描述檔連接器組態]**，然後點選以在編輯模式中開啟組態。
1. 在「用戶配置檔案連接器配置」對話框中，可以添加、刪除或更新用戶配置檔案屬性。 指定的屬性將可用於表單資料模型中。 使用以下格式指定用戶配置檔案屬性：

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   範例：

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >上例中的&#x200B;*****&#x200B;表示CRXDE結構中用戶配置檔案中`profile/empLocation/`節點下AEM的所有節點。 這表示表單資料模型可以訪問`profile/empLocation/`節點下任何節點中存在的`city`類型`string`屬性。 但是，包含指定屬性的節點必須遵循一致的結構。

1. 點選「**[!UICONTROL 儲存]**」以儲存設定。

## 為雲端服務配置配置資料夾{#cloud-folder}

>[!NOTE]
為RESTful、SOAP和OData服務配置雲端服務時，需要配置雲端服務資料夾。

中的所有雲服務配AEM置都整合在儲存庫的`/conf`資料夾中AEM。 依預設，`conf`資料夾包含`global`資料夾，您可在其中建立雲端服務組態。 不過，您必須針對雲端組態手動啟用它。 您也可以在`conf`中建立其他資料夾，以建立並組織雲端服務組態。

要為雲端服務配置配置資料夾：

1. 前往&#x200B;**[!UICONTROL 工具>一般>組態瀏覽器]**。
   * 如需詳細資訊，請參閱[Configuration Browser](/help/sites-administering/configurations.md)檔案。
1. 請執行下列動作，為雲端設定啟用全域資料夾，或略過此步驟，為雲端服務設定建立並設定另一個資料夾。

   1. 在&#x200B;**[!UICONTROL 配置瀏覽器]**&#x200B;中，選擇`global`資料夾並按一下&#x200B;**[!UICONTROL 屬性]**。

   1. 在&#x200B;**[!UICONTROL 配置屬性]**&#x200B;對話框中，啟用&#x200B;**[!UICONTROL 雲配置]**。

   1. 點選&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;以儲存設定並退出對話方塊。

1. 在&#x200B;**[!UICONTROL 配置瀏覽器]**&#x200B;中，按一下&#x200B;**[!UICONTROL 建立]**。
1. 在&#x200B;**[!UICONTROL 建立設定]**&#x200B;對話方塊中，指定資料夾的標題並啟用&#x200B;**[!UICONTROL 雲端設定]**。
1. 點選「**[!UICONTROL 建立]**」以建立可用於雲端服務組態的資料夾。

## 配置REST風格的Web服務{#configure-restful-web-services}

REST風格的Web服務可在Swagger定義檔案中使用[Swagger規格](https://swagger.io/specification/)的JSON或YAML格式來說明。 若要在AEM雲端服務中設定REST風格的網站服務，請確定您的檔案系統上有Swagger檔案，或是檔案所在的URL。

執行以下操作以配置REST風格的服務：

1. 前往&#x200B;**[!UICONTROL 工具>Cloud Services>資料來源]**。 點選以選取您要建立雲端設定的檔案夾。

   如需建立和設定雲端服務組態資料夾的相關資訊，請參閱[設定雲端服務組態資料夾](../../forms/using/configure-data-sources.md#cloud-folder)。

1. 點選&#x200B;**[!UICONTROL Create]**&#x200B;以開啟&#x200B;**[!UICONTROL 建立資料來源設定精靈]**。 指定配置的名稱和可選的標題，從&#x200B;**[!UICONTROL 服務類型]**&#x200B;下拉式清單中選擇&#x200B;**[!UICONTROL RESTful Service]**，選擇瀏覽並選擇配置的縮略圖，然後點選&#x200B;**[!UICONTROL Next]**。
1. 為RESTful服務指定以下詳細資訊：

   * 從「Swagger來源」下拉式清單中選取「URL」或「檔案」，並據以指定Swagger定義檔案的Swagger URL，或從本機檔案系統上傳Swagger檔案。
   * 根據Swagger來源輸入，下列欄位會預先填入值：

      * 方案：REST API使用的傳輸通訊協定。 下拉式清單中顯示的方案類型數目取決於Swagger來源中定義的方案。
      * 主機：提供REST API的主機的域名或IP地址。 這是一個強制欄位。
      * 基本路徑：所有API路徑的URL首碼。 此欄位為選擇性欄位。\
         如有必要，請編輯這些欄位的預先填入值。
   * 選擇驗證類型— 無、OAuth2.0、基本驗證、API金鑰、自訂驗證或相互驗證— 訪問REST風格的服務，並相應地提供驗證的詳細資訊。

   如果您選擇&#x200B;**[!UICONTROL API金鑰]**&#x200B;作為驗證類型，請指定API金鑰的值。 API金鑰可以以請求標題或查詢參數的形式傳送。 從&#x200B;**[!UICONTROL 位置]**&#x200B;下拉式清單中選擇其中一個選項，並在&#x200B;**[!UICONTROL 參數名稱]**&#x200B;欄位中指定標題或查詢參數的名稱。

   如果選擇&#x200B;**[!UICONTROL 互相驗證]**&#x200B;作為驗證類型，請參見[基於證書的REST風格和SOAP Web服務](#mutual-authentication)。

1. 點選&#x200B;**[!UICONTROL Create]**&#x200B;以建立REST風格服務的雲端設定。

### 建立資料模型HTTP用戶端組態以最佳化效能{#fdm-http-client-configuration}

[!DNL Experience Manager Forms] 當與REST風格的Web服務整合作為資料源時，將形成資料模型，包括用於效能優化的HTTP客戶端配置。執行以下步驟來配置表單資料模型HTTP客戶端：

1. 以管理員身分登入「[!DNL Experience Manager Forms]作者例項」，並前往「[!DNL Experience Manager]網頁主控台組合」。 預設URL為[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。

1. 點選「**[!UICONTROL 表單資料模型Http用戶端設定」以取得REST資料來源]**。

1. 在[!UICONTROL 表單資料模型REST資料源的Http客戶端配置]對話框中：

   * 在&#x200B;**[!UICONTROL 總數]**&#x200B;欄位中的「連接限制」中，指定表單資料模型與REST風格Web服務之間允許的最大連接數。 預設值為20個連接。

   * 在&#x200B;**[!UICONTROL Connection limit on per route basis]**&#x200B;欄位中，指定每條路由允許的最大連接數。 預設值為2個連接。

   * 在&#x200B;**[!UICONTROL Keep alive]**&#x200B;欄位中，指定持續HTTP連線保持有效的持續時間。 預設值為15秒。

   * 在&#x200B;**[!UICONTROL 連接超時]**&#x200B;欄位中，指定[!DNL Experience Manager Forms]伺服器等待連接建立的持續時間。 預設值為10秒。

   * 在&#x200B;**[!UICONTROL 通訊端逾時]**&#x200B;欄位中，指定兩個資料封包之間未活動的最長時段。 預設值為30秒。


## 配置SOAP web services {#configure-soap-web-services}

使用[網站服務描述語言(WSDL)規範](https://www.w3.org/TR/wsdl)來說明以SOAP為基礎的網站服務。 若要在AEM雲端服務中設定以SOAP為基礎的Web服務，請確定您擁有Web服務的WSDL URL，並執行下列動作：

1. 前往&#x200B;**[!UICONTROL 工具>Cloud Services>資料來源]**。 點選以選取您要建立雲端設定的檔案夾。

   如需建立和設定雲端服務組態資料夾的相關資訊，請參閱[設定雲端服務組態資料夾](../../forms/using/configure-data-sources.md#cloud-folder)。

1. 點選&#x200B;**[!UICONTROL Create]**&#x200B;以開啟&#x200B;**[!UICONTROL 建立資料來源設定精靈]**。 指定配置的名稱和可選的標題，從&#x200B;**[!UICONTROL 服務類型]**&#x200B;下拉式清單中選擇&#x200B;**[!UICONTROL SOAP Web Service]**，選擇瀏覽並選擇配置的縮略圖，然後點選&#x200B;**[!UICONTROL Next]**。
1. 為SOAP Web服務指定以下內容：

   * Web服務的WSDL URL。
   * 服務端點. 在此欄位中指定一個值，以覆蓋WSDL中提及的服務端點。
   * 選擇驗證類型— 無、OAuth2.0、基本驗證、自訂驗證、X509 Token或相互驗證— 存取SOAP服務，並據以提供驗證的詳細資訊。

      如果您選擇&#x200B;**[!UICONTROL X509 Token]**&#x200B;作為驗證類型，請配置X509證書。 如需詳細資訊，請參閱[設定憑證](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service)。
在**[!UICONTROL 鍵別名]**&#x200B;欄位中為X509證書指定KeyStore別名。 在&#x200B;**[!UICONTROL 即時時間]**&#x200B;欄位中，指定驗證要求保持有效的時間（以秒為單位）。 （可選）選擇簽署消息正文或時間戳標題或兩者。

      如果選擇&#x200B;**[!UICONTROL 互相驗證]**&#x200B;作為驗證類型，請參見[基於證書的REST風格和SOAP Web服務](#mutual-authentication)。

1. 點選「**[!UICONTROL 建立]**」以建立SOAP網站服務的雲端設定。

## 配置OData服務{#config-odata}

OData服務由其服務根URL標識。 若要在AEM雲端服務中設定OData服務，請確定您有服務的服務根URL，並執行下列動作：

>[!NOTE]
有關配置Microsoft Dynamics 365的逐步指南（線上或內部），請參閱[Microsoft Dynamics OData Configuration](/help/forms/using/ms-dynamics-odata-configuration.md)。

1. 前往&#x200B;**[!UICONTROL 工具>Cloud Services>資料來源]**。 點選以選取您要建立雲端設定的檔案夾。

   如需建立和設定雲端服務組態資料夾的相關資訊，請參閱[設定雲端服務組態資料夾](../../forms/using/configure-data-sources.md#cloud-folder)。

1. 點選&#x200B;**[!UICONTROL Create]**&#x200B;以開啟&#x200B;**[!UICONTROL 建立資料來源設定精靈]**。 指定配置的名稱和可選標題，從&#x200B;**[!UICONTROL 服務類型]**&#x200B;下拉式清單中選擇&#x200B;**[!UICONTROL OData服務]**，選擇瀏覽並選擇配置的縮略圖，然後點選&#x200B;**[!UICONTROL Next]**。
1. 為OData服務指定以下詳細資訊：

   * 要配置的OData服務的服務根URL。
   * 選擇驗證類型— 無、OAuth2.0、基本驗證或自訂驗證— 訪問OData服務，並相應地提供驗證的詳細資訊。

   >[!NOTE]
   您必須選擇OAuth 2.0驗證類型，以OData端點作為服務根目錄與Microsoft Dynamics服務連接。

1. 點選&#x200B;**Create**&#x200B;以建立OData服務的雲端設定。

## 針對RESTful和SOAP web services {#mutual-authentication}的憑證式相互驗證

當您啟用表單資料模型的相互驗證時，執行表單資料模型的資料來源和伺服器會先驗證彼此的身分，然後才會共用任何資料。 您可以對基於REST和SOAP的連接（資料源）使用相互驗證。 要在您的AEM Forms環境中為表單資料模型配置相互身份驗證：

1. 將私密金鑰（憑證）上傳至[!DNL AEM Forms]伺服器。 要上傳私密金鑰：
   1. 以管理員身份登錄到您的[!DNL AEM Forms]伺服器。
   1. 導覽至「**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]**」。 選擇`fd-cloudservice`用戶，然後點選&#x200B;**[!UICONTROL 屬性]**。
   1. 開啟&#x200B;**[!UICONTROL Keystore]**&#x200B;標籤，展開&#x200B;**[!UICONTROL 從KeyStore檔案]**&#x200B;新增私密金鑰選項，上傳KeyStore檔案，指定別名、密碼，並點選&#x200B;**[!UICONTROL Submit]**。 憑證已上傳。  私鑰別名在證書中提及，在建立證書時設定。
1. 上傳信任憑證至全域信任商店。 若要上傳憑證：
   1. 導覽至「**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 信任商店]**」。
   1. 展開&#x200B;**[!UICONTROL 從CER檔案]**&#x200B;添加證書選項，按一下&#x200B;**[!UICONTROL 選擇證書檔案]** ，上傳證書，然後按一下&#x200B;**[!UICONTROL 提交]**。
1. 將[SOAP](#configure-soap-web-services)或[RESTful](#configure-restful-web-services) web services配置為資料源，並選擇&#x200B;**[!UICONTROL Mutual authentication]**&#x200B;作為驗證類型。 如果為`fd-cloudservice`用戶配置多個自簽名證書，請指定證書的「密鑰別名」。

## 後續步驟{#next-steps}

您已設定資料來源。 接下來，您可以建立表單資料模型，或如果您已建立不含資料來源的表單資料模型，則可將其與您剛設定的資料來源建立關聯。 如需詳細資訊，請參閱[建立表單資料模型](/help/forms/using/create-form-data-models.md)。
