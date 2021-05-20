---
title: 「教學課程：建立最適化表單」
seo-title: '"建立最適化表單"'
description: 了解如何建立、版面配置和預覽最適化表單。 此外，也可學習如何設定提交動作。
seo-description: 了解如何建立、版面配置和預覽最適化表單。 此外，也可學習如何設定提交動作。
page-status-flag: de-activated
uuid: 0010d274-a683-499e-9fa6-ce355d7898a0
discoiquuid: 55c08940-8c25-4938-8e49-25bce20aaf22
feature: 適用性表單
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 3%

---


# 教學課程：建立最適化表單{#do-not-publish-tutorial-create-an-adaptive-form}

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

本教學課程是[建立第一個最適化表單](/help/forms/using/create-your-first-adaptive-form.md)系列中的步驟。 建議您依序依序依序執行系列，以了解、執行和示範完整的教學課程使用案例。

## 關於教學課程{#about-the-tutorial}

最適化表單是新一代動態且回應迅速的表單。 您可以使用適用性表單來提供個人化體驗。 您也可以將適用性表單與[!DNL Adobe Analytics]整合，以取得使用統計資料，並[!DNL Adobe Campaign]整合以管理促銷活動。 如需適用性表單功能的詳細資訊，請參閱[製作適用性表單簡介](/help/forms/using/introduction-forms-authoring.md)。

遵循適當的程式時，建立和管理表單會更輕鬆。 在本文中，您將學習如何：

* [建立可讓客戶新增送貨地址的最適化表單](/help/forms/using/create-adaptive-form.md#step-create-the-adaptive-form)

* [最適化表單的版面欄位，以顯示並接受客戶的資訊](/help/forms/using/create-adaptive-form.md#step-add-header-and-footer)

* [建立提交動作，以傳送包含表單內容的電子郵件](/help/forms/using/create-adaptive-form.md#step-add-components-to-capture-and-display-information)
* [預覽並提交最適化表單](/help/forms/using/create-adaptive-form.md)

文章結尾會提供類似下列的表單：\
[![](do-not-localize/form-preview-mobile.gif)](do-not-localize/form-preview-mobile.gif)

## 步驟1:建立最適化表單{#step-create-the-adaptive-form}

1. 登入AEM製作例項，並導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**。 預設URL為[http://localhost:4502/aem/forms.html/content/dam/formsanddocuments](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments)。
1. 點選&#x200B;**[!UICONTROL 建立]**&#x200B;並選取&#x200B;**[!UICONTROL 最適化表單]**。 畫面上會顯示選取範本的選項。 點選&#x200B;**[!UICONTROL 空白]**&#x200B;範本以加以選取，然後點選&#x200B;**[!UICONTROL 下一步]**。

1. 出現「**[!UICONTROL 新增屬性]**」選項。 **[!UICONTROL Title]**&#x200B;和&#x200B;**[!UICONTROL Name]**&#x200B;欄位是必填欄位：

   * **標題：** 在標 `Add new or update shipping address` 題欄位中 **** 指定。標題欄位指定表單的顯示名稱。 標題可協助您識別AEM [!DNL Forms]使用者介面中的表單。
   * **名稱：** 在「 `shipping-address-add-update-form` 名稱」欄 **** 位中指定。「名稱」欄位指定表單的名稱。 在儲存庫中建立具有指定名稱的節點。 當您開始輸入標題時，會自動產生名稱欄位的值。 您可以變更建議的值。 名稱欄位只能包含英數字元、連字型大小和底線。 所有無效輸入都會以連字型大小取代。

1. 點選&#x200B;**[!UICONTROL 建立]**。 隨即建立最適化表單，並出現一個對話方塊以開啟表單以進行編輯。 點選&#x200B;**[!UICONTROL 開啟]**&#x200B;以在新索引標籤中開啟新建立的表單。 表單隨即開啟供編輯。 它也會顯示邊欄，以根據需求自訂新建立的表單。

   如需適用性表單製作介面和可用元件的相關資訊，請參閱[製作適用性表單簡介](/help/forms/using/creating-adaptive-form.md)。

   ![新建立 — adaptive-form](assets/newly-created-adaptive-form.png)

## 步驟2:新增頁首與頁尾{#step-add-header-and-footer}

AEM [!DNL Forms]提供許多元件，以顯示最適化表單的資訊。 頁首與頁尾元件有助於提供一致的表單外觀。 標題通常包括公司的標誌、表單標題和摘要。 頁尾通常包含版權資訊和其他頁面的連結。

1. 點選![toggle-side-panel](assets/toggle-side-panel.png) > ![treeexpandall](assets/treeexpandall.png)。 元件瀏覽器隨即開啟。 從元件瀏覽器將&#x200B;**[!UICONTROL Header]**&#x200B;元件拖曳至最適化表單。
1. 點選&#x200B;**[!UICONTROL Logo]**。 工具列隨即出現。 點選工具列上的![aem_6_3_edit](assets/aem_6_3_edit.png)，輸入&#x200B;**We.Retail**，然後點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

1. 點選「影像」。 工具列隨即出現。 點選![cmpr](assets/cmppr.png)。 屬性瀏覽器隨即在螢幕左側開啟。 **** 瀏覽及上傳標誌影像。點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。 影像會出現在標題上。

   如果您沒有標誌，可以點選「取得檔案」以下載本文中使用的標誌。

[取得檔案](assets/logo.png)

1. 將&#x200B;**[!UICONTROL 頁尾]**&#x200B;元件從![treeexpandall](assets/treeexpandall.png)拖曳至最適化表單。 此階段的表單如下所示：

   ![具有頁首和頁尾的適用性表單](assets/adaptive-form-with-headers-and-footers.png)

## 步驟3:添加元件以捕獲和顯示資訊{#step-add-components-to-capture-and-display-information}

元件是最適化表單的建置組塊。 AEM [!DNL Forms]提供許多元件，以擷取和顯示最適化表單中的資訊。 您可以將元件從![treeexpandall](assets/treeexpandall.png)拖曳至表單。 若要了解可用元件和對應的功能，請參閱[製作最適化表單簡介](/help/forms/using/introduction-forms-authoring.md)。

1. 將&#x200B;**[!UICONTROL 數值方塊元件]**&#x200B;拖曳至最適化表單。 將其置於頁尾元件之前。 開啟元件的屬性，將元件的&#x200B;**[!UICONTROL 標題]**&#x200B;變更為&#x200B;**`Customer ID`**，將&#x200B;**[!UICONTROL 元素名稱]**&#x200B;變更為&#x200B;**`customer_ID`**，啟用&#x200B;**[!UICONTROL 必要欄位]**&#x200B;選項，啟用&#x200B;**[!UICONTROL 使用HTML5數字輸入類型]**&#x200B;選項，然後點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。
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
      <td>customer_Name<br /> </td> 
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

1. 拖曳&#x200B;**[!UICONTROL 數值方塊]**&#x200B;元件至頁尾元件之前。 開啟元件的屬性，設定下表中列出的值，點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   | 屬性 | 值 |
   |---|---|
   | 標題 | 郵遞區號 |
   | 元素名稱 | customer_ZIPCode |
   | 數字數量上限 | 6 |
   | 必填欄位 | 已啟用 |
   | 顯示圖樣類型 | 無模式 |

1. 將&#x200B;**[!UICONTROL Email]**&#x200B;元件拖曳到頁尾元件之前。 開啟元件的屬性，設定下表中列出的值，然後點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   | 屬性 | 值 |
   |---|---|
   | 標題 | 電子郵件 |
   | 元素名稱 | customer_Email |
   | 必填欄位 | 已啟用 |

1. 將&#x200B;**[!UICONTROL 檔案附件]**&#x200B;元件拖曳到頁尾元件之前。 開啟元件的屬性，設定下表中列出的值，然後點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

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

1. 將&#x200B;**[!UICONTROL 提交按鈕]**&#x200B;元件拖曳至最適化表單。 將其置於頁尾元件之前。 開啟元件的屬性，將「元素名稱」變更為`address_addition_update_submit`，點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。 表單的版面已完成，表單看起來如下所示：

   ![adaptive-form-with-all-the-components](assets/adaptive-form-with-all-the-components.png)

## 步驟4:設定最適化表單{#step-configure-submit-action-for-the-adaptive-form}的提交動作

使用者點選適用性表單上的「提交」按鈕時，會觸發提交動作。 您可以使用提交動作將表單資料儲存至本機存放庫、將表單資料傳送至REST端點、以電子郵件形式傳送表單資料等。 適用性表單提供更多現成可用的提交動作。 如需詳細資訊，請參閱[設定提交動作](/help/forms/using/configuring-submit-actions.md)。

使用下列步驟，您可以設定表單的電子郵件提交動作和示範提交動作：

1. 設定電子郵件伺服器。 如需詳細資訊，請參閱[設定電子郵件通知](/help/sites-administering/notification.md)。


1. 在「內容」瀏覽器中，點選「 **[!UICONTROL 表單容器]**」，然後點選「![cmpr](assets/cmppr.png)」。 屬性瀏覽器會在左側開啟。
1. 前往「**[!UICONTROL 提交]** > **[!UICONTROL 提交動作]**」。 選擇&#x200B;**[!UICONTROL 發送電子郵件]**。 指定下列值，然後點選![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   | 屬性 | 值 |
   |--- |--- |
   | 從 | `donotreply@weretail.com` |
   | 至 | `${customer_Email}` |
   | 主旨 | 確認：您已在We.Retail網站上新增送貨地址。 |
   | 電子郵件範本 | 您好`${customer_Name}`，會新增下列地址作為您的帳戶的運送地址：<br>`${customer_Name}`、`${customer_Shipping_Address}`、`${customer_State}`、`${customer_ZIPCode}`<br>致意， We.Retail |
   | 包含附件 | 已啟用 |

   你的表格準備好了。 現在，您可以預覽表單並測試功能。 如果您使用了提及教學課程的名稱並存取執行AEM [!DNL Forms]伺服器的電腦上的表單，則表單可在[http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)取得。

## 步驟5:預覽並提交最適化表單{#step-preview-and-submit-the-adaptive-form}

您可以使用&#x200B;**[!UICONTROL 預覽選項]**&#x200B;來評估表單的外觀和行為。 您可以以預覽模式提交表單，也可以檢查表單上套用的驗證。 例如，如果必填欄位留空時顯示錯誤。

適用性表單也提供可針對各種裝置模擬表單體驗的選項。 例如iPhone、iPad和Desktop。 您可以彼此結合使用&#x200B;**[!UICONTROL 預覽]**&#x200B;和&#x200B;**[!UICONTROL 模擬器]** ![尺標](assets/ruler.png)選項，以針對不同螢幕大小的裝置預覽表單。

1. 點選表單編輯器右側的&#x200B;**[!UICONTROL 預覽]**&#x200B;選項。 表單會在預覽模式中開啟。 如果您已使用教學課程提及的名稱，則表單的預覽URL為[http://localhost:4502/content/dam/formsanddocuments/shipping-address-add-update-form/jcr:content?wcmmode=disabled](http://localhost:4502/content/dam/formsanddocuments/shipping-address-addition-updation-form/jcr:content?wcmmode=disabled)
1. 使用![ruler](assets/ruler.png)查看窗體在各種設備上的外觀。
1. 填寫表單的欄位，然後點選&#x200B;**[!UICONTROL Submit]**。 表單會提交，系統會將您重新導向至預設的&#x200B;**感謝**&#x200B;頁面。 您也可以指定自訂的感謝頁面。 如需詳細資訊，請參閱[設定重新導向頁面](/help/forms/using/configuring-redirect-page.md)。

新增地址的最適化表單已就緒。 如果您已使用教學課程中提及的名稱並存取執行AEM Forms伺服器之電腦上的表單，則表單可在[http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)取得。
