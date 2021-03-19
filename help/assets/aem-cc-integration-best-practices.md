---
title: 與Adobe Creative Cloud最佳做法整合
description: 整合 [!DNL Adobe Experience Manager] with [!DNL Adobe Creative Cloud] 以簡化資產轉讓工作流程並達到高內容速度的最佳實務。
contentOwner: AG
role: 業務從業人員、管理員
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '3251'
ht-degree: 14%

---


# [!DNL Adobe Experience Manager] 和整 [!DNL Creative Cloud] 合最佳實務  {#aem-and-creative-cloud-integration-best-practices}

[!DNL Adobe Experience Manager Assets] 是數位資產管理(DAM)解決方案，可與整合， [!DNL Adobe Creative Cloud] 以協助DAM使用者與創意團隊合作，簡化內容建立程式中的協作。

[!DNL Adobe Creative Cloud] 為創意團隊提供解決方案與服務生態系統，以協助他們建立數位資產。它包括案頭和行動應用程式、雲端服務（例如具備案頭同步或網路體驗的儲存空間），以及市集（例如[!DNL Adobe Stock]）。

閱讀內容，瞭解根據您的使用案例，在案頭和企業級DAM之間選擇哪些整合，以及連接工作流程的相關最佳實務。

>[!NOTE]
>
>[!DNL Experience Manager] 至資 [!DNL Creative Cloud] 料夾共用已過時，本指南不再涵蓋。Adobe建議使用較新的功能，例如[Adobe資產連結](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)或[Experience Manager案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html)，讓創意使用者存取[!DNL Experience Manager]中管理的資產。

## 創意人員、行銷人員和DAM使用者的協作需求{#collaboration-needs-of-creatives-marketers-and-dam-users}

| 需求 | 使用案例 | 涉及的曲面 |
|---|---|---|
| 簡化案頭創意人員的體驗 | 簡化從DAM([!DNL Experience Manager Assets])存取資產的流程，讓創意專業人員或更廣泛的案頭使用者，在原生資產建立應用程式中工作。 他們需要簡單明瞭的方式來探索、使用（開啟）、編輯和儲存對[!DNL Experience Manager]所做的變更，以及上傳新檔案。 | Win或Mac案頭；[!DNL Creative Cloud]應用程式 |
| 從[!DNL Adobe Stock]提供高品質、現成可用的資產 | 行銷人員協助資產採購和發現，協助加快內容建立流程。 創意專業人員可直接從其創意工具中使用核准的資產。 | [!DNL Experience Manager Assets]; [!DNL Adobe Stock] 市場；中繼資料欄位 |
| 依組織分發及共用資產 | 內部部門／當地分支機構和外部合作夥伴、分銷商和代理商會使用母公司組織共用的已核准資產。 該組織希望安全無縫地共用已建立的資產，以便更廣泛地重複使用。 | 品牌入口網站、資產分享共用 |

## Adobe方案以支援協作需求{#adobe-offerings-to-support-the-collaboration-need}

| 相關人員的價值主張 | Adobe方案 | 涉及的曲面 |
|---|---|---|
| 創意使用者會從[!DNL Experience Manager]發現資產、開啟並使用資產、編輯和上傳對[!DNL Experience Manager]的變更，以及將新檔案上傳至[!DNL Experience Manager]，而不需離開[!DNL Creative Cloud]應用程式。 | [Adobe資產連結](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | [!DNL Adobe Photoshop]、 [!DNL Adobe Illustrator]和 [!DNL Adobe InDesign]。 |
| 商業使用者可簡化開啟和使用資產、編輯和上傳變更至[!DNL Experience Manager]，以及從案頭環境上傳新檔案至[!DNL Experience Manager]。 他們使用一般整合來開啟原生案頭應用程式中的任何資產類型，包括非Adobe類型。 | [Experience Manager案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | [!DNL Experience Manager] Win和Mac案頭版案頭應用程式 |
| 行銷人員和商業使用者可從[!DNL Experience Manager]內部發現、預覽、授權及儲存並管理[!DNL Adobe Stock]資產。 授權和儲存的資產提供選擇[!DNL Adobe Stock]中繼資料，以提升治理。 | [Experience Manager與Adobe Stock一體化](aem-assets-adobe-stock.md) | [!DNL Experience Manager] 網路介面 |

本文主要針對協作需求的前兩個方面。資產規模分配和採購作為一個使用案例被簡要提及。針對這些需求解決方案，請考慮Adobe品牌入口網站或資產共用公域。應根據具體要求審查[Experience Manager資產](/help/assets/manage-assets.md)的替代解決方案，如[品牌入口](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)、可以基於[資產共用](https://adobe-marketing-cloud.github.io/asset-share-commons/)元件、[連結共用](/help/assets/link-sharing.md)構建的解決方案。

![Creative CloudExperience Manager連接，決定要使用哪些功能](assets/creative-connections-aem.png)

### 用例和Adobe解決方案的映射{#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| 使用案例 | [!DNL Adobe Asset Link] | [!DNL Experience Manager] 桌面應用程式 | 備注／其他解決方案 |
|---|---|---|---|
| Discover —— 瀏覽DAM資料夾 | 是 | [!DNL Experience Manager] 網頁介面和案頭動作 |  |
| Discover —— 存取DAM系列 | 是 | [!DNL Experience Manager] 網頁介面和案頭動作 |  |
| Discover —— 從DAM搜尋資產 | 是 | [!DNL Experience Manager] 網頁介面和案頭動作 |  |
| 使用——開啟資產 | 是 | 是 | [從網頁介面或](manage-assets.md#previewing-assets) 從Finder開啟 |
| 使用——將DAM中的資產放入檔案 | 是——內嵌 | 是——連結或內嵌 | [!DNL Experience Manager] 案頭應用程式可讓您在本機檔案系統上，以檔案形式存取資產。原生應用程式中的這些連結會以本機路徑表示。 |
| 編輯——開啟以進行編輯 | 是——結帳動作 | 是——開啟操作（在網路共用中） | [登出預設](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html) 情況下，將資產儲存至使用者的Creative Cloud儲存帳戶(由Creative Cloud應用程式同步)。 |
| 編輯——在DAM外進行中的工作 | 是——同步至案頭的使用者Creative Cloud儲存帳戶中可用的資產。 | 是 |  |
| 編輯——上傳變更 | 是- [檢查操作](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)並帶有可選注釋 | 是 |  |
| 上傳——單一檔案 | 是——上傳目前的作用中檔案 | 是 | [透過網頁介面上傳](manage-assets.md#uploading-assets) |
| 上傳——多個檔案／階層式資料夾結構 | 否 | 是 | [透過網頁介面](manage-assets.md#uploading-assets) 或自訂指令碼或工具上傳。 |
| 其他——使用者和登入 | Creative Cloud使用者登入Creative Cloud案頭應用程式時，可辨識(SSO) | [!DNL Experience Manager] 用戶和認證 | 這兩個解決方案的使用者都會計入[!DNL Experience Manager]使用者配額。 |
| 其他——網路和訪問 | 需要從用戶的案頭訪問通過網路部署[!DNL Experience Manager] | 需要從用戶的案頭訪問通過網路部署[!DNL Experience Manager] | [!DNL Adobe Asset Link] 不共用網路代理環境。 |
| 其他——移轉大量資產 | 否 | 否 | [資產移轉指南](assets-migration-guide.md) |

為支援資產散發使用案例，應考慮其他解決方案：

* [品牌](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 組合，提供可設定、SaaS附加元件， [!DNL Experience Manager Assets] 以發佈資產。
* 自訂解決方案是根據[資產共用共用共用](https://adobe-marketing-cloud.github.io/asset-share-commons/)程式碼庫建立。
* [!DNL Experience Manager] [連結](/help/assets/link-sharing.md) 共用以使用連結臨機共用資產。
* [Experience Manager資產](/help/assets/manage-assets.md) 網路介面與外部使用者介面，可 [!DNL Experience Manager] 透過存取控制設定和必要的IT/網路組態調整，讓這些外部使用者存取 [!DNL Experience Manager]。

## 主要概念和使用案例{#key-concepts-and-use-cases}

### 常用術語辭彙表{#glossary-of-common-terms}

* **在製品或創意在製品 (WIP)：**&#x200B;在資產生命週期中，資產會經歷多次變更，且通常尚未準備好更廣泛地與其他團隊共用的階段。
* **創意就緒資產：** [!DNL Assets] 可與更廣大的團隊共用，或已經由創意團隊選定或核准，以便與行銷或LOB團隊共用。
* **資產核准：**&#x200B;針對已上傳至 DAM 的資產執行的核准程序，通常包括品牌核准、法律核准等。
* **最終資產：**&#x200B;已完成所有核准/中繼資料標記，且已準備好更廣泛地供團隊使用的資產。此類資產會儲存在 DAM 中，並提供給所有 (或所有相關的) 使用者使用。這類資產可用於行銷管道，或供創意團隊創作設計。
* **小幅度資產更新/變更：**&#x200B;數位資產的快速微幅變更。此類更新/變更通常是為了因應潤飾或微幅編輯請求、資產檢閱或核准 (例如重新定位、變更文字大小、調整飽和度/亮度、顏色等) 而進行的。
* **重大資產更新/變更：**&#x200B;需要大量工作，且有時需要較長時間才能完成的數位資產變更。其中通常包含多項變更。資產在更新時必須儲存多次。重大資產更新通常會導致資產進入 WIP 階段。
* **DAM：**&#x200B;數位資產管理。在本文檔中，它與[!DNL Experience Manager Assets]同義，除非另有特別提及。
* **創意使用者：**&#x200B;使用 Creative Cloud 應用程式和服務建立數位資產的創意專業人員。在某些情況下，創意使用者可能是可使用 Creative Cloud、但不會建立數位資產的創意團隊成員 (例如創意總監或創意團隊經理)。
* **DAM 使用者：** DAM 系統的一般使用者。視組織而異，DAM 使用者可能是行銷或非行銷使用者，例如企業營運 (LOB) 使用者、圖書管理員、銷售人員等。

### 使用[!DNL Experience Manager]和[!DNL Creative Cloud]整合{#considerations-when-using-aem-and-creative-cloud-integration}時的考量事項

* 請參閱[案頭應用程式最佳實務](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html?lang=en#best-practices-to-prevent-troubles)
* 請參閱[Adobe Stock整合](aem-assets-adobe-stock.md)
* 請參閱[Adobe資產連結](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)

這是[!DNL Experience Manager]和[!DNL Creative Cloud]整合最佳實務的簡要摘要。 閱讀本檔案的其餘部分，以詳細瞭解這些內容。

* **對於在Photoshop、InDesign或Illustrator工作的創意使用者：** Adobe資產連結可提供最佳的使用者體驗，包括清理從中取出之資產的在製品處理 [!DNL Experience Manager]。
* **為簡化從案頭存取任何一般檔案格式或應用程式的資產：使** 用桌 [!DNL Experience Manager] 面應用程式。
* **瞭解將資產儲存在DAM的原因和時機：** 更新將提供給組織中的更廣大團隊。
* **** 請留意共用資產的數量：如果您的使用案例是資產分發，則治理和安全性可能是最重要的方面。請考慮使用大型工具 (例如品牌入口網站) 進行此作業。
* **** 瞭解資產生命週期：瞭解不同團隊在組織中如何處理資產
* **** 謹慎處理資產的頻繁儲存：Adobe Asset Link會透過PS、AI、ID為您處理。對於其他應用程式，請勿在映射/共用資料夾中執行進行中的工作，除非您需要DAM中的所有變更

### 從[!DNL Assets] {#access-to-adobe-stock-assets-from-aem-assets}存取[!DNL Adobe Stock]資產

[Experience Manager與Adobe Stock](/help/assets/aem-assets-adobe-stock.md) 的整 [!DNL Experience Manager] 合讓使用者能夠搜尋、預覽、授權並儲存資產，並將資產 [!DNL Adobe Stock] 放入 [!DNL Experience Manager]。已授權和儲存的[!DNL Stock]資產已選取[!DNL Stock]中繼資料，可用來使用額外的篩選條件來搜尋。

有關此整合的幾點重要：

* 當Adobe庫中的資產儲存至[!DNL Experience Manager]時，它們會變成一般[!DNL Assets]，並將二進位檔儲存至[!DNL Experience Manager]儲存庫。 與[!DNL Adobe Stock]相關的某些中繼資料會儲存在[!DNL Experience Manager]中，否則擷取程式會與任何其他檔案的相同。 例如，如果「智慧型標籤」是作用中，則在儲存時會將標籤新增至這些資產。
* 儲存至[!DNL Experience Manager]的資產是副本，而不是回到[!DNL Adobe Stock]的連結。

**使用儲存自中的 [!DNL Adobe Stock] 資 [!DNL Experience Manager] 產[!DNL Creative Cloud]**。此整合與[!DNL Adobe Asset Link]無關，但[!DNL Adobe Asset Link]會以這種方式識別從[!DNL Stock]儲存的這些資產，並在[!DNL Photoshop]、[!DNL Illustrator]或[!DNL InDesign]的[!DNL Adobe Asset Link]擴充功能UI中，在這些資產上顯示額外的中繼資料和[!DNL Adobe Stock]標誌。 這些檔案可供瀏覽、開啟等——因為它們是儲存至[!DNL Experience Manager]時的一般資產。
在副檔名為[!DNL Adobe Asset Link]的[!DNL Creative Cloud]應用程式中工作的創意使用者除了可存取已授權的資產（從[!DNL Adobe Stock]移至[!DNL Experience Manager]）外，還可使用「[!DNL Creative Cloud]資料庫」面板來搜尋、預覽及授權[!DNL Adobe Stock]資產。
[!DNL Assets] 從授 [!DNL Adobe Stock] 權並儲存至 [!DNL Experience Manager] 更廣大的團隊可存取部署，而 [!DNL Experience Manager Assets] 透過「資料庫」面板授權資產的創意人 [!DNL Adobe Stock] 員則會依預設在其帳戶中提供 [!DNL Creative Cloud]  [!DNL Creative Cloud] 資產。

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## 關於在DAM {#about-storing-assets-in-a-dam}中儲存資產

為了在創意和行銷／業務線(LOB)團隊之間設計有效率的工作流程並選擇最佳支援功能，請務必瞭解資產儲存在DAM的時機和原因。

### 資產為何儲存在DAM {#why-assets-are-stored-in-dam}

將資產儲存在DAM中，讓資產更容易存取，而且可尋找。 它可確保整個組織或生態系統中的眾多使用者（包括合作夥伴、客戶等）都能運用這些資產。

大多陣列織選擇僅儲存與下遊行銷/LOB流程相關的資產(通過[!DNL Experience Manager Sites]發佈到Web通道或Adobe Experience Cloud提供的其他通道-Marketing Cloud、Advertising Cloud和Analytics Cloud衡量、向用戶／合作夥伴提供等)。 此外，組織會儲存在DAM中可能須經過審查／核准程式的資產。 如此，DAM會儲存大部分有高可能被利用的資產，並避免儲存閒置資產。

儲存資產也須受技術與資源使用考量。 DAM針對儲存的資產提供其他服務，包括擷取中繼資料、版本修訂、產生預覽／轉碼、管理參照以及新增存取控制資訊。 這些服務需要額外的時間和基礎架構資源。

通常，儲存所有資產和更新是不可取的。 例如，如果特定資產的更新品質不佳，且會耗用過多的資源，則資產可能無法儲存在DAM中。

#### 資產儲存在DAM {#when-assets-are-stored-in-dam}時

創意團隊（和組織）通常對在資產生命週期的每個階段儲存資產不感興趣。 例如，在下列情況下，他們會避免儲存資產：

* 尚未完成或有待試驗的資產。
* 無法通過創意／內部團隊審閱週期的資產。
* 與相關資產相比，團隊有更好的人選向外部團隊代表其工作。

通常，下列類別資產會儲存在DAM中：

* 已到達特定到期日且被視為可共用的資產。
* 創意團隊預先選取的資產。
* 根據特定合約或合約（例如從RAW檔案轉換的JPG檔案、從PSD原稿轉換的TIFF/影像），行銷部門可使用或要求的特定資產格式。

#### 資產更新儲存在DAM {#when-updates-to-assets-are-stored-in-dam}時

通常，只應將與更廣泛的DAM使用者集合相關的資產更新儲存在DAM中。 它可確保使用者（行銷和類似功能）在DAM資產時間軸中只看到相關版本。

通常與資產生命週期中的重要里程碑相關的變更。 例如，創意團隊根據要求／審查提供的初始行銷就緒資產或正式更新應儲存在DAM中，並加以版本控制。

在DAM中要求變更現有資產後，行銷團隊會更新以供其審核，這是相關更新的範例。 它應儲存並更新至DAM的版本，以供進一步參考或還原為舊版。

以下是通常不相關的更新範例：

* 資產上傳的早期版本，在準備好進行行銷審核之前
* 在創作和行銷團隊決定資產已準備就緒之前，在進行中工作階段中經常對資產進行創意變更

### 使用者存取DAM {#user-access-to-dam}

[!DNL Assets] 根據用戶對部署的訪問支援兩種類 [!DNL Assets] 型。通常，企業網路（防火牆）內的使用者可直接存取DAM。 企業網路以外的其他使用者將無法直接存取。 使用者類型會決定從技術角度可使用哪些整合。

#### 直接存取DAM的創意使用者{#creative-users-with-direct-access-to-dam}

通常，內部創意團隊或內部網路的廣告公司／創意專業人員都可存取DAM部署，包括[!DNL Experience Manager]登入。 [!DNL Experience Manager] 網路基礎設施可以設定為允許直接訪問外部方——通常是受信任的組織，如為客戶工作的機構——可以通過網路訪問， [!DNL Experience Manager] 例如通過VPN或IP允許清單。

在這種情況下，Adobe資產連結或[!DNL Experience Manager]案頭應用程式可協助您輕鬆存取最終／核准的資產，並讓您將創意就緒資產儲存至DAM。

#### 無法存取DAM的創意使用者{#creative-users-without-access-to-dam}

無法直接存取DAM部署的外部機構和自由工作者可能需要存取已核准的資產，或想要將其新設計新增至DAM。

使用下列策略來存取最終／核准的資產：

* 如果「資產連結」無法運作，請使用案頭應用程式。
* 使用[Experience Manager資產品牌入口網站](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)將資產安全地發佈給外部合作夥伴
* 使用基於[資產共用共用公域](https://adobe-marketing-cloud.github.io/asset-share-commons/)的分發與採購入口網站的自訂實作
* 使用[!DNL Experience Manager]中設定的訪問控制和必要的網路基礎架構（例如，VPN和IP允許清單），使外部方可以訪問DAM中的專用內容區域。 他們可使用[!DNL Experience Manager]網頁UI來取得資產並將新內容上傳至DAM。

#### 正在從[!DNL Experience Manager] {#work-in-progress-on-assets-from-aem}處理資產

如本檔案所述，建議您對資產進行重大更新，有時稱為「進行中的工作」，而不會將儲存至本機檔案的所有編輯內容也上傳至[!DNL Experience Manager]做變更。 如此可加速案頭使用者的工作、限制網路頻寬的使用，並讓資產時間軸保持簡潔，並集中在受控的重大更新上。

Adobe資產連結提供此使用案例的良好支援：

* 當[!DNL Photoshop]、[!DNL InDesign]或[!DNL Illustrator]的使用者想要編輯檔案時，他們會對指定資產執行「取出」操作
* 資產會在背景下載、放入透過Creative Cloud案頭應用程式同步至磁碟的使用者Creative Cloud帳戶中，並且會在資產的[!DNL Experience Manager]中切換取出標幟，將編輯衝突降至最低
* 從此，使用者會在儲存在同步位置本機的檔案中工作，而且可以繼續工作並儲存必要的變更，以任何頻率需要
* 此外，由於資產位於Creative Cloud帳戶中，因此也可在使用者可能擁有的其他裝置上使用(例如，可在專用的Creative Cloud行動應用程式中開啟或編輯)，並可與其他Creative Cloud使用者共用以進行協作。
* 當創意使用者完成變更後，他們可以在其Creative Cloud應用程式中對該檔案執行「登入」操作，並加上選用的註解。 [!DNL Experience Manager]中的對應資產版本化，並更新為新二進位檔。 [!DNL Experience Manager] 像行銷人員或LOB使用者這樣的使用者可透過資產時間表UI存取重大資產變 [!DNL Experience Manager] 更或里程碑。

[!DNL Experience Manager] 案頭應用程式為在原生應用程式中開啟的資產提供網路共用。依預設，在短暫的時間後，所有在本機完成的變更都會自動上傳至[!DNL Experience Manager]。 有了這種配置，在進行中階段頻繁保存的內容將全部上傳到[!DNL Experience Manager]並版本化，從而帶來許多網路流量和潛在的可擴充性挑戰——更不用說[!DNL Experience Manager]中的不必要版本了。

這裡建議的方法是使用[!DNL Experience Manager]案頭應用程式中的選項來關閉自動更新，並手動將資產的變更上傳至[!DNL Experience Manager]，以運用應用程式的「資產狀態」UI中的上傳變更動作。

#### 批量上傳至DAM {#bulk-upload-to-dam}

在某些情況下，您可能需要同時將大量檔案上傳至DAM，例如：

* 上傳像片或大型專案的結果
* 上傳創意廣告公司提供的資產
* 如果在DAM外完成選取，則從較大的集合上傳選取的資產

此說明是指將檔案上傳為案頭使用者工作流程的一般部分（例如，每週或每張像片）。 此處未涵蓋大型資產遷移。

您可以運用下列上傳功能：

* 若要大量上傳大型／階層式資料夾，請使用提供[資料夾上傳](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en#upload-and-add-new-assets-to-aem)功能的[!DNL Experience Manager]案頭應用程式。 您也可以上傳階層式資料夾結構。 [!DNL Assets] 會在背景上傳，因此不會系結至網頁瀏覽器工作階段
* 若要從單一資料夾上傳幾個檔案，請直接將檔案拖曳至Web介面，或使用[!DNL Assets] Web介面中的「建立」選項。
* 您也可以根據您的業務需求使用自訂的上載程式。

#### 直接從案頭管理數位資產{#managing-digital-assets-directly-from-desktop}

如果您使用「網路檔案分享」來管理數位資產，則僅使用[!DNL Experience Manager]案頭應用程式所映射的網路分享，就可視為方便的替代。 從網路檔案共用轉換時，[!DNL Experience Manager]網頁介面提供一套豐富的數位資產管理功能，遠超網路共用的功能（搜尋、系列、中繼資料、協作、預覽等），而[!DNL Experience Manager]案頭應用程式則提供方便的連結，將伺服器端DAM存放庫與桌上型電腦的工作連結。

請避免使用[!DNL Experience Manager]案頭應用程式直接在[!DNL Assets]的網路共用中管理資產。 例如，請避免使用[!DNL Experience Manager]案頭應用程式來移動／複製多個檔案。 請改用[!DNL Assets]介面，將資料夾從Finder/Explorer拖曳至網路共用，或使用[!DNL Assets]資料夾上傳功能。

#### 資產遷移{#asset-migration}

要規劃並執行資產從現有系統遷移到新系統或遷移儲存在伺服器上的大量資產，請參閱[遷移指南](/help/assets/assets-migration-guide.md)。 [!DNL Experience Manager] 案頭應用程 [!DNL Experience Manager] 式和 [!DNL Creative Cloud] 整合不支援此類移轉。由於需要吸收的資產數量龐大，以及對元資料映射、轉換和提取的額外要求，因此應使用不同的工具和方法來處理遷移。

>[!MORELIKETHIS]
>
>* [Adobe資產連結](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [Experience Manager案頭應用程式最佳範例](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [Experience Manager品牌入口網站](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [Experience Manager與Adobe Stock一體化](aem-assets-adobe-stock.md)

