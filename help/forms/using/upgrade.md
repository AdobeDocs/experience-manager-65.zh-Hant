---
title: 升級至 AEM 6.5 Forms
description: 您可以從AEM 6.3 Forms和AEM 6.4 Forms直接升級至AEM 6.5 Forms。
content-type: reference
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin,User
exl-id: 2fc8abec-8ba6-40b7-bbb1-4288eeea7c86
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms Upgrade
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 6%

---

# 升級至 AEM 6.5 Forms {#upgrade-to-aem-forms}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/migrate-to-forms-as-a-cloud-service.html?lang=zh-Hant) |
| AEM 6.5 | 本文章 |


AEM 6.5 Forms包含數項新功能和增強功能，可簡化表單和對應項的建立、管理和使用者體驗。 若要瞭解AEM 6.5 Forms的所有新功能和增強功能，請參閱[新功能摘要檔案](../../forms/using/whats-new.md)。

您可以升級現有的LiveCycle或AEM Forms安裝，以取得AEM 6.5 Forms中提供的新功能和增強功能，同時完整保留現有的資料、流程和資產。 升級時，也會保留處理序的中繼資料和狀態。 您可以選擇升級路徑以開始升級。

下圖顯示OSGi上AEM Forms的可用升級路徑：

![OSGi升級流程](do-not-localize/osgi-upgrade-path.png)

您可以從下列位置執行直接升級：

* OSGi上的AEM 6.3 Forms
* OSGi上的AEM 6.4 Forms

您也可以從以下位置執行多重躍點升級：

* OSGi上的AEM 6.0 Forms
* OSGi上的AEM 6.1 Forms
* OSGi上的AEM 6.2 Forms

下圖顯示AEM Forms on JEE的可用升級路徑：

![JEE升級6.5](do-not-localize/jee-upgrade-6-5.png)


您可以從下列位置執行直接升級：

* JEE上的AEM 6.3 Forms
* JEE上的AEM 6.4 Forms
* JEE上的AEM 6.5.x.x Forms

您也可以從以下位置執行多重躍點升級：

* LiveCycleES4 SP1
* JEE上的AEM 6.0 Forms
* JEE上的AEM 6.1 Forms
* JEE上的AEM 6.2 Forms

JEE上的AEM 6.5.18.0 Forms提供兩種型別的安裝程式： [完整安裝程式](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hant)和[修補安裝程式](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hant)。

**完整安裝程式**：您可以使用完整安裝程式來設定新的AEM Forms執行個體，或從JEE上的AEM 6.5.x.x Forms升級至JEE上的AEM 6.5.18.0 Forms。

**修補程式安裝程式**：修補程式安裝程式適用於已使用AEM 6.5.x.x版本的客戶。 您可以使用修補程式安裝程式來升級至最新版AEM Forms。

以下影像說明使用完整和修補程式安裝程式的情境。

![完整安裝程式和修補程式安裝程式](/help/forms/using/assets/full-and-patch-installer.png)

請參閱[AEM 6.5 Forms Service Pack安裝指示](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=zh-Hant)文章，安裝JEE環境適用的最新Service Pack。

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


