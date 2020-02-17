---
title: 預覽表格
seo-title: 預覽表格
description: 您可以在發佈或啟動表單之前先預覽表單，以確保表單符合預期。 預覽選項可能會因支援的表單類型而異。
seo-description: 您可以在發佈或啟動表單之前先預覽表單，以確保表單符合預期。 預覽選項可能會因支援的表單類型而異。
uuid: 9ec359ea-f518-441c-9c3d-e3c1ea07a532
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 預覽表格 {#previewing-a-form}

## 概覽 {#overview}

在AEM Forms中，您可以預覽儲存庫中顯示的表單和檔案。 預覽功能有助於確切瞭解表單在發佈給使用者時的外觀和行為。

在預覽表格時，這些表格會以互動式介面呈現，使用者可以用資料填入表格。 在預覽檔案時，它們會以非互動模式呈現，而使用者只能檢視檔案。 對於表單，另有「自訂預覽」選項可供使用。 使用此選項，您可以使用XML檔案中的資料來預覽表格。 資料會填滿正在預覽的表單的部分或全部欄位。

下表列出了可用於不同類型支援表單的預覽選項：

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
   <td>PDF表格</td>
   <td>PDF預覽與預覽資料<br /> </td>
  </tr>
  <tr>
   <td>自適應形式</td>
   <td>HTML預覽與HTML預覽與資料</td>
  </tr>
  <tr>
   <td>表單範本</td>
   <td>PDF預覽、PDF預覽與資料、HTML預覽與HTML預覽與資料<br /> </td>
  </tr>
 </tbody>
</table>

## 預覽表格 {#previewing-a-form-1}

1. 選取您要預覽的資產，然後按一下動作工具 ![列中的「預覽aem6forms_preview](assets/aem6forms_preview.png) 」。

   >[!NOTE]
   >
   >若要選取資產，請從預設的卡片檢視切換至清單檢視。 按一 ![下aem6forms_viewlist](assets/aem6forms_viewlist.png) 或 ![aem6forms_viewcard](assets/aem6forms_viewcard.png) ，以切換檢視。

1. 按一下「預覽」會列出適用於所選資產類型的可能預覽選項。 按一下所要的選項，在新標籤中呈現選取的資產。

   您的選項包括：

   * 預覽為HTML
   * 以資料預覽
   * 預覽為PDF（可用於表單範本）

## 以資料預覽 {#preview-with-data}

當您選取「使 **用資料預覽**」時，您可以看到表格與輸入的實際資料的外觀。 「使用資料預覽」選項可讓您上傳包含範例使用者資料的XML。 範例使用者資料可用來以您選擇的格式填入預覽表格。

1. 選取資產，按一下「預 ![覽aem6forms_preview](assets/aem6forms_preview.png)」，然後選取「 **預覽資料」**。
1. 在「預覽表單」對話方塊中，將FormData提供為XML檔案。 按一下「預覽」，以XML中合併的資料來轉換表格。

