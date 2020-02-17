---
title: 安全性
seo-title: 安全性
description: 應用程式安全性在開發階段開始
seo-description: 應用程式安全性在開發階段開始
uuid: efd5f3bc-da07-4fc8-a6ce-f1e6f5084c9e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: d2267663-6c1d-413c-9862-e82e21ae6906
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 安全性{#security}

應用程式安全性會在開發階段啟動。 Adobe建議套用下列安全性最佳實務。

## 使用請求作業 {#use-request-session}

Adobe建議依循Leas權限原則，使用系結至使用者要求的作業階段和適當的存取控制，來完成每個儲存庫的存取。

## 防止跨網站指令碼(XSS) {#protect-against-cross-site-scripting-xss}

跨網站指令碼(XSS)可讓攻擊者將程式碼注入其他使用者檢視的網頁。 惡意Web使用者可利用此安全性弱點略過存取控制。

AEM會套用在輸出時篩選所有使用者提供內容的原則。 在開發和測試期間，防止XSS的優先順序最高。

AEM提供的XSS保護機制是以 [OWASP(Open Web Application Security Project)提供的](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) AntiSamy Java Library [(AntiSamy Java Library](https://www.owasp.org/))為基礎的。 AntiSamy預設組態可在

`/libs/cq/xssprotection/config.xml`

請務必通過覆蓋配置檔案來調整此配置以滿足您自己的安全需求。 官方 [的AntiSamy檔案](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) ，將提供您所需的所有資訊，以實作您的安全性要求。

>[!NOTE]
>
>我們強烈建議您一律使用AEM提供的 [XSSAPI存取XSS保護API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html)。

此外，Web應用程式防火牆(例如 [mod_security for Apache](https://www.modsecurity.org))可提供可靠、集中的部署環境安全控制，並防止先前未偵測到的跨網站指令碼攻擊。

## 存取雲端服務資訊 {#access-to-cloud-service-information}

>[!NOTE]
>
>「雲端服務資訊」的ACL以及保護您實例所需的OSGi設定會自動化，成為「生產就緒模式」的 [一部分](/help/sites-administering/production-ready.md)。 雖然這表示您不需要手動進行設定變更，但仍建議您在部署上線前先檢閱設定。

當您將 [AEM實例與Adobe Marketing cloud整合時](/help/sites-administering/marketing-cloud.md) ，您會使 [用Cloud服務設定](/help/sites-developing/extending-cloud-config.md)。 有關這些配置的資訊以及收集到的任何統計資訊都儲存在儲存庫中。 我們建議您，如果您使用此功能，請檢閱此資訊的預設安全性是否符合您的需求。

webservicesupport模組將統計資訊和配置資訊寫入以下位置：

`/etc/cloudservices`

使用預設權限：

* 作者環境： `read` for `contributors`

* 發佈環境： `read` for `everyone`

## 防止跨網站偽造要求攻擊 {#protect-against-cross-site-request-forgery-attacks}

如需AEM運用來緩解CSRF攻擊的安全機制的詳細資訊，請參閱安全檢查清單的 [Sling Referrer Filter](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) (Security Checklist)區段和 [CSRF Protection Framwork檔案](/help/sites-developing/csrf-protection.md)。