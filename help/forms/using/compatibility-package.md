---
title: 相容性包
seo-title: Compatibility Package
description: 在AEM Forms6.5上安裝相容性軟體包允許您使用AEM Forms6.4及更早版本的通信管理資產以及過時的自適應表單模板和頁面
seo-description: Installing the Compatibility package on AEM Forms 6.4 allows you to use the Correspondence Management assets from AEM Forms 6.4 and deprecated adaptive forms templates and pages
uuid: b49633d6-2cb3-422c-a314-25f3b8a37b7f
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 73e8ccc6-f857-493e-b6e3-878f93e2a356
docset: aem65
role: Admin
exl-id: bb16017c-a1bf-40d8-a78d-827c05b7ee2e
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 2%

---

# 相容性包{#compatibility-package}

## 概觀 {#overview}

在AEM Forms6.5建立客戶溝通是預設和建議的方式。要繼續在AEM Forms6.5中使用字母，您需要安裝 [AEMFD相容性包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)。

AEMFD相容性包還允許您 [使用AEM Forms6.4、6.3和6.2中的下列資產，在AEM Forms6.5上：](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* 文檔片段
* 字母
* 資料字典
* 不建議使用的自適應表單模板和頁面

有關詳細資訊，請參見 [通過安裝相容性軟體包與AEM Forms6.5相容的資產](../../forms/using/compatibility-package.md#assetsmadecompatible)。

## 增加對AEM Forms6.4、6.3和6.2AEM Forms6.5資產的支援 {#add-support-for-aem-forms-and-assets-in-aem-forms}

執行升級後，請執行以下操作以安裝AEMFD相容性包，並使您的資產與6.5相容：

確保您 [相容AEM性包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 已預裝。

1. 安裝最新的6.5 [相容性包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)。

   有關上載和安裝軟體包的詳細資訊，請參見 [如何使用包](/help/sites-administering/package-manager.md)。

1. 穩定日誌後，重新啟動伺服器。
1. 使用遷移實用程式使資產與6.5相容。

   有關詳細資訊，請參見 [遷移實用程式](../../forms/using/migration-utility.md)。

## 通過安裝相容性軟體包與AEM Forms6.5相容的資產 {#assetsmadecompatible}

通過安裝相容性軟體包，可以使以下資產和模板與AEM Forms6.5相容：

* 6.4及更AEM低版本的Tergement Management資產：

   * [字母](../../forms/using/create-letter.md)
   * [資料字典](/help/forms/using/data-dictionary.md)
   * 文件片段

* 不建議使用的自適應表單模板：

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnrollmentTemplate
   * /libs/fd/af/templates/simpleEnrollmentTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/tabbedEnrollmentTemplate
   * /libs/fd/af/templates/tabbedEnrollmentTemplate2
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate2

* 已過時的自適應表單頁面：

   * /libs/fd/af/components/page/survey
   * /libs/fd/af/components/page/tabedenrolls
   * /libs/fd/afaddon/components/page/advandentrolls
