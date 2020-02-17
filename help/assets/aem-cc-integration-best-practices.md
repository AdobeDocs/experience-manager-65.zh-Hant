---
title: AEM與Creative cloud整合最佳實務
description: 將AEM與Adobe Creative cloud整合的最佳實務，以簡化資產轉讓工作流程並達到最高效率。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# AEM與Creative cloud整合最佳實務 {#aem-and-creative-cloud-integration-best-practices}

<!-- TBD: Reconcile with 6.4 article that's behind this article in terms of content streamlining and structuring.
-->

Adobe Experience Manager Assets是數位資產管理(DAM)解決方案，可與Adobe Creative cloud整合，以協助DAM使用者與創意團隊合作，簡化內容建立程式中的協作。

Adobe Creative cloud為創意團隊提供解決方案與服務生態系統，以協助他們建立數位資產。 它包括案頭和行動應用程式、雲端服務（例如具備案頭同步功能或網頁體驗的儲存空間），以及Adobe Stock等市集。

閱讀內容，瞭解根據您的使用案例，在案頭和企業級DAM之間選擇哪些整合，以及連接工作流程的相關最佳實務。

>[!NOTE]
>
>AEM到Creative cloud資料夾共用已過時，本指南不再涵蓋。 Adobe建議使用較新的功能(例如 [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) 或 [](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/introduction.html) AEM案頭應用程式)，讓創意使用者可存取AEM中管理的資產。

## 創意人員、行銷人員和DAM使用者的協作需求 {#collaboration-needs-of-creatives-marketers-and-dam-users}

| 需求 | 使用案例 | 涉及的曲面 |
|---|---|---|
| 簡化案頭創意人員的體驗 | 簡化從DAM(AEM Assets)為創意專業人員（或更廣泛的是，在原生資產建立應用程式中工作的案頭使用者）存取資產的程式。 他們需要簡單明瞭的方式來探索、使用（開啟）、編輯和儲存AEM的變更，以及上傳新檔案。 | Win或Mac案頭；Creative cloud應用程式 |
| 從Adobe Stock提供高品質、現成可用的資產 | 行銷人員協助資產採購和發現，協助加快內容建立流程。 創意專業人員可直接從其創意工具中使用核准的資產。 | AEM Assets;Adobe Stock市集；中繼資料欄位 |
| 依組織分發及共用資產 | 內部部門／當地分支機構和外部合作夥伴、分銷商和代理商會使用母公司組織共用的已核准資產。 該組織希望安全無縫地共用已建立的資產，以便更廣泛地重複使用。 | 品牌入口網站、資產分享共用 |

## Adobe提供的產品可支援協作需求 {#adobe-offerings-to-support-the-collaboration-need}

| 相關人員的價值主張 | Adobe產品 | 涉及的曲面 |
|---|---|---|
| 創意使用者可從AEM發現資產、開啟並使用資產、編輯和上傳對AEM的變更，以及將新檔案上傳至AEM，而不需離開Creative cloud應用程式。 | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | Photoshop、Illustrator和InDesign |
| 商業使用者可簡化開啟和使用資產、編輯和上傳對AEM的變更，以及從案頭環境將新檔案上傳至AEM。 他們會使用一般整合來開啟原生案頭應用程式中的任何資產類型，包括非Adobe的資產類型。 | [AEM案頭應用程式](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html) | Win和Mac案頭版的AEM案頭應用程式 |
| 行銷人員和商業使用者可從AEM中發現、預覽、授權及儲存及管理Adobe Stock資產。 授權和儲存的資產提供精選的Adobe Stock中繼資料，以提升治理。 | [Experience Manager與Adobe Stock整合](aem-assets-adobe-stock.md) | AEM網頁介面 |

本文主要針對協作需求的前兩個方面。 資產規模分配和採購作為一個使用案例被簡要提及。 針對這些需求解決方案，請考慮Adobe品牌入口網站或資產共用公域。 其他解決方案，例如 [Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html)，這些解決方案可以根據 [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) components、 [Link Share](/help/assets/link-sharing.md)，使用 [](/help/assets/managing-assets-touch-ui.md) Experience Manager Assets建立，應根據特定需求進行審查。

![適用於AEM的Creative cloud連線：決定要使用哪些功能](assets/creative-connections-aem.png)

### 使用案例與Adobe解決方案的對應 {#mapping-of-use-cases-and-adobe-solutions}

| 使用案例 | Adobe Asset Link | AEM案頭應用程式 | 備注／其他解決方案 |
|---|---|---|---|
| Discover —— 瀏覽AEM檔案夾 | 是 | AEM Web UI +案頭動作 | 瀏覽網路共用時，請關閉縮圖以避免下載資產的二進位檔案。 |
| Discover —— 存取AEM系列 | 是 | AEM Web UI +案頭動作 |  |
| Discover —— 搜尋AEM的資產 | 是 | AEM Web UI +案頭動作 |  |
| 使用——開啟資產 | 是 | 是——適用於任何應用程式 | [從Web介面或](managing-assets-touch-ui.md#previewing-assets) Finder開啟 |
| 使用——將AEM的資產置入檔案 | 是——內嵌 | 是——連結或內嵌 | AEM案頭應用程式可讓您在本機檔案系統上，以檔案形式存取資產。 原生應用程式中的這些連結會以本機路徑表示。 |
| 編輯——開啟以進行編輯 | 是——結帳動作 | 是——開啟操作（在網路共用中） | [AAL的結帳功能](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) ，預設會將資產儲存至使用者的Creative cloud儲存帳戶（由Creative cloud應用程式同步）。 |
| 編輯- AEM以外的進行中工作 | 是——同步至案頭的使用者Creative cloud儲存空間帳戶中可用的資產。 | 是 |  |
| 編輯——上傳變更 | 是——使 [用可選注釋](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 簽入操作 | 是 |  |
| 上傳——單一檔案 | 是——上傳目前的作用中檔案 | 是 | [透過網頁介面上傳](managing-assets-touch-ui.md#uploading-assets) |
| 上傳——多個檔案／階層式資料夾結構 | 否 | 是 | [透過網頁介面上傳](managing-assets-touch-ui.md#uploading-assets)；自<br>訂指令碼或工具 |
| 其他——使用者和登入 | 已登入Creative cloud案頭應用程式的Creative cloud使用者可獲得辨識(SSO) | AEM使用者／登入 | 這兩個解決方案的使用者都會根據AEM使用者配額計算。 |
| 其他——網路和訪問 | 需要透過網路從使用者的案頭存取AEM部署 | 需要透過網路從使用者的案頭存取AEM部署 | Adobe Asset Link不會共用網路代理環境。 |
| 其他——移轉大量資產 | 否 | 否 | [遷移指南](assets-migration-guide.md) |

為支援資產散發使用案例，應考慮其他解決方案：

* [品牌入口網站](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html) ，提供可設定、SaaS附加元件至AEM資產，以發佈資產。
* 自訂解決方案是根據「資產共 [用共用共用](https://adobe-marketing-cloud.github.io/asset-share-commons/) 」程式碼庫建立。
* AEM連 [結共用](/help/assets/link-sharing.md) ，使用連結臨機共用資產。
* [AEM Assets網頁介面](/help/assets/managing-assets-touch-ui.md) ，提供由AEM存取控制設定所保護的外部使用者區域，以及必要的IT/網路組態調整，讓這些外部使用者存取AEM。

## 主要概念和使用案例 {#key-concepts-and-use-cases}

### 常見術語辭彙表 {#glossary-of-common-terms}

* **** 在製品或創意在製品(WIP):資產生命週期中的階段，資產會經歷多次變更，通常尚未準備好與更廣泛的團隊共用。
* **** 創意就緒資產：已準備好與更廣大的團隊共用，或已經由創意團隊選取／核准，以便與行銷或LOB團隊共用的資產。
* **** 資產核准：針對已上傳至DAM的資產執行的核准程式，通常包括品牌核准、法律核准等。
* **** 最終資產：已通過所有批准／中繼資料標籤且已準備好供更廣泛團隊使用的資產。 此類資產會儲存在DAM中，並提供給所有（或所有感興趣的）使用者使用。 它可用於行銷管道或創意團隊創作設計。
* **** 次要資產更新／變更：數位資產的快速小變更。 它通常是回應潤飾或次要編輯要求、資產審閱或核准（例如重新定位、變更文字大小、調整飽和度／亮度、顏色等）。
* **** 主要資產更新／變更：對數位資產進行變更，需要做大量工作，有時必須在較長的時間內完成。 它通常包含多項變更。 資產必須在更新時儲存多次。 重大資產更新通常會導致資產進入WIP階段。
* **** DAM:數位資產管理。 在本檔案中，它與AEM Experience Manager Assets同義，除非另有特別提及。
* **** 創意使用者：創意專業人員，使用Creative cloud應用程式和服務來建立數位資產。 在某些情況下，創意使用者可能是可能使用Creative cloud的創意團隊成員，但不會建立數位資產（例如創意主管或創意團隊經理）。
* **** DAM使用者：DAM系統的典型用戶。 DAM使用者可以是行銷或非行銷使用者，例如業務線(LOB)使用者、圖書管理員、銷售人員等。

### 使用AEM和Creative cloud整合時的考量事項 {#considerations-when-using-aem-and-creative-cloud-integration}

* 檢視桌 [面應用程式最佳實務](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/troubleshoot.html#best-practices-to-prevent-troubles)
* 檢視 [Adobe Stock整合](aem-assets-adobe-stock.md)
* 請參 [閱Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)

這是Experience manager與Creative cloud整合的最佳實務簡要摘要。 閱讀本檔案的其餘部分，以詳細瞭解這些內容。

* **** 對於在Photoshop、InDesign或Illustrator中工作的創意使用者：Adobe Asset Link提供最佳的使用者體驗，包括對從AEM結帳的資產進行中工作的簡潔處理
* **** 為簡化從案頭存取任何一般檔案格式或應用程式的資產：使用AEM案頭應用程式
* **** 瞭解在DAM中儲存資產的原因及時機：更新將提供給組織中更廣大的團隊
* **** 請留意共用資產的數量：如果您的使用案例是資產分發，則治理和安全性可能是最重要的方面。 請考慮使用大型工具（例如品牌入口網站）進行此作業。
* **** 瞭解資產生命週期：瞭解不同團隊在組織中如何處理資產
* **** 謹慎處理資產的頻繁儲存：Adobe Asset Link會透過PS、AI、ID為您處理。 對於其他應用程式，請勿在映射／共用資料夾中執行進行中的工作，除非您需要DAM中的所有變更

### 從AEM Assets存取Adobe Stock資產 {#access-to-adobe-stock-assets-from-aem-assets}

[AEM與Adobe Stock整合](/help/assets/aem-assets-adobe-stock.md) ，讓AEM使用者能夠搜尋、預覽、授權和儲存Adobe Stock中的資產。 授權和儲存的Adobe Stock資產已選取Stock中繼資料，可用來使用額外的篩選條件來搜尋。

有關此整合的幾點重要：

* 當Adobe Stock中的資產儲存至AEM時，這些資產會變成一般的AEM資產，並將二進位檔儲存至AEM儲存庫。 有些與Adobe Stock相關的中繼資料會儲存在AEM中用於資產，否則擷取程式看起來與任何其他檔案相同。 例如，如果「智慧型標籤」是作用中，則在儲存時會將標籤新增至這些資產。
* 儲存至AEM的資產是復本，而非回到Adobe Stock的連結。

**在Creative cloud中使用從Adobe Stock儲存至AEM的資產**。 此整合與Adobe Asset Link無關，但Adobe Asset Link會以這種方式辨識從Stock儲存的這些資產，並在Photoshop、Illustrator或InDesign的Adobe Asset Link擴充功能UI中，在這些資產上顯示額外的中繼資料和Stock圖示。 這些檔案可供瀏覽、開啟等使用——因為它們是儲存至AEM時的一般AEM資產。
使用Adobe Asset Link擴充功能之Creative cloud應用程式的創意使用者除了可從Adobe Stock存取已授權的資產到AEM外，還可以使用Creative Cloud Libraries面板來搜尋、預覽及授權Adobe Stock資產。
Adobe Stock中授權並儲存至AEM的資產可供存取AEM Assets部署的更廣大團隊使用，而透過Creative Cloud Libraries面板授權Adobe Stock資產的創意人員則會在其Creative cloud帳戶中預設為自己提供。

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM article.
-->

## 關於在DAM中儲存資產 {#about-storing-assets-in-a-dam}

為了在創意和行銷／業務線(LOB)團隊之間設計有效率的工作流程並選擇最佳支援功能，請務必瞭解資產儲存在DAM的時機和原因。

### 資產為何儲存在DAM中 {#why-assets-are-stored-in-dam}

將資產儲存在DAM中，讓資產更容易存取，而且可尋找。 它可確保整個組織或生態系統中的眾多使用者（包括合作夥伴、客戶等）都能運用這些資產。

大部分組織都選擇只儲存與下遊行銷/LOB程式相關的資產（透過AEM Sites發佈至網路通道，或Adobe Experience Cloud - Marketing Cloud、Advertising cloud提供給使用者／合作夥伴等的其他通道）。 此外，組織會儲存在DAM中可能須經過審查／核准程式的資產。 如此，DAM會儲存大部分有高可能被利用的資產，並避免儲存閒置資產。

儲存資產也須受技術與資源使用考量。 DAM針對儲存的資產提供其他服務，包括擷取中繼資料、版本修訂、產生預覽／轉碼、管理參照以及新增存取控制資訊。 這些服務需要額外的時間和基礎架構資源。

通常，儲存所有資產和更新是不可取的。 例如，如果特定資產的更新品質不佳，且會耗用過多的資源，則資產可能無法儲存在DAM中。

#### 資產儲存在DAM中時 {#when-assets-are-stored-in-dam}

創意團隊（和組織）通常對在資產生命週期的每個階段儲存資產不感興趣。 例如，在下列情況下，他們會避免儲存資產：

* 尚未完成或有待試驗的資產
* 無法通過創意／內部團隊審核週期的資產
* 與相關資產相比，團隊有更好的人選，可向外部團隊代表其工作

通常，下列類別資產會儲存在DAM中：

* 已到期且被視為可供分享的資產
* 創意團隊預先選取的資產
* 根據特定合約或合約（例如從RAW檔案轉換的JPG檔案、從PSD原稿轉換的TIFF/影像），行銷部門可使用或要求的特定資產格式

#### 資產更新儲存在DAM中時 {#when-updates-to-assets-are-stored-in-dam}

通常，只應將與更廣泛的DAM使用者集合相關的資產更新儲存在DAM中。 它可確保使用者（行銷和類似功能）在DAM資產時間軸中只看到相關版本。

通常與資產生命週期中的重要里程碑相關的變更。 例如，創意團隊根據要求／審查提供的初始行銷就緒資產或正式更新應儲存在DAM中，並加以版本控制。

在DAM中要求變更現有資產後，行銷團隊會更新以供其審核，這是相關更新的範例。 它應儲存並更新至DAM的版本，以供進一步參考或還原為舊版。

以下是通常不相關的更新範例：

* 資產上傳的早期版本，在準備好進行行銷審核之前
* 在創作和行銷團隊決定資產已準備就緒之前，在進行中工作階段中經常對資產進行創意變更

### 使用者存取DAM {#user-access-to-dam}

AEM Assets根據使用者對AEM Assets部署的存取權，支援兩種類型的使用者。 通常，企業網路（防火牆）內的使用者可直接存取DAM。 企業網路以外的其他使用者將無法直接存取。 使用者類型會決定從技術角度可使用哪些整合。

#### 直接存取DAM的創意使用者 {#creative-users-with-direct-access-to-dam}

通常，內部創意團隊或已登入內部網路的廣告公司／創意專業人員都可存取DAM例項，包括AEM登入。 AEM和網路基礎架構可設定為允許直接存取外部方——通常是受信任的組織，例如為用戶端工作的機構——可透過網路存取AEM（例如透過VPN或IP白名單）。

在這種情況下，Adobe Asset Link或AEM案頭應用程式可協助您輕鬆存取最終／核准的資產，並讓您將創意就緒的資產儲存至DAM。

#### 無法存取DAM的創意使用者 {#creative-users-without-access-to-dam}

無法直接存取DAM例項的外部機構和自由工作者可能需要存取已核准的資產，或想要將其新設計新增至DAM。

使用下列策略來存取最終／核准的資產：

* 如果「資產連結」無法運作，請使用案頭應用程式。
* 使用 [AEM Assets Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html) ，將資產安全地散發給外部合作夥伴
* 使用基於資產共用公域的分發和採購門戶的自 [訂實施](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* 使用在AEM中設定的存取控制和必要的網路基礎架構（例如VPN和IP白名單），讓外部方存取您DAM中的專屬內容區域。 他們可以使用AEM Web UI來取得資產，並將新內容上傳到您的DAM。

#### AEM資產的進行中工作 {#work-in-progress-on-assets-from-aem}

如本檔案所述，建議您對資產進行重大更新，有時稱為「進行中的作品」，而不會將儲存至本機檔案的所有編輯內容也上傳至AEM。 如此可加速案頭使用者的工作、限制網路頻寬的使用，並讓資產時間軸保持簡潔，並集中在受控的重大更新上。

Adobe Asset Link為此使用案例提供了良好的支援：

* 當Photoshop、InDesign或Illustrator的使用者想要編輯檔案時，會對指定資產執行「取出」操作
* 資產會在背景下載，並放入透過Creative cloud案頭應用程式同步至磁碟的Creative cloud帳戶中，而且會在資產的AEM中切換結帳標幟，將編輯衝突降至最低
* 從此，使用者會在儲存在同步位置本機的檔案中工作，而且可以繼續工作並儲存必要的變更，以任何頻率需要
* 此外，由於資產位於Creative cloud帳戶中，因此也可在使用者可能擁有的其他裝置上使用（例如，可在專用的Creative cloud行動應用程式中開啟或編輯），並可與其他Creative cloud使用者共用以進行協作。
* 當創意使用者完成變更後，他們可以在其Creative cloud應用程式中對該檔案執行「登入」操作，並附上選用的註解。 AEM中的對應資產會版本化，並更新為新的二進位檔。 「行銷人員」或「LOB」等AEM使用者可透過AEM資產時間軸UI，存取主要資產變更或里程碑。

AEM案頭應用程式提供在原生應用程式中開啟之資產的網路共用。 依預設，在短暫的時間後，所有在本機完成的變更都會自動上傳至AEM。 有了這樣的設定，在進行中階段中經常儲存的檔案都會上傳至AEM並加上版本，造成許多網路流量和潛在的擴充性挑戰——更不用說AEM中不必要的版本了。

這裡建議的方法是使用AEM案頭應用程式中的選項來關閉自動更新，並手動將資產的變更上傳至AEM，以運用應用程式的「資產狀態」UI中的上傳變更動作。

#### 大量上傳至DAM {#bulk-upload-to-dam}

在某些情況下，您可能需要同時將大量檔案上傳至DAM，例如：

* 上傳像片或大型專案的結果
* 上傳創意廣告公司提供的資產
* 如果在DAM外完成選取，則從較大的集合上傳選取的資產

此說明是指將檔案上傳為案頭使用者工作流程的一般部分（例如，每週或每張像片）。 此處未涵蓋大型資產遷移。

您可以運用下列上傳功能：

* 若要大量上傳大型／階層式資料夾，請使用提供資料夾上傳功能的AEM [案頭應用程](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html#bulkupload) 式。 您也可以上傳階層式資料夾結構。 資產會在背景上傳，因此不會系結至網頁瀏覽器作業
* 若要從單一檔案夾上傳幾個檔案，請直接將檔案拖曳至Web介面，或使用AEM Assets網頁介面中的「建立」選項。
* 您也可以根據您的業務需求使用自訂的上載程式。

#### 直接從案頭管理數位資產 {#managing-digital-assets-directly-from-desktop}

如果您使用「網路檔案分享」來管理數位資產，只要使用AEM案頭應用程式所映射的網路分享，就會被視為方便的替代項目。 從網路檔案分享轉換時，AEM網頁介面提供豐富的數位資產管理功能集，遠超網路分享（搜尋、系列、中繼資料、協作、預覽等）的可能，而AEM案頭應用程式則提供方便的連結，將伺服器端的DAM存放庫與桌上型電腦的作品連接。

請避免使用AEM案頭應用程式直接在AEM Assets的網路共用中管理資產。 例如，請避免使用AEM案頭應用程式來移動／複製多個檔案。 請改用AEM Assets網頁UI，將檔案夾從Finder/Explorer拖曳至網路共用，或使用AEM Assets檔案夾上傳功能。

#### 資產移轉 {#asset-migration}

要規劃並執行資產從現有系統遷移到新系統或遷移儲存在伺服器上的大量資產，請參閱遷移 [指南](/help/assets/assets-migration-guide.md)。 AEM案頭應用程式和AEM到Creative cloud的整合不支援此類移轉。 由於需要吸收的資產數量龐大，以及對元資料映射、轉換和提取的額外要求，因此應使用不同的工具和方法來處理遷移。

>[!MORELIKETHIS]
>
>* [Adobe Asset Link](https://helpx.adobe.com/in/enterprise/using/adobe-asset-link.html)
>* [AEM案頭應用程式最佳範例](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [AEM Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [AEM與Adobe Stock整合](aem-assets-adobe-stock.md)

