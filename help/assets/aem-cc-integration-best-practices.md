---
title: 與Adobe Creative Cloud最佳實務整合
description: 將 [!DNL Adobe Experience Manager] 與 [!DNL Adobe Creative Cloud] 整合的最佳實務，以簡化資產轉移工作流程，並達到高內容速度。
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: Collaboration,Adobe Asset Link,Desktop App
exl-id: c7d589a3-1c5f-4ff0-879e-15e1c556f6dc
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: a144f7cc75b1a5cdb45d2aaf90e87013ac68a431
workflow-type: tm+mt
source-wordcount: '3173'
ht-degree: 11%

---

# [!DNL Adobe Experience Manager]與[!DNL Creative Cloud]整合最佳實務 {#aem-and-creative-cloud-integration-best-practices}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/aem-cc-integration-best-practices) |
| AEM 6.5 | 本文章 |

[!DNL Adobe Experience Manager Assets]是數位資產管理(DAM)解決方案，可與[!DNL Adobe Creative Cloud]整合，以協助DAM使用者與創意團隊合作，精簡內容建立過程中的共同作業。

[!DNL Adobe Creative Cloud]為創意團隊提供解決方案和服務的生態系統，以協助他們建立數位資產。 其中包含案頭和行動應用程式、雲端服務（例如具有案頭同步或Web體驗的儲存空間）以及行銷場所（例如[!DNL Adobe Stock]）。

請閱讀下文，瞭解根據您的使用案例，在桌上型電腦和企業級DAM之間選擇哪些整合，以及連線工作流程的相關最佳實務為何。

>[!NOTE]
>
>[!DNL Experience Manager]到[!DNL Creative Cloud]資料夾共用已棄用，不再包含在本指南中。 Adobe建議使用較新的功能，例如[AdobeAsset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)或[Experience Manager案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html)，讓創意使用者能存取[!DNL Experience Manager]中管理的資產。

## 創意工作者、行銷人員和DAM使用者的Collaboration需求 {#collaboration-needs-of-creatives-marketers-and-dam-users}

| 要求 | 使用案例 | 相關曲面 |
|---|---|---|
| 簡化創意人員在桌上型電腦上的體驗 | 精簡從DAM ([!DNL Experience Manager Assets])存取資產的程式，方便創意專業人士或更廣義的使用者使用在原生資產建立應用程式中工作的案頭。 他們需要一種簡單明瞭的方式，以探索、使用（開啟）、編輯和儲存對[!DNL Experience Manager]的變更，以及上傳新檔案。 | Win或Mac案頭； [!DNL Creative Cloud]個應用程式 |
| 從[!DNL Adobe Stock]提供高品質、現成可用的資產 | 行銷人員協助資產來源和探索，以加速內容建立流程。 創意專業人士會直接從自己的創意工具中使用核准的資產。 | [!DNL Experience Manager Assets]；[!DNL Adobe Stock]市集；中繼資料欄位 |
| 依組織分配與共用資產 | 內部部門/當地分支機構和外部合作夥伴、分銷商和代理商會使用上級組織共用的已核准資產。 企業想要安全且順暢地共用已建立的資產，以便更廣泛地重複使用。 | Brand Portal、Asset Share Commons |

## 支援協同合作需求的Adobe方案 {#adobe-offerings-to-support-the-collaboration-need}

| 相關角色的價值主張 | Adobe產品 | 相關曲面 |
|---|---|---|
| 創意使用者從[!DNL Experience Manager]探索資產、開啟並使用資產、編輯和上傳變更至[!DNL Experience Manager]，以及上傳新檔案至[!DNL Experience Manager]，無需離開[!DNL Creative Cloud]應用程式。 | [Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html) | [!DNL Adobe Photoshop]、[!DNL Adobe Illustrator] 和 [!DNL Adobe InDesign]。 |
| 商務使用者可簡化開啟和使用資產、編輯和上傳[!DNL Experience Manager]的變更，以及從案頭環境上傳新檔案至[!DNL Experience Manager]的程式。 他們使用一般整合，在原生案頭應用程式中開啟任何資產型別，包括非Adobe資產型別。 | [Experience Manager案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | Win和Mac案頭上的[!DNL Experience Manager]案頭應用程式 |
| 行銷人員和商務使用者可在[!DNL Experience Manager]內探索、預覽、授權及儲存並管理[!DNL Adobe Stock]資產。 授權和儲存的資產提供選取的[!DNL Adobe Stock]個中繼資料，以便進行更好的管理。 | [Experience Manager與Adobe Stock整合](aem-assets-adobe-stock.md) | [!DNL Experience Manager]網頁介面 |

本文主要針對協作需求的前兩個方面。資產規模分配和採購作為一個使用案例被簡要提及。針對這些需求解決方案，請考慮Adobe品牌入口網站或資產共用公域。其他解決方案，例如[Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)，可根據[Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)元件，[Link Share](/help/assets/link-sharing.md)，使用[Experience Manager Assets](/help/assets/manage-assets.md)建置的解決方案，應根據特定需求檢閱。

![Creative CloudExperience Manager的連線，決定要使用哪個功能](assets/creative-connections-aem.png)

### 使用案例和Adobe解決方案的對應 {#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| 使用案例 | [!DNL Adobe Asset Link] | [!DNL Experience Manager] 桌面應用程式 | 備註/其他解決方案 |
|---|---|---|---|
| 探索 — 瀏覽DAM資料夾 | 是 | [!DNL Experience Manager]網頁介面和案頭動作 | |
| 探索 — 存取DAM集合 | 是 | [!DNL Experience Manager]網頁介面和案頭動作 | |
| 探索 — 從DAM搜尋資產 | 是 | [!DNL Experience Manager]網頁介面和案頭動作 | |
| 使用 — 開啟資產 | 是 | 是 | [從網頁介面](manage-assets.md#previewing-assets)或從Finder開啟 |
| 使用 — 將來自DAM的資產放入檔案中 | 是 — 內嵌 | 是 — 連結或內嵌 | [!DNL Experience Manager]案頭應用程式可存取本機檔案系統上的資產。 原生應用程式中的這些連結會以本機路徑表示。 |
| 編輯 — 開啟以進行編輯 | 是 — 結帳動作 | 是 — 開啟動作（在網路共用中） | 依預設，[在AAL中籤出](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)會將資產儲存到使用者的Creative Cloud儲存空間帳戶(由Creative Cloud應用程式同步)。 |
| 編輯 — DAM外部正在進行中的工作 | 是 — 資產可在同步至桌上型電腦的使用者Creative Cloud儲存帳戶中使用。 | 是 | |
| 編輯 — 上傳變更 | 是 — [簽入動作](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)加上選擇性註解 | 是 | |
| 上傳 — 單一檔案 | 是 — 上傳目前作用中的檔案 | 是 | [透過網頁介面上傳](manage-assets.md#uploading-assets) |
| 上傳 — 多個檔案/階層資料夾結構 | 否 | 是 | [透過網頁介面](manage-assets.md#uploading-assets)或自訂指令碼或工具上傳。 |
| 其他 — 使用者和登入 | 可辨識登入Creative Cloud案頭應用程式的Creative Cloud使用者(SSO) | [!DNL Experience Manager]個使用者和認證 | 這兩個解決方案的使用者都計入[!DNL Experience Manager]使用者配額。 |
| 雜項 — 網路與存取 | 需要透過網路從使用者的案頭存取[!DNL Experience Manager]部署 | 需要透過網路從使用者的案頭存取[!DNL Experience Manager]部署 | [!DNL Adobe Asset Link]不共用網路Proxy環境。 |
| 雜項 — 移轉大量資產 | 否 | 否 | [Assets移轉指南](assets-migration-guide.md) |

若要支援資產散佈使用案例，應考慮其他解決方案：

* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)可供設定的SaaS附加元件至[!DNL Experience Manager Assets]以發佈資產。
* 自訂解決方案是根據[Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)程式碼基底建立的。
* [!DNL Experience Manager] [連結共用](/help/assets/link-sharing.md)以使用連結隨選共用資產。
* [Experience Manager Assets網頁介面](/help/assets/manage-assets.md)，包含外部合作對象區域，由[!DNL Experience Manager]存取控制設定保護，並包含必要的IT/網路組態調整，可讓這些外部使用者存取[!DNL Experience Manager]。

## 重要概念與使用案例 {#key-concepts-and-use-cases}

### 常用辭彙表 {#glossary-of-common-terms}

* **在製品或創意在製品 (WIP)：**&#x200B;在資產生命週期中，資產會經歷多次變更，且通常尚未準備好更廣泛地與其他團隊共用的階段。
* **創意成熟資產：** [!DNL Assets]已準備好更廣泛地與其他團隊共用，或已獲創意團隊選取或核准，要與行銷或LOB團隊共用。
* **資產核准：**&#x200B;針對已上傳至 DAM 的資產執行的核准程序，通常包括品牌核准、法律核准等。
* **最終資產：**&#x200B;已完成所有核准/中繼資料標籤，且已準備好更廣泛地供團隊使用的資產。 此類資產會儲存在 DAM 中，並提供給所有 (或所有相關的) 使用者使用。這類資產可用於行銷管道，或供創意團隊創作設計。
* **小幅度資產更新/變更：**&#x200B;數位資產的快速微幅變更。 此類更新/變更通常是為了因應潤飾或微幅編輯請求、資產檢閱或核准 (例如重新定位、變更文字大小、調整飽和度/亮度、顏色等) 而進行的。
* **重大資產更新/變更：**&#x200B;需要大量工作，且有時需要較長時間才能完成的數位資產變更。 其中通常包含多項變更。資產在更新時必須儲存多次。重大資產更新通常會導致資產進入 WIP 階段。
* **DAM：**&#x200B;數位資產管理。在此檔案中，除非另有特別說明，否則與[!DNL Experience Manager Assets]同義。
* **創意使用者：**&#x200B;使用 Creative Cloud 應用程式和服務建立數位資產的創意專業人員。在某些情況下，創意使用者可能是可使用 Creative Cloud、但不會建立數位資產的創意團隊成員 (例如創意總監或創意團隊經理)。
* **DAM 使用者：** DAM 系統的一般使用者。視組織而定，DAM使用者可能是行銷或非行銷使用者，例如企業營運(LOB)使用者、圖書管理員、銷售人員等。

### 使用[!DNL Experience Manager]與[!DNL Creative Cloud]整合時的考量事項 {#considerations-when-using-aem-and-creative-cloud-integration}

* 檢視[案頭應用程式最佳實務](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html#best-practices-to-prevent-troubles)
* 檢視[Adobe Stock整合](aem-assets-adobe-stock.md)
* 檢視[Adobe資產連結](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)

這是[!DNL Experience Manager]與[!DNL Creative Cloud]整合的最佳實務的簡短摘要。 請閱讀本檔案的其餘部分，以取得這些專案的詳細瞭解。

* **對於在Photoshop、InDesign或Illustrator中工作的創意使用者：** Adobe Asset Link提供最佳的使用者體驗，包括對從[!DNL Experience Manager]結帳的資產進行中工作的簡潔處理。
* **為簡化從案頭存取任何一般檔案格式或應用程式的資產：**&#x200B;請使用[!DNL Experience Manager]案頭應用程式。
* **瞭解在DAM中儲存資產的原因和時間：**&#x200B;更新將提供給組織中更廣大的團隊。
* **&#x200B;**&#x200B;請留意共用資產的數量：如果您的使用案例是資產分發，則治理和安全性可能是最重要的方面。請考慮使用大型工具 (例如品牌入口網站) 進行此作業。
* **&#x200B;**&#x200B;瞭解資產生命週期：瞭解不同團隊在組織中如何處理資產
* **&#x200B;**&#x200B;謹慎處理資產的頻繁儲存：Adobe Asset Link會透過PS、AI、ID為您處理。對於其他應用程式，請勿在對映/共用資料夾中執行進行中的工作，除非您需要DAM中的所有變更

### 從[!DNL Assets]存取[!DNL Adobe Stock]資產 {#access-to-adobe-stock-assets-from-aem-assets}

[Experience Manager與Adobe Stock整合](/help/assets/aem-assets-adobe-stock.md)可讓[!DNL Experience Manager]個使用者搜尋、預覽、授權及儲存從[!DNL Adobe Stock]到[!DNL Experience Manager]的資產。 授權並儲存的[!DNL Stock]個資產已選取[!DNL Stock]個中繼資料，這些中繼資料可用來透過額外的篩選器搜尋這些資產。

關於這項整合的一些要點：

* 當Adobe庫存中的資產儲存到[!DNL Experience Manager]時，它們會變成一般[!DNL Assets]，而二進位檔案會儲存到[!DNL Experience Manager]存放庫。 與[!DNL Adobe Stock]相關的部分中繼資料會儲存在[!DNL Experience Manager]中的資產，否則擷取程式看起來會與任何其他檔案相同。 例如，如果智慧標籤作用中，會在儲存時將標籤新增到這些資產。
* 儲存到[!DNL Experience Manager]的資產是復本，而不是連結回[!DNL Adobe Stock]。

**正在處理從[!DNL Adobe Stock]儲存到[!DNL Creative Cloud]**&#x200B;中[!DNL Experience Manager]的資產。 此整合獨立於[!DNL Adobe Asset Link]，但[!DNL Adobe Asset Link]可辨識這些以此方式從[!DNL Stock]儲存的資產，並在[!DNL Photoshop]、[!DNL Illustrator]或[!DNL InDesign]的[!DNL Adobe Asset Link]擴充功能UI中，於這些資產上顯示額外的中繼資料和[!DNL Adobe Stock]標誌。 這些檔案可供瀏覽、開啟等操作，因為它們是儲存至[!DNL Experience Manager]的一般資產。
使用[!DNL Creative Cloud]應用程式，且有[!DNL Adobe Asset Link]副檔名存在的創意使用者，除了可以存取已從[!DNL Adobe Stock]到[!DNL Experience Manager]的已授權資產，還可以使用[!DNL Creative Cloud]資料庫面板來搜尋、預覽和授權[!DNL Adobe Stock]資產。
來自[!DNL Adobe Stock]的授權並儲存至[!DNL Experience Manager]的[!DNL Assets]可供存取[!DNL Experience Manager Assets]部署的更廣泛團隊使用，而來自[!DNL Adobe Stock]的創意內容授權資產則透過[!DNL Creative Cloud]資料庫面板，預設只能在其[!DNL Creative Cloud]帳戶中供自己使用。

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## 關於在DAM中儲存資產 {#about-storing-assets-in-a-dam}

為了在創意和行銷/業務線(LOB)團隊之間設計有效率的工作流程，並選擇最佳支援功能，瞭解資產儲存在DAM中的時間和原因非常重要。

### 為何資產儲存在DAM中 {#why-assets-are-stored-in-dam}

將資產儲存在DAM中，可讓您輕鬆存取及找到資產。 這可確保整個組織或生態系統中的多位使用者（包括合作夥伴、客戶等）都能使用資產。

大多陣列織會選擇僅儲存與下遊行銷/LOB程式相關的資產(透過[!DNL Experience Manager Sites]發佈至Web管道之類的管道，或發佈至Adobe Experience Cloud提供的其他管道(Marketing Cloud、Advertising Cloud和Analytics Cloud測量，提供給使用者/合作夥伴等)。 此外，組織可儲存資產，這些資產可能會在DAM中接受稽核/核准程式。 如此一來，DAM主要儲存極有可能使用的資產，避免儲存閒置資產。

儲存資產也受到技術和資源使用率考量的限制。 DAM提供有關已儲存資產的其他服務，包括擷取中繼資料、版本設定、產生預覽/轉碼、管理參考和新增存取控制資訊。 這些服務會消耗額外的時間和基礎架構資源。

通常情況下，儲存所有資產和更新都是不想要的。 例如，如果特定資產的更新品質不佳並消耗過多資源，則資產可能不會儲存在DAM中。

#### 當資產儲存在DAM時 {#when-assets-are-stored-in-dam}

創意團隊（和組織）通常對儲存資產生命週期每個階段的資產不感興趣。 例如，他們會避免在下列情況下儲存資產：

* 尚未完成或有待實驗的Assets。
* 未通過創意/內部團隊稽核週期的Assets。
* 相較於相關資產，團隊擁有更好的候選人來向外部團隊代表其工作。

通常，以下類別資產會儲存在DAM中：

* 已達特定成熟度並被視為已準備好共用的Assets。
* 創意團隊預先選取的Assets。
* 行銷可用的或請求的特定資產格式，取決於特定合約或協定(例如，從RAW檔案轉換的JPG檔案、來自PSD原始資料的TIFF/影像)。

#### 當資產的更新儲存在DAM中時 {#when-updates-to-assets-are-stored-in-dam}

一般而言，只有與更廣泛的DAM使用者組相關的資產更新才應儲存在DAM中。 這可確保使用者（行銷和類似功能）在DAM資產時間軸中只能看到相關版本。

通常會與資產生命週期中的主要里程碑相關的變更。 例如，初始行銷就緒資產或根據創意團隊提供的請求/稽核的正式更新應儲存在DAM中並進行版本設定。

相關更新的範例為創意團隊的更新，以供行銷團隊在請求變更DAM中的現有資產後檢閱。 應儲存在DAM中並進行版本設定，以供進一步參考或回覆至先前的版本。

以下是通常不相關的更新範例：

* 在資產準備好供行銷檢閱之前上傳資產的早期版本
* 創意和行銷團隊決定資產準備好之前，經常在創作中階段對資產進行創意變更

### DAM的使用者存取權 {#user-access-to-dam}

根據使用者對[!DNL Assets]部署的存取權，[!DNL Assets]支援兩種使用者。 一般而言，企業網路（防火牆）內的使用者可直接存取DAM。 企業網路以外的其他使用者無法直接存取。 使用者型別會從技術的角度決定可使用哪些整合。

#### 可直接存取DAM的創意使用者 {#creative-users-with-direct-access-to-dam}

一般而言，內部創意團隊或加入內部網路的代理商/創意專業人士可存取DAM部署，包括[!DNL Experience Manager]登入。 [!DNL Experience Manager]和網路基礎架構可以設定為允許直接存取外部合作對象（通常是受信任的組織，例如為使用者端工作的代理程式），以透過網路存取[!DNL Experience Manager]，例如透過VPN或IP允許清單。

在這種情況下，AdobeAsset Link或[!DNL Experience Manager]案頭應用程式可協助您輕鬆存取最終/已核准資產，並讓您將創意就緒的資產儲存到DAM。

#### 沒有DAM存取權的創意使用者 {#creative-users-without-access-to-dam}

無法直接存取DAM部署的外部機構和自由職業者可能需要存取已核准的資產，或想要將其新設計新增到DAM。

使用下列策略提供最終/已核准資產的存取權：

* 如果Asset Link無法運作，請使用案頭應用程式。
* 使用[Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)將資產安全地散發給外部合作夥伴
* 使用以[Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)為基礎的自訂發佈和來源入口網站實作
* 使用在[!DNL Experience Manager]中設定的存取控制及必要的網路基礎結構（例如VPN和IP允許清單），讓外部合作對象能夠存取DAM中的專用內容區域。 他們可以使用[!DNL Experience Manager] Web UI來取得資產，並將新內容上傳到您的DAM。

#### 正在處理來自[!DNL Experience Manager]的資產 {#work-in-progress-on-assets-from-aem}

如本檔案所述，建議對資產執行重大更新，有時稱為進行中的工作，而不需將所有編輯內容儲存至本機檔案，且不會以變更形式上傳至[!DNL Experience Manager]。 這可加快案頭使用者的工作速度、限制使用的網路頻寬，並讓資產時間表保持整潔，並專注於受控制的重大更新。

Adobe Asset Link針對此使用案例提供良好的支援：

* 當[!DNL Photoshop]、[!DNL InDesign]或[!DNL Illustrator]中的使用者想要編輯檔案時，他們會對指定的資產執行簽出操作
* 資產會在背景下載，並透過Creative Cloud案頭應用程式放入使用者Creative Cloud帳戶同步處理至磁碟，而資產上的[!DNL Experience Manager]中會切換籤出旗標，以將編輯衝突減至最低
* 從此處，使用者可在檔案中工作，該檔案儲存在同步位置中的本機，並可繼續工作，並視需要以任意頻率儲存必要的變更
* 此外，由於資產位於Creative Cloud帳戶中，因此該資產也可在使用者可能擁有的其他裝置上使用(例如，可在專用的Creative Cloud行動應用程式中開啟或編輯)，並可與其他Creative Cloud使用者共用，以進行共同作業。
* 當創意使用者完成變更時，他們可以在其Creative Cloud應用程式中對該檔案執行簽入操作，並附上可選註釋。 [!DNL Experience Manager]中對應的資產已建立版本，並使用新的二進位檔更新為。 行銷人員或LOB使用者等[!DNL Experience Manager]使用者可以透過[!DNL Experience Manager]資產時間軸UI存取重大資產變更或里程碑。

[!DNL Experience Manager]案頭應用程式為原生應用程式中開啟的資產提供網路共用。 根據預設，所有在本機完成的變更會在短暫的時間後自動上傳到[!DNL Experience Manager]。 透過這種設定，在創作階段期間頻繁的儲存將會全部上傳到[!DNL Experience Manager]並進行版本設定，造成大量的網路流量和潛在的可擴充性挑戰，更不用說[!DNL Experience Manager]中不必要的版本了。

這裡建議的方法是使用[!DNL Experience Manager]案頭應用程式中的選項來關閉自動更新，並使用應用程式資產狀態UI中的上傳變更動作，手動將資產變更上傳到[!DNL Experience Manager]。

#### 大量上傳至DAM {#bulk-upload-to-dam}

在某些案例中，您可能會需要同時將大量檔案上傳到DAM，例如：

* 上傳拍照或大型專案的結果
* 上傳創意公司提供的資產
* 如果選取是在DAM以外完成，則從較大的集合上傳選取的資產

說明是指以作業方式上傳檔案（例如，每週或每次拍照），作為案頭使用者工作流程的一般部分。 這裡不涵蓋大型資產移轉。

您可以使用以下上傳功能：

* 若要大量上傳大型/階層資料夾，請使用提供[資料夾上傳](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem)功能的[!DNL Experience Manager]案頭應用程式。 您也可以上傳階層資料夾結構。 [!DNL Assets]已在背景上傳，因此未繫結至網頁瀏覽器工作階段
* 若要從單一資料夾上傳一些檔案，請直接將檔案拖曳到網頁介面，或使用[!DNL Assets]網頁介面中的[建立]選項。
* 您也可以根據您的業務需求使用自訂上傳程式。

#### 直接從案頭管理數位資產 {#managing-digital-assets-directly-from-desktop}

如果您使用「網路檔案共用」來管理數位資產，只要使用[!DNL Experience Manager]案頭應用程式對應的網路共用就可以被視為方便的替代方式。 從網路檔案共用轉換時，[!DNL Experience Manager]網頁介面提供了一組豐富的數位資產管理功能，這些功能遠遠超越了網路共用上所具備的功能（搜尋、集合、中繼資料、共同作業、預覽等），而[!DNL Experience Manager]案頭應用程式則提供便利的連結，可將伺服器端DAM存放庫與案頭上的工作連結。

避免使用[!DNL Experience Manager]案頭應用程式直接管理[!DNL Assets]網路共用中的資產。 例如，避免使用[!DNL Experience Manager]案頭應用程式來移動/複製多個檔案。 請改用[!DNL Assets]介面將資料夾從Finder/Explorer拖曳至網路共用或使用[!DNL Assets]資料夾上傳功能。

#### 資產移轉 {#asset-migration}

若要規劃並執行從現有系統到新系統的資產移轉，或移轉儲存在伺服器上的大量資產，請參閱[移轉指南](/help/assets/assets-migration-guide.md)。 [!DNL Experience Manager]案頭應用程式和[!DNL Experience Manager]到[!DNL Creative Cloud]的整合不支援這類移轉。 由於要擷取的資產數量龐大，以及中繼資料對應、轉換和擷取方面的其他需求，應使用不同的工具和方法來處理移轉。

>[!MORELIKETHIS]
>
>* [Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)
>* [Experience Manager案頭應用程式最佳實務](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [Experience ManagerBrand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [Experience Manager與Adobe Stock整合](aem-assets-adobe-stock.md)
