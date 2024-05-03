---
title: 「教學課程：建立最適化表單」
description: 瞭解如何建立、佈局和預覽最適化表單。 另外，瞭解如何設定提交動作。
feature: Adaptive Forms
exl-id: c0a2adcd-528a-41af-99b5-d8b423cd6605
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 8%

---

# 教學課程：建立最適化表單 {#do-not-publish-tutorial-create-an-adaptive-form}

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

本教學課程是 [建立第一個最適化表單](/help/forms/using/create-your-first-adaptive-form.md) 數列。 建議您依照序列時間順序來瞭解、執行和示範完整的教學課程使用案例。

## 關於教學課程 {#about-the-tutorial}

調適型表單是新一代的表單，不但動態且回應迅速。 您可以使用調適型表單來提供個人化體驗。 您也可以整合最適化表單與 [!DNL Adobe Analytics] 使用情況統計資料和 [!DNL Adobe Campaign] 用於行銷活動管理。 如需最適化表單功能的詳細資訊，請參閱 [製作調適型表單簡介](/help/forms/using/introduction-forms-authoring.md).

遵循適當的程式時，可更輕鬆建立和管理表單。 在本文中，您將瞭解如何：

* [建立最適化表單，允許客戶新增送貨地址](/help/forms/using/create-adaptive-form.md#step-create-the-adaptive-form)

* [用於顯示和接受客戶資訊的最適化表單版面欄位](/help/forms/using/create-adaptive-form.md#step-add-header-and-footer)

* [建立提交動作以傳送包含表單內容的電子郵件](/help/forms/using/create-adaptive-form.md#step-add-components-to-capture-and-display-information)
* [預覽並提交最適化表單](/help/forms/using/create-adaptive-form.md)

文章結尾處會有類似下列的表單：\
[![行動裝置中的表單預覽](do-not-localize/form-preview-mobile.gif)](do-not-localize/form-preview-mobile.gif)

## 步驟1：建立最適化表單 {#step-create-the-adaptive-form}

1. 登入AEM作者執行個體並導覽至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**. 預設URL為 [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments).
1. 選取 **[!UICONTROL 建立]** 並選取 **[!UICONTROL 最適化表單]**. 隨即顯示選取範本的選項。 選取 **[!UICONTROL 空白]** 範本以選取並選取 **[!UICONTROL 下一個]**.

1. 選項至 **[!UICONTROL 新增屬性]** 隨即顯示。 此 **[!UICONTROL 標題]** 和 **[!UICONTROL 名稱]** 欄位為必填欄位：

   * **標題：** 指定 `Add new or update shipping address` 在 **[!UICONTROL 標題]** 欄位。 標題欄位指定表單的顯示名稱。 標題可協助您識別AEM中的表單 [!DNL Forms] 使用者介面。
   * **名稱：** 指定 `shipping-address-add-update-form` 在 **[!UICONTROL 名稱]** 欄位。 「名稱」欄位指定表單的名稱。 存放庫中會建立具有指定名稱的節點。您開始輸入標題時，就會自動產生名稱欄位的值。您可以變更建議的值。名稱欄位只能包含字母數字字元、連字號和底線。所有無效的輸入都會以連字號取代。

1. 選擇 **[!UICONTROL 建立]**。系統隨即建立最適化表單，並顯示對話方塊以開啟表單進行編輯。 選取 **[!UICONTROL 開啟]** 以在新標籤中開啟新建立的表單。 隨即開啟表單進行編輯。 也會顯示側邊欄，以便您根據需求自訂新建立的表單。

   如需關於最適化表單製作介面和可用元件的資訊，請參閱 [製作調適型表單簡介](/help/forms/using/creating-adaptive-form.md).

   ![新建立的調適型表單。](assets/newly-created-adaptive-form.png)

## 步驟2：新增頁首和頁尾 {#step-add-header-and-footer}

AEM [!DNL Forms] 提供許多元件，以便在最適化表單上顯示資訊。 頁首與頁尾元件有助於提供一致的外觀與風格。 頁首通常包含公司的標誌、表單標題和摘要。 頁尾通常包含版權資訊和其他頁面的連結。

1. 選取 ![切換側面板](assets/toggle-side-panel.png) > ![treeexpandall](assets/treeexpandall.png). 元件瀏覽器隨即開啟。 拖曳 **[!UICONTROL 頁首]** 元件從元件瀏覽器轉換為最適化表單。
1. 選取 **[!UICONTROL 標誌]**. 工具列隨即顯示。 選取 ![aem_6_3_edit](assets/aem_6_3_edit.png) 在工具列上，輸入 **We.Retail**，並選取 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

1. 選取影像。 工具列隨即顯示。 選取 ![cmppr](assets/cmppr.png). 屬性瀏覽器會在畫面左側開啟。 **[!UICONTROL 瀏覽]** 並上傳標誌影像。 選取 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). 影像會顯示在頁首上。

   如果您沒有圖志，可以選取[取得檔案]來下載本文中使用的圖志。

[取得檔案](assets/logo.png)

1. 拖曳 **[!UICONTROL 頁尾]** 元件來源 ![treeexpandall](assets/treeexpandall.png) 至最適化表單。 在此階段，表單看起來像這樣：

   ![adaptive-form-with-headers-and-footers](assets/adaptive-form-with-headers-and-footers.png)

## 步驟3：新增元件以擷取和顯示資訊 {#step-add-components-to-capture-and-display-information}

元件為最適化表單的建置組塊。 AEM [!DNL Forms] 提供許多元件，好讓您以最適化表單擷取和顯示資訊。 您可以從以下位置拖曳元件： ![treeexpandall](assets/treeexpandall.png) 至表單。 若要瞭解可用的元件和對應的功能，請參閱 [製作調適型表單簡介](/help/forms/using/introduction-forms-authoring.md).

1. 拖曳 **[!UICONTROL 數值方塊元件]** 至最適化表單。 將其放在頁尾元件之前。 開啟元件的屬性，變更 **[!UICONTROL 標題]** 至的元件 **`Customer ID`**，變更 **[!UICONTROL 元素名稱]** 至 **`customer_ID`**，啟用 **[!UICONTROL 必填欄位]** 選項，啟用 **[!UICONTROL 使用HTML5數字輸入型別]** 選項，然後選取 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
1. 將三個Text Box元件拖曳至最適化表單。 將這些專案放在頁尾元件之前。 為這些文字方塊設定下列屬性。：

   <table> 
    <tbody> 
     <tr> 
      <td><b>屬性</b></td> 
      <td><b>文字方塊1<br/></b></td> 
      <td><b>文字方塊2<br/></b></td> 
      <td><b>文字方塊3</b></td> 
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
      <td>已停用</td> 
      <td>已啟用</td> 
      <td>已停用</td> 
     </tr> 
    </tbody> 
   </table>

1. 拖曳 **[!UICONTROL 數值方塊]** 頁尾元件之前的元件。 開啟元件的屬性，設定下表列出的值，選取 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | 屬性 | 值 |
   |---|---|
   | 標題 | 郵遞區號 |
   | 元素名稱 | customer_ZIPCode |
   | 數字數量上限 | 6 |
   | 必填欄位 | 已啟用 |
   | 顯示圖樣型別 | 無模式 |

1. 拖曳 **[!UICONTROL 電子郵件]** 頁尾元件之前的元件。 開啟元件的屬性，設定下表列出的值，然後選取 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | 屬性 | 值 |
   |---|---|
   | 標題 | 電子郵件 |
   | 元素名稱 | customer_Email |
   | 必填欄位 | 已啟用 |

1. 拖曳 **[!UICONTROL 檔案附件]** 頁尾元件之前的元件。 開啟元件的屬性，設定下表列出的值，然後選取 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>屬性</b></td> 
      <td><b>值</b></td> 
     </tr> 
     <tr> 
      <td>標題</td> 
      <td>政府核准的地址證明<br /> </td> 
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

1. 拖曳 **[!UICONTROL 提交按鈕]** 元件至最適化表單。 將其放在頁尾元件之前。 開啟元件的屬性，將元素名稱變更為 `address_addition_update_submit`，選取 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). 表單版面配置完整，表單如下所示：

   ![adaptive-form-with-all-the-components](assets/adaptive-form-with-all-the-components.png)

## 步驟4：設定最適化表單的提交動作 {#step-configure-submit-action-for-the-adaptive-form}

當使用者點選最適化表單上的提交按鈕時，就會觸發提交動作。 您可以使用提交動作將表單資料儲存至本機存放庫、將表單資料傳送至REST端點、以電子郵件傳送表單資料等。 調適型表單提供幾個立即可用的提交動作。 如需詳細資訊，請參閱 [設定提交動作](/help/forms/using/configuring-submit-actions.md).

使用下列步驟，您可以設定表單的電子郵件提交動作和示範提交動作：

1. 設定電子郵件伺服器。 如需詳細資訊，請參閱 [設定電子郵件通知](/help/sites-administering/notification.md).


1. 選取 **[!UICONTROL 表單容器]** 在內容瀏覽器中並選取 ![cmppr](assets/cmppr.png). 屬性瀏覽器會在左側開啟。
1. 前往 **[!UICONTROL 提交]** >  **[!UICONTROL 提交動作]**. 選取 **[!UICONTROL 傳送電子郵件]**. 指定下列值並選取 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | 屬性 | 值 |
   |--- |--- |
   | 來自 | `donotreply@weretail.com` |
   | 至 | `${customer_Email}` |
   | 主旨 | 通知：您已在We.Retail網站上新增運送地址。 |
   | 電子郵件範本 | 您好 `${customer_Name}`，下列地址會新增為您的帳戶的運送地址： <br>`${customer_Name}`， `${customer_Shipping_Address}`， `${customer_State}`， `${customer_ZIPCode}`<br> 謹祝， We.Retail |
   | 包含附件 | 已啟用 |

   您的表單已準備就緒。 現在，您可以預覽表單並測試功能。 如果您已使用教學課程中提到的名稱，並在執行AEM的電腦上存取表單 [!DNL Forms] 伺服器，則可在以下位置取得表單： [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).

## 步驟5：預覽並提交最適化表單 {#step-preview-and-submit-the-adaptive-form}

您可以使用 **[!UICONTROL 預覽選項]** 以評估表單的外觀和行為。 您可以在預覽模式中提交表單，也可以檢查表單上套用的驗證。 例如，如果在必填欄位留空時顯示錯誤。

調適型表單也提供模擬各種裝置表單體驗的選項。 例如，iPhone、iPad和案頭。 您可以使用兩者 **[!UICONTROL 預覽]** 和 **[!UICONTROL 模擬器]** ![尺標](assets/ruler.png) 多個選項搭配使用，為不同熒幕大小的裝置預覽表單。

1. 選取 **[!UICONTROL 預覽]** 表單編輯器右側的選項。 表單會在預覽模式中開啟。 如果您使用教學課程中提到的名稱，則表單的預覽URL會是 [http://localhost:4502/content/dam/formsanddocuments/shipping-address-add-update-form/jcr:content?wcmmode=disabled](http://localhost:4502/content/dam/formsanddocuments/shipping-address-addition-updation-form/jcr:content?wcmmode=disabled)
1. 使用 ![尺標](assets/ruler.png) 以檢視表單在各種裝置上的外觀。
1. 填寫表單欄位並選取 **[!UICONTROL 提交]**. 表單已提交，您被重新導向至預設值 **感謝您** 頁面。 您也可以指定自訂感謝頁面。 如需詳細資訊，請參閱 [設定重新導向頁面](/help/forms/using/configuring-redirect-page.md).

新增位址的最適化表單已就緒。 如果您使用本教學課程中提到的名稱，並在執行AEM Forms伺服器的電腦上存取表單，則表單位於 [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).
