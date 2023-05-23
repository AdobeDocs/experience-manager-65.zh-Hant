---
title: 預覽窗體
seo-title: Previewing a form
description: 您可以在發佈或激活表單之前預覽表單，以確保它符合預期。 預覽選項可能因支援的表單類型而異。
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

# 預覽窗體 {#previewing-a-form}

## 概觀 {#overview}

在AEM Forms，您可以預覽儲存庫中存在的表單和文檔。 預覽有助於確切瞭解表單在發佈給最終用戶時的外觀和行為。

在預覽表單時，這些表單會在交互介面中呈現，用戶可以用資料填充表單。 在預覽文檔時，它們會以非交互模式呈現，用戶只能查看文檔。 對於表單，還提供了「自定義預覽」的附加選項。 使用此選項，可以使用XML檔案中的資料預覽表單。 資料填充正在預覽的表單的部分或全部欄位。

下表列出了可用於不同類型的受支援表單的預覽選項：

<table>
 <tbody>
  <tr>
   <td><strong>資產類型</strong><br /> </td>
   <td><strong>可用預覽選項</strong><br /> </td>
  </tr>
  <tr>
   <td>文件</td>
   <td>PDF預覽</td>
  </tr>
  <tr>
   <td>PDF窗體</td>
   <td>PDF預覽和預覽資料<br /> </td>
  </tr>
  <tr>
   <td>自適應形式</td>
   <td>HTML預覽和HTML預覽（帶資料）</td>
  </tr>
  <tr>
   <td>表單模板</td>
   <td>PDF預覽、PDF資料預覽、HTML預覽、HTML資料預覽<br /> </td>
  </tr>
 </tbody>
</table>

## 預覽窗體 {#previewing-a-form-1}

1. 選擇要預覽的資產，然後按一下「預覽」 ![aem6forms_preview](assets/aem6forms_preview.png) 的子菜單。

   >[!NOTE]
   >
   >要選擇資產，請從預設的卡視圖切換到清單視圖。 按一下 ![aem6forms_viewlist](assets/aem6forms_viewlist.png) 或 ![aem6forms_viewcard](assets/aem6forms_viewcard.png) 切換視圖。

1. 按一下「預覽」(Preview)將列出適用於選定資產類型的可能預覽選項。 按一下所需選項以在新頁籤中呈現所選資產。

   您的選項包括：

   * 預覽為HTML
   * 以資料預覽
   * 預覽為PDF（可用於表單模板）

## 以資料預覽 {#preview-with-data}

選擇時 **使用資料預覽**，您可以查看表單與輸入到表單中的實際資料的外觀。 使用資料預覽選項可以上載包含示例用戶資料的XML。 示例用戶資料用於以您選擇的格式填充預覽表單。

1. 選擇資產，按一下預覽 ![aem6forms_preview](assets/aem6forms_preview.png)，然後選擇 **使用資料預覽**。
1. 在「預覽表單」對話框中，將FormData作為XML檔案提供。 按一下「預覽」(Preview)，使用XML中的合併資料呈現表單。
