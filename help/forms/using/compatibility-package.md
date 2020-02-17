---
title: 相容性包
seo-title: 相容性包
description: 在AEM Forms 6.5上安裝Compatibility套件可讓您使用AEM Forms 6.4及舊版的Correponsement Management資產，以及淘汰的調適性表單範本和頁面
seo-description: 在AEM Forms 6.4上安裝Compatibility套件可讓您使用AEM Forms 6.4中的Correponsement Management資產，以及不建議使用的最適化表單範本和頁面
uuid: b49633d6-2cb3-422c-a314-25f3b8a37b7f
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 73e8ccc6-f857-493e-b6e3-878f93e2a356
docset: aem65
translation-type: tm+mt
source-git-commit: dca52c05c413fc96bf7fab012a3be52f6769c2e0

---


# 相容性包{#compatibility-package}

## 概覽 {#overview}

在AEM Forms 6.5中建立客戶通訊的預設和建議方式是互動式通訊。若要繼續在AEM Forms 6.5中使用字母，您必須安裝最新的 [AEMFD相容性套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)。

AEMFD相容性套件也可讓您 [在AEM Forms 6.5上使用AEM Forms 6.4、6.3和6.2的下列資產：](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* 檔案片段
* 字母
* 資料字典
* 不再支援的最適化表單範本和頁面

如需詳細資訊，請 [參閱「透過安裝相容性套件，讓資產與AEM Forms 6.5相容」](../../forms/using/compatibility-package.md#assetsmadecompatible)。

## 在AEM Forms 6.5中新增對AEM Forms 6.4、6.3和6.2資產的支援 {#add-support-for-aem-forms-and-assets-in-aem-forms}

執行升級後，請執行下列動作以安裝AEMFD相容性套件，並讓您的資產與6.5相容：

請確定您已預 [先安裝AEM Compatibility套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 。

1. 安裝最新的6.5兼 [容性套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)。

   有關上傳和安裝軟體包的詳細資訊，請參 [閱How to work with packages](/help/sites-administering/package-manager.md)。

1. 穩定日誌後，重新啟動伺服器。
1. 使用移轉公用程式，讓資產與6.5相容。

   如需詳細資訊，請參閱移 [轉公用程式](../../forms/using/migration-utility.md)。

## 透過安裝Compatibility套件，讓資產與AEM Forms 6.5相容 {#assetsmadecompatible}

透過安裝「相容性」套件，您可讓下列資產和範本與AEM Forms 6.5相容：

* AEM 6.4及舊版的Commernessing Management Assets:

   * [字母](../../forms/using/create-letter.md)
   * [資料字典](/help/forms/using/data-dictionary.md)
   * 文件片段

* 不建議使用的最適化表單範本：

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnrollmentTemplate
   * /libs/fd/af/templates/simpleEnrollmentTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/tabbedEnrollmentTemplate
   * /libs/fd/af/templates/tabbedEnrollmentTemplate2
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate2

* 最適化表單已過時的頁面：

   * /libs/fd/af/components/page/survey
   * /libs/fd/af/components/page/tabbedenrollment
   * /libs/fd/afaddon/components/page/advancedenrollment

