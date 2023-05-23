---
title: 常規AEM Forms設定
seo-title: General AEM Forms settings
description: 瞭解如何在管理控制台中配置「核心配置」頁設定，以幫助提高系統效能。
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

# 常規AEM Forms設定 {#general-aem-forms-settings}

管理控制台中的「核心配置」頁提供了有助於提高系統效能的設定。 配置或更新這些設定後，請重新啟動應用程式伺服器。

有關啟用安全備份模式的資訊，請參見 [啟用和禁用安全備份模式](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode)。


>[!NOTE]
>
>臨時目錄中的檔案和全局文檔儲存(GDS)根目錄中的長期文檔可能包含敏感的用戶資訊，例如在使用API或用戶介面訪問時需要特殊憑據的資訊。 因此，必須使用作業系統可用的任何方法來正確保護此目錄。 建議只有用於運行應用程式伺服器的作業系統帳戶才具有對此目錄的讀寫權限。


1. 在管理控制台中，按一下 **[!UICONTROL 設定>核心繫統設定>配置]**。
1. 在「核心配置」頁上，根據需要更改選項，然後按一下 **[!UICONTROL 確定]**。 有關選項的詳細資訊，請參見 [核心配置選項](configure-general-aem-forms-settings.md#core-configurations-options)。


## 核心配置選項 {#core-configurations-options}

**臨時目錄的位置** 表單將建立產AEM品臨時檔案的目錄路徑。 如果此設定的值為空，則該位置預設為系統臨時目錄。 確保臨時目錄是可寫資料夾。

>[!NOTE]
>
>確保臨時目錄位於本地檔案系統上。 表AEM單不支援遠程位置的臨時目錄。

**全局文檔儲存根目錄** 全局文檔儲存(GDS)根目錄用於以下目的：

* 儲存長期儲存的檔案。 長期文檔沒有過期時間，並會一直持續到刪除(例如，工作流進程中使用的PDF檔案)。 長期文檔是整個系統狀態的關鍵部分。 如果某些或所有這些文檔丟失或損壞，表單伺服器可能會變得不穩定。 因此，此目錄儲存在RAID設備上非常重要。
* 儲存處理過程中需要的臨時文檔。

>[!NOTE]
>
>您還可以在表單資料庫中啟AEM用文檔儲存。 但是，使用GDS時系統效能更好。

* 在群集中的節點之間傳輸文檔。 如果您在群集AEM環境中運行表單，則必須從群集中的所有節點訪問此目錄。
* 從遠程API調用接收傳入參數。

如果未指定GDS根目錄，則該目錄預設為應用伺服器目錄：

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/'server'/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/'server'/adobe/AEMformsserver/DocumentStorage`

>[!NOTE]
>
>更改GDS根目錄設定的值應特別小心。 GDS目錄用於儲存流程中使用的長壽命檔案以及關鍵表單產AEM品元件。 更改GDS目錄的位置是一次重大系統更改。 錯誤配置GDS目錄的位置將導致表AEM單無效，並可能需要完全重新安AEM裝表單。 如果為GDS目錄指定新位置，則需要關閉應用程式伺服器並遷移資料，然後才能重新啟動伺服器。 系統管理員必須將所有檔案從舊位置移動到新位置，但保留內部目錄結構。

>[!NOTE]
>
>不要為臨時目錄和GDS目錄指定同一目錄。

有關GDS目錄的其他資訊，請參見 [準備安AEM裝表單（單伺服器）](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)。

**Adobe伺服器字型目錄的位置** 鍵入包含Adobe伺服器字型的目錄的路徑。 這些字型隨表單AEM一起安裝。 這些字型的預設位置是 [根]/fonts目錄。 如果此目錄無法訪問，則可以將字型複製到其他位置，並使用此設定指定新位置。

**客戶字型目錄的位置** 鍵入包含要使用的其他字型的目錄的路徑。

***附註&#x200B;**:從Windows系統字型快取中選取字型，更新快取時需要系統重新啟動。 指定Customer字型目錄後，請確保重新啟動安裝了表單AEM的系統。*

**系統字型目錄的位置** 鍵入作業系統提供的字型目錄的路徑。 可以添加多個目錄，用分號分隔 **;**。

**資料服務配置檔案的位置** 指定services-config.xml檔案的位置。 預設情況下，此檔案嵌入到adobe-core-appserver.ear檔案中，不能由用戶訪問。 預設services-config.xml檔案的副本位於 [根]\sdk\misc\DataServices\Server-Configuration。 如果更改了此檔案並移動了它，請在此欄位中鍵入新位置。

資料服務配置檔案允許自定義資料服務設定，如驗證類型和調試輸出。

預設情況下，此設定為空。

**預設文檔最大內聯大小（位元組）** 在各種表單元件之間傳遞文檔時記憶體中保留的最大AEM位元組數。 使用此設定進行效能調整。 小於此數目的文檔儲存在記憶體中並保留在資料庫中。 超過此最大值的文檔儲存在硬碟上。

此設定是必需的。 預設值為65536位元組。

**預設文檔處理超時（秒）** 在不同表單元件之間傳遞的文檔被視為活動的最AEM長時間（秒）。 此時間過後，用於儲存此文檔的檔案將被刪除。 使用此設定可控制磁碟空間的使用。

此設定是必需的。 預設值為600秒。

**文檔掃描間隔（秒）** 嘗試刪除不再需要且用於在服務之間傳遞文檔資料的檔案之間的時間（秒）。

此設定是必需的。 預設值為30秒。

**啟用FIPS** 選擇此選項以啟用FIPS模式。 聯邦資訊處理標準(FIPS)140-2是美國政府定義的密碼學標準。 在FIPS模式下運行時AEM，表單使用RSA BSAFE Crypto-C 2.1加密模組將資料保護限制為FIPS 140-2認可的算法。

FIPS模式不支援在7.0以前的Adobe Acrobat®版本中使用的加密算法。如果啟用了FIPS模式，並且您使用加密服務使用相容級別設定為Acrobat 5的密碼對PDF進行加密，則加密嘗試將失敗並出現錯誤。

通常，啟用FIPS後，匯編器服務將不會對任何文檔應用密碼加密。 如果嘗試了此操作，則會引發FIPSModeException，指示「FIPS模式下不允許密碼加密」。 此外，當基本文檔是密碼加密的文檔時，在FIPS模式下不支援「文檔說明XML(DDX)PDFFromBookmarks」元素。

>[!NOTE]
>
>表單AEM軟體不驗證代碼以確保FIPS相容性。 它提供FIPS操作模式，以便FIPS認可的算法用於FIPS認可的庫(RSA)的加密服務。

**啟用WSDL** 選擇此選項可為屬於表單的所有服務啟用Web服務定義語言(WSDL)AEM生成。

在開發環境中啟用此選項，在開發環境中，開發人員使用WSDL生成來構建其客戶端應用程式。 您可以選擇在生產環境中禁用WSDL生成，以避免暴露服務的內部詳細資訊。

**在資料庫中啟用文檔儲存** 選擇此選項可在表單資料庫中儲存長AEM期文檔。 啟用此選項不會刪除GDS目錄的需要。 但是，選擇此選項可簡AEM化表單備份。 如果僅使用GDS ，則備份涉及將AEMformsAEM表單系統置於備份模式，然後完成資料庫和GDS的備份。 如果選擇資料庫選項，則備份涉及完成新安裝的資料庫備份或完成資料庫備份和一次性GDS備份以進行升級。 與僅GDS配置相比，清除作業和資料可能需要對資料庫進行其他管理。 （請參見將資料庫用於文檔儲存時的備份選項。）

**啟用DSC調用統計** 選擇此選項後，AEM表單將跟蹤調用統計資訊，如調用次數、調用所用時間以及調用中的錯誤數。 此資訊儲存在JMX Bean中，以便您可以使用Java™ JConsole或第三方軟體查看統計資訊。 如果不想查看這些統計資訊，請取消選擇此選項以提AEM高表單效能。

**啟用RDS** 選擇此選項可啟用表單中的遠程開發服務(RDS)AEMservlet。 啟用此選項後，客戶端工具可以與資料服務交互，以執行部署或取消部署模型等操作，以建立目標和終結點，或查明哪些模型已部署到終結點。 預設情況下，未選擇此選項。

**允許非安全RDS請求** 選擇此選項後，RDS請求無需使用https。 預設情況下，未選擇此選項，並且與Data Services的所有通信都需要https請求。

**允許從Flex應用程式上傳非安全文檔：** 用於將文檔從AdobeFlex®應用程式上載到表單的文AEM件上載servlet要求用戶在可以上載文檔之前先經過身份驗證和授權。 必須為用戶分配「文檔上載應用程式用戶」角色或包含「文檔上載」權限的其他角色。 這有助於防止未授權用戶將文檔上載到表AEM單伺服器。 如果要在開發環境中禁用此安全功能，或為了向後相容以前版本的表單，請選AEM擇此選項。 預設情況下，未選擇此選項。 有關詳細資訊，請參AEM閱使用AEM表單遠程調用表單。AEM

**允許從Java SDK應用程式上載非安全文檔：** 必須保護HTTP DocumentManager上載。 預設情況下，HTTP上載要求用戶在上載文檔之前先經過身份驗證和授權。 必須為用戶分配「服務用戶」角色或包含「服務調用」權限的其他角色。 這有助於防止未經授權的用戶將文檔上載到表單伺服器。 如果要在開發環境中禁用此安全功能，以向後相容以前版本的表單，或根AEM據防火牆設定，請選擇此選項。 預設情況下，未選擇此選項。 有關詳細資訊，請參AEM閱使用表單寫程式中的調用表AEM單。
