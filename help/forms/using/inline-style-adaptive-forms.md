---
title: 最適化表單元件的內嵌樣式
seo-title: 最適化表單元件的內嵌CSS屬性
description: 雖然您可以在最適化表單上套用自訂樣式，但您也可以在最適化表單的個別元件上套用內嵌CSS屬性。
seo-description: 雖然您可以在最適化表單上套用自訂樣式，但您也可以在最適化表單的個別元件上套用內嵌CSS屬性。
uuid: e863780e-2250-4bea-9569-22be5638d54e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 21dec713-c76d-408b-baea-fc585377b429
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 最適化表單元件的內嵌樣式{#inline-styling-of-adaptive-form-components}

您可以使用主題編輯器指定樣式，以定義最適化表單的整體外 [觀和樣式](../../forms/using/themes.md)。 此外，您也可以將內嵌CSS樣式套用至個別的可調式表單元件，並即時預覽變更。 內嵌樣式會覆寫主題中提供的樣式。

## 套用內嵌CSS屬性 {#apply-inline-css-properties}

若要新增內嵌樣式至元件：

1. 在表單編輯器中開啟您的表單，並將模式變更為樣式模式。 若要將模式變更為樣式模式，請在頁面工具列中，點選「畫 ![布下拉式清單](assets/canvas-drop-down.png) >樣 **式」**。
1. 在頁面中選取元件，然後點選「編輯」按鈕 ![edit-button](assets/edit-button.png)。 樣式屬性會在側欄中開啟。

   您也可以從側欄的表單階層樹狀結構中選取元件。 表單階層樹狀結構在側欄中可作為表單物件使用。

   您也可以從側欄選取元件。 在「樣式」模式中，您可以看到「表單對象」(Form Objects)下列出的元件。 不過，側欄中的「表單物件」清單會列出欄位和面板等元件。 欄位和面板是可包含元件（例如文字方塊和選項按鈕）的通用元件。

   從邊欄中選擇元件時，您會看到列出的所有子元件以及所選元件的屬性。 您可以選取特定的子元件並設定其樣式。

1. 按一下側邊欄中的標籤以指定CSS屬性。 您可以指定屬性，例如：

   * 尺寸與位置（顯示設定、填補、高度、寬度、邊界、位置、z索引、浮動、清除、溢位）
   * 文字（字型系列、粗細、顏色、大小、行高和對齊）
   * 背景（影像和漸層、背景顏色）
   * 邊框（寬度、樣式、顏色、半徑）
   * 特效（陰影、洞察力）
   * 進階（可讓您編寫元件的自訂CSS）

1. 同樣地，您也可以套用元件其他部分的樣式，例如Widget、Caption和Help。
1. 點選 **「完成** 」以確認變更，或點選「取 **消** 」以放棄變更。

## 範例：欄位元件的內嵌樣式 {#example-inline-styles-for-a-field-component}

下列影像會描述套用內嵌樣式前後的文字欄位。

![套用內嵌樣式之前的文字方塊元件](assets/no-style.png)

應用內嵌樣式屬性之前的文本框元件

請注意，套用下列CSS屬性後，文字方塊樣式的變更如下圖所示。

<table>
 <tbody>
  <tr>
   <td><p>選擇器</p> </td>
   <td><p>CSS屬性</p> </td>
   <td><p>值</p> </td>
   <td><p>效果</p> </td>
  </tr>
  <tr>
   <td><p>欄位</p> </td>
   <td><p>邊界</p> </td>
   <td><p>邊框寬度= 2px</p> <p>邊框樣式=實線</p> <p>邊框顏色=#1111</p> </td>
   <td><p>在欄位周圍建立2像素寬的黑色邊框</p> </td>
  </tr>
  <tr>
   <td><p>文字方塊</p> </td>
   <td><p>background-color</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>將背景顏色更改為CornflowerBlue(#6495ED)</p> <p>注意：您可以在值欄位中指定顏色名稱或其十六進位代碼。</p> </td>
  </tr>
  <tr>
   <td><p>標籤</p> </td>
   <td><p>尺寸與位置&gt;寬度</p> </td>
   <td><p>100px</p> </td>
   <td><p>將標籤的寬度修正為100像素</p> </td>
  </tr>
  <tr>
   <td>欄位說明圖示</td>
   <td>「文字&gt;字型顏色」</td>
   <td>#2ECC40</td>
   <td>變更說明圖示臉部的顏色。</td>
  </tr>
  <tr>
   <td><p>詳細說明</p> </td>
   <td><p>text-align</p> </td>
   <td><p>中心點</p> </td>
   <td><p>將詳細說明對齊</p> </td>
  </tr>
 </tbody>
</table>

![套用內嵌樣式後的文字方塊樣式](assets/applied-style.png)

套用內嵌樣式屬性後的文字方塊元件

依照上述步驟，您可以選取其他元件並設定其樣式，例如面板、提交按鈕和選項按鈕。

>[!NOTE]
>
>樣式屬性會根據您選取的元件而有所不同。

