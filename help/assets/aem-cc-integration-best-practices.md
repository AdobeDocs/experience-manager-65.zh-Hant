---
title: 與Adobe Creative Cloud最佳做法整合
description: 整合的最佳做法 [!DNL Adobe Experience Manager] 與 [!DNL Adobe Creative Cloud] 簡化資產轉移工作流並實現高內容速度。
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: Collaboration,Adobe Asset Link,Desktop App
exl-id: c7d589a3-1c5f-4ff0-879e-15e1c556f6dc
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '3280'
ht-degree: 14%

---

# [!DNL Adobe Experience Manager] 和 [!DNL Creative Cloud] 整合最佳做法 {#aem-and-creative-cloud-integration-best-practices}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/aem-cc-integration-best-practices.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/aem-cc-integration-best-practices.html?lang=en) |

[!DNL Adobe Experience Manager Assets] 是可與 [!DNL Adobe Creative Cloud] 幫助DAM用戶與創意團隊協作，簡化內容建立過程中的協作。

[!DNL Adobe Creative Cloud] 為創意團隊提供解決方案和服務生態系統，幫助他們建立數字資產。 它包括案頭和移動應用程式、雲服務（如具有案頭同步或Web體驗的儲存）以及市場，如 [!DNL Adobe Stock]。

閱讀以瞭解根據您的使用案例在台式機和企業級DAM之間選擇哪些整合以及連接工作流的相關最佳實踐。

>[!NOTE]
>
>[!DNL Experience Manager] 至 [!DNL Creative Cloud] 資料夾共用已棄用，本指南不再涉及。 Adobe建議使用較新的功能，如 [Adobe資產連結](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html) 或 [Experience Manager案頭應用](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html) 讓創意用戶能夠訪問管理的資產 [!DNL Experience Manager]。

## 創意人員、營銷人員和DAM用戶的協作需求 {#collaboration-needs-of-creatives-marketers-and-dam-users}

| 要求 | 用例 | 涉及的曲面 |
|---|---|---|
| 簡化台式機創意人員的體驗 | 優化對DAM資產的訪問([!DNL Experience Manager Assets])，或更廣泛地說，適用於在本機資產建立應用程式中工作的台式機用戶。 他們需要一種簡單而直接的方法來發現、使用（開啟）、編輯和保存更改 [!DNL Experience Manager]，以及上載新檔案。 | Win或Mac台式機； [!DNL Creative Cloud] 應用 |
| 提供高質量、可隨時使用的資產 [!DNL Adobe Stock] | 營銷人員通過協助進行資產採購和發現幫助加快內容建立過程。 創意專業人員在其創意工具中直接使用已批准的資產。 | [!DNL Experience Manager Assets]; [!DNL Adobe Stock] 市場；元資料欄位 |
| 按組織分配和共用資產 | 內部部門/地方分支機構和外部合作夥伴、分銷商和代理機構使用母公司共用的批准資產。 該組織希望安全、無縫地共用建立的資產，以便更廣泛地重複使用。 | Brand Portal，資產共用公域 |

## Adobe支援協作需求的產品 {#adobe-offerings-to-support-the-collaboration-need}

| 涉案人員的價值主張 | Adobe | 涉及的曲面 |
|---|---|---|
| 創意用戶從 [!DNL Experience Manager]，開啟並使用它們，編輯和上載更改 [!DNL Experience Manager]，以及將新檔案上載到 [!DNL Experience Manager]，不離開 [!DNL Creative Cloud] 。 | [Adobe資產連結](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | [!DNL Adobe Photoshop], [!DNL Adobe Illustrator], 和 [!DNL Adobe InDesign]. |
| 業務用戶簡化了資產的開啟和使用、編輯和上載更改 [!DNL Experience Manager]，將新檔案上載到 [!DNL Experience Manager] 從案頭環境中。 它們使用通用整合來開啟本機案頭應用程式中的任何資產類型，包括非Adobe類型。 | [Experience Manager案頭應用](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | [!DNL Experience Manager] Win和Mac案頭應用 |
| 營銷人員和業務用戶發現、預覽、許可和保存，並管理 [!DNL Adobe Stock] 資產 [!DNL Experience Manager]。 許可和保存的資產提供選擇 [!DNL Adobe Stock] 元資料，以改善治理。 | [Experience Manager和Adobe Stock一體化](aem-assets-adobe-stock.md) | [!DNL Experience Manager] Web介面 |

本文主要針對協作需求的前兩個方面。資產規模分配和採購作為一個使用案例被簡要提及。針對這些需求解決方案，請考慮Adobe品牌入口網站或資產共用公域。備用解決方案，如 [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)，可基於 [資產共用共用](https://adobe-marketing-cloud.github.io/asset-share-commons/) 元件， [連結共用](/help/assets/link-sharing.md)，使用 [Experience Manager Assets](/help/assets/manage-assets.md) 應根據具體要求進行審查。

![Creative CloudExperience Manager連接，確定要使用的功能](assets/creative-connections-aem.png)

### 用例和Adobe解決方案的映射 {#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| 使用案例 | [!DNL Adobe Asset Link] | [!DNL Experience Manager] 桌面應用程式 | 備注/其他解決方案 |
|---|---|---|---|
| 發現 — 瀏覽DAM資料夾 | 是 | [!DNL Experience Manager] Web介面和案頭操作 |  |
| 發現 — 訪問DAM集合 | 是 | [!DNL Experience Manager] Web介面和案頭操作 |  |
| 發現 — 從DAM搜索資產 | 是 | [!DNL Experience Manager] Web介面和案頭操作 |  |
| 使用 — 開啟資產 | 是 | 是 | [從Web介面開啟](manage-assets.md#previewing-assets) 或來自Finder |
| 使用 — 將資產從DAM放入文檔 | 是 — 嵌入 | 是 — 連結或嵌入 | [!DNL Experience Manager] 案頭應用允許以本地檔案系統上的檔案形式訪問資產。 本機應用中的這些連結由本地路徑表示。 |
| 編輯 — 開啟以進行編輯 | 是 — 簽出操作 | 是 — 開啟操作（在網路共用中） | [AAL簽出](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 預設情況下，將資產保存到用戶的創意雲儲存帳戶(由Creative Cloud應用同步)。 |
| 編輯 — 在DAM外進行中 | 是 — 在與案頭同步的用戶Creative Cloud儲存帳戶中可用的資產。 | 是 |  |
| 編輯 — 上載更改 | 是 —  [簽入操作](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) 帶可選注釋 | 是 |  |
| 上載 — 單個檔案 | 是 — 上載當前活動文檔 | 是 | [通過Web介面上載](manage-assets.md#uploading-assets) |
| 上載 — 多個檔案/分層資料夾結構 | 否 | 是 | [通過Web介面上載](manage-assets.md#uploading-assets) 或通過自定義指令碼或工具。 |
| 雜項 — 用戶和登錄 | Creative Cloud用戶登錄Creative Cloud案頭應用程式後可被識別(SSO) | [!DNL Experience Manager] 用戶和憑據 | 兩種解決方案的用戶都 [!DNL Experience Manager] 用戶配額。 |
| 雜項 — 網路和訪問 | 需要從用戶案頭訪問 [!DNL Experience Manager] 網路部署 | 需要從用戶案頭訪問 [!DNL Experience Manager] 網路部署 | [!DNL Adobe Asset Link] 不共用網路代理環境。 |
| 雜項 — 遷移大量資產 | 否 | 否 | [資產遷移指南](assets-migration-guide.md) |

為支援資產分配使用案例，應考慮其他解決方案：

* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 可配置的SaaS附加模組 [!DNL Experience Manager Assets] 以發佈資產。
* 定制解決方案基於 [資產共用共用](https://adobe-marketing-cloud.github.io/asset-share-commons/) 代碼庫。
* [!DNL Experience Manager] [連結共用](/help/assets/link-sharing.md) 使用連結臨時共用資產。
* [Experience Manager AssetsWeb介面](/help/assets/manage-assets.md) 由外部方擔保的區域 [!DNL Experience Manager] 訪問控制設定和必要的IT/網路配置調整，使這些外部用戶能夠訪問 [!DNL Experience Manager]。

## 關鍵概念和使用案例 {#key-concepts-and-use-cases}

### 通用術語表 {#glossary-of-common-terms}

* **在製品或創意在製品 (WIP)：**&#x200B;在資產生命週期中，資產會經歷多次變更，且通常尚未準備好更廣泛地與其他團隊共用的階段。
* **創意就緒型資產：** [!DNL Assets] 已準備好與更廣泛的團隊共用，或已經由創意團隊選定或批准，以便與市場營銷或LOB團隊共用。
* **資產核准：**&#x200B;針對已上傳至 DAM 的資產執行的核准程序，通常包括品牌核准、法律核准等。
* **最終資產：**&#x200B;已完成所有核准/中繼資料標記，且已準備好更廣泛地供團隊使用的資產。此類資產會儲存在 DAM 中，並提供給所有 (或所有相關的) 使用者使用。這類資產可用於行銷管道，或供創意團隊創作設計。
* **小幅度資產更新/變更：**&#x200B;數位資產的快速微幅變更。此類更新/變更通常是為了因應潤飾或微幅編輯請求、資產檢閱或核准 (例如重新定位、變更文字大小、調整飽和度/亮度、顏色等) 而進行的。
* **重大資產更新/變更：**&#x200B;需要大量工作，且有時需要較長時間才能完成的數位資產變更。其中通常包含多項變更。資產在更新時必須儲存多次。重大資產更新通常會導致資產進入 WIP 階段。
* **DAM：**&#x200B;數位資產管理。在此文檔中， [!DNL Experience Manager Assets]，除非另有說明。
* **創意使用者：**&#x200B;使用 Creative Cloud 應用程式和服務建立數位資產的創意專業人員。在某些情況下，創意使用者可能是可使用 Creative Cloud、但不會建立數位資產的創意團隊成員 (例如創意總監或創意團隊經理)。
* **DAM 使用者：** DAM 系統的一般使用者。視組織而異，DAM 使用者可能是行銷或非行銷使用者，例如企業營運 (LOB) 使用者、圖書管理員、銷售人員等。

### 使用時的注意事項 [!DNL Experience Manager] 和 [!DNL Creative Cloud] 整合 {#considerations-when-using-aem-and-creative-cloud-integration}

* 請參閱 [案頭應用程式最佳實踐](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html#best-practices-to-prevent-troubles)
* 請參閱 [Adobe Stock整合](aem-assets-adobe-stock.md)
* 請參閱 [Adobe資產連結](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)

這是對 [!DNL Experience Manager] 和 [!DNL Creative Cloud] 整合。 閱讀本文檔的其餘部分，以詳細瞭解這些內容。

* **對於在Photoshop、InDesign或Illustrator工作的創意用戶：** Adobe資產連結提供最佳用戶體驗，包括對從中籤出的資產的在建工程進行乾淨處理 [!DNL Experience Manager]。
* **為簡化從案頭訪問任何通用檔案格式或應用程式的資產：** 使用 [!DNL Experience Manager] 案頭應用。
* **瞭解為什麼以及何時將資產儲存在DAM中：** 要提供給您組織中更廣泛團隊的更新。
* **** 請留意共用資產的數量：如果您的使用案例是資產分發，則治理和安全性可能是最重要的方面。請考慮使用大型工具 (例如品牌入口網站) 進行此作業。
* **** 瞭解資產生命週期：瞭解不同團隊在組織中如何處理資產
* **** 謹慎處理資產的頻繁儲存：Adobe Asset Link會透過PS、AI、ID為您處理。對於其他應用程式，請勿在映射/共用資料夾中執行進行中的工作，除非您需要DAM中的所有變更

### 訪問 [!DNL Adobe Stock] 資產 [!DNL Assets] {#access-to-adobe-stock-assets-from-aem-assets}

[Experience Manager和Adobe Stock一體化](/help/assets/aem-assets-adobe-stock.md) 提供 [!DNL Experience Manager] 能夠從中搜索、預覽、許可和保存資產的用戶 [!DNL Adobe Stock] 入 [!DNL Experience Manager]。 許可並保存 [!DNL Stock] 已選擇資產 [!DNL Stock] 元資料，可用於使用額外的篩選器搜索這些元資料。

關於此整合的幾個重要點：

* 將Adobe庫存中的資產保存到 [!DNL Experience Manager]變成了常客 [!DNL Assets]，並將二進位保存到 [!DNL Experience Manager] 儲存庫。 某些與 [!DNL Adobe Stock] 已保存為資產 [!DNL Experience Manager]否則，攝取過程與任何其他檔案看起來相同。 例如，如果智慧標籤處於活動狀態，則在保存時，這些標籤會添加到這些資產中。
* 保存到的資產 [!DNL Experience Manager] 是副本，不是回到的連結 [!DNL Adobe Stock]。

**使用保存自 [!DNL Adobe Stock] 入 [!DNL Experience Manager] 在[!DNL Creative Cloud]**。 此整合獨立於 [!DNL Adobe Asset Link]但 [!DNL Adobe Asset Link] 確認保存自 [!DNL Stock] 並顯示其他元資料和 [!DNL Adobe Stock] 這些資產的徽標 [!DNL Adobe Asset Link] 擴展UI [!DNL Photoshop]。 [!DNL Illustrator]或 [!DNL InDesign]。 這些檔案可用於瀏覽、開啟等 — 因為它們是保存到時的常規資產 [!DNL Experience Manager]。
創意用戶 [!DNL Creative Cloud] 應用程式 [!DNL Adobe Asset Link] 擴展，此外還可以從 [!DNL Adobe Stock] 入 [!DNL Experience Manager]，也可使用 [!DNL Creative Cloud] 用於搜索、預覽和許可的庫面板 [!DNL Adobe Stock] 資產。
[!DNL Assets] 從 [!DNL Adobe Stock] 許可並保存到 [!DNL Experience Manager] 讓更多的團隊 [!DNL Experience Manager Assets] 部署，而創意活動則從 [!DNL Adobe Stock] 通過 [!DNL Creative Cloud] 「庫」面板使它們僅在預設情況下可自用 [!DNL Creative Cloud] 帳戶。

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## 關於在DAM中儲存資產 {#about-storing-assets-in-a-dam}

要在創意和營銷/業務線(LOB)團隊之間設計一個高效的工作流，並選擇最佳支援功能，瞭解資產在何時以及為什麼儲存在DAM中非常重要。

### 為什麼資產儲存在DAM中 {#why-assets-are-stored-in-dam}

將資產儲存在DAM中，可輕鬆訪問和查找。 它確保整個組織或生態系統中的眾多用戶能夠利用這些資產，包括合作夥伴、客戶等。

大多陣列織都選擇只儲存與下游市場營銷/LOB流程相關的資產（通過以下方式發佈到Web渠道等渠道） [!DNL Experience Manager Sites] 或Adobe Experience Cloud提供的其他渠道 — Marketing Cloud、Advertising Cloud、Analytics Cloud等，向用戶/合作夥伴提供服務等)。 此外，組織在DAM中儲存可能要經過審核/批准過程的資產。 這樣，DAM就可以儲存大部分具有高槓桿率的資產，並避免儲存閒置資產。

儲存資產還需要考慮技術和資源利用方面的考慮。 DAM圍繞儲存的資產提供其他服務，包括提取元資料、版本控制、生成預覽/轉碼、管理引用和添加訪問控制資訊。 這些服務消耗了額外的時間和基礎架構資源。

通常，儲存所有資產和更新是不可取的。 例如，如果對特定資產的更新質量差，並且消耗了過多的資源，則資產可能不會儲存在DAM中。

#### 當資產儲存在DAM中時 {#when-assets-are-stored-in-dam}

創意團隊（和組織）通常對在資產生命週期的每個階段儲存資產不感興趣。 例如，在以下情況下，它們避免儲存資產：

* 尚未最終確定或有待試驗的資產。
* 未能通過創意/內部團隊審核週期的資產。
* 與相關資產相比，該團隊有更好的候選人來向外部團隊展示其工作。

通常，以下類資產儲存在DAM中：

* 達到一定期限並被視為可供共用的資產。
* 由創意團隊預先挑選的資產。
* 根據特定合同或協定(例如，從RAW檔案轉換的JPG檔案、從PSD原始檔案轉換的TIFF/影像)，市場營銷可使用或請求的特定資產格式。

#### 當資產更新儲存在DAM中 {#when-updates-to-assets-are-stored-in-dam}

通常，只應將與更廣的DAM用戶組相關的資產更新儲存在DAM中。 它確保用戶（營銷和類似功能）只能在DAM資產時間表中查看相關版本。

通常與資產生命週期中的主要里程碑相關的更改。 例如，應將初始市場準備資產或創意團隊提供的基於請求/審查的正式更新儲存在DAM中並對其進行版本控制。

在請求更改DAM中的現有資產後，創意團隊的更新以供市場營銷團隊審閱是相關更新的示例。 應將其儲存並版本化到DAM中，以供進一步參考或還原到以前的版本。

以下是通常不相關的更新示例：

* 在準備好進行營銷審查之前上載的資產的早期版本
* 在進行中工作階段頻繁對資產進行創造性更改，然後創意和營銷團隊才確定資產已準備好

### 用戶對DAM的訪問 {#user-access-to-dam}

[!DNL Assets] 支援兩種類型的用戶 [!DNL Assets] 部署。 通常，企業網路（防火牆）內的用戶可以直接訪問DAM。 企業網路之外的其他用戶將無權直接訪問。 用戶類型從技術角度確定可以使用哪些整合。

#### 直接訪問DAM的創意用戶 {#creative-users-with-direct-access-to-dam}

通常，內部創意團隊或機構/參與內部網路的創意專業人員可以訪問DAM部署，包括 [!DNL Experience Manager] 登錄。 [!DNL Experience Manager] 網路基礎架構可以設定為允許直接訪問外部方 — 通常是受信任的組織，如為客戶工作的機構 — 以便能夠訪問 [!DNL Experience Manager] 通過網路，例如通過VPN或IP允許清單。

在這種情況下，Adobe資產連結或 [!DNL Experience Manager] 案頭應用程式可幫助您輕鬆訪問最終/批准的資產，並讓您將創意就緒的資產保存到DAM。

#### 無法訪問DAM的創意用戶 {#creative-users-without-access-to-dam}

外部機構和自由職業者無法直接訪問DAM部署，可能需要訪問經批准的資產或希望將新設計添加到DAM。

使用以下策略提供對最終/批准資產的訪問：

* 如果資產連結不工作，則使用案頭應用。
* 使用 [Experience Manager AssetsBrand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) 用於將資產安全地分發給外部合作夥伴
* 使用基於的分發和採購門戶的自定義實現 [資產共用共用](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* 使用在中設定的訪問控制 [!DNL Experience Manager] 以及必要的網路基礎架構（例如，VPN和IP允許清單），使外部方能夠訪問DAM中的專用內容區域。 他們可以 [!DNL Experience Manager] Web UI獲取資產並將新內容上載到您的DAM中。

#### 正在從 [!DNL Experience Manager] {#work-in-progress-on-assets-from-aem}

如本文檔中所討論的，建議對資產執行重大更新，有時稱為正在進行的工作，而不會將保存到本地檔案的所有編輯內容也上載到 [!DNL Experience Manager] 的雙曲餘切值。 這可加快案頭用戶的工作速度，限制網路頻寬的使用，並保持資產時間線整潔，並專注於受控的主要更新。

Adobe資產連結為此使用情形提供了良好的支援：

* 用戶在 [!DNL Photoshop]。 [!DNL InDesign]或 [!DNL Illustrator] 意在編輯檔案，它們對給定資產執行檢出操作
* 資產在後台下載，通過Creative Cloud案頭應用將其放入與磁碟同步的用戶Creative Cloud帳戶中，簽出標誌被切換 [!DNL Experience Manager] 使編輯衝突最小化
* 從此，用戶將在儲存在同步位置本地的檔案中工作，並可以繼續工作並以任何所需頻率保存必要的更改
* 此外，由於資產在Creative Cloud帳戶中，因此用戶可能具有的其他設備上也提供了該資產(例如，可以在專用的Creative Cloud移動應用中開啟或編輯)，並且可以與其他Creative Cloud用戶共用以進行協作。
* 當創意用戶完成更改後，他們可以在其Creative Cloud應用程式中對該檔案執行「簽入」操作，並附上可選注釋。 中的相應資產 [!DNL Experience Manager] 版本化，並使用新二進位檔案更新為。 [!DNL Experience Manager] 像營銷人員或LOB用戶這樣的用戶可以通過以下方式訪問重大資產更改或里程碑： [!DNL Experience Manager] 資產時間表UI。

[!DNL Experience Manager] 案頭應用為在本機應用中開啟的資產提供網路共用。 預設情況下，本地完成的所有更改都上載到 [!DNL Experience Manager] 自動完成。 使用這種配置，在進行中工作階段中經常進行的儲存都將上載到 [!DNL Experience Manager] 版本控制，造成大量網路流量和潛在的可擴充性挑戰 — 更不用說中不必要的版本 [!DNL Experience Manager]。

此處推薦的方法是使用 [!DNL Experience Manager] 案頭應用以關閉自動更新，並將更改上載到 [!DNL Experience Manager] 手動，利用應用的「資產狀態」UI中的上載更改操作。

#### 批量上載到DAM {#bulk-upload-to-dam}

在某些情況下，您可能需要同時將大量檔案上載到DAM中，例如：

* 上傳照片或大型項目的結果
* 上傳創意機構提供的資產
* 如果選擇在DAM外完成，則從較大集上載所選資產

描述是指在操作上（例如，每週或每張照片）上傳檔案，作為案頭用戶工作流的正常部分。 此處未涵蓋大型資產遷移。

您可以利用以下上載功能：

* 要批量上載大型/分層資料夾，請使用 [!DNL Experience Manager] 提供案頭應用 [資料夾上載](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem) 功能。 您還可以上載分層資料夾結構。 [!DNL Assets] 在後台上載，因此它不與Web瀏覽器會話關聯
* 要從單個資料夾上載幾個檔案，請將檔案直接拖到Web介面，或使用 [!DNL Assets] Web介面。
* 根據您的業務需求，您還可以使用自定義上載程式。

#### 直接從台式機管理數字資產 {#managing-digital-assets-directly-from-desktop}

如果您使用網路檔案共用來管理數字資產，只需使用映射的網路共用 [!DNL Experience Manager] 案頭應用可以被視為方便的替代品。 從網路檔案共用轉換時， [!DNL Experience Manager] Web介面提供了一系列豐富的數字資產管理功能，這些功能遠遠超出了網路共用（搜索、收集、元資料、協作、預覽等）的可能範圍， [!DNL Experience Manager] 案頭應用提供了一個方便的連結，可將伺服器端DAM儲存庫與案頭上的工作連接起來。

避免使用 [!DNL Experience Manager] 案頭應用程式，直接管理網路共用中的資產 [!DNL Assets]。 例如，避免使用 [!DNL Experience Manager] 移動/複製多個檔案的案頭應用。 而是使用 [!DNL Assets] 介面，用於將資料夾從Finder/Explorer拖到網路共用或使用 [!DNL Assets] 資料夾上載功能。

#### 資產遷移 {#asset-migration}

要規劃並執行從現有系統到新系統的資產遷移，或遷移儲存在伺服器上的大量資產，請參見 [遷移指南](/help/assets/assets-migration-guide.md)。 [!DNL Experience Manager] 案頭應用和 [!DNL Experience Manager] 至 [!DNL Creative Cloud] 整合不支援此類遷移。 由於要接收的資產數量巨大，以及元資料映射、轉換和接收方面的其他要求，因此應使用不同的工具和方法來處理遷移。

>[!MORELIKETHIS]
>
>* [Adobe資產連結](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [Experience Manager案頭應用最佳實踐](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [Experience ManagerBrand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [Experience Manager和Adobe Stock一體化](aem-assets-adobe-stock.md)

