---
title: Acrobat Reader DC擴充功能使用的憑證類型
seo-title: Acrobat Reader DC擴充功能使用的憑證類型
description: 瞭解Acrobat Reader DC擴充功能使用的憑證類型。
seo-description: 瞭解Acrobat Reader DC擴充功能使用的憑證類型。
uuid: 93c02abc-2d5a-44ed-b93c-981afbd0553d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 331b9317-87b5-4a96-a1bc-429675ff90c5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Acrobat Reader DC擴充功能使用的憑證類型 {#certificate-types-used-by-acrobat-reader-dc-extensions}

「憑證檢視器」提供下列憑證相關資訊：

* 證書「友好」名稱
* 憑證設定檔
* 有效期
* Acrobat Reader DC擴充功能的使用權限

## 證書「友好」名稱 {#certificate-friendly-name}

Acrobat Reader DC擴充功能憑證的「好記」名稱是描述憑證屬性的字串，如下列範例所示：

ARE 2D條形碼完整生產V6.1 P8 0002054

字串包含下列元素：

**** 憑證類型：說明憑證所啟動的AEM表單模組，以及啟動的層級，例如ARE 2D Barcode Full。 有關可用證書類型的清單，請參閱「證書配置檔案」部分表格中的「類型」列。

**** 部署類型：指出憑證的預定用途，例如「生產」。 值可以是「評估」或「生產」。 有關與每個證書類型關聯的部署類型清單，請參閱「證書配置檔案」部分表格中的「部署類型」列。

**** 使用權限版本：說明憑證可用於的使用權限演算法版本，例如V6.1。此版本不表示Acrobat或Acrobat Reader DC擴充功能的版本。

**** 描述檔代碼：描述檔程式碼是完整憑證屬性的速記說明，例如P8。 有關與每種檔案類型關聯的配置檔案代碼的清單，請參閱「證書配置檔案」部分表格中的「配置檔案代碼」列。

**** 序號：Adobe核發的每個憑證都會指派序號，例如0002054。 Adobe企業支援或Adobe企業客戶代表可以使用此序號，將憑證追蹤至特定產品訂單或OEM關係。

## 憑證設定檔 {#certificate-profiles}

下表列出您分析Acrobat Reader DC擴充功能憑證時可能遇到的憑證設定檔。

<table>
 <thead>
  <tr>
   <th><p>描述檔代碼</p></th>
   <th><p>類型</p></th>
   <th><p>有效期</p></th>
   <th><p>部署類型</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>P1</p></td>
   <td><p>SAP Production</p></td>
   <td><p>最大值</p></td>
   <td><p>生產</p></td>
  </tr>
  <tr>
   <td><p>P2</p></td>
   <td><p>SAP內部測試</p></td>
   <td><p>2年</p></td>
   <td><p>評估與測試</p></td>
  </tr>
  <tr>
   <td><p>P3</p></td>
   <td><p>Acrobat Reader DC擴充功能，Production</p></td>
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
   <td><p>評估與測試</p></td>
  </tr>
  <tr>
   <td><p>P6</p></td>
   <td><p>Acrobat Reader DC擴充功能，評估版</p></td>
   <td><p>60天</p></td>
   <td><p>評估</p></td>
  </tr>
  <tr>
   <td><p>P8</p></td>
   <td><p>表單、製作</p></td>
   <td><p>最大值</p></td>
   <td><p>生產</p></td>
  </tr>
  <tr>
   <td><p>P9</p></td>
   <td><p>Adobe Acrobat 7.x,Production</p></td>
   <td><p>最大值</p></td>
   <td><p>生產</p></td>
  </tr>
  <tr>
   <td><p>I10</p></td>
   <td><p>表單；可供OEM使用。</p></td>
   <td><p>最大值</p></td>
   <td><p>生產與評估</p></td>
  </tr>
  <tr>
   <td><p>I11</p></td>
   <td><p>表單；可供OEM使用。</p></td>
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
   <td><p>僅加上註解；可供OEM使用。</p></td>
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

## 有效期 {#validity-period}

評估憑證會核發給客戶和開發人員，讓他們可以評估和開發產品的範例應用程式。 這些證書的有效期為60至90天。 它們會在問題資料之後的第二個月底到期。

合作夥伴整合憑證會核發給Adobe商業合作夥伴，以支援軟體開發、整合、建立原型和展示。 該等證書自發行日期起計有效期為兩年。

Adobe內部使用憑證可用於支援軟體開發、整合、建立原型和展示。 該等證書自發行日期起計有效期為兩年。

生產憑證會核發給購買Acrobat Reader DC擴充功能的客戶。 這些憑證的有效期限為憑證授權機構(CA)所允許的最長期間，如「憑證設定檔 ** 」表格中的「最大值」所示。

## Acrobat Reader DC擴充功能的使用權限 {#acrobat-reader-dc-extensions-usage-rights}

當您在憑證檢視器中檢查Acrobat Reader DC擴充功能憑證時，可以從「詳細資訊」標籤（如果已設定）中選取使用權限項目，以查看憑證可啟用的Adobe Reader使用權限明細清單。 在特定文檔上啟用的使用權限可以是由證書啟用的使用權限的子集。

如果非協作環境中需要線上註解，請聯絡Adobe支援以取得詳細資訊。 Mode屬性與部署類型相符，是生產 *或**評估*。

允許的Acrobat Reader DC擴充功能使用權限包含一或多個特定元素。 這些元素會以不同的組合來使用，以達成各種授權產品功能。

<table>
 <thead>
  <tr>
   <th><p>使用權限元素</p></th>
   <th><p>檢視具權限的PDF檔案時，在Adobe Reader中啟用的功能</p></th>
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
   <td><p>在PDF表單中新增、變更或刪除欄位和欄位屬性。</p></td>
  </tr>
  <tr>
   <td><p>SubmitStandalone</p></td>
   <td><p>當資料未在瀏覽器作業階段中執行時，以電子郵件或離線方式提交至伺服器。</p></td>
  </tr>
  <tr>
   <td><p>衍生範本</p></td>
   <td><p>從相同PDF表單中的範本頁面建立頁面。</p></td>
  </tr>
  <tr>
   <td><p>簽署</p></td>
   <td><p>數位簽署並儲存PDF檔案，並清除數位簽名。</p></td>
  </tr>
  <tr>
   <td><p>AnnotModify</p></td>
   <td><p>建立和修改文檔注釋，如注釋。</p></td>
  </tr>
  <tr>
   <td><p>AnnotImportExport</p></td>
   <td><p>將注釋（例如注釋）儲存在個別的資料檔案中，並從檔案載入注釋。</p></td>
  </tr>
  <tr>
   <td><p>BarcodePlaintext</p></td>
   <td><p>以未加密的格式列印表格資料列碼的檔案，不需要授權伺服器軟體進行解碼。</p></td>
  </tr>
  <tr>
   <td><p>AnnotOnline</p></td>
   <td><p>從線上檔案審閱與注釋伺服器上傳及下載注釋，例如注釋。</p></td>
  </tr>
  <tr>
   <td><p>FormOnline</p></td>
   <td><p>連線至在PDF表單中定義的網站服務或資料庫。</p></td>
  </tr>
  <tr>
   <td><p>EFModif</p></td>
   <td><p>修改與PDF文檔關聯的嵌入檔案對象。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Acrobat Reader DC擴充功能的使用權限只能透過特定搭配運作的組合，向Adobe授權。 無法單獨授權這些功能。 如需使用權限的可用組合資訊，請聯絡AEM表單帳戶代表。

