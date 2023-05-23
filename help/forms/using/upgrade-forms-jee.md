---
title: 升級至AEMJEE上的6.5Forms
description: 您可以執行從AEM6.1Forms、AEM6.2Forms和LiveCycleES4 SP1到AEM6.3Forms的直接升級。
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

# 升級至AEMJEE上的6.5Forms {#upgrade-to-aem-forms-jee}

AEM6.5.12.0FormsJEE提供兩種類型的安裝程式：完整安裝程式和修補程式安裝程式。

**完整安裝程式**:您可以使用 [AEM6.5.12.0 on JEE完整安裝程式](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 設定新的AEM Forms實例或從JEE上的AEM6.3Forms、AEMJEE上的6.4升級，以及從JEE上的AEM6.5.x.xForms升級到JEE上的AEM6.5.12.0Forms升級。

**修補程式安裝程式**: [AEM 6.5.12.0上的JEE修補程式安裝程式](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 適用於已使AEM用6.5.x.x版本的客戶。 您可以使用修補程式安裝程式升級到最新版本的AEM Forms。

下表描述了使用完整安裝程式和修補程式安裝程式的感測器。

![](assets/full-and-patch-installer.png)

執行以下步驟，使用完整安裝程式將JEE上的AEM現有6.3Forms或JEE上的6.4Forms升級到JEE上的AEM6.5.12.0Forms:

1. 從AEM下載JEE安裝程式上的6.5Forms [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)。 您需要有效的維護和支援合同才能使用安裝程式。
1. 請參閱 [升級核對表和規劃](https://www.adobe.com/go/learn_aemforms_upgrade_checklist_65) 瞭解要執行的檢查以確保成功升級。
1. 請參閱 [準備升級到AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareupgrade_65) 瞭解並執行確保升級在最短伺服器停機時間內正確運行的任務。
1. 根據您現有的環境和應用程式伺服器，選擇以下文檔之一併按照說明操作。

   * [將JBossAEM從6.3或AEM6.4Forms升級AEM到6.5Forms](https://www.adobe.com/go/learn_aemforms_upgradeJBoss_65)
   * [從AEM6.3或AEM6.4Forms升級到AEM6.5FormsWebSphere](https://www.adobe.com/go/learn_aemforms_upgradeWebSphere_65)
   * [從6AEM.3或6.AEM4Forms升級到AEM6.5Forms](https://www.adobe.com/go/learn_aemforms_upgradeTurnkey_65)

無法直接從LiveCycleES2、LiveCycleES3、AEM6.0Forms、AEM6.1Forms、AEM6.2Forms升級到AEM6.5。 您可以執行到LiveCycle或AEM Forms的一個或多個版本的中間升級，然後升級到AEM6.5Forms。 有關中間版本清單和相應升級說明，請參見 [選擇升級路徑](upgrade.md)。
