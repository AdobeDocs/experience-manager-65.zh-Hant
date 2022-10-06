---
title: Acrobat Reader DC擴充功能使用的憑證類型
seo-title: Certificate types used by Acrobat Reader DC extensions
description: 了解Acrobat Reader DC擴充功能使用的憑證類型。
seo-description: Learn about the certificate types used by Acrobat Reader DC extensions.
uuid: 93c02abc-2d5a-44ed-b93c-981afbd0553d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 331b9317-87b5-4a96-a1bc-429675ff90c5
exl-id: 800bffd5-0cdc-4251-bba4-e350f226f019
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 4%

---

# Acrobat Reader DC擴充功能使用的憑證類型 {#certificate-types-used-by-acrobat-reader-dc-extensions}

憑證檢視器提供憑證的下列相關資訊：

* 憑證「好記」名稱
* 憑證設定檔
* 有效期限
* Acrobat Reader DC擴充功能使用權限

## 憑證「好記」名稱 {#certificate-friendly-name}

Acrobat Reader DC擴充功能憑證的「好記」名稱是描述憑證屬性的字串，如下列範例所示：

是2D條形碼完整生產版V6.1 P8 0002054

字串包含下列元素：

**證書類型：** 說明憑證會啟用的AEM表單模組，以及啟動的層級，例如ARE 2D條碼已滿。 如需可用憑證類型的清單，請參閱「憑證設定檔」區段中表格中的「類型」欄。

**部署類型：** 指出憑證的預期用途，例如生產。 值可以是「評估」(Evaluation)或「生產」(Production)。 有關與每個證書類型關聯的部署類型的清單，請參閱「證書配置檔案」部分表中的「部署類型」列。

**使用權版本：** 說明憑證可用於的使用權限演算法版本，例如V6.1。此版本不表示Acrobat或Acrobat Reader DC擴充功能的版本。

**設定檔代碼：** 設定檔程式碼是完整憑證屬性的簡稱，例如P8。 有關與每個檔案類型關聯的配置檔案代碼的清單，請參閱「證書配置檔案」部分表中的「配置檔案代碼」列。

**序列號：** 系統會為Adobe核發的每個憑證指派序列號，例如0002054。 Adobe企業支援或Adobe企業客戶代表可以使用此序列號跟蹤特定產品訂單或OEM關係的證書。

## 憑證設定檔 {#certificate-profiles}

下表列出分析Acrobat Reader DC擴充功能憑證時可能遇到的憑證設定檔。

<table>
 <thead>
  <tr>
   <th><p>設定檔程式碼</p></th>
   <th><p>類型</p></th>
   <th><p>有效期限</p></th>
   <th><p>部署類型</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>P1</p></td>
   <td><p>SAP生產</p></td>
   <td><p>最大值</p></td>
   <td><p>生產</p></td>
  </tr>
  <tr>
   <td><p>P2</p></td>
   <td><p>SAP內部測試</p></td>
   <td><p>2年</p></td>
   <td><p>評估和測試</p></td>
  </tr>
  <tr>
   <td><p>P3</p></td>
   <td><p>Acrobat Reader DC擴充功能，生產</p></td>
   <td><p>最大值</p></td>
   <td><p>生產</p></td>
  </tr>
  <tr>
   <td><p>P4</p></td>
   <td><p>Acrobat Reader DC擴充功能，內部Adobe使用</p></td>
   <td><p>2年</p></td>
   <td><p>生產</p></td>
  </tr>
  <tr>
   <td><p>P5</p></td>
   <td><p>Acrobat Reader DC擴充功能，合作夥伴整合</p></td>
   <td><p>2年</p></td>
   <td><p>評估和測試</p></td>
  </tr>
  <tr>
   <td><p>P6</p></td>
   <td><p>Acrobat Reader DC擴充功能，評估</p></td>
   <td><p>60 天</p></td>
   <td><p>評估</p></td>
  </tr>
  <tr>
   <td><p>P8</p></td>
   <td><p>Forms，生產</p></td>
   <td><p>最大值</p></td>
   <td><p>生產</p></td>
  </tr>
  <tr>
   <td><p>P9</p></td>
   <td><p>Adobe Acrobat 7.x，生產</p></td>
   <td><p>最大值</p></td>
   <td><p>生產</p></td>
  </tr>
  <tr>
   <td><p>I10</p></td>
   <td><p>Forms;可供OEM使用。</p></td>
   <td><p>最大值</p></td>
   <td><p>生產與評估</p></td>
  </tr>
  <tr>
   <td><p>I11</p></td>
   <td><p>Forms;可供OEM使用。</p></td>
   <td><p>最大值</p></td>
   <td><p>生產與評估</p></td>
  </tr>
  <tr>
   <td><p>I12</p></td>
   <td><p>僅簽名；可供OEM使用。</p></td>
   <td><p>最大值</p></td>
   <td><p>生產與評估</p></td>
  </tr>
  <tr>
   <td><p>I13</p></td>
   <td><p>僅限離線注釋；可供OEM使用。</p></td>
   <td><p>最大值</p></td>
   <td><p>生產與評估</p></td>
  </tr>
  <tr>
   <td><p>I14</p></td>
   <td><p>僅供評論；可供OEM使用。</p></td>
   <td><p>最大值</p></td>
   <td><p>生產與評估</p></td>
  </tr>
  <tr>
   <td><p>I15</p></td>
   <td><p>完整權限；可供OEM使用。</p></td>
   <td><p>最大值</p></td>
   <td><p>生產與評估</p></td>
  </tr>
 </tbody>
</table>

## 有效期限 {#validity-period}

評估證書頒發給客戶和開發人員，以便他們能夠評估和開發產品的示例應用程式。 這些證書的有效期為60至90天。 在問題資料後的第二個月結束時到期。

合作夥伴整合證書頒發給Adobe業務合作夥伴，以支援軟體開發、整合、建立原型和演示。 該等憑證自發行日期起計有效期為兩年。

Adobe內部使用憑證用於Adobe內，以支援軟體開發、整合、建立原型和示範。 該等憑證自發行日期起計有效期為兩年。

生產憑證會核發給購買Acrobat Reader DC擴充功能的客戶。 這些證書在證書頒發機構(CA)允許的最長期限內有效，如下所示 *Max* (在「證書配置檔案」(Certificate Profiles)表格中)。

## Acrobat Reader DC擴充功能使用權限 {#acrobat-reader-dc-extensions-usage-rights}

當您在憑證檢視器中檢查Acrobat Reader DC擴充功能憑證時，可以從「詳細資訊」標籤中選取使用權限項目（如果已設定），以查看憑證可啟用的Adobe Reader使用權限明細清單。 在特定文檔上啟用的使用權限可以是證書所啟用的使用權限的子集。

如果在非協作環境中需要聯機注釋，請聯繫Adobe支援以了解詳細資訊。 Mode屬性與部署類型匹配，且為 *生產* 或 *評價*.

允許的Acrobat Reader DC擴充功能使用權限包含一或多個特定元素。 這些元素被用於不同的組合中，以實現各種授權產品功能。

<table>
 <thead>
  <tr>
   <th><p>使用權限元素</p></th>
   <th><p>檢視已啟用權限的PDF檔案時在Adobe Reader中啟用的功能</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>FormFillInAndSave</p></td>
   <td><p>填寫表單欄位並將檔案儲存在本機。</p></td>
  </tr>
  <tr>
   <td><p>FormImportExport</p></td>
   <td><p>將表單資料匯入和匯出為FDF、XFDF、XML和XDP檔案。</p></td>
  </tr>
  <tr>
   <td><p>FormAddDelete</p></td>
   <td><p>添加、更改或刪除PDF表單上的欄位和欄位屬性。</p></td>
  </tr>
  <tr>
   <td><p>SubmitStandalone</p></td>
   <td><p>當資料未在瀏覽器工作階段中執行時，以電子郵件或離線方式提交至伺服器。</p></td>
  </tr>
  <tr>
   <td><p>SpawnTemplate</p></td>
   <td><p>從相同PDF表單內的範本頁面建立頁面。</p></td>
  </tr>
  <tr>
   <td><p>正在簽署</p></td>
   <td><p>以數位方式簽署和儲存PDF檔案，並清除數位簽名。</p></td>
  </tr>
  <tr>
   <td><p>AnnotModify</p></td>
   <td><p>建立和修改文檔注釋，如注釋。</p></td>
  </tr>
  <tr>
   <td><p>AnnotImportExport</p></td>
   <td><p>將注釋（如注釋）保存在單獨的資料檔案中，並從檔案載入注釋。</p></td>
  </tr>
  <tr>
   <td><p>BarcodePlatext</p></td>
   <td><p>打印以未加密形式對表單資料進行條碼編碼的文檔，該格式不需要授權伺服器軟體進行解碼。</p></td>
  </tr>
  <tr>
   <td><p>AnnotOnline</p></td>
   <td><p>從線上文檔審閱和注釋伺服器上載和下載注釋（如注釋）。</p></td>
  </tr>
  <tr>
   <td><p>FormOnline</p></td>
   <td><p>連接到在PDF表單中定義的Web服務或資料庫。</p></td>
  </tr>
  <tr>
   <td><p>EFModif</p></td>
   <td><p>修改與PDF文檔關聯的嵌入檔案對象。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Acrobat Reader DC擴充功能的使用權限，只能透過搭配使用的特定組合，從Adobe取得授權。 無法單獨授權這些功能。 如需可用使用權組合的相關資訊，請聯絡AEM Forms客戶代表。
