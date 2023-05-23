---
title: 安全性
seo-title: Security
description: 應用程式安全性在開發階段啟動
seo-description: Application Security starts during the development phase
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
source-git-commit: c55b70ec11842d3f7d82adbf552b2624c1dcc599
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 安全性{#security}

應用程式安全性在開發階段啟動。 Adobe建議應用以下安全最佳做法。

## 使用請求會話 {#use-request-session}

遵循最小權限原則，Adobe建議使用綁定到用戶請求的會話和適當的訪問控制來完成每個儲存庫訪問。

## Protect反對跨站點指令碼(XSS) {#protect-against-cross-site-scripting-xss}

跨站點指令碼(XSS)允許攻擊者將代碼注入其他用戶查看的網頁。 惡意Web用戶可利用此安全漏洞繞過訪問控制。

應AEM用輸出時過濾所有用戶提供的內容的原則。 在開發和測試期間，防止XSS是最優先的任務。

提供的XSS保護機制AEM基於 [AntiSamy Java庫](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) 提供 [OWASP（Open Web應用程式安全項目）](https://www.owasp.org/)。 預設AntiSamy配置可在

`/libs/cq/xssprotection/config.xml`

通過覆蓋配置檔案來調整此配置以適應您自己的安全需要，這一點非常重要。 官員 [AntiSamy文檔](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) 將為您提供實施安全要求所需的所有資訊。

>[!NOTE]
>
>我們強烈建議您始終使用 [XSSAPI由提供AEM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html)。

另外，Web應用防火牆，例如 [mod_security for Apache](https://www.modsecurity.org)，可以對部署環境的安全性提供可靠、集中的控制，並防止以前未被發現的跨站點指令碼攻擊。

## 訪問Cloud Service資訊 {#access-to-cloud-service-information}

>[!NOTE]
>
>Cloud Service資訊的ACL以及保護實例所需的OSGi設定將作為 [生產就緒模式](/help/sites-administering/production-ready.md)。 雖然這意味著您不需要手動更改配置，但仍建議您在開始部署之前先查看配置更改。

當你 [將你AEM的實例與Adobe Marketing Cloud](/help/sites-administering/marketing-cloud.md) 您使用 [Cloud Service配置](/help/sites-developing/extending-cloud-config.md)。 有關這些配置的資訊以及收集到的任何統計資訊都儲存在儲存庫中。 如果您正在使用此功能，我們建議您查看此資訊上的預設安全性是否與您的要求相符。

Webservicesupport模組將統計資訊和配置資訊寫入：

`/etc/cloudservices`

具有預設權限：

* 作者環境： `read` 為 `contributors`

* 發佈環境： `read` 為 `everyone`

## Protect反跨站點偽造請求攻擊 {#protect-against-cross-site-request-forgery-attacks}

有關用於緩解CSRF攻AEM擊的安全機制的詳細資訊，請參見 [吊具引用過濾器](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 和 [CSRF保護框架文檔](/help/sites-developing/csrf-protection.md)。
