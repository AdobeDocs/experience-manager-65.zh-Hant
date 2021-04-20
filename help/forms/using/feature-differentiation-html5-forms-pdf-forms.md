---
title: HTML5表單與PDF forms的功能區隔
seo-title: HTML5表單與PDF forms的功能區隔
description: HTML5表格和PDF forms支援的功能
seo-description: HTML5表格和PDF forms支援的功能
uuid: 6ddee197-d108-4897-9976-77d115a06504
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdd97c20-d1f2-4898-9862-1a6a8071be88
docset: aem65
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# HTML5表單與PDF forms的功能區隔{#feature-differentiation-between-html-forms-and-pdf-forms}

下表指定HTML5表單和PDF forms的功能支援：

<table>
 <tbody>
  <tr>
   <th>功能</th>
   <th>HTML5 表單</th>
   <th>PDF</th>
  </tr>
  <tr>
   <td>條形碼<br /> </td>
   <td>不適用於使用者介面層級。 </td>
   <td>支援</td>
  </tr>
  <tr>
   <td>簽名欄位<br /> </td>
   <td><strong>不支</strong> 援數位簽章，但會針對 <strong>紙本</strong> 檔案（如簽章）新增新的Scribble Signature欄位。您可以使用<strong>Scribble Signature</strong>欄位，在表格上塗鴉其簽名。 簽名會儲存在表單中，做為影像。 您可以在<strong>塗鴉簽名</strong>欄位中儲存地理位置資訊。</td>
   <td><strong>數位簽名</strong>的簽名欄位。</td>
  </tr>
  <tr>
   <td>資料合併</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>影像</td>
   <td>資料URI方案用於顯示影像。 所有最新版瀏覽器都支援此配置，但每個瀏覽器支援的影像格式範圍有差異。<br /> </td>
   <td>支援。gif、.png、.jpeg、.bmp和。tiff格式。</td>
  </tr>
  <tr>
   <td>分頁<br /> </td>
   <td><p>HTML5表格會分割為面板和方塊，讓其外觀與PDF forms類似。 頁面大小會動態計算。 如果HTML5表單中的頁面內容全部被刪除或標示為隱藏，則空白頁面會隱藏，空白頁面上方和下方的頁面之間不會顯示空白（空白空間）。</p> <p>如果資料合併或指令碼將內容新增至頁面，則頁面的長度會擴充以容納新新增的內容。 表單中不會新增任何頁面，以容納新增的內容。 </p> <p><strong>注意：</strong> 當HTML5表單中的頁面內容全部刪除或標示為隱藏時，第1頁和第2頁之間仍會顯示空白頁面（空白字元），但其他頁面之間不會顯示空白頁面。</p> </td>
   <td>PDF中的分頁取決於合併的資料內容或使用者內容，而且會根據此內容增加／減少頁數。</td>
  </tr>
  <tr>
   <td>頁首／頁尾 </td>
   <td>支援。<br /> <br /> 由於HTML5行動表單不支援分頁，因此頁首和頁尾只會顯示一次。不過，您可以在版面中設定它們，以便在行動表單預覽的多個位置顯示。<br /> </td>
   <td>支援。</td>
  </tr>
  <tr>
   <td>自訂Widget</td>
   <td>您可以自訂Widget，以增強行動裝置上的使用者體驗。<br /> </td>
   <td>所有Widget都已鎖定，無法插入任何自訂Widget。<br /> </td>
  </tr>
  <tr>
   <td>XFA指令碼API</td>
   <td>支援最常用的XFA指令碼結構。 有關支援的構造的詳細資訊清單，請參見<a href="/help/forms/using/scripting-support.md">指令碼支援</a>。</td>
   <td>支援所有XFA指令碼結構。</td>
  </tr>
  <tr>
   <td>Acrobat指令碼API </td>
   <td>HTML5表格支援最常用的API。 如需詳細資訊，請參閱<a href="/help/forms/using/scripting-support.md">指令碼支援</a>。</td>
   <td>如果PDF檔案是在Acrobat或Reader內開啟，也支援Acrobat提供的所有指令碼API。</td>
  </tr>
  <tr>
   <td>支援從右到左語言 </td>
   <td>支援</td>
   <td>支援</td>
  </tr>
 </tbody>
</table>

<!--Follow the best practices to enable a form template for HTML5 renditions and ensure that the behavior and appearance of HTML5 forms and XFA-based PDF is consistent. For detailed list of best practices, see [Best practices to design an HTML5 form.](/help/forms/using/best-practices-design-html5-forms.md)-->
