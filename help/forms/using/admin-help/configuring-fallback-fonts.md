---
title: 配置回退字型
seo-title: Configuring fallback fonts
description: 瞭解如何配置備用字型。
seo-description: Learn how to configure fallback fonts.
uuid: 2745541c-8c6d-4bb4-aa14-ec19afd6bc35
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d997a268-a40a-462d-badd-94f0731f7ba4
feature: PDF Generator
exl-id: 76dd2b0c-9f16-47bf-a565-99277be750fb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# 配置回退字型 {#configuring-fallback-fonts}

如果伺服器上沒有預設字型，可手動配置FontManagerResources.properties檔案AEM，將預設表單字型映射為回退（或替代）。 此屬性檔案位於adobe-fontmanager.jar檔案中。

>[!NOTE]
>
>回退字型配置也適用於匯編程式服務。

1. 導航到Adobe-Livecycle-*`[appserver]`*.ear檔案 *`[aem-forms root]`*/configurationManager/export目錄，建立備份副本，並取消包裝原始檔案。
1. 找到adobe-fontmanager.jar檔案並取消打包。
1. 找到FontManagerResources.properties檔案，然後在文本編輯器中開啟它。
1. 根據需要修改「一般」和「回退」字型位置和名稱，並保存檔案。

   FontManagerResources.properties檔案中的字型條目與 *`[aem-forms root]`*/fonts目錄。 如果指定的字型不是預設AEM的表單字型，則必須在此目錄結構中（在現有目錄中或新建立的目錄中）安裝這些字型。

   >[!NOTE]
   >
   >如果指定的字型或預設字型不包含特定的unicode字元或者該字元不可用，則根據以下優先順序從備用字型中取出該字元：

   * 特定於區域設定的字型
   * 如果未設定區域設定，則ROOT字型
   * 通用字型，按回退表中的順序集搜索

1. 重新打包adobe-fontmanager.jar檔案。
1. 重新打包Adobe-Livecycle-*`[appserver]`*.ear檔案，然後手動或通過運行Configuration Manager重新部署它。

>[!NOTE]
>
>不要使用Configuration Manager重新打包Adobe-livecycle-`[appserver]`.ear檔案，因為它將用表單預設值AEM覆蓋修改。
