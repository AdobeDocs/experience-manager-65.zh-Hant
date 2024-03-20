---
title: 安全性
description: 應用程式安全性在開發階段開始
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# 安全性{#security}

應用程式安全性會在開發階段啟動。 Adobe建議套用下列安全性最佳實務。

## 使用要求工作階段 {#use-request-session}

按照最小許可權原則，Adobe建議每個存放庫存取都透過使用繫結至使用者要求的工作階段和適當的存取控制來完成。

## Protect避免跨網站指令碼(XSS) {#protect-against-cross-site-scripting-xss}

跨網站指令碼(XSS)可讓攻擊者將程式碼插入其他使用者檢視的網頁。 惡意的Web使用者可能會利用這個安全性弱點來略過存取控制。

AEM會套用輸出時篩選所有使用者提供內容的原則。 在開發和測試期間，防止XSS都被給予最高優先順序。

AEM提供的XSS保護機制是根據 [AntiSamy Java™資料庫](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project) 提供者 [OWASP (Open Web Application Security Project)](https://owasp.org/). 預設AntiSamy設定可在以下位置找到：

`/libs/cq/xssprotection/config.xml`

請務必透過覆蓋設定檔案來調整此設定，以符合您自己的安全性需求。 官方 [AntiSamy檔案](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project) 提供您實作安全性需求所需的所有資訊。

>[!NOTE]
>
>Adobe建議您一律使用 [AEM提供的XSSAPI](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/xss/XSSAPI.html).

此外，Web應用程式防火牆，例如 [Apache適用的mod_security](https://www.modsecurity.org)，可提供部署環境安全性的可靠集中控制，並防止先前未偵測到的跨網站指令碼攻擊。

## 存取Cloud Service資訊 {#access-to-cloud-service-information}

>[!NOTE]
>
>Cloud Service資訊的ACL和確保執行個體安全所需的OSGi設定會隨著 [生產就緒模式](/help/sites-administering/production-ready.md). 雖然這表示您不需要手動變更設定，但建議您先檢閱設定，然後再開始部署。

當您 [將您的AEM執行個體與Adobe Experience Cloud整合](/help/sites-administering/marketing-cloud.md)，您會使用 [Cloud Service設定](/help/sites-developing/extending-cloud-config.md). 這些組態的相關資訊以及所收集的任何統計資料都會儲存在儲存區域中。 Adobe建議，如果您使用此功能，請檢閱此資訊的預設安全性是否符合您的需求。

webservicesupport模組會將統計資料與組態資訊寫入下方：

`/etc/cloudservices`

使用預設許可權：

* 作者環境： `read` 的 `contributors`

* 發佈環境： `read` 的 `everyone`

## Protect抵禦跨網站請求偽造攻擊 {#protect-against-cross-site-request-forgery-attacks}

如需AEM用於減少CSRF攻擊的安全性機制的詳細資訊，請參閱 [Sling查閱者篩選器](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 安全性檢查清單的區段及 [CSRF Protection Framework檔案](/help/sites-developing/csrf-protection.md).
