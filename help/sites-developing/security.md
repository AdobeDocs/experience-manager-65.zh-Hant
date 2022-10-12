---
title: 安全性
seo-title: Security
description: 應用程式安全性在開發階段開始
seo-description: Application Security starts during the development phase
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
source-git-commit: c55b70ec11842d3f7d82adbf552b2624c1dcc599
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 安全性{#security}

應用程式安全性在開發階段期間啟動。 Adobe建議套用下列安全性最佳實務。

## 使用要求工作階段 {#use-request-session}

遵循最小權限原則，Adobe建議使用綁定到用戶請求的會話和適當的訪問控制來完成每個儲存庫訪問。

## Protect反對跨網站指令碼(XSS) {#protect-against-cross-site-scripting-xss}

跨網站指令碼(XSS)可讓攻擊者將程式碼插入其他使用者檢視的網頁。 惡意Web用戶可利用此安全漏洞繞過訪問控制。

AEM會套用在輸出時篩選所有使用者提供的內容的原則。 在開發和測試期間，防止XSS的優先順序最高。

AEM提供的XSS保護機制以 [AntiSamy Java庫](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) 由 [OWASP（Open Web應用安全項目）](https://www.owasp.org/). 預設的AntiSamy配置位於

`/libs/cq/xssprotection/config.xml`

請務必借由覆蓋設定檔案，將此設定調整為符合您的安全需求。 官員 [AntiSamy檔案](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) 會提供您實施安全需求所需的所有資訊。

>[!NOTE]
>
>強烈建議您一律使用 [AEM提供的XSSAPI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html).

此外，Web應用程式防火牆，例如 [Apache的mod_security](https://www.modsecurity.org)，可提供對部署環境安全性的可靠中央控制，並防止先前未偵測到的跨網站指令碼攻擊。

## 存取Cloud Service資訊 {#access-to-cloud-service-information}

>[!NOTE]
>
>Cloud Service資訊的ACL以及保護執行個體所需的OSGi設定，會在 [生產就緒模式](/help/sites-administering/production-ready.md). 雖然這表示您不需要手動變更設定，但仍建議您在部署上線前先檢閱設定。

當您 [將AEM執行個體與Adobe Marketing Cloud整合](/help/sites-administering/marketing-cloud.md) 您使用 [Cloud Service配置](/help/sites-developing/extending-cloud-config.md). 這些設定的相關資訊以及收集的任何統計資訊都儲存在儲存庫中。 建議您，如果您使用此功能，請檢閱此資訊的預設安全性是否符合您的需求。

Webservicesupport模組將統計資訊和配置資訊寫入：

`/etc/cloudservices`

具有預設權限：

* 製作環境： `read` for `contributors`

* 發佈環境： `read` for `everyone`

## Protect防止跨網站請求偽造攻擊 {#protect-against-cross-site-request-forgery-attacks}

如需AEM用來緩解CSRF攻擊的安全機制的詳細資訊，請參閱 [Sling反向連結篩選器](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 安全檢查清單和 [CSRF保護框架文檔](/help/sites-developing/csrf-protection.md).
