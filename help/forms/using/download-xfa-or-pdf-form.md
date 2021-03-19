---
title: 下載XFA或PDF表單範本
seo-title: 下載XFA或PDF表單範本
description: 您可以將表單從儲存庫導出到本地系統，並將下載的表單遷移到新儲存庫。
seo-description: 您可以將表單從儲存庫導出到本地系統，並將下載的表單遷移到新儲存庫。
uuid: 5f7fbd14-cb9d-4749-8708-7efe49df89d7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 6699e0e7-fd42-41ae-86a2-3b940d905111
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---


# 下載XFA或PDF表單範本{#download-an-xfa-or-a-pdf-form-template}

如名稱所示，下載操作可讓您將表單從儲存庫導出到本地系統。 此操作與上載操作相結合，可幫助您將表單從一個儲存庫遷移到另一個儲存庫。

在AEM Forms，下載作業支援下列資產類型：

* 表單範本(XFAForms)
* PDF forms
* 檔案（平面PDF檔案）

AEM Forms支援個別下載這些表格類型，或在包含一或多個支援表格的資料夾中下載。

除了這些資產外，如果`Resource`類型的資產存在於資料夾中，您也可以下載該資產。 此功能可讓您下載XFA表單所參照的資源以及表單。

## 下載一或多個表單{#download-one-or-more-forms}

1. 登錄至`https://<server>:<port>/aem/forms.html`的AEM Forms用戶介面。

1. 導覽至您要下載的資產所在的位置。

1. 選取資產。 按一下工具列中的&#x200B;**[!UICONTROL Download]** ![ aem6forms_download](assets/aem6forms_download.png)圖示。

   >[!NOTE]
   >
   >您只能選擇一個表單供下載。 如果您想要下載多個表格，則必須將其下載為資料夾。

1. 在出現的對話方塊中，按一下「下載&#x200B;**[!UICONTROL 」。]**

   AEM Forms生成包含選定檔案或選定資料夾的ZIP檔案。

   如果您正在下載資料夾，資料夾內的受支援資產會下載至其現有階層。

   ZIP檔案將保存到系統上的`Downloads`資料夾。

## 上載操作{#related-considerations-for-the-upload-operation}的相關注意事項

* 您可以將ZIP檔案上載到同一儲存庫或另一個儲存庫中的任何其他位置
* 在上傳作業期間，資料夾中資產的階層會保留
* 下載前對下載資產所做的任何中繼資料變更，都會在上傳時反映

