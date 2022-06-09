---
title: 設定資料來源
seo-title: Configure data sources
description: 瞭解如何配置不同類型的資料源並利用它們建立表單資料模型。
seo-description: Learn how to configure different types of data sources and leverage to create form data models.
uuid: 12360c8c-b596-4f9b-837a-10a8ff5c7448
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9d78a6dc-fc9c-415b-b817-164fe6648b30
docset: aem65
feature: Form Data Model
exl-id: 7a1d9d57-66f4-4f20-91c2-ace5a71a52f2
source-git-commit: 98854fa3b852f511cf95adc13b945c06b1afff96
workflow-type: tm+mt
source-wordcount: '2011'
ht-degree: 1%

---

# 設定資料來源{#configure-data-sources}

![](do-not-localize/data-integeration.png)

AEM Forms資料整合允許您配置和連接到不同的資料源。 支援開箱即用的以下類型。 但是，只需少量自定義，您也可以整合其他資料源。

* 關係資料庫 — MySQL、MicrosoftSQL Server、IBMDB2、OracleRDBMS和Sybase
* AEM用戶配置檔案
* REST風格的Web服務
* 基於SOAP的Web服務
* OData服務

資料整合支援OAuth2.0、基本身份驗證和API密鑰身份驗證類型的開箱即用，並允許為訪問Web服務實施自定義身份驗證。 在AEM雲服務中配置RESTful、基於SOAP和OData服務時，在Web控制台中配置關係資料庫的JDBC和AEM用戶配置檔案的連接AEM器。

## 配置關係資料庫 {#configure-relational-database}

可以使用Web控制台配AEM置配置關係資料庫。 請執行下列動作：

1. 請轉AEM至https://server:host/system/console/configMgr。
1. 查找 **[!UICONTROL Apache Sling連接池化資料源]** 配置。 按一下以在編輯模式下開啟配置。
1. 在「配置」對話框中，指定要配置的資料庫的詳細資訊，如：

   * 資料源的名稱
   * 儲存資料源名稱的資料源服務屬性
   * JDBC驅動程式的Java類名
   * JDBC連接URI
   * 用於建立與JDBC驅動程式連接的用戶名和密碼

   >[!NOTE]
   >
   >在配置資料源之前，請確保加密密碼等敏感資訊。 要加密：
   >
   >    
   >    
   >    1. 請訪問https://&#39;[伺服器]:[埠]「/system/console/crypto。
   >    1. 在 **[!UICONTROL 純文字檔案]** 欄位，指定要加密和點擊的密碼或任何字串 **[!UICONTROL Protect]**。

   >    
   >    
   >    
   >加密的文本將顯示在「受保護的文本」欄位中，您可以在配置中指定該欄位。

1. 啟用 **[!UICONTROL Test借用]** 或 **[!UICONTROL Test返回]** 指定在分別從池和池中借入或返回對象之前驗證對象。
1. 在 **[!UICONTROL 驗證查詢]** 欄位以驗證來自池的連接。 查詢必須至少返回一行。 根據您的資料庫，指定以下選項之一：

   * 選擇1（MySQL和MS SQL）
   * 從雙(Oracle)中選擇1

1. 點擊 **[!UICONTROL 保存]** 的子菜單。

## 配置AEM用戶配置檔案 {#configure-aem-user-profile}

可以在Web控AEM制台中使用用戶配置檔案連接器配AEM置用戶配置檔案。 請執行下列動作：

1. 請訪問AEMWeb控制台，網址為https://&#39;[伺服器]:[埠]&#39;system/console/configMgr。
1. 查找 **[!UICONTROL AEM Forms資料整合 — 用戶配置檔案連接器配置]** 並點擊以編輯模式開啟配置。
1. 在「用戶配置檔案連接器配置」對話框中，可以添加、刪除或更新用戶配置檔案屬性。 指定的屬性將可用於表單資料模型。 使用以下格式指定用戶配置檔案屬性：

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   範例：

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >的 **&#42;** 在上例中，表示 `profile/empLocation/` CRXDE結構中AEM的用戶配置檔案中的節點。 表單資料模型可以訪問 `city` 類型屬性 `string` 位於下面的任何節點中 `profile/empLocation/` 的下界。 但是，包含指定屬性的節點必須遵循一致的結構。

1. 點擊 **[!UICONTROL 保存]** 的子菜單。

## 為雲服務配置配置資料夾 {#cloud-folder}

>[!NOTE]
>
>配置RESTful、SOAP和OData服務的雲服務需要配置雲服務資料夾。

中的所有雲服務配AEM置都整合到 `/conf` 檔案AEM夾。 預設情況下， `conf` 資料夾包含 `global` 建立雲服務配置的資料夾。 但是，您需要為雲配置手動啟用它。 您也可以在 `conf` 建立和組織雲服務配置。

要為雲服務配置配置資料夾：

1. 轉到 **[!UICONTROL 工具>常規>配置瀏覽器]**。
   * 查看 [配置瀏覽器](/help/sites-administering/configurations.md) 的子菜單。
1. 執行以下操作以啟用雲配置的全局資料夾，或跳過此步驟為雲服務配置建立和配置另一個資料夾。

   1. 在 **[!UICONTROL 配置瀏覽器]**，選擇 `global` 資料夾和點擊 **[!UICONTROL 屬性]**。

   1. 在 **[!UICONTROL 配置屬性]** 對話框，啟用 **[!UICONTROL 雲配置]**。

   1. 點擊 **[!UICONTROL 保存並關閉]** 以保存配置並退出對話框。

1. 在 **[!UICONTROL 配置瀏覽器]**&#x200B;按一下 **[!UICONTROL 建立]**。
1. 在 **[!UICONTROL 建立配置]** 對話框，指定資料夾的標題並啟用 **[!UICONTROL 雲配置]**。
1. 點擊 **[!UICONTROL 建立]** 建立為雲服務配置啟用的資料夾。

## 配置REST風格的Web服務 {#configure-restful-web-services}

可使用 [Swagger規格](https://swagger.io/specification/) JSON或YAML格式的Swagger定義檔案。 要在AEM雲服務中配置REST風格的Web服務，請確保檔案系統上有Swagger檔案或檔案托管的URL。

執行以下操作以配置REST風格的服務：

1. 轉到 **[!UICONTROL 工具>Cloud Services>資料源]**。 點擊以選擇要在其中建立雲配置的資料夾。

   請參閱 [為雲服務配置配置資料夾](../../forms/using/configure-data-sources.md#cloud-folder) 有關為雲服務配置建立和配置資料夾的資訊。

1. 點擊 **[!UICONTROL 建立]** 開啟 **[!UICONTROL 建立資料源配置嚮導]**。 指定配置的名稱和標題（可選），選擇 **[!UICONTROL REST風格服務]** 從 **[!UICONTROL 服務類型]** 下拉，（可選）瀏覽並選擇配置的縮略圖，然後點擊 **[!UICONTROL 下一個]**。
1. 為RESTful服務指定以下詳細資訊：

   * 從「Swagger源」下拉清單中選擇「URL」或「檔案」，並相應地指定「Swagger URL」到「Swagger定義」檔案，或從本地檔案系統上載「Swagger檔案」。
   * 根據Swagger源輸入，以下欄位預填充了值：

      * 方案：REST API使用的傳輸協定。 在下拉清單中顯示的方案類型數取決於在Swagger源中定義的方案。
      * 主機：為REST API提供服務的主機的域名或IP地址。 這是一個強制欄位。
      * 基本路徑：所有API路徑的URL前置詞。 它是一個可選欄位。\
         如有必要，請編輯這些欄位的預填充值。
   * 選擇身份驗證類型（無）、OAuth2.0、基本身份驗證、API密鑰、自定義身份驗證或相互身份驗證)以訪問REST風格的服務，並相應地提供身份驗證的詳細資訊。

   如果選擇 **[!UICONTROL API密鑰]** 作為驗證類型，指定API密鑰的值。 API密鑰可以作為請求頭或查詢參數發送。 從 **[!UICONTROL 位置]** 下拉清單，並在 **[!UICONTROL 參數名稱]** 欄位。

   如果選擇 **[!UICONTROL 相互驗證]** 作為驗證類型，請參見 [基於證書的RESTful和SOAP Web服務的相互身份驗證](#mutual-authentication)。

1. 點擊 **[!UICONTROL 建立]** 為REST風格服務建立雲配置。

### 表單資料模型HTTP客戶端配置以優化效能 {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] 當與REST風格的Web服務整合為資料源時，將形成資料模型，包括用於效能優化的HTTP客戶端配置。
執行以下步驟來配置表單資料模型HTTP客戶端：

1. 登錄到 [!DNL Experience Manager Forms] 以管理員身份建立實例並轉到 [!DNL Experience Manager] web控制台捆綁包。 預設URL為 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。

1. 點擊 **[!UICONTROL REST資料源的表單資料模型HTTP客戶端配置]**。

1. 在 [!UICONTROL REST資料源的表單資料模型HTTP客戶端配置] 對話框：

   * 指定表單資料模型和REST風格Web服務之間允許的最大連接數 **[!UICONTROL 連接限制總數]** 的子菜單。 預設值為20個連接。

   * 指定中每個路由允許的最大連接數 **[!UICONTROL 每個路由的連接限制]** 的子菜單。 預設值為2個連接。

   * 指定持續HTTP連接保持活動的持續時間， **[!UICONTROL 保持活力]** 的子菜單。 預設值為15秒。

   * 指定持續時間， [!DNL Experience Manager Forms] 伺服器等待建立連接，在 **[!UICONTROL 連接超時]** 的子菜單。 預設值為10秒。

   * 指定中兩個資料包之間不活動的最大時間段 **[!UICONTROL 套接字超時]** 的子菜單。 預設值為30秒。


## 配置SOAP Web服務 {#configure-soap-web-services}

使用 [Web服務描述語言(WSDL)規範](https://www.w3.org/TR/wsdl)。 要在AEM雲服務中配置基於SOAP的Web服務，請確保您具有Web服務的WSDL URL，並執行以下操作：

1. 轉到 **[!UICONTROL 工具>Cloud Services>資料源]**。 點擊以選擇要在其中建立雲配置的資料夾。

   請參閱 [為雲服務配置配置資料夾](../../forms/using/configure-data-sources.md#cloud-folder) 有關為雲服務配置建立和配置資料夾的資訊。

1. 點擊 **[!UICONTROL 建立]** 開啟 **[!UICONTROL 建立資料源配置嚮導]**。 指定配置的名稱和標題（可選），選擇 **[!UICONTROL SOAP Web服務]** 從 **[!UICONTROL 服務類型]** 下拉，（可選）瀏覽並選擇配置的縮略圖，然後點擊 **[!UICONTROL 下一個]**。
1. 為SOAP Web服務指定以下內容：

   * Web服務的WSDL URL。
   * 服務端點. 在此欄位中指定值以覆蓋WSDL中提及的服務端點。
   * 選擇身份驗證類型 — 無、OAuth2.0、基本身份驗證、自定義身份驗證、X509令牌或相互身份驗證 — 以訪問SOAP服務，並相應地提供身份驗證的詳細資訊。

      如果選擇 **[!UICONTROL X509令牌]** 作為「Authentication type（驗證類型）」 ，配置X509證書。 有關詳細資訊，請參見 [設定證書](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service)。
在中為X509證書指定KeyStore別名 **[!UICONTROL 密鑰別名]** 的子菜單。 指定驗證請求保持有效的時間（秒）。 **[!UICONTROL 活到]** 的子菜單。 （可選）選擇以簽名消息正文或時間戳標頭或兩者。

      如果選擇 **[!UICONTROL 相互驗證]** 作為驗證類型，請參見 [基於證書的RESTful和SOAP Web服務的相互身份驗證](#mutual-authentication)。

1. 點擊 **[!UICONTROL 建立]** 為SOAP web服務建立雲配置。

## 配置OData服務 {#config-odata}

OData服務由其服務根URL標識。 要在AEM雲服務中配置OData服務，請確保您具有該服務的服務根URL，並執行以下操作：

>[!NOTE]
>
> 表單資料模型支援 [OData版本4](https://www.odata.org/documentation/)。
>有關配置MicrosoftDynamics 365的分步指南，請參見 [MicrosoftDynamics OData配置](/help/forms/using/ms-dynamics-odata-configuration.md)。

1. 轉到 **[!UICONTROL 工具>Cloud Services>資料源]**。 點擊以選擇要在其中建立雲配置的資料夾。

   請參閱 [為雲服務配置配置資料夾](../../forms/using/configure-data-sources.md#cloud-folder) 有關為雲服務配置建立和配置資料夾的資訊。

1. 點擊 **[!UICONTROL 建立]** 開啟 **[!UICONTROL 建立資料源配置嚮導]**。 指定配置的名稱和標題（可選），選擇 **[!UICONTROL OData服務]** 從 **[!UICONTROL 服務類型]** 下拉，（可選）瀏覽並選擇配置的縮略圖，然後點擊 **[!UICONTROL 下一個]**。
1. 為OData服務指定以下詳細資訊：

   * 要配置的OData服務的服務根URL。
   * 選擇身份驗證類型（無）、OAuth2.0、基本身份驗證或自定義身份驗證)以訪問OData服務，並相應地提供身份驗證的詳細資訊。

   >[!NOTE]
   >
   >必須選擇OAuth 2.0身份驗證類型，才能使用OData終結點作為服務根連接MicrosoftDynamics服務。

1. 點擊 **建立** 為OData服務建立雲配置。

## 基於證書的RESTful和SOAP Web服務的相互身份驗證 {#mutual-authentication}

當您為表單資料模型啟用相互身份驗證時，運行表單資料模型AEM的資料源和伺服器在共用任何資料之前都會對彼此的身份進行身份驗證。 可以對基於REST和SOAP的連接（資料源）使用相互身份驗證。 要在AEM Forms環境上為表單資料模型配置相互身份驗證：

1. 將私鑰（證書）上載到 [!DNL AEM Forms] 伺服器。 上載私鑰：
   1. 登錄到 [!DNL AEM Forms] 伺服器作為管理員。
   1. 導航到 **[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 用戶]**。 選擇 `fd-cloudservice` 用戶和點擊 **[!UICONTROL 屬性]**。
   1. 開啟 **[!UICONTROL 密鑰庫]** 的 **[!UICONTROL 從KeyStore檔案添加私鑰]** 選項，上載KeyStore檔案，指定別名、密碼，然後點擊 **[!UICONTROL 提交]**。 證書已上載。  在證書中提到私鑰別名，並在建立證書時設定。
1. 將信任證書上載到全局信任儲存。 要上載證書：
   1. 導航到 **[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 信任儲存]**。
   1. 展開 **[!UICONTROL 從CER檔案添加證書]** 選項，點擊 **[!UICONTROL 選擇證書檔案]**，上載證書，然後點擊 **[!UICONTROL 提交]**。
1. 配置 [SOAP](#configure-soap-web-services) 或 [REST風格](#configure-restful-web-services) Web服務作為資料源並選擇 **[!UICONTROL 相互驗證]** 類型。 如果為配置多個自簽名證書 `fd-cloudservice` 指定證書的密鑰別名。

## 後續步驟 {#next-steps}

您已配置資料源。 接下來，您可以建立表單資料模型，或者如果您已經建立了沒有資料源的表單資料模型，則可以將其與剛剛配置的資料源關聯。 請參閱 [建立表單資料模型](/help/forms/using/create-form-data-models.md) 的雙曲餘切值。
