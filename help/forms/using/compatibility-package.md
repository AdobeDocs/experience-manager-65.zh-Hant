---
title: 相容性套件
description: 在AEM Forms 6.5上安裝相容性套件，可讓您使用AEM Forms 6.4及舊版本的通訊管理資產，以及已棄用的調適型表單範本和頁面
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin,User
exl-id: bb16017c-a1bf-40d8-a78d-827c05b7ee2e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 1%

---

# 相容性套件{#compatibility-package}

## 概觀 {#overview}

在AEM Forms 6.5中建立客戶通訊時，互動式通訊是預設且建議使用的方法。若要繼續使用AEM Forms 6.5中的字母，您必須安裝最新的[AEMFD相容性套件](https://helpx.adobe.com/tw/aem-forms/kb/aem-forms-releases.html)。

AEMFD相容性套件也可讓您[在AEM Forms 6.5上使用AEM Forms 6.4、6.3和6.2的下列資產：](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* 檔案片段
* 字母
* 資料字典
* 最適化表單已棄用的範本和頁面

如需詳細資訊，請參閱[藉由安裝相容性套件](../../forms/using/compatibility-package.md#assetsmadecompatible)，讓Assets與AEM Forms 6.5相容。

## 在AEM Forms 6.5中新增對AEM Forms 6.4、6.3和6.2資產的支援 {#add-support-for-aem-forms-and-assets-in-aem-forms}

執行升級後，請執行以下操作以安裝AEMFD相容性套件，並讓您的資產相容於6.5：

確定您已預先安裝[AEM相容性套件](https://helpx.adobe.com/tw/aem-forms/kb/aem-forms-releases.html)。

1. 安裝最新的6.5 [相容性套件](https://helpx.adobe.com/tw/aem-forms/kb/aem-forms-releases.html)。

   如需上傳和安裝套件的詳細資訊，請參閱[如何使用套件](/help/sites-administering/package-manager.md)。

1. 在記錄穩定後，請重新啟動伺服器。
1. 使用移轉公用程式，讓您的資產相容於6.5。

   >[!NOTE]
   >
   > 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式）可能會導致AEM開發環境不一致。

   如需詳細資訊，請參閱[移轉公用程式](../../forms/using/migration-utility.md)。

## 透過安裝相容性套件，Assets可與AEM Forms 6.5相容 {#assetsmadecompatible}

透過安裝相容性套件，您可以使下列資產和範本與AEM Forms 6.5相容：

* AEM 6.4及舊版的Correspondence Management Assets：

   * [字母](../../forms/using/create-letter.md)
   * [資料字典](/help/forms/using/data-dictionary.md)
   * 文件片段

* 最適化表單已棄用的範本：

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnrollmentTemplate
   * /libs/fd/af/templates/simpleEnrollmentTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/tabbedEnrollmentTemplate
   * /libs/fd/af/templates/tabbedEnrollmentTemplate2
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate2

* 調適型表單已棄用頁面：

   * /libs/fd/af/components/page/survey
   * /libs/fd/af/components/page/tabbedenrollment
   * /libs/fd/afaddon/components/page/advancedenrollment
