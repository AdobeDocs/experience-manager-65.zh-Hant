---
title: 資料保護和資料隱私法規 — Adobe Experience Manager就緒性
description: 瞭解Adobe Experience Manager對各種資料保護和資料隱私法規的支援。 它包括歐盟一般資料保護條例(GDPR)、加利福尼亞消費者隱私法以及實施新項目時如AEM何遵守。
uuid: 9b0b8101-929c-4232-8c6e-1f9b8b2e0aa2
contentOwner: AEM Docs
topic-tags: introduction, grdp
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
discoiquuid: 0bcd7ac4-3071-466d-bd11-701f35ccf5bd
docset: aem65
exl-id: 46c1ca14-78f6-4b33-9fdf-1b90a9875f66
source-git-commit: d8ae63edd71c7d27fe93d24b30fb00a29332658d
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 25%

---

# Adobe Experience Manager為資料保護和資料隱私法規做好準備 {#aem-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本文件的內容並不構成法律建議，其宗旨並非取代專業的法律建議。
>
>有關資料保護和資料隱私法規的建議，請咨詢您公司的法律部門。

>[!NOTE]
>
>有關Adobe對隱私問題的響應以及它對您作為Adobe客戶意味著什麼的詳細資訊，請參閱 [Adobe隱私中心](https://www.adobe.com/tw/privacy.html)。

Adobe提供文檔和過程（如果有API），讓客戶隱私管理員或管理員AEM處理資料保護和資料隱私請求。 它可以幫助您遵守這些法規。 所記錄的過程允許客戶手動或通過從外部門戶或服務調用API（如果可用）來運行管理法規請求。

>[!CAUTION]
>
>此處記錄的細節僅限於Adobe Experience Manager。
>
>來自其他Adobe按需服務的資料以及任何相關的隱私請求要求對該服務採取操作。
>
>有關詳細資訊，請參見 [Adobe隱私中心](https://www.adobe.com/tw/privacy.html)。

## 簡介 {#introduction}

Adobe Experience Manager的實例以及運行在它們上的應用程式由Adobe客戶擁有和操作。

因此，GDPR、CCPA 等資料保護法規主要是客戶的責任。

作為簡要介紹，資料隱私和保護法規包括了新的規則，應遵循以下角色：

* 商業實體 (CCPA) 和/或資料控制者 (GDPR)

* 服務提供者 (CCPA) 和/或資料處理者 (GDPR)

這些法規的主要規定包括：

1. 擴大個人資料的定義以包括所有唯一 ID；如直接和間接可識別的資料。

2. 加強同意要求。

3. 更加關注刪除權 (資料清除)。

4. 選擇退出資料銷售。

Adobe Experience Manager:

* 執行個體，以及在其上執行的應用程式由客戶所擁有和營運。

   * 客戶管理管理法規角色，包括業務實體和服務提供商、資料控制器和資料處理器等。

   * 如下圖所示，Adobe Experience Platform Privacy Service不AEM是工作流的一部分。

* AEM 包含相關文件和程序，供客戶隱私權管理員和/或 AEM 管理員執行隱私權法規請求；無論是以手動方式或透過 API (可用時)。

* 沒有新增新的服務或 UI。

   * 反而是記錄各個程序和 API，以供處理隱私權監管請求的客戶 UI/入口網站使用。

* 不AEM包括任何支援隱私請求工作流的現成工具。

   * Adobe為客戶的隱私管理員和管理員提供文檔和AEM過程，讓他們手動運行與隱私法規相關的請求。

Adobe正在提供處理與Adobe Experience Manager訪問、刪除和退出相關的隱私請求的程式。 有時，可從客戶開發的門戶或指令碼中調用可用的API，以幫助實現自動化。

下圖說明了隱私權請求工作流程的模樣 (使用 Adobe Experience Manager 6.5 進行說明)：

![資料保護和隱私權](assets/data-protection-and-privacy-01.png)

## Adobe Experience Manager和法規就緒性 {#aem-and-regulatory-readiness}

有關產品區域的法規文檔，請參閱以下各節AEM。

## 基AEM礎 {#aem-foundation}

請參閱 [處理Foundation的資料保護和隱私AEM請求](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)。

## 選AEM擇聚合使用統計資訊收集 {#aem-opting-into-aggregate-usage-statistics-collection}

請參閱 [聚合使用情況統計資訊收集](/help/sites-deploying/opt-in-aggregated-usage-statistics.md)。

## AEM Sites {#aem-sites}

請參閱 [AEM Sites — 資料保護和隱私準備。](/help/sites-administering/gdpr-compliance-sites.md)

## 商AEM業 {#aem-commerce}

請參閱 [商AEM務 — 資料保護和隱私準備](/help/sites-administering/gdpr-compliance-commerce.md)。

## AEM Mobile {#aem-mobile}

請參閱 [AEM Mobile — 資料保護和隱私準備](/help/mobile/aem-mobile-gdpr-compliance.md)。

## 與AEMAdobe Target和Adobe Analytics整合 {#aem-integration-with-adobe-target-adobe-analytics}

Adobe Experience Manager的這些整合與資料保護和隱私（例如GDPR或CCPA）就緒服務相結合。 來自 Adobe Target 或 Adobe Analytics 與整合相關的個人資料不會儲存在 AEM 中。


有關詳細資訊，請參閱以下內容：

* [Adobe Target - 隱私權概觀](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=en)

* [Adobe Analytics 資料隱私權工作流程](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)

## AEM Communities {#aem-communities}

AEM Communities賦予資料主體資料可移植性、訪問權和被遺忘權 [開箱即用API](/help/communities/user-ugc-management-service.md)。 這些API允許批量刪除和批量導出用戶生成的內容，並禁用通過其授權ID標識的用戶帳戶。 但是，通過刪除CRXDE Lite中的用戶節點實現永久刪除用戶帳戶，這滿足了從系統中輕鬆選擇退出的需要。

此外，AEM Communities通過其Bulk Doveration控制台提供設計上的隱私保護，該控制台允許特權成員查找和刪除用戶的貢獻和詳細資訊。 「成員」管理控制台允許限制為禁止參與者。 此外，它授權資料主體刪除其所作貢獻。

## AEM Forms {#aem-forms}

AEM Forms包括可捕獲、處理和儲存資料以協調業務流程和完成數字交易的元件和工作流。 不同的元件使用不同的資料儲存，並允許與自定義資料儲存整合。 以下文檔說明了訪問和處理用戶資料以支援元件的資料保護和隱私（例如，GDPR或CCPA）工作流的過程和指南。

* [表單入口網站](/help/forms/using/forms-portal-handling-user-data.md)
* [通信管理](/help/forms/using/correspondence-management-handling-user-data.md)
* [與Adobe Sign](/help/forms/using/integration-adobe-sign-handling-user-data.md)
* [以Forms為中心的OSGi工作流](/help/forms/using/forms-workflow-osgi-handling-user-data.md)
* [FormsJEE工作流](/help/forms/using/forms-workflow-jee-handling-user-data.md) (僅AEM FormsJEE)
* [文檔安全性](/help/forms/using/document-security-handling-user-data.md) (僅AEM FormsJEE)
* [用戶管理](/help/forms/using/user-management-handling-user-data.md) (僅AEM FormsJEE)
