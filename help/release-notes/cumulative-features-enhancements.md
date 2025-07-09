---
title: Adobe Experience Manager 6.5版本中的累積主要功能和增強功能。
description: Adobe Experience Manager 6.5在前八個Service Pack發行版本中所做主要功能和增強功能的累計清單。
content-type: reference
docset: aem65
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 01fe5b53-2244-445f-a4d0-bd58ea38b611
solution: Experience Manager
source-git-commit: eef3ad559612c338de0c4232aadc4133c910aaf8
workflow-type: tm+mt
source-wordcount: '3109'
ht-degree: 13%

---

# 累積的重要功能和增強功能

舊版八個Service Pack所累積的Adobe Experience Manager 6.5主要功能和增強功能清單。

另請參閱[Adobe Experience Manager 6.5最新Service Pack發行說明](/help/release-notes/release-notes.md)。


## AEM 6.5， Service Pack 23—2025年5月22日

### Forms {#forms-sp23}

* [在靜態PDF中具有混合文字樣式的輔助功能超連結](https://helpx.adobe.com/tw/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf)：在靜態PDF中包含混合文字樣式的超連結，現在已標籤為單一輔助功能元素。 此增強功能簡化了標籤樹結構、改善了熒幕助讀程式導覽，並支援更出色的協助工具合規性。

* [已更新支援的平台矩陣](/help/forms/using/aem-forms-jee-supported-platforms.md)

  最新版本引進了支援平台對照表的更新，確保與更新技術相容。

   * IBM® Content Manager Client 8.7

   * MongoDB Enterprise 7.0

   * MySQL 8.4

   * Microsoft® SQL Server 2022

   * Microsoft® SQL Server JDBC驅動程式12.8

   * Red Hat® Enterprise Linux® 9 （核心4.x，64位元）

* [強化的檔案附件元件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment)：作為安全性測量，此元件現在會防止提交副檔名經過修改、嘗試略過允許的檔案型別檢查的檔案。 提交期間會封鎖這類檔案，以確保僅接受有效的檔案型別。

## AEM 6.5， Service Pack 22—2024年11月21日

### Sites {#sites}

[Universal Editor](/help/sites-developing/universal-editor/introduction.md)現在可在AEM 6.5上用於套用Feature Pack的Headless使用案例。

### [!DNL Assets]

IPTC索引標籤現在支援[!UICONTROL 替代文字]和[!UICONTROL 延伸說明]文字欄位。 (Assets-34918)

### Forms {#forms-sp22}

#### AEM Forms中的新GA功能 {#ga-aem-forms-sp22}

* 新增在[Interactive Communications Batch API](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/interactive-communications/create-interactive-communication#output-format-print-channel)中啟用字型內嵌的支援 — 現在，Interactive Communications支援在透過Batch API產生的PDF中內嵌Adobe Ming和Adobe Myungjo字型。 此增強功能可確保產生的檔案能正確呈現文字，即使使用字型子集亦然，改善了PDF輸出中的多語言內容支援。

* [適用於PDF協助工具的內容目錄API](/help/forms/using/aem-document-services-programmatically.md#auto-tag-pdf-documents-auto-tag-api) - OSGi上的AEM Forms現在支援新的TOC標籤API，以增強PDF的協助工具標準。 它可讓具有輔助技術的使用者更容易存取PDF。

* [片段XDP解析](/help/forms/using/assembler-service.md#resolve-references-on-crx-repository-resolve-references-on-crx-repository) - OSGi上的AEM Forms現在解析主要XDP中參考並儲存在AEM CRX存放庫中的片段XDP。

* [PDF/A合規性增強功能](/help/forms/developing/pdf-a-documents.md#converting-documents-to-pdfa-documents-converting-documents-to-pdf-a-documents) — 現在，使用者可以將PDF轉換為PDF/A格式(1a、2a、3a)以進行封存，同時確保可存取性並驗證是否符合這些標準。

* **支援靜態PDF檔案的自動調整字型大小** - AEM Forms Designer、OutputService和FormsService現在支援靜態PDF的自動調整字型大小。 如果使用者將文字、數值、密碼或日期時間欄位的字型大小設為0，則字型大小會自動調整這些欄位中的字型大小，而不會改變欄位的整體大小。 若要使用此功能，使用者會在自訂XCI中傳遞旗標： `<behaviorOverride>patch-LC-3921991:1</behaviorOverride>`。

#### AEM Forms的Beta新功能 {#beta-aem-forms-sp22}

Beta版功能為您提供獨一無二的機會，讓您以獨家方式存取尖端的創新技術，並幫助打造其開發藍圖。 有興趣為您的環境啟用Beta版功能嗎？ 從您的正式地址傳送電子郵件至aem-forms-ea@adobe.com ，其中包含您感興趣的功能清單。

* [驗證碼](/help/forms/using/integrate-adaptive-forms-hcaptcha.md)和[Cloudflare Turnstile驗證碼服務](/help/forms/using/integrate-adaptive-forms-turnstile.md)： AEM Forms支援下列Captcha服務：
   * 驗證碼會使用核取方塊Widget來挑戰使用者，以保護表單免受機器人、垃圾訊息和自動化濫用。 這樣可確保只有人類使用者才能進行，進而增強線上交易的安全性。
   * Cloudflare Turnstile提供安全性措施，旨在保護表單免受自動化機器人、惡意攻擊、垃圾郵件以及不需要的自動化流量的侵害。 在允許提交表單前，它會在表單提交上顯示核取方塊，以驗證使用者是否為人類。

* 最適化表單版本設定：
   * [建立多個版本的最適化表單](/help/forms/using/add-versioning-reviews-comments.md) — 現在，使用者可以輕鬆管理現有表單的變化。 此程式可簡化版本控制，並有助於表單最佳化的比較，而這一切都可在單一、簡化的工作流程中完成。
   * [比較最適化Forms](/help/forms/using/compare-forms-core-components.md)：使用者現在可以輕鬆比較兩種表單以找出差異。 這可方便團隊成員有效地比較修訂版本並討論變更，進而讓成員可順利協作。

## AEM 6.5， Service Pack 21—2024年6月6日

### [!DNL Assets]

#### 增強功能

IPTC索引標籤現在支援[!UICONTROL 替代文字]和[!UICONTROL 延伸說明]文字欄位。 (Assets-34918)

#### 協助工具

* 如果資產的處理狀態為「失敗」或「中繼資料失敗」，註解和音訊追蹤UI現在可以正常運作。 (Assets-37281)
* 儲存資產中繼資料並嘗試編輯時，現在會顯示語言名稱。 (Assets-37281)

### [!DNL Forms]

* **支援Oauth認證**：新的、更易於使用伺服器對伺服器驗證的認證，取代現有的服務帳戶(JWT)認證。 (NPR-41994)
* AEM Forms中的[規則編輯器增強功能](/help/forms/using/rule-editor-core-components.md)：
   * 支援以`When-then-else`功能實作巢狀條件。
   * 驗證或重設面板和表單，包括欄位。
   * 支援現代JavaScript功能，例如「自訂函式」中的let和arrow函式（ES10支援）。
* [適用於PDF協助工具的AutoTag API](/help/forms/using/aem-document-services-programmatically.md#doc-utility-services-doc-utility-services)： OSGi上的AEM Forms現在支援新的AutoTag API，透過新增標籤：段落和清單來增強PDF的協助工具標準。 它可讓具有輔助技術的使用者更容易存取PDF。
* **16位元PNG支援**： PDF Generator的ImageToPdf服務現在支援16位元色彩深度的PNG轉換。
* **將成品套用至XDP中的個別文字區塊**： Forms Designer現在可讓使用者在XDP檔案中的個別文字區塊上設定設定。 此功能可讓您控制在產生的PDF中被視為成品的元素。 這些元素（例如頁首和頁尾）可供輔助技術存取。 主要功能包括將文字區塊標示為成品，並將這些設定內嵌於XDP中繼資料。 Forms Output服務會在產生PDF期間套用這些設定，以確保正確使用PDF/UA標籤。
* **AEM Forms Designer已通過`GB18030:2022`標準認證**：透過`GB18030:2022`認證，Forms Designer現在支援中文Unicode字元集，可讓您在所有可編輯的欄位和對話方塊中輸入中文字元。
* [在JEE伺服器](/help/forms/using/admin-help/configure-service-settings.md#generate-pdf-service-settings-generate-pdf-service-settings)中使用PDF Generator服務支援WebToPDF路由，現在支援將HTML檔案轉換為JEE上的PDF檔案的WebToPDF路由。 此支援是現有Webkit和WebCapture （僅限Windows）路由的補充。 雖然WebToPDF路由可在OSGi上取得並延伸至JEE。 現在，在JEE和OSGi平台上，PDF Generator服務支援跨不同作業系統的下列路由：
   * **Windows**： Webkit、WebCapture、WebToPDF
   * **Linux®**： Webkit， WebToPDF


## AEM 6.5， Service Pack 20—2024年2月22日

### [!DNL Assets]

* Dynamic Media現在支援Apple iOS/iPadOS的無損HEIC影像格式。 請參閱Dynamic Media影像提供與轉譯API中的[fmt](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt)。
* 多站台管理員(MSM)現在支援體驗片段結構，包括資料夾和子資料夾，以便有效地將體驗片段大量轉出到即時副本。

### [!DNL Forms]

* **JEE版AEM Forms的交易報告功能**：已針對JEE版AEM Forms引入交易報告功能。 它可全面記錄檔案交易，例如轉換、轉譯和提交。 此增強功能可提高效率，並有助於更好地儲存記錄。 此功能預設為停用。 您可以從管理員UI啟用它。
* **具有ECDSA支援的增強式安全性**： AEM Forms現在針對JEE和OSGi棧疊的橢圓曲線數位簽名演演算法(ECDSA)提供強大的支援。 使用者現在可以透過增強的安全性來簽署、認證及驗證PDF檔案。 支援的EC曲線演演算法包括：
   * 使用SHA256摘要演演算法的ECDSA橢圓曲線P256
   * 使用SHA384摘要演演算法的ECDSA橢圓曲線P384
   * 使用SHA512摘要演演算法的ECDSA橢圓曲線P512
* **與Forms Designer的Windows 11緊密相容**： AEM Forms Designer現在支援Windows 11，確保順利安裝和操作。 使用者可以放心地升級至Windows 11，不必重新安裝Forms Designer，也不用擔心相容性問題，確保工作流程不會中斷。
* **AEM Forms Designer中的自訂「Caption」角色強化協助工具**： AEM Forms Designer現在包含名為「Caption」的自訂協助工具角色，可讓使用者使用個人化的字幕元素來建立XDP。 此功能可讓使用者將自訂註解整合到其檔案設計中，藉此增強協助工具，進而改善包容性和使用者體驗。

## AEM 6.5， Service Pack 19—2023年12月7日

* 啟用Sites頁面編輯器/影像元件使用者，以參照遠端Assets Cloud Service的資產。 (SITES-13448， SITES-13433)
* AEM現在支援伺服器端排序，以便在「清單」檢視中更快速地導覽專案。 專案節點會在出現在介面之前，根據使用者選取的欄排序。

### [!DNL Forms]

* **新最適化表單核心元件**：已新增垂直標籤、條款與條件以及核取方塊，以提升表單的擴充性。
   * **[核取方塊元件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox)**：以核心元件為主的最適化表單現在可以包含核取方塊元件。可讓使用者二選一，選取或取消選取特定選項。它通常為一個小方塊，可以按一下或點選以在兩種狀態之間切換：選取和取消選取。核取方塊是一種常見的表單元素，用來表示選擇是/否或真/假。

   * **[條款與條件元件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions)**：核心元件型最適化Forms現在包含條款與條件元件。 表單作者新增此區段，向使用者顯示服務、產品或平台的條款、條件或法律合約。 此元件的設計用意是在告知使用者他們透過提交表單同意的規則、法規和義務。

     ![垂直標籤、條款與條件及核取方塊元件](/help/forms/using/assets/forms-components.png)

   * **[垂直標籤元件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs)**：以核心元件為主的最適化表單現在可以將表單內容組織成垂直的標籤清單，提供結構化、可導覽的版面。表單中的垂直標籤可簡化導覽和組織內容，進而增強使用者體驗。 當表單包含多個區段或複雜資訊時，這些變數特別實用。

* **[64位元版本的AEM Forms Designer](/help/forms/using/installing-configuring-designer.md)**： 64位元版本的AEM Forms Designer提供增強的效能、擴充能力及記憶體管理，讓您能夠建立表單。 透過 64 位元架構，您可以輕鬆處理更大、更複雜的專案，確保設計工作流程流暢和最佳效率。透過這最先進的版本，提升您的表單設計能力並擁抱 AEM Forms Designer 的未來。

* **[連線最適化Forms與Microsoft® SharePoint清單](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)**： AEM Forms提供立即可用的整合，可直接將表單資料提交至SharePoint清單，讓您使用SharePoint的清單功能。 您可以將Microsoft® SharePoint清單設定為表單資料模型的資料來源，並使用使用表單資料模型提交動作來連線最適化表單與SharePoint清單。

* **[支援設定最適化表單片段的記錄檔案屬性](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)**：您現在可以輕鬆自訂最適化表單片段及其在最適化表單編輯器中的欄位。

* **64位元XMLFM**： XMLFM的64位元反複專案提供更優異的效能、擴充能力，以及更精細的記憶體管理。 這是第一個在伺服器端部署的64位元原生服務。 XMLFM 64位元可利用其固有的功能，存取與32位元對應的記憶體資源相比更大的記憶體資源，因此能夠順暢處理更大的演算工作負載。 這個里程碑不僅代表效能的飛躍，也為AEM Forms伺服器內的原生服務架構引入重要增強功能。 此更新讓AEM Forms Server能夠順暢地支援任何64位元原生服務。

## AEM 6.5， Service Pack 18—2023年8月24日

* Assets、Dynamic Media - [Dynamic Media中視訊的多重字幕與音軌支援](/help/assets/video.md#about-msma) — 您現在可以輕鬆地將多重字幕與多重音軌新增到主要視訊。 擁有此功能代表全球觀眾都可以存取您的影片。您可以著手自訂一部已發佈的主要影片，以多種語言提供給全球觀眾，並遵守不同地理區域的無障礙指南。作者還可以從使用者介面中的單個標籤管理字幕和音訊。
* Assets — 您現在可以從搜尋結果導覽至包含資產的檔案夾位置，讓您執行各種資產管理任務。
* 內容片段中的Sites Polaris選取器已改善效能。
* 啟用Sites頁面編輯器/影像元件使用者，以參照遠端Assets Cloud Service的資產。
* 為了在「清單」檢視中快速找到系統中可能有多個專案的專案，Adobe現在支援伺服器端排序。 專案節點會在使用者介面中呈現之前，根據使用者選取的欄在後端排序。
* AEM 6.5.18.0支援MongoDB 5.0至6.0。

### [!DNL Forms]

* **[規則編輯器中使用自訂錯誤處理常式的增強錯誤處理](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms)** — 您現在可以叫用自訂函式（使用使用者端程式庫）來回應外部服務傳回的錯誤。 此外，您也可以為使用者提供量身打造的回應。 或者，您可以針對服務傳回的錯誤採取特定動作。例如，您可以在後端叫用自訂工作流程來取得特定錯誤代碼，或通知客戶服務已停止服務

* **[增強型Adobe Sign工作流程步驟](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/workflows/aem-forms-workflow-step-reference#sign-document-step)** - AEM工作流程中的Adobe Sign工作流程步驟提供下列增強功能。

   * **Adobe Sign的政府機關身分證件驗證強化安全性** - Adobe Acrobat Sign的政府機關身分證件驗證提供額外的驗證層。 它可讓使用者使用政府頒發的ID （駕照、國民身分證、護照）來驗證身分。 此增強功能利用受信任的身分識別文件為簽名過程額外增加一層可信度，使其成為需要增強安全性、合規性和使用者驗證等情境的理想選擇。

   * **使用Adobe Sign檔案的稽核軌跡來增強透明度** — 使用稽核軌跡功能來深入瞭解Adobe Sign檔案的生命週期。 使用「稽核軌跡」，您現在可以維護與檔案相關的所有動作與互動的完整記錄。 這些動作和互動包括檢視、編輯或簽署檔案的人員，以及每個事件的時間戳記。 此加強功能對於維持合規性、解決爭議和確保數位協議的完整性至關重要。


   * **將合約收件者的角色擴充至簽署者** - Adobe Acrobat Sign可讓您將合約收件者的角色擴充至簽署者之外，以便更符合其工作流程需求。 啟用後，協定中的每個收件者皆可個別設定其角色，預設為簽署者。


* **[JEE上的AEM Forms完整安裝程式](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms)** — 此Service Pack為JEE上的AEM Forms提供完整安裝程式，可支援多種新軟體組合，包括：
   * Microsoft® Windows Server 2022
   * Microsoft® Active Directory 2022
   * Windows Server 2022上的Oracle WebLogic 14C
   * Red Hat® JBoss® 7.4.10
   * MongoDB 6.0 <!-- it was previously MongoDB 4.4 -->
   * MySQL JDBC聯結器8

如果您在JEE環境中安裝或計畫使用適用於AEM 6.5 Forms的最新軟體，Adobe建議在JEE完整安裝程式上使用AEM 6.5.18.0 Forms 。 若要探索新增和淘汰的軟體的完整清單，請參閱JEE上的AEM Forms或OSGi上的AEM Forms檔案。

## AEM 6.5， Service Pack 17—2023年5月25日

* **搜尋體驗增強功能** - 您現在可以對搜尋結果中顯示的資產快速執行以下作業：
   * 建立工作流程
   * 建立版本
   * 建立資產關聯或取消關聯

  若要執行這些作業，您並不需要瀏覽至資產位置及檢視其屬性。

* **Dynamic Media _快照_**&#x200B;可讓您使用測試影像或Dynamic Media URL，預覽影像修飾元和智慧型影像最佳化，例如WebP或AVIF輸出、頻寬感知壓縮和裝置畫素比例縮放。 然後您可以立即比較每個設定對品質和檔案大小的影響。
請參閱 [Dynamic Media 快照](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot)。
* **使用Dynamic Media的DASH串流** — 針對Dynamic Media視訊傳送中的自我調整串流（已啟用CMAF）啟動新通訊協定（DASH — 透過HTTP的動態自我調整串流）。 現在可供所有區域使用。
* **整合Experience Manager Sites和內容片段與Assets新一代Dynamic Media** — 使用者現在可以在Experience Manager Sites 6.5中使用其雲端託管的資產。他們可以在內部部署或Managed Services執行個體上編寫及傳遞這些資產。

### [!DNL Forms]

* **[AEM頁面編輯器中的最適化Forms](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)** — 您現在可以使用AEM頁面編輯器快速建立多個表單並新增到您的網站頁面。 此功能讓內容作者可使用最適化表單元件 (包括動態行為、驗證、資料整合、產生記錄文件和業務流程自動化) 的強大功能，在 Sites 頁面內建立順暢的資料擷取體驗。您可以：
   * 建立最適化表單，方法是將表單元件拖放至AEM Sites編輯器或體驗片段中的最適化Forms容器元件。
   * 在AEM Sites編輯器中使用最適化Forms精靈，以便您可以獨立於任何Sites頁面來建立表單，讓您自由地在多個頁面中重複使用這類表單。
   * 將多個表單新增到 Sites 頁面，簡化使用者體驗並提供更大的彈性。
* **[Experience Manager Forms中的reCAPTCHA Enterprise支援](/help/forms/using/captcha-adaptive-forms.md)** — 新增Experience Manager Forms中的reCAPTCHA Enterprise支援。 除了現有的Google reCAPTCHA v2支援之外，此功能還提供更強大的保護，以防止詐騙活動和垃圾郵件。
* **[新增對具有Experience Manager Forms的政府用Adobe Acrobat Sign的支援](/help/forms/using/adobe-sign-integration-adaptive-forms.md)** - AEM Forms現在與適用於政府的Adobe Acrobat Sign整合（符合FedRAMP規範）。 此整合針對政府相關帳戶（政府部門和機構）提交的Adaptive Form，提供電子簽章的進階法規遵循與安全性。 與適用於政府的Adobe Acrobat Sign整合，可讓Adobe的合作夥伴和政府客戶在Adaptive Forms中使用電子簽章，從事最關鍵和敏感的業務線。 這額外一層的安全性可確保所有電子簽名完全符合 FedRAMP 中等合規性，讓 Adobe 的政府客戶安心使用。
* **啟用Salesforce與Experience Manager Forms的整合以進行資料交換** — 使用OAuth 2.0使用者端憑證流程設定Experience Manager Forms與Salesforce應用程式之間的整合。 此功能可啟用應用程式的安全且直接的驗證和授權，並允許無縫通訊，而不需要使用者介入。
* **最佳化及增強工作流程引擎的功能**：將工作流程執行個體數目減到最少，以提高工作流程引擎的效能。 除了`COMPLETED`和`RUNNING`狀態值之外，工作流程也支援三個新的狀態值： `ABORTED`、`SUSPENDED`和`FAILED`。

## AEM 6.5， Service Pack 16—2023年2月23日

新通訊協定DASH (Dynamic Adaptive Streaming over HTTP)已啟動，以在Dynamic Media視訊傳遞中進行自我調整位元速率串流（已啟用CMAF [通用媒體應用程式格式]）。

* 最適化串流(DASH/HLS)可確保獲得更出色的視訊使用者觀看體驗。
* DASH是適用於最適化視訊串流的國際標準通訊協定，在業界被廣泛採用。
* 現已於亞太及北美推出；即將於歐洲 — 中東 — 非洲推出。

### [!DNL Forms]

* [無頭式最適化Forms](https://experienceleague.adobe.com/en/docs/experience-manager-headless-adaptive-forms/using/overview)可讓您的開發人員建立、發佈和管理可透過API （而非透過傳統的圖形使用者介面）存取及互動式表單。

* [最適化Forms核心元件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction#features)是一組24個開放原始碼、符合BEM規範的元件，建立在Adobe Experience Manager WCM核心元件的基礎上。 這些元件是開放原始碼，讓開發人員能夠輕鬆自訂和擴充這些元件，以符合其組織的特定需求。 擁有自訂[WCM核心元件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/get-started/authoring)的現有技能的任何人都可以輕鬆自訂這些元件並設定其樣式。

* OSGi上的Reader擴充功能現在提供個別選項，可啟用PDF的匯入和匯出使用許可權，以便在Adobe Acrobat Reader中匯入或匯出資料。
