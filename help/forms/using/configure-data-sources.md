---
title: 設定資料來源
description: 瞭解如何設定不同型別的資料來源，以便建立表單資料模型。
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Form Data Model
exl-id: 7a1d9d57-66f4-4f20-91c2-ace5a71a52f2
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '2073'
ht-degree: 1%

---

# 設定資料來源{#configure-data-sources}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-data-sources.html) |
| AEM 6.5 | 本文章 |


![資料整合](do-not-localize/data-integeration.png)

AEM Forms資料整合可讓您設定並連線至不同的資料來源。 下列是支援的現成可用型別。 不過，只要很少自訂，您也可以整合其他資料來源。

* 關聯式資料庫 — MySQL、Microsoft SQL Server、IBM DB2、OracleRDBMS、postgreSQL和Sybase
* AEM使用者設定檔
* RESTful Web服務
* SOAP型網站服務
* OData服務

資料整合可支援OAuth2.0（[授權代碼](https://oauth.net/2/grant-types/authorization-code/)、[使用者端認證](https://oauth.net/2/grant-types/client-credentials/)）、基本驗證及API金鑰驗證型別，並且允許實作自訂驗證以存取Web服務。 在AEMCloud Service中設定RESTful、SOAP型和OData服務時，在AEM Web主控台中設定關聯式資料庫的JDBC和AEM使用者設定檔的聯結器。

## 設定關聯式資料庫 {#configure-relational-database}

您可以使用「AEM Web主控台組態」來設定關聯式資料庫。 請執行下列動作：

1. 前往`https://server:host/system/console/configMgr`的AEM Web主控台。
1. 尋找&#x200B;**[!UICONTROL Apache Sling Connection Pooled DataSource]**&#x200B;設定。 選取以在編輯模式中開啟設定。
1. 在設定對話方塊中，指定您要設定的資料庫詳細資訊，例如：

   * 資料來源的名稱
   * 儲存資料來源名稱的資料來源服務屬性
   * JDBC驅動程式的Java類別名稱
   * JDBC連線URI
   * 與JDBC驅動程式建立連線的使用者名稱和密碼

   >[!NOTE]
   >
   >在設定資料來源之前，請務必先加密機密資訊，例如密碼。 若要加密：
   >
   > 1. 移至https://&#39;[伺服器]：[連線埠]&#39;/system/console/crypto。
   > 1. 在&#x200B;**[!UICONTROL 純文字]**&#x200B;欄位中，指定要加密的密碼或任何字串，並選取&#x200B;**[!UICONTROL Protect]**。
   >
   >加密的文字會顯示在「受保護的文字」欄位中，您可以在設定中指定該欄位。

1. 啟用&#x200B;**[!UICONTROL 借入時測試]**&#x200B;或&#x200B;**[!UICONTROL 傳回時測試]**，以指定物件在從集區借入或傳回集區之前，先進行驗證。
1. 在&#x200B;**[!UICONTROL 驗證查詢]**&#x200B;欄位中指定SQL SELECT查詢，以驗證集區的連線。 查詢至少必須傳回一列。 根據您的資料庫，指定下列其中一項：

   * 選取1 （MySQL和MS SQL）
   * 選取1個(雙Oracle)

1. 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存組態。

   >[!NOTE]
   >
   > 如果您的Forms資料模型包含物件，而該物件是關聯式資料庫的保留關鍵字，則可能會導致資料新增、更新或擷取問題。 因此，請避免在表單資料模型中使用這類物件。

## 設定AEM使用者設定檔 {#configure-aem-user-profile}

您可以使用AEM Web Console中的使用者設定檔聯結器組態來設定AEM使用者設定檔。 請執行下列動作：

1. 移至AEM網頁主控台，網址為https://&#39;[server]：[port]&#39;system/console/configMgr。
1. 尋找&#x200B;**[!UICONTROL AEM Forms資料整合 — 使用者設定檔聯結器設定]**，並選取以在編輯模式中開啟設定。
1. 在「使用者設定檔聯結器組態」對話方塊中，您可以新增、移除或更新使用者設定檔屬性。 指定的屬性可用於表單資料模型。 使用下列格式指定使用者設定檔屬性：

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   範例：

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >上述範例中的&#x200B;**&#42;**&#x200B;表示CRXDE結構中AEM使用者設定檔中`profile/empLocation/`節點下的所有節點。 這表示表單資料模型可以存取`profile/empLocation/`節點下任何節點中存在的型別`string`的`city`屬性。 不過，包含指定屬性的節點必須遵循一致結構。

1. 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存組態。

## 設定雲端服務設定的資料夾 {#cloud-folder}

>[!NOTE]
>
設定RESTful、SOAP和OData服務的雲端服務時，需要設定雲端服務資料夾。

AEM中的所有雲端服務設定都已整合到AEM存放庫的`/conf`資料夾中。 根據預設，`conf`資料夾包含您可以建立雲端服務設定的`global`資料夾。 不過，您需要為雲端設定手動啟用它。 您也可以在`conf`中建立其他資料夾，以建立並組織雲端服務設定。

若要設定雲端服務設定的資料夾：

1. 前往&#x200B;**[!UICONTROL 工具 > 一般 > 設定瀏覽器]**。
   * 如需詳細資訊，請參閱[設定瀏覽器](/help/sites-administering/configurations.md)檔案。
1. 請執行以下操作來啟用雲端設定的全域資料夾，或跳過此步驟來建立和設定雲端服務設定的另一個資料夾。

   1. 在&#x200B;**[!UICONTROL 設定瀏覽器]**&#x200B;中，選取`global`資料夾並選取&#x200B;**[!UICONTROL 屬性]**。

   1. 在&#x200B;**[!UICONTROL 設定屬性]**&#x200B;對話方塊中，啟用&#x200B;**[!UICONTROL 雲端設定]**。

   1. 選取&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;以儲存設定並結束對話方塊。

1. 在&#x200B;**[!UICONTROL 設定瀏覽器]**&#x200B;中，選取&#x200B;**[!UICONTROL 建立]**。
1. 在&#x200B;**[!UICONTROL 建立設定]**&#x200B;對話方塊中，指定資料夾的標題並啟用&#x200B;**[!UICONTROL 雲端設定]**。
1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以建立為雲端服務設定啟用的資料夾。

## 設定RESTful Web服務 {#configure-restful-web-services}

在Swagger定義檔中，可以使用JSON或YAML格式的[Swagger規格](https://swagger.io/specification/)來描述RESTful Web服務。 若要在AEM雲端服務中設定RESTful Web服務，請確保您的檔案系統上有Swagger檔案，或該檔案託管所在的URL。

執行下列操作以設定RESTful服務：

1. 移至&#x200B;**[!UICONTROL 工具>Cloud Service>資料來源]**。 選取以選取您要建立雲端設定的資料夾。

   請參閱[設定雲端服務設定的資料夾](../../forms/using/configure-data-sources.md#cloud-folder)，以取得關於建立和設定雲端服務設定的資料夾的資訊。

1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以開啟&#x200B;**[!UICONTROL 建立資料Source設定精靈]**。 指定設定的名稱及標題，從&#x200B;**[!UICONTROL 服務型別]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL RESTful服務]**，選擇性地瀏覽並選取設定的縮圖影像，然後選取&#x200B;**[!UICONTROL 下一步]**。
1. 指定RESTful服務的下列詳細資料：

   * 從Swagger Source下拉式清單中選取「URL」或「檔案」，接著指定Swagger URL至Swagger定義檔案或從本機檔案系統上傳Swagger檔案。
   * 根據Swagger Source輸入，下列欄位已預先填入值：

      * 配置： REST API使用的傳輸通訊協定。 下拉式清單中顯示的配置型別數目，取決於Swagger來源中定義的配置。
      * 主機：提供REST API之主機的網域名稱或IP位址。 這是必填欄位。
      * 基本路徑：所有API路徑的URL首碼。 它是選用欄位。\
        如有需要，請編輯這些欄位的預先填入值。

   * 選取驗證型別 — 無、OAuth2.0（[授權碼](https://oauth.net/2/grant-types/authorization-code/)、[使用者端認證](https://oauth.net/2/grant-types/client-credentials/)）、基本驗證、API金鑰、自訂驗證或相互驗證 — 以存取RESTful服務，並相應地提供驗證的詳細資料。

   如果您選取&#x200B;**[!UICONTROL API金鑰]**&#x200B;作為驗證型別，請指定API金鑰的值。 API金鑰可作為請求標頭或查詢引數傳送。 從&#x200B;**[!UICONTROL 位置]**&#x200B;下拉式清單中選取其中一個選項，並相應地在&#x200B;**[!UICONTROL 引數名稱]**&#x200B;欄位中指定標頭名稱或查詢引數。

   如果您選取&#x200B;**[!UICONTROL 相互驗證]**&#x200B;做為驗證型別，請參閱[RESTful與SOAP Web服務的憑證式相互驗證](#mutual-authentication)。

1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以建立RESTful服務的雲端設定。

### 表單資料模型HTTP使用者端設定可最佳化效能 {#fdm-http-client-configuration}

與RESTful Web服務整合時，[!DNL Experience Manager Forms]表單資料模型，因為資料來源包括用於效能最佳化的HTTP使用者端設定。
執行以下步驟來設定表單資料模型HTTP使用者端：

1. 以管理員身分登入[!DNL Experience Manager Forms]作者執行個體並移至[!DNL Experience Manager]網頁主控台組合。 預設URL為[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。

1. 選取REST資料來源&#x200B;]**的**[!UICONTROL &#x200B;表單資料模型Http使用者端設定。

1. 在[!UICONTROL 表單資料模型REST資料來源]的Http使用者端設定對話方塊中：

   * 在&#x200B;**[!UICONTROL 連線限制（共]**&#x200B;個欄位）中，指定表單資料模型與RESTful Web服務之間允許的最大連線數目。 預設值為20個連線。

   * 在&#x200B;**[!UICONTROL 每個路由的連線限制]**&#x200B;欄位中，指定每個路由允許的最大連線數目。 預設值為2個連線。

   * 在&#x200B;**[!UICONTROL 保持連線]**&#x200B;欄位中指定持續性HTTP連線持續運作的持續時間。 預設值為15秒。

   * 在&#x200B;**[!UICONTROL 連線逾時]**&#x200B;欄位中指定[!DNL Experience Manager Forms]伺服器等待連線建立的持續時間。 預設值為10秒。

   * 在&#x200B;**[!UICONTROL 通訊端逾時]**&#x200B;欄位中，指定兩個資料封包之間閒置的最長時間。 預設值為30秒。

## 設定SOAP網站服務 {#configure-soap-web-services}

以SOAP為基礎的Web服務是使用[Web服務描述語言(WSDL)規格](https://www.w3.org/TR/wsdl)來描述。 若要在AEM雲端服務中設定SOAP架構的Web服務，請確定您擁有Web服務的WSDL URL，並執行下列動作：

1. 移至&#x200B;**[!UICONTROL 工具>Cloud Service>資料來源]**。 選取以選取您要建立雲端設定的資料夾。

   請參閱[設定雲端服務設定的資料夾](../../forms/using/configure-data-sources.md#cloud-folder)，以取得關於建立和設定雲端服務設定的資料夾的資訊。

1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以開啟&#x200B;**[!UICONTROL 建立資料Source設定精靈]**。 指定組態的名稱與標題，從&#x200B;**[!UICONTROL 服務型別]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL SOAP Web服務]**，瀏覽並選取組態的縮圖影像，然後選取&#x200B;**[!UICONTROL 下一步]**。
1. 為SOAP Web服務指定下列專案：

   * Web服務的WSDL URL。
   * 服務端點。 在此欄位中指定值，以覆寫WSDL中提及的服務端點。
   * 選取驗證型別 — None、OAuth2.0（[授權碼](https://oauth.net/2/grant-types/authorization-code/)、[使用者端認證](https://oauth.net/2/grant-types/client-credentials/)）、Basic Authentication、Custom Authentication、X509 Token或Mutual Authentication — 以存取SOAP服務，並相應地提供驗證的詳細資料。

     如果您選取&#x200B;**[!UICONTROL X509 Token]**&#x200B;作為驗證型別，請設定X509憑證。 如需詳細資訊，請參閱[設定憑證](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service)。
在**[!UICONTROL 金鑰別名]**&#x200B;欄位中指定X509憑證的KeyStore別名。 在&#x200B;**[!UICONTROL 存留時間]**&#x200B;欄位中，指定驗證要求保持有效的時間（以秒為單位）。 或者，選取以簽署訊息本文或時間戳記標題，或兩者皆簽署。

     如果您選取&#x200B;**[!UICONTROL 相互驗證]**&#x200B;做為驗證型別，請參閱[RESTful與SOAP Web服務的憑證式相互驗證](#mutual-authentication)。

1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以建立SOAP Web服務的雲端設定。

## 設定OData服務 {#config-odata}

OData服務由其服務根URL識別。 若要在AEM雲端服務中設定OData服務，請確定您擁有該服務的服務根URL，並執行下列動作：

>[!NOTE]
>
表單資料模型支援[OData 4](https://www.odata.org/documentation/)版。
如需設定Microsoft Dynamics 365線上或內部部署的逐步指南，請參閱[Microsoft Dynamics OData設定](/help/forms/using/ms-dynamics-odata-configuration.md)。

1. 移至&#x200B;**[!UICONTROL 工具>Cloud Service>資料來源]**。 選取以選取您要建立雲端設定的資料夾。

   請參閱[設定雲端服務設定的資料夾](../../forms/using/configure-data-sources.md#cloud-folder)，以取得關於建立和設定雲端服務設定的資料夾的資訊。

1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以開啟&#x200B;**[!UICONTROL 建立資料Source設定精靈]**。 指定組態的名稱與標題，從&#x200B;**[!UICONTROL 服務型別]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL OData服務]**，選擇性地瀏覽並選取組態的縮圖影像，然後選取&#x200B;**[!UICONTROL 下一步]**。
1. 指定OData服務的下列詳細資料：

   * 要設定之OData服務的服務根URL。
   * 選取驗證型別 — None、OAuth2.0（[授權碼](https://oauth.net/2/grant-types/authorization-code/)、[使用者端認證](https://oauth.net/2/grant-types/client-credentials/)）、Basic Authentication或Custom Authentication — 以存取OData服務，並相應地提供驗證的詳細資料。

   >[!NOTE]
   >
   選取OAuth 2.0驗證型別，以使用OData端點作為服務根來與Microsoft Dynamics服務連線。

1. 選取&#x200B;**建立**&#x200B;以建立OData服務的雲端設定。

## RESTful和SOAP Web服務的憑證式相互驗證 {#mutual-authentication}

當您啟用表單資料模型的相互驗證時，資料來源和執行表單資料模型的AEM Server會在共用任何資料之前先驗證彼此的身分。 您可以針對REST和SOAP型連線（資料來源）使用相互驗證。 若要在您的AEM Forms環境中設定表單資料模型的相互驗證：

1. 將私密金鑰（憑證）上傳到[!DNL AEM Forms]伺服器。 若要上傳私密金鑰：
   1. 以系統管理員身分登入您的[!DNL AEM Forms]伺服器。
   1. 瀏覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]**。 選取`fd-cloudservice`使用者並選取&#x200B;**[!UICONTROL 屬性]**。
   1. 開啟&#x200B;**[!UICONTROL 金鑰存放區]**&#x200B;標籤，展開&#x200B;**[!UICONTROL 從KeyStore檔案新增私密金鑰]**&#x200B;選項，上傳KeyStore檔案，指定別名、密碼，然後選取&#x200B;**[!UICONTROL 提交]**。 憑證已上傳。  私密金鑰別名會在憑證中提及，並在建立憑證時設定。
1. 將信任憑證上傳至全域信任存放區。 若要上傳憑證：
   1. 瀏覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 信任存放區]**。
   1. 展開&#x200B;**[!UICONTROL 從CER檔案新增憑證]**&#x200B;選項，選取&#x200B;**[!UICONTROL 選取憑證檔案]**，上傳憑證，然後選取&#x200B;**[!UICONTROL 提交]**。
1. 設定[SOAP](#configure-soap-web-services)或[RESTful](#configure-restful-web-services)網頁服務做為資料來源，並選取&#x200B;**[!UICONTROL 相互驗證]**&#x200B;做為驗證型別。 如果您為`fd-cloudservice`使用者設定多個自我簽署憑證，請指定憑證的金鑰別名。

## 後續步驟 {#next-steps}

您已設定資料來源。 接下來，您可以建立表單資料模型，或者，如果您已建立不含資料來源的表單資料模型，則可以將其與您設定的資料來源建立關聯。 如需詳細資訊，請參閱[建立表單資料模型](/help/forms/using/create-form-data-models.md)。
