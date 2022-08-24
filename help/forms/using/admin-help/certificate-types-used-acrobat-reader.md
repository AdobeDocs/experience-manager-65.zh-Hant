---
title: Acrobat Reader DC擴展使用的證書類型
seo-title: Certificate types used by Acrobat Reader DC extensions
description: 瞭解Acrobat Reader DC擴展使用的證書類型。
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
ht-degree: 3%

---

# Acrobat Reader DC擴展使用的證書類型 {#certificate-types-used-by-acrobat-reader-dc-extensions}

證書查看器提供有關證書的以下資訊：

* 證書「友好」名稱
* 證書配置檔案
* 有效期限
* Acrobat Reader DC擴展使用權

## 證書「友好」名稱 {#certificate-friendly-name}

Acrobat Reader DC擴展證書的「友好」名稱是描述證書屬性的字串，如下例所示：

ARE 2D條形碼完整生產V6.1 P8 0002054

該字串包含以下元素：

**證書類型：** 描述AEM證書激活的表單模組和激活級別，如ARE 2D條形碼已滿。 有關可用證書類型的清單，請參閱「證書配置檔案」部分表中的「類型」列。

**部署類型：** 指示證書的預期用途，如生產。 值可以是「評估」(Evaluation)或「生產」(Production)。 有關與每個證書類型關聯的部署類型的清單，請參閱「證書配置檔案」部分表中的「部署類型」列。

**使用權限版本：** 描述證書可用於的使用權限算法版本，如V6.1。此版本不表示Acrobat或Acrobat Reader DC擴展的版本。

**配置檔案代碼：** 配置檔案代碼是完整證書屬性的簡寫說明，例如P8。 有關與每種檔案類型關聯的配置檔案代碼的清單，請參閱「證書配置檔案」部分表中的「配置檔案代碼」列。

**序列號：** 序列號分配給Adobe頒發的每個證書，如0002054。 Adobe企業支援或Adobe企業客戶代表可以使用此序列號將證書跟蹤到特定產品訂單或OEM關係。

## 證書配置檔案 {#certificate-profiles}

下表列出了分析Acrobat Reader DC擴展證書時可能遇到的證書配置檔案。

<table>
 <thead>
  <tr>
   <th><p>配置檔案代碼</p></th>
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
   <td><p>SAP內部Test</p></td>
   <td><p>2年</p></td>
   <td><p>評價和test</p></td>
  </tr>
  <tr>
   <td><p>P3</p></td>
   <td><p>Acrobat Reader DC分機，生產</p></td>
   <td><p>最大值</p></td>
   <td><p>生產</p></td>
  </tr>
  <tr>
   <td><p>P4</p></td>
   <td><p>Acrobat Reader DC擴展，內部Adobe使用</p></td>
   <td><p>2年</p></td>
   <td><p>生產</p></td>
  </tr>
  <tr>
   <td><p>P5</p></td>
   <td><p>Acrobat Reader DC擴展，合作夥伴整合</p></td>
   <td><p>2年</p></td>
   <td><p>評價和test</p></td>
  </tr>
  <tr>
   <td><p>P6</p></td>
   <td><p>Acrobat Reader DC擴展，評估</p></td>
   <td><p>60天</p></td>
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
   <td><p>Adobe Acrobat7.x，生產</p></td>
   <td><p>最大值</p></td>
   <td><p>生產</p></td>
  </tr>
  <tr>
   <td><p>I10</p></td>
   <td><p>Forms;可供OEM使用。</p></td>
   <td><p>最大值</p></td>
   <td><p>生產和評價</p></td>
  </tr>
  <tr>
   <td><p>I11</p></td>
   <td><p>Forms;可供OEM使用。</p></td>
   <td><p>最大值</p></td>
   <td><p>生產和評價</p></td>
  </tr>
  <tr>
   <td><p>I12</p></td>
   <td><p>僅簽名；可供OEM使用。</p></td>
   <td><p>最大值</p></td>
   <td><p>生產和評價</p></td>
  </tr>
  <tr>
   <td><p>I13</p></td>
   <td><p>僅離線注釋；可供OEM使用。</p></td>
   <td><p>最大值</p></td>
   <td><p>生產和評價</p></td>
  </tr>
  <tr>
   <td><p>I14</p></td>
   <td><p>僅注釋；可供OEM使用。</p></td>
   <td><p>最大值</p></td>
   <td><p>生產和評價</p></td>
  </tr>
  <tr>
   <td><p>I15</p></td>
   <td><p>完全權限；可供OEM使用。</p></td>
   <td><p>最大值</p></td>
   <td><p>生產和評價</p></td>
  </tr>
 </tbody>
</table>

## 有效期限 {#validity-period}

評估證書頒發給客戶和開發人員，以便他們能夠評估和開發產品的示例應用程式。 證書有效期為60天至90天。 在問題資料後的第二個月結束時到期。

合作夥伴整合證書將頒發給Adobe業務合作夥伴，以支援軟體開發、整合、原型製作和演示。 該等證書自發行日期起計兩年有效。

Adobe內部使用證書在Adobe內用於支援軟體開發、整合、原型製作和演示。 該等證書自發行日期起計兩年有效。

生產證書將頒發給購買Acrobat Reader DC擴展的客戶。 這些證書在證書頒發機構(CA)允許的最長期限內有效，如下所示 *最大* 的下界。

## Acrobat Reader DC擴展使用權 {#acrobat-reader-dc-extensions-usage-rights}

在證書查看器中檢查Acrobat Reader DC擴展證書時，可以從「詳細資訊」頁籤（如果已配置）中選擇使用權限項，以查看證書可啟用的Adobe Reader使用權限的明細清單。 在特定文檔上啟用的使用權限可以是由證書啟用的使用權限的子集。

如果在非協作環境中需要聯機注釋，請聯繫Adobe支援以獲取詳細資訊。 Mode屬性與部署類型匹配，並且 *生產* 或 *評價*。

允許的Acrobat Reader DC擴展使用權限由一個或多個特定元素組成。 這些元素被用在不同的組合中，以實現各種許可產品功能。

<table>
 <thead>
  <tr>
   <th><p>使用權限元素</p></th>
   <th><p>在Adobe Reader查看啟用權限的PDF文檔時啟用的功能</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>表單填充並保存</p></td>
   <td><p>填寫表單域並將檔案保存到本地。</p></td>
  </tr>
  <tr>
   <td><p>窗體導入導出</p></td>
   <td><p>將表單資料作為FDF、XFDF、XML和XDP檔案導入和導出。</p></td>
  </tr>
  <tr>
   <td><p>表單添加刪除</p></td>
   <td><p>添加、更改或刪除PDF窗體上的欄位和欄位屬性。</p></td>
  </tr>
  <tr>
   <td><p>提交獨立</p></td>
   <td><p>當資料未在瀏覽器會話中運行時，通過電子郵件或離線將資料提交到伺服器。</p></td>
  </tr>
  <tr>
   <td><p>衍生模板</p></td>
   <td><p>從同一PDF表單中的模板頁建立頁面。</p></td>
  </tr>
  <tr>
   <td><p>簽名</p></td>
   <td><p>對PDF文檔進行數字簽名和保存，並清除數字簽名。</p></td>
  </tr>
  <tr>
   <td><p>無修改</p></td>
   <td><p>建立和修改文檔注釋。</p></td>
  </tr>
  <tr>
   <td><p>無導入導出</p></td>
   <td><p>將注釋（如注釋）保存到單獨的資料檔案中，並從檔案中載入注釋。</p></td>
  </tr>
  <tr>
   <td><p>條形碼明文</p></td>
   <td><p>打印不需要授權伺服器軟體解碼的未加密格式的格式資料條形碼的文檔。</p></td>
  </tr>
  <tr>
   <td><p>AnnotOnline</p></td>
   <td><p>將注釋（如注釋）上載到聯機文檔審閱和注釋伺服器並從中下載注釋。</p></td>
  </tr>
  <tr>
   <td><p>表單聯機</p></td>
   <td><p>連接到在PDF窗體中定義的Web服務或資料庫。</p></td>
  </tr>
  <tr>
   <td><p>EFModif</p></td>
   <td><p>修改與PDF文檔關聯的嵌入檔案對象。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Acrobat Reader DC擴展使用權只能在某些組合中通過Adobe獲得許可。 無法單獨授權這些功能。 有關可用的使用權組合的資訊，請與表單客AEM戶代表聯繫。
