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
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# 安全性{#security}

應用程式安全性在開發階段期間啟動。 Adobe建議套用下列安全性最佳實務。

## 使用請求會話{#use-request-session}

按照最小權限原則，Adobe建議使用綁定到用戶請求的會話和適當的訪問控制來完成每個儲存庫訪問。

## Protect反對跨網站指令碼(XSS){#protect-against-cross-site-scripting-xss}

跨網站指令碼(XSS)可讓攻擊者將程式碼插入其他使用者檢視的網頁。 惡意Web用戶可利用此安全漏洞繞過訪問控制。

AEM會套用在輸出時篩選所有使用者提供的內容的原則。 在開發和測試期間，防止XSS的優先順序最高。

AEM提供的XSS保護機制基於[OWASP（Open Web應用程式安全項目）](https://www.owasp.org/)提供的[AntiSamy Java庫](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project)。 預設的AntiSamy配置位於

`/libs/cq/xssprotection/config.xml`

請務必借由覆蓋設定檔案，將此設定調整為符合您的安全需求。 官方的[AntiSamy文檔](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project)將為您提供實施安全要求所需的所有資訊。

>[!NOTE]
>
>強烈建議您一律使用AEM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html)提供的[XSSAPI來存取XSS保護API。

此外，Web應用程式防火牆（如Apache](https://www.modsecurity.org)的[mod_security）可提供對部署環境安全的可靠、集中的控制，並保護其免受以前未檢測到的跨站點指令碼攻擊。

## 訪問Cloud Service資訊{#access-to-cloud-service-information}

>[!NOTE]
>
>「Cloud Service資訊」的ACL以及保護實例所需的OSGi設定將作為[「生產就緒模式」](/help/sites-administering/production-ready.md)的一部分自動執行。 雖然這表示您不需要手動變更設定，但仍建議您在部署上線前先檢閱設定。

當您[將AEM例項與Adobe Marketing Cloud](/help/sites-administering/marketing-cloud.md)整合時，請使用[Cloud Service設定](/help/sites-developing/extending-cloud-config.md)。 這些設定的相關資訊以及收集的任何統計資訊都儲存在儲存庫中。 建議您，如果您使用此功能，請檢閱此資訊的預設安全性是否符合您的需求。

Webservicesupport模組將統計資訊和配置資訊寫入：

`/etc/cloudservices`

具有預設權限：

* 製作環境：`contributors`的`read`

* 發佈環境：`everyone`的`read`

## Protect針對跨網站請求偽造攻擊{#protect-against-cross-site-request-forgery-attacks}

如需AEM用來緩解CSRF攻擊的安全機制的詳細資訊，請參閱安全性檢查清單的[Sling Referrer Filter](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)區段和[CSRF保護框架檔案](/help/sites-developing/csrf-protection.md)。
