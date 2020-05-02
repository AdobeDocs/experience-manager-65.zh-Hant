---
title: Adobe Creative Cloud和[!DNL Adobe Experience Manager]整合最佳實務。
description: 將[!DNL Adobe Experience Manager]與[!DNL Adobe Creative Cloud]整合的最佳實務，以簡化資產轉讓工作流程並達到高內容速度。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 1321aa3421455d78fd4562d6cb524aa232ee2ce1

---


# [!DNL Adobe Experience Manager] 整合 [!DNL Creative Cloud] 最佳範例 {#aem-and-creative-cloud-integration-best-practices}

<!-- TBD: Reconcile with 6.4 article that's behind this article in terms of content streamlining and structuring.
-->

[!DNL Adobe Experience Manager Assets] 是數位資產管理(DAM)解決方案，可與 [!DNL Adobe Creative Cloud] DAM使用者整合，以協助DAM使用者與創意團隊合作，簡化內容建立程式中的協作。

[!DNL Adobe Creative Cloud] 為創意團隊提供解決方案與服務生態系統，以協助他們建立數位資產。 它包括案頭和行動應用程式、雲端服務（例如具備案頭同步功能或網頁體驗的儲存空間），以及市集(例如 [!DNL Adobe Stock])。

閱讀內容，瞭解根據您的使用案例，在案頭和企業級DAM之間選擇哪些整合，以及連接工作流程的相關最佳實務。

>[!NOTE]
>
>[!DNL Experience Manager] 不 [!DNL Creative Cloud] 再提倡資料夾共用，本指南不再涵蓋。 Adobe建議使用較新的功能(例如 [Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html) 或 [Experience Manager案頭應用程式)，讓創意使用者可存取管理中的資產](Https://docs.adobe.com/content/help/zh-Hant/experience-manager-desktop-app/using/introduction.html)[!DNL Experience Manager]。

## 創意人員、行銷人員和DAM使用者的協作需求 {#collaboration-needs-of-creatives-marketers-and-dam-users}

| 需求 | 使用案例 | 涉及的曲面 |
|---|---|---|
| 簡化案頭創意人員的體驗 | 簡化從DAM([!DNL Experience Manager Assets])存取資產的流程，以供創意專業人員使用，或更廣泛地，讓使用桌上型電腦的使用者在原生資產建立應用程式中工作。 他們需要簡單明瞭的方式來探索、使用（開啟）、編輯和儲存變更， [!DNL Experience Manager]以及上傳新檔案。 | Win或Mac案頭； [!DNL Creative Cloud] 應用程式 |
| 提供高品質、現成可用的資產， [!DNL Adobe Stock] | 行銷人員協助資產採購和發現，協助加快內容建立流程。 創意專業人員可直接從其創意工具中使用核准的資產。 | [!DNL Experience Manager Assets]; [!DNL Adobe Stock] 市場； 中繼資料欄位 |
| 依組織分發及共用資產 | 內部部門／當地分支機構和外部合作夥伴、分銷商和代理商會使用母公司組織共用的已核准資產。 該組織希望安全無縫地共用已建立的資產，以便更廣泛地重複使用。 | 品牌入口網站、資產分享共用 |

## Adobe提供的產品可支援協作需求 {#adobe-offerings-to-support-the-collaboration-need}

| 相關人員的價值主張 | Adobe產品 | 涉及的曲面 |
|---|---|---|
| 創意使用者可從中 [!DNL Experience Manager]發現資產、開啟並使用資產、編輯和上傳變更至 [!DNL Experience Manager]，以及將新檔案上傳至 [!DNL Experience Manager]，毋需離開應用 [!DNL Creative Cloud] 程式。 | [Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html) | Photoshop、Illustrator和InDesign |
| 商業使用者可簡化開啟和使用資產、編輯和上傳變更 [!DNL Experience Manager]至，以及從案頭環境 [!DNL Experience Manager] 上傳新檔案的程式。 他們會使用一般整合來開啟原生案頭應用程式中的任何資產類型，包括非Adobe的資產類型。 | [Experience Manager案頭應用程式](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html) | [!DNL Experience Manager] Win和Mac案頭版案頭應用程式 |
| 行銷人員和商業使用者可從內部探索、預覽、授權和儲 [!DNL Adobe Stock] 存及管理資產 [!DNL Experience Manager]。 授權和儲存的資產提供精選的中繼 [!DNL Adobe Stock] 資料，以提升治理。 | [Experience Manager與Adobe Stock整合](aem-assets-adobe-stock.md) | [!DNL Experience Manager] 網路介面 |

本文主要針對協作需求的前兩個方面。資產規模分配和採購作為一個使用案例被簡要提及。針對這些需求解決方案，請考慮Adobe品牌入口網站或資產共用公域。Alternate solutions such as [Brand Portal](https://helpx.adobe.com/tw/experience-manager/brand-portal/user-guide.html), solutions that can be built based on [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) components, [Link Share](/help/assets/link-sharing.md), using [Experience Manager Assets](/help/assets/managing-assets-touch-ui.md) should be reviewed based on specific requirement.

![適用於Experience Manager的Creative Cloud連線，決定要使用哪些功能](assets/creative-connections-aem.png)

### 使用案例與Adobe解決方案的對應 {#mapping-of-use-cases-and-adobe-solutions}

| 使用案例 | [!DNL Adobe Asset Link] | [!DNL Experience Manager] 案頭應用程式 | 備注／其他解決方案 |
|---|---|---|---|
| Discover —— 瀏覽DAM資料夾 | 是 | [!DNL Experience Manager] 網頁UI +案頭動作 | 瀏覽網路共用時，請關閉縮圖以避免下載資產的二進位檔案。 |
| Discover —— 存取DAM系列 | 是 | [!DNL Experience Manager] 網頁UI +案頭動作 |  |
| Discover —— 從DAM搜尋資產 | 是 | [!DNL Experience Manager] 網頁UI +案頭動作 |  |
| 使用——開啟資產 | 是 | 是——適用於任何應用程式 | [從Web介面或](managing-assets-touch-ui.md#previewing-assets) Finder開啟 |
| 使用——將DAM中的資產放入檔案 | 是——內嵌 | 是——連結或內嵌 | [!DNL Experience Manager] 案頭應用程式可讓您在本機檔案系統上，以檔案形式存取資產。 原生應用程式中的這些連結會以本機路徑表示。 |
| 編輯——開啟以進行編輯 | 是——結帳動作 | 是——開啟操作（在網路共用中） | [AAL的結帳功能](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html) ，預設會將資產儲存至使用者的Creative Cloud儲存帳戶（由Creative Cloud應用程式同步）。 |
| 編輯——在DAM外進行中的工作 | 是——同步至案頭的使用者Creative Cloud儲存空間帳戶中可用的資產。 | 是 |  |
| 編輯——上傳變更 | 是——使 [用可選注釋](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html) 簽入操作 | 是 |  |
| 上傳——單一檔案 | 是——上傳目前的作用中檔案 | 是 | [透過網頁介面上傳](managing-assets-touch-ui.md#uploading-assets) |
| 上傳——多個檔案／階層式資料夾結構 | 否 | 是 | [透過網頁介面上傳](managing-assets-touch-ui.md#uploading-assets)；自<br>訂指令碼或工具 |
| 其他——使用者和登入 | 已登入Creative Cloud案頭應用程式的Creative Cloud使用者可獲得辨識(SSO) | [!DNL Experience Manager] 用戶／登錄 | 這兩個解決方案的使用者都會根據使用者 [!DNL Experience Manager] 配額計算。 |
| 其他——網路和訪問 | 需要從用戶的案頭訪問，才能通過 [!DNL Experience Manager] 網路進行部署 | 需要從用戶的案頭訪問，才能通過 [!DNL Experience Manager] 網路進行部署 | Adobe Asset Link不會共用網路代理環境。 |
| 其他——移轉大量資產 | 否 | 否 | [遷移指南](assets-migration-guide.md) |

為支援資產散發使用案例，應考慮其他解決方案：

* [品牌入口](https://helpx.adobe.com/tw/experience-manager/brand-portal/user-guide.html) ，提供可設定、SaaS附加元件，以 [!DNL Experience Manager Assets] 發佈資產。
* 自訂解決方案是根據「資產共 [用共用共用](https://adobe-marketing-cloud.github.io/asset-share-commons/) 」程式碼庫建立。
* [!DNL Experience Manager] [連結共用](/help/assets/link-sharing.md) ，使用連結臨機共用資產。
* [Experience Manager Assets網路介面](/help/assets/managing-assets-touch-ui.md) ，可讓外部使用者存取控制設定 [!DNL Experience Manager] ，以及必要的IT/網路組態調整，為他們提供存取權 [!DNL Experience Manager]。

## 主要概念和使用案例 {#key-concepts-and-use-cases}

### 常見術語辭彙表 {#glossary-of-common-terms}

* **在製品或創意在製品 (WIP)：**&#x200B;在資產生命週期中，資產會經歷多次變更，且通常尚未準備好更廣泛地與其他團隊共用的階段。
* **創意就緒資產：** [!DNL Assets] 已準備好與更廣大的團隊分享，或已經由創意團隊選取／核准，以便與行銷或LOB團隊分享。
* **資產核准：**&#x200B;針對已上傳至 DAM 的資產執行的核准程序，通常包括品牌核准、法律核准等。
* **最終資產：**&#x200B;已完成所有核准/中繼資料標記，且已準備好更廣泛地供團隊使用的資產。此類資產會儲存在 DAM 中，並提供給所有 (或所有相關的) 使用者使用。這類資產可用於行銷管道，或供創意團隊創作設計。
* **小幅度資產更新/變更：**&#x200B;數位資產的快速微幅變更。此類更新/變更通常是為了因應潤飾或微幅編輯請求、資產檢閱或核准 (例如重新定位、變更文字大小、調整飽和度/亮度、顏色等) 而進行的。
* **重大資產更新/變更：**&#x200B;需要大量工作，且有時需要較長時間才能完成的數位資產變更。其中通常包含多項變更。資產在更新時必須儲存多次。重大資產更新通常會導致資產進入 WIP 階段。
* **DAM：**&#x200B;數位資產管理。In this document, it is synonymous with [!DNL Experience Manager Assets], unless specifically mentioned otherwise.
* **創意使用者：**&#x200B;使用 Creative Cloud 應用程式和服務建立數位資產的創意專業人員。在某些情況下，創意使用者可能是可使用 Creative Cloud、但不會建立數位資產的創意團隊成員 (例如創意總監或創意團隊經理)。
* **DAM 使用者：** DAM 系統的一般使用者。視組織而異，DAM 使用者可能是行銷或非行銷使用者，例如企業營運 (LOB) 使用者、圖書管理員、銷售人員等。

### 使用和整合時的 [!DNL Experience Manager] 考量事 [!DNL Creative Cloud] 項 {#considerations-when-using-aem-and-creative-cloud-integration}

* 檢視桌 [面應用程式最佳實務](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/troubleshoot.html#best-practices-to-prevent-troubles)
* 檢視 [Adobe Stock整合](aem-assets-adobe-stock.md)
* 請參 [閱Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)

這是最佳實務與整合的簡 [!DNL Experience Manager] 要摘 [!DNL Creative Cloud] 要。 閱讀本檔案的其餘部分，以詳細瞭解這些內容。

* **對於在Photoshop、InDesign或Illustrator中工作的創意使用者：** Adobe Asset Link提供最佳的使用者體驗，包括清楚處理從中取出之資產的「進行中工作」 [!DNL Experience Manager]。
* **為簡化從案頭存取任何一般檔案格式或應用程式的資產：** 使用桌 [!DNL Experience Manager] 面應用程式。
* **瞭解在DAM中儲存資產的原因及時機：** 更新將提供給組織中更廣大的團隊。
* **** 請留意共用資產的數量：如果您的使用案例是資產分發，則治理和安全性可能是最重要的方面。請考慮使用大型工具 (例如品牌入口網站) 進行此作業。
* **** 瞭解資產生命週期：瞭解不同團隊在組織中如何處理資產
* **** 謹慎處理資產的頻繁儲存：Adobe Asset Link會透過PS、AI、ID為您處理。對於其他應用程式，請勿在映射/共用資料夾中執行進行中的工作，除非您需要DAM中的所有變更

### 存取 [!DNL Adobe Stock] 資產 [!DNL Assets] {#access-to-adobe-stock-assets-from-aem-assets}

[Experience Manager與Adobe Stock整合](/help/assets/aem-assets-adobe-stock.md) ，讓 [!DNL Experience Manager] 使用者能夠搜尋、預覽、授權及儲存資產，並將資產 [!DNL Adobe Stock] 放入 [!DNL Experience Manager]。 授權和儲 [!DNL Stock] 存的資產已選 [!DNL Stock] 取中繼資料，可用來使用額外的篩選來搜尋。

有關此整合的幾點重要：

* 當Adobe Stock中的資產儲存至時， [!DNL Experience Manager]它們會變成一般的 [!DNL Assets]資產，並將二進位檔儲存至儲存 [!DNL Experience Manager] 庫。 某些與相關的中繼資 [!DNL Adobe Stock] 料會儲存在中的資產中， [!DNL Experience Manager]否則擷取程式看起來會與任何其他檔案的相同。 例如，如果「智慧型標籤」是作用中，則在儲存時會將標籤新增至這些資產。
* 儲存至的資產 [!DNL Experience Manager] 是復本，而非回到的連結 [!DNL Adobe Stock]。

**使用儲存自中的[!DNL Adobe Stock]資[!DNL Experience Manager]產[!DNL Creative Cloud]**。 此整合不受[!DNL Adobe Asset Link]影響，但[!DNL Adobe Asset Link]可識別以這種方式儲存的資產，並在延伸UI中、[!DNL Stock][!DNL Stock]、或Extension UI中，在這些資產上顯示其他中繼資料和圖[!DNL Adobe Asset Link][!DNL Photoshop][!DNL Illustrator][!DNL InDesign]示。 這些檔案可供瀏覽、開啟等——因為它們是儲存至時的一般資產[!DNL Experience Manager]。
使用擴充功能[!DNL Creative Cloud]應用程式的創意使[!DNL Adobe Asset Link]用者除了可從中存取已授權的資產外[!DNL Adobe Stock]，還可使用「資料庫」面板來搜尋、預覽和授權[!DNL Experience Manager][!DNL Creative Cloud][!DNL Adobe Stock]資產。[!DNL Assets]從授[!DNL Adobe Stock]權並儲存為可[!DNL Experience Manager]存取部署的更廣大團隊都可使用，而透過「資料庫」面板授權資產的創[!DNL Experience Manager Assets]意人士則會依預設，在其帳戶中僅提供自[!DNL Adobe Stock][!DNL Creative Cloud][!DNL Creative Cloud]己。

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM article.
-->

## 關於在DAM中儲存資產 {#about-storing-assets-in-a-dam}

為了在創意和行銷／業務線(LOB)團隊之間設計有效率的工作流程並選擇最佳支援功能，請務必瞭解資產儲存在DAM的時機和原因。

### 資產為何儲存在DAM中 {#why-assets-are-stored-in-dam}

將資產儲存在DAM中，讓資產更容易存取，而且可尋找。 它可確保整個組織或生態系統中的眾多使用者（包括合作夥伴、客戶等）都能運用這些資產。

大部分組織都選擇只儲存與下遊行銷/LOB程式相關的資產(透過Adobe Experience Cloud [!DNL Experience Manager Sites] Marketing Cloud、Advertising Cloud等提供給使用者／合作夥伴等的Analytics Cloud或其他通道發佈至網路通道等通道)。 此外，組織會儲存在DAM中可能須經過審查／核准程式的資產。 如此，DAM會儲存大部分有高可能被利用的資產，並避免儲存閒置資產。

儲存資產也須受技術與資源使用考量。 DAM針對儲存的資產提供其他服務，包括擷取中繼資料、版本修訂、產生預覽／轉碼、管理參照以及新增存取控制資訊。 這些服務需要額外的時間和基礎架構資源。

通常，儲存所有資產和更新是不可取的。 例如，如果特定資產的更新品質不佳，且會耗用過多的資源，則資產可能無法儲存在DAM中。

#### 資產儲存在DAM中時 {#when-assets-are-stored-in-dam}

創意團隊（和組織）通常對在資產生命週期的每個階段儲存資產不感興趣。 例如，在下列情況下，他們會避免儲存資產：

* 尚未完成或有待試驗的資產。
* 無法通過創意／內部團隊審閱週期的資產。
* 與相關資產相比，團隊有更好的人選向外部團隊代表其工作。

通常，下列類別資產會儲存在DAM中：

* 已到達特定到期日且被視為可共用的資產。
* 創意團隊預先選取的資產。
* 根據特定合約或合約（例如從RAW檔案轉換的JPG檔案、從PSD原稿轉換的TIFF/影像），行銷部門可使用或要求的特定資產格式。

#### 資產更新儲存在DAM中時 {#when-updates-to-assets-are-stored-in-dam}

通常，只應將與更廣泛的DAM使用者集合相關的資產更新儲存在DAM中。 它可確保使用者（行銷和類似功能）在DAM資產時間軸中只看到相關版本。

通常與資產生命週期中的重要里程碑相關的變更。 例如，創意團隊根據要求／審查提供的初始行銷就緒資產或正式更新應儲存在DAM中，並加以版本控制。

在DAM中要求變更現有資產後，行銷團隊會更新以供其審核，這是相關更新的範例。 它應儲存並更新至DAM的版本，以供進一步參考或還原為舊版。

以下是通常不相關的更新範例：

* 資產上傳的早期版本，在準備好進行行銷審核之前
* 在創作和行銷團隊決定資產已準備就緒之前，在進行中工作階段中經常對資產進行創意變更

### 使用者存取DAM {#user-access-to-dam}

[!DNL Assets] 根據用戶對部署的訪問支援兩種類 [!DNL Assets] 型。 通常，企業網路（防火牆）內的使用者可直接存取DAM。 企業網路以外的其他使用者將無法直接存取。 使用者類型會決定從技術角度可使用哪些整合。

#### 直接存取DAM的創意使用者 {#creative-users-with-direct-access-to-dam}

通常，內部創意團隊或內部網路的廣告公司／創意專業人員都可存取DAM例項，包括登 [!DNL Experience Manager] 入。 [!DNL Experience Manager] 網路基礎設施可以設定為允許直接訪問外部方——通常是受信任的組織，如為客戶工作的機構——通過網路訪問， [!DNL Experience Manager] 例如通過VPN或IP白名單。

在這種情況下，Adobe Asset Link或案頭應用程 [!DNL Experience Manager] 式可協助您輕鬆存取最終／核准的資產，並讓您將創意就緒的資產儲存至DAM。

#### 無法存取DAM的創意使用者 {#creative-users-without-access-to-dam}

無法直接存取DAM例項的外部機構和自由工作者可能需要存取已核准的資產，或想要將其新設計新增至DAM。

使用下列策略來存取最終／核准的資產：

* 如果「資產連結」無法運作，請使用案頭應用程式。
* 使用 [Experience Manager Assets Brand Portal](https://helpx.adobe.com/tw/experience-manager/brand-portal/user-guide.html) ，將資產安全地發佈至外部合作夥伴
* 使用基於資產共用公域的分發和採購門戶的自 [訂實施](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* 使用在必要的網路基礎 [!DNL Experience Manager] 架構（例如，VPN和IP白名單）中設定的訪問控制，讓外部方能夠訪問DAM中的專用內容區域。 他們可以 [!DNL Experience Manager] 使用Web UI取得資產，並將新內容上傳至DAM。

#### 資產的進行中工作 [!DNL Experience Manager] {#work-in-progress-on-assets-from-aem}

如本檔案所述，建議您對資產進行重大更新，有時稱為「進行中的作品」，而不會將儲存至本機檔案的所有編輯內容也上傳至變 [!DNL Experience Manager] 更中。 如此可加速案頭使用者的工作、限制網路頻寬的使用，並讓資產時間軸保持簡潔，並集中在受控的重大更新上。

Adobe Asset Link為此使用案例提供了良好的支援：

* 當Photoshop、InDesign或Illustrator的使用者想要編輯檔案時，會對指定資產執行「取出」操作
* 資產會在背景下載，並放入使用者Creative Cloud案頭應用程式同步至磁碟的Creative Cloud帳戶中，而且會在資產上切換結帳標幟，將編輯衝突降 [!DNL Experience Manager] 至最低
* 從此，使用者會在儲存在同步位置本機的檔案中工作，而且可以繼續工作並儲存必要的變更，以任何頻率需要
* 此外，由於資產位於Creative Cloud帳戶中，因此也可在使用者可能擁有的其他裝置上使用（例如，可在專用的Creative Cloud行動應用程式中開啟或編輯），並可與其他Creative Cloud使用者共用以進行協作。
* 當創意使用者完成變更後，他們可以在其Creative Cloud應用程式中對該檔案執行「登入」操作，並附上選用的註解。 中的對應資產 [!DNL Experience Manager] 會版本化，並更新為新二進位檔。 [!DNL Experience Manager] 像行銷人員或LOB使用者這樣的使用者可透過資產時間表UI存取重大資產變更或里程碑 [!DNL Experience Manager] 的資訊。

[!DNL Experience Manager] 案頭應用程式為在原生應用程式中開啟的資產提供網路共用。 依預設，在本機完成的所有變更會在短暫的一 [!DNL Experience Manager] 段時間後自動上傳至。 有了這種配置，在進行中階段頻繁保存的內容都將上傳到並版本化，從而帶來許多網路流量和潛在的可擴充性挑戰——更不用說中的不必要版本 [!DNL Experience Manager][!DNL Experience Manager]。

這裡建議的方法是使用案頭應用程式中的選項來關閉自動更新，並將資產的變更上傳至手動 [!DNL Experience Manager][!DNL Experience Manager] ，以便運用應用程式的「資產狀態」UI中的上傳變更動作。

#### 大量上傳至DAM {#bulk-upload-to-dam}

在某些情況下，您可能需要同時將大量檔案上傳至DAM，例如：

* 上傳像片或大型專案的結果
* 上傳創意廣告公司提供的資產
* 如果在DAM外完成選取，則從較大的集合上傳選取的資產

此說明是指將檔案上傳為案頭使用者工作流程的一般部分（例如，每週或每張像片）。 此處未涵蓋大型資產遷移。

您可以運用下列上傳功能：

* 若要大量上傳大型／階層式資料夾，請使用提 [!DNL Experience Manager] 供資料夾上傳功能的 [案頭應用程式](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html#bulkupload) 。 您也可以上傳階層式資料夾結構。 [!DNL Assets] 會在背景上傳，因此不會系結至網頁瀏覽器工作階段
* 若要從單一檔案夾上傳幾個檔案，請直接將檔案拖曳至網頁介面，或使用網頁介面中的「建立」 [!DNL Assets] 選項。
* 您也可以根據您的業務需求使用自訂的上載程式。

#### 直接從案頭管理數位資產 {#managing-digital-assets-directly-from-desktop}

如果您使用「網路檔案分享」來管理數位資產，只使用案頭應用程式所映射的網 [!DNL Experience Manager] 路分享就可視為方便的替代方式。 從網路檔案共用轉換時， [!DNL Experience Manager][!DNL Experience Manager] Web介面提供一套豐富的數位資產管理功能，遠超網路共用的功能（搜尋、系列、中繼資料、協作、預覽等），而案頭應用程式則提供方便的連結，將伺服器端的DAM存放庫與桌上型電腦的工作連結。

請避免使 [!DNL Experience Manager] 用案頭應用程式直接在的網路共用中管理資產 [!DNL Assets]。 例如，請避免使用桌 [!DNL Experience Manager] 面應用程式來移動／複製多個檔案。 請改用介 [!DNL Assets] 面，將資料夾從Finder/Explorer拖曳至網路共用，或使用「資料夾上傳」 [!DNL Assets] 功能。

#### 資產移轉 {#asset-migration}

要規劃並執行資產從現有系統遷移到新系統或遷移儲存在伺服器上的大量資產，請參閱遷移 [指南](/help/assets/assets-migration-guide.md)。 [!DNL Experience Manager] 案頭應用程式 [!DNL Experience Manager] 和整 [!DNL Creative Cloud] 合不支援此類移轉。 由於需要吸收的資產數量龐大，以及對元資料映射、轉換和提取的額外要求，因此應使用不同的工具和方法來處理遷移。

>[!MORELIKETHIS]
>
>* [Adobe Asset Link](https://helpx.adobe.com/in/enterprise/using/adobe-asset-link.html)
>* [Experience Manager案頭應用程式最佳實務](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [Experience Manager品牌入口網站](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [Experience Manager與Adobe Stock整合](aem-assets-adobe-stock.md)

