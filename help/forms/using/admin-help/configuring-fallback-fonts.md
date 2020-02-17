---
title: 設定備援字型
seo-title: 設定備援字型
description: 瞭解如何設定備援字型。
seo-description: 瞭解如何設定備援字型。
uuid: 2745541c-8c6d-4bb4-aa14-ec19afd6bc35
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d997a268-a40a-462d-badd-94f0731f7ba4
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# 設定備援字型 {#configuring-fallback-fonts}

您可以手動設定FontManagerResources.properties檔案，將預設AEM表單字型對應至備援（或替代）（如果伺服器上沒有預設字型）。 此屬性檔案位於adobe-fontmanager.jar檔案中。

>[!NOTE]
>
>備援字型配置也適用於匯編器服務。

1. 導覽至&#x200B;*`[appserver]`*/configurationManager/export目錄中的adobe-livecycle- *`[aem-forms root]`*.ear檔案，製作備份副本，並解除封裝原稿。
1. 找到adobe-fontmanager.jar檔案並解除封裝。
1. 找到FontManagerResources.properties檔案，並在文本編輯器中將其開啟。
1. 視需要修改一般和備援字型位置和名稱，並儲存檔案。

   FontManagerResources.properties檔案中的字型條目與 *`[aem-forms root]`*/fonts目錄相關。 如果您指定的字型不是預設的AEM表單字型，則必須將此字型安裝在此目錄結構中（在現有目錄中或在新建立的目錄中）。

   >[!NOTE]
   >
   >如果指定的字型或預設字型不包含特定的Unicode字元，或者該字元不可用，則根據以下優先順序從備用字型提取該字元：

   * 地區設定特定字型
   * 如果未設定地區設定，則ROOT字型
   * 一般字型，依備援表格中的順序集搜尋

1. 重新封裝adobe-fontmanager.jar檔案。
1. 重新封裝adobe-livecycle-*`[appserver]`*.ear檔案，然後手動重新部署它，或執行Configuration Manager。

>[!NOTE]
>
>請勿使用Configuration manager重新封裝adobe-livecycle-`[appserver]`.ear檔案，因為它會以AEM表單的預設值覆寫您的修改。

