---
title: 智慧型影像
description: 智慧影像處理會套用每個使用者的獨特檢視特性，自動提供針對其體驗最佳化的適當影像，進而提供更出色的效能和參與度。
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
feature: Asset Management,Renditions
role: User, Admin
exl-id: e427d4ee-d5c8-421b-9739-f3cf2de36e41
source-git-commit: 164b3745c5bddf6ec77f9ac2ada19cfa10c6d266
workflow-type: tm+mt
source-wordcount: '3624'
ht-degree: 1%

---

# 智慧型影像 {#smart-imaging}

## 什麼是「智慧影像處理」？ {#what-is-smart-imaging}

智慧型影像處理技術運用Adobe Sensei AI功能，並可與現有的「影像預設集」搭配使用。 它能根據用戶端瀏覽器功能自動最佳化影像格式、大小和品質，進而提升影像傳送效能。

現在，借助AVIF和WebP支援的增強智慧影像功能，獲得LCP（最大的內容塗料）更好的Google核心Web重要分數。

>[!IMPORTANT]
>
>智慧型影像處理需要您使用隨附於Adobe Experience Manager - Dynamic Media的現成可用CDN（內容傳遞網路）。 此功能不支援任何其他自訂CDN。

>[!TIP]
>
>請試用並探索Dynamic Media影像修飾元和智慧影像處理的優點，使用Dynamic Media [_快照_](https://snapshot.scene7.com/).
>
> Snapshot是視覺化的示範工具，旨在說明Dynamic Media在最佳化和動態影像傳送方面的強大功能。 試用測試影像或Dynamic Media URL，以視覺化方式觀察各種Dynamic Media影像修飾元的輸出，並針對下列項目最佳化智慧型影像：
>* 檔案大小（使用WebP和AVIF傳送）
>* 網路頻寬
>* DPR（裝置像素比率）
>
>要了解使用快照有多簡單，請播放 [快照培訓視頻](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html?lang=en) （3分17秒）。

與Adobe同級最佳的CDN（內容傳遞網路）服務充分整合，可提升效能，讓智慧型影像處理受益匪淺。 此服務可在伺服器、網路和互連點之間找到最佳的Internet路由。 它找到的路由延遲最低，丟包率最低，而不是使用網際網路上的預設路由。

下列影像資產範例將說明新增的智慧型影像處理最佳化：

| 影像(URL) | 縮圖 | 大小(JPEG) | 大小(WebP)，帶智慧影像 | Size(AVIF)，帶智慧影像 | 使用WebP減少% | AVIF減少% |
|---|---|---|---|---|---|---|
| [影像1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 145 KB | 106 KB | 90.2 KB | 26.89% | 37.79% |
| [影像2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 412 KB | 346 KB | 113 KB | 16.01% | 72.57% |
| [影像3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 221 KB | 189 KB | 87.1 KB | 14.47% | 60.58% |
| [影像4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 594 KB | 545 KB | 286 KB | 8.25% | 51.85% |

與上方類似，Adobe也會以較大的範例集執行測試。 AVIF格式比WebP提供了20%的額外尺寸縮減，比JPEG減少27%。 視覺質量相同。 AVIF總計比JPEG平均縮小41%。

比較WebP和AVIF與PNG,WebP和AVIF的大小可減少84%,AVIF可減少87%。 此外，由於WebP和AVIF格式都支援透明和多個影像動畫，因此非常適合替換透明的PNG和GIF檔案。

另請參閱 [使用新一代影像格式（WebP和AVIF）進行影像優化](https://blog.developer.adobe.com/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)

<!-- HIDDEN ON MAY 19, 2022 BASED ON CQDOC-19280 On the mobile web, the challenges are compounded by two factors:

* Large variety of devices with different form factors and high-resolution displays.
* Constrained network bandwidth.

In terms of images, the goal is to serve the best quality images as efficiently as possible. -->

## 最新智慧映像有哪些主要優勢？ {#what-are-the-key-benefits-of-smart-imaging}

智慧影像處理可根據使用中的用戶端瀏覽器、裝置顯示和網路條件，自動最佳化影像檔案大小，提供更佳的影像傳送效能。 由於影像是頁面載入時間的大部分，因此任何效能改善都可能對業務KPI產生深遠影響，例如較高的轉換率、網站逗留時間以及較低的網站跳出率。

最新智慧影像處理的最新主要優點包括：

* 現在支援新一代AVIF格式。
* PNG轉WebP和AVIF現在支援有損轉換。 由於PNG是無損格式，因此早期傳送的WebP和AVIF是無損的。
* 瀏覽器格式轉換(`bfc`)
* 裝置像素比率(`dpr`)
* 網路頻寬(`network`)

### 關於瀏覽器格式轉換(bfc) {#bfc}

透過附加 `bfc=on` 至影像URL會自動將JPEG和PNG轉換為有損AVIF、有損WebP、有損JPEGXR、有損JPEG2000（針對不同瀏覽器）。 對於不支援這些格式的瀏覽器，智慧型影像處理會繼續提供JPEG或PNG。 與格式一起，新格式的品質會由智慧型影像重新計算。

智慧型影像也可以透過附加 `bfc=off` 至影像的URL。

另請參閱 [bfc](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-bfc.html?lang=en) 在Dynamic Media影像提供與轉譯API中。

### 關於裝置像素比率(dpr)最佳化 {#dpr}

裝置像素比率(DPR)（也稱為CSS像素比率）是裝置的物理像素與邏輯像素之間的關係。 特別是隨著視網膜螢幕的出現，現代移動設備的像素解析度正以快速的速度增長。

啟用「裝置像素比率」最佳化會以螢幕的原生解析度呈現影像，使其銳利化。

目前，顯示器的像素密度來自Akamai CDN標頭值。

| 影像URL中的允許值 | 說明 |
|---|---|
| `dpr=off` | 在個別影像URL層級關閉DPR最佳化。 |
| `dpr=on,dprValue` | 使用自訂值（由任何用戶端邏輯或其他方法偵測）覆寫智慧型影像偵測到的DPR值。 的允許值 `dprValue` 是大於0的任何數字。 |

>[!NOTE]
>
>* 您可以使用 `dpr=on,dprValue` 即使公司層級DPR設為「關閉」。
>* 由於DPR優化，當結果影像大於MaxPix Dynamic Media設定時，通過保持影像的長寬比始終可以識別MaxPix寬度。


| 請求的影像大小 | 裝置像素比率(dpr)值 | 傳遞的影像大小 |
|---|---|---|
| 816 x 500 | 1 | 816 x 500 |
| 816 x 500 | 2 | 1632 x 1000 |

另請參閱 [使用影像時](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-images) 和 [使用智慧型裁切時](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

### 關於網路頻寬優化 {#network}

開啟網路頻寬會自動根據實際網路頻寬調整提供的影像質量。 對於較差的網路頻寬，DPR（設備像素比）優化將自動關閉，即使它已開啟。

如果需要，您的公司可以借由附加 `network=off` 至影像的URL。

| 影像URL中的允許值 | 說明 |
|---|---|
| `network=off` | 在個別影像URL層級關閉網路最佳化。 |

DPR和網路頻寬值以所偵測到的套裝CDN用戶端值為基礎。 這些值有時不準確。 例如，DPR為2的iPhone5和DPR為2的iPhone12 `dpr=3`，均顯示 `dpr=2`. 不過，對於高解析度設備，發送 `dpr=2` 比發送好 `dpr=1`. 但是，克服這種不正確的最佳方式，是使用用戶端DPR來提供100%的精確值。 它適用於任何裝置，無論是Apple或其他啟動的裝置。 請參閱 [使用具有用戶端裝置像素比的智慧型影像](/help/assets/client-side-dpr.md).

### 智慧映像的其他主要優勢

* 改善使用最新智慧型影像處理之網頁的Google SEO排名。
* 立即提供最佳化內容（在執行階段）。
* 根據品質使用Adobe Sensei技術進行轉換(`qlt`)。
* 獨立於TTL（存留時間）。 過去，智慧型影像處理必須具備至少12小時的TTL才能運作。
* 之前，原始和衍生影像都會進行快取，而使快取失效需要兩步驟。 在最新的智慧型影像處理中，只會快取衍生產品，進而允許執行單步快取失效程式。
* 在規則集中使用自訂標頭的客戶將受益於最新的智慧型影像處理，因為這些標頭不會遭到封鎖，這與舊版的智慧型影像處理不同。 例如「計時允許來源」、「X-Robot」，如 [將自訂標頭值新增至影像回應|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html).

## 是否存在與智慧映像相關的許可成本？ {#are-there-any-licensing-costs-associated-with-smart-imaging}

否. 智慧影像處理隨附於您現有的授權。 Dynamic Media Classic或Experience Manager- Dynamic Media(內部部署、AMS和Experience Manageras a Cloud Service)適用此規則。

>[!NOTE]
>
>Dynamic Media — 混合客戶無法使用智慧影像處理。

## 智慧影像處理如何運作？ {#how-does-smart-imaging-work}

當消費者要求影像時，智慧影像處理會檢查使用者特性，並根據使用中的瀏覽器將其轉換為適當的影像格式。 這些格式轉換的執行方式不會降低視覺逼真度。 智慧型影像會以下列方式根據瀏覽器功能自動將影像轉換為不同格式。

* 如果瀏覽器支援格式，則自動轉換為AVIF
* 如果AVIF轉換不利或瀏覽器不支援AVIF，則自動轉換為WebP
* 如果Safari不支援WebP，則自動轉換為JPEG2000
* 自動轉換為IE 9+版JPEGXR，或如果Edge不支援WebP\
   |影像格式 |受支援的瀏覽器 | |—|—| | AVIF | [https://caniuse.com/avif](https://caniuse.com/avif) | | WebP | [https://caniuse.com/webp](https://caniuse.com/webp) | |JPEG2000 | [https://caniuse.com/jpeg2000](https://caniuse.com/jpeg2000) | | JPEGXR | [https://caniuse.com/jpegxr](https://caniuse.com/jpegxr) |
* 若瀏覽器不支援這些格式，則會提供原始要求的影像格式。

如果原始影像大小小於智慧型影像產生的大小，則會提供原始影像。

## 支援哪些影像格式？ {#what-image-formats-are-supported}

智慧影像處理支援下列影像格式：

* JPEG
* PNG

對於JPEG影像檔案格式，智慧影像會重新計算新格式的品質。

對於支援PNG等透明度的影像檔案格式，您可以配置智慧影像處理來傳送有損的AVIF和WebP。 對於有損格式轉換，智慧影像會使用影像URL中提及的品質，或使用Dynamic Media公司帳戶中設定的品質。

## 智慧型影像處理如何與已使用的現有影像預設集搭配運作？ {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

智慧型影像處理可與您現有的影像預設集搭配使用，並觀察您的所有影像設定。 變更的是影像格式、品質設定或兩者。 對於格式轉換，智慧影像處理會根據影像預設集設定所定義的完整視覺逼真度，但檔案大小較小。

例如，假設已使用JPEG格式定義影像預設集，大小為500 x 500，品質=85，遮色片=0.1,1,5。 當智慧型影像處理偵測到使用者位於Chrome瀏覽器時，影像會轉換為大小為500 x 500的WebP格式。 而且，銳利化遮色片=0.1,1,5是以盡可能接近85的JPEG品質符合的WebP品質。 會比較該WebP轉換的佔用空間與JPEG，並傳回兩者中較小者。

## 是否必須變更任何URL、影像預設集，或在我的網站上部署任何智慧型影像處理的新程式碼？ {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

否. 智慧型影像處理可順暢地與您現有的影像URL和影像預設集搭配運作。 此外，智慧影像處理不需要您將程式碼新增至網站以偵測使用者的瀏覽器。 所有這些功能都會自動處理。

<!-- Smart Imaging works seamlessly with your existing image URLs and image presets if you configure Smart Imaging on your existing custom domain. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. It is all handled automatically.

In case you must configure a new custom domain to use Smart Imaging, the URLs must be updated to reflect this custom domain.

To understand pre-requisites for Smart Imaging, see [Am I eligible to use Smart Imaging?](#am-i-eligible-to-use-smart-imaging) -->

<!-- OLD As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## 智慧型影像處理是否可搭配HTTPS運作？ HTTP/2如何？ {#does-smart-imaging-working-with-https-how-about-http}

智慧型影像處理可透過HTTP或HTTPS傳送的影像。 此外，它也可透過HTTP/2運作。

## 我是否符合使用智慧影像處理的資格？ {#am-i-eligible-to-use-smart-imaging}

若要使用智慧影像處理，您公司的Dynamic Media Classic或Dynamic MediaExperience Manager帳戶必須符合下列需求：

* 將Adobe隨附的CDN（內容傳遞網路）用於授權。
* 使用專用網域(例如 `images.company.com` 或 `mycompany.scene7.com`)，而非一般網域(例如 `s7d1.scene7.com`, `s7d2.scene7.com`，或 `s7d13.scene7.com`)。

若要尋找您的網域，請開啟 [Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的公司帳戶或帳戶。

前往 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 一般設定]**. 尋找標示為的欄位 **[!UICONTROL 已發佈的伺服器名稱]**. 如果您目前使用一般網域，可以要求移至您自己的自訂網域。 在提交支援案例時提出此轉變請求。

使用Dynamic Media授權，您的第一個自訂網域不需額外付費。

## 為我的帳戶啟用智慧影像處理的程式為何？ {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

您可以啟動使用智慧影像處理的請求；不會自動啟用。

建立支援案例，如下所述。 在您的支援案例中，請務必提及您要在帳戶上啟用的下列智慧影像處理功能（一或多個）:

* WebP
* AVIF
* DPR和網路頻寬最佳化
* PNG到有損AVIF或有損WebP

如果您已使用WebP啟用智慧影像處理，但想要如上所述的其他新功能，則必須建立支援案例。

**若要建立支援案例以在您的帳戶上啟用智慧影像處理：**

1. [使用Admin Console開始建立新的支援案例](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html).
1. 在您的支援案例中提供下列資訊：

   * 主要聯繫人姓名、電子郵件、電話。

   * 列出您要在帳戶上啟用的下列智慧影像處理功能（一個或多個）:
      * WebP
      * AVIF
      * DPR和網路頻寬最佳化
      * PNG到有損AVIF或有損WebP
   * 要啟用智慧映像的所有域(即 `images.company.com` 或 `mycompany.scene7.com`)。

      若要尋找您的網域，請開啟 [Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的公司帳戶或帳戶。

      前往 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 一般設定]**.

      尋找標示為的欄位 **[!UICONTROL 已發佈的伺服器名稱]**.

   * 確認您是透過Adobe使用CDN，而非以直接關係進行管理。

   * 確認您使用的是專用網域，例如 `images.company.com` 或 `mycompany.scene7.com`，而非一般網域，例如 `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      若要尋找您的網域，請開啟 [Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的公司帳戶或帳戶。

      前往 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 一般設定]**.

      尋找標示為的欄位 **[!UICONTROL 已發佈的伺服器名稱]**. 如果您目前使用一般Dynamic Media Classic網域，可以請求移轉至您自己的自訂網域，作為此轉變的一部分。

   * 指出是否希望它透過HTTP/2運作。


1. Adobe客戶支援會根據提交請求的順序將您添加到智慧映像客戶等待清單中。
1. 當Adobe準備好處理您的請求時，客戶支援會聯絡您以協調並設定目標日期。
1. **可選**:您可以選擇在測試環境中測試智慧影像，然後Adobe將新功能推送至生產環境。
1. 客戶支援在完成後通知您。
1. 為最大程度提升智慧型影像處理的效能，Adobe建議將存留時間(TTL)設為24小時或更長。 TTL會定義CDN快取資產的時間長度。 要更改此設定：

   1. 如果您使用Dynamic Media Classic，請前往 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 發佈設定]** > **[!UICONTROL 影像伺服器]**. 設定 **[!UICONTROL 預設客戶端快取的存留時間]** 值設為24或更新版本。
   1. 如果您使用Dynamic Media，請遵循 [這些指示](/help/assets/dm-publish-settings.md#common-thumbnail-attributes-tab). 設定 **[!UICONTROL 過期]** 值24小時或更久。

## 何時可以使用智慧影像處理啟用帳戶？ {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

系統會根據等待清單，依客戶支援接收請求的順序處理請求。

>[!NOTE]
>
>啟用智慧影像處理需要Adobe清除快取，因此可能需要較長的前置時間。 因此，在任何指定時間都只能處理少數客戶轉變。

## 切換到使用智慧映像有什麼風險？ {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

客戶網頁沒有風險。 不過，轉換至智慧型影像處理確實會清除CDN快取。 此操作涉及在Experience Manager上移至Dynamic Media Classic或Dynamic Media的新設定。

在初始轉變期間，非快取的影像會直接點擊Adobe的原始伺服器，直到重新建置快取為止。 因此，Adobe計劃一次處理一些客戶轉變，以在從來源提取請求時維持可接受的效能。 對於大部分的客戶，快取會在約1至2天內，於CDN中重新完全建立。

## 如何驗證智慧影像處理是否如預期般運作？{#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. 使用智慧型影像處理設定帳戶後，請在瀏覽器上載入Dynamic Media Classic或Adobe Experience Manager - Dynamic Media影像URL。
1. 開啟Chrome開發人員窗格，方法是前往 **[!UICONTROL 檢視]** > **[!UICONTROL 開發人員]** > **[!UICONTROL 開發人員工具]** 在瀏覽器中。 或者，選擇您選擇的任何瀏覽器開發人員工具。

1. 開啟開發人員工具時，請確定已停用快取。

   * 在Windows®上，導覽至開發人員工具窗格中的設定，然後選取 **[!UICONTROL 禁用快取（在開啟設備時）]** 框。
   * 在macOS中，在開發人員窗格的 **[!UICONTROL 網路]** 索引標籤，選取 **[!UICONTROL 禁用快取]**.

1. 觀察「內容類型」已轉換為適當的格式。 下列螢幕擷圖顯示在Chrome上動態轉換為WebP的PNG影像。 如果您的網域已啟用AVIF，您也可以在「內容類型」中看到AVIF。
1. 在不同的瀏覽器和使用者條件上重複此測試。

>[!NOTE]
>
>並非所有影像都經過轉換。 智慧型影像處理決定轉換是否能改善效能。 有時，如果沒有預期的效能增益，或格式不是JPEG或PNG，則不會轉換影像。

![image2017-11-14_15398](/help/assets/assets/image2017-11-14_15398.png)

## 我如何知道效能的提升？ 是否有辦法了解智慧映像的優勢？ {#benefits}

智慧影像頭決定了智慧影像處理的優勢。 啟用智慧型影像處理後，請求影像後，位於 **[!UICONTROL 回應標題]** 標題，您可以看到 `-X-Adobe-Smart-Imaging` 如下列醒目提示的範例所示：

![智慧型影像頭](/help/assets/assets-dm/smart-imaging-header2.png)

此標題會告訴您下列事項：

* 智慧影像處理正在為公司工作。
* 正值表示轉換成功。 在這種情況下，會傳回新的WebP影像。
* 負值表示轉換未成功。 在這種情況下，會傳回原始請求的影像(如果未指定，則預設為JPEG)。
* 正值顯示所請求影像與新影像之間的位元組差異。 在上述範例中，儲存的位元組為 `75048` 或一個影像大約75 KB。
* 負值表示請求的影像小於新影像。 會顯示負大小差，但提供的影像僅為原始請求影像。

>[!NOTE]
>
>**X-Adobe — 智慧型影像= -1，並傳送WebP**
>
>若 `X-Adobe-Smart-Imaging` 為–1且WebP仍在傳送，這表示智慧影像處理正常運作，但由於舊快取，大小優勢未計算。 您可以使用 `cache=update` （僅一次）填入影像URL以修正此問題。
>使用修飾詞的範例：
>`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`
>若要使整個快取失效，您必須建立支援案例。

## 如何在智慧影像處理中停用AVIF最佳化？{#disable-avif}

如果您想要在預設情況下切換回為WebP服務，請為此建立支援案例。 照常，您可以新增參數來關閉智慧型影像處理 `bfc=off` 至影像的URL。 但是，您無法在智慧影像處理的URL修飾元中選取WebP或AVIF。 這項功能會由您的公司帳戶層級維護。

## 是否可以針對任何請求關閉智慧影像？{#turning-off-smart-imaging}

可以。您可以新增下列任何修飾元，以關閉智慧型影像處理：

* `bfc=off` 關閉瀏覽器格式轉換。 另請參閱 [瀏覽器格式轉換](#bfc).
* `dpr=off` 關閉「設備像素比率」。 另請參閱 [裝置像素比率](#dpr).
* `network=off` 關閉網路頻寬。 另請參閱 [網路頻寬](#network).

## 可以使用什麼「調整」？ 是否有任何可定義的設定或行為？ {#tuning-settings}

智慧影像處理有三個選項可啟用或禁用。

* [瀏覽器格式轉換](#bfc)
* [裝置像素比率](#dpr)
* [網路頻寬](#network)

## 我在Chrome網頁瀏覽器上有一個URL，其中fmt=tif。 但我的請求因ImageServer錯誤而失敗。 原因為何？ {#fmt-tif}

如果未在您的帳戶上啟用智慧型影像處理，則不會發生此錯誤。 智慧型影像處理僅適用於JPEG或PNG格式。

若要避免此錯誤，您可以：

* 指定JPEG或PNG，或
* 不使用 `fmt` 完全修改，或
* 使用智慧型影像處理所定義的瀏覽器偏好格式。 例如，您可以對Chrome網頁瀏覽器使用WebP。

## 我想從影像的URL下載TIFF影像。 我該怎麼做？ {#download-tif}

新增 `fmt=tif` 和 `bfc=off` 至影像的URL路徑。

## 智慧影像處理是否僅管理影像格式，還是也管理影像質量設定以獲得最佳結果？

智慧型影像處理會同時使用格式和品質。 如果在影像的URL中提出要求，其餘的參數會維持不變。

## 如果智慧影像處理確實管理質量設定，是否有可設定的最小值和最大值？ 換句話說，質量不低於60，不大於80? {#quality-setting}

目前沒有此類布建。

## 智慧影像是自動調整百分比質量輸出設定，還是手動調整的設定，並應用於所有影像？ 在什麼範圍？ {#percent-quality}

智慧影像處理會自動調整品質百分比。 此品質百分比是使用由Adobe開發的機器學習演算法來決定。 此百分比不是特定範圍。

## 使用智慧影像處理，支援或忽略哪些影像伺服命令？ {#support-ignore}

唯一被忽略的命令是 `fmt` 和 `qlt`. 所有剩餘命令均受支援。

## 是否只有JPEG影像被智慧影像取代？ 如果我要求WebP、PNG或其他項目，該怎麼辦？ {#replace-request}

此功能僅適用於JPEG和PNG。

## 為何有時JPEG影像會傳回至Chrome而非WebP? {#jpeg-returned}

智慧型影像處理會判斷轉換是否有益。 它只會傳回轉換的新影像，是有益的。

## 為什麼在複合影像中，裝置像素比率(dpr)功能無法如預期運作？ {#composite-images}

如果複合影像涉及太多圖層，則使用位置修飾元時，dpr功能可能會受到影響。 此問題已知，將於未來版本的智慧型影像處理中修正。 如果其他智慧型影像處理功能未如預期運作，您可以建立支援案例來報告問題。

## 為什麼Smart Imaging PNG仍轉換為無損WebP/AVIF? {#convert-to-lossless}

由於PNG是無損格式，因此，以前傳送的WebP和AVIF是無損的，因此大小比預期的要大。 智慧型影像處理現在支援有損轉換。 您可以使用修飾詞 `cache=update` （僅限一次）。 使用此修飾詞的範例：

`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`

若要使整個快取無效，您必須建立支援案例，請求執行此動作。

## 如何在智慧影像處理中繼續使用PNG進行無損轉換？ {#continue-using}

智慧型影像處理現在支援以品質層級為基礎的有損轉換。 若要繼續使用無損轉換，您可以使用100個品質，這些品質是透過公司設定，或透過影像的URL，使用 `qlt=100` 在路徑中。