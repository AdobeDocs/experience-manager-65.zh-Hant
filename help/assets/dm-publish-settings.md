---
title: 為映像伺服器配置Dynamic Media發佈設定
description: 瞭解如何在Dynamic Media設定Publishing。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: c86e79c4-e887-4ee3-bb54-eeffb34a33c2
source-git-commit: 8561eb8b4b5164188ebf387c8f0344b462b830ec
workflow-type: tm+mt
source-wordcount: '3467'
ht-degree: 2%

---

# 為映像伺服器配置Dynamic Media發佈設定

配置Dynamic Media發佈設定僅在以下情況下可用：

* 您以Scene7模式運行Dynamic Media。 請參閱 [在Scene7模式下啟用Dynamic Media](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode)。
* 你有 *現有* **[!UICONTROL Dynamic Media配置]** (在 **[!UICONTROL Cloud Services]**)，在Adobe Experience Manager6.5.11或更高版本。 請參閱 [在Cloud Services中建立Dynamic Media配置](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)。
* 您是具有管理員權限的Experience Manager系統管理員。

Dynamic Media發佈安裝程式僅供經驗豐富的網站開發人員和程式設計師使用。 Adobe·Dynamic Media建議更改這些發佈設定的用戶熟悉AdobeDynamic Media、HTTP協定標準和慣例以及基本成像技術。

「Dynamic Media發佈設定」頁建立預設設定，確定如何將資產從AdobeDynamic Media伺服器傳送到網站或應用程式。 如果未指定任何設定，AdobeDynamic Media伺服器將根據在Dynamic Media發佈設定頁面上配置的預設設定來傳遞資產。

另請參閱 [可選 — Dynamic Media-Scene7模式設定的設定和配置](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings) 的子菜單。

>[!NOTE]
>
>從Dynamic Media Classic升級到Adobe Experience ManagerDynamic Media? 的 [常規設定](/help/assets/dm-general-settings.md) 頁面和「發佈設定」頁面在Dynamic Media預填充了從您的Dynamic Media Classic帳戶獲取的值。 例外是列在 **[!UICONTROL 預設上載選項]** 的子菜單。 這些值已經處於Experience Manager。 因此，您在 **[!UICONTROL 預設上載選項]**，通過Experience Manager用戶介面，在五個頁籤中的任何一個頁籤上都反映在Dynamic Media，而不是Dynamic Media Classic。 中的所有其他設定和值 [常規設定](/help/assets/dm-general-settings.md) 頁面和「發佈設定」頁面將在Dynamic Media Classic和Dynamic Media之間Experience Manager。

**配置Dynamic Media發佈設定映像伺服器：**

1. 在「Experience Manager作者」模式下，選擇Experience Manager徽標以訪問全局導航控制台。
1. 在左滑軌中，選擇「工具」表徵圖，然後轉到 **[!UICONTROL 資產]** > **[!UICONTROL Dynamic Media發佈設定]**。
1. 在「影像伺服器」頁中，設定「影像伺服器 — 發佈」上下文，然後使用五個頁籤配置預設發佈設定。

   * [影像伺服器](#image-server)
   * [安全](#security-tab) 頁籤
   * [目錄管理](#catalog-management-tab) 頁籤
   * [請求屬性](#request-attributes-tab) 頁籤
   * [常用縮略圖屬性](#common-thumbnail-attributes-tab) 頁籤
   * [顏色管理屬性](#color-management-attributes-tab) 頁籤

   ![Dynamic Media發佈設定頁面](/help/assets/assets-dm/dm-publish-setup.png)
   *Dynamic Media發佈設定頁面，**[!UICONTROL 請求屬性]**的子菜單。*<br><br>

1. 完成後，在頁面右上角附近，選擇 **[!UICONTROL 保存]**。

## 影像伺服器 {#image-server}

「映像伺服器」頁為從映像伺服器傳送映像建立預設設定。 設定有五個類別

| 發佈內容 | 說明 |
| --- | --- |
| 影像服務 | 指定發佈設定的上下文。 |
| 測試影像服務 | 指定測試發佈設定的上下文。<br>僅對新Dynamic Media帳戶，預設 **[!UICONTROL 客戶端地址]** 欄位設定為 `127.0.0.1` 的下界。<br>請參閱 [Test資產，然後再公開](#test-assets-before-making-public)。 |

### 「安全」頁籤 {#security-tab}

**[!UICONTROL 客戶端地址]**  — 用於指定一個或多個IP地址或IP地址範圍。 如果指定，則拒絕從未列出IP地址的客戶端發出的對此映像目錄的請求。 此規則既適用於影像的傳遞，也適用於渲染的影像。

![「安全」頁籤&#x200B;](/help/assets/assets-dm/dm-ipallowlist.png)<br>*顯示IP「允許」欄位的安全頁籤。*

### 目錄管理頁籤 {#catalog-management-tab}

**[!UICONTROL 規則集定義檔案路徑]**  — 指定包含映像目錄的規則集定義的檔案。

另請參閱 [規則集檔案](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile.html) 參數。

>[!NOTE]
>
>如果你的Dynamic Media Classic帳戶 **[!UICONTROL 規則集定義檔案路徑]** 選定(如 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式]** > **[!UICONTROL 發佈設定]**&#x200B;下 **[!UICONTROL 目錄管理]** 組)，您的Dynamic MediaExperience Manager帳戶從Dynamic Media Classic提取檔案。 然後，在開啟 **[!UICONTROL Dynamic Media發佈設定]** 的雙曲餘切值。

### 「請求屬性」頁籤 {#request-attributes-tab}

這些設定與影像的預設外觀有關。

| 設定 | 說明 |
| --- | --- |
| **[!UICONTROL 回覆影像大小限制]** | 必要.<br>僅對於新Dynamic Media帳戶，預設大小限制將自動設定為寬度： `3000` 和高度： `3000` 兩者 **[!UICONTROL 影像服務]** 和 **[!UICONTROL Test影像服務]**。<br>指定返回給客戶端的最大回復影像寬度和高度。 如果請求導致寬度、高度或兩者均大於此設定的應答影像，則伺服器會返回錯誤。<br>另請參閱 [最大圖](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html) 參數。 |
| **[!UICONTROL 要求混淆模式]** | 如果希望將base64編碼應用於有效請求，則啟用。<br>另請參閱 [請求模糊處理](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation.html) 參數。 |
| **[!UICONTROL 要求鎖定模式]** | 如果希望請求中包含簡單的哈希鎖，則啟用。<br>另請參閱 [請求鎖](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock.html) 參數。 |
| **[!UICONTROL 預設要求屬性]** |  |
| **[!UICONTROL 預設影像檔案字尾]** | 必要.<br>如果路徑不包括檔案尾碼，則附加到目錄Path和MaskPath欄位值的預設資料檔案副檔名。<br>另請參閱 [預設分機](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext.html) 參數。 |
| **[!UICONTROL 預設字體名稱]** | 指定如果文本圖層請求未提供字型，則使用哪種字型。 如果指定，則必須是此影像目錄的字型映射或預設目錄的字型映射中的有效字型名稱值。<br>另請參閱 [預設字型](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont.html) 參數。 |
| **[!UICONTROL 預設影像]** | 提供預設映像以響應找不到請求映像的請求返回。<br>另請參閱 [預設影像](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage.html) 參數。<br>**注釋**:如果你的Dynamic Media Classic帳戶 **[!UICONTROL 預設影像]** 選定(如 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式]** > **[!UICONTROL 發佈設定]**&#x200B;下 **[!UICONTROL 預設請求屬性]** 組)，您的Dynamic MediaExperience Manager帳戶從Dynamic Media Classic提取檔案。 然後，在開啟 **[!UICONTROL Dynamic Media發佈設定]** 的雙曲餘切值。 |
| **[!UICONTROL 預設影像模式]** | 啟用滑塊框（右側的滑塊）時， **[!UICONTROL 預設影像]** 用預設影像替換源影像中的每個缺失圖層，並像往常一樣返回複合影像。 禁用滑塊框（左側的滑塊）時，預設影像將替換整個複合影像，即使缺少的影像只是幾個圖層中的一個。<br>另請參閱 [預設影像模式](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode.html) 參數。 |
| **[!UICONTROL 預設檢視大小]** | 必要.<br>僅對於新Dynamic Media帳戶，預設視圖大小將自動設定為「寬度： `1280` 和高度： `1280` 兩者 **[!UICONTROL 影像服務]** 和 **[!UICONTROL Test影像服務]**。<br>如果請求未使用顯式指定視圖大小，則伺服器將回復影像限制為不大於此寬度和高度 `wid=`。 `hei=`或 `scl=`。<br>另請參閱 [預設影像](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html) 參數。 |
| **[!UICONTROL 預設縮圖大小]** | 必要.<br>已使用而不是屬性 **[!UICONTROL 預設視圖大小]** 對於縮略圖請求(`req=tmb`)。 如果縮略圖請求(`req=tmb`)不顯式指定大小 `wid=`。 `hei=`或 `scl=`。<br>另請參閱 [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html) 參數。 |
| **[!UICONTROL 預設背景顏色]** | 指定用於填充不包含實際影像資料的回復影像任何區域的RGB值。<br>另請參閱 [Bkg顏色](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html) 參數。 |
| **[!UICONTROL JPEG 編碼屬性]** |  |
| **[!UICONTROL 品質]** | <br>指定JPEG回復影像的預設屬性。<br>僅對新Dynamic Media帳戶， **[!UICONTROL 質量]** 預設值自動設定為 `80` 兩者 **[!UICONTROL 影像服務]** 和 **[!UICONTROL Test影像服務]**。<br>此欄位在1 - 100範圍內定義。<br>另請參閱 [Jpeg質量](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html) 參數。 |
| **[!UICONTROL 色度縮減取樣]** | 啟用或禁用由JPEG編碼器使用的色下採樣。 |
| **[!UICONTROL 預設重新取樣模式]** | 指定用於縮放影像資料的預設重採樣和插值屬性。 使用時間 `resMode` 未在請求中指定。<br>僅對於新Dynamic Media帳戶，預設重採樣模式將自動設定為 `Sharp2` 兩者 **[!UICONTROL 影像服務]** 和 **[!UICONTROL Test影像服務]**。<br>另請參閱 [Res模式](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html) 參數。 |

### 「通用縮略圖屬性」頁籤 {#common-thumbnail-attributes-tab}

這些設定與縮略圖的預設外觀和對齊方式有關。

| 設定 | 說明 |
| --- | --- |
| **[!UICONTROL 縮圖的預設背景顏色]** | 指定用於填充不包含實際影像資料的輸出縮略圖影像的RGB值。 僅用於縮略圖請求(`req=tmb`)和 **[!UICONTROL 預設縮略圖類型]** 設定設定為 **[!UICONTROL 適合]** 或 **[!UICONTROL 紋理]**。<br>另請參閱 [拇指Bkg顏色](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor.html) 參數。 |
| **[!UICONTROL 水平對齊方式]** | 指定由指定的回復影像矩形中縮略圖的水準對齊方式 `wid=` 和 `hei=` 值。<br>僅用於縮略圖請求(`req=tmb`)和 **[!UICONTROL 預設縮略圖類型]** 設定設定為 **[!UICONTROL 適合]**。<br>有三個水準對齊可供選擇： **[!UICONTROL 居中對齊]**。 **[!UICONTROL 左對齊]**, **[!UICONTROL 右對齊]**。<br>另請參閱 [拇指對齊](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign.html) 參數。 |
| **[!UICONTROL 垂直對齊方式]** | 指定由指定的回復影像矩形中縮略圖的垂直對齊方式 `wid=` 和 `hei=` 值。 僅用於縮略圖請求(`req=tmb`)和 **[!UICONTROL 預設縮略圖類型]** 設定設定為 **[!UICONTROL 適合]**。<br>有三個垂直對齊可供選擇： **[!UICONTROL 頂部對齊]**。 **[!UICONTROL 居中對齊]**, **[!UICONTROL 底部對齊]**。<br>另請參閱 [拇指垂直對齊](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign.html) 參數。 |
| **[!UICONTROL 預設快取存留時間]** | 在特定目錄記錄未包含有效的目錄到期值時，提供預設到期間隔（以小時為單位）。 設定為 `-1` 標籤為永不過期。 <br>另請參閱 [到期](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) 參數。 |
| **[!UICONTROL 預設縮圖類型]** | 如果特定目錄記錄不包含有效的目錄ThumbType值，則為縮略圖類型提供預設值。 僅用於縮略圖請求(`req=tmb`)。<br>有三種縮略圖類型可供選擇： **[!UICONTROL 裁剪]**。 **[!UICONTROL 適合]**, **[!UICONTROL 紋理]**。<br>另請參閱 [ThumbType](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype.html) 參數。 |
| **[!UICONTROL 預設縮圖解析度]** | 提供縮略圖對象解析的預設值，以防特定目錄記錄不包含有效的目錄ThumbRes值。 僅用於縮略圖請求(`req=tmb`)和 **[!UICONTROL 預設縮略圖類型]** 設定設定為 **[!UICONTROL 紋理]**。<br>另請參閱 [拇指](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres.html) 參數。 |

### 「顏色管理屬性」頁籤 {#color-management-attributes-tab}

這些設定確定哪些ICC顏色配置檔案用於影像。

**顏色轉換渲染意圖**
顏色轉換繪製意圖允許覆蓋工作輪廓的預設繪製意圖以確定如何調整源顏色。 使用時間：

1. 預設的ICC配置檔案之一是顏色轉換的目標顏色空間。
1. 輸出設備（打印機或監視器）的特徵是此配置檔案。
1. 而且，指定的渲染意圖對此配置檔案有效。

不同的渲染方式使用不同的規則來確定如何調整源顏色。

另請參閱 [IccRenderIntent](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html) 參數。

>[!NOTE]
>
>通常，最好使用所選顏色設定的預設渲染方法，該設定已通過Adobe測試以符合行業標準。 例如，如果為北美或歐洲選擇顏色設定，則預設顏色轉換呈現方式為 **[!UICONTROL 相對比色]**。 如果為日本選擇顏色設定，則預設顏色轉換渲染方法為 **[!UICONTROL 感知]**。

| 設定 | 特徵 |
| --- | --- |
| **[!UICONTROL CMYK 預設色彩空間]** | 指定用作CMYK資料工作配置檔案的ICC顏色配置檔案的名稱。 如果 **[!UICONTROL 未指定]** 選擇後，當涉及CMYK源影像時，將禁用此影像目錄的顏色管理。 所有CMYK工作空間都與設備相關，這意味著它們基於實際的油墨和紙張組合。 CMYK工作空間Adobe供應基於標準商業印刷條件。<br> 另請參閱 [IccProfileCMYK](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html) 參數。 |
| **[!UICONTROL 灰階預設色彩空間]** | 指定用作灰度資料工作配置檔案的ICC顏色配置檔案的名稱。 如果 **[!UICONTROL 未指定]** 如果選擇，則當涉及灰度級源影像時，將禁用此影像目錄的顏色管理。<br>另請參閱 [Icc配置檔案灰色](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html) 參數。 |
| **[!UICONTROL RGB 預設色彩空間]** | 指定用作RGB資料的工作配置檔案的ICC顏色配置檔案的名稱。 如果 **[!UICONTROL 未指定]** 選中此選項後，當涉及RGB源影像時，將禁用此影像目錄的顏色管理。 總的來說，最好選擇 **[!UICONTROL Adobe RGB]** 或 **[!UICONTROL sRGB]**，而不是特定設備的配置檔案（如監視器配置檔案）。 **[!UICONTROL sRGB]** 建議在為web或移動設備準備影像時使用，因為它定義了用於查看web上影像的標準監視器的顏色空間。 **[!UICONTROL sRGB]** 在處理來自消費者級數位相機的影像時，這也是一個不錯的選擇，因為這些相機中的大多數都使用sRGB作為預設顏色空間。<br>另請參閱 [IccProfileRBG](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html) 參數。 |
| **[!UICONTROL 色彩轉換的色彩演算比對方式]** | **[!UICONTROL 感知]**  — 旨在保持顏色之間的視覺關係，使其在人眼中被視為自然，即使顏色值本身可能發生變化。 本發明適用於具有大量色域外色彩的攝影影像。 此設定是日本印刷行業的標準繪製意圖。 |
|  | **[!UICONTROL 相對比色]**  — 將源顏色空間的極端突出顯示與目標顏色空間的極端突出顯示進行比較，並相應地移動所有顏色。 將色域外的顏色移位到目標顏色空間中最接近的可再現顏色。 相對比色比感知保留影像中更多的原始顏色。 此設定是北美和歐洲打印的標準繪製意圖。 |
|  | **[!UICONTROL 飽和度]**  — 嘗試在影像中生成生動的顏色，而犧牲顏色精度。 此繪製意圖適用於圖形或圖表等商業圖形，其中明亮的飽和色比顏色之間的精確關係更為重要。 |
|  | **[!UICONTROL 絕對比色]**  — 保持目標色域內的顏色不變。 色域外顏色被剪輯。 不執行顏色到目標白點的縮放。 本發明旨在以保持顏色之間的關係為代價來保持顏色精度，並且適於校對以模擬特定設備的輸出。 此方法對於預覽紙張顏色如何影響打印顏色非常有用。 |

## Test資產，然後再公開 {#test-assets-before-making-public}

安全測試可幫助您定義安全的test環境，並基於一組可配置的IP地址和範圍構建強健的企業對企業解決方案。 此功能使您能夠將您的AdobeDynamic Media部署與內容管理和業務系統的體系結構相匹配。

使用安全測試，您可以預覽包含未發佈內容的網站的暫存版本。

如果需要，請建立轉移環境，而不是使資產公開可用，原因如下：

* 在公開啟動前預覽網站（暫存網站）。
* 為需要限制訪問的資產提供服務，例如在B2B Web應用程式中顯示價格的eCatalog。
* 使用防火牆後的資產作為產品資訊管理系統、客戶服務應用程式、培訓站點等的一部分。

>[!NOTE]
>
>安全測試不影響訪問Adobe Dynamic Media Classic。 Adobe Dynamic Media Classic安全保持一致，需要通常的證書才能訪問Adobe Dynamic Media Classic和相關網路服務。

### 安全測試的工作原理 {#how-test-assets-works}

大多數公司都把網際網路置於防火牆之下。 通過某些路由（通常通過有限範圍的公有IP地址）訪問Internet是可能的。

從公司網路中，您可以使用網站(如 [https://www.whatismyip.com](https://www.whatismyip.com/) 或從您的公司IT部門請求此資訊。

通過安全測試，AdobeDynamic Media為臨時環境或內部應用程式建立了專用的映像伺服器。 對此伺服器的任何請求都檢查源IP地址。 如果傳入請求不在批准的IP地址清單中，則返回失敗響應。 AdobeDynamic Media公司管理員為其公司的安全測試環境配置批准的IP地址清單。

因為必須確認原始請求的位置，所以安全測試服務的流量不會通過內容分發網路(如公共Dynamic Media映像伺服器流量)路由。 與公有的Dynamic Media映像伺服器相比，請求安全測試服務的延遲稍高一些。

未發佈的資產可立即從安全測試服務獲得，而無需發佈。 這樣，您就可以在資產發佈到面向公共的影像伺服器之前運行預覽。

>[!NOTE]
>
>安全測試服務使用配置了內部發佈上下文的目錄伺服器。 因此，如果您的公司配置為發佈到安全測試，則Dynamic MediaAdobe中所有上載的資產都可立即在安全測試服務上使用。 無論資產是否標籤為在上載時發佈，此功能均為true。

安全測試服務當前支援以下資產類型和功能：

* 影像.
* Vignettes（Render Server請求）。
* 呈現伺服器請求（支援，但必須由客戶明確請求）。
* 集，包括映像集、eCatalog、呈現集和媒體集。
* 標準AdobeDynamic Media富媒體觀眾。
* AdobeDynamic MediaOnDemand JSP頁。
* 靜態內容，如PDF檔案和逐步提供的視頻。
* HTTP視頻流。
* 逐行視頻流。

當前不支援以下資產類型和功能：

* Adobe Dynamic Media Classic資訊或電子目錄搜索
* RTMP視頻流
* Web到打印
* UGC（用戶生成的內容）服務

>[!IMPORTANT]
>
>2021年9月30日結束了對Dynamic MediaAdobe新的或現有的UGC向量影像資產的支援。

### Test安全測試服務 {#test-secure-testing-service}

要確保安全測試服務按預期工作，請執行以下操作：

#### 準備帳戶

1. 聯繫Adobe客戶關懷，並請求他們在您的帳戶上啟用安全測試。
1. 在Adobe Experience Manager，選擇 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL Dynamic Media發佈設定]**。
1. 在「映像伺服器」頁上， **[!UICONTROL 發佈上下文]** 下拉清單，選擇 **[!UICONTROL Test影像服務]**。
1. 選擇 **[!UICONTROL 安全]** 頁籤。
1. 對於 **[!UICONTROL 客戶端地址]** 選擇 **[!UICONTROL 添加]**。
1. 在 **[!UICONTROL IP地址]** 鍵入IP地址。
1. 在 **[!UICONTROL 蒙版]** 欄位中鍵入網掩碼。

   >[!NOTE]
   >
   >如果您添加了多個IP地址和網路掩碼，它實際上允許 *全部* IP地址進行資產調用，所有地址都顯示出來。

1. 執行下列操作之一：

   * 要添加更多IP地址，請重複前三步。
   * 繼續下一步。

1. 在「影像伺服器」頁的右上角，選擇 **[!UICONTROL 保存]**。
1. 將所需映像上載到您的AdobeDynamic Media帳戶。

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. 確保某些影像已標籤為要發佈，而其他影像未標籤，然後提交發佈作業。

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. 通過轉到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL Dynamic Media總體設定]**。
1. 在 **[!UICONTROL 伺服器]** 頁，查找伺服器名稱，位於 **[!UICONTROL 已發佈伺服器名稱]**。

聯繫Adobe如果伺服器名稱缺失或伺服器的URL無效，請小心。

#### 準備網站變體

您需要兩個網站變體來連結已發佈和未發佈的資產：

* 公共版本 — 使用傳統AdobeDynamic MediaURL語法連結資產。
* 臨時版本 — 使用相同語法但使用安全測試站點名稱連結資產。

#### 運行test

執行以下test:

1. 檢查資產是否可從公司網路中看到。

   從由先前定義的IP地址範圍標識的公司網路中，網站的暫存版本顯示所有影像，無論是否標籤為發佈。 因此，您可以在預覽批准或產品發佈前不意外地使影像可用，而進行test。

   確認您的網站的公共版本顯示已發佈的資產，如以前與AdobeDynamic Media所經歷的那樣。

1. 從公司網路外部驗證未發佈的資產（即未標籤為發佈）是否受到第三方訪問的保護。

   從外部（如從家庭電腦或通過4G/5G連接）訪問您的網路，然後驗證網站的公共版本是否顯示所有已發佈的資產，但不顯示任何未發佈的內容。

   確認轉移版本不顯示任何資產，因為您正在從未批准的IP地址訪問安全測試服務。
