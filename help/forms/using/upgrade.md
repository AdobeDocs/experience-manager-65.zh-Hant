---
title: 升級至 AEM 6.5 Forms
seo-title: 升級至 AEM 6.5 Forms
description: 您可以執行從6.3Forms和6.4AEMForms直AEM接升級到AEM6.5Forms。
seo-description: 您可以執行從6.3Forms和6.4AEMForms直AEM接升級到AEM6.5Forms。
uuid: 7a38cd72-2d01-4af7-b6a3-00dc34c4f02b
content-type: reference
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f89921ef-c638-4a07-88d5-3dd8614c5166
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 5%

---


# 升級至 AEM 6.5 Forms{#upgrade-to-aem-forms}

AEM6.5Forms包含數種新功能和增強功能，可簡化建立、管理和使用者體驗的表單和通訊。 要瞭解Forms6.5版的所有新功能和增AEM強功能，請參閱[新功能摘要文檔](../../forms/using/whats-new.md)。

您可以升級您現有的LiveCycle或AEM Forms安裝，以取得Forms6.5版中提供的新功能和增強功能，AEM同時保留現有資料、流程和資產的完整性。 升級時，也會保留中繼資料和程式狀態。 您可以選擇升級途徑，開始升級。

下圖顯示了OSGi上AEM Forms的可用升級路徑：

![](do-not-localize/osgi-upgrade-path.png)

您可以從以下位置執行直接升級：

* AEM6.3FormsOSGi
* AEM6.4FormsOSGi

您也可以從

* AEM6.0FormsOSGi
* AEM6.1FormsOSGi
* AEM6.2FormsOSGi

下圖顯示了JEE上AEM Forms的可用升級路徑：

![](do-not-localize/jee-upgrade-6-5.png)

您可以從以下位置執行直接升級：

* AEM6.3Forms關於JEE
* AEM6.4Forms關於JEE

您也可以從

* LiveCycleES2
* LiveCycleES3
* LiveCycleES4 SP1
* AEM6.0FormsJEE
* AEM6.1Forms關於JEE
* AEM6.2Forms關於JEE

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
