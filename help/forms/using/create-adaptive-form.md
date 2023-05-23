---
title: '''教程：建立自適應窗體`'
seo-title: Create an adaptive form
description: 學習建立、佈局和預覽自適應表單。 另外，學習配置提交操作。
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

# 教程：建立自適應窗體 {#do-not-publish-tutorial-create-an-adaptive-form}

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

本教程是 [建立第一個自適應窗體](/help/forms/using/create-your-first-adaptive-form.md) 的下界。 建議按時間順序按系列進行操作，以瞭解、執行和演示完整的教程使用案例。

## 關於教程 {#about-the-tutorial}

自適應形式是動態和響應的新一代形式。 您可以使用自適應表單來提供個性化體驗。 還可以將自適應表單與 [!DNL Adobe Analytics] 用於使用統計和 [!DNL Adobe Campaign] 用於市場活動管理。 有關自適應表單功能的詳細資訊，請參見 [創作自適應表單簡介](/help/forms/using/introduction-forms-authoring.md)。

在遵循正確的流程時，建立和管理表單會更容易。 在本文中，您將學習如何：

* [建立允許客戶添加發運地址的自適應表單](/help/forms/using/create-adaptive-form.md#step-create-the-adaptive-form)

* [用於顯示和接受客戶資訊的自適應表單的佈局欄位](/help/forms/using/create-adaptive-form.md#step-add-header-and-footer)

* [建立提交操作以發送包含表單內容的電子郵件](/help/forms/using/create-adaptive-form.md#step-add-components-to-capture-and-display-information)
* [預覽並提交自適應表單](/help/forms/using/create-adaptive-form.md)

在文章末尾，您將有一個類似以下的表單：\
[![](do-not-localize/form-preview-mobile.gif)](do-not-localize/form-preview-mobile.gif)

## 步驟1:建立自適應窗體 {#step-create-the-adaptive-form}

1. 登錄到作AEM者實例並導航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。 預設URL為 [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments)。
1. 點擊 **[!UICONTROL 建立]** 選擇 **[!UICONTROL 自適應窗體]**。 將顯示一個選擇模板的選項。 點擊 **[!UICONTROL 空白]** 選擇模板並點擊 **[!UICONTROL 下一個]**。

1. 一個選項 **[!UICONTROL 添加屬性]** 的子菜單。 的 **[!UICONTROL 標題]** 和 **[!UICONTROL 名稱]** 欄位為必填項：

   * **標題：** 指定 `Add new or update shipping address` 的 **[!UICONTROL 標題]** 的子菜單。 標題欄位指定窗體的顯示名稱。 標題可幫助您識別表單AEM [!DNL Forms] 用戶介面。
   * **名稱：** 指定 `shipping-address-add-update-form` 的 **[!UICONTROL 名稱]** 的子菜單。 「名稱」(Name)欄位指定表單的名稱。 在儲存庫中建立具有指定名稱的節點。 開始鍵入標題時，將自動生成名稱欄位的值。 您可以更改建議的值。 名稱欄位只能包含字母數字字元、連字元和下划線。 所有無效輸入都用連字元替換。

1. 點擊 **[!UICONTROL 建立]**。 建立一個自適應表單，並出現一個用於開啟表單以進行編輯的對話框。 點擊 **[!UICONTROL 開啟]** 的子菜單。 此時將開啟窗體進行編輯。 它還顯示邊欄，以根據需要定制新建立的表單。

   有關自適應表單創作介面和可用元件的資訊，請參見 [創作自適應表單簡介](/help/forms/using/creating-adaptive-form.md)。

   ![新建立的自適應形式](assets/newly-created-adaptive-form.png)

## 步驟2:添加頁眉和頁腳 {#step-add-header-and-footer}

AEM [!DNL Forms] 提供了許多元件以顯示自適應窗體上的資訊。 頁眉和頁腳元件有助於為表單提供一致的外觀。 標題通常包括公司徽標、表單標題和摘要。 頁腳通常包括版權資訊和指向其他頁面的連結。

1. 點擊 ![切換側面板](assets/toggle-side-panel.png) > ![樹擴展](assets/treeexpandall.png)。 元件瀏覽器開啟。 拖動 **[!UICONTROL 標題]** 元件從元件瀏覽器到自適應窗體。
1. 點擊 **[!UICONTROL 標識]**。 工具欄出現。 點擊 ![aem_6_3_edit](assets/aem_6_3_edit.png) 在工具欄上，鍵入 **We.Retail**，然後點擊 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

1. 點擊影像。 工具欄出現。 點擊 ![招商](assets/cmppr.png)。 屬性瀏覽器在螢幕左側開啟。 **[!UICONTROL 瀏覽]** 並上傳標誌影像。 點擊 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。 影像出現在標題上。

   如果您沒有徽標，可點擊「獲取檔案」下載本文中使用的徽標。

[取得檔案](assets/logo.png)

1. 拖動 **[!UICONTROL 頁腳]** 元件 ![樹擴展](assets/treeexpandall.png) 的雙曲餘切值。 在此階段，窗體如下所示：

   ![帶頁眉和頁腳的自適應格式](assets/adaptive-form-with-headers-and-footers.png)

## 第3步：添加元件以捕獲和顯示資訊 {#step-add-components-to-capture-and-display-information}

元件是自適應形式的構造塊。 AEM [!DNL Forms] 提供了許多元件，以便以自適應形式捕獲和顯示資訊。 可從 ![樹擴展](assets/treeexpandall.png) 的下界。 要瞭解可用元件和相應功能，請參閱 [創作自適應表單簡介](/help/forms/using/introduction-forms-authoring.md)。

1. 拖動 **[!UICONTROL 數字框元件]** 的雙曲餘切值。 將其置於頁腳元件之前。 開啟元件的屬性，更改 **[!UICONTROL 標題]** 到 **`Customer ID`**&#x200B;更改 **[!UICONTROL 元素名稱]** 至 **`customer_ID`**，啟用 **[!UICONTROL 必填欄位]** 選項，啟用 **[!UICONTROL 使用HTML5數字輸入類型]** 選項，然後按一下 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。
1. 將三個文本框元件拖到自適應窗體中。 將這些內容放在腳注元件之前。 為這些文本框設定以下屬性。:

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
      <td>客戶名稱<br /> </td> 
      <td>customer_shipping_address</td> 
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

1. 拖動 **[!UICONTROL 數字框]** 元件。 開啟元件的屬性，設定下表中列出的值，點擊 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   | 屬性 | 值 |
   |---|---|
   | 標題 | 郵遞區號 |
   | 元素名稱 | customer_ZIPCode |
   | 數字數量上限 | 6 |
   | 必填欄位 | 已啟用 |
   | 顯示圖案類型 | 無模式 |

1. 拖動 **[!UICONTROL 電子郵件]** 元件。 開啟元件的屬性，設定下表中列出的值，然後點擊 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   | 屬性 | 值 |
   |---|---|
   | 標題 | 電子郵件 |
   | 元素名稱 | customer_E-mail |
   | 必填欄位 | 已啟用 |

1. 拖動 **[!UICONTROL 檔案附件]** 元件。 開啟元件的屬性，設定下表中列出的值，然後點擊 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

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

1. 拖動 **[!UICONTROL 提交按鈕]** 到自適應窗體的元件。 將其置於頁腳元件之前。 開啟元件的屬性，將「元素名稱」更改為 `address_addition_update_submit`按一下 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。 表單的佈局已完成，表單如下所示：

   ![自適應形式 — 包含所有元件](assets/adaptive-form-with-all-the-components.png)

## 第4步：配置自適應表單的提交操作 {#step-configure-submit-action-for-the-adaptive-form}

當用戶點擊自適應表單上的「提交」按鈕時，將觸發提交操作。 您可以使用提交操作將表單資料保存到本地儲存庫、將表單資料發送到REST終結點、將表單資料作為電子郵件發送等。 自適應表單提供了更多現成的提交操作。 有關詳細資訊，請參見 [配置提交操作](/help/forms/using/configuring-submit-actions.md)。

使用以下步驟，您可以配置表單的電子郵件提交操作和演示提交操作：

1. 配置電子郵件伺服器。 有關詳細資訊，請參閱 [配置電子郵件通知](/help/sites-administering/notification.md)。


1. 點擊 **[!UICONTROL 窗體容器]** 在「內容」瀏覽器中按一下 ![招商](assets/cmppr.png)。 屬性瀏覽器在左側開啟。
1. 轉到 **[!UICONTROL 提交]** >  **[!UICONTROL 提交操作]**。 選擇 **[!UICONTROL 發送電子郵件]**。 指定以下值並點擊 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   | 屬性 | 值 |
   |--- |--- |
   | 從 | `donotreply@weretail.com` |
   | 至 | `${customer_Email}` |
   | 主旨 | 確認：您已在We.Retail網站上添加送貨地址。 |
   | 電子郵件範本 | 嗨 `${customer_Name}`，以下地址將添加為您帳戶的發運地址： <br>`${customer_Name}`。 `${customer_Shipping_Address}`。 `${customer_State}`。 `${customer_ZIPCode}`<br> 致謝，我們。零售 |
   | 包括附件 | 已啟用 |

   你的表格準備好了。 現在，您可以預覽表單並test功能。 如果您使用了本教程中提到的名稱並訪問運行的電腦上的表單AEM [!DNL Forms] 伺服器，則表單可在 [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)。

## 第5步：預覽並提交自適應表單 {#step-preview-and-submit-the-adaptive-form}

您可以使用 **[!UICONTROL 預覽選項]** 來評估窗體的外觀和行為。 您可以在預覽模式下提交表單，還可以檢查對表單應用的驗證。 例如，如果強制欄位為空時顯示錯誤。

自適應表單還提供了用於模擬各種設備的表單體驗的選項。 例如，iPhone、iPad和台式機。 您可以同時使用 **[!UICONTROL 預覽]** 和 **[!UICONTROL 模擬器]** ![尺](assets/ruler.png) 選項，以預覽不同螢幕大小設備的窗體。

1. 點擊 **[!UICONTROL 預覽]** 的上界。 窗體在預覽模式下開啟。 如果您使用了本教程中提到的名稱，則表單的預覽URL為 [http://localhost:4502/content/dam/formsanddocuments/shipping-address-add-update-form/jcr:content?wcmmode=disabled](http://localhost:4502/content/dam/formsanddocuments/shipping-address-addition-updation-form/jcr:content?wcmmode=disabled)
1. 使用 ![尺](assets/ruler.png) 查看窗體在各種設備上的顯示方式。
1. 填寫表單的欄位並點擊 **[!UICONTROL 提交]**。 表單已提交，您將重定向到預設 **謝謝** 的子菜單。 您還可以指定自定義感謝頁。 有關詳細資訊，請參閱 [配置重定向頁](/help/forms/using/configuring-redirect-page.md)。

添加地址的自適應表單已準備好。 如果您使用了本教程中提到的名稱並訪問運行AEM Forms伺服器的電腦上的表單，則表單可在 [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)。
