---
title: 「教學課程：建立最適化表單」
seo-title: '"建立適應性表單"'
description: 瞭解如何建立、排版和預覽最適化表單。 此外，還要瞭解如何設定提交動作。
seo-description: 瞭解如何建立、排版和預覽最適化表單。 此外，還要瞭解如何設定提交動作。
page-status-flag: de-activated
uuid: 0010d274-a683-499e-9fa6-ce355d7898a0
discoiquuid: 55c08940-8c25-4938-8e49-25bce20aaf22
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78

---


# 教學課程：建立最適化表單 {#do-not-publish-tutorial-create-an-adaptive-form}

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

本教學課程是「建立您的第 [一個最適化表單](/help/forms/using/create-your-first-adaptive-form.md) 」系列的步驟。 建議依序依序依序排列，以瞭解、執行和展示完整的教學課程使用案例。

## 關於教學課程 {#about-the-tutorial}

最適化表單是新一代的動態回應表單。 您可以使用最適化表單來提供個人化體驗。 您也可以將最適化表單與Adobe Analytics整合，以取得使用統計資料，並將Adobe Campaign整合以進行宣傳活動管理。 如需最適化表單功能的詳細資訊，請參 [閱製作最適化表單簡介](/help/forms/using/introduction-forms-authoring.md)。

當遵循適當的程式時，建立和管理表格會更輕鬆。 在本文中，您將學習如何：

* [建立可讓客戶新增送貨地址的最適化表單](/help/forms/using/create-adaptive-form.md#step-create-the-adaptive-form)

* [顯示並接受客戶資訊的最適化表單的版面欄位](/help/forms/using/create-adaptive-form.md#step-add-header-and-footer)

* [建立提交動作以傳送包含表單內容的電子郵件](/help/forms/using/create-adaptive-form.md#step-add-components-to-capture-and-display-information)
* [預覽並送出最適化表單](/help/forms/using/create-adaptive-form.md)

在文章結尾處，您會有類似下列的表格：\
[![](do-not-localize/form-preview-mobile.gif)](do-not-localize/form-preview-mobile.gif)

## 步驟1:建立最適化表單 {#step-create-the-adaptive-form}

1. 登入AEM作者例項並導覽至 **Adobe Experience Manager** > **Forms** > **Forms &amp; Documents**。 預設URL為 [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments)。
1. 點選「 **建立** 」並選 **取「最適化表單**」。 此時會出現選擇範本的選項。 點選「 **Blank** 」範本以選取範本，然後點選「 **Next」**。

1. 出現「Add Properties(添 **加屬性** )」選項。 「標 **題** 」和「 **名稱** 」欄位是必填欄位：

   * **** 標題：在「 `Add new or update shipping address` 標題」欄位中指定。 標題欄位會指定表單的顯示名稱。 標題可協助您識別AEM Forms使用者介面中的表單。
   * **** 名稱：在「名 `shipping-address-add-update-form` 稱」欄位中指定。 「名稱」欄位指定表單的名稱。 在儲存庫中建立具有指定名稱的節點。 當您開始輸入標題時，系統會自動產生名稱欄位的值。 您可以變更建議的值。 名稱欄位只能包含英數字元、連字型大小和底線。 所有無效輸入都會以連字型大小取代。

1. 點選「 **建立**」。 會建立最適化表單，並出現對話方塊以開啟表單以供編輯。 點選 **「開啟** 」，在新標籤中開啟新建立的表格。 表格隨即開啟以供編輯。 它還顯示邊欄，以根據需求自訂新建立的表格。

   有關最適化表單製作介面和可用元件的資訊，請參 [閱製作最適化表單簡介](/help/forms/using/creating-adaptive-form.md)。

   ![新建——自適應形式](assets/newly-created-adaptive-form.png)

## 步驟2:新增頁首和頁尾 {#step-add-header-and-footer}

AEM Forms提供許多元件，以顯示最適化表單的資訊。 頁首和頁尾元件有助於為表單提供一致的外觀和感覺。 標題通常包含公司的標誌、表單標題和摘要。 頁尾通常包含版權資訊和其他頁面的連結。

1. 點選 ![「切換側面板](assets/toggle-side-panel.png) >樹狀 ![擴充」](assets/treeexpandall.png)。 元件瀏覽器隨即開啟。 將Header元 **件從元件瀏覽** 器拖曳至最適化表單。
1. 點選 **標誌**。 工具列隨即出現。 在工 ![具列上點選aem_6_3_edit](assets/aem_6_3_edit.png) ，輸入 **We.Retail**，然後點選 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

1. 點選「影像」。 工具列隨即出現。 點選 ![cmppr](assets/cmppr.png)。 屬性瀏覽器會在畫面左側開啟。 **瀏覽** 並上傳標誌影像。 點 ![選aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。 影像會出現在頁首上。

   如果您沒有標誌，可以點選「取得檔案」下載本文中使用的標誌。

   [取得檔案](assets/logo.png)

1. 將Footer元 **件從** tree ![expanall拖](assets/treeexpandall.png) 曳至最適化表單。 在此階段，表單如下所示：

   ![adaptive-form-with-headers-and-foots](assets/adaptive-form-with-headers-and-footers.png)

## 步驟3:新增元件以擷取和顯示資訊 {#step-add-components-to-capture-and-display-information}

元件是自適應形式的構建塊。 AEM Forms提供許多元件，可擷取並顯示最適化表單中的資訊。 您可以將元件從樹狀擴 ![展全部拖曳](assets/treeexpandall.png) 到表單。 若要瞭解可用的元件和相應的功能，請參 [閱製作最適化表單簡介](/help/forms/using/introduction-forms-authoring.md)。

1. 將「數值方塊」元件拖曳至最適化表單。 將它置於頁尾元件之前。 開啟元件的屬性，將元件的 **Title** 更改為 **`Customer ID`**，將 **Element Name** 更改為，啟用Required Field選項，使 **`customer_ID`**********![](assets/aem_6_3_forms_save.png)The Required Properments Use H HTML5 Input Type Option，並且TapAem_6 Forms_saveChorms3。
1. 將三個文本框元件拖動到最適化表單。 將這些項目置於頁尾元件之前。 為這些文本框設定以下屬性。:

<table> 
 <tbody> 
  <tr> 
   <td>屬性</td> 
   <td>Text Box 1<br /> </td> 
   <td>Text Box 2<br /> </td> 
   <td>文字方塊3</td> 
  </tr> 
  <tr> 
   <td>標題</td> 
   <td>名稱<br /> </td> 
   <td>送貨地址</td> 
   <td>狀態</td> 
  </tr> 
  <tr> 
   <td>元素名稱</td> 
   <td>customer_name<br /> </td> 
   <td>customer_Shipping_Address</td> 
   <td>customer_state</td> 
  </tr> 
  <tr> 
   <td>必填欄位</td> 
   <td>已啟用</td> 
   <td>已啟用</td> 
   <td>已啟用</td> 
  </tr> 
  <tr> 
   <td>允許多行<br /> </td> 
   <td>停用</td> 
   <td>已啟用</td> 
   <td>停用</td> 
  </tr> 
 </tbody> 
</table>

1. 將數值 **** 框元件拖曳到腳注元件之前。 開啟元件的屬性，設定下表「點選 ![aem_6_3_forms_save」中所列的值](assets/aem_6_3_forms_save.png)。

   | 屬性 | 值 |
   |---|---|
   | 標題 | 郵遞區號 |
   | 元素名稱 | customer_ZIPCode |
   | 數字數量上限 | 6 |
   | 必填欄位 | 已啟用 |
   | 顯示模式類型 | 無模式 |

1. 拖曳 **Email** 元件至頁尾元件之前。 開啟元件的屬性、設定下表中所列的值，然後點選 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   | 屬性 | 值 |
   |---|---|
   | 標題 | 電子郵件 |
   | 元素名稱 | customer_Email |
   | 必填欄位 | 已啟用 |

1. 在腳注組 **件之前拖動「檔案附件** 」元件。 開啟元件的屬性、設定下表中所列的值，然後點選 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

<table> 
 <tbody> 
  <tr> 
   <td>屬性</td> 
   <td>值</td> 
  </tr> 
  <tr> 
   <td>標題</td> 
   <td>政府批准的地址證明<br /> </td> 
  </tr> 
  <tr> 
   <td>元素名稱</td> 
   <td>customer_Address_Proof</td> 
  </tr> 
  <tr> 
   <td>必填欄位</td> 
   <td>已啟用</td> 
  </tr> 
 </tbody> 
</table>

1. 將「提 **交按鈕** 」元件拖曳至最適化表單。 將它置於頁尾元件之前。 開啟元件的屬性，將「元素名稱」變 **更為address_addition_update_submit**，點 ![選aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。 表單的版面配置已完成，表單外觀如下：

   ![adaptive-form-with-all-the-components](assets/adaptive-form-with-all-the-components.png)

## 步驟4:為最適化表單設定提交動作 {#step-configure-submit-action-for-the-adaptive-form}

當使用者點選最適化表單上的「提交」按鈕時，會觸發提交動作。 您可以使用提交操作將表單資料保存到本地儲存庫、將表單資料發送到REST端點、以電子郵件形式發送表單資料等。 最適化表單提供一些現成可用的提交動作。 如需詳細資訊，請參 [閱設定提交動作](/help/forms/using/configuring-submit-actions.md)。

使用下列步驟，您可以設定表單的電子郵件提交動作和示範提交動作：

1. 配置電子郵件伺服器。 如需詳細資訊，請參 [閱設定電子郵件通知](/help/sites-administering/notification.md)。


1. 在「內 **容」瀏覽器中點選** 「表單容器」，然後點 ![選cmppr](assets/cmppr.png)。 屬性瀏覽器會在左側開啟。
1. 前往「提 **交** >提 **交動作」**。 選擇「 **傳送電子郵件**」。 指定下列值並點 ![選aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   | 屬性 | 值 |
   |--- |--- |
   | 從 | `donotreply@weretail.com` |
   | 至 | `${customer_Email}` |
   | 主旨 | 確認：您已在We.Retail網站上新增送貨地址。 |
   | 電子郵件範本 | 您 `${customer_Name}`好，以下地址會新增為您帳戶的運送地址： <br>`${customer_Name}`, `${customer_Shipping_Address}`, `${customer_State}`問候 `${customer_ZIPCode}`<br> ，我們零售 |
   | 包含附件 | 已啟用 |

   您的表格已備妥。 現在，您可以預覽表單並測試功能。 如果您使用了教學課程中提及的名稱，並在執行AEM Forms伺服器的機器上存取表格，則表格可在http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html [取得](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)。

## 步驟5:預覽並送出最適化表單 {#step-preview-and-submit-the-adaptive-form}

您可以使用「預 **覽」選項** ，評估表單的外觀和行為。 您可以在預覽模式下提交表單，也可以檢查套用在表單上的驗證。 例如，如果強制欄位留空時顯示錯誤。

最適化表單也提供選項，可讓您針對各種裝置模擬表單的使用體驗。 例如，iPhone、iPad和Desktop。 您可以搭配使 **用「預覽** 」和「模擬器 **** 」尺標選項 ![](assets/ruler.png) ，來預覽不同螢幕大小裝置的表格。

1. 點選表 **單編輯器右側的** 「預覽」選項。 表單會在預覽模式中開啟。 如果您使用了教學課程中提及的名稱，則表單的預覽URL為 [http://localhost:4502/content/dam/formsanddocuments/shipping-address-add-update-form/jcr:content?wcmmode=disabled](http://localhost:4502/content/dam/formsanddocuments/shipping-address-addition-updation-form/jcr:content?wcmmode=disabled)
1. 使用 ![尺標](assets/ruler.png) ，檢視表格在各種裝置上的外觀。
1. 填寫表單欄位並點選「送 **出」**。 表單已送出，您會重新導向至預設的「感 **謝您** 」頁面。 您也可以指定自訂的感謝頁面。 如需詳細資訊，請參 [閱設定重新導向頁面](/help/forms/using/configuring-redirect-page.md)。

添加地址的最適化表單已就緒。 如果您使用了教學課程中提及的名稱，並在執行AEM Forms伺服器的機器上存取表格，則表格可在http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html [取得](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)。
