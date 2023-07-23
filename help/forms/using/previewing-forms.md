---
title: 預覽表單
seo-title: Previewing a form
description: 您可以在發佈或啟用表單前進行預覽，以確保表單符合預期。 預覽選項可能因支援的表單型別而異。
seo-description: You can preview your forms before publishing or activating to ensure it meets the expectations. Preview options may vary across the supported form types.
uuid: 9ec359ea-f518-441c-9c3d-e3c1ea07a532
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
feature: Adaptive Forms
exl-id: aed5703e-4fe6-4839-9657-c660ac48521e
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 4%

---

# 預覽表單 {#previewing-a-form}

<span class="preview"> Adobe建議使用現代化且可擴充的資料擷取 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 的 [建立新的Adaptive Forms](/help/forms/using/create-an-adaptive-form-core-components.md) 或 [將最適化Forms新增至AEM Sites頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). 這些元件代表最適化Forms建立工作取得重大進展，可確保提供令人驚歎的使用者體驗。 本文說明使用基礎元件製作最適化Forms的舊方法。 </span>

## 概觀 {#overview}

在AEM Forms中，您可以預覽存在於存放庫中的表單和檔案。 預覽有助於瞭解表單發佈給使用者時的確切外觀和行為。

預覽表單時，表單會以互動式介面呈現，使用者可以用資料填入表單。 預覽檔案時，會以非互動模式呈現，使用者只能檢視檔案。 對於表單，有其他自訂預覽選項可供使用。 使用此選項，您可以使用XML檔案中的資料預覽表單。 資料會填滿正在預覽之表單的部分或全部欄位。

下表列出適用於不同支援表單型別的預覽選項：

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
   <td>PDF預覽和透過資料預覽<br /> </td>
  </tr>
  <tr>
   <td>最適化表單</td>
   <td>使用資料的HTML預覽和HTML預覽</td>
  </tr>
  <tr>
   <td>表單範本</td>
   <td>PDF預覽、使用資料進行PDF預覽、HTML預覽、使用資料進行HTML預覽<br /> </td>
  </tr>
 </tbody>
</table>

## 預覽表單 {#previewing-a-form-1}

1. 選取您要預覽的資產，然後按一下預覽 ![aem6forms_preview](assets/aem6forms_preview.png) （在動作工具列中）。

   >[!NOTE]
   >
   >若要選取資產，請從預設的卡片檢視切換至清單檢視。 按一下 ![aem6forms_viewlist](assets/aem6forms_viewlist.png) 或 ![aem6forms_viewcard](assets/aem6forms_viewcard.png) 以切換檢視。

1. 按一下「預覽」會列出適用於所選資產型別的可能預覽選項。 按一下所需的選項，在新索引標籤中轉譯選取的資產。

   您的選項有：

   * 以HTML預覽
   * 以資料預覽
   * 以PDF預覽（適用於表單範本）

## 以資料預覽 {#preview-with-data}

當您選取 **使用資料預覽**，您可以檢視表單中輸入的真實資料的外觀。 「使用資料預覽」選項可讓您上傳包含範例使用者資料的XML。 範例使用者資料可用來以您選擇的格式填入預覽表單。

1. 選取資產，按一下預覽 ![aem6forms_preview](assets/aem6forms_preview.png)，並選取 **使用資料預覽**.
1. 在「預覽表單」對話方塊中，以XML檔案形式提供FormData。 按一下「預覽」，使用合併的來自XML的資料來轉譯表單。
