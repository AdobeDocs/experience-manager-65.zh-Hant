---
title: 下載XFA或PDF表單模板
seo-title: Download an XFA or a PDF form template
description: 您可以將表單從儲存庫導出到本地系統，並將下載的表單遷移到新儲存庫。
seo-description: You can export forms from the repository to the local system and migrate the downloaded forms to new repository.
uuid: 5f7fbd14-cb9d-4749-8708-7efe49df89d7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 6699e0e7-fd42-41ae-86a2-3b940d905111
role: Admin
exl-id: 5b7b9816-38c1-4780-b1fc-8184971f3772
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# 下載XFA或PDF表單模板 {#download-an-xfa-or-a-pdf-form-template}

如名稱所示，下載操作允許您將表單從儲存庫導出到本地系統。 與上載操作結合使用，此操作可幫助您將表單從一個儲存庫遷移到另一個儲存庫。

在AEM Forms，以下資產類型支援下載操作：

* 表單模板(XFAForms)
* PDF forms
* 文檔(平面PDF檔案)

AEM Forms支援單獨或在包含一個或多個受支援表單的資料夾中下載這些表單類型。

除了這些資產外，您還可以下載 `Resource` 資產類型（如果它存在於資料夾中）。 提供此功能後，您可以下載XFA表單所引用的資源以及表單。

## 下載一個或多個表單 {#download-one-or-more-forms}

1. 登錄AEM Forms用戶介面 `https://<server>:<port>/aem/forms.html`。

1. 導航到要下載的資產的位置。

1. 選擇資產。 按一下 **[!UICONTROL 下載]** ![aem6forms_download](assets/aem6forms_download.png) 的子菜單。

   >[!NOTE]
   >
   >您只能選擇一個表單進行下載。 如果要下載多個表單，則必須將其作為資料夾下載。

1. 在出現的對話框中，按一下 **[!UICONTROL 下載]**。

   AEM Forms生成包含選定檔案或選定資料夾的ZIP檔案。

   如果正在下載資料夾，則資料夾內支援的資產將在其現有層次結構中下載。

   ZIP檔案將保存到 `Downloads` 資料夾。

## 上載操作的相關注意事項 {#related-considerations-for-the-upload-operation}

* 您可以將ZIP檔案上載到同一儲存庫或另一個儲存庫中的任何其他位置
* 在上載操作期間保留資料夾中資產的層次結構
* 下載前對下載的資產所做的任何元資料更改都會在上載時反映
