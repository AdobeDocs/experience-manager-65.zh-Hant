---
title: 自適應表單元件的內聯樣式
seo-title: Inline CSS properties for adaptive form components
description: 雖然可以在自適應表單上應用自定義樣式，但也可以在自適應表單的各個元件上應用內嵌CSS屬性。
seo-description: While you can apply custom styles on an adaptive form, you can also apply inline CSS properties on individual components of an adaptive form.
uuid: e863780e-2250-4bea-9569-22be5638d54e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 21dec713-c76d-408b-baea-fc585377b429
docset: aem65
feature: Adaptive Forms
exl-id: 67cfecb8-c31d-4192-904d-7bfaa1a31ea5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 2%

---

# 自適應表單元件的內聯樣式 {#inline-styling-of-adaptive-form-components}

通過使用指定樣式來定義自適應表單的整體外觀和樣式 [主題編輯器](../../forms/using/themes.md)。 此外，您還可以將內聯CSS樣式應用於單個自適應表單元件，並即時預覽更改。 內聯樣式會覆蓋主題中提供的樣式。

## 應用內聯CSS屬性 {#apply-inline-css-properties}

要向元件添加內聯樣式：

1. 在窗體編輯器中開啟窗體，並將模式更改為樣式模式。 要將模式更改為樣式模式，請在頁面工具欄中按一下 ![畫布下拉清單](assets/canvas-drop-down.png) > **樣式**。
1. 在頁面中選擇元件，然後按一下編輯按鈕 ![編輯按鈕](assets/edit-button.png)。 樣式屬性在邊欄中開啟。

   也可以從邊欄的表單層次結構樹中選擇元件。 表單層次結構樹在提要欄中可用作表單對象。

   也可以從邊欄中選擇元件。 在「樣式」模式下，可以看到「表單對象」(Form Objects)下列出的元件。 但是，邊欄中的「表單對象」清單會列出欄位和面板等元件。 欄位和面板是可包含文本框和單選按鈕等元件的通用元件。

   從提要欄中選擇元件時，將看到列出的所有子元件以及選定元件的屬性。 可以選擇特定的子元件並對其進行樣式化。

1. 按一下提要欄中的頁籤以指定CSS屬性。 可以指定屬性，如：

   * Dimension和位置（顯示設定、填充、高度、寬度、邊距、位置、z索引、浮動、清除、溢出）
   * 文本（字型系列、粗細、顏色、大小、行高和對齊方式）
   * 背景（影像和漸變，背景顏色）
   * 邊框（寬度、樣式、顏色、半徑）
   * 效果（陰影、容量）
   * 高級（用於為元件編寫自定義CSS）

1. 同樣，您可以為元件的其他部分應用樣式，如小部件、標題和幫助。
1. 點擊 **完成** 確認更改或 **取消** 來放棄更改。

## 示例：欄位元件的內聯樣式 {#example-inline-styles-for-a-field-component}

以下影像描述了在將內嵌樣式應用到它之前和之後的文本欄位。

![應用內聯樣式之前的文本框元件](assets/no-style.png)

應用內聯樣式屬性之前的文本框元件

注意在應用以下CSS屬性後，文本框樣式的更改如下圖所示。

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
   <td><p>邊框寬度=2px</p> <p>邊框樣式=實體</p> <p>邊框顏色=#1111</p> </td>
   <td><p>在欄位周圍建立黑色2px寬邊框</p> </td>
  </tr>
  <tr>
   <td><p>文本框</p> </td>
   <td><p>background-color</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>將背景顏色更改為CornflowerBlue(#6495ED)</p> <p>注：可以在值欄位中指定顏色名稱或其十六進位代碼。</p> </td>
  </tr>
  <tr>
   <td><p>標籤</p> </td>
   <td><p>尺寸和位置&gt;寬度</p> </td>
   <td><p>100px</p> </td>
   <td><p>將標籤的寬度固定為100px</p> </td>
  </tr>
  <tr>
   <td>欄位說明圖示</td>
   <td>文本&gt;字型顏色</td>
   <td>#2ECC40</td>
   <td>更改幫助表徵圖臉的顏色。</td>
  </tr>
  <tr>
   <td><p>長描述</p> </td>
   <td><p>text-align</p> </td>
   <td><p>中心點</p> </td>
   <td><p>將幫助的詳細說明與中心對齊</p> </td>
  </tr>
 </tbody>
</table>

![應用內聯樣式後的文本框樣式](assets/applied-style.png)

應用內聯樣式屬性後的文本框元件

按照上述步驟，您可以選擇和設定其他元件的樣式，如面板、提交按鈕和單選按鈕。

>[!NOTE]
>
>造型屬性會因所選元件而異。
