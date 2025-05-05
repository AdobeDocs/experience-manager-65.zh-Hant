---
title: 設定影像伺服器的Dynamic Media Publish設定
description: 瞭解如何設定影像伺服器的Dynamic Media Publish設定，以便發佈資產。 您也可以在將資產公開之前先測試資產。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: c86e79c4-e887-4ee3-bb54-eeffb34a33c2
solution: Experience Manager, Experience Manager Assets
source-git-commit: 2b7c8765d4fa6af1d729875a9ec234287ffb088f
workflow-type: tm+mt
source-wordcount: '3368'
ht-degree: 0%

---

# 設定影像伺服器的Dynamic Media Publish設定

只有符合下列條件時，才可使用設定Dynamic Media Publish安裝選項：

* 您正在以Scene7模式執行Dynamic Media。 請參閱[在Scene7模式中啟用Dynamic Media](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode)。
* 您在Adobe Experience Manager 6.5.11或更新版本中有&#x200B;*現有* **[!UICONTROL Dynamic Media設定]** (在&#x200B;**[!UICONTROL 個Cloud Service]**&#x200B;中)。 請參閱[在Cloud Service](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)中建立Dynamic Media設定。
* 您是具有管理員許可權的Experience Manager系統管理員。

經驗豐富的網站開發人員和程式設計人員將使用Dynamic Media Publish設定。 Adobe Dynamic Media建議變更發佈設定的使用者熟悉Adobe Dynamic Media、HTTP通訊協定標準和慣例，以及基本影像處理技術。

Dynamic Media Publish設定頁面會建立預設設定，用來決定如何從AdobeDynamic Media伺服器將資產傳送至網站或應用程式。 如果未指定設定，AdobeDynamic Media伺服器會根據Dynamic Media Publish設定頁面上設定的預設設定傳送資產。

另請參閱[選擇性 — Dynamic Media的設定和組態 — Scene7模式設定](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)，以取得更多選擇性組態工作。

>[!NOTE]
>
>在Adobe Experience Manager上從Dynamic Media Classic升級為Dynamic Media？ Dynamic Media中的[一般設定](/help/assets/dm-general-settings.md)頁面和Publish設定頁面已預先填入從您的Dynamic Media Classic帳戶取得的值。 例外情況是「一般設定」頁面的&#x200B;**[!UICONTROL 預設上傳選項]**&#x200B;區域下列出的所有值。 這些值已在Experience Manager中。 因此，您透過Experience Manager使用者介面在5個標籤中的任一個標籤上，於&#x200B;**[!UICONTROL 預設上傳選項]**&#x200B;下所做的任何變更都會反映在Dynamic Media中，而非Dynamic Media Classic中。 Experience Manager時，[一般設定](/help/assets/dm-general-settings.md)頁面和Publish設定頁面中的所有其他設定和值都會在Dynamic Media Classic和Dynamic Media之間維護。

**若要設定Dynamic Media Publish安裝程式影像伺服器：**

1. 在Experience Manager作者模式中，選取Experience Manager標誌以存取全域導覽主控台。
1. 在左側邊欄中，按一下「工具」圖示，然後前往&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media Publish設定]**。
1. 在「影像伺服器」頁面的下拉式清單中，選擇您的發佈內容，以建立從「影像伺服器」傳送影像的預設設定。

| Publish內容 | 說明 |
| --- | --- |
| 影像服務 | 指定發佈設定的內容。 |
| 測試影像服務 | 指定測試發佈設定的內容。<br>僅針對新的Dynamic Media帳戶，預設&#x200B;**[!UICONTROL 使用者端位址]**&#x200B;欄位會自動設定為`127.0.0.1`。<br>檢視[測試資產，再將其設為公開資產](#test-assets-before-making-public)。 |

1. 使用五個標籤來設定預設的發佈內容設定。

   * [安全性](#security-tab)標籤
   * [目錄管理](#catalog-management-tab)索引標籤
   * [要求屬性](#request-attributes-tab)標籤
   * [通用縮圖屬性](#common-thumbnail-attributes-tab)標籤
   * [色彩管理屬性](#color-management-attributes-tab)標籤

   ![Dynamic Media Publish設定頁面](/help/assets/assets-dm/dm-publish-setup.png)
   *Dynamic Media Publish設定頁面，已選取&#x200B;**[!UICONTROL 要求屬性]**&#x200B;索引標籤。*<br><br>

1. 完成後，在頁面的右上角附近，按一下[儲存]。**&#x200B;**

## 安全性索引標籤 {#security-tab}

>[!NOTE]
>
>*影像伺服*&#x200B;發佈內容不支援安全性設定。

當&#x200B;*測試影像伺服*&#x200B;設定為發佈內容時，您可以設定下列安全性設定：

**[!UICONTROL 使用者端位址]** — 可讓您指定一或多個IP位址或IP位址範圍。 指定後，系統會拒絕從未列出的IP位址之使用者端對此影像目錄提出的要求。 此規則會同時套用至影像傳送和演算後的影像。

![安全性標籤&#x200B;](/help/assets/assets-dm/dm-ipallowlist.png)<br>*顯示IP「允許」欄位的安全性標籤。*

## 目錄管理標籤 {#catalog-management-tab}

**[!UICONTROL 規則集定義檔案路徑]** — 指定包含影像目錄之規則集定義的檔案。

另請參閱Dynamic Media檢視器參考指南中的[RuleSetFile](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile)引數。

>[!NOTE]
>
>如果您的Dynamic Media Classic帳戶已在&#x200B;**[!UICONTROL 設定]** > **[!UICONTROL 應用程式]** > **[!UICONTROL Publish設定]**&#x200B;中選取&#x200B;**[!UICONTROL 規則集定義檔案路徑]**，則Experience Manager會擷取檔案。 您的Dynamic Media帳戶會從Dynamic Media Classic擷取檔案。 當您第一次開啟&#x200B;**[!UICONTROL Dynamic Media Publish設定]**&#x200B;頁面時，就會儲存檔案並在此欄位中使用。

## 要求屬性標籤 {#request-attributes-tab}

這些設定與影像的預設外觀有關。

| 設定 | 說明 |
| --- | --- |
| **[!UICONTROL 回覆影像大小限制]** | 必填。<br>僅針對新的Dynamic Media帳戶，**[!UICONTROL 影像伺服]**&#x200B;和&#x200B;**[!UICONTROL 測試影像伺服]**&#x200B;的預設大小限制都會自動設定為寬度： `3000`和高度： `3000`。<br>指定傳回給使用者端的回覆影像寬度與高度最大值。 如果要求造成回覆影像的寬度或/及高度大於此設定，則伺服器會傳回錯誤。<br>另請參閱Dynamic Media檢視器參考指南中的[MaxPix](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix)引數。 |
| **[!UICONTROL 要求模糊化模式]** | 若要將base64編碼套用至有效的要求，請啟用。<br>另請參閱Dynamic Media檢視器參考指南中的[RequestObfuscation](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation)引數。 |
| **[!UICONTROL 要求鎖定模式]** | 如果您想要在要求中包含簡單的雜湊鎖定，請啟用此選項。<br>另請參閱Dynamic Media檢視器參考指南中的[RequestLock](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock)引數。 |
| **[!UICONTROL 預設要求屬性]** | |
| **[!UICONTROL 預設影像檔案字尾]** | 必填。<br>路徑不包含檔案字尾時，附加至目錄Path和MaskPath欄位值的預設資料檔案副檔名。<br>另請參閱Dynamic Media檢視器參考指南中的[DefaultExt](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext)引數。 |
| **[!UICONTROL 預設字型名稱]** | 指定如果文字圖層要求未提供任何字型，使用何種字型。 如果已指定，它必須是此影像目錄的字型地圖或預設目錄的字型地圖中的有效字型名稱值。<br>另請參閱Dynamic Media檢視器參考指南中的[DefaultFont](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont)引數。 |
| **[!UICONTROL 預設影像]** | 在找不到所要求的影像時，會傳回預設影像以回應要求。<br>另請參閱Dynamic Media檢視器參考指南中的[DefaultImage](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage)引數。<br>**注意**：如果您的Dynamic Media Classic帳戶在&#x200B;**[!UICONTROL 設定]** > **[!UICONTROL 應用程式]** > **[!UICONTROL Publish設定]**&#x200B;下選取了&#x200B;**[!UICONTROL 預設影像]**，在&#x200B;**[!UICONTROL 預設要求屬性]**&#x200B;群組中，Experience Manager會擷取檔案。 當您第一次開啟&#x200B;**[!UICONTROL Dynamic Media Publish設定]**&#x200B;頁面時，就會儲存檔案並在此欄位中使用。 |
| **[!UICONTROL 預設影像模式]** | 啟用滑桿方塊（右側的滑桿）時，**[!UICONTROL 預設影像]**&#x200B;會以預設影像取代來源影像中每個遺失的圖層，並照常傳回複合影像。 停用滑桿方塊（左側的滑桿）時，預設影像會取代整個複合影像，即使遺失的影像隻是數個圖層中的一個圖層亦然。<br>另請參閱Dynamic Media檢視器參考指南中的[DefaultImageMode](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode)引數。 |
| **[!UICONTROL 預設檢視大小]** | 必填。<br>僅針對新的Dynamic Media帳戶，**[!UICONTROL 影像伺服]**&#x200B;和&#x200B;**[!UICONTROL 測試影像伺服]**&#x200B;的預設檢視大小會自動設定為寬度： `1280`和高度： `1280`。<br>如果要求未使用`wid=`、`hei=`或`scl=`明確指定檢視大小，伺服器會將回覆影像限製為不得大於此寬度與高度。<br>另請參閱Dynamic Media檢視器參考指南中的[DefaultPix](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix)引數。 |
| **[!UICONTROL 預設縮圖大小]** | 必填。<br>用於縮圖要求(`req=tmb`)，而非屬性&#x200B;**[!UICONTROL 預設檢視大小]**。 如果縮圖要求(`req=tmb`)未使用`wid=`、`hei=`或`scl=`明確指定大小，伺服器會將回覆影像限製為不得大於此寬度與高度。<br>另請參閱Dynamic Media檢視器參考指南中的[DefaultThumbPix](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix)引數。 |
| **[!UICONTROL 預設背景顏色]** | 指定用於填滿不包含實際影像資料之回覆影像的任何區域的RGB值。<br>另請參閱Dynamic Media檢視器參考指南中的[BkgColor](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor)引數。 |
| **[!UICONTROL JPEG編碼屬性]** |  |
| **[!UICONTROL 品質]** | <br>指定JPEG回覆影像的預設屬性。<br>僅針對新的Dynamic Media帳戶，**[!UICONTROL 影像伺服]**&#x200B;和&#x200B;**[!UICONTROL 測試影像伺服]**&#x200B;的&#x200B;**[!UICONTROL 品質]**&#x200B;預設值會自動設定為`80`。<br>此欄位定義在1到100的範圍內。<br>另請參閱Dynamic Media檢視器參考指南中的[JpegQuality](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality)引數。 |
| **[!UICONTROL 色度縮減取樣]** | 啟用或停用色度縮減取樣，JPEG編碼器會採用此方式。 |
| **[!UICONTROL 預設重新取樣模式]** | 指定用來縮放影像資料的預設重新取樣與內插屬性。 當要求中未指定`resMode`時使用。<br>僅針對新的Dynamic Media帳戶，**[!UICONTROL 影像伺服]**&#x200B;和&#x200B;**[!UICONTROL 測試影像伺服]**&#x200B;的預設重新取樣模式都會自動設定為`Sharp2`。<br>另請參閱Dynamic Media檢視器參考指南中的[ResMode](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode)引數。 |

## 通用縮圖屬性索引標籤 {#common-thumbnail-attributes-tab}

這些設定與縮圖影像的預設外觀和對齊有關。

| 設定 | 說明 |
| --- | --- |
| **[!UICONTROL 縮圖的預設背景顏色]** | 指定用來對不包含實際影像資料的輸出縮圖影像區域進行填色的RGB值。 僅用於縮圖要求(`req=tmb`)以及當&#x200B;**[!UICONTROL 預設縮圖型別]**&#x200B;設定設為&#x200B;**[!UICONTROL 符合]**&#x200B;或&#x200B;**[!UICONTROL 紋理]**&#x200B;時。<br>另請參閱Dynamic Media檢視器參考指南中的[ThumbBkgColor](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor)引數。 |
| **[!UICONTROL 水準對齊]** | 指定回覆影像矩形（由`wid=`和`hei=`值指定）中縮圖影像的水準對齊方式。<br>僅用於縮圖要求(`req=tmb`)以及當&#x200B;**[!UICONTROL 預設縮圖型別]**&#x200B;設定設為&#x200B;**[!UICONTROL 符合]**&#x200B;時。<br>有三個水準對齊可供選擇： **[!UICONTROL 置中對齊]**、**[!UICONTROL 左對齊]**&#x200B;和&#x200B;**[!UICONTROL 右對齊]**。<br>另請參閱Dynamic Media檢視器參考指南中的[ThumbHorizAlign](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign)引數。 |
| **[!UICONTROL 垂直對齊]** | 指定回覆影像矩形（由`wid=`和`hei=`值指定）中縮圖影像的垂直對齊方式。 僅用於縮圖要求(`req=tmb`)以及當&#x200B;**[!UICONTROL 預設縮圖型別]**&#x200B;設定設為&#x200B;**[!UICONTROL 符合]**&#x200B;時。<br>有三個垂直對齊方式可供選擇： **[!UICONTROL 靠上對齊]**、**[!UICONTROL 置中對齊]**&#x200B;以及&#x200B;**[!UICONTROL 靠下對齊]**。<br>另請參閱Dynamic Media檢視器參考指南中的[ThumbVertAlign](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign)引數。 |
| **[!UICONTROL 預設快取存留時間]** | 若特定目錄記錄未包含有效的目錄Expiration值，則會以小時為單位提供預設的到期時間間隔。 設為`-1`以標籤為永不過期。 <br>另請參閱Dynamic Media檢視器參考指南中的[有效期](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration)引數。 |
| **[!UICONTROL 預設縮圖型別]** | 若特定目錄記錄未包含有效的目錄ThumbType值，則會提供縮圖型別的預設值。 僅用於縮圖要求(`req=tmb`)。<br>有三種縮圖型別可供選擇： **[!UICONTROL 裁切]**、**[!UICONTROL 符合]**&#x200B;和&#x200B;**[!UICONTROL 紋理]**。<br>另請參閱Dynamic Media檢視器參考指南中的[ThumbType](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype)引數。 |
| **[!UICONTROL 預設縮圖解析度]** | 如果特定目錄記錄未包含有效的目錄ThumbRes值，則會提供縮圖物件解析度的預設值。 僅用於縮圖要求(`req=tmb`)以及當&#x200B;**[!UICONTROL 預設縮圖型別]**&#x200B;設定設為&#x200B;**[!UICONTROL 紋理]**&#x200B;時。<br>另請參閱Dynamic Media檢視器參考指南中的[ThumbRes](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres)引數。 |

## 色彩管理屬性標籤 {#color-management-attributes-tab}

這些設定會決定影像要使用的ICC色彩設定檔。

**色彩轉換演算色彩比對方式**
色彩轉換演算色彩比對方式允許覆寫使用中設定檔的預設演算色彩比對方式，以決定如何調整來源顏色。 使用時機：

1. 其中一個預設ICC設定檔是色彩轉換的目標色域。
1. 此描述檔描述輸出裝置，例如印表機或熒幕。
1. 而且，指定的演算色彩比對方式對此設定檔有效。

不同的演算意圖會使用不同的規則來決定如何調整來源顏色。

另請參閱Dynamic Media檢視器參考指南中的[IccRenderIntent](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent)引數。

>[!NOTE]
>
>一般而言，會針對選取的顏色設定使用預設的色彩演算比對方式，Adobe已經過測試以符合業界標準。 例如，如果您選擇北美或歐洲的色彩設定，預設的色彩轉換色彩比對方式為&#x200B;**[!UICONTROL 相對比色]**。 如果您選擇日本的色彩設定，預設的色彩轉換演算色彩比對方式為&#x200B;**[!UICONTROL 感應式]**。

| 設定 | 特性 |
| --- | --- |
| **[!UICONTROL CMYK預設色域]** | 指定要用作CMYK資料使用中之設定檔的ICC色彩設定檔名稱。 如果選擇&#x200B;**[!UICONTROL 未指定]**，則在涉及CMYK來源影像時，將停用此影像目錄的色彩管理。 所有CMYK工作空間都依裝置而定，表示它們是以實際的油墨和紙張組合為基礎。 CMYK工作區Adobe供應品是以標準商業列印條件為基礎。<br>另請參閱Dynamic Media檢視器參考指南中的[IccProfileCMYK](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk)引數。 |
| **[!UICONTROL 灰階預設色彩空間]** | 指定用作灰階資料使用中描述檔的ICC色彩描述檔名稱。 如果選擇&#x200B;**[!UICONTROL 未指定]**，則在涉及灰階來源影像時，將停用此影像目錄的色彩管理。<br>另請參閱Dynamic Media檢視器參考指南中的[IccProfileGray](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray)引數。 |
| **[!UICONTROL RGB預設色域]** | 指定要用作RGB資料使用中之設定檔的ICC色彩設定檔名稱。 如果選擇&#x200B;**[!UICONTROL 未指定]**，則在涉及RGB來源影像時停用此影像目錄的色彩管理。 一般來說，最好選擇&#x200B;**[!UICONTROL Adobe RGB]**&#x200B;或&#x200B;**[!UICONTROL sRGB]**，而不是特定裝置的設定檔（例如監視器設定檔）。 當您準備網頁或行動裝置的影像時，建議使用&#x200B;**[!UICONTROL sRGB]**，因為它定義了用來在網頁上檢視影像的標準監視器的色域。 當您處理消費者等級的數位相機影像時，**[!UICONTROL sRGB]**&#x200B;也是很好的選擇，因為這些相機大多使用sRGB做為預設色域。<br>另請參閱Dynamic Media檢視器參考指南中的[IccProfileRBG](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb)引數。 |
| **[!UICONTROL 色彩轉換演算色彩比對方式]** | **[!UICONTROL 可感知]** — 旨在保留色彩間的視覺關係，即使色彩值本身可能會變更，也能讓人眼感覺自然。 此意圖適用於具有大量超出色域顏色的攝影影像。 此設定是日本印刷業的標準色彩演算比對方式。 |
|  | **[!UICONTROL 相對色度]** — 比較來源色域和目的地色域的極端亮部並相應地移動所有顏色。 超出色域的顏色會移至目標色域中最接近的可複製顏色。 「相對比色」保留影像中比「感應式」更多的原始顏色。 此設定是北美及歐洲列印的標準色彩演算比對方式。 |
|  | **[!UICONTROL 飽和度]** — 嘗試在影像中產生生動的色彩，但犧牲色彩精確度。 此演算色彩比對方式適用於圖形或圖表等商業圖形，其中明亮飽和色彩比色彩之間的確切關係更重要。 |
|  | **[!UICONTROL 絕對比色]** — 讓落在目的地色域內的顏色不變。 超出色域的顏色會被剪裁。 不會執行將顏色縮放到目標白點的動作。 此意圖旨在維持色彩的精確性，但會犧牲色彩間的關聯性，並適合用來模擬特定裝置輸出的校樣。 此意圖對於預覽紙張顏色對列印顏色的影響非常有用。 |

## 在公開資產之前先測試資產 {#test-assets-before-making-public}

Secure Testing可協助您定義安全的測試環境，並根據可設定的IP位址和範圍組合，建立健全的企業對企業解決方案。 此功能可讓您將AdobeDynamic Media部署與內容管理和業務系統的架構搭配起來。

使用Secure Testing，您可以預覽包含未發佈內容的網站測試版本。

如有需要，請建立測試環境，而非讓資產公開可用，理由如下：

* 在公開啟動前預覽網站（測試網站）。
* 提供需要限制存取的資產，例如在B2B Web應用程式中顯示價格的eCatalog。
* 在防火牆後面使用資產，做為產品資訊管理系統、客戶服務應用程式、訓練網站等的一部分。

>[!NOTE]
>
>安全測試不會影響對Adobe Dynamic Media Classic的存取。 Adobe Dynamic Media Classic安全性會保持一致，且需要一般憑證才能存取Adobe Dynamic Media Classic及相關網路服務。

### 安全測試的運作方式 {#how-test-assets-works}

大部分企業都透過防火牆執行網際網路。 網際網路存取可透過特定路由進行，通常透過有限的公用IP位址範圍進行。

透過您的公司網路，您可以使用[https://www.whatismyip.com](https://www.whatismyip.com/)之類的網站來找出您的公用IP位址，或向您的公司IT組織要求此資訊。

透過安全測試，Adobe Dynamic Media可為中繼環境或內部應用程式建立專用的影像伺服器。 對此伺服器的任何請求都會檢查原始IP位址。 如果傳入的請求不在核准的IP位址清單中，則會傳回失敗回應。 AdobeDynamic Media公司管理員會為公司的安全測試環境設定已核准的IP位址清單。

由於原始請求的位置必須確認，因此Secure Testing Service的流量不會透過內容發佈網路(例如公用Dynamic Media影像伺服器流量)進行路由。 向安全測試服務提出的請求與公開Dynamic Media影像伺服器的請求相比，延遲時間稍微長一些。

未發佈的資產可立即從Secure Testing Services取得，而不需要發佈。 透過這種方式，您可以在資產發佈到公開顯示的影像伺服器之前執行預覽。

>[!NOTE]
>
>Secure Testing Services會使用已設定內部發佈內容的目錄伺服器。 因此，如果您的公司設定為發佈至Secure Testing，則Adobe Dynamic Media中上傳的任何資產均可在Secure Testing服務中立即使用。 不論資產是否標示為上傳時發佈，此功能皆為true。

Secure Testing服務目前支援下列資產型別和功能：

* 影像。
* 暈映（轉譯器伺服器請求）。
* 客戶必須明確要求可用的Render Server支援。
* 集，包括影像集、eCatalog、演算集和媒體集。
* 標準AdobeDynamic Media多媒體檢視器。
* AdobeDynamic Media OnDemand JSP頁面。
* 靜態內容，例如PDF檔案和逐步提供的視訊。
* HTTP視訊串流。
* 漸進式視訊串流。

目前不支援下列資產型別和功能：

* Adobe Dynamic Media Classic資訊或eCatalog搜尋
* RTMP視訊串流
* 網頁列印
* UGC （使用者產生的內容）服務

  >[!IMPORTANT]
  >
  >自2023年5月1日起，Dynamic Media中的UGC資產最多可在上傳日期起的60天內使用。 60天後，資產會移除。

  >[!NOTE]
  >
  >Adobe Dynamic Media已於2021年9月30日停止支援新的或現有的UGC向量影像資產。

### 測試Secure Testing service {#test-secure-testing-service}

若要確保Secure Testing服務如預期般運作，請執行下列動作：

#### 準備您的帳戶

1. 請聯絡Adobe客戶服務，要求他們啟用您帳戶的安全測試。
1. 在Adobe Experience Manager中，選取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media Publish安裝程式]**。
1. 在「影像伺服器」頁面的&#x200B;**[!UICONTROL Publish內容]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL 測試影像伺服]**。
1. 選取&#x200B;**[!UICONTROL 安全性]**&#x200B;標籤。
1. 對於&#x200B;**[!UICONTROL 使用者端位址]**&#x200B;篩選器，請選取&#x200B;**[!UICONTROL 新增]**。
1. 在&#x200B;**[!UICONTROL IP位址]**&#x200B;欄位中，輸入IP位址。
1. 在&#x200B;**[!UICONTROL 遮罩]**&#x200B;欄位中輸入網路遮罩。

   >[!NOTE]
   >
   >如果您新增一個以上的IP位址和網路遮罩，它就會有效地允許&#x200B;*所有*&#x200B;個IP位址進行資產呼叫，而且這些位址都會顯示。

1. 執行下列任一項作業：

   * 若要新增更多IP位址，請重複前三個步驟。
   * 繼續下一個步驟。

1. 在「影像伺服器」頁面的右上角，選取&#x200B;**[!UICONTROL 儲存]**。
1. 將所需的影像上傳至您的AdobeDynamic Media帳戶。

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. 確定部分影像已標示為發佈，其他影像已取消標籤，然後提交發佈工作。

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. 請前往&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media一般設定]**，決定您的Secure Testing服務名稱。
1. 在&#x200B;**[!UICONTROL 伺服器]**&#x200B;頁面上，尋找&#x200B;**[!UICONTROL 已發佈的伺服器名稱]**&#x200B;右側的伺服器名稱。

如果伺服器名稱遺失或伺服器的URL無法運作，請聯絡Adobe服務。

#### 準備網站變體

您需要連結已發佈和未發佈資產的兩種網站變體：

* 公開版本 — 使用傳統AdobeDynamic Media URL語法連結資產。
* 測試版本 — 使用相同語法但具有安全測試網站名稱的連結資產。

#### 執行測試

執行下列測試：

1. 檢查資產是否可從您的公司網路中看見。

   從先前定義的IP位址範圍所識別的公司網路中，網站的測試版本會顯示所有影像，無論是否標示為發佈。 因此，在預覽核准或產品上市之前，您可以進行測試而不會意外讓影像可供使用。

   確認您的網站公開版本會顯示已發佈的資產，例如先前在AdobeDynamic Media時所體驗的資產。

1. 在公司網路外部，確認未發佈的資產（即未標示為發佈）受到保護，不會受到第三方存取。

   從外部存取您的網路（例如從您的家用電腦或透過4G/5G連線），然後確認網站的公開版本顯示所有已發佈的資產，但不顯示任何未發佈的內容。

   確認測試版本未顯示任何資產，因為您正從未核准的IP位址存取Secure Testing服務。
