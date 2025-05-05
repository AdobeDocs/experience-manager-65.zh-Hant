---
title: 將提交稽核者與表單建立關聯
description: 瞭解如何在AEM Forms中將提交稽核者與表單建立關聯。 相關聯的稽核者稽核透過表單入口網站提交的表單。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 46e7b858-44d1-41c8-9f44-4e959e593dc1
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 9%

---

# 將提交稽核者與表單建立關聯 {#associating-submission-reviewers-with-a-form}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant)，用來[建立新的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

建立表單時，您可以指定透過表單入口網站稽核表單提交內容並提供意見回饋的使用者。 您的組織可以收集意見並對提交的表單進行重新處理。

AEM Forms可讓您將檢閱者群組與表單建立關聯。 新增至表單稽核群組的使用者可以檢視此表單的提交內容，並提供意見反應。

指派給表單的稽核者群組只能稽核指定表單的提交。

## 必備條件 {#prerequisite}

### 使用中繼資料結構編輯器啟用最適化表單的提交稽核者群組屬性 {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

若要將稽核者群組與表單建立關聯，請編輯最適化表單的中繼資料結構。 依預設，您無法將稽核者群組新增至提交的表單。

若要編輯中繼資料結構：

1. 在作者模式的Experience Manager底下，按一下&#x200B;**工具** > **Assets** > **中繼資料結構描述**。
1. 在「結構描述Forms」頁面中，導覽至&#x200B;**Forms** > **在AEM中撰寫的Forms。**

   頁面的URL為：

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. 選取&#x200B;**最適化表單**&#x200B;並按一下&#x200B;**編輯**。
1. 在[編輯表單]頁面中，按一下[**進階**]。
1. 在[進階]索引標籤中，拖放[建置表單]下可用的&#x200B;**單行文字**&#x200B;元件。
1. 選取新增的文字元件以檢視其設定。

   在[設定]下，在[對應至屬性]欄位中輸入`./jcr:content/metadata/form-submission-reviewer-group`。

   您的最適化表單的「進階」屬性中的「提交稽核者群組」欄位會以您在「欄位標籤」下指定的名稱啟用。

## 將提交稽核者與表單建立關聯 {#associating-submission-reviewers-with-a-form-1}

若要將提交稽核者與最適化表單建立關聯，請建立稽核者群組並新增使用者。 在表單的進階屬性中，於表單提交稽核者欄位下新增建立的稽核者群組。
使用者群組可讓您將不同的提交稽核者集與不同的調適型表單建立關聯。 此功能可防止未經授權的使用者進行提交稽核。

執行以下步驟之前，請參閱[先決條件](../../forms/using/adding-reviewers-form.md#prerequisite)。

若要建立群組並新增成員，請瀏覽至&#x200B;**工具** > **作業** > **安全性** > **群組**。
如需詳細資訊，請參閱[使用者管理與服務](/help/sites-administering/security.md)。
請確定您將建立的群組新增為現成使用者群組的成員： **forms-submission-reviewers**。 此使用者群組隨附於AEM Forms，可確保將使用者新增為提交稽核者。

若要將使用者群組與最適化表單建立關聯：

1. 在撰寫模式中，導覽至&#x200B;**Forms** > **Forms和檔案**。
1. 使用&#x200B;**選取**&#x200B;選項選取最適化表單，然後按一下&#x200B;**檢視屬性**。
1. 在表單的[內容]視窗中，按一下[**編輯**]，然後按一下[**進階**]。
1. 在提交稽核者群組欄位中輸入群組，然後按一下&#x200B;**完成**。

   提交稽核者群組欄位會以您在已編輯的最適化表單中繼資料結構描述中指定的名稱顯示。

>[!NOTE]
>
>複製使用者和表單，以確保AEM Forms遠端實作中的使用者和表單可用性。
>
>確定所有使用者都復寫為檢閱遠端實作中使用者群組的成員。
