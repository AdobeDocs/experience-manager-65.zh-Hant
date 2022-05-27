---
title: 智慧型影像
description: 智慧映像應用每個用戶的獨特觀看特性，自動提供針對其體驗而優化的正確影像，從而獲得更好的效能和參與。
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
feature: Asset Management,Renditions
role: User, Admin
exl-id: e427d4ee-d5c8-421b-9739-f3cf2de36e41
source-git-commit: 9b02a5363d32771cd9c039f97044e8a1d72fe286
workflow-type: tm+mt
source-wordcount: '3518'
ht-degree: 1%

---

# 智慧型影像 {#smart-imaging}

## 什麼是「智慧映像」？ {#what-is-smart-imaging}

智慧成像技術應用了Adobe SenseiAI功能，並與現有的&quot;影像預設&quot;配合使用。 它致力於通過基於客戶端瀏覽器功能自動優化影像格式、大小和質量來增強影像傳送效能。

現在，通過改進的Smart Imaging（AVIF和WebP支援）為LCP（最大內容塗料）獲得更好的Google核心Web Vital得分。

>[!IMPORTANT]
>
>智慧映像要求您使用與Adobe Experience Manager-Dynamic Media捆綁的現成CDN（內容交付網路）。 此功能不支援任何其他自定義CDN。

智慧映像與Adobe的同類最佳高級CDN（內容交付網路）服務完全整合，可增強效能。 此服務可在伺服器、網路和對等點之間找到最佳Internet路由。 它會找到延遲最小和丟包率最低的路由，而不是使用Internet上的預設路由。

以下映像資產示例說明了添加的智慧映像優化：

| 影像(URL) | 縮圖 | 大小(JPEG) | Size(WebP)，帶智慧映像 | Size(AVIF)，帶智慧映像 | 使用WebP減少% | 使用AVIF減少% |
|---|---|---|---|---|---|---|
| [影像1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![圖片1](/help/assets/assets-dm/picture1.png) | 145 KB | 106 KB | 90.2 KB | 百分之二十六點八九 | 百分之三十七點七九 |
| [影像2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![圖片2](/help/assets/assets-dm/picture2.png) | 412 KB | 346 KB | 113 KB | 百分之十六點零一 | 72.57% |
| [影像3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![圖片3](/help/assets/assets-dm/picture3.png) | 221 KB | 189 KB | 87.1 KB | 百分之十四點四七 | 60.58% |
| [影像4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![圖片4](/help/assets/assets-dm/picture4.png) | 594 KB | 545 KB | 286 KB | 百分之八點二五 | 51.85% |

與上麵類似，Adobe還運行了具有較大樣本集的test。 AVIF格式比WebP提供了20%的額外尺寸縮減，比JPEG減少27%。 視覺質量都一樣。 總的來說，AVIF比JPEG平均減少41%。

將WebP和AVIF與PNG進行比較，WebP和AVIF的大小減少了84%,AVIF減少了87%。 而且，由於WebP和AVIF格式都支援透明和多個影像動畫，因此它很好地替代了透明PNG和GIF檔案。

另請參閱 [基於新一代影像格式（WebP和AVIF）的影像優化](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)

<!-- HIDDEN ON MAY 19, 2022 BASED ON CQDOC-19280 On the mobile web, the challenges are compounded by two factors:

* Large variety of devices with different form factors and high-resolution displays.
* Constrained network bandwidth.

In terms of images, the goal is to serve the best quality images as efficiently as possible. -->

## 最新智慧映像的主要優勢是什麼？ {#what-are-the-key-benefits-of-smart-imaging}

智慧映像通過基於使用中的客戶端瀏覽器、設備顯示和網路條件自動優化影像檔案大小而提供更好的影像傳輸效能。 因為影像是頁面負載時間的大部分，所以任何效能改進都會對業務KPI產生深刻影響，如更高的轉換率、在站點上花費的時間以及更低的站點跳轉率。

最新智慧映像的最新主要優勢包括：

* 現在支援下一代AVIF格式。
* PNG到WebP和AVIF現在支援有損轉換。 由於PNG是無損格式，因此早期交付的WebP和AVIF是無損的。
* 瀏覽器格式轉換(`bfc`)
* 設備像素比率(`dpr`)
* 網路頻寬(`network`)

### 關於瀏覽器格式轉換(bfc) {#bfc}

通過附加開啟瀏覽器格式轉換 `bfc=on` 到影像URL時，會自動將JPEG和PNG轉換為有損AVIF、有損WebP、有損JPEGXR、有損JPEG2000，用於不同的瀏覽器。 對於不支援這些格式的瀏覽器，Smart Imaging繼續為JPEG或PNG服務。 同時，通過Smart Imaging對新格式的質量進行重新計算。

還可以通過附加 `bfc=off` 的子菜單。

另請參閱 [足球](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-bfc.html?lang=en) 的子菜單。

### 關於設備像素比(dpr)優化 {#dpr}

設備像素比(DPR) — 也稱為CSS像素比 — 是設備的物理像素與邏輯像素之間的關係。 特別是隨著視網膜螢幕的出現，現代移動設備的像素解析度正在以快速的速度增長。

啟用設備像素比率優化將以螢幕的本機解析度呈現影像，使影像看起來清晰。

目前，顯示器的像素密度來自Akamai CDN報頭值。

| 影像URL中允許的值 | 說明 |
|---|---|
| `dpr=off` | 在單個影像URL級別關閉DPR優化。 |
| `dpr=on,dprValue` | 使用自定義值（由任何客戶端邏輯或其他方法檢測）覆蓋智慧映像檢測到的DPR值。 允許的值 `dprValue` 是大於0的任何數字。 |

>[!NOTE]
>
>* 您可以使用 `dpr=on,dprValue` 即使公司級DPR設定為「關閉」。
>* 由於DPR優化，當結果影像大於MaxPixDynamic Media設定時，通過保持影像的長寬比始終識別MaxPix寬度。


| 請求的映像大小 | 設備像素比率(dpr)值 | 已傳送的影像大小 |
|---|---|---|
| 816 x 500 | 1 | 816 x 500 |
| 816 x 500 | 2 | 1632 x 1000 |

另請參閱 [使用影像時](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-images) 和 [使用Smart Crop時](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop)。

### 關於網路頻寬優化 {#network}

啟用網路頻寬可根據實際網路頻寬自動調整提供的影像質量。 對於網路頻寬較差的情況，即使DPR（設備像素比率）優化已開啟，也會自動關閉。

如果需要，您的公司可以通過添加 `network=off` 的子菜單。

| 影像URL中允許的值 | 說明 |
|---|---|
| `network=off` | 在單個影像URL級別關閉網路優化。 |

DPR和網路頻寬值基於所綁定CDN的檢測到的客戶端值。 這些價值有時是不準確的。 例如，DPR為2的iPhone5和iPhone12 `dpr=3`雙 `dpr=2`。 不過，對於高解析度設備，發送 `dpr=2` 比發送 `dpr=1`。 但是，克服這種不準確性的最佳方法是使用客戶端DPR為您提供100%的準確值。 它適用於任何設備，無論是Apple還是其他發射的設備。 請參閱 [使用具有客戶端設備像素比的智慧映像](/help/assets/client-side-dpr.md)。

### 智慧映像的其他關鍵優勢

* 改進了使用最新智慧映像的網頁的GoogleSEO排名。
* 立即（在運行時）提供優化內容。
* 使用Adobe Sensei技術根據質量進行轉換(`qlt`)。
* TTL（生存時間）獨立。 以前，智慧映像的最低TTL為12小時是必需的。
* 以前，原始和衍生影像都被快取，而使快取失效的過程是兩步。 在最新的智慧映像中，只有衍生產品被快取，從而允許單步快取失效過程。
* 在規則集中使用自定義標頭的客戶可以從最新的智慧映像中獲益，因為這些標頭不會被阻止，這與以前版本的智慧映像不同。 例如，「計時允許原點」、「X-Robot」（如中所建議） [向映像響應添加自定義標頭值|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html)。

## 是否存在與智慧映像相關的許可成本？ {#are-there-any-licensing-costs-associated-with-smart-imaging}

否. 智慧映像隨您現有許可證一起提供。 此規則適用於Dynamic Media Classic或Experience Manager-Dynamic Media(On-prem、AMS和Experience Manageras a Cloud Service)。

>[!NOTE]
>
>Smart Imaging不適用於Dynamic Media — 混合型客戶。

## Smart Imaging是如何工作的？ {#how-does-smart-imaging-work}

當用戶請求影像時，智慧映像會檢查用戶特徵並根據使用中的瀏覽器轉換為適當的影像格式。 這些格式轉換以不降低視覺保真度的方式進行。 智慧成像按照以下方式根據瀏覽器功能自動將影像轉換為不同格式。

* 如果瀏覽器支援格式，則自動轉換為AVIF
* 如果AVIF轉換無益或瀏覽器不支援AVIF，則自動轉換為WebP
* 如果Safari不支援WebP，則自動轉換為JPEG2000
* 自動轉換為IE 9+的JPEGXR或Edge不支援WebP\
   |影像格式 |支援的瀏覽器 | |—| | AVIF | [https://caniuse.com/avif](https://caniuse.com/avif) | | WebP | [https://caniuse.com/webp](https://caniuse.com/webp) | |JPEG2000 | [https://caniuse.com/jpeg2000](https://caniuse.com/jpeg2000) | |JPEGXR | [https://caniuse.com/jpegxr](https://caniuse.com/jpegxr) |
* 對於不支援這些格式的瀏覽器，將提供最初請求的影像格式。

如果原始影像大小小於智慧成像生成的影像大小，則提供原始影像。

## 支援哪些影像格式？ {#what-image-formats-are-supported}

智慧映像支援以下影像格式：

* JPEG
* PNG

對於JPEG影像檔案格式，通過Smart Imaging重新計算新格式的質量。

對於支援PNG等透明度的影像檔案格式，可以配置Smart Imaging以提供有損的AVIF和WebP。 對於有損格式轉換，Smart Imaging使用影像URL中提到的質量，或者使用Dynamic Media公司帳戶中配置的質量。

## Smart Imaging如何使用我現有的已使用影像預設？ {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

Smart Imaging可使用您現有的影像預設並觀察您的所有影像設定。 更改的是影像格式或質量設定，或兩者。 對於格式轉換，Smart Imaging會按照影像預設設定的定義保持完全的視覺保真度，但檔案大小較小。

例如，假設影像預設是使用JPEG格式定義的，大小為500 x 500，質量為85，非銳化蒙版=0.1,1,5。 當智慧成像檢測到用戶在Chrome瀏覽器上時，影像將轉換為WebP格式，其大小為500 x 500，且WebP質量的非銳化掩碼=0.1,1,5，盡可能接近85的JPEG質量。 將該WebP轉換的佔用空間與JPEG進行比較，並返回兩者中較小的一個。

## 是否必須更改任何URL、影像預設，或在我的網站上部署任何新代碼以用於智慧成像？ {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

否. Smart Imaging可與您現有的影像URL和影像預設無縫協作。 此外，智慧映像不需要您向網站添加代碼來檢測用戶的瀏覽器。 所有此功能都將自動處理。

<!-- Smart Imaging works seamlessly with your existing image URLs and image presets if you configure Smart Imaging on your existing custom domain. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. It is all handled automatically.

In case you must configure a new custom domain to use Smart Imaging, the URLs must be updated to reflect this custom domain.

To understand pre-requisites for Smart Imaging, see [Am I eligible to use Smart Imaging?](#am-i-eligible-to-use-smart-imaging) -->

<!-- OLD As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## 智慧映像是否與HTTPS配合使用？ HTTP/2如何？ {#does-smart-imaging-working-with-https-how-about-http}

智慧映像可與通過HTTP或HTTPS傳送的映像配合使用。 此外，它還通過HTTP/2工作。

## 我是否有資格使用智慧映像？ {#am-i-eligible-to-use-smart-imaging}

要使用Smart Imaging，您公司的Dynamic Media Classic或Dynamic MediaExperience Manager客戶必須滿足以下要求：

* 將Adobe捆綁的CDN（內容分發網路）用作許可證的一部分。
* 使用專用域(例如， `images.company.com` 或 `mycompany.scene7.com`)，而不是泛型域(例如， `s7d1.scene7.com`。 `s7d2.scene7.com`或 `s7d13.scene7.com`)。

要查找域，請開啟 [Dynamic Media Classic台式機應用](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登錄到您的公司帳戶或帳戶。

轉到 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 常規設定]**。 查找標有 **[!UICONTROL 已發佈伺服器名稱]**。 如果您當前使用通用域，則可以請求移至您自己的自定義域。 在提交支援案例時發出此過渡請求。

您的第一個自定義域不需要額外的Dynamic Media許可證費用。

## 為我的帳戶啟用智慧映像的過程是什麼？ {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

您啟動使用智慧映像的請求；未自動啟用。

按如下所述建立支援案例。 在您的支援案例中，請確保提到您希望在帳戶上啟用以下哪些智慧映像功能（一個或多個）:

* 網頁
* 阿維夫
* DPR和網路頻寬優化
* PNG到有損AVIF或有損WebP

如果您已通過WebP啟用了智慧映像，但希望獲得上面列出的其他新功能，則必須建立支援案例。

**要建立支援案例以在您的帳戶上啟用Smart Imaging:**

1. [使用Admin Console開始建立新支援案例](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)。
1. 在支援案例中提供以下資訊：

   * 主要聯繫人姓名，電子郵件，電話。

   * 列出您要在帳戶上啟用的下列智慧映像功能（一個或多個）:
      * 網頁
      * 阿維夫
      * DPR和網路頻寬優化
      * PNG到有損AVIF或有損WebP
   * 要啟用智慧映像的所有域(即 `images.company.com` 或 `mycompany.scene7.com`)。

      要查找域，請開啟 [Dynamic Media Classic台式機應用](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登錄到您的公司帳戶或帳戶。

      轉到 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 常規設定]**。

      查找標有 **[!UICONTROL 已發佈伺服器名稱]**。

   * 驗證您是否正通過Adobe使用CDN，而不是使用直接關係進行管理。

   * 驗證您是否使用專用域，如 `images.company.com` 或 `mycompany.scene7.com`，而不是泛型域，如 `s7d1.scene7.com`。 `s7d2.scene7.com`。 `s7d13.scene7.com`。

      要查找域，請開啟 [Dynamic Media Classic台式機應用](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登錄到您的公司帳戶或帳戶。

      轉到 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 常規設定]**。

      查找標有 **[!UICONTROL 已發佈伺服器名稱]**。 如果您當前使用的是通用的Dynamic Media Classic域，則可以請求將此過渡過程的一部分移到您自己的自定義域。

   * 指示是否希望它通過HTTP/2工作。


1. Adobe客戶支援根據請求的提交順序將您添加到智慧映像客戶等待清單。
1. 當Adobe準備好處理您的請求時，客戶支援會聯繫您以協調和設定目標日期。
1. **可選**:在將新功能推送到生產之前，您可以選擇在轉移中test智慧映像。
1. 完成後，客戶支援會通知您。
1. 為最大限度地提高智慧映像的效能，Adobe建議將「生存時間」(TTL)設定為24小時或更長。 TTL定義CDN快取資產的時間。 要更改此設定：

   1. 如果你用Dynamic Media Classic **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 發佈設定]** > **[!UICONTROL 映像伺服器]**。 設定 **[!UICONTROL 預設客戶端快取生存時間]** 值為24或更高。
   1. 如果你用Dynamic Media，跟上 [這些說明](/help/assets/dm-publish-settings.md#common-thumbnail-attributes-tab)。 設定 **[!UICONTROL 到期]** 值24小時或更長。

## 我何時可以期望使用智慧映像啟用我的帳戶？ {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

請求按客戶支援根據等待清單接收的順序進行處理。

>[!NOTE]
>
>可能需要較長的提前期，因為啟用智慧映像涉及Adobe清除快取。 因此，在任何給定時間都只能處理少數客戶過渡。

## 切換到使用智慧映像有何風險？ {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

客戶網頁沒有風險。 但是，向智慧映像的過渡確實會清除您的CDN快取。 這項行動涉及轉向Dynamic Media Classic或Dynamic Media的Experience Manager新配置。

在初始過渡期間，非快取映像直接命中Adobe的源伺服器，直到重新生成快取。 因此，Adobe計劃一次處理幾個客戶過渡，以便在從原點拉回請求時保持可接受的效能。 對於大多數客戶，在大約1到2天內在CDN上再次完全建立快取。

## 如何驗證智慧映像是否按預期工作？{#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. 配置了智慧映像後，請在瀏覽器上載入Dynamic Media Classic或Adobe Experience Manager-Dynamic Media映像URL。
1. 通過轉到 **[!UICONTROL 視圖]** > **[!UICONTROL 開發人員]** > **[!UICONTROL 開發人員工具]** 的雙曲餘切值。 或者，選擇您選擇的任何瀏覽器開發工具。

1. 確保在開發人員工具開啟時禁用快取。

   * 在Windows®上，導航到開發人員工具窗格中的設定，然後選擇 **[!UICONTROL 禁用快取（當devtools處於開啟狀態時）]** 的子菜單。
   * 在macOS，在開發人員的窗格下 **[!UICONTROL 網路]** 頁籤 **[!UICONTROL 禁用快取]**。

1. 觀察內容類型已轉換為相應格式。 以下螢幕快照顯示了動態轉換為Chrome上WebP的PNG影像。 如果域啟用了AVIF，您還可以在「內容類型」中查看AVIF。
1. 在不同的瀏覽器和用戶條件上重複此test。

>[!NOTE]
>
>並非所有影像都已轉換。 Smart Imaging決定轉換是否可以提高效能。 有時，如果沒有預期的效能增益或格式不是JPEG或PNG，則不轉換影像。

![image2017-11-14_15398](/help/assets/assets/image2017-11-14_15398.png)

## 我如何知道效能的提升？ 是否有一種方法瞭解智慧映像的好處？ {#benefits}

Smart Imaging Header可確定Smart Imaging的優勢。 啟用智慧映像後，請求映像後， **[!UICONTROL 響應標頭]** 標題，您可以看到 `-X-Adobe-Smart-Imaging` 如以下突出顯示的示例所示：

![智慧映像頭](/help/assets/assets-dm/smart-imaging-header2.png)

此標題將告訴您以下內容：

* Smart Imaging正在為公司工作。
* 正值表示轉換成功。 在這種情況下，將返回新的WebP影像。
* 負值表示轉換不成功。 在這種情況下，將返回原始請求的映像(預設情況下，如果未指定JPEG)。
* 正值顯示請求的影像和新影像之間的位元組差。 在上例中，保存的位元組為 `75048` 或一個映像大約75 KB。
* 負值表示所請求的影像小於新影像。 顯示負大小差，但所提供的影像僅是原始請求的影像。

>[!NOTE]
>
>**XAdobe智慧映像= -1，正在提供WebP**
>
>如果 `X-Adobe-Smart-Imaging` 是–1，並且WebP仍在提供，這意味著智慧映像正在工作，但由於舊快取而未計算大小優勢。 您可以使用 `cache=update` （僅一次）。
>使用修改量的示例：
>`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`
>要使整個快取失效，必須建立支援案例。

## 如何在智慧映像中禁用AVIF優化？{#disable-avif}

如果要在預設情況下切換回為WebP服務，請為此建立支援案例。 與往常一樣，可以通過添加參數來關閉智慧映像 `bfc=off` 的子菜單。 但是，您不能在Smart Imaging的URL修飾符中選擇WebP或AVIF。 此能力在您的公司帳戶級別進行維護。

## 是否可以關閉智慧映像以滿足任何請求？{#turning-off-smart-imaging}

可以。 通過添加以下任何修飾符，可以關閉Smart Imaging:

* `bfc=off` 按鈕。 另請參閱 [瀏覽器格式轉換](#bfc)。
* `dpr=off` 關閉設備像素比。 另請參閱 [設備像素比](#dpr)。
* `network=off` 關閉網路頻寬。 另請參閱 [網路頻寬](#network)。

## 有哪些「調諧」可用？ 是否可以定義任何設定或行為？ {#tuning-settings}

智慧映像有三個選項，您可以啟用或禁用。

* [瀏覽器格式轉換](#bfc)
* [設備像素比](#dpr)
* [網路頻寬](#network)

## 我在Chrome Web瀏覽器上有一個帶fmt=tif的URL。 但我的請求失敗，出現ImageServer錯誤。 為什麼？ {#fmt-tif}

如果帳戶上未啟用智慧映像，則不會出現此錯誤。 Smart Imaging僅能使用JPEG或PNG格式。

為避免此錯誤，您可以：

* 指定JPEG或PNG，或
* 不使用 `fmt` 修改量，或
* 使用由智慧映像定義的瀏覽器首選格式。 例如，可以將WebP用於Chrome Web瀏覽器。

## 我想從影像的URL下載TIFF影像。 我該怎麼做？ {#download-tif}

添加 `fmt=tif` 和 `bfc=off` 到影像的URL路徑。

## 智慧映像是僅管理映像格式還是還管理映像質量設定以獲得最佳效果？

智慧映像使用格式和質量。 如果在影像的URL中請求，其餘參數將保持不變。

## 如果Smart Imaging確實管理質量設定，我是否可以設定最小值和最大值？ 換句話說，一個不低於60，不大於80的品質？ {#quality-setting}

當前沒有此類設定。

## Smart Imaging是自動調整質量百分比輸出設定還是手動調整的設定，並且它應用於所有影像？ 在什麼範圍內？ {#percent-quality}

Smart Imaging自動調整質量百分比。 該質量百分比是使用由Adobe開發的機器學習算法確定的。 此百分比不特定於範圍。

## 使用Smart Imaging ，支援或忽略哪些影像服務命令？ {#support-ignore}

僅忽略的命令 `fmt` 和 `qlt`。 支援所有剩餘命令。

## 是否只有JPEG映像被智慧映像取代？ 如果我請求WebP、PNG或其他什麼？ {#replace-request}

此功能僅適用於JPEG和PNG。

## 為什麼有時JPEG影像會返回到Chrome而不是WebP? {#jpeg-returned}

Smart Imaging確定轉換是否有益。 它只返回轉換的新影像是有益的。

## 為什麼設備像素比(dpr)功能在複合影像中不能按預期工作？ {#composite-images}

如果複合影像涉及的圖層太多，則使用位置修飾符時可能會影響dpr功能。 此問題已知，並將在未來的智慧映像版本中解決。 如果其他智慧映像功能未按預期工作，則可以建立支援案例來報告問題。

## 為什麼Smart Imaging PNG仍轉換為無損WebP/AVIF? {#convert-to-lossless}

由於PNG是無損格式，所以早期交付的WebP和AVIF是無損的，因此其大小比預期的要高。 智慧成像現在支援有損轉換。 您可以使用修改量 `cache=update` （僅一次）在映像請求中修復此問題。 使用此修改量的示例：

`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`

要使整個快取失效，必須建立請求執行此類工作的支援案例。

## 如何在Smart Imaging中繼續使用PNG到無損轉換？ {#continue-using}

智慧成像現在支援基於質量級別的有損轉換。 要繼續使用無損轉換，可以使用通過公司設定或通過影像的URL設定的100質量 `qlt=100` 在路上。