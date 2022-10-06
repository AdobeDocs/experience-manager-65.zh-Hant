---
title: 一般AEM Forms設定
seo-title: General AEM Forms settings
description: 了解如何在管理控制台中配置核心配置頁面設定，以幫助改善系統效能。
seo-description: Learn to configure the Core Configurations page settings in administration console that can help improve system performance.
uuid: 940680fd-b7ab-4376-aa5b-e139223522ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: bd648c38-731b-420e-973d-a4728b69868e
exl-id: e1519477-b5a8-4947-8597-26b945a3b819
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1713'
ht-degree: 0%

---

# 一般AEM Forms設定 {#general-aem-forms-settings}

管理控制台中的「核心配置」頁提供了有助於改善系統效能的設定。 配置或更新這些設定後，請重新啟動應用程式伺服器。

有關啟用安全備份模式的資訊，請參見 [啟用和禁用安全備份模式](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode).


>[!NOTE]
>
>臨時目錄中的檔案和全局文檔儲存(GDS)根目錄中的長期文檔可能包含敏感用戶資訊，例如在使用API或用戶介面訪問時需要特殊憑據的資訊。 因此，必須使用作業系統可用的任何方法來正確保護此目錄。 建議只有運行應用程式伺服器的作業系統帳戶具有此目錄的讀寫權限。


1. 在管理控制台中，按一下 **[!UICONTROL 設定>核心繫統設定>配置]**.
1. 在核心設定頁面上，視需要變更選項，然後按一下 **[!UICONTROL 確定]**. 如需選項的詳細資訊，請參閱 [核心配置選項](configure-general-aem-forms-settings.md#core-configurations-options).


## 核心配置選項 {#core-configurations-options}

**臨時目錄的位置** AEM表單將建立產品臨時檔案的目錄路徑。 如果此設定的值為空，則位置預設為系統臨時目錄。 確保臨時目錄是可寫資料夾。

>[!NOTE]
>
>確保本地檔案系統上有臨時目錄。 AEM表單不支援遠端位置的臨時目錄。

**全局文檔儲存根目錄** 全局文檔儲存(GDS)根目錄用於以下用途：

* 儲存長期文檔。 長期文檔沒有到期時間，並且會持續到刪除它們(例如，工作流進程中使用的PDF檔案)為止。 長期文檔是整個系統狀態的關鍵部分。 如果丟失或損壞了這些文檔，則表單伺服器可能會變得不穩定。 因此，必須將此目錄儲存在RAID設備上。
* 儲存處理期間所需的臨時文檔。

>[!NOTE]
>
>您也可以在AEM表單資料庫中啟用檔案儲存。 但是，使用GDS時系統效能更好。

* 在群集中的節點之間傳輸文檔。 如果您在叢集環境中執行AEM表單，則必須可從叢集內的所有節點存取此目錄。
* 接收來自遠端API呼叫的傳入參數。

如果未指定GDS根目錄，則該目錄預設為應用程式伺服器目錄：

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/'server'/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/'server'/adobe/AEMformsserver/DocumentStorage`

>[!NOTE]
>
>更改GDS根目錄設定的值應特別謹慎。 GDS目錄用於儲存流程中使用的長期檔案，以及重要的AEM表單產品元件。 更改GDS目錄的位置是一次重大的系統更改。 不正確配置GDS目錄的位置將導致AEM表單無法運作，並且可能需要完全重新安裝AEM表單。 如果為GDS目錄指定新位置，則需要關閉應用程式伺服器，並在伺服器重新啟動之前遷移資料。 系統管理員必須將所有檔案從舊位置移動到新位置，但保留內部目錄結構。

>[!NOTE]
>
>請勿為臨時目錄和GDS目錄指定相同的目錄。

有關GDS目錄的其他資訊，請參見 [準備安裝AEM表單（單一伺服器）](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

**Adobe伺服器字型目錄的位置** 鍵入包含Adobe伺服器字型的目錄的路徑。 這些字型會隨AEM表單一起安裝。 這些字型的預設位置為 [aem-forms根]/fonts目錄。 如果無法訪問此目錄，則可以將字型複製到其他位置，並使用此設定指定新位置。

**客戶字型目錄的位置** 鍵入目錄的路徑，該目錄包含要使用的其他字型。

***附註&#x200B;**:從Windows系統字型快取中選擇字型，更新快取時需要系統重新啟動。 指定客戶字型目錄後，請務必重新啟動安裝AEM表單的系統。*

**系統字型目錄的位置** 鍵入作業系統提供的字型目錄的路徑。 可以添加多個目錄，用分號分隔 **;**.

**資料服務配置檔案的位置** 指定services-config.xml檔案的位置。 依預設，此檔案內嵌於adobe-core-appserver.ear檔案中，且無法供使用者存取。 預設services-config.xml檔案的副本位於 [aem-forms根]\sdk\misc\DataServices\Server-Configuration。 如果更改了此檔案並將其移動，請在此欄位中鍵入新位置。

資料服務配置檔案允許自定義資料服務設定，如身份驗證類型和調試輸出。

此設定預設為空。

**預設文檔最大內嵌大小（位元組）** 在各種AEM表單元件之間傳遞檔案時記憶體中保留的最大位元組數。 使用此設定進行效能調整。 小於此編號的文檔儲存在記憶體中並保存在資料庫中。 超過此上限的文檔儲存在硬碟上。

此設定為必填。 預設值為65536位元組。

**預設文檔處理超時（秒）** 在各種AEM表單元件之間傳遞的檔案被視為作用中的最大時間（以秒為單位）。 此時間過後，將刪除用於儲存此文檔的檔案。 使用此設定可控制磁碟空間的使用。

此設定為必填。 預設值為600秒。

**文檔掃描間隔（秒）** 嘗試刪除不再需要的檔案和用於在服務之間傳遞文檔資料之間的時間長度（以秒為單位）。

此設定為必填。 預設值為30秒。

**啟用FIPS** 選擇此選項以啟用FIPS模式。 聯邦資訊處理標準(FIPS)140-2是美國政府定義的密碼學標準。 在FIPS模式下運行時，AEM表單將使用RSA BSAFE Crypto-C 2.1加密模組將資料保護限制為FIPS 140-2認可的算法。

FIPS模式不支援在7.0之前的Adobe Acrobat®版本中使用的加密算法。如果啟用了FIPS模式，並且您使用將相容級別設定為Acrobat 5的密碼來加密PDF，則加密嘗試將失敗，並且出現錯誤。

通常，當啟用FIPS時，組合器服務將不將密碼加密應用於任何文檔。 如果嘗試了此操作，則會引發FIPSModeException，指明「FIPS模式下不允許密碼加密」。 此外，當基本文檔被密碼加密時，FIPS模式不支援「文檔描述XML(DDX)PDFsFromBookmarks」元素。

>[!NOTE]
>
>AEM forms軟體不驗證代碼以確保FIPS相容。 它提供FIPS操作模式，以便FIPS認可的算法用於來自FIPS認可的庫(RSA)的加密服務。

**啟用WSDL** 選擇此選項可為屬於AEM表單的所有服務啟用Web服務定義語言(WSDL)生成。

在開發環境中啟用此選項，在此環境中，開發人員使用WSDL生成來構建其客戶端應用程式。 您可以選擇在生產環境中禁用WSDL生成，以避免顯示服務的內部詳細資訊。

**在資料庫中啟用文檔儲存** 選擇此選項可在AEM表單資料庫中儲存長期文檔。 啟用此選項並不會消除對GDS目錄的需要。 不過，選擇此選項可簡化AEM表單備份。 如果您只使用GDS，則備份涉及將AEM formsAEM forms系統置於備份模式，然後完成資料庫和GDS的備份。 如果選擇資料庫選項，則備份涉及完成新安裝的資料庫備份或完成資料庫備份以及一次性完成升級的GDS備份。 與僅GDS配置相比，清除作業和資料可能需要對資料庫進行額外管理。 （請參閱將資料庫用於文檔儲存時的備份選項。）

**啟用DSC調用統計** 選中此選項時，AEM Forms將跟蹤調用統計資訊，如調用次數、調用所花費的時間以及調用中的錯誤數。 此資訊儲存在JMX Bean中，以便您可以使用Java™ JConsole或第三方軟體查看統計資訊。 如果您不想查看這些統計資料，請取消選取此選項以改善AEM表單效能。

**啟用RDS** 選擇此選項將啟用AEM表單中的遠程開發服務(RDS)servlet。 啟用此選項後，用戶端工具可與資料服務互動，以執行部署或取消部署模型等操作，以建立目的地和端點，或找出已部署至端點的模型。 依預設，不會選取此選項。

**允許非安全RDS請求** 選中此選項時，RDS請求不需要使用https。 依預設，不會選取此選項，所有與資料服務的通訊都必須是https要求。

**允許從Flex應用程式上傳非安全檔案：** 從AdobeFlex®應用程式將檔案上傳至AEM表單的檔案上傳servlet，需先取得驗證和授權，使用者才能上傳檔案。 必須為用戶分配「文檔上載應用程式用戶」角色或包含「文檔上載」權限的其他角色。 這有助於防止未經授權的使用者將檔案上傳至AEM表單伺服器。 如果您想在開發環境中停用此安全性功能，或想與舊版AEM表單回溯相容，請選取此選項。 依預設，不會選取此選項。 如需詳細資訊，請參閱使用AEM表單進行程式設計中的「使用AEM表單遠端叫用AEM表單」。

**允許從Java SDK應用程式上傳非安全檔案：** HTTP DocumentManager上載必須安全。 預設情況下，HTTP上載要求用戶先經過身份驗證和授權，然後才能上載文檔。 必須為用戶分配服務用戶角色或包含服務調用權限的其他角色。 這有助於防止未經授權的使用者將檔案上傳至表單伺服器。 如果您想在開發環境中停用此安全性功能、與舊版AEM表單的回溯相容，或根據防火牆設定，請選取此選項。 依預設，不會選取此選項。 如需詳細資訊，請參閱使用AEM表單進行程式設計中的「使用Java API叫用AEM表單」。
