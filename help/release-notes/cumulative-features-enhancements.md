---
title: Adobe Experience Manager 6.5版本中的累積主要功能和增強功能。
description: Adobe Experience Manager 6.5在前八個Service Pack發行版本中所做主要功能和增強功能的累計清單。
content-type: reference
docset: aem65
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 01fe5b53-2244-445f-a4d0-bd58ea38b611
solution: Experience Manager
source-git-commit: 54b508809733ed86798558aee50f8c7b5de00af9
workflow-type: tm+mt
source-wordcount: '2308'
ht-degree: 25%

---

# 累積的重要功能和增強功能

舊版八個Service Pack所累積的Adobe Experience Manager 6.5主要功能和增強功能清單。

另請參閱[Adobe Experience Manager 6.5最新Service Pack發行說明](/help/release-notes/release-notes.md)。

## AEM 6.5， Service Pack 18—2023年12月7日

* 啟用Sites頁面編輯器/影像元件使用者，以參照遠端Assets Cloud Service的資產。 (SITES-13448， SITES-13433)
* AEM現在支援伺服器端排序，以便在「清單」檢視中更快速地導覽專案。 專案節點會在出現在介面之前，根據使用者選取的欄排序。

### [!DNL Forms]

* **新最適化表單核心元件**：已新增垂直標籤、條款與條件以及核取方塊，以提升表單的擴充性。
   * **[核取方塊元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html)**：以核心元件為主的最適化表單現在可以包含核取方塊元件。可讓使用者二選一，選取或取消選取特定選項。它通常為一個小方塊，可以按一下或點選以在兩種狀態之間切換：選取和取消選取。核取方塊是一種常見的表單元素，用來表示選擇是/否或真/假。

   * **[條款與條件元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html)**：以核心元件為主的最適化表單現在可以包含條款與條件元件。它可讓Forms作者在表單中推出特定區段，向使用者提供與服務、產品或平台使用相關的條款、條件或法律協定。 此元件的設計用意是在告知使用者他們透過提交表單同意的規則、法規和義務。

     ![垂直標籤、條款與條件及核取方塊元件](/help/forms/using/assets/forms-components.png)

   * **[垂直標籤元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html)**：以核心元件為主的最適化表單現在可以將表單內容組織成垂直的標籤清單，提供結構化、可導覽的版面。在表單中使用垂直標籤可以簡化導覽和改進表單內容組織，進而提升使用者整體體驗，特別是在表單包含多個部分或複雜資訊時。

* **[64位元版本的AEM Forms Designer](/help/forms/using/installing-configuring-designer.md)**： 64位元版本的AEM Forms Designer提供增強的效能、擴充能力及記憶體管理，讓您能夠建立表單。 透過 64 位元架構，您可以輕鬆處理更大、更複雜的專案，確保設計工作流程流暢和最佳效率。透過這最先進的版本，提升您的表單設計能力並擁抱 AEM Forms Designer 的未來。

* **[連線最適化Forms與Microsoft® SharePoint清單](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)**： AEM Forms提供立即可用的整合，可直接將表單資料提交至SharePoint清單，讓您使用SharePoint的清單功能。 您可以將Microsoft® SharePoint清單設定為表單資料模型的資料來源，並使用使用表單資料模型提交動作來連線最適化表單與SharePoint清單。

* **[支援設定最適化表單片段的記錄檔案屬性](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)**：您現在可以在最適化表單編輯器中輕鬆自訂最適化表單片段及其欄位。

* **64位元XMLFM**： XMLFM的64位元反複專案提供更優異的效能、擴充能力，以及更精細的記憶體管理。 這是第一個在伺服器端部署的64位元原生服務。 XMLFM 64位元可利用其固有的功能，存取與32位元對應的記憶體資源相比更大的記憶體資源，因此能夠順暢處理更大的演算工作負載。 這個里程碑不僅代表效能的飛躍，也為AEM Forms伺服器內的原生服務架構引入重要增強功能。 此更新讓AEM Forms伺服器可順暢支援任何64位元原生服務。

## AEM 6.5， Service Pack 18—2023年8月24日

* Assets、Dynamic Media - [Dynamic Media中視訊的多重字幕與音軌支援](/help/assets/video.md#about-msma) — 您現在可以輕鬆地將多重字幕與多重音軌新增到主要視訊。 此功能表示全球觀眾都可以存取您的影片。您可以以多種語言向全球客群自訂單一已發佈的主要影片，並遵守不同地理區域的輔助功能指南。作者還可以從使用者介面中的單個標籤管理字幕和音訊。
* Assets — 您現在可以從搜尋結果導覽至包含資產的檔案夾位置，讓您執行各種資產管理任務。
* 內容片段中的Sites Polaris選取器已改善效能。
* 啟用Sites頁面編輯器/影像元件使用者，以參照遠端Assets Cloud Service的資產。
* 為了在清單檢視中快速尋找您可能有許多專案的專案，Adobe現在支援伺服器端排序。 專案節點會在使用者介面中呈現之前，根據使用者選取的欄在後端排序。
* AEM 6.5.18.0支援MongoDB 5.0至6.0。

### [!DNL Forms]

* **[規則編輯器中使用自訂錯誤處理常式的增強錯誤處理](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms.html)** — 您現在可以叫用自訂函式（使用使用者端程式庫）來回應外部服務傳回的錯誤。 此外，您也可以為使用者提供量身打造的回應。 或者，您可以針對服務傳回的錯誤採取特定動作。例如，您可以在後端叫用自訂工作流程來取得特定錯誤代碼，或通知客戶服務已停止服務

* **[增強型Adobe Sign工作流程步驟](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/aem-forms-workflow-step-reference.html#sign-document-step)** - AEM工作流程中的Adobe Sign工作流程步驟提供下列增強功能。

   * **Adobe Sign的政府ID型驗證強化安全性** - Adobe Acrobat Sign的政府ID型驗證提供額外的驗證層。 它可讓使用者使用政府頒發的ID （駕照、國民身分證、護照）來驗證身分。 此增強功能利用受信任的身分識別文件為簽名過程額外增加一層可信度，使其成為需要增強安全性、合規性和使用者驗證等情境的理想選擇。

   * **增強Adobe Sign檔案稽核軌跡的透明度** — 使用「稽核軌跡」功能，深入瞭解Adobe Sign檔案的生命週期。 透過稽核軌跡，您現在可以保留與文件相關的所有動作和互動的全面記錄。其中包括查看、編輯或簽署文件等人員的詳細資訊，以及每個事件的時間戳記。此加強功能對於維持合規性、解決爭議和確保數位協議的完整性至關重要。


   * **將協定收件者的角色擴充至簽署者** - Adobe Acrobat Sign可讓您將協定收件者的角色擴充至簽署者之外，以便更符合其工作流程需求。 啟用後，協定中的每個收件者皆可個別設定其角色，預設為簽署者。


* **[JEE上的AEM Forms完整安裝程式](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms.html)** — 此Service Pack為JEE上的AEM Forms提供完整安裝程式，可支援多種新軟體組合，包括：
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
* **Dynamic Media _快照_**— 嘗試測試影像或Dynamic Media URL，以檢視不同影像修飾元的輸出，以及針對檔案大小（使用WebP和AVIF傳遞）、網路頻寬和裝置畫素比最佳化的智慧型影像處理。 請參閱 [Dynamic Media 快照](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html)。
* **使用Dynamic Media的DASH串流** — 針對Dynamic Media視訊傳送中的自我調整串流（已啟用CMAF）啟動新通訊協定（DASH — 透過HTTP的動態自我調整串流）。 現在可供所有區域使用。
* **整合Experience Manager Sites和內容片段與Assets新一代Dynamic Media** - Experience Manager Assets as a Cloud Service新一代Dynamic Media的使用者現在可以使用這些雲端託管的資產，透過Experience Manager Sites 6.5的內部部署或Managed Services執行個體進行製作和傳遞。

### [!DNL Forms]

* **[AEM 頁面編輯器中的最適化表單](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)**：您現在可以使用 AEM 頁面編輯器快速建立多個表單，並將這些表單新增至您的 Sites 頁面。此功能讓內容作者可使用最適化表單元件 (包括動態行為、驗證、資料整合、產生記錄文件和業務流程自動化) 的強大功能，在 Sites 頁面內建立順暢的資料擷取體驗。您可以：
   * 將表單元件拖放到 AEM Sites 編輯器或體驗片段中的最適化表單容器元件，即可建立最適化表單。
   * 使用 AEM Sites 編輯器中的最適化表單精靈，以便建立不屬於任何 Sites 頁面的表單，讓您能夠在多個頁面之間自由地重複使用這些表單。
   * 將多個表單新增到 Sites 頁面，簡化使用者體驗並提供更大的彈性。
* **[在Experience Manager Forms中支援reCAPTCHA Enterprise](/help/forms/using/captcha-adaptive-forms.md)**：除了現有的Experience Manager Forms reCAPTCHA v2支援之外，新增在Google中支援reCAPTCHA Enterprise，針對詐騙活動和垃圾郵件提供增強型保護。
* **[透過Experience Manager Forms支援適用於政府的Adobe Acrobat Sign](/help/forms/using/adobe-sign-integration-adaptive-forms.md)**： AEM Forms現在與適用於政府的Adobe Acrobat Sign整合（符合FedRAMP規範）。 此整合針對政府相關帳戶（政府部門和機構）提交的Adaptive Form，提供電子簽章的進階法規遵循與安全性。 藉由與政府適用之 Adobe Acrobat Sign 整合，在一些最重要的關鍵任務和敏感業務線，Adobe 的合作夥伴和政府客戶便可以在最適化表單使用電子簽名。這額外一層的安全性可確保所有電子簽名完全符合 FedRAMP 中等合規性，讓 Adobe 的政府客戶安心使用。
* **啟用Salesforce與Experience Manager Forms的整合以進行資料交換**：使用OAuth 2.0使用者端憑證流程設定Experience Manager Forms與Salesforce應用程式之間的整合。 此功能可啟用應用程式的安全且直接的驗證和授權，並允許無縫通訊，而不需要使用者介入。
* **最佳化及增強工作流程引擎的功能**：將工作流程執行個體數目減到最少，以提高工作流程引擎的效能。 除了`COMPLETED`和`RUNNING`狀態值之外，工作流程也支援三個新的狀態值： `ABORTED`、`SUSPENDED`和`FAILED`。

## AEM 6.5， Service Pack 16—2023年2月23日

新通訊協定DASH (Dynamic Adaptive Streaming over HTTP)已啟動，以在Dynamic Media視訊傳遞中進行自我調整位元速率串流（已啟用CMAF [通用媒體應用程式格式]）。

* 最適化串流(DASH/HLS)可確保獲得更出色的視訊使用者觀看體驗。
* DASH是適用於最適化視訊串流的國際標準通訊協定，在業界被廣泛採用。
* 現已於亞太及北美推出；即將於歐洲 — 中東 — 非洲推出。

### [!DNL Forms]

* [無頭式最適化Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html)可讓您的開發人員建立、發佈和管理可透過API （而非透過傳統的圖形使用者介面）存取及互動式表單。

* [最適化Forms核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features)是一組24個開放原始碼、符合BEM規範的元件，建立在Adobe Experience Manager WCM核心元件的基礎上。 這些元件是開放原始碼，讓開發人員能夠輕鬆自訂和擴充這些元件，以符合其組織的特定需求。 擁有自訂[WCM核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/authoring.html)的現有技能的任何人都可以輕鬆自訂這些元件並設定其樣式。

* OSGi上的Reader擴充功能現在提供個別選項，可啟用PDF的匯入和匯出使用許可權，以便在Adobe Acrobat Reader中匯入或匯出資料。

## AEM 6.5， Service Pack 15—2022年11月24日

### [!DNL Forms]

* AEM Forms Designer現在可在[西班牙語地區設定](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)中使用。
* 您現在可以使用[OAuth2驗證Microsoft® Office 365郵件伺服器通訊協定（SMTP和IMAP）](/help/forms/using/oauth2-support-for-mail-service.md)。
* 您可以將伺服器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#enabling-server-side-validation-br)屬性上的[Revalidate設定為true，以識別從伺服器端的記錄檔案排除的隱藏欄位。
* AEM Forms Designer需要32位元版的Visual C++ 2019可轉散發套件(x86)。

## AEM 6.5， Service Pack 14—2022年8月25日

僅限錯誤修正。

## AEM 6.5， Service Pack 13—2022年5月26日

* 在最適化表單中使用隱藏的驗證碼：只有在可疑活動的情況下，您現在才能使用隱藏的驗證碼來顯示驗證碼質詢。 如果未發現可疑活動，則不顯示驗證碼質詢。 它有助於評估人工表單完成情況而不需要核取方塊、減少自訂工作，並改善終端使用者體驗。

* 新增在REST端點的表單資料模型後處理器中擷取回應標題的支援。

* 現在，在產生調適型表單轉譯檔案時，產生的XLIFF檔案的相同文字順序與對應調適型表單中的元件順序相同。

* 將最適化表單當地語系化後，即使對基本語言的文字做了很小的變更，其他所有語言的完整翻譯也會消失。 已在[!DNL Experience Manager] 6.5.13.0中修正問題。

* Forms的協助工具改良：

   * 新增熒幕助讀程式的支援，可將表格的標題和內文辨識為連續和連線的實體。 它有助於熒幕助讀程式正確導覽表格。 (NPR-37139)
   * 新增熒幕助讀程式的支援，可在對話方塊開啟前停止導覽HTML工作區。

## AEM 6.5， Service Pack 12—2022年2月24日

* 在設定遠端DAM和Sites部署之間的連線後，遠端DAM上的資產可在Sites部署中使用。 您現在可以在遠端DAM資產或資料夾上執行更新、刪除、重新命名和移動操作。 這些更新會在Sites部署中自動提供，但會有一些延遲。
* 現在預設可以推送轉出即時副本來源至多個即時副本，無需Blueprint設定。
* 進行中非同步操作的狀態現在會顯示在使用者介面中，以防止使用者意外觸發相同路徑上的多個非同步操作。
* 為Analytics 2.0 API提供IMS型驗證支援。
* JSON選件型別體驗片段的API支援。
* 現在已針對IMS中的刪除選件（體驗片段API）提供選件請求。
* 內建存放庫(Apache Jackrabbit Oak)仍維持在1.22.9。
