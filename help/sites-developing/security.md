---
title: 安全性
description: 應用程式安全性在開發階段開始
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
solution: Experience Manager, Experience Manager Sites
feature: Developing,Security
role: Developer
source-git-commit: 9f5812d7b252bcf39896b4fbf2e3ac5c24bdb808
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%
---
# 安全性{#security}

應用程式安全性會在開發階段啟動。 Adobe建議您套用下列安全性最佳實務。

## 使用要求工作階段 {#use-request-session}

根據最低許可權原則，Adobe建議使用與使用者要求繫結的工作階段和適當的存取控制，來完成每個存放庫存取權。

## 避免跨網站指令碼(XSS) {#protect-against-cross-site-scripting-xss}

跨網站指令碼(XSS)可讓攻擊者將程式碼插入其他使用者檢視的網頁。 惡意的Web使用者可能會利用這個安全性弱點來略過存取控制。

AEM會套用輸出時篩選所有使用者提供內容的原則。 在開發和測試期間，防止XSS都被給予最高優先順序。

AEM提供的XSS保護機制是以[OWASP (Open Web Application Security Project)](https://owasp.org/)提供的[AntiSamy Java™資料庫](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project)為基礎。 預設AntiSamy設定可在以下位置找到：

`/libs/cq/xssprotection/config.xml`

請務必透過覆蓋設定檔案來調整此設定，以符合您自己的安全性需求。 官方[AntiSamy檔案](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project)提供您實作安全性需求所需的所有資訊。

>[!NOTE]
>
>Adobe建議您一律使用AEM[&#128279;](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5/javadoc/com/adobe/granite/xss/XSSAPI.html)提供的XSSAPI來存取XSS保護API。

此外，Web應用程式防火牆（例如Apache的[mod_security](https://www.modsecurity.org)）可提供部署環境安全性的可靠集中控制，並防止先前未偵測到的跨網站指令碼攻擊。

## 存取Cloud Service資訊 {#access-to-cloud-service-information}

>[!NOTE]
>
>作為[生產就緒模式](/help/sites-administering/production-ready.md)的一部分，保護您的執行個體所需的Cloud Service資訊和OSGi設定的ACL會自動完成。 雖然這表示您不需要手動變更設定，但建議您先檢閱設定，然後再開始部署。

當您[將您的AEM執行個體與Adobe Experience Cloud](/help/sites-administering/marketing-cloud.md)整合時，您會使用[Cloud Service設定](/help/sites-developing/extending-cloud-config.md)。 這些組態的相關資訊以及所收集的任何統計資料都會儲存在儲存區域中。 Adobe建議，如果您使用此功能，請檢閱此資訊的預設安全性是否符合您的需求。

webservicesupport模組會將統計資料與組態資訊寫入下方：

`/etc/cloudservices`

使用預設許可權：

* 作者環境： `contributors`的`read`

* 發佈環境： `everyone`的`read`

## 避免跨網站請求偽造攻擊 {#protect-against-cross-site-request-forgery-attacks}

如需AEM用來減少CSRF攻擊的安全性機制的詳細資訊，請參閱安全性檢查清單的[Sling反向連結篩選器](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)區段及[CSRF Protection Framework檔案](/help/sites-developing/csrf-protection.md)。
