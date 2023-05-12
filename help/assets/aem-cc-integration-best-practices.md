---
title: 與Adobe Creative Cloud最佳實務整合
description: 整合的最佳實務 [!DNL Adobe Experience Manager] with [!DNL Adobe Creative Cloud] 簡化資產轉移工作流程並實現高內容速度。
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: Collaboration,Adobe Asset Link,Desktop App
exl-id: c7d589a3-1c5f-4ff0-879e-15e1c556f6dc
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '3268'
ht-degree: 14%

---

# [!DNL Adobe Experience Manager] 和 [!DNL Creative Cloud] 整合最佳實務 {#aem-and-creative-cloud-integration-best-practices}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/aem-cc-integration-best-practices.html?lang=en) |
| AEM 6.5 | 本文 |

[!DNL Adobe Experience Manager Assets] 是數位資產管理(DAM)解決方案，可與 [!DNL Adobe Creative Cloud] 協助DAM使用者與創意團隊合作，簡化內容建立程式中的共同作業。

[!DNL Adobe Creative Cloud] 為創意團隊提供解決方案和服務生態系統，協助他們建立數位資產。 它包括案頭和移動應用程式、雲端服務（如具有案頭同步或網路體驗的儲存），以及市場(如 [!DNL Adobe Stock].

請閱讀以了解根據您的使用案例在案頭和企業級DAM之間挑選哪些整合，以及連線工作流程的相關最佳實務。

>[!NOTE]
>
>[!DNL Experience Manager] to [!DNL Creative Cloud] 資料夾共用已遭取代，本指南不再涵蓋。 Adobe建議使用較新的功能，例如 [Adobe資產連結](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html) 或 [Experience Manager案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html) 為創意使用者提供中管理的資產的存取權 [!DNL Experience Manager].

## 創意人員、行銷人員和DAM使用者的共同作業需求 {#collaboration-needs-of-creatives-marketers-and-dam-users}

| 要求 | 使用案例 | 相關曲面 |
|---|---|---|
| 簡化案頭創意人員的體驗 | 簡化從DAM存取資產([!DNL Experience Manager Assets])，適用於創意專業人員，更廣泛而言，適用於案頭使用者，使用原生資產建立應用程式。 他們需要簡單明瞭的方式來探索、使用（開啟）、編輯和儲存變更，以 [!DNL Experience Manager]，以及上傳新檔案。 | Win或Mac案頭； [!DNL Creative Cloud] app |
| 提供高品質、現成可用的資產，來自 [!DNL Adobe Stock] | 行銷人員可協助進行資產來源搜尋和探索，協助加速內容建立流程。 創意專業人員可直接在其創意工具中使用已核准的資產。 | [!DNL Experience Manager Assets]; [!DNL Adobe Stock] 市場；中繼資料欄位 |
| 按組織分發和共用資產 | 內部部門/當地分支機構和外部合作夥伴、分銷商和代理使用母公司共用的已核准資產。 該組織希望安全無縫地共用已建立的資產，以便更廣泛地重複使用。 | Brand Portal, Asset Share Commons |

## Adobe產品以支援協作需求 {#adobe-offerings-to-support-the-collaboration-need}

| 相關角色的價值主張 | Adobe產品 | 相關曲面 |
|---|---|---|
| 創意使用者可從 [!DNL Experience Manager]，開啟並使用這些變更，編輯和上傳變更 [!DNL Experience Manager]，以及將新檔案上傳至 [!DNL Experience Manager]，不離開 [!DNL Creative Cloud] 應用程式。 | [Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html) | [!DNL Adobe Photoshop]、[!DNL Adobe Illustrator] 和 [!DNL Adobe InDesign]。 |
| 業務使用者可簡化開啟和使用資產、編輯和上傳變更至 [!DNL Experience Manager]，以及將新檔案上傳至 [!DNL Experience Manager] 從案頭環境。 他們會使用一般整合來開啟原生案頭應用程式中的任何資產類型，包括非Adobe的資產類型。 | [Experience Manager案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | [!DNL Experience Manager] Win和Mac案頭應用程式 |
| 行銷人員和商務使用者可探索、預覽、授權及儲存，並管理 [!DNL Adobe Stock] 資產內 [!DNL Experience Manager]. 授權和儲存的資產提供精選 [!DNL Adobe Stock] 元資料，以改善控管。 | [Experience Manager與Adobe Stock整合](aem-assets-adobe-stock.md) | [!DNL Experience Manager] 網頁介面 |

本文主要針對協作需求的前兩個方面。資產規模分配和採購作為一個使用案例被簡要提及。針對這些需求解決方案，請考慮Adobe品牌入口網站或資產共用公域。替代解決方案，例如 [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)，可根據 [資產共用公域](https://adobe-marketing-cloud.github.io/asset-share-commons/) 元件， [連結共用](/help/assets/link-sharing.md)，使用 [Experience Manager Assets](/help/assets/manage-assets.md) 應根據具體要求審查。

![Creative CloudExperience Manager連線，決定要使用的功能](assets/creative-connections-aem.png)

### 對應使用案例和Adobe解決方案 {#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| 使用案例 | [!DNL Adobe Asset Link] | [!DNL Experience Manager] 桌面應用程式 | 備注/其他解決方案 |
|---|---|---|---|
| Discover — 瀏覽DAM資料夾 | 是 | [!DNL Experience Manager] 網頁介面和案頭動作 |  |
| Discover — 存取DAM集合 | 是 | [!DNL Experience Manager] 網頁介面和案頭動作 |  |
| Discover — 從DAM搜尋資產 | 是 | [!DNL Experience Manager] 網頁介面和案頭動作 |  |
| 使用 — 開啟資產 | 是 | 是 | [從Web介面開啟](manage-assets.md#previewing-assets) 或從Finder |
| 使用 — 將資產從DAM放入檔案中 | 是 — 內嵌 | 是 — 連結或內嵌 | [!DNL Experience Manager] 案頭應用程式可在本機檔案系統上以檔案形式存取資產。 原生應用程式中的這些連結會以本機路徑表示。 |
| 編輯 — 開啟以進行編輯 | 是 — 結帳動作 | 是 — 開啟操作（在網路共用中） | [AAL結帳](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 依預設，會將資產儲存至使用者的creative cloud儲存空間帳戶(由Creative Cloud應用程式同步)。 |
| 編輯 — 在DAM外進行中的工作 | 是 — 使用者Creative Cloud儲存帳戶中可用的資產已同步至案頭。 | 是 |  |
| 編輯 — 上傳變更 | 是 —  [簽入操作](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 使用可選注釋 | 是 |  |
| 上傳 — 單一檔案 | 是 — 上載當前活動文檔 | 是 | [透過網頁介面上傳](manage-assets.md#uploading-assets) |
| 上傳 — 多個檔案/階層式資料夾結構 | 否 | 是 | [透過網頁介面上傳](manage-assets.md#uploading-assets) 或透過自訂指令碼或工具。 |
| Misc — 用戶和登錄 | Creative Cloud使用者登入Creative Cloud案頭應用程式後即可辨識(SSO) | [!DNL Experience Manager] 使用者和憑證 | 這兩個解決方案的使用者都會計入 [!DNL Experience Manager] 用戶配額。 |
| 雜項 — 網路和接入 | 需要從用戶的案頭訪問 [!DNL Experience Manager] 網路部署 | 需要從用戶的案頭訪問 [!DNL Experience Manager] 網路部署 | [!DNL Adobe Asset Link] 不共用網路代理環境。 |
| Misc — 遷移大量資產 | 否 | 否 | [資產移轉指南](assets-migration-guide.md) |

為支援資產散布使用案例，應考慮其他解決方案：

* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 針對 [!DNL Experience Manager Assets] 發佈資產。
* 自訂解決方案是根據 [資產共用公域](https://adobe-marketing-cloud.github.io/asset-share-commons/) 代碼庫。
* [!DNL Experience Manager] [連結分享](/help/assets/link-sharing.md) 使用連結來臨機共用資產。
* [Experience Manager Assets網頁介面](/help/assets/manage-assets.md) 由外部各方擔保的區域 [!DNL Experience Manager] 訪問控制設定，並進行必要的IT/網路配置調整，使這些外部用戶能夠訪問 [!DNL Experience Manager].

## 重要概念和使用案例 {#key-concepts-and-use-cases}

### 常用術語表 {#glossary-of-common-terms}

* **在製品或創意在製品 (WIP)：**&#x200B;在資產生命週期中，資產會經歷多次變更，且通常尚未準備好更廣泛地與其他團隊共用的階段。
* **創意就緒資產：** [!DNL Assets] 已準備好與更廣泛的團隊共用，或已由創意團隊選取或核准，以便與行銷或LOB團隊共用。
* **資產核准：**&#x200B;針對已上傳至 DAM 的資產執行的核准程序，通常包括品牌核准、法律核准等。
* **最終資產：**&#x200B;已完成所有核准/中繼資料標記，且已準備好更廣泛地供團隊使用的資產。此類資產會儲存在 DAM 中，並提供給所有 (或所有相關的) 使用者使用。這類資產可用於行銷管道，或供創意團隊創作設計。
* **小幅度資產更新/變更：**&#x200B;數位資產的快速微幅變更。此類更新/變更通常是為了因應潤飾或微幅編輯請求、資產檢閱或核准 (例如重新定位、變更文字大小、調整飽和度/亮度、顏色等) 而進行的。
* **重大資產更新/變更：**&#x200B;需要大量工作，且有時需要較長時間才能完成的數位資產變更。其中通常包含多項變更。資產在更新時必須儲存多次。重大資產更新通常會導致資產進入 WIP 階段。
* **DAM：**&#x200B;數位資產管理。在本檔案中，它是 [!DNL Experience Manager Assets]，除非另有特別提及。
* **創意使用者：**&#x200B;使用 Creative Cloud 應用程式和服務建立數位資產的創意專業人員。在某些情況下，創意使用者可能是可使用 Creative Cloud、但不會建立數位資產的創意團隊成員 (例如創意總監或創意團隊經理)。
* **DAM 使用者：** DAM 系統的一般使用者。視組織而異，DAM 使用者可能是行銷或非行銷使用者，例如企業營運 (LOB) 使用者、圖書管理員、銷售人員等。

### 使用時的考量事項 [!DNL Experience Manager] 和 [!DNL Creative Cloud] 整合 {#considerations-when-using-aem-and-creative-cloud-integration}

* 請參閱 [案頭應用程式最佳作法](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html#best-practices-to-prevent-troubles)
* 請參閱 [Adobe Stock整合](aem-assets-adobe-stock.md)
* 請參閱 [Adobe資產連結](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)

以下是 [!DNL Experience Manager] 和 [!DNL Creative Cloud] 整合。 閱讀本檔案的其餘部分，以詳細了解這些內容。

* **對於在Photoshop、InDesign或Illustrator中工作的創意使用者：** Adobe資產連結提供最佳的使用者體驗，包括對結帳自的資產的進行中工作進行簡潔的處理 [!DNL Experience Manager].
* **為簡化從案頭存取任何一般檔案格式或應用程式的資產：** use [!DNL Experience Manager] 案頭應用程式。
* **了解在DAM中儲存資產的原因及時機：** 更新內容將提供給組織中更廣大的團隊。
* **** 請留意共用資產的數量：如果您的使用案例是資產分發，則治理和安全性可能是最重要的方面。請考慮使用大型工具 (例如品牌入口網站) 進行此作業。
* **** 瞭解資產生命週期：瞭解不同團隊在組織中如何處理資產
* **** 謹慎處理資產的頻繁儲存：Adobe Asset Link會透過PS、AI、ID為您處理。對於其他應用程式，請勿在映射/共用資料夾中執行進行中的工作，除非您需要DAM中的所有變更

### 存取 [!DNL Adobe Stock] 資產 [!DNL Assets] {#access-to-adobe-stock-assets-from-aem-assets}

[Experience Manager與Adobe Stock整合](/help/assets/aem-assets-adobe-stock.md) proves [!DNL Experience Manager] 能夠搜尋、預覽、授權和儲存的使用者 [!DNL Adobe Stock] into [!DNL Experience Manager]. 授權並儲存 [!DNL Stock] 已選取資產 [!DNL Stock] 中繼資料，可用來搜尋含有額外篩選器的項目。

此整合的幾項重要要點：

* Adobe庫存中的資產儲存至時 [!DNL Experience Manager]，它們會變成 [!DNL Assets]，將二進位儲存至 [!DNL Experience Manager] 存放庫。 與相關的一些中繼資料 [!DNL Adobe Stock] 會針對中的資產儲存 [!DNL Experience Manager]，否則擷取程式看起來與任何其他檔案相同。 例如，如果智慧標籤處於作用中狀態，則會在儲存時將標籤新增至這些資產。
* 資產已儲存至 [!DNL Experience Manager] 是復本，而非回傳的連結 [!DNL Adobe Stock].

**使用從儲存的資產 [!DNL Adobe Stock] into [!DNL Experience Manager] in[!DNL Creative Cloud]**. 此整合獨立於 [!DNL Adobe Asset Link]，但 [!DNL Adobe Asset Link] 會辨識 [!DNL Stock] 方式，並顯示其他中繼資料和 [!DNL Adobe Stock] 在 [!DNL Adobe Asset Link] 擴充功能UI(位於 [!DNL Photoshop], [!DNL Illustrator]，或 [!DNL InDesign]. 這些檔案可供瀏覽、開啟等使用，因為它們是儲存至時的一般資產 [!DNL Experience Manager].
在中工作的創意使用者 [!DNL Creative Cloud] 應用程式 [!DNL Adobe Asset Link] 擴充功能會顯示，此外也可從 [!DNL Adobe Stock] into [!DNL Experience Manager]，也可以使用 [!DNL Creative Cloud] 用於搜索、預覽和許可的庫面板 [!DNL Adobe Stock] 資產。
[!DNL Assets] 從 [!DNL Adobe Stock] 授權並儲存至 [!DNL Experience Manager] 讓更多的團隊 [!DNL Experience Manager Assets] 部署，而創作者會從 [!DNL Adobe Stock] via [!DNL Creative Cloud] 「程式庫」面板可讓這些程式庫在 [!DNL Creative Cloud] 帳戶。

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## 關於在DAM中儲存資產 {#about-storing-assets-in-a-dam}

若要在創意與行銷/業務線(LOB)團隊之間設計有效的工作流程，並選擇最佳支援功能，請務必了解資產儲存於DAM的時間和原因。

### 資產為何儲存在DAM中 {#why-assets-are-stored-in-dam}

將資產儲存在DAM中，可讓資產輕鬆存取且可尋找。 它可確保組織或生態系統中的眾多使用者都能運用這些資產，包括合作夥伴、客戶等。

大多陣列織選擇僅儲存與下遊行銷/LOB流程相關的資產（透過發佈至Web管道等管道） [!DNL Experience Manager Sites] 或Adobe Experience Cloud提供的其他管道 — Marketing Cloud、Advertising Cloud，以及Analytics Cloud測量，提供給使用者/合作夥伴等)。 此外，組織會儲存DAM中可能經過審核/核准程式的資產。 這樣，DAM就能儲存大多數具有高利用機會的資產，並避免儲存閒置的資產。

儲存資產還需考慮技術和資源利用。 DAM提供儲存資產的其他相關服務，包括擷取中繼資料、版本設定、產生預覽/轉碼、管理參考以及新增存取控制資訊。 這些服務需要額外的時間和基礎架構資源。

通常，儲存所有資產和更新是不理想的。 例如，如果特定資產的更新品質不佳，且耗用過多資源，則資產可能不會儲存在DAM中。

#### 資產儲存在DAM時 {#when-assets-are-stored-in-dam}

創意團隊（和組織）通常對在資產生命週期的每個階段儲存資產不感興趣。 例如，在下列情況下，他們會避免儲存資產：

* 尚未定稿或有待試驗的資產。
* 無法通過創意/內部團隊審核週期的資產。
* 與相關資產相比，團隊有更好的候選人來代表其工作給外部團隊。

通常，下列類別資產會儲存在DAM中：

* 已到期且被視為可供共用的資產。
* 創意團隊預先選取的資產。
* 根據特定合約或合約(例如從RAW檔案轉換的JPG檔案、TIFF/PSD原始影像)，行銷可使用或要求的特定資產格式。

#### 資產更新儲存於DAM時 {#when-updates-to-assets-are-stored-in-dam}

一般而言，DAM中只應儲存與較廣的DAM使用者集合相關的資產更新。 它可確保使用者（行銷和類似功能）只能在DAM資產時間軸中看到相關版本。

通常與資產生命週期中的主要里程碑相關的變更。 例如，創意團隊提供的初始行銷就緒資產或根據請求/檢閱的官方更新應儲存在DAM中，並加以版本控制。

創意團隊在請求變更DAM中現有資產後進行更新，供行銷團隊檢閱，這是相關更新的範例。 應將其儲存並在DAM中加以版本控制，以供進一步參考或還原為舊版。

以下是通常不相關的更新範例：

* 在資產可供行銷審核之前先上傳的舊版資產
* 在創意和行銷團隊決定資產已就緒之前，會在進行中階段經常對資產進行創意變更

### DAM的使用者存取權 {#user-access-to-dam}

[!DNL Assets] 根據使用者對 [!DNL Assets] 部署。 企業網路（防火牆）內的使用者通常可直接存取DAM。 企業網路以外的其他使用者將無法直接存取。 使用者類型會從技術觀點決定可使用的整合。

#### 可直接存取DAM的創意使用者 {#creative-users-with-direct-access-to-dam}

內部創意團隊或加入內部網路的代理商/創意專業人員通常都能存取DAM部署，包括 [!DNL Experience Manager] 登入。 [!DNL Experience Manager] 網路基礎設施的設定允許直接訪問外部方 — 通常是受信任的組織，如為客戶工作的機構 — 以訪問 [!DNL Experience Manager] 通過網路，例如通過VPN或IP允許清單。

在此情況下，Adobe資產連結或 [!DNL Experience Manager] 案頭應用程式可協助您輕鬆存取最終/核准的資產，並將創意資產儲存至DAM。

#### 無法存取DAM的創意使用者 {#creative-users-without-access-to-dam}

無法直接存取DAM部署的外部機構和自由工作者可能需要存取已核准的資產，或想要將其新設計新增至DAM。

使用下列策略來提供對最終/核准資產的存取權：

* 如果「資產連結」無法運作，請使用案頭應用程式。
* 使用 [Experience Manager AssetsBrand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 以安全方式向外部合作夥伴發佈資產
* 根據使用發佈和來源補充入口網站的自訂實作 [資產共用公域](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* 使用在 [!DNL Experience Manager] 和必要的網路基礎架構（例如VPN和IP允許清單），讓外部方能存取您DAM中的專用內容區域。 他們可以使用 [!DNL Experience Manager] Web UI，以取得資產並將新內容上傳至DAM。

#### 正在從 [!DNL Experience Manager] {#work-in-progress-on-assets-from-aem}

如本檔案所述，建議您對資產執行重大更新，有時稱為進行中的工作，而不要將所有已儲存至本機檔案的編輯內容也上傳至 [!DNL Experience Manager] 變更。 這可加快案頭用戶的工作速度、限制所使用的網路頻寬，並保持資產時間清晰，並將重點放在受控的重大更新上。

Adobe資產連結對此使用案例提供良好支援：

* 當 [!DNL Photoshop], [!DNL InDesign]，或 [!DNL Illustrator] 為了編輯檔案，他們會對指定資產執行「簽出」操作
* 資產會在背景下載，放入透過Creative Cloud案頭應用程式同步至磁碟的使用者Creative Cloud帳戶中，然後勾選結帳標幟即會切換 [!DNL Experience Manager] 在資產上，將編輯衝突最小化
* 之後，使用者會在同步位置儲存於本機的檔案中操作，並可以繼續操作並儲存必要的變更，以執行任何所需頻率
* 此外，由於資產位於Creative Cloud帳戶中，因此也可在使用者可能擁有的其他裝置上使用(例如，可以在專用的Creative Cloud行動應用程式中開啟或編輯)，並且可與其他Creative Cloud使用者共用以進行共同作業。
* 創意使用者完成變更後，即可在其Creative Cloud應用程式中對該檔案執行簽入操作，並附上選用備注。 中的對應資產 [!DNL Experience Manager] 已更新版本，並更新為使用新二進位檔。 [!DNL Experience Manager] 行銷人員或LOB使用者等使用者可透過 [!DNL Experience Manager] 資產時間軸UI。

[!DNL Experience Manager] 案頭應用程式為原生應用程式中開啟的資產提供網路共用。 依預設，在本機完成的所有變更都會上傳至 [!DNL Experience Manager] 會自動過一段時間。 有了這種配置，在進行中階段期間頻繁保存的所有內容都將上載到 [!DNL Experience Manager] 和版本化，會造成大量網路流量和潛在的可擴充性挑戰，更不用說 [!DNL Experience Manager].

此處的建議方法是使用 [!DNL Experience Manager] 案頭應用程式關閉自動更新，並將資產變更上傳至 [!DNL Experience Manager] 在應用程式的「資產狀態」UI中，以手動方式運用「上傳變更」動作。

#### 大量上傳至DAM {#bulk-upload-to-dam}

在某些情況下，您可能需要同時將大量檔案上傳至DAM，例如：

* 上傳像片或大型專案的結果
* 上傳由創意廣告公司提供的資產
* 如果選取是在DAM外完成，則從較大的集合上傳選取的資產

說明是指以正常的案頭使用者工作流程，在運作上（例如每週或每張像片）上傳檔案。 此處未涵蓋大型資產遷移。

您可善用下列上傳功能：

* 若要大量上傳大型/階層式資料夾，請使用 [!DNL Experience Manager] 提供案頭應用程式 [資料上傳](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem) 功能。 您也可以上傳階層式資料夾結構。 [!DNL Assets] 會在背景上傳，因此不會系結至網頁瀏覽器工作階段
* 若要從單一資料夾上傳幾個檔案，請直接將檔案拖曳至Web介面，或使用 [!DNL Assets] 網頁介面。
* 您也可以使用自訂上傳程式，視您的業務需求而定。

#### 直接從案頭管理數位資產 {#managing-digital-assets-directly-from-desktop}

如果您使用網路檔案共用來管理數位資產，只需使用 [!DNL Experience Manager] 案頭應用程式可視為方便的替代項目。 從網路檔案共用轉換時， [!DNL Experience Manager] 網頁介面提供豐富的數位資產管理功能，遠遠超出了網路共用（搜尋、集合、中繼資料、共同作業、預覽等）的可能範圍，以及 [!DNL Experience Manager] 案頭應用程式提供便利的連結，可將伺服器端的DAM存放庫與案頭上的工作連線。

避免使用 [!DNL Experience Manager] 案頭應用程式，直接在的網路共用中管理資產 [!DNL Assets]. 例如，請避免使用 [!DNL Experience Manager] 移動/複製多個檔案的案頭應用程式。 請改用 [!DNL Assets] 介面，將資料夾從Finder/Explorer拖動到網路共用或使用 [!DNL Assets] 資料夾上傳功能。

#### 資產移轉 {#asset-migration}

要規劃並執行從現有系統到新系統的資產遷移，或遷移儲存在伺服器上的大量資產，請參閱 [移轉指南](/help/assets/assets-migration-guide.md). [!DNL Experience Manager] 案頭應用程式和 [!DNL Experience Manager] to [!DNL Creative Cloud] 整合不支援這類移轉。 由於要內嵌的資產數量龐大，以及中繼資料對應、轉換和內嵌等其他需求，因此應使用不同的工具和方法來處理移轉。

>[!MORELIKETHIS]
>
>* [Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)
>* [Experience Manager案頭應用程式最佳實務](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [Experience ManagerBrand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [Experience Manager與Adobe Stock整合](aem-assets-adobe-stock.md)

