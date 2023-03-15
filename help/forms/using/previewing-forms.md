---
title: 預覽表單
seo-title: Previewing a form
description: 您可以在發佈或啟動表單之前進行預覽，確保表單符合預期。 預覽選項可能因支援的表單類型而異。
seo-description: You can preview your forms before publishing or activating to ensure it meets the expectations. Preview options may vary across the supported form types.
uuid: 9ec359ea-f518-441c-9c3d-e3c1ea07a532
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
feature: Adaptive Forms
exl-id: aed5703e-4fe6-4839-9657-c660ac48521e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 2%

---

# 預覽表單 {#previewing-a-form}

## 概觀 {#overview}

在AEM Forms中，您可以預覽存放庫中顯示的表單和檔案。 預覽有助於確切了解表單發佈給使用者時的外觀和行為。

預覽表單時，表單會以互動式介面呈現，使用者可以用資料填入表單。 預覽文檔時，它們以非交互模式呈現，用戶只能查看文檔。 若是表單，則另有自訂預覽選項可供使用。 使用此選項，可以使用XML檔案中的資料預覽表單。 資料會填滿正在預覽之表單的部分或全部欄位。

下表列出不同支援表單類型可用的預覽選項：

<table>
 <tbody>
  <tr>
   <td><strong>資產類型</strong><br /> </td>
   <td><strong>可用的預覽選項</strong><br /> </td>
  </tr>
  <tr>
   <td>文件</td>
   <td>PDF預覽</td>
  </tr>
  <tr>
   <td>PDF表單</td>
   <td>PDF預覽和預覽資料<br /> </td>
  </tr>
  <tr>
   <td>適用性表單</td>
   <td>HTML預覽和HTML預覽（使用資料）</td>
  </tr>
  <tr>
   <td>表單範本</td>
   <td>PDF預覽、PDF預覽與資料、HTML預覽、HTML預覽與資料<br /> </td>
  </tr>
 </tbody>
</table>

## 預覽表單 {#previewing-a-form-1}

1. 選取您要預覽的資產，然後按一下「預覽」 ![aem6forms_preview](assets/aem6forms_preview.png) （在操作工具欄中）。

   >[!NOTE]
   >
   >若要選取資產，請從預設的卡片檢視切換至清單檢視。 按一下 ![aem6forms_viewlist](assets/aem6forms_viewlist.png) 或 ![aem6forms_viewcard](assets/aem6forms_viewcard.png) 切換檢視。

1. 按一下「預覽」會列出適用於所選資產類型的可能預覽選項。 按一下所需的選項，在新索引標籤中呈現選取的資產。

   您的選項為：

   * 預覽為HTML
   * 以資料預覽
   * 預覽為PDF（適用於表單範本）

## 以資料預覽 {#preview-with-data}

選取 **使用資料預覽**，您就會看到表單中輸入的真實資料外觀。 使用資料預覽選項可讓您上傳包含範例使用者資料的XML。 範例使用者資料可用來以您選擇的格式填入預覽表單。

1. 選取資產，按一下「預覽」 ![aem6forms_preview](assets/aem6forms_preview.png)，然後選取 **使用資料預覽**.
1. 在「預覽表單」對話框中，將FormData作為XML檔案提供。 按一下「預覽」，使用XML中的合併資料呈現表單。
