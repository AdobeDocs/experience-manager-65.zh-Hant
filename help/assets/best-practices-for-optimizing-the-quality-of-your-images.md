---
title: 優化您在Dynamic Media的映像質量的最佳做法
description: 瞭解優化Dynamic Media影像質量的最佳做法
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

# 優化您在Dynamic Media的映像質量的最佳做法 {#best-practices-for-optimizing-the-quality-of-your-images}

優化影像質量可能是一個耗時的過程，因為許多因素都有助於繪製可接受的結果。 結果部分是主觀的，因為個體對影像質量的看法不同。 結構化實驗是關鍵。

Adobe Experience Manager公司包括100多個Dynamic Media影像傳輸命令，用於調整和優化影像和渲染結果。 以下指南可幫助您簡化流程，並使用一些基本命令和最佳做法快速獲得良好效果。

## 映像格式的最佳做法(`&fmt=`) {#best-practices-for-image-format-fmt}

* JPG或PNG是提供高質量且尺寸和重量均可管理的影像的最佳選擇。
* 如果URL中未提供format命令，則Dynamic Media影像傳遞預設為傳遞JPG。
* JPG以10:1的比例進行壓縮，通常會產生較小的影像檔案大小。 PNG壓縮的比率約為2:1，但有時除外，例如當影像包含白色背景時。 但是，PNG檔案大小通常比JPG檔案大。
* JPG使用有損壓縮，這意味著在壓縮期間圖片元素（像素）會被丟棄。 而PNG則使用無損壓縮。
* JPG通常以比具有銳邊和對比度的合成影像更高的逼真度壓縮照片影像。
* 如果影像包含透明度，請使用PNG，因為JPG不支援透明度。

作為影像格式的最佳做法，請從最常見的設定開始 `&fmt=JPG`。

## 映像大小的最佳做法 {#best-practices-for-image-size}

動態減小影像大小是最常見的任務之一。 它涉及指定大小和（可選）用於縮小影像的縮小採樣模式。

* 對於影像大小調整，最好、最直接的方法是使用 `&wid=<value>` 和 `&hei=<value>,`或者 `&hei=<value>`。 這些參數根據縱橫比自動設定影像寬度。
* `&resMode=<value>`控制用於下採樣的算法。 開始於 `&resMode=sharp2`。 此值提供最佳影像質量。 使用縮減採樣時 `value =bilin` 速度更快，通常會導致偽像的混淆。

作為影像調整的最佳做法，請使用 `&wid=<value>&hei=<value>&resMode=sharp2` 或 `&hei=<value>&resMode=sharp2`

## 用於影像銳化的最佳做法 {#best-practices-for-image-sharpening}

影像銳化是控制網站上影像的最複雜方面，在這些方面會犯很多錯誤。 請花點時間瞭解有關銳化和反銳化掩碼在Experience Manager中如何工作的更多資訊，參考以下有用資源：

最佳做法白皮書 [銳化Adobe Dynamic Media Classic](/help/assets/assets/sharpening_images.pdf) 也適用於Experience Manager。

<!-- To be reviewed and updated: Broken link.
See also [Sharpening an image with unsharp mask](https://helpx.adobe.com/photoshop/atv/cs6-tutorials/sharpening-an-image-with-unsharp-mask.html). -->

使用Experience Manager，您可以在攝取、遞送或兩者上銳化影像。 但是，通常只使用一種方法或另一種方法來銳化影像，但不同時使用兩種方法。 在遞送時銳化URL上的影像通常會獲得最佳結果。

可以使用兩種影像銳化方法：

* 簡單銳化( `&op_sharpen`) — 與在Photoshop使用的銳化濾鏡類似，簡單銳化將基本銳化應用於動態調整後影像的最終視圖。 但是，此方法不可用戶配置。 最佳做法是，除非需要，否則不使用&amp;op_sharpen。
* 反銳化掩碼( `&op_USM`) — 反銳化掩碼是行業標準銳化濾鏡。 最佳做法是按照下面的准則，使用反銳化掩碼來銳化影像。 通過取消銳化掩碼，可以控制以下三個參數：

   * `&op_sharpen=amount,radius,threshold`

      * **[!UICONTROL *金額&#x200B;*]**（0-5，效果強度）。
      * **[!UICONTROL *半徑&#x200B;*]**(0-250，「銳化線」圍繞銳化對象繪製的寬度（以像素為單位）。)

      請記住，參數半徑和量是相互作用的。 通過增加數量可以補償減小的半徑。 半徑允許更精細的控制，因為較低值僅會銳化邊緣像素，而較高值會銳化較寬的像素帶。

      * **[!UICONTROL *閾值&#x200B;*]**（0-255，效果敏感。）

             此參數可決定銳化像素與周圍區域的差異程度，之後才會被視為邊緣像素，濾鏡會銳化這些像素。**[!UICONTROL threshold]**參數有助於避免色彩相似的區域過度銳利化，例如膚色。例如，閾值為12會忽略膚色亮度的微小變化，以避免加上「雜訊」，同時仍會加上邊緣對比度至高對比區域，例如睫毛與皮膚相遇的區域。
         
         有關如何設定這三個參數（包括與篩選器一起使用的最佳做法）的詳細資訊，請參閱以下資源：

         Experience Manager銳化影像的幫助主題。

         最佳做法白皮書 [銳化Adobe Dynamic Media Classic](/help/assets/assets/sharpening_images.pdf)。

      * Experience Manager還允許您控制第四個參數：單色(0,1)。 此參數確定是否使用值0將反銳化掩蔽分別應用於每個顏色分量，或使用值1將反銳化掩蔽應用於影像亮度/強度。


最佳做法是從非銳化蒙版半徑參數開始。 可以開始的半徑設定如下：

* **[!UICONTROL 網站]** - 0.2-0.3像素
* **[!UICONTROL 照相印刷(250-300 ppi)]** - 0.3-0.5像素
* **[!UICONTROL 膠印(266-300 ppi)]** - 0.7-1.0像素
* **[!UICONTROL 畫布打印(150 ppi)]** - 1.5-2.0像素

逐步從1.75增加到4. 如果銳化仍不是您想要的方式，請將半徑增加一個小數點，然後再次運行從1.75到4的量。 根據需要重複。

將單色參數設定保留為0。

### JPEG壓縮的最佳做法(`&qlt=`) {#best-practices-for-jpeg-compression-qlt}

* 此參數控制JPG編碼質量。 值越高，影像質量越高，但檔案大小越大；或者，較低值表示較低質量的影像但較小的檔案大小。 此參數的範圍是0-100。
* 要優化質量，請不要將參數值設定為100。 設定90或95和100之間的差異幾乎是難以察覺的，但100不必要地增加了影像檔案的大小。 因此，要優化質量，同時避免影像檔案過大，請設定 `qlt= value` 到九十五歲。
* 要優化較小的影像檔案大小，但將影像質量保持在可接受的級別，請設定 `qlt= value` 到80 低於70到75的值會導致影像質量顯著下降。
* 作為最佳實踐，要在中間， `qlt= value` 到85歲才能留在中間。
* 在中使用色度標誌 `qlt=`

   * 的 `qlt=` 參數具有第二個設定，允許您使用值開啟RGB色度下採樣 `,1` 或取消使用值 `,0`。
   * 要保持其簡單性，請先關閉RGB色度下採樣(`,0`)。 該設定通常會獲得更好的影像質量，特別是對於具有大量銳邊和對比度的合成影像。

作為JPG壓縮使用的最佳做法 `&qlt=85,0`。

## JPEG規模調整的最佳做法(`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

jpegSize是一個有用的參數，如果您希望確保影像不會超過某個大小，以便傳輸到記憶體有限的設備。

* 此參數以千位元組(`jpegSize=&lt;size_in_kilobytes&gt;`)。 它定義了影像傳送允許的最大大小。
* `&jpegSize=` 與JPG壓縮參數交互 `&qlt=`。 如果JPG響應具有指定的JPG壓縮參數(`&qlt=`)未超過jpegSize值，則影像返回時 `&qlt=` 定義。 否則， `&qlt=` 會逐漸減少，直到映像達到允許的最大大小，或直到系統確定它無法適應並返回錯誤。

作為最佳做法， `&jpegSize=` 並添加參數 `&qlt=` 將JPG映像交付到記憶體有限的設備。

## 最佳做法摘要 {#best-practices-summary}

作為最佳實踐，要獲得高影像質量和小檔案大小，請從以下參陣列合開始：

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

這種設定組合在大多數情況下都會取得優異的效果。

如果影像需要進一步優化，則從半徑設定為0.2或0.3開始，逐漸微調銳化（反銳化）參數。然後，逐漸將這一數額從1.75增加到最多4(相當於Photoshop的400%)。 檢查以查看是否達到了預期結果。

如果銳化結果仍不令人滿意，則以小數增量增加半徑。 對於每個小數增量，以1.75重新啟動金額，並逐漸將其增加到4。 重複此過程，直到達到所需結果。 儘管上述價值觀是創意工作室已經驗證的方法，但請記住，你可以從其他價值觀開始，並遵循其他策略。 結果是否令人滿意是一個主觀問題，因此結構化實驗是關鍵。

在您進行實驗時，以下一般性建議有助於進一步優化您的工作流：

* 直接在URL上即時嘗試並test不同的參數。
* 作為最佳做法，請記住，可以將「Dynamic Media影像服務」命令分組到影像預設中。 影像預設基本上是具有自定義預設名稱(如 `$thumb_low$` 和 `&product_high$`。 URL路徑中的自定義預設名稱將調用這些預設。 此類功能可幫助您管理網站上不同影像使用模式的命令和質量設定，並縮短URL的總長度。
* Experience Manager還提供了更高級的調整影像質量的方法，例如對攝取應用銳化影像。 對於有選項可以調整和優化渲染結果的高級使用情形， [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html) 可以幫助您掌握定製的見解和最佳實踐。
