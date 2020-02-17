---
title: 資料保護與資料隱私權法規- Adobe Experience Manager就緒性
seo-title: Adobe Experience Manager資料保護與資料隱私權法規的準備；例如GDPR、CCPA等
description: '瞭解Adobe Experience manager對各種資料保護與資料隱私權法規的支援；包括歐盟通用資料保護規則(GDPR)、加州消費者隱私法，以及實作新AEM專案時如何遵守。 '
seo-description: '瞭解Adobe Experience manager對各種資料保護與資料隱私權法規的支援；包括歐盟通用資料保護規則(GDPR)、加州消費者隱私法，以及實作新AEM專案時如何遵守。 '
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: aheimoz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: grdp
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
translation-type: tm+mt
source-git-commit: 9b16c8ae2ee28c60f35f9e0f990d79173463c33b

---


# Adobe Experience Manager資料保護與資料隱私法規的準備 {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本檔案內容不構成法律咨詢，不代表法律咨詢。
>
>請洽詢貴公司的法律部門，以取得有關資料保護與資料隱私權法規的建議。

>[!NOTE]
>
>如需Adobe對隱私權問題之回應，以及這對您身為Adobe客戶意味著什麼的詳細資訊，請參 [閱Adobe的隱私權中心](https://www.adobe.com/privacy.html)。

Adobe提供檔案和程式（當有API時），讓客戶隱私權管理員或AEM管理員處理資料保護和資料隱私權要求，並協助客戶遵守這些規定。 說明的程式可讓客戶手動或從外部入口網站或服務呼叫API（若有的話），以執行法規要求。

>[!CAUTION]
>
>此處說明的詳細資訊僅限Adobe Experience Manager。
>
>來自其他Adobe隨選服務的資料，連同任何相關的隱私權要求，都需要對該服務採取行動。
>
>如需詳細資訊， [請參閱Adobe的隱私權中心](https://www.adobe.com/privacy.html)。

## 簡介 {#introduction}

Adobe Experience manager的執行個體，以及在其上執行的應用程式，都歸我們的客戶所有和營運。

因此， GDPR、CCPA等資料保護法規在很大程度上是客戶的責任。

作為簡短的介紹，資料隱私和保護法規包括了新規則，應遵循新規則，其角色包括：

* 業務實體(CCPA)和／或資料控制器(GDPR)

* 服務提供商(CCPA)和／或資料處理器(GDPR)

這些條例的主要規定是：

1. 將個人資料的定義擴充為包含所有唯一ID;直接和間接可識別的資料。

2. 已強化同意要求。

3. 增加對刪除權限（資料擦除）的關注。

4. 選擇退出資料銷售。

若是Adobe Experience Manager:

* 客戶擁有並操作執行個體和在其上執行的應用程式。

   * 這有效地意味著客戶管理法規角色，包括業務實體和服務提供商、資料控制器和資料處理器等。

   * Adobe Experience Platform Privacy service不屬於AEM的工作流程，如下圖所示。

* AEM包含客戶隱私權管理員和／或AEM管理員執行隱私權法規要求的檔案和程式；手動或透過API（若有）。

* 未新增任何服務或UI。

   * 相反，程式和API會記錄在案，以供處理隱私權法規要求的客戶UI/入口網站使用。

* AEM將不包含任何現成可用的工具，以支援隱私權要求工作流程。

   * Adobe將提供客戶的隱私權管理員和／或AEM管理員的檔案和程式，讓他們可以手動執行與隱私權規定相關的要求。

Adobe提供處理與Adobe Experience Manager的存取、刪除和選擇退出相關隱私權要求的程式。 在某些情況下，有些API可從客戶開發的入口網站或指令碼中呼叫，以協助自動化。

下圖說明隱私權要求工作流程的外觀（使用Adobe Experience Manager 6.5說明）:

![資料保護與隱私權](assets/data-protection-and-privacy-01.png)

## Adobe Experience manager與法規準備 {#aem-and-regulatory-readiness}

如需AEM產品區域的法規檔案，請參閱以下章節。

## AEM Foundation {#aem-foundation}

請參 [閱「處理AEM Foundation的資料保護與隱私權要求」](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)。

## AEM Opting Into Aggregate Usage Statistics Collection {#aem-opting-into-aggregate-usage-statistics-collection}

請參 [閱匯總使用統計資訊收集](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)。

## AEM Sites {#aem-sites}

請參 [閱「AEM網站——資料保護與隱私權準備」。](/help/sites-administering/gdpr-compliance-sites.md)

## AEM Commerce {#aem-commerce}

請參 [閱「AEM商務——資料保護與隱私權準備](/help/sites-administering/gdpr-compliance-commerce.md)」。

## AEM Mobile {#aem-mobile}

請參 [閱AEM Mobile —— 資料保護與隱私權準備](/help/mobile/aem-mobile-gdpr-compliance.md)。

## AEM與Adobe Target和Adobe Analytics整合 {#aem-integration-with-adobe-target-adobe-analytics}

這些Adobe Experience manager整合包含資料保護與隱私權（例如GDPR或CCPA）就緒服務。 AEM中不會儲存Adobe target或Adobe Analytics中與整合相關的個人資料。
如需詳細資訊，請參閱：

* [Adobe Target —— 隱私權概觀](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/privacy.html)

* [Adobe Analytics資料隱私權工作流程](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

AEM Communities賦予資料主體資料可攜性、存取權和透過現成可用的API [被遺忘權](/help/communities/user-ugc-management-service.md)。 這些API可大量刪除和大量匯出使用者產生的內容，並停用透過其可授權ID識別的使用者帳戶。 但是，通過刪除CRXDE Lite中的用戶節點，可以實現永久刪除用戶帳戶，這滿足了從系統中輕鬆退出的需要。

此外，AEM Communities由於其Bulk Moderation主控台（可讓特權會員尋找和刪除使用者的貢獻和詳細資料），所以設計上提供隱私權。 「會員管理控制台」可限制到禁止參與者的程度。 此外，它授權資料主體刪除由其撰寫的稿件。

## AEM Forms {#aem-forms}

AEM Forms包含擷取、處理和儲存資料的元件和工作流程，以協調商業程式和完成數位交易。 不同的元件使用不同的資料儲存區，並可與自訂資料儲存區整合。 以下檔案說明存取和處理使用者資料以支援元件資料保護和隱私權（例如GDPR或CCPA）工作流程的程式和准則。

* [表單入口網站](/help/forms/using/forms-portal-handling-user-data.md)
* [信件管理](/help/forms/using/correspondence-management-handling-user-data.md)
* [與Adobe Sign整合](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [OSGi上的表單導向工作流程](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Forms JEE工作流程](/help/forms/using/forms-workflow-jee-handling-user-data.md) （僅限AEM Forms JEE）
* [Document Security](/help/forms/using/document-security-handling-user-data.md) （僅限AEM Forms JEE）
* [使用者管理](/help/forms/using/user-management-handling-user-data.md) （僅限AEM Forms JEE）
