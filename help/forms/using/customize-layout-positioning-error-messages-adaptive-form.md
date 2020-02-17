---
title: 自訂最適化表單的錯誤訊息版面配置和位置
seo-title: 自訂最適化表單的錯誤訊息版面配置和位置
description: '您可以自訂最適化錯誤訊息的版面配置和位置。 '
seo-description: '您可以自訂最適化錯誤訊息的版面配置和位置。 '
uuid: 6d3490f6-c867-44c9-a527-55f6d7221f99
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 136ac7e3-9d1f-4d58-bd4f-9dbe09eeafee
docset: aem65
translation-type: tm+mt
source-git-commit: 9d90bc5f77f827925e3e1ecd12d56a94a2bbae30

---


# 自訂最適化表單的錯誤訊息版面配置和位置{#customize-layout-and-positioning-of-error-messages-of-an-adaptive-form}

您可以自訂最適化表單的錯誤訊息的版面配置和位置。 您可以執行下列自訂：

* 自訂欄位標題的位置和版面配置，而不需對對應的CSS屬性做任何變更
* 自訂內嵌錯誤訊息的位置
* 自訂動態說明指標的內容
* 自訂欄位元件（標題、介面工具集、簡短說明、詳細說明和說明指示元件）的位置，而不需對對應的CSS屬性進行任何變更

## 自訂欄位版面 {#customize-layout-of-fields}

您可以自訂單一欄位或所有欄位的版面配置，以變更標題和錯誤訊息的位置。 執行下列步驟，將自訂版面套用至欄位：

### 自訂單一欄位的版面配置 {#customize-layout-of-a-single-field}

執行下列步驟，將自訂版面套用至單一欄位：

1. 在樣式模式下 **開啟表** 格。 若要在樣式模式中開啟表格，請在頁面工具列中點選「畫 ![布下拉式清單](assets/canvas-drop-down.png) >樣 **式」**。
1. 在側欄的「表單物 **件」下**，選取欄位並點選「編輯」 ![按鈕編輯按鈕](assets/edit-button.png)。
1. 選取您要自訂的欄位狀態，並指定該狀態的樣式。

   ![指定欄位的內嵌樣式](assets/edit-error-state.png)

### 自訂表單中所有欄位的版面配置 {#customize-layout-of-all-the-fields-of-a-form}

有了AEM Forms，您現在可以建立主題並套用至表單。 主題編輯器可讓您在單一位置指定表單元件的樣式。 當您建立主題時，可在元件層級指定樣式。 如需主題的詳細資訊，請參閱「 [AEM Forms中的主題」](../../forms/using/themes.md)。

使用主題編輯器建立主題，以自訂表單中所有欄位的版面配置。 建立主題後，請執行下列步驟，將其套用至表單：

1. 在編輯模式下開啟表格。
1. 在編輯模式中，選取元件，然後點選欄 ![位層級](assets/field-level.png) > **最適化表單容器**，然後點選 ![cmppr](assets/cmppr.png)。
1. 在側欄的「最適化表單主題」下，選取您使用主題編輯器建立的主題。

## 建立自訂欄位版面 {#create-a-custom-field-layout}

1. 開啟CRXDE lite。 預設URL為https://[Server]:[Port]/crx/de。
1. 將欄位版面從/libs/fd/af/layouts/field節點（例如defaultFieldLayout）複製至/apps節點（例如/apps/af-field-layout）。
1. 重新命名複製的節點和defaultFieldLayout.jsp檔案。 例如，errorOnRight.jsp。

1. 更改複製節點的qtip和jcr:description屬性的值。 例如，將屬性的值更改為「右側出現錯誤」

1. 若要新增樣式和行為，請在/etc節點中建立用戶端程式庫。

   例如，在/etc/af-field-layout-clientlib位置，建立節點client-library。 新增包含值af.field.errorOnRight和style.less檔案的類別屬性，並包含以下程式碼：

   ```css
   .widgetErrorWrapper {
   
    height: 38px;
    margin: 5px;
   
    .guideFieldWidget{
    width: 60%;
    float: left; 
    }
   
    .guideFieldError{
    overflow:hidden;
    width:40%; 
    }
   
   }
   ```

1. 若要增強外觀和行為，請將在版面檔案(errorOnRight.jsp)中建立的用戶端程式庫包含在內。
1. 開啟欄位的編輯對話框，選擇「樣 **式** 」頁籤。 在「設 **定欄位配置** 」下拉式方塊中，選取新建立的配置，然後按一下「 **確定」**。

ErrorOnRight.zip套件包含在欄位右側顯示錯誤訊息的程式碼。

[取得檔案](assets/erroronright.zip)
