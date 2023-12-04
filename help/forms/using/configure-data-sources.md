---
title: 設定資料來源
description: 瞭解如何設定不同型別的資料來源，以便建立表單資料模型。
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Form Data Model
exl-id: 7a1d9d57-66f4-4f20-91c2-ace5a71a52f2
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
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
* 以SOAP為基礎的web服務
* OData服務

資料整合支援OAuth2.0([授權代碼](https://oauth.net/2/grant-types/authorization-code/)， [使用者端認證](https://oauth.net/2/grant-types/client-credentials/))、基本驗證和API金鑰驗證是現成可用的型別，可實作自訂驗證以存取網站服務。 雖然已在AEMCloud Service中設定RESTful、SOAP型和OData服務，但在AEM Web主控台中設定關聯式資料庫的JDBC和AEM使用者設定檔的聯結器。

## 設定關聯式資料庫 {#configure-relational-database}

您可以使用「AEM Web主控台組態」來設定關聯式資料庫。 請執行下列動作：

1. 前往AEM網頁主控台，位於 `https://server:host/system/console/configMgr`.
1. 尋找 **[!UICONTROL Apache Sling連線集區資料來源]** 設定。 選取以在編輯模式中開啟設定。
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
   > 1. 前往https://&#39;[伺服器]：[連線埠]&#39;/system/console/crypto.
   > 1. 在 **[!UICONTROL 純文字]** 欄位，指定要加密的密碼或任何字串，然後選取 **[!UICONTROL Protect]**.
   >
   >加密的文字會顯示在「受保護的文字」欄位中，您可以在設定中指定該欄位。

1. 啟用 **[!UICONTROL 借入時測試]** 或 **[!UICONTROL 回訪時測試]** 以指定物件在從集區借入或傳回集區之前，先進行驗證。
1. 指定SQL SELECT查詢 **[!UICONTROL 驗證查詢]** 欄位以驗證來自集區的連線。 查詢至少必須傳回一列。 根據您的資料庫，指定下列其中一項：

   * 選取1 （MySQL和MS SQL）
   * 選取1個(雙Oracle)

1. 選取 **[!UICONTROL 儲存]** 以儲存組態。

   >[!NOTE]
   >
   > 如果您的Forms資料模型包含物件，而該物件是關聯式資料庫的保留關鍵字，則可能會導致資料新增、更新或擷取問題。 因此，請避免在表單資料模型中使用這類物件。

## 設定AEM使用者設定檔 {#configure-aem-user-profile}

您可以使用AEM Web Console中的使用者設定檔聯結器組態來設定AEM使用者設定檔。 請執行下列動作：

1. 前往AEM網頁主控台： https://&#39;[伺服器]：[連線埠]&#39;system/console/configMgr.
1. 尋找 **[!UICONTROL AEM Forms資料整合 — 使用者設定檔聯結器設定]** 並選取以在編輯模式中開啟設定。
1. 在「使用者設定檔聯結器組態」對話方塊中，您可以新增、移除或更新使用者設定檔屬性。 指定的屬性可用於表單資料模型。 使用下列格式指定使用者設定檔屬性：

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   範例：

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >此 **&#42;** 在上述範例中，代表 `profile/empLocation/` CRXDE結構的AEM使用者設定檔中的節點。 這表示表單資料模型可以存取 `city` 型別的屬性 `string` 出現在下的任何節點中 `profile/empLocation/` 節點。 不過，包含指定屬性的節點必須遵循一致結構。

1. 選取 **[!UICONTROL 儲存]** 以儲存組態。

## 設定雲端服務設定的資料夾 {#cloud-folder}

>[!NOTE]
>
>設定RESTful、SOAP和OData服務的雲端服務時，需要設定雲端服務資料夾的設定。

AEM中的所有雲端服務設定都會整合至 `/conf` AEM存放庫中的資料夾。 根據預設， `conf` 資料夾包含 `global` 資料夾，您可在其中建立雲端服務設定。 不過，您需要為雲端設定手動啟用它。 您也可以在中建立其他資料夾 `conf` 建立和組織雲端服務組態。

若要設定雲端服務設定的資料夾：

1. 前往&#x200B;**[!UICONTROL 工具 > 一般 > 設定瀏覽器]**。
   * 請參閱 [設定瀏覽器](/help/sites-administering/configurations.md) 檔案以取得詳細資訊。
1. 請執行以下操作來啟用雲端設定的全域資料夾，或跳過此步驟來建立和設定雲端服務設定的另一個資料夾。

   1. 在 **[!UICONTROL 設定瀏覽器]**，選取 `global` 資料夾並選取 **[!UICONTROL 屬性]**.

   1. 在 **[!UICONTROL 設定屬性]** 對話方塊，啟用 **[!UICONTROL 雲端設定]**.

   1. 選取 **[!UICONTROL 儲存並關閉]** 以儲存組態並結束對話方塊。

1. 在 **[!UICONTROL 設定瀏覽器]**，選取 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL 建立設定]** 對話方塊，指定資料夾的標題並啟用 **[!UICONTROL 雲端設定]**.
1. 選取 **[!UICONTROL 建立]** 以建立為雲端服務設定啟用的資料夾。

## 設定RESTful Web服務 {#configure-restful-web-services}

RESTful Web服務可使用以下方式描述 [Swagger規格](https://swagger.io/specification/) JSON或YAML格式的Swagger定義檔案中。 若要在AEM雲端服務中設定RESTful Web服務，請確保您的檔案系統上有Swagger檔案，或該檔案託管所在的URL。

執行下列操作以設定RESTful服務：

1. 前往 **[!UICONTROL 「工具>Cloud Service>資料來源」]**. 選取以選取您要建立雲端設定的資料夾。

   另請參閱 [設定雲端服務設定的資料夾](../../forms/using/configure-data-sources.md#cloud-folder) 以取得為雲端服務設定建立和設定資料夾的資訊。

1. 選取 **[!UICONTROL 建立]** 以開啟 **[!UICONTROL 建立資料來源設定精靈]**. 指定設定的名稱及標題（選擇性），選取 **[!UICONTROL RESTful服務]** 從 **[!UICONTROL 服務型別]** 下拉式清單(可選擇瀏覽並選取設定的縮圖影像，然後選取 **[!UICONTROL 下一個]**.
1. 指定RESTful服務的下列詳細資料：

   * 從「Swagger來源」下拉式清單中選取「URL」或「檔案」，並相應地指定Swagger URL至Swagger定義檔案或從本機檔案系統上傳Swagger檔案。
   * 根據Swagger來源輸入，下列欄位已預先填入值：

      * 配置： REST API使用的傳輸通訊協定。 下拉式清單中顯示的配置型別數目，取決於Swagger來源中定義的配置。
      * 主機：提供REST API之主機的網域名稱或IP位址。 這是必填欄位。
      * 基本路徑：所有API路徑的URL首碼。 它是選用欄位。\
        如有需要，請編輯這些欄位的預先填入值。

   * 選取驗證型別 — 無、OAuth2.0([授權代碼](https://oauth.net/2/grant-types/authorization-code/)， [使用者端認證](https://oauth.net/2/grant-types/client-credentials/))、基本驗證、API金鑰、自訂驗證或相互驗證 — 存取RESTful服務，並相應地提供驗證的詳細資訊。

   如果您選取 **[!UICONTROL API金鑰]** 由於是驗證型別，請指定API金鑰的值。 API金鑰可作為請求標頭或查詢引數傳送。 從以下選項中選取其中一個選項： **[!UICONTROL 位置]** 下拉式清單，並在「 」中指定標頭的名稱或查詢引數 **[!UICONTROL 引數名稱]** 欄位中輸入。

   如果您選取 **[!UICONTROL 相互驗證]** 由於是驗證型別，請參閱 [RESTful和SOAP Web服務的憑證式相互驗證](#mutual-authentication).

1. 選取 **[!UICONTROL 建立]** 以建立RESTful服務的雲端設定。

### 表單資料模型HTTP使用者端設定可最佳化效能 {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] 表單資料模型已與RESTful網路服務整合，可作為資料來源使用，且包括用於效能最佳化的HTTP使用者端設定。
執行以下步驟來設定表單資料模型HTTP使用者端：

1. 登入 [!DNL Experience Manager Forms] 以管理員身分編寫執行個體並前往 [!DNL Experience Manager] Web控制檯套件組合。 預設URL為 [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).

1. 選取 **[!UICONTROL REST資料來源的表單資料模型Http使用者端設定]**.

1. 在 [!UICONTROL REST資料來源的表單資料模型Http使用者端設定] 對話方塊：

   * 指定表單資料模型與RESTful Web服務之間允許的最大連線數。 **[!UICONTROL 連線總數限制]** 欄位。 預設值為20個連線。

   * 指定中每個路由的允許連線數目上限。 **[!UICONTROL 每個路由的連線限制]** 欄位。 預設值為2個連線。

   * 在「 」中指定持續HTTP連線持續運作的持續時間 **[!UICONTROL 保持連線]** 欄位。 預設值為15秒。

   * 指定持續時間，期間為 [!DNL Experience Manager Forms] 伺服器會等待連線建立，在 **[!UICONTROL 連線逾時]** 欄位。 預設值為10秒。

   * 指定中兩個資料封包之間閒置的最長時間 **[!UICONTROL 通訊端逾時]** 欄位。 預設值為30秒。

## 設定SOAP Web服務 {#configure-soap-web-services}

以下說明以SOAP為基礎的Web服務： [Web服務描述語言(WSDL)規格](https://www.w3.org/TR/wsdl). 若要在AEM雲端服務中設定以SOAP為基礎的Web服務，請確定您擁有Web服務的WSDL URL，並執行下列動作：

1. 前往 **[!UICONTROL 「工具>Cloud Service>資料來源」]**. 選取以選取您要建立雲端設定的資料夾。

   另請參閱 [設定雲端服務設定的資料夾](../../forms/using/configure-data-sources.md#cloud-folder) 以取得為雲端服務設定建立和設定資料夾的資訊。

1. 選取 **[!UICONTROL 建立]** 以開啟 **[!UICONTROL 建立資料來源設定精靈]**. 指定設定的名稱及標題（選擇性），選取 **[!UICONTROL SOAP Web服務]** 從 **[!UICONTROL 服務型別]** 下拉式清單(可選擇瀏覽並選取設定的縮圖影像，然後選取 **[!UICONTROL 下一個]**.
1. 為SOAP Web服務指定下列專案：

   * Web服務的WSDL URL。
   * 服務端點。 在此欄位中指定值，以覆寫WSDL中提及的服務端點。
   * 選取驗證型別 — 無、OAuth2.0([授權代碼](https://oauth.net/2/grant-types/authorization-code/)， [使用者端認證](https://oauth.net/2/grant-types/client-credentials/))、基本驗證、自訂驗證、X509權杖或相互驗證 — 存取SOAP服務，並相應地提供驗證的詳細資訊。

     如果您選取 **[!UICONTROL X509 Token]** 以「驗證」型別，請設定X509憑證。 如需詳細資訊，請參閱 [設定憑證](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).
在中指定X509憑證的KeyStore別名 **[!UICONTROL 金鑰別名]** 欄位。 請以秒數指定時間，直到驗證要求保持有效，請在 **[!UICONTROL 存留時間]** 欄位。 或者，選取以簽署訊息本文或時間戳記標題，或兩者皆簽署。

     如果您選取 **[!UICONTROL 相互驗證]** 由於是驗證型別，請參閱 [RESTful和SOAP Web服務的憑證式相互驗證](#mutual-authentication).

1. 選取 **[!UICONTROL 建立]** 以建立SOAP Web服務的雲端設定。

## 設定OData服務 {#config-odata}

OData服務由其服務根URL識別。 若要在AEM雲端服務中設定OData服務，請確定您擁有該服務的服務根URL，並執行下列動作：

>[!NOTE]
>
>表單資料模型支援 [OData版本4](https://www.odata.org/documentation/).
>如需設定Microsoft Dynamics 365 （線上或內部部署）的逐步指南，請參閱 [Microsoft Dynamics OData設定](/help/forms/using/ms-dynamics-odata-configuration.md).

1. 前往 **[!UICONTROL 「工具>Cloud Service>資料來源」]**. 選取以選取您要建立雲端設定的資料夾。

   另請參閱 [設定雲端服務設定的資料夾](../../forms/using/configure-data-sources.md#cloud-folder) 以取得為雲端服務設定建立和設定資料夾的資訊。

1. 選取 **[!UICONTROL 建立]** 以開啟 **[!UICONTROL 建立資料來源設定精靈]**. 指定設定的名稱及標題（選擇性），選取 **[!UICONTROL OData服務]** 從 **[!UICONTROL 服務型別]** 下拉式清單(可選擇瀏覽並選取設定的縮圖影像，然後選取 **[!UICONTROL 下一個]**.
1. 指定OData服務的下列詳細資料：

   * 要設定之OData服務的服務根URL。
   * 選取驗證型別 — 無、OAuth2.0([授權代碼](https://oauth.net/2/grant-types/authorization-code/)， [使用者端認證](https://oauth.net/2/grant-types/client-credentials/))、基本驗證或自訂驗證 — 存取OData服務，並相應地提供驗證的詳細資訊。

   >[!NOTE]
   >
   >選取OAuth 2.0驗證型別，以使用OData端點作為服務根來與Microsoft Dynamics服務連線。

1. 選取 **建立** 以建立OData服務的雲端設定。

## RESTful和SOAP Web服務的憑證式相互驗證 {#mutual-authentication}

當您啟用表單資料模型的相互驗證時，資料來源和執行表單資料模型的AEM Server會在共用任何資料之前先驗證彼此的身分。 您可以針對以REST和SOAP為基礎的連線（資料來源）使用相互驗證。 若要在您的AEM Forms環境中設定表單資料模型的相互驗證：

1. 上傳私密金鑰（憑證）至 [!DNL AEM Forms] 伺服器。 若要上傳私密金鑰：
   1. 登入您的 [!DNL AEM Forms] server作為管理員。
   1. 瀏覽至 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]**. 選取 `fd-cloudservice` 使用者並選取 **[!UICONTROL 屬性]**.
   1. 開啟 **[!UICONTROL 金鑰存放區]** 標籤，展開 **[!UICONTROL 從KeyStore檔案新增私人金鑰]** 選項，上傳KeyStore檔案，指定別名、密碼，然後選取 **[!UICONTROL 提交]**. 憑證已上傳。  私密金鑰別名會在憑證中提及，並在建立憑證時設定。
1. 將信任憑證上傳至全域信任存放區。 若要上傳憑證：
   1. 瀏覽至 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 信任存放區]**.
   1. 展開 **[!UICONTROL 從CER檔案新增憑證]** 選項，選取 **[!UICONTROL 選取憑證檔案]**，上傳憑證，然後選取 **[!UICONTROL 提交]**.
1. 設定 [SOAP](#configure-soap-web-services) 或 [RESTful](#configure-restful-web-services) 以網站服務作為資料來源，然後選取 **[!UICONTROL 相互驗證]** 做為驗證型別。 如果您設定多個自我簽署憑證 `fd-cloudservice` 使用者，指定憑證的金鑰別名。

## 後續步驟 {#next-steps}

您已設定資料來源。 接下來，您可以建立表單資料模型，或者，如果您已建立不含資料來源的表單資料模型，則可以將其與您設定的資料來源建立關聯。 另請參閱 [建立表單資料模型](/help/forms/using/create-form-data-models.md) 以取得詳細資訊。
