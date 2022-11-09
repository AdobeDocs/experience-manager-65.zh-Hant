---
title: 資料保護與資料隱私權法規 — Adobe Experience Manager整備
seo-title: Adobe Experience Manager Readiness for Data Protection and Data Privacy Regulations; such as GDPR, CCPA, etc
description: 了解Adobe Experience Manager對各種資料保護和資料隱私權法規的支援；包括歐盟一般資料保護規範(GDPR)、加州消費者隱私法，以及實作新AEM專案時如何遵循。
seo-description: Learn about Adobe Experience Manager support for the various Data Protection and Data Privacy Regulations; including the EU General Data Protection Regulation (GDPR), the California Consumer Privacy Act and how to comply when implementing a new AEM project.
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: AEM Docs
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
exl-id: 46c1ca14-78f6-4b33-9fdf-1b90a9875f66
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 1%

---

# Adobe Experience Manager對資料保護與資料隱私權法規的整備 {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本檔案的內容不構成法律建議，且用意並非取代法律建議。
>
>如需資料保護與資料隱私權法規的相關建議，請諮詢貴公司的法律部門。

>[!NOTE]
>
>如需有關Adobe對隱私權問題之回應，以及這對您身為Adobe客戶所代表之意義的詳細資訊，請參閱 [Adobe的隱私中心](https://www.adobe.com/privacy.html).

Adobe提供檔案和程式（若有API可用），供客戶隱私權管理員或AEM管理員處理資料保護和資料隱私權請求，並協助客戶遵守這些法規。 記錄的程式可讓客戶手動執行法規要求，或透過外部入口網站或服務呼叫API（若有）。

>[!CAUTION]
>
>此處記錄的詳細資訊僅限於Adobe Experience Manager。
>
>其他Adobe隨選服務的資料，連同任何相關的隱私權要求，都需要對該服務採取動作。
>
>如需詳細資訊，請參閱 [Adobe的隱私中心](https://www.adobe.com/privacy.html).

## 簡介 {#introduction}

Adobe Experience Manager的例項以及在其上執行的應用程式，由我們的客戶擁有和運作。

因此，GDPR、CCPA等資料保護法規在很大程度上是客戶的責任。

作為非常簡短的介紹，資料隱私和保護法規包括了新規則，這些規則將遵循：

* 業務實體(CCPA)和/或資料控管單位(GDPR)

* 服務提供者(CCPA)及/或資料處理者(GDPR)

這些條例的主要規定是：

1. 擴展個人資料的定義，納入所有唯一ID;與可直接或間接識別的資料相同。

2. 加強同意要求。

3. 增加對刪除權限（資料擦除）的關注。

4. 選擇退出資料銷售。

若為Adobe Experience Manager:

* 執行個體和在其上執行的應用程式由客戶擁有和操作。

   * 這意味著客戶管理法規角色，包括業務實體和服務提供商、資料控制方和資料處理方等。

   * 如下圖所示，Adobe Experience Platform Privacy Service不屬於AEM的工作流程。

* AEM包含客戶隱私權管理員和/或AEM管理員執行隱私權法規要求的檔案和程式；手動或透過API（若有）。

* 未新增任何服務或UI。

   * 而是會記錄程式和API，以供處理隱私權法規要求的客戶UI/入口網站使用。

* AEM將不包含任何現成可用的工具，以支援隱私權要求工作流程。

   * Adobe將提供客戶隱私權管理員和/或AEM管理員的檔案和程式，讓他們能手動執行與隱私權法規相關的要求。

Adobe提供處理Adobe Experience Manager存取、刪除和選擇退出相關隱私權要求的程式。 某些情況下，客戶可從開發的入口網站或指令碼呼叫可用的API，以協助實現自動化。

下圖說明隱私權要求工作流程看起來的樣子(使用Adobe Experience Manager 6.5圖示):

![資料保護與隱私](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager與法規整備 {#aem-and-regulatory-readiness}

如需AEM產品區域的規範檔案，請參閱以下各節。

## AEM Foundation {#aem-foundation}

請參閱 [處理AEM Foundation的資料保護和隱私權要求](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

## AEM選擇匯總使用情況統計資訊收集 {#aem-opting-into-aggregate-usage-statistics-collection}

請參閱 [匯總使用情況統計資訊收集](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

## AEM Sites {#aem-sites}

請參閱 [AEM Sites — 資料保護與隱私權整備。](/help/sites-administering/gdpr-compliance-sites.md)

## AEM Commerce {#aem-commerce}

請參閱 [AEM商務 — 資料保護與隱私權整備](/help/sites-administering/gdpr-compliance-commerce.md).

## AEM Mobile {#aem-mobile}

請參閱 [AEM Mobile — 資料保護與隱私權整備](/help/mobile/aem-mobile-gdpr-compliance.md).

## AEM與Adobe Target和Adobe Analytics整合 {#aem-integration-with-adobe-target-adobe-analytics}

這些Adobe Experience Manager整合包含資料保護與隱私權（例如GDPR或CCPA）就緒服務。 AEM中不會儲存任何來自Adobe Target或Adobe Analytics的與整合相關的個人資料。
如需詳細資訊，請參閱：

* [Adobe Target — 隱私權概觀](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/privacy.html)

* [Adobe Analytics資料隱私權工作流程](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

AEM Communities賦予資料主體資料可移植性、存取權及透過以下方式被遺忘的權利 [現成可用的API](/help/communities/user-ugc-management-service.md). 這些API可大量刪除和大量匯出使用者產生的內容，以及停用透過其可授權ID識別的使用者帳戶。 但是，通過刪除CRXDE Lite中的用戶節點，可以實現永久刪除用戶帳戶，這解決了從系統中輕鬆退出的需要。

此外，AEM Communities的「大量協調」主控台可讓有權限的成員尋找和刪除使用者的貢獻和詳細資訊，讓您的設計能提供隱私權。 「成員管理」控制台允許限制到禁止貢獻者的程度。 此外，它授權資料主體刪除由它們編寫的稿件。

## AEM Forms {#aem-forms}

AEM Forms包含擷取、處理和儲存資料以協調業務流程和完成數位交易的元件和工作流程。 不同的元件會使用不同的資料存放區，並可與自訂資料存放區整合。 下列檔案說明存取和處理使用者資料的程式和准則，以支援元件的資料保護和隱私權（例如GDPR或CCPA）工作流程。

* [表單入口網站](/help/forms/using/forms-portal-handling-user-data.md)
* [通信管理](/help/forms/using/correspondence-management-handling-user-data.md)
* [與Adobe Sign整合](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [Forms OSGi工作流程](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Forms JEE工作流程](/help/forms/using/forms-workflow-jee-handling-user-data.md) (僅限AEM Forms JEE)
* [檔案安全性](/help/forms/using/document-security-handling-user-data.md) (僅限AEM Forms JEE)
* [使用者管理](/help/forms/using/user-management-handling-user-data.md) (僅限AEM Forms JEE)
