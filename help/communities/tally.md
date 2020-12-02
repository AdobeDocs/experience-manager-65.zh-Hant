---
title: Tally Essentials
seo-title: Tally Essentials
description: 計數分類概覽
seo-description: 計數分類概覽
uuid: c369c6a1-9ced-4b5c-af43-8c03236eaa52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 9941ba90-3d40-4c90-bca8-5db49603cbfa
translation-type: tm+mt
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---


# Tally Essentials {#tally-essentials}

Tally是抽象類別，提供一套標準方法，可收集會員對特定產品和服務的評價意見。 不支援匿名意見回應。 網站訪客必須註冊並登入才能參與並登入，以變更其意見回應。 登入的要求可避免多則貼文，以協調並提升意見回應的價值。

可通過擴展抽象計數類來建立自定義計數元件。

[](essentials-liking.md) Liking是一種簡單的表達積極意見的統計。

[沃](essentials-voting.md) 廷格是一種簡單的表達正面或負面意見的方式。

[Rating是](rating-basics.md) 一種實施統計的方法，它使用星型系統來表達從正面到負面的一系列觀點。

自AEM 6.1起，民調問答元件不再可用。

[回](reviews-basics.md) 顧SCF元件，它是注釋和評 [](essentials-comments.md) 分的 [混合](rating-basics.md)。

## 客戶端{#essentials-for-client-side}的基本功能

* [用戶端自訂](client-customize.md)

## 伺服器端{#essentials-for-server-side}的基本工具

* [計數API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [計數端點](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [伺服器端自訂](server-customize.md)

### 存取已張貼的記錄(UGC){#accessing-posted-tallies-ugc}

UGC應使用其中一種標準的協調方法來協調。
請參閱[協調使用者產生的內容](moderate-ugc.md)。

自AEM 6.1 Communities起，使用[通用商店](working-with-srp.md)做為UGC，不論選擇的儲存選項（例如ASRP、MSRP或JSRP），都可程式化存取UGC。

**UGC在儲存庫中的位置和格式可能會變更，但不會發出警告**。

請參閱：

* [儲存資源提供方概述](srp.md) -簡介和儲存庫使用概述。
* [SRP和UGC Essentials](srp-and-ugc.md)  - SRP實用程式方法和示例。
* [使用SRP](accessing-ugc-with-srp.md) -編碼准則存取UGC。
* [SocialUtils重構](socialutils.md) -將不建議使用的公用程式方法對應至目前的SRP公用程式方法。

