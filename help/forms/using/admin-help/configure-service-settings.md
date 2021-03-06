---
title: 配置服務設定
seo-title: 配置服務設定
description: 了解如何配置服務設定。
seo-description: 了解如何配置服務設定。
uuid: e95425a4-62f6-473e-b21b-d081c432e02d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 2fab4b0c-e5db-47cd-b85a-4ff5ad6eb178
exl-id: a6a10ff0-6f4d-42df-9b4e-f98a53cf1806
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '10710'
ht-degree: 0%

---

# 配置服務設定{#configure-service-settings}

您可以使用「服務管理」頁面，為屬於AEM表單的每個服務配置設定。 可用的設定會依所設定的服務而有所不同。

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「服務管理」。
1. 請先停止服務再進行變更。 （請參閱[啟動和停止服務](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)。）
1. 按一下您要設定的服務名稱。
1. 如果服務有「配置」頁簽，則使用它更改服務的設定。 如需詳細資訊，請參閱下方的連結清單。

   >[!NOTE]
   >
   >「服務管理」頁上列出的所有服務都沒有「配置」頁簽。 對於您已建立的程式，只有在您已將設定參數新增至Workbench中的程式時，才會顯示「設定」標籤。 （請參閱[Workbench說明](https://www.adobe.com/go/learn_aemforms_workbench_63)中的「設定參數」。）


1. 按一下「安全性」頁簽，然後設定服務的安全性設定。 請參閱[修改服務](configure-service-settings.md#modifying-security-settings-for-a-service)的安全設定。
1. 如果服務具有「端點」頁簽，則使用該頁簽更改端點設定。 請參閱[管理端點](/help/forms/using/admin-help/adding-enabling-modifying-or-removing.md)。
1. 按一下「池」頁簽並設定池設定。 請參閱[配置服務的池](configure-service-settings.md#configuring-pooling-for-a-service)。
1. 按一下「儲存」以儲存變更，或按一下「取消」以捨棄變更。
1. 選中服務名稱旁邊的複選框，然後按一下「啟動」以重新啟動服務。

## 審核工作流服務設定{#audit-workflow-service-settings}

Workbench提供記錄執行階段執行的程式例項，然後播放這些例項，以觀察程式的行為。 （請參閱[Workbench說明](https://www.adobe.com/go/learn_aemforms_workbench_63)。） 若要節省表單伺服器檔案系統上的空間，您可以限制記錄所儲存資料的處理程式數量。 您可以配置審核工作流服務(`AuditWorkflowService`)的以下屬性：

**maxNumberOfRecordingInstances:** 儲存的錄制數上限。當儲存最大數量時，建立新記錄時，從檔案系統中刪除最舊的記錄。 如果您傾向於建立許多錄制，而且想要自動移除舊錄制，此屬性就十分實用。 預設值為 50。

**MaxNumberOfRecordingEntries:** 可針對每個記錄儲存的最大資料項數。資料項是有關進程中操作的資訊。 為操作的每次執行儲存多個條目，例如操作是否開始、操作是否完成以及引導操作的路由是否完成。 當進程可以包括許多操作執行時（例如，當遇到無限循環時），此屬性非常有用。 預設值為 50。

## 條碼式表單服務設定{#barcoded-forms-service-settings}

條碼式表單服務`(BarcodedFormsService)`從掃描的影像中提取條碼資料。 該服務接受條碼格式（TIFF或PDF）作為輸入，並提取由條碼編碼的資料的機器表示。

條碼式表單服務提供下列設定。

**左閱讀：** 選取此選項時，條碼影像會從右到左水準掃描。

**向右讀取：** 選取時，條碼影像會從左到右水準掃描。

**向上讀取：** 選取此選項時，條碼影像會從下到上垂直掃描。

**向下讀取：** 選取此選項時，條碼影像會從上到下垂直掃描。

>[!NOTE]
>
>預設會選取所有選項。 只有在您確定表單上沒有條形碼出現時，才取消選取選項。

**基本檔案路徑：** 相對於檔案路徑，用於解析運行XML檔案作業和運行一般檔案作業操作的批處理輸入和輸出檔案參數。在群集配置中，基本檔案路徑必須是所有群集節點都具有讀/寫訪問權限的共用檔案系統位置。

**資料來源名稱：** 用於維護批次處理作業之狀態和歷史記錄資訊的資料來源名稱。指定的資料源必須支援全局(XA)事務。

## 中央遷移橋服務（已廢止）設定{#central-migration-bridge-service-settings}

中央遷移橋服務(`CentralMigrationBridge`)調用Adobe Central Pro Output Server（中央）功能的子集，其中包括JFMERGE、JFTRANS和XMLIMPORT命令。 Central Migration Bridge服務操作可讓您在AEM表單中重複使用下列中央資產：

* 範本設計(&amp;ast;.ifd)
* 輸出模板(&amp;ast;.mdf)
* 資料檔案（&amp;ast;.dat檔案）
* 前導檔案（&amp;ast;.pre檔案）
* 資料定義檔案(&amp;ast;.tdf)

中央遷移橋服務可使用以下設定。

**中央安裝目錄：** 安裝Adobe中心5.7的目錄。

## EMC Documentum服務設定的Content Repository Connector {#content-repository-connector-for-emc-documentum-service-settings}

Content Repository Connector for EMC Documentum服務(`EMCDocumentumContentRepositoryConnector`)允許您建立與儲存在Documentum儲存庫中的內容交互的過程。

下列設定可用於「 EMC Documentum」服務的Content Repository Connector。

**資產連結對象預設路徑：** Documentum儲存庫中用於儲存資產連結對象的路徑的預設部分。實際路徑包含預設路徑和表單範本在AEM表單存放庫中的位置。

例如，如果預設路徑設定為`/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects`，且表單模板儲存在資料夾`/Docbase/forms/`中，則資產連結對象將儲存在以下位置：

`/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects/Docbase/forms/`

此設定的預設值為`/LiveCycleES/ConnectorforEMCDocumentum/AssetLinkObjects`。

## IBM FileNet服務設定的Content Repository Connector {#content-repository-connector-for-ibm-filenet-service-settings}

Content Repository Connector for IBM FileNet允許您建立與儲存在IBM FileNet儲存庫中的內容交互的過程。

以下設定可用於IBM FileNet服務的Content Repository Connector。

**資產連結對象預設路徑：** IBM FileNet儲存庫中用於儲存資產連結對象的路徑的預設部分。實際路徑包含預設路徑和表單範本在AEM表單存放庫中的位置。

例如，如果預設路徑設定為`/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects`，且表單模板儲存在資料夾`/Docbase/forms/`中，則資產連結對象將儲存在以下位置：

`/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects/Docbase/forms/`

此設定的預設值為`/LiveCycleES/ConnectorforIBMFileNet/AssetLinkObjects`。

## 轉換PDF服務設定{#convert-pdf-service-settings}

「轉換PDF」服務(`ConvertPdfService`)將PDF文檔轉換為PostScript和多種影像格式（JPEG、JPEG 2000、PNG和TIFF）。 將PDF文檔轉換為PostScript對於在任何PostScript打印機上基於伺服器的無人值守打印非常有用。 將PDF檔案轉換為多頁TIFF檔案，對於在不支援PDF檔案的內容管理系統中封存檔案而言，是很實用的做法。

「轉換PDF」服務可使用下列設定。

**交易類型：** 指定應如何將交易內容傳播到操作。

**必要：** 支援交易內容（若有）;否則，將建立新的事務上下文。這是預設值。

**需要新：** 一律會建立新的交易內容。如果活動事務上下文存在，則掛起。

**事務超時（秒）:** 在回退正在包裝此操作的事務之前，基礎事務提供程式應等待的秒數。如果傳播現有的交易內容，則會忽略此值。 預設值為 180。

**平滑的閾值解析度（以dpi為單位）:** 如果已為這些元素選擇了「將平滑應用於」選項，則對文本、線條圖和影像應用平滑（或消除鋸齒）的影像解析度低於此解析度。

**將平滑套用至文字：** 控制文字的消除鋸齒功能。要禁用文本平滑，並使用螢幕放大鏡使文本更清晰、更易閱讀，請清除此複選框。

**將平滑應用於線條圖：** 應用平滑以刪除線條中的突然角。

**將平滑套用至影像：** 套用平滑以將影像的突然變更最小化。

## Distiller服務設定{#distiller-service-settings}

Distiller服務(`DistillerService`)通過網路將PostScript、封裝的PostScript(EPS)和PRN檔案轉換為PDF檔案。

下列設定適用於Distiller服務。

**Adobe PDF設定：** 下列預先設定會套用至產生的PDF:

* 高質量打印
* 超大的頁面
* PDFA1b 2005 CMYK
* PDFA1b 2005 RGB
* PDFX1a 2001
* PDFX3 2002
* 印刷品質
* 檔案大小最小
* 標準

可透過PDF產生器使用者介面建立新設定。

**安全設定：** 套用至產生之PDF檔案的預先設定安全設定。預設值為「無安全性」。 您必須使用PDF產生器建立安全性設定，然後在此輸入設定。

**池大小：** 池的初始大小。部署Distiller服務時，此數字用於確定建立並分配給等待調用請求的空閒池的服務實施實例的數量。 然後，服務容器可以立即響應調用請求，而不需要首先初始化服務實例。

## 文檔管理服務設定{#document-management-service-settings}

>[!NOTE]
>
>Adobe®LiveCycle® Content Services ES（已過時）是隨LiveCycle安裝的內容管理系統。 它使用戶能夠設計、管理、監控和優化以人為中心的流程。 內容服務（已過時）支援將於12/31/2014終止。 請參閱[Adobe產品生命週期文檔](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html)。 若要了解如何設定內容服務（已淘汰），請參閱[管理內容服務](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf)。

文檔管理服務(`DocumentManagementService`)使進程能夠使用由內容服務提供的內容管理功能（已廢止）。 文檔管理操作提供了在內容管理系統中維護空間和內容所需的基本任務。 此類任務的示例包括複製、刪除、移動、檢索和儲存內容、建立空間和關聯，以及獲取和設定內容屬性。

以下設定可用於文檔管理服務。

**儲存配置：** 內容所在的儲存的配置。預設值為工作區。

**HTTP連接埠：** 用於存取內容服務的連接埠（已過時）。預設值為 8080。

## 電子郵件服務設定{#email-service-settings}

電子郵件通常用於發佈內容，或在自動化流程中提供狀態資訊。 電子郵件服務(`EmailService`)使進程能夠從POP3或IMAP伺服器接收電子郵件，並將電子郵件發送到SMTP伺服器。

例如，程式使用電子郵件服務傳送包含PDF表單附件的電子郵件訊息。 電子郵件服務會連接到SMTP伺服器，以發送包含附件的電子郵件。 PDF表單的設計目的，是讓收件者在完成表單後按一下「提交」。 此動作會將表單作為附件傳回至指定的電子郵件伺服器。 電子郵件服務會擷取傳回的電子郵件訊息，並將完成的表單儲存在處理資料表單變數中。

電子郵件服務可使用下列設定。

**SMTP主機：** 用於傳送電子郵件的SMTP伺服器的IP位址或URL。

**SMTP埠號：** 用於連接到SMTP伺服器的埠。

**SMTP驗證：** 選擇是否需要用戶驗證才能連接到SMTP伺服器。

**SMTP使用者：** 用來登入SMTP伺服器的使用者帳戶的使用者名稱。

**SMTP密碼：** 與SMTP用戶帳戶關聯的密碼。

**SMTP傳輸安全性：** 用於連接到SMTP伺服器的安全協定：

* 如果未使用任何協定，則選擇「無」（以明文發送資料）
* 如果使用安全套接字層協定，請選擇SSL。
* 如果使用傳輸層安全性，請選取TLS。

**POP3/IMAP主機：** 用於發送電子郵件的POP3或IMAP伺服器的IP地址或URL。

**POP3/IMAP用戶名：** 用於登錄到POP3或IMAP伺服器的用戶帳戶的用戶名。

**POP3/IMAP密碼：** 與POP3或IMAP用戶帳戶關聯的密碼。

**POP3/IMAP埠號：** 用於連接到POP3或IMAP伺服器的埠。

**POP3/IMAP:** 用於發送和接收電子郵件的協定。

**接收傳輸安全性：** 用於連接到SMTP伺服器的安全協定：

* 如果未使用任何協定，請選擇「無」（以明文發送資料）。
* 如果使用安全套接字層協定，請選擇SSL。
* 如果使用傳輸層安全性，請選取TLS。

## 加密服務設定{#encryption-service-settings}

加密服務(`EncryptionService`)允許您加密和解密文檔。 文檔被加密後，其內容將變得不可讀。 授權用戶可以解密該文檔以獲得對內容的訪問。 如果PDF檔案使用密碼加密，使用者必須先指定開啟的密碼，才能在Adobe Reader或Adobe Acrobat中檢視該檔案。 同樣，如果PDF文檔用證書加密，則用戶必須用與用於加密PDF文檔的證書（私鑰）對應的公鑰解密PDF文檔。

加密服務可使用以下設定。

**連接到的預設LDAP伺服器：** 用於檢索文檔加密證書的LDAP伺服器的主機名。

**連接到的預設LDAP埠：** LDAP伺服器的埠號。

**預設LDAP用戶名：** 如果LDAP伺服器需要身份驗證，請指定要用於連接到LDAP伺服器的用戶名。

**預設LDAP密碼：** 如果LDAP伺服器需要身份驗證，請指定與要用於連接到LDAP伺服器的用戶名對應的密碼。

>[!NOTE]
>
>只有在通過SSL保護連接時（使用LDAPS），才使用簡單身份驗證（用戶名和密碼）。

**相容性模式：**

## FTP服務設定{#ftp-service-settings}

FTP服務(`FTP`)可讓程式與FTP伺服器互動。 FTP服務操作可從FTP伺服器擷取檔案、將檔案放在FTP伺服器上，以及從FTP伺服器刪除檔案。 例如，從程式產生的報表等檔案可儲存在FTP伺服器上以供發佈。 或者，外部系統可能根據進程中的先前步驟生成一些檔案。 在該過程的後續步驟中，檔案可被傳輸到遠程位置。

下列設定適用於FTP服務。

**預設主機：** FTP伺服器的IP位址或URL。

**預設埠：** 用來連線至FTP伺服器的埠。預設值為 21。

**預設使用者名稱：** 您可用來存取FTP伺服器的使用者帳戶名稱。使用者帳戶必須有足夠的權限，才能執行此服務所需的FTP作業。

**預設密碼：** 與指定的使用者名稱搭配使用，以便與FTP伺服器進行驗證的密碼。

## 生成PDF服務設定{#generate-pdf-service-settings}

生成PDF服務(`GeneratePDFService`)將各種原生格式的檔案轉換為PDF文檔，並將PDF文檔轉換為多種檔案格式。

「產生PDF」服務可使用下列設定。

**Adobe PDF設定：** 若未在API呼叫參數中指定這些設定，則要套用至轉換工作的預先設定Adobe PDF設定的名稱。Adobe PDF設定是在管理控制台中設定，方法是按一下「服務> PDF產生器> Adobe PDF設定」。 這些設定僅適用於PDFMaker基於的轉換。

**安全設定：** 如果未將這些設定指定為API呼叫參數的一部分，則要套用至轉換作業的預先設定安全設定的名稱。安全設定是在管理控制台中配置的，方法是按一下「服務」>「PDF生成器」>「安全設定」。

**檔案類型設定：** 如果未將這些設定指定為API調用參數的一部分，則要套用至轉換作業的預先設定檔案類型設定的名稱。檔案類型設定是在管理控制台中配置的，方法是按一下「服務」>「PDF生成器」>「檔案類型設定」。

**使用Acrobat WebCapture（僅限Windows）:** 若此設定為true，「產生PDF」服務會將Acrobat X Pro用於所有HTML轉換為PDF。這可以改善由HTML產生的PDF檔案的品質，但效能可能會稍低。 預設值為false。

**使用Acrobat影像轉換（僅限Windows）:** 若此設定為true，「產生PDF」服務會使用Acrobat X Pro進行所有影像轉換為PDF。只有在預設純Java轉換機制無法成功轉換很大一部分輸入影像時，此設定才有用。 預設值為false。

**啟用Acrobat式AutoCAD轉換（僅限Windows）:** 若此設定為true，則所有DWG轉換為PDF的轉換都會使用Acrobat X Pro進行。只有當伺服器上未安裝AutoCAD或AutoCAD轉換機制無法成功轉換檔案時，此設定才有用。

**用於找出使用者名稱中禁止的特殊字元的規則運算式（僅限Windows）:** 指定當字元出現在使用者名稱中時，會干擾Export PDF和Optimize PDF操作的字元。

**ImageToPDF池大小：** 「生成PDF」服務中預設（純Java）Image-to-PDF轉換器的池大小。此設定可控制「產生PDF」服務可同時執行的影像至PDF轉換數上限。 此設定的預設值（建議用於單處理器系統）為3，在多處理器系統上，可增加此值。

**HTML到PDF的池大小：** 生成PDF服務中HTML到PDF轉換器的池大小。此設定可控制「產生PDF」服務可同時執行的HTML至PDF轉換數上限。 此設定的預設值（建議用於單處理器系統）為3，在多處理器系統上，可增加此值。

**OCR池大小：** PDF生成器用於OCR的PaperCaptureService的池大小。此設定的預設值（建議用於單處理器系統）為3，在多處理器系統上，可增加此值。 此設定僅在Windows系統上有效。

**用於HTML到PDF轉換的後援字型系列：** 當原始HTML中使用的字型無法供AEM表單伺服器使用時，要用於PDF檔案的字型系列名稱。如果希望轉換使用不可用字型的HTML頁，請指定字型系列。 例如，以區域語言編寫的頁面可能會使用無法使用的字型。

**原生轉換的重試** 邏輯如果首次嘗試轉換失敗，則控制PDF產生重試：

**無重試**

如果第一次轉換嘗試失敗，請勿重試PDF轉換

**重試**

無論逾時臨界值是否已達到，請重試PDF轉換。 第一次嘗試的預設逾時期間為270秒。

**若時間允許再試一次**

如果第一次轉換嘗試所耗用的時間少於指定的逾時期間，則重試PDF轉換。 例如，如果逾時期間為270秒，且第一次嘗試使用200秒，PDF產生器將重新嘗試轉換。 如果第一次嘗試本身耗用了270秒，則不會重試轉換。

## 參考線ES4實用程式服務設定{#guides-es4-utilities-service-settings}

建立指南時，指南中嵌入了一些資源，如指南定義。 資源也可以存在，作為儲存於本機或AEM表單伺服器上之應用程式資產的參考。 本指南不包含資料，且提交位置和輸入的值不適用於所有外部環境。

在大多數情況下，預設的參考線呈現服務足以準備指南以用於工作區或其他外部環境。 (在「服務」檢視的Workbench中，預設服務是「參考線（系統）/流程/呈現指南 — 1.0」。) 指南實用程式服務(`GuidesUtility`)允許您根據需要建立用於呈現指南的自定義過程。

指南實用程式操作允許您將以下指南呈現任務添加到進程：

* 判斷是否有資料可填入指南
* 內嵌指南資料或將其轉換為連結
* 將參考內容轉換為可外部存取的URL
* 替換HTML文檔或其他包裝函式中的值，或將它們轉換為可從外部訪問的URL
* 設定提交位置
* 指定輸入值
* 建立參數以表示參考的內容
* 如果有變數可用，請設定變數

「指南實用程式」服務的預設值支援大多數使用案例。 不過，如有必要，您可以變更下列值。

**publicPaths:** 已棄用此選項。請勿將此選項用於AEM表單。

**pathInfoExpiryInSeconds:** 從客戶端獲取路徑資訊的請求過期的間隔。預設為1。

**cantroalExpiryInSeconds:** 客戶要求抵押品的間隔。預設為315576000。

**MismatchExpiryInSeconds:** 當eTag（實體標籤）不匹配時，客戶端的宣傳資料請求過期的間隔。（eTag是HTTP回應標題。） 預設為1。

**指南內容：** 指南Web應用程式的內容根目錄。與使用「參考線」Web應用程式設定的值匹配。 預設值為/Guides/。

**secureRandomAlgorithm:** 產生索引鍵和識別碼時要使用的演算法。此值會傳遞至SecureRandom Java類的getInstance方法。 預設為SHA1PRNG。

**idBytes:** 用於密鑰標識符的隨機位元組數。預設為6。

**macAlgorithm:** 用於輔助URL驗證的MAC（訊息驗證代碼）演算法。此方法會傳遞至Mac類的getInstance方法。 預設為HmacSHA1。

**macRefreshIntervalInMinutes:** 金鑰作用中的時間量。在此間隔內，當鍵處於活動狀態時，將生成新鍵。 新密鑰成為活動密鑰。 在刷新間隔的10%內，將保留以前的活動密鑰。 此行為可讓使用舊索引鍵產生的URL在金鑰開關間繼續運作。 預設為144000。

**macOverlapIntervalInMinutes:** 產生新索引鍵後，舊索引鍵仍有效的時間長度。預設為1440分鐘（1天）。

**macKeySeed:** 用於產生安全URL的種子值。此選項時，系統不會重新整理金鑰。 在不同伺服器上設定相同種子，會導致這些伺服器產生相容的安全URL。 如果負載平衡器後面使用了多個表單伺服器，則此功能可能會很實用。 輸入隨機的字元和數字序列作為種子。

### 在伺服器群集{#using-guides-in-a-server-cluster}中使用參考線

在未使用黏著工作階段的伺服器叢集中轉譯指南會因NullPointerException而失敗。 「參考線」請求會運用安全URL，依預設，這些URL對其產生所在的伺服器是唯一的。 在使用黏著工作階段的叢集中，當請求點擊叢集中的節點後，該工作階段或使用者的所有後續請求都會專門路由至該伺服器，而且一切正常。 在不使用黏著工作階段的叢集中，後續請求可能會點擊叢集中的任何伺服器。 如果請求點擊的伺服器不是原始伺服器，則無法解析安全URL。

如果在不使用粘滯會話的伺服器群集中使用「參考線」，請為GuidesUtility服務設定macKeySeed值，然後停止並啟動群集。

macKeySeed值是隨機數產生器的種子，用於產生安全URL。 設定此值會導致每個叢集節點以相同方式初始化隨機數字產生器，並擁有相同安全URL的存取權。 您可以對此種子值使用任何隨機字串。

需要重新整理安全URL時，請變更macKeySeed值。 刷新安全URL取決於您的安全策略，與更改伺服器主根密碼的刷新策略類似。 macSeedValue類似於安全URL的主密碼，因為它用於生成新的唯一隨機數，以用於安全URL的生成和檢索。

必須重新啟動群集，因為macSeedValue在系統啟動時為只讀。 所有節點都需要重新啟動才能讀取值，因為它們會獨立使用此值，以使用種子值初始化其內部隨機數。

## JDBC服務設定{#jdbc-service-settings}

JDBC服務(`JdbcService`)使進程能夠與資料庫交互。

以下設定可用於JDBC服務。

**資料源名稱：** 一個字串值，它表示用於連接到資料庫伺服器的資料源的JNDI名稱。必須在承載表單伺服器的應用程式伺服器上定義資料源。 預設值是AEM表單資料庫的資料源的JNDI名稱。

## JMS服務設定{#jms-service-settings}

JMS服務(`JMS`)允許與Java消息傳送系統(JMS)提供程式交互，這些提供程式實現了點對點消息傳送和發佈/訂閱消息傳送。

使用預設屬性配置JMS服務，以便服務操作可以與JMS提供程式和關聯的JNDI服務連接和交互。 服務屬性的值會根據JBoss Application Server設定為預設值。 如果您使用不同的應用程式伺服器來托管AEM表單，請變更這些值。

JMS服務可使用以下設定。

**提供程式URL:**  JNDI服務提供程式的URL。預設值以JBoss Application Server為基礎。 下列URL是AEM表單支援之應用程式伺服器的預設值：

**JBoss:** `<server name>:1099`

**WebLogic:** `<server name>:7001`

**WebSphere:** `<server name>:2809`

**JNDI用戶名：** 用於與JNDI服務提供程式（用於查找隊列和主題名）進行身份驗證的帳戶的用戶名。預設值為guest。

**JNDI密碼：** 與為JNDI用戶名指定的用戶名關聯的密碼。預設值為guest。

**初始上下文工廠：** 用作初始上下文工廠的Java類。JMS服務使用此類建立初始上下文，這是解決主題和隊列名稱的起始點。 預設值是JBoss上JMS服務的初始上下文工廠。 以下類是AEM表單所支援應用程式伺服器的初始上下文工廠：

**JBoss:** org.jnp.interfaces.NamingContextFactory

**WebLogic:** weblogic.jndi.WLInitialContextFactory

**WebSphere:** com.ibm.websphere.naming.WsnInitialContextFactory

**連接用戶名：** 與為連接用戶名指定的用戶名關聯的密碼。預設值為guest。

**連接密碼：** 與為「連接用戶名」指定的用戶名關聯的密碼。預設值為guest。

**其他屬性：** 您可以傳遞至JNDI服務提供程式的屬性名稱和值對。這些屬性取決於您所使用的提供者的實施和設定。

屬性名稱和值對由分號&#x200B;**;**&#x200B;分隔。 例如，以下文本顯示將為名為name1和name2的兩個屬性指定的值，分別包含值value1和value2:

`name1=value1;name2=value2`

## LDAP服務設定{#ldap-service-settings}

LDAP服務(`LDAPService`)提供查詢LDAP目錄的操作。 LDAP目錄通常用於儲存組織中的人員、組和服務的資訊。

LDAP服務可使用以下設定。

**初始上下文工廠：** 用作上下文工廠的Java類。此類用於建立與LDAP伺服器的連接。 預設值為com.sun.jndi.ldap.LdapCtxFactory，適用於大多數LDAP伺服器。

**提供程式URL:** 用來連線至LDAP服務的URL。值的格式為`ldap://server name:port`

*伺* 服器名稱是承載LDAP伺服器的電腦的名稱

** 會提供LDAP服務使用的通訊埠。預設值為389，這是用於LDAP連接的標準埠。

**用戶名：** 用於登錄到LDAP伺服器的用戶帳戶的用戶名。用戶帳戶需要有連接到伺服器的權限，並讀取LDAP目錄中的資訊。

根據LDAP伺服器，用戶名可以是簡單的用戶名，如`myname`或DN，如`cn=myname,cn=users,dc=myorg`。

**密碼：** 與為「用戶名」設定提供的用戶名相對應的密碼。

**其他屬性：** 一個字串值，它表示可以提供給LDAP伺服器的其他屬性及其對應值。值的格式如下：

`property=value;property=value;...`

## Microsoft SharePoint配置服務設定{#microsoft-sharepoint-configuration-service-settings}

Microsoft SharePoint配置服務`(MSSharePointConfigService)`允許您指定具有模擬權限的AEM Forms用戶的憑據。 有關模擬權限的資訊，請參閱[配置Microsoft SharePoint的連接器](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html)。

下列設定可用於Microsoft SharePoint配置服務：

* 具有模擬權限的用戶的用戶名
* 上述用戶的密碼

**啟用SSL(HTTPS):**

**存留時間：** 此設定設定檔在用戶端上有效並經快取的時間長度（以秒為單位）。預設為86400（24小時）。 當客戶端應用程式與伺服器同步且已經過指定的時間量時，客戶端應用程式會向伺服器請求新的設定配置檔案。

**加密：** 指定是否加密儲存在行動裝置上的資料。

**Forms應用程式：** 在行動用戶端應用程式中啟用Forms功能。選取此選項時，使用者可以從行動裝置開啟表單並起始程式。

**任務應用程式：** 在行動用戶端應用程式中啟用任務功能。選取此選項時，使用者可以從行動裝置存取其任務清單和完成工作。

**內容服務應用程式：** 在行動用戶端應用程式中啟用內容服務功能。此功能僅適用於iOS。 選取此選項時，iPhone和iPad使用者可以存取儲存在您組織WebDAV伺服器中的檔案。

**離線支援：** 可讓使用者即使沒有與伺服器的連線，也能繼續使用行動用戶端應用程式（例如，當使用者超出儲存格範圍或處于飛航模式時）。使用者也必須在行動裝置上啟用「離線支援」設定。 此功能適用於Android和iOS裝置。 預設情況下，此功能為關閉。

>[!NOTE]
>
>如果已啟用離線支援，然後您加以停用，則會立即更新使用者的布建設定檔，或在使用者上線時立即更新。 如果用戶已離線工作，則所有掛起的任務將返回到其「任務」清單，並且其「隊列」中的所有項（包括掛起的表單、任務和包含驗證錯誤的表單）將從「隊列」中刪除。

**Android:** 允許Android裝置連線至伺服器。

**Apple iOS:** 允許iPhone和iPad連線至伺服器。

**AIR:** 允許執行以Adobe AIR®為基礎之應用程式的裝置連線至伺服器。

**BlackBerry:** 允許BlackBerry設備連接到伺服器。

**需要Android Microsoft Exchange ActiveSync:** 指定是否必須在Android裝置上安裝Microsoft Exchange ActiveSync策略管理器(EA)並啟用。選取此選項時，必須在Android裝置上強制執行EA。 未選取此選項時，不會執行任何檢查，儘管仍會強制執行其他要求。

**Android最小PIN長度：** Android裝置必須具有可強制PIN或密碼至少為此長度的全域設定。僅僅具有指定長度的PIN是不夠的。 PIN長度必須由系統強制執行，以便用戶以後不能刪除或縮短PIN。 預設值為 4。

**擦去前的Android最大密碼重試次數：** Android裝置具有全域設定，可在指定數量的無效密碼嘗試後擦除系統。此全域設定已啟用，且等於或低於此處指定的值。 預設值為 5。

**移除時Android擦去：** 指定當Android裝置上發生原則違規時會發生什麼事。選取此選項時，會刪除帳戶。 若未選取此選項，則會刪除儲存的帳戶密碼和快取資料。 在用戶修正策略違規之前，不會再進行同步嘗試。

## 輸出服務設定{#output-service-settings}

輸出服務`(OutputService)`使您能夠將XML表單資料與在AEM Forms Designer中建立的表單設計合併，以建立以下格式之一的文檔輸出流：

* PDF或PDF/A檔案輸出流。
* Adobe PostScript輸出流。
* 打印機控制語言(PCL)輸出流。
* 一種斑馬寫程式語言(ZPL)輸出流。

輸出流可被發送到網路打印機、本地打印機或磁碟檔案。 當您將輸出服務用於流程時，您也可以將輸出流作為檔案附件發送給電子郵件收件人。

以下設定適用於輸出服務。

**事務處理類型：** 指定應如何將事務處理上下文傳播到工序：

**必要：** 支援交易內容（若已存在）;否則，將建立新的事務上下文。這是預設值。

**需要新：** 一律會建立新的交易內容。如果活動事務上下文存在，則掛起。

**事務超時（秒）:** 在回退包含此操作的事務之前，基礎事務提供程式等待的秒數。如果傳播現有的交易內容，則會忽略此值。

在處理大型資料檔案或在繁忙的伺服器上操作時，可能需要增加輸出服務超時。 要更改超時值，請確保硬體伺服器有足夠的記憶體，並且記憶體可用於Java應用程式伺服器堆。 預設值為 `180`.

## PDFG配置服務設定{#pdfg-config-service-settings}

下列設定可用於PDFG配置服務(`PDFGConfigService`)。

**用戶作業選項目錄：** c服務寫入作業選項檔案的檔案系統資料夾路徑，這些檔案可供Acrobat Pro Extended訪問。預設值為[user.home]/Application Data/Adobe/Adobe PDF/Settings。

**PS啟動目錄：** 檔案系統資料夾的路徑，用於保存Adobe Acrobat Distiller所需的啟動檔案。預設值為[user.home]/Application Data/Adobe/Adobe PDF/Distiller/Startup。

**PS啟動檔案：** Adobe Acrobat Distiller所需的啟動檔案名稱。預設值為example.ps。

**伺服器轉換逾時：** 產生PDF服務和Distiller服務的最大作業轉換逾時（以秒為單位）。此設定會限制可在config.xml檔案和PDF產生器的管理控制台頁面中指定的轉換逾時上限。 預設值為 270。

**伺服器全域逾時：** 執行PDF轉換時，表單伺服器會考慮逾時限制。設定逾時值以解決問題。

**作業選項首碼：** 產生PDF服務用來在作業選項檔案的開頭加上短字串，以供暫時建立供Acrobat Distiller使用。預設值為pdfg。

**非Unicode應用程式：** 以逗號分隔的應用程式名稱清單，已知該清單不能使用Unicode。此清單已預先填入數個應用程式的名稱，PDF產生器已預先設定支援。 如果您選擇透過其他無法使用Unicode的協力廠商應用程式新增PDF轉換支援，則必須將其新增至此清單。 預設值為Autocad、Excel、PowerPoint、Project、Publisher、Visio、Word、WordPerfect。

**伺服器線程池計數：** 控制「生成PDF」服務內部使用的線程池的大小，以處理涉及尖峰的HTML到PDF轉換請求（轉換可從首頁訪問的連結頁）。預設值為 20。

**PDFG清理掃描秒數：** 如需詳細資訊，請參閱作業過期秒數區段。

**工作過期秒數：** 產生PDF服務會在轉換輸入檔案時立即刪除這些檔案。它會暫時儲存輸出檔案，時間長度由PDFG清除掃描秒數和作業過期秒數設定決定。

「作業過期秒數」設定指定檔案或空資料夾在符合刪除條件之前必須具有的版本。 PDFG清理掃描秒數設定指定清理線程掃描可刪除檔案的臨時資料夾的頻率。

例如，如果「作業過期秒數」設為100，而「PDFG清理掃描秒數」設為200，則清理線程每200秒運行一次，並刪除100秒或更舊的檔案。

PDFG清理掃描秒數的預設值為`43200`（12小時）。 作業過期秒數的預設值為`86400`（24小時）。

**預設地區：** 用於覆寫部署「生成PDF」服務的伺服器的預設地區（國家/地區+語言）。如果此參數未指定，則預設區域設定由部署服務的作業系統確定。 此參數會控制將錯誤訊息傳回API的語言。

## 表單工作流資料服務服務設定{#forms-workflow-data-services-service-settings}

下列服務會擴充Data Services並公開Workspace用來與伺服器通訊的組合程式。 除非Adobe支援指示您執行此操作，否則請勿更改這些服務的配置選項。 這些服務不是直接存取的：

* `ProcessManagementLcdsAttachmentService`
* `ProcessManagementLcdsPropertyService`
* `ProcessManagementLcdsTaskService`

## 遠程服務設定{#remoting-service-settings}

大部分的服務都已設定好，您才能透過(AEM表單已過時)AEM Forms Remoting存取。 有關(AEM表單已過時)AEM表單遠程處理的資訊，請參閱[使用AEM表單寫程式](https://adobe.com/go/learn_aemforms_programming_63)。

以下設定可用於遠程處理服務。

**Flex用戶端驗證方法：** 判斷啟用安全性時，伺服器傳回給用戶端的回應類型，叫用的操作不支援匿名叫用，且用戶端傳入的憑證無或無效。從「自訂」或「基本」中選擇。 預設值為Basic。

**允許序列化不可序列化類：** 大多數AEM表單端點只允許使用可序列化類來調用。在較舊版本中，遠程化端點允許使用非可序列化類來從基於Flex的客戶端調用。 為了防止APS11-15中描述的安全漏洞，已變更。 如果要繼續將非可序列化類與Flex Remoting端點一起使用，請選中此複選框。

## 儲存庫服務設定{#repository-service-settings}

存放庫服務(`RepositoryService`)為AEM表單提供資源儲存和管理服務。 開發人員建立應用程式時，可以在存放庫中部署資產，而非在檔案系統中部署。 這些資產可以包括任何類型的宣傳材料，包括XML表單、PDF forms(包括Acrobat表單)、表單片段、影像、配置檔案、策略、SWF檔案、DDX檔案、XML架構、WSDL檔案和測試資料。

您可以使用AEM Forms隨附的預設儲存庫，或使用第三方儲存庫（EMC Documentum Content Server、IBM FileNet Content Manager或IBM Content Manager）。

儲存庫提供程式服務是服務委派，充當提供程式服務的介面。 這可讓您連線至通用API，而不必知道哪個提供者服務正在實作儲存功能。 儲存庫提供程式服務為儲存庫服務資源提供資料庫儲存。

以下設定適用於儲存庫服務。

**提供者服務：** 用作儲存提供者的服務名稱。預設值為RepositoryProviderService。

## 簽名服務設定{#signature-service-settings}

簽名服務(`SignatureService`)可讓您的組織保護其分發和接收的Adobe PDF檔案的安全性和隱私。 此服務使用數位簽名和認證，以確保檔案不會遭到更改。 更改文檔會破壞其簽名。 由於安全功能應用於文檔本身，因此文檔在整個生命週期中都保持安全並受到控制；防火牆外、離線下載時，以及將防火牆提交回您的組織時。

簽名服務可使用以下設定。

**遠程HSM SPI服務的名稱：** 此選項用於在遠程電腦上安裝HSM時使用。當AEM表單安裝在64位Windows上，且您使用HSM裝置進行簽署時，請指定此選項。

**遠程HSM Web服務的URL:** 當AEM表單安裝在64位Windows上且您使用HSM設備進行簽名時，請指定此選項。

**包含表單載入變更的認證：** 選取此選項時，除了XFA範本，還會認證XFA表單狀態。請注意，啟用此選項可能會對效能造成負面影響。 預設值為true。

**執行文檔JavaScript指令碼：** 指定在簽名操作期間是否執行文檔JavaScript指令碼。預設值為false。

**處理具有Acrobat 9相容性的檔案：** 指定是否啟用Acrobat 9相容性。例如，選取此選項時，動態PDF中的可見認證即會啟用。 預設值為false。

**簽名時嵌入吊銷資訊：** 指定在簽名PDF文檔時是否嵌入吊銷資訊。預設值為false。

**驗證時嵌入吊銷資訊：** 指定在驗證PDF文檔時是否嵌入吊銷資訊。預設值為false。

**在簽名/證書期間強制嵌入所有證書的吊銷資訊：** 指定如果未嵌入所有證書的有效吊銷資訊，則簽名或證書操作是否失敗。請注意，如果證書不包含任何CRL或OCSP資訊，則該證書將被視為有效，即使未檢索任何吊銷資訊也是如此。 預設值為false。

**吊銷檢查順序：** 指定在通過證書吊銷清單(CRL)和聯機證書狀態協定(OCSP)機制進行檢查時的吊銷檢查順序。預設值為OCSPFirst。

**吊銷存檔資訊的最大大小：** 吊銷存檔資訊的最大大小（千位元組）。AEM表單會嘗試儲存盡可能多的撤銷資訊，而不會超過限制。 預設值為10 KB。

**支援從Adobe產品的搶鮮版組建建立的簽名：** 選取此選項時，使用Adobe產品的搶鮮版建立的簽名將可正確驗證。預設值為false。

**驗證時間選項：** 指定驗證簽署者憑證的時間。預設值為「安全時間」(Secure Time)「其他當前時間」(Else Current Time)。

**使用驗證期間在簽名中存檔的吊銷資訊：** 指定是否使用與簽名一起存檔的吊銷資訊進行吊銷檢查。預設值為true。

**使用文檔中儲存的驗證資訊來驗證簽名：** 選擇此選項時，將使用文檔中嵌入的驗證資訊（包括吊銷和時間戳資訊）來驗證簽名。預設值為true。

**允許的最大嵌套驗證會話數：** 允許的最大嵌套驗證會話數。AEM Forms使用此值來防止在驗證OCSP或CRL簽名器證書時無法正確設定OCSP或CRL證書時出現無限循環。 預設值為 10。

**驗證的最大時鐘偏差：** 簽名時間可以晚於驗證時間的最大時間（以分鐘為單位）。如果時鐘偏差大於此值，則簽名將無效。 預設值為65分鐘。

**憑證存留期快取：** 在快取中以線上或透過其他方式擷取之憑證存留期。預設值為1天。

### 傳輸選項{#transport-options}

**代理主機：** 代理主機的URL。僅在提供了某些有效值時使用。 無預設值。

**代理埠：** 代理埠。鍵入從0到65535的任何有效埠號。 預設值為 80。

**代理登入使用者名稱：** 代理登入使用者名稱。僅當為代理主機和代理埠提供了某些有效值時才使用。 無預設值。

**代理登入密碼：** 代理登入密碼。僅當為代理主機、代理埠和代理登錄用戶名提供了一些有效值時才使用。 無預設值。

**最大下載限制：** 每個連線可接收的最大資料量（以MB為單位）。最小值為1 MB，最大值為1024 MB。 預設值為16 MB。

**連線逾時：** 建立新連線所需等候的秒數上限。最小值為1，最大值為300。 預設值為 5。

**通訊端逾時：** 發生通訊端逾時（等待資料傳輸時）之前等待的最長時間（以秒為單位）。最小值為1，最大值為3600。 預設值為 30。

### 路徑驗證選項{#path-validation-options}

**需要顯式策略：** 指定路徑是否必須對與簽名者證書的信任錨點關聯的至少一個證書策略有效。預設值為false。

**禁止ANY策略：** 指定如果策略對象標識符(OID)包含在證書中，則是否應該處理它。預設值為false。

**禁止策略映射：** 指定是否允許在證書路徑中進行策略映射。預設值為false。

**勾選所有路徑：** 指定是否應驗證所有路徑，或在找到第一個有效路徑後是否應停止驗證。選取true或false。 預設值為false。

**LDAP伺服器：** 用於查找證書以進行路徑驗證的LDAP伺服器。無預設值。

**在證書AIA中跟蹤URI:** 指定在路徑發現期間是否處理證書AIA中的統一資源標識符(URI)。預設值為false。

**CA憑證中需要的基本限制擴充功能：** 指定CA憑證是否必須有憑證授權單位(CA)基本限制憑證擴充功能。某些早期德國認證的根證書（7和更早版本）不符合RFC 3280，並且不包含基本約束擴展。 如果已知用戶的EE證書鏈到如此的德文根，請取消選中此複選框。 預設值為true。

**鏈構建期間需要有效的證書籤名：** 指定鏈構建器是否需要用於構建鏈的證書的有效簽名。選中此複選框後，鏈生成器將不會在證書上生成具有無效RSA簽名的鏈。 請考慮鏈CA > ICA > EE，其中CA在ICA上的簽名無效。 如果此設定為true，則鏈式構建將停止在ICA，而CA不會包含在鏈中。 如果此設定為false，則會產生完整的3憑證鏈。 此設定不會影響DSA簽名。 預設值為false。

### 時間戳提供程式選項{#timestamp-provider-options}

**TSP伺服器URL:** 預設時間戳記提供者的URL。僅在提供了某些有效值時使用。 無預設值。

**TSP伺服器使用者名稱：** 時間戳記提供者要求的使用者名稱。僅當為URL提供了某些有效值時才使用。 無預設值。

**TSP伺服器密碼：** 時間戳提供程式要求時上述使用者名稱的密碼。僅當為URL和使用者名稱提供了某些有效值時才使用。 無預設值。

**請求雜湊演算法：** 指定為時間戳提供者建立請求時要使用的雜湊演算法。預設值為SHA1。

**吊銷檢查樣式：** 指定用於從觀察到的吊銷狀態中確定時間戳提供程式證書的信任狀態的吊銷檢查樣式。預設值為BestEffort。

**傳送Nonce:** 指定是否隨時間戳記提供者要求傳送Nonce。Nonce可以是時間戳記、網頁上的造訪計數器，或用來限制或防止未授權的重播或重放檔案的特殊標籤。 預設值為true。

**在驗證期間使用過期時間戳：** 選取此選項時，過期的時間戳可用於擷取簽名的驗證時間。預設值為true。

**TSP回應大小：** TSP回應的預估大小（以位元組為單位）。此值應代表已設定時間戳記提供者可傳回之時間戳記回應的最大大小。 除非您完全確定，否則請勿更改此項。 最小值為60B，最大值為10240B。 預設值為4096B。

**忽略TimeStamp伺服器擴展**:選擇「 **忽略TimeStamp伺** 服器擴展」選項，以阻止AEM Forms伺服器與指定的時間戳伺服器聯繫。選取選項有助於避免因AEM Forms與時間戳記伺服器之間的連線逾時而發生的程式失敗。

### 證書吊銷清單選項{#certificate-revocation-list-options}

**請首先查閱本地URI:** 指定是否應將本地URI或CRL查找中提供的CRL位置指定為優先於證書中指定的任何位置，以便進行吊銷檢查。預設值為false。

**CRL查找的本地URI:** 本地CRL提供程式的URL。僅當Consult Local URI First設定設定為true時，才咨詢此值。 無預設值。

**吊銷檢查樣式：** 指定用於從觀察到的吊銷狀態確定CRL提供程式證書信任狀態的吊銷檢查樣式。預設值為BestEffort。

**用於CRL查找的LDAP伺服器：** 用於獲取CRL的LDAP伺服器(如www.ldap.com)。所有基於DN的CRL查詢都將定向到此伺服器。 無預設值。

**聯機：** 指定是否聯機以提取CRL。如果為false，則只咨詢快取的CRL（在本地磁碟上或嵌入簽名的CRL）。 預設值為true。

**忽略有效日期：** 指定是否忽略響應的thisUpdate和nextUpdate時間，這可防止這些時間對響應有效性產生負面影響。預設值為false。

**在CRL中需要AKI擴展：** 指定是否必須將授權密鑰標識符擴展包含在CRL中。預設值為false。

### 聯機證書狀態協定選項{#online-certificate-status-protocol-options}

**OCSP伺服器URL:** 預設OCSP伺服器的URL。是否使用透過此URL指定的OCSP伺服器取決於「要查詢的URL」選項設定。 無預設值。

**要查詢的URL選項：** 控制用於執行狀態檢查的OCSP伺服器的清單和順序。預設值為UseAIAInCert。

**吊銷檢查樣式：** 指定在驗證OCSP伺服器的證書時使用的吊銷檢查樣式。預設值為CheckIfAvailable。

**傳送Nonce:** 指定是否隨OCSP要求傳送Nonce。Nonce可以是時間戳記、網頁上的造訪計數器，或用來限制或防止未授權的重播或重放檔案的特殊標籤。 預設值為true。

**最大時鐘偏斜時間：** 在響應時間和本地時間之間允許的最大偏差（以分鐘為單位）。最小值為0，最大值為2147483647m。 預設值為5m。

**回應時效性時間：** 將預先建構的OCSP回應視為有效的最長時間（以分鐘為單位）。最小值為1m，允許的最大值為2147483647。 預設值為525600（一年）。

**簽署OCSP請求：** 指定是否應簽署OCSP請求。預設值為false。

**請求籤名者憑據別名：** 指定在啟用簽名時用於簽名OCSP請求的憑據別名。僅在啟用OCSP請求籤名時使用。 無預設值。

**上線：** 指定是否要上線以進行吊銷檢查。預設值為true。

**忽略響應的thisUpdate和nextUpdate時間：** 指定是否忽略響應的thisUpdate和nextUpdate時間，這可防止這些時間對響應有效性產生負面影響。預設值為false。

**允許OCSPNoCheck擴展：** 指定是否在響應簽名證書中允許OCSPNoCheck擴展。預設值為true。

**需要OCSP ISIS-MTT CertHash擴充功能：** 指定OCSP回應中是否必須包含憑證公開金鑰雜湊擴充功能。預設值為false。

### {#error-handling-options-for-debugging}調試的錯誤處理選項

**下次API呼叫時清除憑證快取：** 指定下次呼叫簽名服務作業時是否要清除憑證快取。呼叫操作後，此選項會設回false。 預設值為false。

**在下次API調用時清除CRL快取：** 指定是否在調用下次簽名服務操作時清除CRL快取。呼叫操作後，此選項會設回false。 預設值為false。

**在下次API呼叫時清除OCSP快取：** 指定是否在下次呼叫簽名服務作業時清除OCSP快取。呼叫操作後，此選項會設回false。 預設值為false。

## 已觀看資料夾服務設定{#watched-folder-service-settings}

「觀看資料夾」服務(`WatchedFolder`)配置所有觀看資料夾端點的共同屬性。 它也提供受監視資料夾端點的預設值。 （請參閱[設定觀看的資料夾端點](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints)。） 外部用戶端應用程式不會叫用它，或用於在Workbench中建立的程式。

「已觀看資料夾」服務可使用下列設定。

**Cron運算式：** 用於調度輸入目錄輪詢的Cron運算式。

**重複計數：** 輪詢輸入目錄的次數。如果未在端點配置中指定此值，則使用的預設重複計數。 值–1表示對目錄進行了無限掃描。 預設值為–1。

**重複間隔：** 如果每次輪詢之間的秒數為預設數。除非在監看的資料夾端點設定中指定了不同的值，否則此值將用作重複間隔。 預設值為 5。如需詳細資訊，請參閱批次大小設定的說明。

**非同步：** 將呼叫類型識別為非同步或同步。只能同步調用瞬態和同步進程。 預設值為非同步。

**等待時間：** 從輸入資料夾擷取檔案的預設時間值（以秒為單位）。如果檔案或資料夾早於等待時間中指定的時間，系統會擷取該檔案或資料夾以進行處理。 預設值為 0。

**批次大小：** 每次掃描處理的檔案或資料夾數量的預設值。預設值為 2。

「重複間隔」和「批次大小」設定決定「監看資料夾」在每次掃描中擷取的檔案數。 「監視資料夾」使用Quartz線程池掃描輸入資料夾。 線程池與其他服務共用。 如果掃描間隔較小，線程會經常掃描輸入資料夾。 如果檔案經常被拖放到監看的資料夾中，請保持較小的掃描間隔。 如果檔案不常被刪除，請使用較大的掃描間隔，以便其他服務可以使用線程。

如果要刪除的檔案量很大，請使批處理大小較大。 例如，如果受監視資料夾端點調用的服務每分鐘可處理700個檔案，並且用戶以相同的速率將檔案拖放到輸入資料夾中，則將「批大小」設定為350，將「重複間隔」設定為30秒，將有助於「受監視資料夾」的效能，而不會導致掃描受監視資料夾的成本過多。

將檔案放入觀看的資料夾時，會列出輸入中的檔案，如果每秒都進行掃描，會降低效能。 增加掃描間隔可以提高效能。 如果要丟棄的檔案量較小，請相應調整「批大小」和「重複間隔」。 例如，如果每秒丟棄10個檔案，請嘗試將「重複間隔」設定為1秒，將「批大小」設定為10。

在群集配置中，監視資料夾終結點的批處理大小不會擴展到多個群集節點。 例如，如果為兩節點群集將批大小設定為`2` ，並且選擇了「節點」選項，則節點將以兩個批次集體處理檔案，而不是每個節點一次處理兩個檔案。

**覆寫重複檔案名：** 一個布林字串，指定監視的資料夾是否覆蓋重複的結果檔案名以及是否應覆蓋保留的同名文檔。

**保留資料夾：** 保留資料夾的預設值。此資料夾用於將源檔案複製到中，以備成功處理輸入時使用。 此值可以是空路徑、相對路徑或具有檔案模式的絕對路徑，如「結果資料夾」設定所述。

**失敗資料夾：** 複製失敗檔案的資料夾名稱。此值可以是空路徑、相對路徑或具有檔案模式的絕對路徑，如「結果資料夾」設定所述。

**結果資料夾：** 結果資料夾的預設名稱。此資料夾用於將結果檔案複製到中。 此值可以是空路徑、相對路徑或具有下列檔案模式的絕對路徑。

* %F =檔案名首碼
* %E =副檔名
* %Y =年（已滿）
* %y =年（最後兩位）
* %M =月
* %D =月中的第幾天
* %d =年
* %H =小時（24小時時鐘）
* %h =小時（12小時時鐘）
* %m =分鐘
* %s =秒
* %l =毫秒
* %R =隨機數（從0到9）
* %P =進程或作業ID

例如，如果2009年7月17日晚上8點，而您指定了`C:/Test/WF0/failure/%Y/%M/%D/%H/`，則結果資料夾為`C:/Test/WF0/failure/2009/07/17/20`。

如果路徑不是絕對路徑，而是相對路徑，則會在觀看的資料夾內建立資料夾。 有關檔案模式的詳細資訊，請參閱[關於檔案模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns)。

>[!NOTE]
>
>結果資料夾的大小越小，「觀看的資料夾」效能就越好。 例如，如果監看資料夾的預計負載每小時為1000個檔案，請嘗試類似`result/%Y%M%D%H`的模式，以便每小時建立一個新子資料夾。 如果載入較小（例如，每天1000個檔案），您可以使用`result/%Y%M%D`之類的模式。

**預備資料夾：** 觀看資料夾內的預備資料夾的預設名稱。

**輸入資料夾：** 觀看資料夾內輸入資料夾的預設名稱。

**失敗時保留：** 如果為true，則失敗時原始檔案會保留在失敗資料夾中。

**限制：** 選取此選項時，會限制AEM表單在任何指定時間處理的已觀看資料夾作業數量。Batch Size值確定作業的最大數量（請參閱關於限制）。

## Web服務設定{#web-service-service-settings}

Web服務服務(`WebService`)使進程能夠調用Web服務操作。

Web服務使進程能夠調用Web服務操作。 例如，組織可能希望通過調用服務提供商公開的Web服務來整合一個過程以儲存和檢索諸如聯繫人和帳戶詳細資訊之類的資訊。 Web服務調用指定的Web服務並傳遞其每個參數的值。 接著，會將操作的傳回值儲存至處理程式內指定的變數。

Web服務通過發送和接收SOAP消息來與Web服務交互。 該服務還支援使用WS-Attachment協定發送帶有SOAP消息的MIME、MTOM和SwaRef附件。 Web服務交互與SAP系統和.NET Web服務相容。

Web服務可使用下列設定。

**金鑰存放區：** 金鑰存放區檔案的完整路徑，其中包含要用於驗證的私密金鑰。表單伺服器必須能夠存取檔案。

**金鑰存放區密碼：** 金鑰存放區檔案的密碼。

**金鑰存放區類型：** 金鑰存放區的類型。請不提供值來使用為運行表單伺服器的JVM配置的預設密鑰庫類型。 否則，請提供下列其中一個值：

* jks
* pkcs12
* cms
* jceks

**信任存放區：** 包含Web服務伺服器公開金鑰之信任存放區檔案的完整路徑。

**信任儲存密碼：** 信任儲存檔案的密碼。

**信任存放區類型：** 信任存放區的類型。請不提供值來使用為運行表單伺服器的JVM配置的預設密鑰庫類型。 否則，請提供下列其中一個值：

* jks
* pkcs12
* cms
* jceks

## XSLT轉換服務設定{#xslt-transformation-service-settings}

XSLT轉換服務(`XSLTService`)使進程能夠在XML文檔上應用可擴展樣式表語言轉換(XSLT)。

下列設定可用於XSLT轉換服務。

**工廠名稱：** 用於執行XSLT轉換的Java類的完全限定名稱。如果未指定值，則使用運行表單伺服器的Java虛擬機中配置的預設工廠。

## 修改服務{#modifying-security-settings-for-a-service}的安全設定

forms伺服器可讓您為每個服務配置安全設定，從而允許您按服務級別配置細粒度的訪問控制。

已安裝預設安全性設定檔，然後可依您的系統需求進行設定。 每個安全配置檔案都有一個關聯的域，並在用戶級別或組級別建立。

### 修改服務{#modify-security-settings-for-a-service}的安全設定

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「服務管理」。
1. 在「服務管理」頁上，按一下要配置的服務。
1. 按一下「安全性」標籤。
1. 在「要求呼叫者進行身份驗證」清單中，選擇「是」或「否」以指定是否可以使用或不使用憑據調用該服務。

   如果選擇「是」，則必須驗證服務的調用方，並且必須授權該調用方的用戶主體調用該服務；否則，將拒絕調用嘗試。

   如果選擇「否」，則服務的呼叫者可能或可能未被驗證。 由於沒有授權檢查，服務調用將始終成功。

1. 對於包含標籤為匿名訪問的一個或多個操作的服務，請選擇或取消選擇「允許匿名訪問」。 啟用匿名訪問時，系統內的任何用戶都可以調用該服務的操作。 如果禁用匿名訪問，則必須授予用戶調用服務和調用操作的權限。 使用者可直接取得這些權限，或作為具有這些權限之群組的一員。
1. 對於某些服務，執行該操作的用戶帳戶會影響結果。 例如，在「內容服務」（已過時）中，儲存內容的使用者會設為內容的擁有者，這會影響之後可以存取內容的使用者。 如果您使用進程來儲存內容，請考慮使用哪個用戶來執行文檔管理服務，因為該用戶將擁有所儲存的內容。

   要指定服務用於執行操作的運行時標識，請選擇指定運行方式，從關聯清單中選擇一個選項，然後按一下保存。 從下列選項中選擇：

   **調用者：** 使用與叫用服務的使用者相同的身分。

   **系統：** 使用系統用戶以完全權限運行服務。

   **指名的使用者：** 可讓您以特定使用者身分執行服務。選擇此選項時，按一下「選擇用戶」(Select User)以顯示「選擇承擔者」(Select Principal)頁，在該頁中可以搜索並選擇用戶。

   如果未選擇指定運行方式，則使用預設行為。

   >[!NOTE]
   >
   >隨xfaForm、Document Form和Form變數一起使用的轉譯和提交服務，一律使用系統使用者帳戶執行。

1. 按一下「新增主體」 ，指定使用者和群組對此服務擁有的權限。
1. 選擇主體螢幕顯示在用戶管理中配置的用戶和組。 如果未顯示您想要的用戶或組，請使用搜索函式來查找它。 按一下使用者或群組名稱。
1. 在「新增權限」畫面中，選取要指派給此服務之使用者或群組的權限：

   * **INVOKE_PERM:** 調用服務上的所有操作
   * **MODIFY_CONFIG_PERM:** 修改服務的配置
   * **SUPERVISOR_PERM:** 查看從進程建立的服務的進程實例資料
   * **START_STOP_PERM:** 啟動和停止服務
   * **ADD_REMOVE_ENDPOINTS_PERM:** 添加、刪除和修改服務的端點
   * **CREATE_VERSION_PERM:** 建立服務的新版本
   * **DELETE_VERSION_PERM:** 刪除服務版本的方式
   * **MODIFY_VERSION_PERM:** 修改服務版本的方式
   * **READ_PERM:** 檢視服務的方式
   * **PROCESS_OWNER_PERM:** 以用於未來版本的AEM表單。請勿使用此權限。
   * **SERVICE_MANAGER_PERM:** 以用於未來版本的AEM表單。請勿使用此權限。
   * **SERVICE_AGENT_PERM:** 以用於未來版本的AEM表單。請勿使用此權限。

1. 按一下「新增」。

### 從安全配置檔案{#remove-the-principal-from-a-security-profile}中刪除主體

1. 在「服務管理」頁上，選擇要配置的服務。
1. 按一下&#x200B;**Security**&#x200B;頁簽，選擇要刪除的安全配置檔案，然後按一下&#x200B;**Remove**。

## 配置服務{#configuring-pooling-for-a-service}的池

每個服務都可以利用池功能來處理傳入的調用請求。 使用服務池可確保服務實例一次由單個線程調用，並在調用請求間重複使用，這可能導致效能的提高。 您也可以使用集區來指定「最大非同步服務實例數」選項，該選項允許服務限制並行處理的請求數。

### 啟用池{#enable-pooling}

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「服務管理」。
1. 在「服務管理」頁上，按一下要配置的服務。
1. 按一下「集區」標籤。
1. 在「請求處理策略」清單中，選取所有請求的池化例項。
1. 在「初始服務實例池大小」框中，輸入池的初始大小。 在部署服務時，此數字用於確定建立並分配給空閒池、等待調用請求的服務實現實例的數量。 這可讓服務容器立即回應叫用請求，而不需先初始化服務例項。
1. 在「最大服務實例池大小」框中，輸入給定服務的池中的最大實例數。 此設定控制在給定時間可執行給定服務的線程數。 預設值為0，因此池大小不限。
1. 在「最大非同步服務實例數」框中，輸入池中可用於在任何給定時間處理非同步請求的最大實例數。 此設定可讓服務限制可同時處理的請求數。
1. 在「調用等待超時」框中，輸入等待服務可用於調用請求的毫秒數。 如果未指定此設定的值，則預設值為0，因此不會有等待時間。
1. 按一下「儲存」。

### 刪除池{#remove-pooling}

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「服務管理」。
1. 在「服務管理」頁上，按一下要配置的服務。
1. 按一下「集區」標籤。
1. 在「請求處理策略」清單中，為每個請求選擇新例項，或為所有請求選擇單一例項。

   **所有請求的單一例項：** 當第一個請求進入容器時，會建立並快取服務例項。該要求之後的每個要求都會使用相同的服務例項來處理要求。

   **每個請求的新例項：** 會為收到的每個呼叫建立新的服務例項。

1. 按一下「儲存」。
