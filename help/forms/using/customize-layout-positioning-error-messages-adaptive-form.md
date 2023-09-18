---
title: 自訂最適化表單的錯誤訊息佈局和位置
description: 您可以自訂最適化之錯誤訊息的版面配置和位置。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 5cb3ee55-f411-4692-84f7-89bf6ade729d
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# 自訂最適化表單的錯誤訊息佈局和位置{#customize-layout-and-positioning-of-error-messages-of-an-adaptive-form}

您可以自訂最適化表單的錯誤訊息版面配置和位置。 您可以執行下列自訂：

* 自訂欄位標題的位置和版面配置，而不變更對應的CSS屬性
* 自訂內嵌錯誤訊息的位置
* 自訂動態說明指標的內容
* 自訂欄位元件（標題、Widget、簡短說明、完整說明和說明指標元件）的位置，而不變更對應的CSS屬性

## 自訂欄位佈局 {#customize-layout-of-fields}

您可以自訂單一欄位或所有欄位的版面配置，以變更註解和錯誤訊息的位置。

若要將自訂配置套用至欄位，請執行下列動作：

### 自訂單一欄位的版面 {#customize-layout-of-a-single-field}

1. 在中開啟表單 **樣式** 模式。 若要以樣式模式開啟表單，請在頁面工具列中點選 ![畫佈下拉式清單](assets/canvas-drop-down.png) > **樣式**.
1. 在側邊欄中的下方 **表單物件**，選取欄位並點選編輯按鈕 ![編輯按鈕](assets/edit-button.png).
1. 選取您要自訂的欄位狀態，並指定該狀態的樣式。

   ![指定欄位的內嵌樣式](assets/edit-error-state.png)

### 自訂表單所有欄位的版面 {#customize-layout-of-all-the-fields-of-a-form}

透過AEM Forms，您現在可以建立佈景主題並將其套用至您的表單。 主題編輯器可讓您在一個位置指定表單元件的樣式。 建立主題時，您可在元件層級指定樣式。 如需主題的詳細資訊，請參閱 [AEM Forms中的主題](../../forms/using/themes.md).

使用主題編輯器建立主題，以自訂表單中所有欄位的版面。 建立主題後，請執行下列步驟以將其套用至表單：

1. 在編輯模式中開啟您的表單。
1. 在編輯模式中，選取元件，然後點選 ![欄位層級](assets/field-level.png) > **最適化表單容器**，然後點選 ![cmppr](assets/cmppr.png).
1. 在側邊欄中的「最適化表單主題」下方，選取您使用「主題編輯器」建立的主題。

## 建立自訂欄位佈局 {#create-a-custom-field-layout}

1. 開啟 CRXDE Lite。預設URL為https://&#39;[伺服器]：[連線埠]&#39;/crx/de.
1. 將欄位配置從/libs/fd/af/layouts/field節點（例如defaultFieldLayout）複製到/apps節點（例如/apps/af-field-layout）。
1. 重新命名複製的節點和defaultFieldLayout.jsp檔案。 例如，errorOnRight.jsp。

1. 變更所複製節點的qtip和jcr：description屬性的值。 例如，將屬性的值變更為Error On Right

1. 若要新增樣式和行為，請在/etc節點中建立使用者端程式庫。

   例如，在/etc/af-field-layout-clientlib位置，建立節點client-library。 使用下列程式碼，以值af.field.errorOnRight和style.less檔案新增categories屬性：

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

1. 若要增強外觀和行為，請在版面配置檔案(errorOnRight.jsp)中包含建立的使用者端程式庫。
1. 開啟欄位的編輯對話方塊並選取 **樣式** 標籤。 在 **設定欄位佈局** 下拉式方塊，選取新建立的版面，然後按一下 **確定**.

ErrorOnRight.zip套件包含可在欄位右側顯示錯誤訊息的程式碼。

[取得檔案](assets/erroronright.zip)
