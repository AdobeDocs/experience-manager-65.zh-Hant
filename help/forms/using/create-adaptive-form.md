---
title: '''教學課程：建立最適化表單'
seo-title: Create an adaptive form
description: 了解如何建立、版面配置和預覽最適化表單。 此外，也可學習如何設定提交動作。
seo-description: Learn to create, layout, and preview an adaptive form. Also, learn to configure submit actions.
page-status-flag: de-activated
uuid: 0010d274-a683-499e-9fa6-ce355d7898a0
discoiquuid: 55c08940-8c25-4938-8e49-25bce20aaf22
feature: Adaptive Forms
exl-id: c0a2adcd-528a-41af-99b5-d8b423cd6605
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1376'
ht-degree: 3%

---

# 教學課程：建立最適化表單 {#do-not-publish-tutorial-create-an-adaptive-form}

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

本教學課程是 [建立第一個最適化表單](/help/forms/using/create-your-first-adaptive-form.md) 系列。 建議您依序依序依序執行系列，以了解、執行和示範完整的教學課程使用案例。

## 關於教學課程 {#about-the-tutorial}

最適化表單是新一代動態且回應迅速的表單。 您可以使用適用性表單來提供個人化體驗。 您也可以將最適化表單與 [!DNL Adobe Analytics] 用量統計和 [!DNL Adobe Campaign] 用於行銷活動管理。 如需適用性表單功能的詳細資訊，請參閱 [製作最適化表單簡介](/help/forms/using/introduction-forms-authoring.md).

遵循適當的程式時，建立和管理表單會更輕鬆。 在本文中，您將學習如何：

* [建立可讓客戶新增送貨地址的最適化表單](/help/forms/using/create-adaptive-form.md#step-create-the-adaptive-form)

* [最適化表單的版面欄位，以顯示並接受客戶的資訊](/help/forms/using/create-adaptive-form.md#step-add-header-and-footer)

* [建立提交動作，以傳送包含表單內容的電子郵件](/help/forms/using/create-adaptive-form.md#step-add-components-to-capture-and-display-information)
* [預覽並提交最適化表單](/help/forms/using/create-adaptive-form.md)

文章結尾會提供類似下列的表單：\
[![](do-not-localize/form-preview-mobile.gif)](do-not-localize/form-preview-mobile.gif)

## 步驟1:建立最適化表單 {#step-create-the-adaptive-form}

1. 登入AEM製作例項並導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**. 預設URL為 [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments).
1. 點選 **[!UICONTROL 建立]** 選取 **[!UICONTROL 適用性表單]**. 畫面上會顯示選取範本的選項。 點選 **[!UICONTROL 空白]** 選取範本並點選 **[!UICONTROL 下一個]**.

1. 選項 **[!UICONTROL 新增屬性]** 框。 此 **[!UICONTROL 標題]** 和 **[!UICONTROL 名稱]** 欄位是必填欄位：

   * **標題：** 指定 `Add new or update shipping address` 在 **[!UICONTROL 標題]** 欄位。 標題欄位指定表單的顯示名稱。 標題可協助您識別AEM中的表單 [!DNL Forms] 使用者介面。
   * **名稱：** 指定 `shipping-address-add-update-form` 在 **[!UICONTROL 名稱]** 欄位。 「名稱」欄位指定表單的名稱。 在儲存庫中建立具有指定名稱的節點。 當您開始輸入標題時，會自動產生名稱欄位的值。 您可以變更建議的值。 名稱欄位只能包含英數字元、連字型大小和底線。 所有無效輸入都會以連字型大小取代。

1. 點選 **[!UICONTROL 建立]**. 隨即建立最適化表單，並出現一個對話方塊以開啟表單以進行編輯。 點選 **[!UICONTROL 開啟]** 在新頁簽中開啟新建立的窗體。 表單隨即開啟供編輯。 它也會顯示邊欄，以根據需求自訂新建立的表單。

   如需適用性表單製作介面和可用元件的相關資訊，請參閱 [製作最適化表單簡介](/help/forms/using/creating-adaptive-form.md).

   ![新建立 — adaptive-form](assets/newly-created-adaptive-form.png)

## 步驟2:新增頁首與頁尾 {#step-add-header-and-footer}

AEM [!DNL Forms] 提供許多元件，以顯示最適化表單的資訊。 頁首與頁尾元件有助於提供一致的表單外觀。 標題通常包括公司的標誌、表單標題和摘要。 頁尾通常包含版權資訊和其他頁面的連結。

1. 點選 ![切換側面板](assets/toggle-side-panel.png) > ![樹狀擴展](assets/treeexpandall.png). 元件瀏覽器隨即開啟。 拖曳 **[!UICONTROL 標題]** 元件（從元件瀏覽器）到最適化表單。
1. 點選 **[!UICONTROL 標誌]**. 工具列隨即出現。 點選 ![aem_6_3_edit](assets/aem_6_3_edit.png) 在工具列上，輸入 **We.Retail**，然後點選 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

1. 點選「影像」。 工具列隨即出現。 點選 ![cppr](assets/cmppr.png). 屬性瀏覽器隨即在螢幕左側開啟。 **[!UICONTROL 瀏覽]** 上傳標誌影像。 點選 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). 影像會出現在標題上。

   如果您沒有標誌，可以點選「取得檔案」以下載本文中使用的標誌。

[取得檔案](assets/logo.png)

1. 拖曳 **[!UICONTROL 頁尾]** 元件 ![樹狀擴展](assets/treeexpandall.png) 至最適化表單。 此階段的表單如下所示：

   ![具有頁首和頁尾的適用性表單](assets/adaptive-form-with-headers-and-footers.png)

## 步驟3:新增元件以擷取和顯示資訊 {#step-add-components-to-capture-and-display-information}

元件是最適化表單的建置組塊。 AEM [!DNL Forms] 提供許多元件，以擷取和顯示最適化表單中的資訊。 您可以從 ![樹狀擴展](assets/treeexpandall.png) 填入表單。 若要了解可用元件和對應的功能，請參閱 [製作最適化表單簡介](/help/forms/using/introduction-forms-authoring.md).

1. 拖曳 **[!UICONTROL 數值方塊元件]** 至最適化表單。 將其置於頁尾元件之前。 開啟元件的屬性，更改 **[!UICONTROL 標題]** 的 **`Customer ID`**，變更 **[!UICONTROL 元素名稱]** to **`customer_ID`**，啟用 **[!UICONTROL 必填欄位]** 選項，啟用 **[!UICONTROL 使用HTML5數字輸入類型]** 選項，然後點選 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
1. 拖曳三個文字方塊元件至最適化表單。 將這些內容放在頁尾元件中。 為這些文本框設定以下屬性。:

   <table> 
    <tbody> 
     <tr> 
      <td><b>屬性</b></td> 
      <td><b>文本框1<br/></b></td> 
      <td><b>文本框2<br/></b></td> 
      <td><b>文本框3</b></td> 
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

1. 拖曳 **[!UICONTROL 數值方塊]** 元件。 開啟元件的屬性，設定下表中列出的值，點選 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | 屬性 | 值 |
   |---|---|
   | 標題 | 郵遞區號 |
   | 元素名稱 | customer_ZIPCode |
   | 數字數量上限 | 6 |
   | 必填欄位 | 已啟用 |
   | 顯示圖樣類型 | 無模式 |

1. 拖曳 **[!UICONTROL 電子郵件]** 元件。 開啟元件的屬性，設定下表中列出的值，然後點選 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | 屬性 | 值 |
   |---|---|
   | 標題 | 電子郵件 |
   | 元素名稱 | customer_Email |
   | 必填欄位 | 已啟用 |

1. 拖曳 **[!UICONTROL 檔案附件]** 元件。 開啟元件的屬性，設定下表中列出的值，然後點選 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>屬性</b></td> 
      <td><b>值</b></td> 
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

1. 拖曳 **[!UICONTROL 提交按鈕]** 元件至最適化表單。 將其置於頁尾元件之前。 開啟元件的屬性，將「元素名稱」變更為 `address_addition_update_submit`，點選 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). 表單的版面已完成，表單看起來如下所示：

   ![adaptive-form-with-all-the-components](assets/adaptive-form-with-all-the-components.png)

## 步驟4:設定最適化表單的提交動作 {#step-configure-submit-action-for-the-adaptive-form}

使用者點選適用性表單上的「提交」按鈕時，會觸發提交動作。 您可以使用提交動作將表單資料儲存至本機存放庫、將表單資料傳送至REST端點、以電子郵件形式傳送表單資料等。 適用性表單提供更多現成可用的提交動作。 如需詳細資訊，請參閱 [設定提交動作](/help/forms/using/configuring-submit-actions.md).

使用下列步驟，您可以設定表單的電子郵件提交動作和示範提交動作：

1. 設定電子郵件伺服器。 如需詳細資訊，請參閱 [設定電子郵件通知](/help/sites-administering/notification.md).


1. 點選 **[!UICONTROL 表單容器]** 在「內容」瀏覽器中，然後點選 ![cppr](assets/cmppr.png). 屬性瀏覽器會在左側開啟。
1. 前往 **[!UICONTROL 提交]** >  **[!UICONTROL 提交動作]**. 選擇 **[!UICONTROL 傳送電子郵件]**. 指定下列值並點選 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | 屬性 | 值 |
   |--- |--- |
   | 從 | `donotreply@weretail.com` |
   | 至 | `${customer_Email}` |
   | 主旨 | 確認：您已在We.Retail網站上新增送貨地址。 |
   | 電子郵件範本 | 你好 `${customer_Name}`，則會新增下列地址作為您的帳戶的運送地址： <br>`${customer_Name}`, `${customer_Shipping_Address}`, `${customer_State}`, `${customer_ZIPCode}`<br> 此致，We.Retail |
   | 包含附件 | 已啟用 |

   你的表格準備好了。 現在，您可以預覽表單並測試功能。 如果您已使用本教學課程所提及的名稱，並存取執行AEM之電腦上的表單 [!DNL Forms] 伺服器，則表單可在 [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).

## 步驟5:預覽並提交最適化表單 {#step-preview-and-submit-the-adaptive-form}

您可以使用 **[!UICONTROL 預覽選項]** 來評估表單的外觀和行為。 您可以以預覽模式提交表單，也可以檢查表單上套用的驗證。 例如，如果必填欄位留空時顯示錯誤。

適用性表單也提供可針對各種裝置模擬表單體驗的選項。 例如iPhone、iPad和案頭。 您可以同時使用 **[!UICONTROL 預覽]** 和 **[!UICONTROL 模擬器]** ![尺標](assets/ruler.png) 選項，可針對不同螢幕大小的裝置預覽表單。

1. 點選 **[!UICONTROL 預覽]** 選項。 表單會在預覽模式中開啟。 如果您已使用教學課程提及的名稱，則表單的預覽URL為 [http://localhost:4502/content/dam/formsanddocuments/shipping-address-add-update-form/jcr:content?wcmmode=disabled](http://localhost:4502/content/dam/formsanddocuments/shipping-address-addition-updation-form/jcr:content?wcmmode=disabled)
1. 使用 ![尺標](assets/ruler.png) 檢視表單在各種裝置上的外觀。
1. 填寫表單的欄位並點選 **[!UICONTROL 提交]**. 表單會提交，系統會將您重新導向至預設值 **謝謝** 頁面。 您也可以指定自訂的感謝頁面。 如需詳細資訊，請參閱 [設定重新導向頁面](/help/forms/using/configuring-redirect-page.md).

新增地址的最適化表單已就緒。 如果您已使用教學課程中提及的名稱，並存取執行AEM Forms伺服器之電腦上的表單，則表單可在 [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).
