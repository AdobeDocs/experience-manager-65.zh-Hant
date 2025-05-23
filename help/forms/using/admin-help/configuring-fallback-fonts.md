---
title: 設定遞補字型
description: 瞭解如何設定AEM Forms的遞補字型。 您可以使用FontManagerResources.properties檔案，手動將預設字型對應到遞補字型。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 76dd2b0c-9f16-47bf-a565-99277be750fb
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# 設定遞補字型 {#configuring-fallback-fonts}

您可以手動設定FontManagerResources.properties檔案，將預設AEM Forms字型對應至備援（或替代），如果伺服器上無法使用預設字型。 此屬性檔案位於adobe-fontmanager.jar檔案中。

>[!NOTE]
>
>後援字型組態也適用於組合器服務。

1. 導覽至&#x200B;*`[aem-forms root]`*/configurationManager/export目錄中的adobe-livecycle-*`[appserver]`*.ear檔案、製作備份復本，並取消封裝原始檔案。
1. 找到adobe-fontmanager.jar檔案並將其解除封裝。
1. 找到FontManagerResources.properties檔案，然後在文字編輯器中開啟它。
1. 視需要修改「一般」和「後援」字型位置和名稱，並儲存檔案。

   FontManagerResources.properties檔案中的字型專案是相對於&#x200B;*`[aem-forms root]`*/fonts目錄。 如果您指定的字型不是預設的AEM表單字型，則必須將這些字型安裝在此目錄結構內（在現有目錄內或新建立的目錄中）。

   >[!NOTE]
   >
   >如果指定的字型或預設字型未包含特定的Unicode字元，或者無法使用字元，則會根據下列優先順序從備援字型取得字元：

   * 地區設定的特定字型
   * ROOT字型（如果未設定地區）
   * 一般字型，依遞補表格中的順序集搜尋

1. 重新封裝adobe-fontmanager.jar檔案。
1. 重新封裝adobe-livecycle-*`[appserver]`*.ear檔案，然後手動或執行Configuration Manager來重新部署。

>[!NOTE]
>
>請勿使用Configuration Manager重新封裝adobe-livecycle-`[appserver]`.ear檔案，因為這將以AEM表單預設值覆寫您的修改。
