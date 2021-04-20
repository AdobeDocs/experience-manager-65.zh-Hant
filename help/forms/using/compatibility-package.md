---
title: 相容性包
seo-title: 相容性包
description: 在AEM Forms6.5上安裝相容性軟體包可讓您使用AEM Forms6.4和更早版本的通信管理資產，以及過時的自適應表單模板和頁面
seo-description: 在AEM Forms6.4上安裝相容性軟體包可讓您使用AEM Forms6.4的通信管理資產和不建議使用的自適應表單模板和頁面
uuid: b49633d6-2cb3-422c-a314-25f3b8a37b7f
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 73e8ccc6-f857-493e-b6e3-878f93e2a356
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 2%

---


# 相容性包{#compatibility-package}

## 概覽 {#overview}

在AEM Forms6.5中，互動式通訊是建立客戶通訊的預設和建議方式。要繼續使用AEM Forms6.5中的字母，您需要安裝最新的[AEMFD相容性軟體包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)。

AEMFD相容性軟體包還允許您[使用AEM Forms6.5上的AEM Forms6.4、6.3和6.2的以下資產：](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* 檔案片段
* 字母
* 資料字典
* 不再支援的最適化表單範本和頁面

如需詳細資訊，請參閱[透過安裝Compatibility套件使資產與AEM Forms6.5相容。](../../forms/using/compatibility-package.md#assetsmadecompatible)

## 在AEM Forms6.5 {#add-support-for-aem-forms-and-assets-in-aem-forms}中增加對AEM Forms6.4、6.3和6.2資產的支援

執行升級後，請執行下列動作以安裝AEMFD相容性套件，並讓您的資產與6.5相容：

確保已預裝[AEM Compatibility package](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)。

1. 安裝最新的6.5 [相容性軟體包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)。

   有關上載和安裝軟體包的詳細資訊，請參閱[如何使用軟體包](/help/sites-administering/package-manager.md)。

1. 穩定日誌後，重新啟動伺服器。
1. 使用移轉公用程式，讓資產與6.5相容。

   有關詳細資訊，請參見[遷移實用程式](../../forms/using/migration-utility.md)。

## 通過安裝Compatibility軟體包{#assetsmadecompatible}與AEM Forms6.5相容的資產

通過安裝Compatibility軟體包，您可以使以下資產和模板與AEM Forms6.5相容：

* 6.4版及更AEM舊版本的Commernance Management Assets:

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

