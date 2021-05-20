---
title: 設定資料來源
seo-title: 設定資料來源
description: 了解如何設定不同類型的資料來源，並運用來建立表單資料模型。
seo-description: 了解如何設定不同類型的資料來源，並運用來建立表單資料模型。
uuid: 12360c8c-b596-4f9b-837a-10a8ff5c7448
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9d78a6dc-fc9c-415b-b817-164fe6648b30
docset: aem65
feature: 表單資料模型
exl-id: 7a1d9d57-66f4-4f20-91c2-ace5a71a52f2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2023'
ht-degree: 0%

---

# 配置資料源{#configure-data-sources}

![](do-not-localize/data-integeration.png)

AEM Forms資料整合可讓您設定並連線至不同的資料來源。 下列類型可立即使用。 不過，只要很少自訂，您也可以整合其他資料來源。

* 關係資料庫 — MySQL、Microsoft SQL Server、IBM DB2和OracleRDBMS。
* AEM使用者設定檔
* RESTful Web服務
* 基於SOAP的Web服務
* OData服務

資料整合支援OAuth2.0、基本驗證和API金鑰驗證類型，且可立即使用，並可實作自訂驗證以存取網站服務。 雖然AEM雲端服務中已設定RESTful、SOAP型和OData服務，但AEM web主控台中已設定關係資料庫的JDBC和AEM使用者設定檔的連接器。

## 配置關係資料庫{#configure-relational-database}

您可以使用AEM Web控制台配置配置關係資料庫。 請執行下列動作：

1. 前往AEM Web主控台，網址為https://server:host/system/console/configMgr 。
1. 尋找&#x200B;**[!UICONTROL Apache Sling Connection Pooled DataSource]**&#x200B;設定。 點選以在編輯模式中開啟設定。
1. 在配置對話框中，指定要配置的資料庫的詳細資訊，例如：

   * 資料源的名稱
   * 儲存資料源名稱的資料源服務屬性
   * JDBC驅動程式的Java類名
   * JDBC連接URI
   * 用於建立與JDBC驅動程式連接的用戶名和口令

   >[!NOTE]
   >
   >在配置資料源之前，請確保加密密碼等敏感資訊。 要加密：
   >
   >    
   >    
   >    1. 轉到https://&#39;[server]:[port]&#39;/system/console/crypto。
   >    1. 在&#x200B;**[!UICONTROL 純文字]**&#x200B;欄位中，指定要加密的密碼或任何字串，並點選&#x200B;**[!UICONTROL Protect]**。

   >    
   >    
   >    
   >加密的文字會顯示在「受保護的文字」欄位中，您可以在配置中指定該欄位。

1. 啟用&#x200B;**[!UICONTROL 借用時測試]**&#x200B;或&#x200B;**[!UICONTROL 回訪時測試]** ，以指定在借用對象之前，或從和返回到池中，分別驗證對象。
1. 在&#x200B;**[!UICONTROL 驗證查詢]**&#x200B;欄位中指定SQL SELECT查詢，以驗證池中的連接。 查詢必須至少返回一行。 根據您的資料庫，指定下列任一項：

   * 選擇1（MySQL和MS SQL）
   * 從雙(Oracle)中選擇1

1. 點選&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存設定。

## 配置AEM用戶配置檔案{#configure-aem-user-profile}

您可以使用AEM Web Console中的「使用者設定檔連接器」設定來設定AEM使用者設定檔。 請執行下列動作：

1. 前往AEM Web主控台，網址為https://&#39;[server]:[port]&#39;system/console/configMgr。
1. 尋找&#x200B;**[!UICONTROL AEM Forms資料整合 — 使用者設定檔連接器組態]**，然後點選以在編輯模式中開啟組態。
1. 在「用戶配置檔案連接器配置」對話框中，可以添加、刪除或更新用戶配置檔案屬性。 指定的屬性將可用於表單資料模型。 使用以下格式指定用戶配置檔案屬性：

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   範例：

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >上例中的&#x200B;*****&#x200B;表示CRXDE結構中AEM用戶配置檔案中`profile/empLocation/`節點下的所有節點。 這表示表單資料模型可以存取`profile/empLocation/`節點下任何節點中出現的`string`類型的`city`屬性。 但是，包含指定屬性的節點必須遵循一致的結構。

1. 點選&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存設定。

## 配置雲服務配置的資料夾{#cloud-folder}

>[!NOTE]
為RESTful、SOAP和OData服務配置雲服務時，需要配置雲服務資料夾。

AEM中的所有雲端服務設定皆整合至AEM存放庫的`/conf`資料夾中。 依預設，`conf`資料夾包含您可建立雲端服務設定的`global`資料夾。 不過，您必須為雲端設定手動啟用此功能。 您也可以在`conf`中建立其他資料夾，以建立和組織雲端服務設定。

要配置雲端服務配置的資料夾：

1. 前往「**[!UICONTROL 工具>一般>設定瀏覽器]**」。
   * 如需詳細資訊，請參閱[設定瀏覽器](/help/sites-administering/configurations.md)檔案。
1. 請執行下列操作以啟用雲配置的全局資料夾，或跳過此步驟以建立和配置雲服務配置的其他資料夾。

   1. 在&#x200B;**[!UICONTROL Configuration Browser]**&#x200B;中，選擇`global`資料夾，然後點選&#x200B;**[!UICONTROL Properties]**。

   1. 在&#x200B;**[!UICONTROL 配置屬性]**&#x200B;對話框中，啟用&#x200B;**[!UICONTROL 雲配置]**。

   1. 點選&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;以儲存設定並退出對話方塊。

1. 在「**[!UICONTROL 設定瀏覽器]**」中，點選「**[!UICONTROL 建立]**」。
1. 在&#x200B;**[!UICONTROL 建立配置]**&#x200B;對話框中，指定資料夾的標題並啟用&#x200B;**[!UICONTROL 雲配置]**。
1. 點選&#x200B;**[!UICONTROL 建立]**&#x200B;以建立為雲端服務設定啟用的資料夾。

## 配置RESTful Web服務{#configure-restful-web-services}

RESTful Web服務可使用JSON的[Swagger規範](https://swagger.io/specification/)或Swagger定義檔案的YAML格式描述。 若要在AEM雲端服務中設定RESTful Web服務，請確定您的檔案系統上有Swagger檔案，或檔案托管所在的URL。

請執行以下操作來配置RESTful服務：

1. 前往「**[!UICONTROL 工具>Cloud Services>資料來源]**」。 點選以選取您要建立雲端設定的資料夾。

   如需建立和設定雲端服務設定資料夾的相關資訊，請參閱[設定雲端服務設定資料夾](../../forms/using/configure-data-sources.md#cloud-folder) 。

1. 點選&#x200B;**[!UICONTROL Create]**&#x200B;以開啟&#x200B;**[!UICONTROL Create Data Source Configuration精靈]**。 指定配置的名稱和可選的標題，從&#x200B;**[!UICONTROL 服務類型]**&#x200B;下拉清單中選擇&#x200B;**[!UICONTROL RESTful服務]**，選擇瀏覽並選擇配置的縮略圖，然後點選&#x200B;**[!UICONTROL 下一步]**。
1. 為RESTful服務指定以下詳細資訊：

   * 從「Swagger來源」下拉式清單中選取「URL」或「檔案」，並據此指定Swagger URL至Swagger定義檔案，或從本機檔案系統上傳Swagger檔案。
   * 根據Swagger來源輸入，下列欄位會預先填入值：

      * 方案：REST API使用的傳輸通訊協定。 下拉式清單中顯示的配置類型數目取決於Swagger來源中定義的配置。
      * 主機：提供REST API之主機的網域名稱或IP位址。 這是必填欄位。
      * 基本路徑：所有API路徑的URL首碼。 此為選用欄位。\
         如有必要，請編輯這些欄位的預先填入值。
   * 選擇身份驗證類型（無、OAuth2.0、基本身份驗證、API密鑰、自定義身份驗證或相互身份驗證）以訪問RESTful服務，並相應地提供身份驗證的詳細資訊。

   如果您選取&#x200B;**[!UICONTROL API金鑰]**&#x200B;作為驗證類型，請指定API金鑰的值。 API金鑰可以以要求標題或查詢參數的形式傳送。 從&#x200B;**[!UICONTROL Location]**&#x200B;下拉清單中選擇以下選項之一，並在&#x200B;**[!UICONTROL Parameter Name]**&#x200B;欄位中相應地指定標題的名稱或查詢參數。

   如果選擇&#x200B;**[!UICONTROL 相互身份驗證]**&#x200B;作為身份驗證類型，請參閱[基於證書的RESTful和SOAP Web服務的相互身份驗證](#mutual-authentication)。

1. 點選&#x200B;**[!UICONTROL 建立]**&#x200B;以建立RESTful服務的雲配置。

### 表單資料模型HTTP用戶端配置，以最佳化效能{#fdm-http-client-configuration}

[!DNL Experience Manager Forms] 表單資料模型與RESTful網站服務整合時，作為資料來源時包含HTTP用戶端設定，以最佳化效能。執行下列步驟來設定表單資料模型HTTP用戶端：

1. 以管理員身分登入[!DNL Experience Manager Forms]製作執行個體，並前往[!DNL Experience Manager] Web主控台套件組合。 預設URL為[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。

1. 點選&#x200B;**[!UICONTROL 表單資料模型Http用戶端設定以取得REST資料來源]**。

1. 在[!UICONTROL Form Data Model Http Client Configuration for REST data source]對話方塊中：

   * 在&#x200B;**[!UICONTROL 總計]**&#x200B;欄位中的連接限制中，指定表單資料模型與RESTful Web服務之間允許的連接數上限。 預設值為20個連線。

   * 在&#x200B;**[!UICONTROL Connection limit on per route basis]**&#x200B;欄位中，指定每條路由允許的最大連接數。 預設值為2個連線。

   * 在&#x200B;**[!UICONTROL Keep alive]**&#x200B;欄位中，指定持續HTTP連線保持運作的持續時間。 預設值為15秒。

   * 在&#x200B;**[!UICONTROL 連線逾時]**&#x200B;欄位中，指定[!DNL Experience Manager Forms]伺服器等待連線建立的持續時間。 預設值為10秒。

   * 在&#x200B;**[!UICONTROL 通訊端逾時]**&#x200B;欄位中，指定兩個資料封包之間未活動的最長時間。 預設值為30秒。


## 配置SOAP Web服務{#configure-soap-web-services}

使用[Web服務描述語言(WSDL)規範](https://www.w3.org/TR/wsdl)描述基於SOAP的Web服務。 若要在AEM雲端服務中設定以SOAP為基礎的網站服務，請確定您有網站服務的WSDL URL，並執行下列動作：

1. 前往「**[!UICONTROL 工具>Cloud Services>資料來源]**」。 點選以選取您要建立雲端設定的資料夾。

   如需建立和設定雲端服務設定資料夾的相關資訊，請參閱[設定雲端服務設定資料夾](../../forms/using/configure-data-sources.md#cloud-folder) 。

1. 點選&#x200B;**[!UICONTROL Create]**&#x200B;以開啟&#x200B;**[!UICONTROL Create Data Source Configuration精靈]**。 指定配置的名稱和可選的標題，從&#x200B;**[!UICONTROL 服務類型]**&#x200B;下拉清單中選擇&#x200B;**[!UICONTROL SOAP Web Service]**，選擇瀏覽並選擇配置的縮略圖，然後點選&#x200B;**[!UICONTROL Next]**。
1. 為SOAP Web服務指定以下內容：

   * Web服務的WSDL URL。
   * 服務端點. 在此欄位中指定一個值，以覆蓋WSDL中提及的服務端點。
   * 選取驗證類型（無、OAuth2.0、基本驗證、自訂驗證、X509代號或相互驗證）以存取SOAP服務，並據此提供驗證的詳細資訊。

      如果選擇&#x200B;**[!UICONTROL X509 Token]**&#x200B;作為驗證類型，請配置X509證書。 如需詳細資訊，請參閱[設定憑證](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service)。
在**[!UICONTROL 密鑰別名]**&#x200B;欄位中指定X509證書的KeyStore別名。 在&#x200B;**[!UICONTROL 存留時間]**&#x200B;欄位中指定驗證請求保持有效的時間（以秒為單位）。 （可選）選擇簽署消息正文或時間戳標頭或兩者。

      如果選擇&#x200B;**[!UICONTROL 相互身份驗證]**&#x200B;作為身份驗證類型，請參閱[基於證書的RESTful和SOAP Web服務的相互身份驗證](#mutual-authentication)。

1. 點選&#x200B;**[!UICONTROL 建立]**&#x200B;以建立SOAP網站服務的雲配置。

## 配置OData服務{#config-odata}

OData服務由其服務根URL識別。 若要在AEM雲端服務中設定OData服務，請確定您有服務的服務根URL，並執行下列操作：

>[!NOTE]
有關配置Microsoft Dynamics 365的線上或內部部署的逐步指南，請參閱[Microsoft Dynamics OData配置](/help/forms/using/ms-dynamics-odata-configuration.md)。

1. 前往「**[!UICONTROL 工具>Cloud Services>資料來源]**」。 點選以選取您要建立雲端設定的資料夾。

   如需建立和設定雲端服務設定資料夾的相關資訊，請參閱[設定雲端服務設定資料夾](../../forms/using/configure-data-sources.md#cloud-folder) 。

1. 點選&#x200B;**[!UICONTROL Create]**&#x200B;以開啟&#x200B;**[!UICONTROL Create Data Source Configuration精靈]**。 指定配置的名稱和可選的標題，從&#x200B;**[!UICONTROL 服務類型]**&#x200B;下拉清單中選擇&#x200B;**[!UICONTROL OData服務]**，選擇瀏覽並選擇配置的縮略圖，然後點選&#x200B;**[!UICONTROL Next]**。
1. 指定OData服務的以下詳細資訊：

   * 要配置的OData服務的服務根URL。
   * 選擇身份驗證類型（無、OAuth2.0、基本身份驗證或自定義身份驗證）以訪問OData服務，並相應地提供身份驗證的詳細資訊。

   >[!NOTE]
   必須選擇OAuth 2.0身份驗證類型，以OData端點作為服務根連接到Microsoft Dynamics服務。

1. 點選&#x200B;**建立**&#x200B;以建立OData服務的雲配置。

## RESTful和SOAP Web服務{#mutual-authentication}的基於證書的相互驗證

當您為表單資料模型啟用相互驗證時，執行表單資料模型的資料來源和AEM Server會先驗證彼此的身分，再共用任何資料。 您可以對REST和SOAP連線（資料來源）使用相互驗證。 若要在AEM Forms環境中為表單資料模型設定相互驗證：

1. 上傳私密金鑰（憑證）至[!DNL AEM Forms]伺服器。 上傳私密金鑰：
   1. 以管理員身分登入您的[!DNL AEM Forms]伺服器。
   1. 導覽至&#x200B;**[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**。 選取`fd-cloudservice`使用者，然後點選&#x200B;**[!UICONTROL 屬性]**。
   1. 開啟&#x200B;**[!UICONTROL 金鑰存放區]**&#x200B;標籤，展開&#x200B;**[!UICONTROL 從KeyStore檔案]**&#x200B;新增私密金鑰選項，上傳KeyStore檔案，指定別名、密碼，然後點選&#x200B;**[!UICONTROL 提交]**。 已上傳憑證。  私鑰別名在證書中提及，並在建立證書時設定。
1. 上傳信任證書到全局信任儲存。 上傳憑證：
   1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 信任存放區]**。
   1. 展開&#x200B;**[!UICONTROL 從CER檔案]**&#x200B;添加證書選項，點選&#x200B;**[!UICONTROL 選擇證書檔案]**，上傳證書，點選&#x200B;**[!UICONTROL 提交]**。
1. 將[SOAP](#configure-soap-web-services)或[RESTful](#configure-restful-web-services) Web服務配置為資料源，並選擇&#x200B;**[!UICONTROL 相互身份驗證]**&#x200B;作為身份驗證類型。 如果為`fd-cloudservice`用戶配置多個自簽名證書，請指定證書的密鑰別名。

## 後續步驟 {#next-steps}

您已設定資料來源。 接下來，您可以建立表單資料模型，或者如果您已建立表單資料模型而不使用資料來源，則可將其與您剛設定的資料來源建立關聯。 如需詳細資訊，請參閱[建立表單資料模型](/help/forms/using/create-form-data-models.md)。
