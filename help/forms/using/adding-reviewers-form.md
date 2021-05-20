---
title: 將提交審核者與表單關聯
seo-title: 將提交審核者與表單關聯
description: 了解如何在AEM Forms中將提交審核者與表單建立關聯。 相關審核人員會審核通過表單門戶提交的表單。
seo-description: 了解如何在AEM Forms中將提交審核者與表單建立關聯。 相關審核人員會審核通過表單門戶提交的表單。
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
docset: aem65
feature: 適用性表單
exl-id: 46e7b858-44d1-41c8-9f44-4e959e593dc1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---

# 將提交審核者與表單{#associating-submission-reviewers-with-a-form}關聯

建立表單時，您可以指定透過表單入口網站審核表單提交內容並提供意見回饋的使用者。 貴組織可以收集提交表單的意見回饋和重新工作。

AEM Forms可讓您將審核者群組與表單建立關聯。 新增至表單審核群組的使用者可查看此表單的提交內容，並提供意見反應。

分配給表單的審核者組只能審核指定表單的提交。

## 必備條件 {#prerequisite}

### 使用中繼資料結構編輯器{#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}啟用適用性表單的提交審核者群組屬性

若要將審核者群組與表單建立關聯，請編輯最適化表單的中繼資料結構。 預設情況下，無法將審核者組添加到提交的表單中。

若要編輯中繼資料結構：

1. 在製作模式中，在「Experience Manager」下，按一下「**工具** > **資產** > **中繼資料結構**」。
1. 在「結構Forms」頁面中，導覽至「在AEM中撰寫的&#x200B;**Forms** > **Forms」。**

   頁面的URL為：

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. 選擇&#x200B;**適用性表單**&#x200B;並按一下&#x200B;**編輯**。
1. 在「編輯表單」頁中，按一下&#x200B;**Advanced**。
1. 在「進階」標籤中，拖放「建置表單」下可用的&#x200B;**單行文字**&#x200B;元件。
1. 選取新增的文字元件，以查看其設定。

   在「設定」下，在「映射到屬性」欄位中輸入`./jcr:content/metadata/form-submission-reviewer-group`。

   適用性表單的「進階」屬性中的提交審核者群組欄位會以您在「欄位標籤」下指定的名稱啟用。

## 將提交審核者與表單{#associating-submission-reviewers-with-a-form-1}關聯

若要將提交審核者與最適化表單建立關聯，請建立審核者群組並新增使用者。 在表單的進階屬性中的表單提交審核者欄位下，新增已建立的審核者群組。
使用者群組可讓您將不同的提交審核者集合與不同的最適化表單建立關聯。 此功能可防止未經授權的使用者檢閱提交作業。

執行下列步驟之前，請參閱[先決條件](../../forms/using/adding-reviewers-form.md#prerequisite)。

要建立組並向其添加成員，請導航至&#x200B;**工具** > **操作** > **安全** > **組**。
如需詳細資訊，請參閱[使用者管理與服務](/help/sites-administering/security.md)。
請確定您將建立的群組新增為現成可用使用者群組的成員：**forms-submission-reviewers**。 此使用者群組隨AEM Forms提供，可確保將使用者新增為提交審核者。

若要將使用者群組與最適化表單建立關聯：

1. 在製作模式中，導覽至&#x200B;**Forms** > **Forms與檔案**。
1. 使用**選擇**選項選擇最適化表單，然後按一下&#x200B;**查看屬性**。
1. 在表單的「屬性」窗口中，按一下「**編輯**」，然後按一下「**高級」**。
1. 在提交審核者組欄位中輸入組，然後按一下&#x200B;**Done**。

   「提交審核者組」欄位將與您在編輯的最適化表單中繼資料結構中指定的名稱一起顯示。

>[!NOTE]
>
>復寫使用者和表單，以確保AEM Forms遠端實作中的使用者和表單可供使用。
>
>確保將所有用戶複製為遠程實施中查看用戶組的成員。
