---
title: 相容性套件
seo-title: 相容性套件
description: 在AEM Forms 6.5上安裝相容性套件可讓您使用AEM Forms 6.4及舊版的通信管理資產，以及過時的適用性表單範本和頁面
seo-description: 在AEM Forms 6.4上安裝相容性套件可讓您使用AEM Forms 6.4的通信管理資產以及過時的適用性表單範本和頁面
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
source-wordcount: '343'
ht-degree: 2%

---

# 相容性套件{#compatibility-package}

## 概覽 {#overview}

互動式通訊是在AEM Forms 6.5中建立客戶通訊的預設且建議的方法。若要繼續在AEM Forms 6.5中使用信函，您需要安裝最新的[AEMFD相容性套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)。

AEMFD相容性套件也可讓您[使用AEM Forms 6.5上AEM Forms 6.4、6.3和6.2的下列資產：](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* 檔案片段
* 字母
* 資料字典
* 適用性表單已棄用的範本和頁面

如需詳細資訊，請參閱安裝相容性套件](../../forms/using/compatibility-package.md#assetsmadecompatible)讓資產與AEM Forms 6.5相容。[

## 新增對AEM Forms 6.4、6.3和6.2資產在AEM Forms 6.5中的支援 {#add-support-for-aem-forms-and-assets-in-aem-forms}

執行升級後，請執行下列動作以安裝AEMFD相容性套件，並讓您的資產與6.5相容：

請確定您已預先安裝[AEM相容性套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)。

1. 安裝最新的6.5 [相容性包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)。

   有關上載和安裝包的詳細資訊，請參閱[如何使用包](/help/sites-administering/package-manager.md)。

1. 穩定日誌後，重新啟動伺服器。
1. 使用移轉公用程式，讓資產與6.5相容。

   如需詳細資訊，請參閱[migration utility](../../forms/using/migration-utility.md)。

## 安裝相容性套件，使資產與AEM Forms 6.5相容 {#assetsmadecompatible}

安裝相容性套件後，您就可以讓下列資產和範本與AEM Forms 6.5相容：

* 來自AEM 6.4及舊版的通信管理資產：

   * [字母](../../forms/using/create-letter.md)
   * [資料字典](/help/forms/using/data-dictionary.md)
   * 文件片段

* 已棄用的最適化表單範本：

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnrollmentTemplate
   * /libs/fd/af/templates/simpleEnrollmentTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/tabbedEnrollmentTemplate
   * /libs/fd/af/templates/tabbedEnrollmentTemplate2
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate2

* 已棄用的適用性表單頁面：

   * /libs/fd/af/components/page/survey
   * /libs/fd/af/components/page/tabbedenrollment
   * /libs/fd/afaddon/components/page/advandenrollment
