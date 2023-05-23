---
title: HTML5形式與PDF forms的特徵區分
seo-title: Feature differentiation between HTML5 forms and PDF forms
description: HTML5表單和PDF forms中支援的功能
seo-description: Feature supported in HTML5 forms and PDF forms
uuid: 6ddee197-d108-4897-9976-77d115a06504
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdd97c20-d1f2-4898-9862-1a6a8071be88
docset: aem65
feature: Mobile Forms
exl-id: 3150f95f-7150-4eee-b5a9-121422dec2a1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 2%

---

# HTML5形式與PDF forms的特徵區分 {#feature-differentiation-between-html-forms-and-pdf-forms}

下表指定了為HTML5表單和PDF forms提供的功能支援：

<table>
 <tbody>
  <tr>
   <th>功能</th>
   <th>HTML5 Forms</th>
   <th>PDF</th>
  </tr>
  <tr>
   <td>條形碼<br /> </td>
   <td>在用戶介面級別不可用。 </td>
   <td>支援</td>
  </tr>
  <tr>
   <td>簽名欄位<br /> </td>
   <td><strong>數字簽名</strong> 不支援，但是新 <strong>Scribble簽名</strong> 將為類似紙面簽名添加欄位。 你可以用 <strong>Scribble簽名</strong> 的子菜單。 簽名將作為影像保存在表單上。 可以在 <strong>Scribble簽名</strong> 的子菜單。</td>
   <td>簽名欄位可用於 <strong>數字簽名</strong>。</td>
  </tr>
  <tr>
   <td>資料合併</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>影像</td>
   <td>資料URI方案用於顯示影像。 所有現代版本的瀏覽器都支援此方案，但每個瀏覽器支援的影像格式範圍存在差異。<br /> </td>
   <td>支援.gif、.png、.jpeg、.bmp和.tiff格式。</td>
  </tr>
  <tr>
   <td>分頁<br /> </td>
   <td><p>將HTML5形式分成面板和框，使其外觀類似於PDF forms。 動態計算頁面大小。 如果HTML5窗體中的頁面的所有內容都被刪除或標籤為隱藏，則空白頁面將被隱藏，並且空白頁面上方和下方的頁面之間不顯示空白（空白空間）。</p> <p>如果資料合併或指令碼將內容添加到頁面，則頁面的長度將擴展以容納新添加的內容。 表單中不會添加新頁面以容納新添加的內容。 </p> <p><strong>注：</strong> 當HTML5窗體中某頁的所有內容被刪除或標籤為隱藏時，空白頁（空白空間）在第1頁和第2頁之間仍可見，但在任何其他頁之間則不可見。</p> </td>
   <td>PDF中的分頁取決於合併的資料內容或用戶內容，並且根據它增加/減少頁數。</td>
  </tr>
  <tr>
   <td>頁眉/頁腳 </td>
   <td>支援. <br /> <br /> 由於HTML5移動表單不支援分頁符，因此頁眉和頁腳只顯示一次。 但是，您可以在佈局中將它們設定為在移動表單預覽的多個位置顯示。<br /> </td>
   <td>支援。</td>
  </tr>
  <tr>
   <td>自定義小部件</td>
   <td>可以定制小部件以增強移動設備上的用戶體驗。<br /> </td>
   <td>所有小部件都已鎖定，無法插入任何自定義小部件。<br /> </td>
  </tr>
  <tr>
   <td>XFA指令碼API</td>
   <td>支援最常用的XFA指令碼結構。 有關支援的結構的詳細資訊清單，請參見 <a href="/help/forms/using/scripting-support.md">指令碼支援</a>。</td>
   <td>支援所有XFA指令碼結構。</td>
  </tr>
  <tr>
   <td>Acrobat指令碼API </td>
   <td>HTML5表單支援最常用的API。 有關詳細資訊，請參閱 <a href="/help/forms/using/scripting-support.md">指令碼支援</a>。</td>
   <td>如果PDF檔案在Acrobat或Reader內開啟，它還支援Acrobat提供的所有指令碼API。</td>
  </tr>
  <tr>
   <td>支援從右到左的語言 </td>
   <td>支援</td>
   <td>支援</td>
  </tr>
 </tbody>
</table>

<!--Follow the best practices to enable a form template for HTML5 renditions and ensure that the behavior and appearance of HTML5 forms and XFA-based PDF is consistent. For detailed list of best practices, see [Best practices to design an HTML5 form.](/help/forms/using/best-practices-design-html5-forms.md)-->
