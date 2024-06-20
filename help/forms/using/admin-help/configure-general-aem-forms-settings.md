---
title: 一般AEM Forms設定
description: 瞭解如何在管理主控台中設定有助於改善系統效能的核心設定頁面設定。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
exl-id: e1519477-b5a8-4947-8597-26b945a3b819
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1762'
ht-degree: 0%

---

# 一般AEM Forms設定 {#general-aem-forms-settings}

Administration Console中的「核心組態」頁面提供有助於改善系統效能的設定。 在設定或更新這些設定後，請重新啟動應用程式伺服器。

>[!NOTE]
>
> 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式）可能會導致AEM開發環境不一致。

如需有關啟用安全備份模式的資訊，請參閱 [啟用和停用安全備份模式](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode).


>[!NOTE]
>
>臨時目錄中的檔案和全域檔案儲存(GDS)根目錄中的長期檔案可能包含敏感的使用者資訊，例如使用API或使用者介面存取時需要特殊認證的資訊。 因此，請務必使用作業系統可用的任何方法來適當地保護此目錄。 建議只有用來執行應用程式伺服器的作業系統帳戶才有這個目錄的讀寫存取權。


1. 在管理控制檯中，選擇 **[!UICONTROL 設定>核心系統設定>設定]**.
1. 在核心設定頁面，視需要變更選項並選取 **[!UICONTROL 確定]**. 如需有關選項的詳細資訊，請參閱 [核心設定選項](configure-general-aem-forms-settings.md#core-configurations-options).


## 核心設定選項 {#core-configurations-options}

**暫存目錄的位置** AEM表單將建立產品暫存檔的目錄路徑。 如果此設定的值為空，則位置會預設為系統暫存目錄。 確定暫存目錄是可寫入的資料夾。

>[!NOTE]
>
>確定暫存目錄位於本機檔案系統上。 AEM forms不支援遠端位置的暫存目錄。

**全域檔案儲存根目錄** *ndash；全域檔案儲存(GDS)根目錄用於以下目的：

* 儲存長期檔案。 長效檔案沒有到期時間，而且會持續存在，直到被移除為止(例如，工作流程流程流程中使用的PDF檔案)。 長效檔案是整體系統狀態的關鍵部分。 如果其中的部分或全部檔案遺失或損毀，Forms伺服器可能會變得不穩定。 因此，此目錄必須儲存在RAID裝置上。
* 正在儲存處理期間所需的臨時檔案。

>[!NOTE]
>
>您也可以在AEM表單資料庫中啟用檔案儲存。 不過，使用GDS時，系統效能會更好。

* 在叢集中的節點之間傳輸檔案。 如果您在叢集環境中執行AEM表單，則必須從叢集內的所有節點存取此目錄。
* 接收來自遠端API呼叫的傳入引數。

如果您未指定GDS根目錄，則該目錄會預設為應用程式伺服器目錄：

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/'server'/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/'server'/adobe/AEMformsserver/DocumentStorage`

>[!NOTE]
>
>變更GDS根目錄設定的值時應特別小心。 GDS目錄可用來儲存流程中使用的長期檔案，以及重要的AEM表單產品元件。 變更GDS目錄的位置是重大的系統變更。 錯誤設定GDS目錄的位置將會導致AEM表單無法運作，並且可能需要完全重新安裝AEM表單。 如果您為GDS目錄指定了新位置，則必須先關閉應用程式伺服器並移轉資料，才能重新啟動伺服器。 系統管理員必須將所有檔案從舊位置移動到新位置，但保留內部目錄結構。

>[!NOTE]
>
>請勿為暫存目錄和GDS目錄指定相同的目錄。

如需有關GDS目錄的其他資訊，請參閱 [準備安裝AEM表單（單一伺服器）](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

**Adobe伺服器字型目錄的位置** *ndash；鍵入包含Adobe伺服器字型的目錄路徑。 這些字型會隨AEM表單一起安裝。 這些字型的預設位置為 [aem-forms根]/fonts目錄。 如果無法存取此目錄，您可以將字型複製到其他地方，並使用此設定來指定新位置。

**Customer Fonts目錄的位置** *ndash；鍵入包含要使用的其他字型的目錄路徑。

***注意&#x200B;**：從Windows系統字型快取中挑選字型，並需要重新啟動系統以更新快取。 指定Customer字型目錄後，請確定重新啟動安裝AEM表單的系統。*

**System Fonts目錄的位置** *ndash；輸入作業系統所提供的字型目錄路徑。 可以新增多個目錄，以分號分隔 **；**.

**資料服務組態檔的位置** *ndash；指定services-config.xml檔案的位置。 依預設，此檔案內嵌於adobe-core-appserver.ear檔案中，使用者無法存取。 預設services-config.xml檔案的副本位於 [aem-forms根]\sdk\misc\DataServices\Server-Configuration. 如果您已變更此檔案並移動它，請在此欄位中輸入新位置。

資料服務組態檔允許自訂資料服務設定，例如驗證型別和偵錯輸出。

此設定預設為空白。

**預設檔案最大內嵌大小（位元）** *ndash；在各種AEM表單元件之間傳遞檔案時保留在記憶體中的最大位元組數。 使用此設定進行效能調整。 小於此數字的檔案會儲存在記憶體中，並儲存在資料庫中。 超過此上限的檔案會儲存在硬碟上。

此設定是強制性的。 預設值為65536位元組。

**預設檔案處置逾時（秒）** *ndash；在各種AEM Forms元件之間傳遞的檔案視為作用中檔案的最長時間（以秒為單位）。 在這段時間過後，將會移除用來儲存此檔案的檔案。 使用此設定來控制磁碟空間的使用。

此設定是強制性的。 預設值為600秒。

**檔案整理間隔（秒）** *ndash；嘗試刪除不再需要的檔案與用來在服務之間傳遞檔案資料的時間間隔（秒）。

此設定是強制性的。 預設值為30秒。

**啟用FIPS** *ndash；選取此選項以啟用FIPS模式。 Federal Information Processing Standard (FIPS) 140-2是美國政府定義的密碼學標準。 在FIPS模式下執行時，AEM Forms會使用RSA BSAFE Crypto-C 2.1加密模組，將資料保護限製為FIPS 140-2核准的演演算法。

FIPS模式不支援在Adobe Acrobat® 7.0之前的版本中使用的加密演演算法。如果啟用了FIPS模式，而您使用密碼來加密PDF，並將相容性等級設定為Acrobat 5，則加密嘗試將失敗，並出現錯誤。

一般而言，啟用FIPS時，Assembler服務不會將密碼加密套用至任何檔案。 如果嘗試進行此動作，系統會擲回FIPSModeException，指出「FIPS模式不允許密碼加密」。 此外，當基礎檔案使用密碼加密時，FIPS模式中不支援Document Description XML (DDX) PDFsFromBookmarks元素。

>[!NOTE]
>
>AEM forms軟體不會驗證程式碼以確保FIPS相容性。 它提供FIPS操作模式，以便將FIPS認可的演演算法用於來自FIPS認可的程式庫(RSA)的密碼編譯服務。

**啟用WSDL** *ndash；選取此選項可為AEM表單中的所有服務啟用Web服務定義語言(WSDL)產生。

在開發人員使用WSDL世代來建置其使用者端應用程式的開發環境中啟用此選項。 您可以選擇在生產環境中停用WSDL產生，以避免公開服務的內部詳細資料。

**啟用資料庫中的檔案儲存** *ndash；選取此選項可將長效檔案儲存在AEM表單資料庫中。 啟用此選項不會移除對GDS目錄的需求。 不過，選擇此選項可簡化AEM表單備份。 如果您只使用GDS，備份會涉及將AEM formsAEM forms系統置於備份模式，然後完成資料庫和GDS的備份。 如果您選取資料庫選項，備份會涉及完成新安裝的資料庫備份，或完成資料庫備份，以及升級的GDS的一次性備份。 與僅限GDS的組態相比，可能需要額外管理資料庫，以清除作業和資料。 （請參閱當資料庫用於檔案儲存時的備份選項。）

**啟用DSC呼叫統計資料** *ndash；選取此選項時，AEM Forms會追蹤呼叫統計資料，例如呼叫次數、呼叫所花費的時間以及呼叫中的錯誤次數。 此資訊儲存在JMX Bean中，因此您可以使用Java™ JConsole或協力廠商軟體來檢視統計資料。 如果您不想檢視這些統計資料，請取消選取此選項以改善AEM表單效能。

**啟用RDS** *ndash；選取此選項會啟用AEM表單中的遠端開發服務(RDS) servlet。 啟用此選項後，使用者端工具可與資料服務互動，執行部署或取消部署模型等操作，以建立目的地和端點，或找出哪些模型已部署至端點。 依預設，不會選取此選項。

**允許不安全的RDS要求** *ndash；選取此選項時，RDS要求不需要使用https。 預設不會選取此選項，所有與資料服務的通訊都必須是https要求。

**允許從Flex應用程式上傳不安全的檔案** *ndash；從AdobeFlex®應用程式上傳檔案至AEM表單的檔案上傳servlet要求使用者在上傳檔案前必須經過驗證和授權。 必須為使用者指派檔案上傳應用程式使用者角色或包含檔案上傳許可權的其他角色。 這有助於防止未經授權的使用者將檔案上傳至AEM Forms伺服器。 如果您要在開發環境中停用此安全性功能，或想與舊版AEM表單回溯相容，請選取此選項。 依預設，不會選取此選項。 如需詳細資訊，請參閱使用AEM表單的程式設計中的「使用AEM表單遠端叫用AEM表單」。

**允許從Java SDK應用程式上傳不安全的檔案** *ndash； HTTP DocumentManager上傳必須安全。 依預設，HTTP上傳要求使用者在可以上傳檔案之前必須經過驗證和授權。 必須為使用者指派服務使用者角色或其他包含服務啟動許可權的角色。 這有助於防止未經授權的使用者將檔案上傳至Forms伺服器。 如果您要在開發環境中停用此安全性功能、想要與舊版AEM表單回溯相容，或根據您的防火牆設定，請選取此選項。 依預設，不會選取此選項。 如需詳細資訊，請參閱使用AEM表單進行程式設計中的「使用Java API叫用AEM表單」。
