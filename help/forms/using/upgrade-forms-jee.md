---
title: 在JEE上升級至AEM 6.5 Forms
description: 您可以從AEM 6.1 Forms、AEM 6.2 Forms和LiveCycleES4 SP1直接升級至AEM 6.3 Forms。
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
role: Admin
exl-id: 722e75a0-bcb3-465e-bb74-ea94a3b99fd3
source-git-commit: 34be3b4695679a9b5e8001d28f05ed804f929e61
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 1%

---

# 在JEE上升級至AEM 6.5 Forms {#upgrade-to-aem-forms-jee}

JEE上的AEM 6.5.12.0 Forms提供兩種型別的安裝程式：完整安裝程式和修補程式安裝程式。

**完整安裝程式**：您可以使用 [jee上的AEM 6.5.12.0完整安裝程式](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 以設定全新AEM Forms執行個體，或從JEE上的AEM 6.5.x.x Forms升級至JEE上的AEM 6.5.12.0 Forms。

**修補程式安裝程式**： [JEE上的AEM 6.5.12.0修補程式安裝程式](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 適用於已使用AEM 6.5.x.x版本的客戶。 您可以使用修補程式安裝程式來升級至最新版AEM Forms。

<!--
The following table depicts senarios for using full and patch installer.

![Full and Patch installer scenario](assets/full-and-patch-installer.png) -->

執行以下程式，使用完整安裝程式將JEE上的現有AEM Forms 6.5.x.x升級為JEE上的AEM 6.5.12.0 Forms：

1. 下載AEM 6.5 Forms on JEE安裝程式，網址為 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). 您需要有效的維護與支援合約才能使用安裝程式。
1. 另請參閱 [升級檢查清單與規劃](https://www.adobe.com/go/learn_aemforms_upgrade_checklist_65) 瞭解為確保成功升級而執行的檢查。
1. 另請參閱 [準備升級至AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareupgrade_65) 瞭解並執行確保升級正確執行的工作，並將伺服器停機時間降至最低。
1. 根據您現有的環境和應用程式伺服器，選擇下列其中一份檔案並依照指示操作。

   * [從AEM 6.3或AEM 6.4 Forms升級至適用於JBoss的AEM 6.5 Forms](https://www.adobe.com/go/learn_aemforms_upgradeJBoss_65)
   * [從AEM 6.3或AEM 6.4 Forms升級至適用於WebSphere的AEM 6.5 Forms](https://www.adobe.com/go/learn_aemforms_upgradeWebSphere_65)
   * [從AEM 6.3或AEM 6.4 Forms升級至適用於JBoss Turnkey的AEM 6.5 Forms](https://www.adobe.com/go/learn_aemforms_upgradeTurnkey_65)

無法從LiveCycle ES2、LiveCycle ES3、AEM 6.0 Forms、AEM 6.1 Forms、AEM 6.2 Forms直接升級至AEM 6.5 Forms。 您可以對一或多個LiveCycle或AEM Forms版本執行中繼升級，然後升級至AEM 6.5 Forms。 如需中間版本和對應升級指示的清單，請參閱 [選擇升級路徑](upgrade.md).
