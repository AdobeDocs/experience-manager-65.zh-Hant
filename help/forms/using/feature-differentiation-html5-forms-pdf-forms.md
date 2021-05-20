---
title: HTML5表單和PDF forms的功能差異
seo-title: HTML5表單和PDF forms的功能差異
description: HTML5表單和PDF forms支援的功能
seo-description: HTML5表單和PDF forms支援的功能
uuid: 6ddee197-d108-4897-9976-77d115a06504
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdd97c20-d1f2-4898-9862-1a6a8071be88
docset: aem65
feature: 行動表單
exl-id: 3150f95f-7150-4eee-b5a9-121422dec2a1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 3%

---

# HTML5表單與PDF forms的功能差異{#feature-differentiation-between-html-forms-and-pdf-forms}

下表指定HTML5表單和PDF forms的功能支援：

<table>
 <tbody>
  <tr>
   <th>功能</th>
   <th>HTML5 表單</th>
   <th>PDF</th>
  </tr>
  <tr>
   <td>條碼<br /> </td>
   <td>在用戶介面級別不可用。 </td>
   <td>支援</td>
  </tr>
  <tr>
   <td>簽名欄位<br /> </td>
   <td><strong>不支</strong> 援數位簽名，但已為 <strong>紙</strong> 面文字（如簽名）新增手寫簽名欄位。您可以使用<strong>手寫簽名</strong>欄位在表單上手寫簽名。 簽名將作為影像保存在窗體上。 您可以在<strong>手寫簽名</strong>欄位中保存地理位置資訊。</td>
   <td><strong>數字簽名</strong>可用的簽名欄位。</td>
  </tr>
  <tr>
   <td>資料合併</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>影像</td>
   <td>資料URI配置用於顯示影像。 所有新版瀏覽器均支援此配置，但每個瀏覽器支援的影像格式範圍有差異。<br /> </td>
   <td>支援.gif、.png、.jpeg、.bmp和.tiff格式。</td>
  </tr>
  <tr>
   <td>分頁<br /> </td>
   <td><p>HTML5表單會分為面板和方塊，提供與PDF forms類似的外觀。 頁面大小會動態計算。 如果刪除或標籤HTML5表單中某頁的所有內容，則隱藏空白頁，且空白頁上方和下方的頁面之間不會顯示空白字元（空白字元）。</p> <p>如果資料合併或指令碼將內容新增至頁面，則頁面的長度會擴展以容納新新增的內容。 表單中不會新增任何頁面以容納新新增的內容。 </p> <p><strong>注意：</strong> 刪除或標示隱藏HTML5表單中的頁面所有內容後，第1頁和第2頁之間仍會顯示空白頁面（空白字元），但其他頁面之間不會顯示空白頁面。</p> </td>
   <td>PDF中的分頁取決於合併的資料內容或使用者內容，而頁面計數也會隨之增加/減少。</td>
  </tr>
  <tr>
   <td>頁首/頁尾 </td>
   <td>支援。<br /> <br /> 由於HTML5行動表單不支援分頁，因此頁首和頁尾只會顯示一次。不過，您可以在版面中設定它們，以在行動表單預覽的多個位置顯示。<br /> </td>
   <td>支援。</td>
  </tr>
  <tr>
   <td>自訂介面工具集</td>
   <td>您可以自訂Widget以增強行動裝置上的使用者體驗。<br /> </td>
   <td>所有小部件都被鎖定，無法插入自定義小部件。<br /> </td>
  </tr>
  <tr>
   <td>XFA指令碼API</td>
   <td>支援最常使用的XFA指令碼結構。 有關支援的構造的詳細資訊，請參閱<a href="/help/forms/using/scripting-support.md">指令碼支援</a>。</td>
   <td>支援所有XFA指令碼結構。</td>
  </tr>
  <tr>
   <td>Acrobat指令碼API </td>
   <td>HTML5表單支援最常使用的API。 如需詳細資訊，請參閱<a href="/help/forms/using/scripting-support.md">指令碼支援</a>。</td>
   <td>如果PDF檔案是在Acrobat或Reader內開啟，也支援Acrobat提供的所有指令碼API。</td>
  </tr>
  <tr>
   <td>支援由右至左語言 </td>
   <td>支援</td>
   <td>支援</td>
  </tr>
 </tbody>
</table>

<!--Follow the best practices to enable a form template for HTML5 renditions and ensure that the behavior and appearance of HTML5 forms and XFA-based PDF is consistent. For detailed list of best practices, see [Best practices to design an HTML5 form.](/help/forms/using/best-practices-design-html5-forms.md)-->
