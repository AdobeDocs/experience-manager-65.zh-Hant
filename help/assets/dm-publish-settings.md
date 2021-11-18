---
title: 設定影像伺服器的Dynamic Media發佈設定
description: 了解如何在Dynamic Media中設定發佈。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
hide: true
hidefromtoc: true
exl-id: null
source-git-commit: 26f521868d0b983a05579d0d4c1ef50684b721ee
workflow-type: tm+mt
source-wordcount: '3443'
ht-degree: 2%

---


# 設定影像伺服器的Dynamic Media發佈設定

只有符合以下條件時，才可使用設定Dynamic Media發佈設定：

* 您以Scene7模式執行Dynamic Media。 請參閱 [在Scene7模式中啟用Dynamic Media](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode)
* 您有 *現有* **[!UICONTROL Dynamic Media設定]** (在 **[!UICONTROL Cloud Services]**)、Adobe Experience Manager 6.5或Experience Manageras a Cloud Service。
* 您是具有管理員權限的Experience Manager系統管理員。

Dynamic Media發佈設定供經驗豐富的網站開發人員和程式設計人員使用。 Adobe Dynamic Media建議變更這些發佈設定的使用者熟悉AdobeDynamic Media、HTTP通訊協定標準和慣例，以及基本影像技術。

「Dynamic Media發佈設定」頁面會建立預設設定，決定如何將AdobeDynamic Media伺服器傳遞至網站或應用程式。 如果未指定任何設定，AdobeDynamic Media伺服器會根據Dynamic Media發佈設定頁面上設定的預設設定來傳送資產。

>[!NOTE]
>
>在Adobe Experience Manager上從Dynamic Media Classic升級至Dynamic Media? Dynamic Media中的「一般設定」和「發佈設定」頁面會預先填入您Dynamic Media Classic帳戶取得的值。 例外是 **[!UICONTROL 預設上傳選項]** 「一般設定」頁面的區域。 這些值已處於Experience Manager。 因此，您在 **[!UICONTROL 預設上傳選項]**，則透過「Experience Manager」使用者介面顯示在Dynamic Media中，而非Dynamic Media Classic中。 「一般設定」和「發佈設定」頁面中的所有其他設定和值，都會在Dynamic Media Classic和Dynamic Media之間Experience Manager維護。

另請參閱 [Dynamic Media - Scene7模式設定的設定與設定](/help/assets/option-b-config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings).

**若要設定Dynamic Media Publish設定影像伺服器：**

1. 在「Experience Manager作者」模式中，選取Experience Manager標誌以存取全域導覽主控台。
1. 在左側邊欄中，選取「工具」圖示，然後前往 **[!UICONTROL 資產]** > **[!UICONTROL Dynamic Media發佈設定]**.
1. 在「影像伺服器」頁面中，設定您的影像伺服器 — 發佈內容，然後使用五個索引標籤來配置預設發佈設定。

   * [影像伺服器](#image-server)
   * [安全性](#security-tab) 標籤
   * [目錄管理](#catalog-management-tab) 標籤
   * [請求屬性](#request-attributes-tab) 標籤
   * [常見縮圖屬性](#common-thumbnail-attributes-tab) 標籤
   * [色彩管理屬性](#color-management-attributes-tab) 標籤

   ![Dynamic Media發佈設定頁面](/help/assets/assets-dm/dm-publish-setup.png)
   *Dynamic Media發佈設定頁面，**[!UICONTROL 請求屬性]**頁簽。*<br><br>

1. 完成後，在頁面右上角附近選取 **[!UICONTROL 儲存]**.

## 影像伺服器 {#image-server}

「影像伺服器」頁建立從影像伺服器傳送影像的預設設定。 設定分為五個類別

| 發佈內容 | 說明 |
| --- | --- |
| 影像服務 | 指定發佈設定的上下文。 |
| 測試影像服務 | 指定測試發佈設定的上下文。<br>僅限新Dynamic Media帳戶，預設為 **[!UICONTROL 用戶端地址]** 欄位設為 `127.0.0.1` 自動。<br>請參閱 [在將資產公開之前先測試資產](#test-assets-before-making-public). |

### 「安全」頁簽 {#security-tab}

**[!UICONTROL 用戶端地址]**  — 可讓您指定一或多個IP位址或IP位址範圍。 指定後，拒絕對源自未列出IP地址的客戶端的此映像目錄的請求。 此規則同時適用於影像傳送和已轉譯的影像。

### 目錄管理索引標籤 {#catalog-management-tab}

**[!UICONTROL 規則集定義檔案路徑]**  — 指定包含影像目錄規則集定義的檔案。

另請參閱 [RuleSetFile](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile.html) 參數。

>[!NOTE]
>
>如果您的Dynamic Media Classic帳戶已 **[!UICONTROL 規則集定義檔案路徑]** 已選（如設定） **[!UICONTROL 設定]** > **[!UICONTROL 應用程式]** > **[!UICONTROL 發佈設定]**，在 **[!UICONTROL 目錄管理]** 群組)，則您Experience Manager上的Dynamic Media帳戶會從Dynamic Media Classic擷取檔案。 接著，會儲存檔案，並在您開啟 **[!UICONTROL Dynamic Media發佈設定]** 頁面。

### 請求屬性索引標籤 {#request-attributes-tab}

這些設定與影像的預設外觀相關。

| 設定 | 說明 |
| --- | --- |
| **[!UICONTROL 回覆影像大小限制]** | 必要.<br>僅限新Dynamic Media帳戶，預設大小限制會自動設為寬度： `3000` 和高度： `3000` 兩者 **[!UICONTROL 影像提供]** 和 **[!UICONTROL 測試影像提供]**.<br>指定傳回給用戶端的最大回覆影像寬度和高度。 如果請求導致寬度、高度或兩者均大於此設定的回覆影像，則伺服器會傳回錯誤。<br>另請參閱 [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html) 參數。 |
| **[!UICONTROL 要求混淆模式]** | 如果要將base64編碼應用於有效請求，請啟用。<br>另請參閱 [RequestObfuscation](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation.html) 參數。 |
| **[!UICONTROL 要求鎖定模式]** | 如果您想在請求中加入簡單雜湊鎖定，請啟用。<br>另請參閱 [RequestLock](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock.html) 參數。 |
| **[!UICONTROL 預設要求屬性]** |  |
| **[!UICONTROL 預設影像檔案字尾]** | 必要.<br>如果路徑不包含檔案尾碼，則預設資料檔案副檔名附加到目錄路徑和掩碼路徑欄位值。<br>另請參閱 [DefaultExt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext.html) 參數。 |
| **[!UICONTROL 預設字體名稱]** | 指定如果文字層請求未提供字型，則使用的字型。 如果指定，則必須是此影像目錄的字型映射或預設目錄的字型映射中的有效字型名稱值。<br>另請參閱 [DefaultFont](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont.html) 參數。 |
| **[!UICONTROL 預設影像]** | 提供預設影像以回應找不到要求影像的要求。<br>另請參閱 [預設影像](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage.html) 參數。<br>**注意**:如果您的Dynamic Media Classic帳戶已 **[!UICONTROL 預設影像]** 已選（如設定） **[!UICONTROL 設定]** > **[!UICONTROL 應用程式]** > **[!UICONTROL 發佈設定]**，在 **[!UICONTROL 預設請求屬性]** 群組)，則您Experience Manager上的Dynamic Media帳戶會從Dynamic Media Classic擷取檔案。 接著會儲存檔案，並在您開啟 **[!UICONTROL Dynamic Media發佈設定]** 頁面。 |
| **[!UICONTROL 預設影像模式]** | 啟用滑桿方塊時（右側的滑桿）, **[!UICONTROL 預設影像]** 以預設影像替換源影像中的每個缺失層，並照常返回複合。 當滑塊框被禁用時（左側的滑塊），預設影像將替換整個複合影像，即使缺少的影像只是多個圖層中的一個。<br>另請參閱 [DefaultImageMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode.html) 參數。 |
| **[!UICONTROL 預設檢視大小]** | 必要.<br>僅限新Dynamic Media帳戶，預設檢視大小會自動設為寬度： `1280` 和高度： `1280` 兩者 **[!UICONTROL 影像提供]** 和 **[!UICONTROL 測試影像提供]**.<br>如果請求未明確指定檢視大小，則伺服器會限制回覆影像不大於此寬度和高度 `wid=`, `hei=`，或 `scl=`.<br>另請參閱 [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html) 參數。 |
| **[!UICONTROL 預設縮圖大小]** | 必要.<br>使用而非屬性 **[!UICONTROL 預設視圖大小]** 針對縮圖請求(`req=tmb`)。 如果縮圖請求(`req=tmb`)未明確指定大小 `wid=`, `hei=`，或 `scl=`.<br>另請參閱 [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html) 參數。 |
| **[!UICONTROL 預設背景顏色]** | 指定用於填入不包含實際影像資料之回覆影像任何區域的RGB值。<br>另請參閱 [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html) 參數。 |
| **[!UICONTROL JPEG 編碼屬性]** |  |
| **[!UICONTROL 品質]** | <br>指定JPEG回覆影像的預設屬性。<br>僅限新Dynamic Media帳戶， **[!UICONTROL 品質]** 預設值會自動設為 `80` 兩者 **[!UICONTROL 影像提供]** 和 **[!UICONTROL 測試影像提供]**.<br>此欄位的定義範圍為1 - 100。<br>另請參閱 [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html) 參數。 |
| **[!UICONTROL 色度縮減取樣]** | 啟用或停用JPEG編碼器所採用的色彩下採樣。 |
| **[!UICONTROL 預設重新取樣模式]** | 指定用於縮放影像資料的預設重採樣和插值屬性。 使用時機 `resMode` 未在請求中指定。<br>僅適用於新Dynamic Media帳戶，預設的重新取樣模式會自動設為 `Sharp2` 兩者 **[!UICONTROL 影像提供]** 和 **[!UICONTROL 測試影像提供]**.<br>另請參閱 [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html) 參數。 |

### 常見縮圖屬性索引標籤 {#common-thumbnail-attributes-tab}

這些設定與縮圖影像的預設外觀和對齊方式有關。

| 設定 | 說明 |
| --- | --- |
| **[!UICONTROL 縮圖的預設背景顏色]** | 指定用於填充不包含實際影像資料的輸出縮圖影像區域的RGB值。 僅用於縮圖請求(`req=tmb`)和 **[!UICONTROL 預設縮圖類型]** 設定設為 **[!UICONTROL 適合]** 或 **[!UICONTROL 紋理]**.<br>另請參閱 [ThumbBkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor.html) 參數。 |
| **[!UICONTROL 水平對齊方式]** | 指定回復影像矩形中縮圖影像的水準對齊方式，由 `wid=` 和 `hei=` 值。<br>僅用於縮圖請求(`req=tmb`)和 **[!UICONTROL 預設縮圖類型]** 設定設為 **[!UICONTROL 適合]**.<br>有三個水準對齊可供選擇： **[!UICONTROL 中心對齊]**, **[!UICONTROL 左對齊]**，和 **[!UICONTROL 右對齊]**.<br>另請參閱 [ThumbHorizAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign.html) 參數。 |
| **[!UICONTROL 垂直對齊方式]** | 指定回復影像矩形中縮圖影像的垂直對齊方式，由 `wid=` 和 `hei=` 值。 僅用於縮圖請求(`req=tmb`)和 **[!UICONTROL 預設縮圖類型]** 設定設為 **[!UICONTROL 適合]**.<br>有三個垂直對齊可供選擇： **[!UICONTROL 頂端對齊方式]**, **[!UICONTROL 中心對齊]**，和 **[!UICONTROL 底部對齊]**.<br>另請參閱 [ThumbVertAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign.html) 參數。 |
| **[!UICONTROL 預設快取存留時間]** | 提供預設過期時間間隔（小時），以防特定目錄記錄未包含有效的目錄過期值。 設為 `-1` 以標示為永不過期。 <br>另請參閱 [過期](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) 參數。 |
| **[!UICONTROL 預設縮圖類型]** | 提供縮圖類型的預設值，以備特定目錄記錄不包含有效的目錄ThumbType值時使用。 僅用於縮圖請求(`req=tmb`)。<br>有三種縮圖類型可供選擇： **[!UICONTROL 裁切]**, **[!UICONTROL 適合]**，和 **[!UICONTROL 紋理]**.<br>另請參閱 [ThumbType](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype.html) 參數。 |
| **[!UICONTROL 預設縮圖解析度]** | 提供縮圖對象解析的預設值，以備特定目錄記錄不包含有效的目錄ThumbRes值時使用。 僅用於縮圖請求(`req=tmb`)和 **[!UICONTROL 預設縮圖類型]** 設定設為 **[!UICONTROL 紋理]**.<br>另請參閱 [ThumbRes](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres.html) 參數。 |

### 色彩管理屬性索引標籤 {#color-management-attributes-tab}

這些設定確定用於影像的ICC顏色配置檔案。

**色彩轉換演算方式**
顏色轉換呈現意圖允許覆蓋工作配置檔案的預設呈現意圖以確定如何調整源顏色。 用於：

1. 預設的ICC配置檔案之一是顏色轉換的目標顏色空間。
1. 輸出設備（打印機或顯示器）由此配置檔案特徵。
1. 而且，指定的呈現目的對此配置檔案有效。

不同的渲染意圖使用不同的規則來確定如何調整源顏色。

另請參閱 [IccRenderIntent](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html) 參數。

>[!NOTE]
>
>一般而言，最好針對選取的顏色設定使用預設的演算方式，此設定已由Adobe測試，以符合業界標準。 例如，如果您選擇北美或歐洲的色彩設定，預設的色彩轉換演算方式為 **[!UICONTROL 相對比色]**. 如果您選擇日本的顏色設定，預設的顏色轉換呈現方式為 **[!UICONTROL 知覺]**.

| 設定 | 特徵 |
| --- | --- |
| **[!UICONTROL CMYK 預設色彩空間]** | 指定要用作CMYK資料工作配置檔案的ICC顏色配置檔案的名稱。 若 **[!UICONTROL 未指定]** 如果選擇，則當涉及CMYK源影像時，將禁用此影像目錄的顏色管理。 所有CMYK工作空間都取決於設備，這意味著它們基於實際的油墨和紙張組合。 CMYK工作空間Adobe供應基於標準商業打印條件。<br> 另請參閱 [IccProfileCMYK](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html) 參數。 |
| **[!UICONTROL 灰階預設色彩空間]** | 指定要用作灰度資料工作配置檔案的ICC顏色配置檔案的名稱。 若 **[!UICONTROL 未指定]** 選擇，當涉及灰度源影像時，將禁用此影像目錄的顏色管理。<br>另請參閱 [IccProfileGray](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html) 參數。 |
| **[!UICONTROL RGB 預設色彩空間]** | 指定要用作RGB資料工作配置檔案的ICC顏色配置檔案的名稱。 若 **[!UICONTROL 未指定]** 選擇此選項時，當涉及RGB源影像時，將禁用此影像目錄的顏色管理。 總的來說，最好選擇 **[!UICONTROL Adobe RGB]** 或 **[!UICONTROL sRGB]**，而非特定裝置的設定檔（例如監視器設定檔）。 **[!UICONTROL sRGB]** 當您為網頁或行動裝置準備影像時，建議使用，因為它會定義用於在網頁上檢視影像的標準監視器的色彩空間。 **[!UICONTROL sRGB]** 當您使用消費者層級數位相機的影像時，也是不錯的選擇，因為這些相機大多使用sRGB作為預設的色域。<br>另請參閱 [IccProfileRBG](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html) 參數。 |
| **[!UICONTROL 色彩轉換的色彩演算比對方式]** | **[!UICONTROL 知覺]**  — 旨在保持顏色之間的視覺關係，使人眼認為顏色是自然的，即使顏色值本身可能改變。 本目的適用於具有大量色域外顏色的照片影像。 此設定是日本印刷業的標準轉譯目的。 |
|  | **[!UICONTROL 相對比色]**  — 將源顏色空間的極高亮與目標顏色空間的極高亮進行比較，並相應地移動所有顏色。 色域外顏色被移動到目標顏色空間中最接近的可再現顏色。 相對比色保留了影像中更多的原始顏色，而不是感知。 此設定是在北美和歐洲打印的標準渲染意圖。 |
|  | **[!UICONTROL 飽和度]**  — 試圖在影像中生成生動的顏色，但犧牲顏色準確度。 此渲染方式適用於圖形或圖表等商業圖形，其中亮飽和顏色比顏色之間的精確關係更重要。 |
|  | **[!UICONTROL 絕對比色]**  — 保持目標色域內部的顏色不變。 色域外的顏色被剪下。 不執行顏色到目標白點的縮放。 該目的旨在以保持顏色之間關係為代價來保持顏色精度，並且適於校樣以模擬特定設備的輸出。 此目的對於預覽紙張顏色對打印顏色的影響很有用。 |

## 在將資產公開之前先測試資產 {#test-assets-before-making-public}

Secure Testing可幫助您定義安全的測試環境，並基於一組可配置的IP地址和範圍，構建強大的企業對企業解決方案。 此功能可讓您將AdobeDynamic Media部署與內容管理和業務系統的架構搭配使用。

透過安全測試，您可以預覽含有未發佈內容之網站的測試版本。

如果需要，請建立測試環境，而非公開提供資產，原因如下：

* 在公開啟動前預覽網站（測試網站）。
* 提供需要限制存取的資產，例如在B2B Web應用程式中顯示價格的eCatalog。
* 使用防火牆後的資產作為產品資訊管理系統、客戶服務應用程式、培訓網站等的一部分。

>[!NOTE]
>
>安全測試不會影響對Adobe Dynamic Media Classic的存取。 Adobe Dynamic Media Classic安全性仍維持一致，並需有存取Adobe Dynamic Media Classic和相關網站服務的一般認證。

### 安全測試如何運作 {#how-test-assets-works}

大多數公司都把網際網路放在防火牆的後面。 某些路由（通常通過有限的公用IP地址）可以訪問Internet。

從您的公司網路中，您可以使用以下網站來找出您的公開IP位址： [https://www.whatismyip.com](https://www.whatismyip.com/) 或向貴公司的IT組織請求此資訊。

通過安全測試，AdobeDynamic Media為測試環境或內部應用程式建立專用的映像伺服器。 對此伺服器的任何請求都會檢查來源IP位址。 如果傳入的請求不在核准的IP位址清單內，則會傳回失敗回應。 AdobeDynamic Media公司管理員會為其公司的安全測試環境設定已核准的IP位址清單。

由於必須確認原始請求的位置，因此安全測試服務的流量不會經由內容分發網路(如公用Dynamic Media影像伺服器流量)路由。 與公開的Dynamic Media影像伺服器相比，向安全測試服務提出的延遲略高。

取消發佈的資產可立即從安全測試服務取得，而無需發佈。 如此一來，您就可以在資產發佈至其公開的影像伺服器之前，執行預覽。

>[!NOTE]
>
>安全測試服務使用配置了內部發佈上下文的目錄伺服器。 因此，如果貴公司已設定為發佈至Secure Testing,AdobeDynamic Media中任何上傳的資產都會立即在Secure Testing服務上使用。 無論資產是否在上傳時標示為要發佈，此功能都為true。

安全測試服務目前支援下列資產類型和功能：

* 影像.
* 暈映（呈現伺服器請求）。
* 呈現伺服器請求（支援，但必須由客戶明確請求）。
* 集，包括影像集、eCatalog、渲染集和媒體集。
* 標準AdobeDynamic Media多媒體檢視器。
* AdobeDynamic Media OnDemand JSP頁。
* 靜態內容，例如PDF檔案和逐步提供的影片。
* HTTP視訊串流。
* 漸進式視訊串流。

目前不支援下列資產類型和功能：

* Adobe Dynamic Media Classic資訊或eCatalog搜尋
* RTMP視訊串流
* 網路印刷
* UGC（使用者產生的內容）服務

>[!IMPORTANT]
>
>Adobe Dynamic Media中對新或現有UGC向量影像資產的支援已於2021年9月30日終止。

### 測試安全測試服務 {#test-secure-testing-service}

要確保安全測試服務正常工作，請執行以下操作：

#### 準備您的帳戶

1. 請連絡Adobe客戶服務，要求他們在您的帳戶上啟用安全測試。
1. 在Adobe Experience Manager中，選取 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL Dynamic Media發佈設定]**.
1. 在「影像伺服器」頁面上， **[!UICONTROL 發佈內容]** 下拉清單，選擇 **[!UICONTROL 測試影像提供]**.
1. 選取 **[!UICONTROL 安全性]** 標籤。
1. 若 **[!UICONTROL 用戶端地址]** 篩選，選取 **[!UICONTROL 新增]**.
1. 在 **[!UICONTROL IP位址]** 欄位，輸入IP位址。
1. 在 **[!UICONTROL 遮色片]** 欄位，鍵入網路掩碼。

   >[!NOTE]
   >
   >如果添加多個IP地址和網路掩碼，則它實際上允許 *all* 進行資產呼叫的IP位址，都會顯示。

1. 執行下列任一操作：

   * 若要新增更多IP位址，請重複前三個步驟。
   * 繼續下一步。

1. 在「影像伺服器」頁的右上角，選擇 **[!UICONTROL 儲存]**.
1. 上傳所需影像至您的AdobeDynamic Media帳戶。

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. 請確定某些影像已標示為要發佈，而其他影像已取消標示，然後提交發佈工作。

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. 請前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL Dynamic Media一般設定]**.
1. 在 **[!UICONTROL 伺服器]** 頁面，找到右側的伺服器名稱 **[!UICONTROL 已發佈的伺服器名稱]**.

如果伺服器名稱遺失或伺服器的URL無法運作，請聯絡Adobe服務。

#### 準備網站變體

您需要連結已發佈和未發佈資產的網站的兩個變數：

* 公開版本 — 使用傳統AdobeDynamic Media URL語法連結資產。
* 測試版本 — 使用相同語法但使用安全測試網站名稱連結資產。

#### 執行測試

執行下列測試：

1. 檢查公司網路中是否顯示資產。

   從由先前定義的IP位址範圍所識別的公司網路中，網站的測試版本會顯示所有影像，無論是否標示為發佈。 因此，您可以在預覽核准或產品發佈之前，不會意外讓影像可供使用，進行測試。

   確認網站的公開版本顯示先前使用AdobeDynamic Media時所體驗的已發佈資產。

1. 從公司網路外部，確認未發佈的資產（即未標示為發佈）受到保護，不受第三方存取。

   從外部（例如從家用電腦或4G/5G連線）存取您的網路，然後確認網站的公開版本顯示所有已發佈資產，但未顯示任何未發佈的內容。

   確認測試版本不顯示任何資產，因為您是從未核准的IP位址存取安全測試服務。
