---
title: 一般AEM Forms設定
seo-title: 一般AEM Forms設定
description: 瞭解如何在管理控制台中設定「核心組態」頁面設定，以協助改善系統效能。
seo-description: 瞭解如何在管理控制台中設定「核心組態」頁面設定，以協助改善系統效能。
uuid: 940680fd-b7ab-4376-aa5b-e139223522ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: bd648c38-731b-420e-973d-a4728b69868e
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# 一般AEM Forms設定 {#general-aem-forms-settings}

管理控制台中的「核心組態」頁面提供可協助改善系統效能的設定。 在設定或更新這些設定後，請重新啟動您的應用程式伺服器。

有關啟用安全備份模式的資訊，請參 [閱啟用和禁用安全備份模式](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode)。


>[!NOTE]
>
>臨時目錄中的檔案和全局文檔儲存(GDS)根目錄中的長期文檔可能包含敏感用戶資訊，例如在使用API或用戶介面訪問時需要特殊憑據的資訊。 因此，必須使用作業系統可用的任何方法正確保護此目錄。 建議只有用於運行應用程式伺服器的作業系統帳戶具有此目錄的讀寫權限。


1. 在管理控制台中，按一 **[!UICONTROL 下「設定>核心繫統設定>設定」]**。
1. 在「核心配置」頁面中，根據需要更改選項，然後按一下「確 **[!UICONTROL 定」]**。 如需選項的詳細資訊，請參閱核 [心設定選項](configure-general-aem-forms-settings.md#core-configurations-options)。


## 核心配置選項 {#core-configurations-options}

**temp目錄的位置** AEM表單將建立產品暫存檔案的目錄路徑。 如果此設定的值為空，則位置預設為系統臨時目錄。 確保temp目錄是可寫資料夾。

***注意&#x200B;**:確保臨時目錄位於本地檔案系統中。 AEM表格不支援遠端位置的臨時目錄。*

**全局文檔儲存根目錄** 全局文檔儲存(GDS)根目錄用於以下用途：

* 儲存長期保存的檔案。 長期使用的檔案沒有過期時間，而且會持續存留，直到移除為止（例如，在工作流程中使用的PDF檔案）。 長期使用的檔案是整個系統狀態的關鍵部分。 如果部分或全部這些檔案遺失或損毀，表單伺服器可能會變得不穩定。 因此，此目錄必須儲存在RAID設備上。
* 儲存處理期間需要的暫存檔案。

   ***注意&#x200B;**:您也可以在AEM表單資料庫中啟用檔案儲存。 但是，使用GDS時，系統效能更好。*

* 在群集中的節點之間傳輸文檔。 如果您在叢集環境中執行AEM表單，此目錄必須可從叢集內的所有節點存取。
* 從遠端API呼叫接收傳入參數。

如果未指定GDS根目錄，則該目錄預設為應用程式伺服器目錄：

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/[server]/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/[server]/adobe/AEMformsserver/DocumentStorage`

***注意&#x200B;**:更改GDS根目錄設定的值應特別小心。 GDS目錄可用來儲存流程中使用的長期檔案，以及重要的AEM表單產品元件。 更改GDS目錄的位置是系統的一項主要更改。 錯誤設定GDS目錄的位置會導致AEM表單無法運作，而且可能需要完整重新安裝AEM表單。 如果您為GDS目錄指定了新位置，則應用程式伺服器需要關閉，並且資料必須在伺服器重新啟動之前遷移。 系統管理員必須將所有檔案從舊位置移動到新位置，但保留內部目錄結構。*

***注意&#x200B;**:請勿為temp目錄和GDS目錄指定相同的目錄。*

如需GDS目錄的其他資訊，請參 [閱「準備安裝AEM表單(Single Server)」](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)。

**Adobe Server Fonts目錄的位置** ：輸入包含Adobe伺服器字型之目錄的路徑。 這些字型會隨AEM表格安裝。 這些字型的預設位置是 [aem-forms root]/fonts目錄。 如果此目錄無法存取，您可以將字型複製到其他位置，並使用此設定來指定新位置。

**客戶字型目錄的位置** ：鍵入目錄的路徑，該目錄包含您要使用的其他字型。

***注意&#x200B;**:從Windows系統字型快取中挑選字型，而更新快取時需要重新啟動系統。 指定Customer字型目錄後，請確定您重新啟動安裝AEM表單的系統。*

**「系統字型」目錄的位置** ：鍵入作業系統提供的字型目錄的路徑。 可以添加多個目錄，並以分號 **分隔**。

**資料服務設定檔的位置** ：指定services-config.xml檔案的位置。 依預設，此檔案會內嵌在adobe-core-appserver.ear檔案中，且無法由使用者存取。 預設services-config.xml檔案的復本位於 [aem-forms root]\sdk\misc\DataServices\Server-Configuration。 如果您變更了此檔案並加以移動，請在此欄位中輸入新位置。

資料服務設定檔案允許自訂資料服務設定，例如驗證類型和除錯輸出。

此設定預設為空。

**預設檔案最大內嵌大小（位元組）** ：在各種AEM表單元件之間傳送檔案時，記憶體中儲存的位元組數上限。 使用此設定進行效能調整。 小於此編號的文檔儲存在記憶體中並保存在資料庫中。 超過此上限的檔案會儲存在硬碟上。

此設定為強制性。 預設值為65536位元組。

**預設檔案處理逾時（秒）** ：在多種AEM表單元件之間傳送的檔案被視為作用中的最大時間量（以秒為單位）。 此時間過後，用於儲存此文檔的檔案將被刪除。 使用此設定可控制磁碟空間的使用。

此設定為強制性。 預設值為600秒。

**檔案掃描間隔（秒）** ：嘗試刪除不再需要且用於在服務之間傳遞檔案資料的檔案之間的時間（以秒為單位）。

此設定為強制性。 預設值為30秒。

**啟用FIPS** 選擇此選項以啟用FIPS模式。 聯邦資訊處理標準(FIPS)140-2是美國政府定義的密碼學標準。 在FIPS模式下運行時，AEM表單使用RSA BSAFE Crypto-C 2.1加密模組將資料保護限制為FIPS 140-2認可的算法。

FIPS模式不支援在7.0之前的Adobe Acrobat®版本中使用的加密演算法。如果啟用了FIPS模式，而且您使用Encryption服務使用設為Acrobat 5的相容性等級的密碼來加密PDF，則加密嘗試將失敗並出現錯誤。

通常，啟用FIPS後，Assembler服務將不對任何文檔應用密碼加密。 如果嘗試這樣做，則會拋出FIPSModeException，指出「FIPS模式下不允許密碼加密」。 此外，當基本文檔使用密碼加密時，FIPS模式不支援「文檔描述XML(DDX)PDFFromBookmarks」元素。

***注意&#x200B;**:AEM表單軟體不驗證程式碼以確保FIPS相容性。 它提供FIPS操作模式，以便FIPS認可的算法用於來自FIPS認可的庫(RSA)的加密服務。*

**啟用WSDL** 選取此選項，可針對屬於AEM表單一部分的所有服務啟用「網站服務定義語言(WSDL)」產生。

在開發環境中啟用此選項，開發人員可使用WSDL產生來建立其用戶端應用程式。 您可以選擇在生產環境中停用WSDL產生功能，以避免暴露服務的內部詳細資訊。

**在資料庫中啟用檔案儲存** ：選取這個選項，可將長期存留的檔案儲存在AEM表單資料庫中。 啟用此選項並不會移除GDS目錄的需求。 不過，選擇這個選項可簡化AEM表單備份。 如果您只使用GDS，則備份會將AEM formsAEM表單系統置於備份模式，然後完成資料庫和GDS的備份。 如果選擇資料庫選項，則備份將包括完成資料庫備份以進行新安裝或完成資料庫備份以及一次性備份GDS以進行升級。 與僅GDS配置相比，清除作業和資料可能需要對資料庫進行額外管理。 （請參閱將資料庫用於文檔儲存時的備份選項。）

**啟用DSC呼叫統計** ：選取此選項時，AEM表單會追蹤呼叫統計資料，例如呼叫數、呼叫所花的時間，以及呼叫中的錯誤數。 此資訊會儲存在JMX Bean中，以便您使用Java™ JConsole或協力廠商軟體來查看統計資料。 如果您不想看到這些統計資料，請取消選取這個選項以改善AEM表格的效能。

**Enable RDS** Selecting this option enables the Remote Development Services(RDS)servlet within AEM forms. 啟用此選項後，用戶端工具可與資料服務互動，以部署或取消部署模型來建立目標和端點，或找出已部署在端點的模型。 依預設，不會選取此選項。

**允許非安全的RDS請求** ：當選取此選項時，RDS請求不需要使用https。 依預設，未選取此選項，所有與資料服務的通訊都必須是https要求。

**** 允許從Flex應用程式上傳非安全的檔案：從Adobe Flex®應用程式將檔案上傳至AEM表單的檔案上傳servlet，需要先經過驗證並授權，使用者才能上傳檔案。 必須為用戶分配「文檔上載應用程式用戶」角色或包含「文檔上載」權限的其他角色。 這有助於防止未經授權的使用者將檔案上傳至AEM表單伺服器。 如果您想要在開發環境中停用此安全性功能，或為了向後相容於舊版AEM表單，請選取這個選項。 依預設，不會選取此選項。 如需詳細資訊，請參閱「使用AEM表單進行程式設計」中的「使用AEM表單叫用AEM表單」。

**** 允許從Java SDK應用程式上傳非安全的檔案：必須保護HTTP DocumentManager上載。 依預設，HTTP上傳作業需要使用者先經過驗證並取得授權，才能上傳檔案。 必須為用戶分配「服務用戶」角色或包含「服務調用」權限的其他角色。 這有助於防止未經授權的使用者將檔案上傳至表單伺服器。 如果您想要在開發環境中停用此安全性功能，以向後相容於舊版AEM表單，或根據防火牆設定，請選取此選項。 依預設，不會選取此選項。 如需詳細資訊，請參閱「使用AEM表單進行程式設計」中的「使用Java API叫用AEM表單」。
