---
title: 在Dynamic Media中最佳化影像品質的最佳作法
description: 瞭解在Dynamic Media中最佳化影像品質的最佳實務
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Asset Management
role: User, Admin
exl-id: 7a568cae-e505-4b3a-abc5-8aae723460c3
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 4%

---

# 在Dynamic Media中最佳化影像品質的最佳作法 {#best-practices-for-optimizing-the-quality-of-your-images}

最佳化影像品質是一項耗時的程式，因為許多因素都會產生可接受的演算結果。 由於個人對影像品質的認知不同，所以最後的結果會有部分主觀性。 結構化的實驗是關鍵。

Adobe Experience Manager包含100多項Dynamic Media影像傳送命令，用於調整及最佳化影像和演算結果。 下列准則可協助您使用一些基本指令和最佳作法，簡化程式並快速取得良好的結果。

## 影像格式的最佳實務(`&fmt=`) {#best-practices-for-image-format-fmt}

* JPG或PNG是最佳選擇，可提供高品質且大小與重量可管理之影像。
* 如果URL中未提供格式命令，Dynamic Media影像傳送預設為JPG傳送。
* JPG會以10:1的比例壓縮，通常會產生較小的影像檔案大小。 PNG會以大約2:1的比例壓縮，除非有時影像包含白色背景時。 不過，PNG檔案通常比JPG檔案大。
* JPG使用有失真壓縮，表示壓縮期間會捨棄圖片元素（畫素）。 另一方面，PNG使用無失真壓縮。
* JPG通常會以比合成影像更好的逼真度壓縮像片影像，而合成影像則具有銳利的邊緣和對比。
* 如果影像包含透明度，請使用PNG，因為JPG不支援透明度。

影像格式的最佳作法是從最常見的設定開始 `&fmt=JPG`.

## 影像大小相關最佳實務 {#best-practices-for-image-size}

動態縮小影像大小是最常見的工作之一。 它涉及指定大小，以及（選擇性）用來縮減影像規模的縮減取樣模式。

* 調整影像大小的最佳且最直接的方法是使用 `&wid=<value>` 和 `&hei=<value>,`或只是 `&hei=<value>`. 這些引數會根據外觀比例自動設定影像寬度。
* `&resMode=<value>`控制縮減取樣所使用的演演算法。 開始於 `&resMode=sharp2`. 這個值可提供最佳的影像品質。 使用縮減取樣時 `value =bilin` 速度更快，通常會導致鋸齒狀不自然感。

如需調整影像大小的最佳作法，請使用 `&wid=<value>&hei=<value>&resMode=sharp2` 或 `&hei=<value>&resMode=sharp2`

## 影像銳利化的最佳作法 {#best-practices-for-image-sharpening}

影像銳利化是控制網站上影像的最複雜方面，也會造成許多錯誤。 請參考下列實用資源，以花時間進一步瞭解銳利化和遮色片銳利化在Experience Manager中的運作方式：

最佳實務白皮書 [Adobe Dynamic Media Classic中的銳利化影像](/help/assets/assets/sharpening_images.pdf) 也適用於Experience Manager。

<!-- To be reviewed and updated: Broken link.
See also [Sharpening an image with unsharp mask](https://helpx.adobe.com/photoshop/atv/cs6-tutorials/sharpening-an-image-with-unsharp-mask.html). -->

透過Experience Manager，您可以在內嵌和/或傳送時銳利化影像。 不過，通常只會使用一種方法或另一種方法來銳利化影像，但不會同時使用兩者。 在URL上傳送影像時銳利化，通常能提供最佳結果。

您可以使用兩種影像銳利化方法：

* 簡單銳利化( `&op_sharpen`) — 類似於Photoshop中使用的銳利化濾鏡，簡單銳利化會在動態調整大小後，將基本銳利化套用至影像的最終檢視。 不過，此方法無法由使用者設定。 除非必要，否則最佳實務是不使用&amp;op_sharpen。
* 不銳利化遮色片( `&op_USM`) — 不銳利化遮色片是業界標準的銳利化濾鏡。 最佳作法是依照下列方針，使用遮色片銳利化來銳利化影像。 「不銳利化遮色片」可讓您控制下列三個引數：

   * `&op_sharpen=amount,radius,threshold`

      * **[!UICONTROL *數量&#x200B;*]**（0-5，效果強度。）
      * **[!UICONTROL *半徑&#x200B;*]**(0-250，在銳利化物件周圍繪製的「銳利化線條」寬度（以畫素為測量單位）。

     請記住，引數半徑和數量彼此對應。 可透過增加量來補償減小的半徑。 「半徑」允許更細微的控制，因為較低的值只會銳利化邊緣畫素，而較高的值會銳利化較寬的畫素範圍。

      * **[!UICONTROL *臨界值&#x200B;*]**（0-255，效果敏感度。）

            此參數可決定銳化像素與周圍區域的差異程度，之後才會被視為邊緣像素，濾鏡會銳化這些像素。**[!UICONTROL threshold]**參數有助於避免色彩相似的區域過度銳利化，例如膚色。例如，閾值為12會忽略膚色亮度的微小變化，以避免加上「雜訊」，同時仍會加上邊緣對比度至高對比區域，例如睫毛與皮膚相遇的區域。
        
        如需如何設定這三個引數的詳細資訊，包括篩選使用的最佳實務，請參閱下列資源：

        有關銳利化影像的Experience Manager說明主題。

        最佳實務白皮書 [Adobe Dynamic Media Classic中的銳利化影像](/help/assets/assets/sharpening_images.pdf).

      * Experience Manager也可讓您控制第四個引數：單色(0,1)。 此引數決定使用0值將遮色片銳利化調整分別套用至每個色彩元件，或是使用1值將影像亮度/強度套用至影像。

最佳作法是從「遮色片銳利化調整半徑」引數開始。 您可以開始使用的半徑設定如下：

* **[!UICONTROL 網站]** - 0.2-0.3畫素
* **[!UICONTROL 像片列印(250-300 ppi)]** - 0.3-0.5畫素
* **[!UICONTROL 膠片列印(266-300 ppi)]** - 0.7至1.0畫素
* **[!UICONTROL 畫布列印(150 ppi)]** - 1.5至2.0畫素

逐漸將數量從1.75增加到4。 如果銳利化仍不是您想要的方式，請將半徑增加小數點，然後再次從1.75到4執行量。 視需要重複。

將單色引數設定保留為0。

### JPEG壓縮的最佳作法(`&qlt=`) {#best-practices-for-jpeg-compression-qlt}

* 此引數可控制JPG編碼品質。 較高的值表示影像品質較高，但檔案大小較大；或者，較低的值表示影像品質較低，但檔案大小較小。 此引數的範圍為0至100。
* 若要最佳化品質，請勿將引數值設為100。 設定90或95與100之間的差異幾乎無法察覺，但100卻不必要地增加了影像檔案的大小。 因此，若要最佳化品質但避免影像檔案變得太大，請設定 `qlt= value` 到90或95。
* 若要針對較小的影像檔案大小進行最佳化，但將影像品質維持在可接受的等級，請設定 `qlt= value` 至80。 值低於70到75會導致影像品質顯著下降。
* 作為最佳實務，若要保持在中間，請將 `qlt= value` 到85歲才能居於中間。
* 在中使用色度旗標 `qlt=`

   * 此 `qlt=` 引數有第二個設定，可讓您使用值開啟RGB色度縮減取樣 `,1` 或關閉使用值 `,0`.
   * 為了保持簡單，請從RGB色度縮減取樣關閉(`,0`)。 此設定通常會產生更好的影像品質，尤其是對於具有大量銳利邊緣和對比的人工合成影像。

使用JPG壓縮作為最佳實務 `&qlt=85,0`.

## JPEG規模調整的最佳實務(`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

如果您想要保證影像不會超過特定大小，以傳送至記憶體有限的裝置，jpegSize會是一個有用的引數。

* 此引數是以KB為單位(`jpegSize=&lt;size_in_kilobytes&gt;`)。 它會定義影像傳送的允許大小上限。
* `&jpegSize=` 會與JPG壓縮引數互動 `&qlt=`. 如果JPG回應具有指定的JPG壓縮引數(`&qlt=`)不會超過jpegSize值，而影像會以 `&qlt=` 依定義。 否則， `&qlt=` 會逐漸減少，直到影像符合最大允許大小，或直到系統判斷它無法符合併傳回錯誤為止。

最佳實務是，設定 `&jpegSize=` 並新增引數 `&qlt=` 如果您要將JPG影像傳送至記憶體有限的裝置。

## 最佳實務摘要 {#best-practices-summary}

為了達到高影像品質和小檔案大小，最佳實務建議從下列參陣列合開始：

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

此設定組合可在大多數情況下提供絕佳的結果。

如果影像需要進一步最佳化，請從半徑設定為0.2或0.3開始，逐步微調銳利化（不銳利化遮色片）引數。然後，逐漸將數量從1.75增加到最大值4 (相當於Photoshop中的400%)。 檢查是否達到所需結果。

如果銳利化結果仍然不令人滿意，請以小數點為增量增加半徑。 對於每個小數點增量，請在1.75處重新啟動該數量，並逐漸將其增加到4。 重複此程式，直到您達到想要的結果為止。 雖然上述值是經過創意工作室驗證的方法，但請記住，您可以從其他值開始，並遵循其他策略。 結果是否令您滿意是主觀問題，因此結構化的實驗是關鍵。

實驗時，以下一般建議有助於進一步最佳化您的工作流程：

* 請直接在URL上即時嘗試並測試不同的引數。
* 如需參考最佳做法，請記得您可以將「Dynamic Media影像伺服」命令群組至影像預設集。 影像預設集基本上是URL指令巨集，其中包含自訂預設集名稱，例如 `$thumb_low$` 和 `&product_high$`. URL路徑中的自訂預設集名稱會呼叫這些預設集。 這類功能可協助您針對網站上不同的影像使用模式管理命令和品質設定，並縮短URL的整體長度。
* Experience Manager也提供更進階的方式來調整影像品質，例如在擷取時套用銳利化影像。 對於進階使用案例，其中提供了調整和最佳化演算結果的選項， [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html) 可協助您提供客製化的深入分析和最佳作法。
