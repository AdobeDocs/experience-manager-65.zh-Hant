---
title: 資料保護和資料隱私權法規 — Adobe Experience Manager整備
description: 瞭解Adobe Experience Manager對各種資料保護和資料隱私權法規的支援。 其中包括歐盟一般資料保護規範(GDPR)、加州消費者隱私法，以及在實施新的AEM專案時如何遵守。
contentOwner: AEM Docs
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
docset: aem65
exl-id: 46c1ca14-78f6-4b33-9fdf-1b90a9875f66
solution: Experience Manager, Experience Manager 6.5
source-git-commit: 1751bfb32386685e3a159939113b9667b5e17f0e
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 36%

---

# Adobe Experience Manager的資料保護與資料隱私權法規整備 {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本文件的內容並不構成法律建議，其宗旨並非取代專業的法律建議。
>
>如需有關資料保護和資料隱私權法規的建議，請諮詢貴公司的法律部門。

>[!NOTE]
>
>如需關於 Adobe 對隱私權問題的回應以及這對於您身為 Adobe 客戶所代表之意義的詳細資訊，請參閱 [Adobe 隱私權中心](https://www.adobe.com/tw/privacy.html)。

Adobe正為客戶隱私權管理員或AEM管理員提供檔案和程式（可用時透過API）以處理資料保護和資料隱私權請求。 它可以協助您符合這些法規。 記錄的程式可讓客戶從外部入口網站或服務，以手動方式或透過呼叫API （可用時）來執行法規請求。

>[!CAUTION]
>
>此處記錄的詳細資料僅限於Adobe Experience Manager。
>
>來自其他 Adobe 隨選服務的資料以及任何相關的隱私權請求，會要求對該服務採取動作。
>
>如需詳細資訊，請參閱 [Adobe 的隱私權中心](https://www.adobe.com/tw/privacy.html)。

## 簡介 {#introduction}

Adobe Experience Manager的執行個體以及在其上執行的應用程式是由Adobe客戶所擁有和營運。

因此，GDPR、CCPA 等資料保護法規主要是客戶的責任。

簡單介紹，資料隱私權和保護法規包括以下角色要遵循的新規則：

* 商業實體 (CCPA) 和/或資料控制者 (GDPR)

* 服務提供者 (CCPA) 和/或資料處理者 (GDPR)

這些法規的主要規定包括：

1. 擴大個人資料的定義以包括所有唯一 ID；如直接和間接可識別的資料。

2. 加強同意要求。

3. 更加關注刪除權 (資料清除)。

4. 選擇退出資料銷售。

若為Adobe Experience Manager：

* 執行個體，以及在其上執行的應用程式由客戶所擁有和營運。

   * 客戶管理法規角色，包括商業實體和服務提供者、資料控制者和資料處理者等。

   * Adobe Experience Platform Privacy Service 不是 AEM 工作流程的一部分，如下圖所示。

* AEM 包含相關文件和程序，供客戶隱私權管理員和/或 AEM 管理員執行隱私權法規請求；無論是以手動方式或透過 API (可用時)。

* 沒有新增新的服務或 UI。

   * 反而是記錄各個程序和 API，以供處理隱私權監管請求的客戶 UI/入口網站使用。

* AEM 不包括任何現成工具來支援隱私權請求工作流程。

   * Adobe向客戶隱私權管理員和AEM管理員提供檔案和程式，讓他們手動執行與隱私權法規相關的請求。

Adobe提供各項程式，用於處理與Adobe Experience Manager的存取、刪除和選擇退出相關的隱私權請求。 有時候，可以從客戶開發的入口網站或指令碼中呼叫可用的API，以幫助實現自動化。

下圖說明了隱私權請求工作流程的模樣 (使用 Adobe Experience Manager 6.5 進行說明)：

![資料保護和隱私權](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager和法規整備 {#aem-and-regulatory-readiness}

如需有關AEM產品領域的監管檔案，請參閱以下各節。

## AEM Foundation {#aem-foundation}

另請參閱 [處理AEM Foundation的資料保護和隱私權請求](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

## AEM選擇加入彙總使用狀況統計資料的收集 {#aem-opting-into-aggregate-usage-statistics-collection}

另請參閱 [彙總的使用狀況統計資料集合](/help/sites-deploying/opt-in-aggregated-usage-statistics.md).

## AEM Sites {#aem-sites}

另請參閱 [AEM Sites — 資料保護和隱私權整備。](/help/sites-administering/gdpr-compliance-sites.md)

## AEM Commerce {#aem-commerce}

另請參閱 [AEM Commerce — 資料保護和隱私權整備](/help/sites-administering/gdpr-compliance-commerce.md).

## AEM Mobile {#aem-mobile}

另請參閱 [AEM Mobile — 資料保護和隱私權整備](/help/mobile/aem-mobile-gdpr-compliance.md).

## AEM與Adobe Target和Adobe Analytics的整合 {#aem-integration-with-adobe-target-adobe-analytics}

這些Adobe Experience Manager整合具有資料保護和隱私權（例如GDPR或CCPA）整備服務。 來自Adobe Target或Adobe Analytics與整合相關的個人資料不會儲存在AEM中。

如需詳細資訊，請參閱下列內容：

* [Adobe Target - 隱私權概觀](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=en)

* [Adobe Analytics 資料隱私權工作流程](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

AEM Communities賦予資料主體資料可攜性、存取許可權及被遺忘的權利 [現成可用的API](/help/communities/user-ugc-management-service.md). 這些API允許大量刪除和大量匯出使用者產生的內容，並停用透過其可授權ID識別的使用者帳戶。 不過，透過刪除CRXDE Lite中的使用者節點，即可永久刪除使用者帳戶，滿足輕鬆選擇退出系統的需求。

此外，AEM Communities的「大量調節」主控台可讓有特殊許可權的成員尋找和刪除使用者的貢獻和詳細資訊，因此在設計上提供隱私權。 「成員」管理主控台可限制在禁止投稿人的程度。 此外，它可授權資料主體刪除其所撰寫的貢獻。

## AEM Forms {#aem-forms}

AEM Forms包含可擷取、處理和儲存資料的元件和工作流程，以協調業務流程和完成數位交易。 不同的元件使用不同的資料存放區，並允許與自訂資料存放區整合。 以下檔案說明存取和處理使用者資料的程式和准則，以支援元件的資料保護和隱私權（例如GDPR或CCPA）工作流程。

* [Forms入口網站](/help/forms/using/forms-portal-handling-user-data.md)
* [通信管理](/help/forms/using/correspondence-management-handling-user-data.md)
* [與Adobe Sign整合](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [OSGi上以Forms為中心的工作流程](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [Forms JEE工作流程](/help/forms/using/forms-workflow-jee-handling-user-data.md) (僅限AEM Forms JEE)
* [Document Security](/help/forms/using/document-security-handling-user-data.md) (僅限AEM Forms JEE)
* [User Management](/help/forms/using/user-management-handling-user-data.md) (僅限AEM Forms JEE)
