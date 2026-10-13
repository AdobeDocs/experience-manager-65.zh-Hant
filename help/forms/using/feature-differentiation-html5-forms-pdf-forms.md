---
title: HTML5 表單和 PDF 表單之間的功能差異
description: 瞭解HTML5 Forms和PDF forms之間的功能差異。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 3150f95f-7150-4eee-b5a9-121422dec2a1
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 6%
---
# HTML5 表單和 PDF 表單之間的功能差異 {#feature-differentiation-between-html-forms-and-pdf-forms}

下表指定為HTML5 Forms和PDF forms提供的功能支援：

<table>
 <tbody>
  <tr>
   <th>功能</th>
   <th>HTML5 表單</th>
   <th>PDF</th>
  </tr>
  <tr>
   <td>條碼<br /> </td>
   <td>在使用者介面層級無法使用。 </td>
   <td>支援</td>
  </tr>
  <tr>
   <td>簽章欄位<br /> </td>
   <td>不支援<strong>數位簽章</strong>，但已新增新的<strong>草寫簽章</strong>欄位，以供類似紙本的簽章使用。 可以使用<strong>草寫簽名</strong>欄位在表單上草寫簽名。 簽名會以影像形式儲存在表單上。 您可以在<strong>手寫簽名</strong>欄位中儲存地理位置資訊。</td>
   <td><strong>數位簽章</strong>可用的簽章欄位。</td>
  </tr>
  <tr>
   <td>資料合併</td>
   <td>支援</td>
   <td>支援</td>
  </tr>
  <tr>
   <td>影像</td>
   <td>資料URI配置用於顯示影像。 所有新版的瀏覽器都支援此配置，但每個瀏覽器支援的影像格式範圍有所不同。<br /> </td>
   <td>支援.gif、.png、.jpeg、.bmp及.tiff格式。</td>
  </tr>
  <tr>
   <td>分頁<br /> </td>
   <td><p>HTML5表單會分成多個面板和方塊，以提供類似於PDF forms的外觀。 頁面大小會以動態方式計算。 如果HTML5表單中頁面的所有內容已刪除或標籤為隱藏，則會隱藏空白頁面。 空白頁面上方和下方頁面之間不會顯示空白字元（空格）。</p> <p>如果資料合併或指令碼新增內容至頁面，則頁面長度會展開以容納新新增的內容。 不會將任何新頁面新增至表單，以容納新新增的內容。 </p> <p><strong>注意：</strong>當HTML5表單中某個頁面的所有內容被刪除或標籤為隱藏時，在第一頁和第二頁之間會保持可見的空白頁面（空格），但在其他任何頁面之間則不會保持可見。</p> </td>
   <td>PDF中的分頁視合併的資料內容或使用者內容而定，頁面計數會據此增加/減少。</td>
  </tr>
  <tr>
   <td>頁首/頁尾 </td>
   <td>支援。<br /> <br /> 由於HTML5行動表單不支援分頁，所以頁首和頁尾只會出現一次。 不過，您可以在版面中設定這些引數，使其顯示在行動表單預覽中的多個位置。<br /> </td>
   <td>支援。</td>
  </tr>
  <tr>
   <td>自訂Widget</td>
   <td>可以自訂Widget來增強行動裝置上的使用者體驗。<br /> </td>
   <td>所有Widget都已鎖定，無法插入任何自訂Widget。<br /> </td>
  </tr>
  <tr>
   <td>XFA指令碼API</td>
   <td>支援最常用的XFA指令碼建構。 如需支援的建構詳細清單，請參閱<a href="/help/forms/using/scripting-support.md">指令碼支援</a>。</td>
   <td>支援所有XFA指令碼建構。</td>
  </tr>
  <tr>
   <td>Acrobat指令碼API </td>
   <td>HTML5表單支援最常用的API。 如需詳細資訊，請參閱<a href="/help/forms/using/scripting-support.md">指令碼支援</a>。</td>
   <td>如果在Acrobat或Reader中開啟PDF檔案，也支援Acrobat提供的所有指令碼API。</td>
  </tr>
  <tr>
   <td>支援由右至左語言 </td>
   <td>支援</td>
   <td>支援</td>
  </tr>
 </tbody>
</table>

<!--Follow the best practices to enable a form template for HTML5 renditions and ensure that the behavior and appearance of HTML5 forms and XFA-based PDF is consistent. For detailed list of best practices, see [Best practices to design an HTML5 form.](/help/forms/using/best-practices-design-html5-forms.md)-->
