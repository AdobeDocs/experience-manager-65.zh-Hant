---
title: 在JEE升級至AEM 6.5 Forms
description: 您可以從AEM 6.1 Forms、AEM 6.2 Forms和LiveCycleES4 SP1直接升級至AEM 6.3 Forms。
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
role: Admin
exl-id: 722e75a0-bcb3-465e-bb74-ea94a3b99fd3
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 1%

---

# 在JEE升級至AEM 6.5 Forms {#upgrade-to-aem-forms-jee}

AEM 6.5.12.0 Forms on JEE提供兩種類型的安裝程式：完整安裝程式和修補程式安裝程式。

**完整安裝程式**:您可以使用 [AEM 6.5.12.0（JEE完整安裝程式）](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 若要設定最新的AEM Forms執行個體，或從JEE版的AEM 6.3 Forms、JEE版的AEM 6.4以及從JEE版的AEM 6.5.x.x Forms現成升級為JEE版的AEM 6.5.12.0 Forms 。

**修補程式安裝程式**: [AEM 6.5.12.0（JEE修補程式安裝程式）](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 適用於已使用AEM 6.5.x.x版的客戶。 您可以使用修補程式安裝程式來升級至最新版本的AEM Forms。

下表描述了使用完整安裝程式和修補程式安裝程式的參數。

![](assets/full-and-patch-installer.png)

請執行下列程式，使用完整安裝程式將JEE上的現有AEM 6.3 Forms或JEE上的AEM 6.4 Forms升級至JEE上的AEM 6.5.12.0 Forms:

1. 從下載AEM 6.5 Forms on JEE安裝程式 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). 您需要有效的維護和支援合同才能使用安裝程式。
1. 請參閱 [升級檢查清單和規劃](https://www.adobe.com/go/learn_aemforms_upgrade_checklist_65) 了解要執行的檢查，以確保成功升級。
1. 請參閱 [準備升級至AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareupgrade_65) 學習並執行各項任務，以確保在最短的伺服器停機時間內正確運行升級。
1. 根據您現有的環境和應用程式伺服器，選擇以下文檔之一併按照說明操作。

   * [從AEM 6.3或AEM 6.4 Forms升級至AEM 6.5 Forms for JBoss](https://www.adobe.com/go/learn_aemforms_upgradeJBoss_65)
   * [從AEM 6.3或AEM 6.4 Forms升級至AEM 6.5 Forms for WebSphere](https://www.adobe.com/go/learn_aemforms_upgradeWebSphere_65)
   * [從AEM 6.3或AEM 6.4 Forms升級至AEM 6.5 Forms，以完成JBoss整套功能](https://www.adobe.com/go/learn_aemforms_upgradeTurnkey_65)

無法從LiveCycleES2、LiveCycleES3、AEM 6.0 Forms、AEM 6.1 Forms、AEM 6.2 Forms直接升級至AEM 6.5 Forms。 您可以執行一或多個版本的LiveCycle或AEM Forms的中繼升級，然後升級至AEM 6.5 Forms。 如需中間版本清單及對應的升級指示，請參閱 [選擇升級路徑](upgrade.md).
