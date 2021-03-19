---
title: 將提交審核者與表單建立關聯
seo-title: 將提交審核者與表單建立關聯
description: 瞭解如何將提交審核者與AEM Forms的表格建立關聯。 相關審核者會檢閱透過表單入口網站提交的表單。
seo-description: 瞭解如何將提交審核者與AEM Forms的表格建立關聯。 相關審核者會檢閱透過表單入口網站提交的表單。
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
docset: aem65
feature: 適用性表單
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---


# 將提交審核者與表單{#associating-submission-reviewers-with-a-form}關聯

當您建立表單時，您可以指定透過表單入口網站審核表單提交的使用者並提供意見回應。 您的組織可以收集意見回應並重新製作已提交的表單。

AEM Forms允許您將審核者組與表單關聯。 新增至表單審核群組的使用者可檢視此表單的提交內容，並提供意見回應。

分配給表單的審核者組只能審核指定表單的提交。

## 必備條件 {#prerequisite}

### 使用元資料架構編輯器{#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}為自適應表單啟用提交審核者組屬性

要將審核者組與表單關聯，請編輯最適化表單的元資料模式。 預設情況下，無法將審核者組添加到已提交的表單中。

要編輯元資料結構：

1. 在作者模式中，在Experience Manager下，按一下「工具&#x200B;**** > **資產** > **中繼資料結構**」。
1. 在「方案Forms」頁中，導航至&#x200B;**Forms** > **以AEM.**&#x200B;創作的Forms

   頁面的URL為：

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. 選擇&#x200B;**最適化表單**&#x200B;並按一下&#x200B;**編輯**。
1. 在「編輯表單」頁中，按一下&#x200B;**高級**。
1. 在「進階」索引標籤中，拖放「建置表單」下方的&#x200B;**單行文字**&#x200B;元件。
1. 選取新增的文字元件，以檢視其設定。

   在「設定」下，在「映射到屬性」欄位中輸入`./jcr:content/metadata/form-submission-reviewer-group`。

   在最適化表單的「進階」屬性中，會啟用「欄位標籤」下您指定的名稱的提交審核者群組欄位。

## 將提交審核者與表單{#associating-submission-reviewers-with-a-form-1}關聯

要將提交審核者與適應性表單關聯，請建立審核者組並向其添加用戶。 在表單的高級屬性中，在表單提交審核者欄位下添加建立的審核者組。
使用者群組可讓您將不同的提交審核者集合與不同的調適性表單建立關聯。 此功能可防止未經授權的使用者進行提交審核。

執行以下步驟之前，請參閱[先決條件](../../forms/using/adding-reviewers-form.md#prerequisite)。

要建立組並向其添加成員，請導航至&#x200B;**工具** > **操作** > **安全** > **組**。
如需詳細資訊，請參閱[使用者管理與服務](/help/sites-administering/security.md)。
請確定您新增所建立的群組，成為現成可用的使用者群組的成員：**forms-submission-reviewers**。 此使用者群組隨附於AEM Forms，可確保將使用者新增為提交審核者。

要將用戶組與最適化表單關聯：

1. 在編寫模式中，導覽至&#x200B;**Forms** > **Forms與檔案**。
1. 使用**選擇**選項選擇自適應表單，然後按一下&#x200B;**查看屬性**。
1. 在表單的「屬性」窗口中，按一下「編輯」，然後按一下「**編輯」，然後按一下「**&#x200B;高級」。****
1. 在提交審核者組欄位中輸入組，然後按一下&#x200B;**Done**。

   此時將顯示提交審閱者組欄位，其名稱與您在編輯的自適應表單元資料模式中指定的名稱相同。

>[!NOTE]
>
>複製用戶和表單，以確保用戶和表單在AEM Forms遠程實施中可用。
>
>確保所有用戶都被複製為遠程實施中查看用戶組的成員。

