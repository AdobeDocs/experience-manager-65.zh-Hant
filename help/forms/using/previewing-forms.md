---
title: 預覽表單
description: 您可以在發佈或啟用表單前進行預覽，以確保表單符合預期。 預覽選項可能因支援的表單型別而異。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
feature: Adaptive Forms,Foundation Components
exl-id: aed5703e-4fe6-4839-9657-c660ac48521e
solution: Experience Manager, Experience Manager Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 7da902b6-fe94-5180-8e7c-f6d1e38d01d5
    internal-label: Foundation Components
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 21%
---
# 預覽表單 {#previewing-a-form}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，用來[建立新的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。 這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。 本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

## 概觀 {#overview}

在AEM Forms中，您可以預覽存放庫中呈現的表單和檔案。 預覽有助於瞭解表單發佈給使用者時的確切外觀和行為。

預覽表單時，表單會以互動式介面呈現，使用者可以使用資料填寫表單。 預覽檔案時，會以非互動模式呈現，使用者只能檢視檔案。 對於表單，還有一個自訂預覽選項可供使用。 使用此選項，您可以使用XML檔案中的資料來預覽表單。 資料會填滿正在預覽之表單的部分或所有欄位。

下表列出不同支援表單型別可用的預覽選項：

<table>
 <tbody>
  <tr>
   <td><strong>資產型別</strong><br /> </td>
   <td><strong>可用的預覽選項</strong><br /> </td>
  </tr>
  <tr>
   <td>文件</td>
   <td>PDF 預覽</td>
  </tr>
  <tr>
   <td>PDF 表單</td>
   <td>使用資料預覽和預覽PDF<br /> </td>
  </tr>
  <tr>
   <td>最適化表單</td>
   <td>包含資料的HTML預覽和HTML預覽</td>
  </tr>
  <tr>
   <td>表單範本</td>
   <td>PDF預覽、含資料的PDF預覽、HTML預覽、含資料的HTML預覽<br /> </td>
  </tr>
 </tbody>
</table>

## 預覽表單 {#previewing-a-form-1}

1. 選取您要預覽的資產，然後按一下動作工具列中的[預覽![aem6forms_preview](assets/aem6forms_preview.png)]。

   >[!NOTE]
   >
   >若要選取資產，請從預設的「卡片」檢視切換至「清單」檢視。 按一下![aem6forms_viewlist](assets/aem6forms_viewlist.png)或![aem6forms_viewcard](assets/aem6forms_viewcard.png)以切換檢視。

1. 按一下「預覽」會列出適用於所選資產型別的可能預覽選項。 按一下所需的選項，在新索引標籤中呈現選取的資產。

   您的選項有：

   * 以 HTML 預覽
   * 以資料預覽
   * 以PDF預覽（適用於表單範本）

## 以資料預覽 {#preview-with-data}

選取&#x200B;**使用資料預覽**&#x200B;時，您可以看到表單在輸入真實資料時的外觀。 使用資料預覽選項可讓您上傳包含範例使用者資料的XML。 範例使用者資料可用來以您選擇的格式填入預覽表單。

1. 選取資產，按一下「預覽![aem6forms_preview](assets/aem6forms_preview.png)」，然後選取「**使用資料預覽**」。
1. 在「預覽表單」對話方塊中，以XML檔案形式提供FormData。 按一下「預覽」，使用合併的來自XML的資料來呈現表單。
