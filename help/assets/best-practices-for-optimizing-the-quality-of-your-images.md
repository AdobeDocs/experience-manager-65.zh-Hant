---
title: 在Dynamic Media中最佳化影像品質的最佳作法
description: 了解在Dynamic Media中最佳化影像品質的最佳實務
uuid: b73f0918-c723-4a0d-a63f-4242223c2d47
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 12baf001-dfc9-410a-9821-a3bae1324392
feature: Asset Management
role: User, Admin
exl-id: 7a568cae-e505-4b3a-abc5-8aae723460c3
source-git-commit: 471f9e99078a1e0af60024d439afd42ae77cba8c
workflow-type: tm+mt
source-wordcount: '1449'
ht-degree: 4%

---

# 在Dynamic Media中最佳化影像品質的最佳作法 {#best-practices-for-optimizing-the-quality-of-your-images}

最佳化影像品質可能是一項耗時的過程，因為許多因素都有助於呈現可接受的結果。 結果部分是主觀的，因為個體對影像質量的看法不同。 結構化實驗是關鍵。

Adobe Experience Manager包含超過100個Dynamic Media影像傳送命令，用於調整和最佳化影像及轉譯結果。 下列准則可協助您使用一些基本命令和最佳實務來簡化程式並快速取得良好結果。

## 影像格式的最佳實務(`&fmt=`) {#best-practices-for-image-format-fmt}

* JPG或PNG是提供高品質且大小和重量可控影像的最佳選擇。
* 如果URL中未提供format命令，Dynamic Media影像傳送預設為要傳送的JPG。
* JPG以10:1的比例壓縮，通常會產生較小的影像檔案大小。 PNG壓縮的比率約為2:1，但有時候除外，例如影像包含白色背景時。 不過，PNG檔案通常比JPG檔案大。
* JPG使用有損壓縮，這表示在壓縮期間會捨棄圖片元素（像素）。 PNG則使用無損壓縮。
* JPG通常以比具有銳邊和對比度的合成影像更高的逼真度來壓縮照片影像。
* 如果影像包含透明度，請使用PNG，因為JPG不支援透明度。

影像格式最佳實務，請從最常見的設定開始 `&fmt=JPG`.

## 影像大小最佳實務 {#best-practices-for-image-size}

動態縮小影像大小是最常見的任務之一。 它涉及指定大小，以及（可選）使用哪個縮減取樣模式來縮小影像。

* 對於影像大小調整，最佳且最直接的方法是使用 `&wid=<value>` 和 `&hei=<value>,`或 `&hei=<value>`. 這些參數會根據長寬比自動設定影像寬度。
* `&resMode=<value>`控制用於縮減取樣的演算法。 開始於 `&resMode=sharp2`. 此值可提供最佳的影像品質。 使用縮減取樣時 `value =bilin` 速度較快，通常會導致偽影的混疊。

作為影像大小調整的最佳實務，請使用 `&wid=<value>&hei=<value>&resMode=sharp2` 或 `&hei=<value>&resMode=sharp2`

## 影像銳利化最佳作法 {#best-practices-for-image-sharpening}

影像銳利化是控制網站上影像的最複雜環節，也是常有錯誤發生的地方。 請參考下列實用資源，以深入了解銳利化和遮色片銳利化在Experience Manager中的運作方式：

最佳實務白皮書 [銳化Adobe Dynamic Media Classic中的影像](/help/assets/assets/sharpening_images.pdf) 也適用於Experience Manager。

<!-- To be reviewed and updated: Broken link.
See also [Sharpening an image with unsharp mask](https://helpx.adobe.com/photoshop/atv/cs6-tutorials/sharpening-an-image-with-unsharp-mask.html). -->

透過Experience Manager，您可以在擷取、傳送或兩者時銳利化影像。 但是，通常只使用一種或另一種方法來銳化影像，但不同時使用兩種方法。 傳送時在URL上銳利化影像，通常能提供最佳結果。

您可以使用兩種影像銳利化方法：

* 簡單銳利化( `&op_sharpen`) — 類似於Photoshop中使用的銳利化濾鏡，簡單銳利化會在動態調整大小後將基本銳利化套用至影像的最終檢視。 不過，此方法不可由使用者設定。 除非需要，否則最佳做法是不使用&amp;op_sharpen。
* 遮色片銳利化( `&op_USM`) — 遮色片銳利化是業界標準的銳利化濾鏡。 最佳作法是依照下列准則，使用非銳利化遮色片來銳利化影像。 遮色片銳利化可讓您控制下列三個參數：

   * `&op_sharpen=amount,radius,threshold`

      * **[!UICONTROL *金額&#x200B;*]**（0-5，效果強度。）
      * **[!UICONTROL *半徑&#x200B;*]**(0-250，在銳化對象周圍繪製的「銳利化線」寬度（以像素計）。

      請記得，參數半徑和量彼此相互作用。 通過增加量可以補償減小的半徑。 半徑允許更精細的控制，因為較低的值只銳化邊緣像素，而較高的值銳化較寬的像素帶。

      * **[!UICONTROL *臨界值&#x200B;*]**（0-255，效應的敏感性。）

             此參數可決定銳化像素與周圍區域的差異程度，之後才會被視為邊緣像素，濾鏡會銳化這些像素。**[!UICONTROL threshold]**參數有助於避免色彩相似的區域過度銳利化，例如膚色。例如，閾值為12會忽略膚色亮度的微小變化，以避免加上「雜訊」，同時仍會加上邊緣對比度至高對比區域，例如睫毛與皮膚相遇的區域。
         
         如需如何設定這三個參數的詳細資訊，包括搭配篩選器使用的最佳實務，請參閱下列資源：

         銳利化影像的Experience Manager說明主題。

         最佳實務白皮書 [銳化Adobe Dynamic Media Classic中的影像](/help/assets/assets/sharpening_images.pdf).

      * Experience Manager也可讓您控制第四個參數：單色(0,1)。 此參數確定是否使用值0分別對每個顏色分量應用銳利化遮色片，或使用值1對影像亮度/強度應用銳利化遮色片。


最佳實務是從遮色片半徑不銳利化參數開始。 可以開頭的半徑設定如下：

* **[!UICONTROL 網站]** - 0.2-0.3像素
* **[!UICONTROL 照片打印(250-300 ppi)]** - 0.3-0.5像素
* **[!UICONTROL 膠印(266-300 ppi)]** - 0.7-1.0像素
* **[!UICONTROL 畫布列印(150 ppi)]** - 1.5-2.0像素

逐步從1.75增加到4。 如果銳利化仍不是您想要的方式，請將半徑增加小數點，然後從1.75重新執行量至4。 視需要重複。

將單色參數設定保留為0。

### JPEG壓縮的最佳實務(`&qlt=`) {#best-practices-for-jpeg-compression-qlt}

* 此參數會控制JPG編碼品質。 值越高，表示影像質量越高，但檔案大小越大；或者，值越低，表示影像質量越低，但檔案大小越小。 此參數的範圍是0-100。
* 若要最佳化品質，請勿將參數值設為100。 設定90或95與100之間的差異幾乎不可察覺，但100會不必要地增加影像檔案的大小。 因此，若要最佳化品質，同時避免影像檔案變得過大，請設定 `qlt= value` 90或95。
* 要針對小的影像檔案大小進行優化，但將影像質量保持在可接受的級別，請設定 `qlt= value` 80。 低於70到75的值會導致影像質量顯著下降。
* 最佳實務是，若要居中，請設定 `qlt= value` 到85，才能留在中間。
* 在 `qlt=`

   * 此 `qlt=` 參數有第二個設定，可讓您使用值開啟RGB色度下採樣 `,1` 或不使用值 `,0`.
   * 要保持其簡單，請從關閉RGB色度下採樣開始(`,0`)。 此設定通常能產生更好的影像品質，特別是對於具有大量銳邊和對比度的合成影像。

使用JPG壓縮是最佳實務 `&qlt=85,0`.

## JPEG大小最佳實務(`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

如果您想要保證影像不會超過特定大小，以便傳送給記憶體有限的裝置，jpegSize就是有用的參數。

* 此參數以千位元組(`jpegSize=&lt;size_in_kilobytes&gt;`)。 它定義了影像傳送的允許大小上限。
* `&jpegSize=` 與JPG壓縮參數互動 `&qlt=`. 如果JPG以指定的JPG壓縮參數(`&qlt=`)未超過jpegSize值，則影像會以 `&qlt=` 定義。 否則， `&qlt=` 會逐漸縮小，直到影像符合允許的最大大小，或直到系統確定無法符合併傳回錯誤為止。

作為最佳實務，請設定 `&jpegSize=` 並新增參數 `&qlt=` 如果您要將JPG影像傳送至記憶體有限的裝置。

## 最佳實務摘要 {#best-practices-summary}

最佳實務是要達到高影像品質和小檔案大小，請從以下參陣列合開始：

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

這種設定組合在大多數情況下都會產生極好的結果。

如果影像需要進一步優化，則從半徑設定為0.2或0.3開始，逐漸微調銳利化（非銳利化遮色片）參數。然後，逐漸將量從1.75增加到最大4(相當於Photoshop的400%)。 檢查是否達到所需結果。

如果銳利化結果仍不理想，請增加小數點增量的半徑。 對於每小數增量，以1.75重新開始該量，並逐漸將其增加至4。 重複此過程，直到達到所需結果。 雖然上述價值是創意工作室已驗證的方法，但請記住，您可以從其他價值開始，並遵循其他策略。 結果是否令人滿意是主觀問題，因此結構化實驗是關鍵。

在實驗中，下列一般建議有助於進一步最佳化您的工作流程：

* 直接在URL上即時試用並測試不同的參數。
* 最佳實務是，您可以將「Dynamic Media影像伺服」命令分組至影像預設集。 影像預設集基本上是具有自訂預設集名稱(例如 `$thumb_low$` 和 `&product_high$`. URL路徑中的自訂預設集名稱會呼叫這些預設集。 這些功能可協助您管理網站上不同影像使用模式的命令和品質設定，並縮短URL的整體長度。
* Experience Manager也提供更進階的影像品質調整方法，例如在擷取時套用銳利化影像。 針對有選項可調整和最佳化演算結果的進階使用案例， [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html) 可協助您運用自訂的深入分析和最佳實務。
