---
title: 升級至 AEM 6.5 Forms
seo-title: Upgrade to AEM 6.5 Forms
description: 您可以執行從AEM6.3Forms和AEM6.4Forms到6.AEM5Forms的直接升級。
seo-description: You can perform a direct upgrade from AEM 6.3 Forms and AEM 6.4 Forms to AEM 6.5 Forms.
uuid: 7a38cd72-2d01-4af7-b6a3-00dc34c4f02b
content-type: reference
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f89921ef-c638-4a07-88d5-3dd8614c5166
docset: aem65
role: Admin
exl-id: 2fc8abec-8ba6-40b7-bbb1-4288eeea7c86
source-git-commit: a98550c11405e6d0f43ff7ed8905644a3aedd78c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 2%

---

# 升級至 AEM 6.5 Forms{#upgrade-to-aem-forms}

6AEM.5Forms包括若干新功能和增強功能，這些功能和增強功能簡化了表單和對應的建立、管理和用戶體驗。 要瞭解6.5Forms的所有新功能和AEM增強功能，請參見 [新功能摘要文檔](../../forms/using/whats-new.md)。

您可以升級現有LiveCycle或AEM Forms安裝，以獲得Forms6.5版中提供的新功能和增強功能AEM，同時保持現有資料、流程和資產完好無損。 在升級時，還保留這些進程的元資料和狀態。 您可以選擇升級路徑以開始升級。

下圖顯示OSGi上AEM Forms的可用升級路徑：

![](do-not-localize/osgi-upgrade-path.png)

您可以從以下位置執行直接升級：

* OSGiAEM上的6.3Forms
* AEMOSGi上的Forms6.4

您還可以從

* OSGiAEM上的Forms6.0
* OSGiAEM上的6.1Forms
* OSGiAEM上的6.2Forms

下圖顯示JEE上AEM Forms的可用升級路徑：

![](do-not-localize/jee-upgrade-6-5.png)

您可以從以下位置執行直接升級：

* AEM6.3FormsJEE
* AEM6.4FormsJEE
* AEM6.5.x.xFormsJEE

您還可以從

* LiveCycleES2
* LiveCycleES3
* LiveCycleES4 SP1
* AEM6.0FormsJEE
* AEM6.1FormsJEE
* AEM6.2FormsJEE

AEM6.5.12.0FormsJEE提供兩種類型的安裝程式： [完整安裝程式](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 和 [修補程式安裝程式](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)。

**完整安裝程式**:您可以使用完整安裝程式設定新的AEM Forms實例或從JEE上的AEM6.3Forms、AEMJEE上的6.4執行升級，以及從JEE上的AEM6.5.x.xForms升級到JEE上的AEM6.5.12.0Forms升級。

**修補程式安裝程式**:修補程式安裝程式是針對已使用AEM6.5.x.x版本的客戶。 您可以使用修補程式安裝程式升級到最新版本的AEM Forms。

下圖描述了使用完整安裝程式和修補程式安裝程式的感測器。

![完整安裝程式和修補程式安裝程式](/help/forms/using/assets/full-and-patch-installer.png)

<!--
[Work in Progress]

Migration involves moving only assets (PDF, XDP, images, adaptive forms, correspondence management assets) from one server to another - processes (LCA), settings, configurations, and a few other pieces of metadata are not migrated. Perform the following steps to migrate to AEM 6.3 Forms:

1. Set up a fresh environment of [AEM 6.3 Forms](https://adobe.com/go/learn_aemforms_documentation_63).
1. Move XDP or other compatible assets to the freshly set instance. For detailed instructions, see [Importing and exporting assets to AEM Forms](../../forms/using/import-export-forms-templates.md). [
   ](../../forms/using/import-export-forms-templates.md)
1. Build the required services, if any.

   For example, if you are using AEM Forms on JEE Document Services, changes are required in the code to use document services available in AEM Forms on OSGi.

1. Perform post-installation activities:

    * **Run Migration Utility**

      The migration utility makes the adaptive forms and correspondence management assets of earlier versions compatible with AEM 6.3 forms. You can download the utility from AEM Software Distribution. For step-by-step information to configure and use the migration utility, see [migration utility](../../forms/using/migration-utility.md) documentation.

    * **Reconfigure Adobe Sign**

      If you had Adobe Sign configured in the previous version of AEM Forms, then reconfigure Adobe Sign from AEM Cloud services. For more details, see [Integrate Adobe Sign with AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

      Moreover, AEM 6.3 Forms release has introduced many new Adobe Sign features. For step-by-step information to use Adobe Sign, see [Using Adobe Sign in an adaptive form](../../forms/using/working-with-adobe-sign.md).

    * **Reconfigure analytics and reports**

      In AEM 6.3 Forms, traffic variable for source and success event for impression are not available. So, when you upgrade to AEM 6.3 Forms, AEM Forms stops sending data to Adobe Analytics server and analytics reports for adaptive forms are not available. Moreover, AEM 6.3 Forms introduces traffic variable for the version of form analytics and success event for the amount of time spent on a field. So, reconfigure analytics and reports for your AEM Forms environment. For detailed steps, see [Configuring analytics and reports](../../forms/using/configure-analytics-forms-documents.md).

      Methods to calculate average fill time for forms and average read time for have changed. So, when you upgrade to AEM 6.3 forms, older data (data from previous AEM Forms release) for these metrics is available only in Adobe Analytics. It is not visible in AEM Forms analytics reports. For these metrics, AEM Forms analytics reports display data which is captured after performing the upgrade.
      
      -->
