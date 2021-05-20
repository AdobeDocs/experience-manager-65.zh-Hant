---
title: 自訂最適化表單的錯誤訊息版面配置和位置
seo-title: 自訂最適化表單的錯誤訊息版面配置和位置
description: '您可以自訂適用的錯誤訊息的版面配置和位置。 '
seo-description: '您可以自訂適用的錯誤訊息的版面配置和位置。 '
uuid: 6d3490f6-c867-44c9-a527-55f6d7221f99
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 136ac7e3-9d1f-4d58-bd4f-9dbe09eeafee
docset: aem65
exl-id: 5cb3ee55-f411-4692-84f7-89bf6ade729d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# 自定義自適應表單的錯誤消息佈局和定位{#customize-layout-and-positioning-of-error-messages-of-an-adaptive-form}

您可以自訂最適化表單的錯誤訊息版面配置和位置。 您可以執行下列自訂：

* 自訂欄位標題的位置和版面，而不對對應的CSS屬性進行任何變更
* 自訂內嵌錯誤訊息的位置
* 自訂動態說明指標的內容
* 自訂欄位元件（註解、介面工具集、簡短說明、長說明和說明指標元件）的位置，而不對對應的CSS屬性進行任何變更

## 自定義欄位佈局{#customize-layout-of-fields}

您可以自訂單一欄位或所有欄位的版面，以變更註解和錯誤訊息的位置。 執行下列步驟將自訂配置套用至欄位：

### 自定義單個欄位{#customize-layout-of-a-single-field}的佈局

執行下列步驟將自訂配置套用至單一欄位：

1. 在&#x200B;**Style**&#x200B;模式中開啟表單。 若要以樣式模式開啟表單，請在頁面工具列中點選![Canvas-drop-down](assets/canvas-drop-down.png) > **Style**。
1. 在側欄的&#x200B;**表單對象**&#x200B;下，選擇欄位並點選編輯按鈕![edit-button](assets/edit-button.png)。
1. 選取要自訂欄位的狀態，並指定該狀態的樣式。

   ![指定欄位的內嵌樣式](assets/edit-error-state.png)

### 自定義表單{#customize-layout-of-all-the-fields-of-a-form}中所有欄位的佈局

透過AEM Forms，您現在可以建立主題並套用至表單。 主題編輯器可讓您在單一位置指定表單元件的樣式。 建立主題時，需在元件層級指定樣式。 有關主題的詳細資訊，請參閱[AEM Forms中的主題](../../forms/using/themes.md)。

使用主題編輯器建立主題，以自訂表單中所有欄位的版面。 建立主題後，請執行下列步驟將其應用於表單：

1. 在編輯模式中開啟表單。
1. 在編輯模式中，選取元件，然後點選![欄位層級](assets/field-level.png) > **適用性表單容器**，然後點選![cmppr](assets/cmppr.png)。
1. 在側欄的「最適化表單主題」下方，選取您使用主題編輯器建立的主題。

## 建立自訂欄位配置{#create-a-custom-field-layout}

1. 開啟CRXDE lite。 預設URL為https://&#39;[server]:[port]&#39;/crx/de。
1. 將欄位佈局從/libs/fd/af/layouts/field節點（例如，defaultFieldLayout）複製到/apps節點（例如， /apps/af-field-layout）。
1. 更名複製的節點和defaultFieldLayout.jsp檔案。 例如， errorOnRight.jsp。

1. 更改複製節點的qtip和jcr:description屬性的值。 例如，將屬性的值變更為「Error On Right」

1. 若要新增樣式和行為，請在/etc節點中建立用戶端程式庫。

   例如，在/etc/af-field-layout-clientlib位置，建立節點client-library。 使用值af.field.errorOnRight和style.less檔案添加categories屬性，其中包含以下代碼：

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

1. 要增強外觀和行為，請包括在佈局檔案(errorOnRight.jsp)中建立的客戶端庫。
1. 開啟欄位的編輯對話方塊，選取&#x200B;**Styling**&#x200B;標籤。 在&#x200B;**配置欄位佈局**&#x200B;下拉框中，選擇新建的佈局，然後按一下&#x200B;**確定**。

ErrorOnRight.zip套件包含的程式碼會顯示欄位右側的錯誤訊息。

[取得檔案](assets/erroronright.zip)
