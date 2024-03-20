---
title: 以生產就緒模式執行AEM
description: 瞭解如何在生產就緒模式下執行AEM。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 3c342014-f8ec-4404-afe5-514bdb651aae
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 3%

---

# 以生產就緒模式執行AEM{#running-aem-in-production-ready-mode}

Adobe透過AEM 6.1推出全新的 `"nosamplecontent"` 執行模式旨在將準備AEM執行個體以在生產環境中部署所需的步驟自動化。

新的執行模式不僅會自動設定執行個體以遵循安全性檢查清單中所述的安全性最佳實務，而且還會移除流程中的所有範例Geometrixx應用程式和設定。

>[!NOTE]
>
>由於實際原因，AEM生產就緒模式將僅涵蓋保護執行個體所需的大部分任務，因此強烈建議您參閱 [安全性檢查清單](/help/sites-administering/security-checklist.md) 開始使用您的生產環境之前。
>
>另外也請注意，以生產就緒模式執行AEM將有效地停用對CRXDE Lite的存取。 如果您需要此工具以進行偵錯，請參閱 [在AEM中啟用CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

![chlimage_1-83](assets/chlimage_1-83a.png)

若要以生產就緒模式執行AEM，您只需新增 `nosamplecontent` 透過 `-r` 執行模式切換至您現有的啟動引數：

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

例如，您可以使用生產準備啟動具有MongoDB持續性的作者執行個體，如下所示：

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## 變更部分生產就緒模式 {#changes-part-of-the-production-ready-mode}

更具體來說，當AEM在生產就緒模式下執行時，會執行以下設定變更：

1. 此 **CRXDE支援套裝** ( `com.adobe.granite.crxde-support`)預設會在生產就緒模式中停用。 您可以隨時從Adobe公共Maven存放庫安裝。 AEM 6.1需要版本3.0.0。

1. 此 **Apache Sling對存放庫的簡單WebDAV存取** ( `org.apache.sling.jcr.webdav`)套件組合將僅適用於 **作者** 執行個體。

1. 新建立的使用者必須在第一次登入時變更密碼。 這不適用於管理員使用者。
1. **產生偵錯資訊** 已為「 」停用 **Apache Sling JavaScript處理常式**.

1. **對應的內容** 和 **產生偵錯資訊** 已針對停用 **Apache Sling JSP指令碼處理常式**.

1. 此 **Day CQ WCM篩選器** 設為 `edit` 於 **作者** 和 `disabled` 於 **發佈** 執行個體。

1. 此 **AdobeGraniteHTML庫管理員** 已使用下列設定進行設定：

   1. **縮制：** `enabled`
   1. **偵錯：** `disabled`
   1. **Gzip：** `enabled`
   1. **時間：** `disabled`

1. 此 **Apache SlingGETServlet** 預設為支援安全設定，如下所示：

| **設定** | **作者** | **發佈** |
|---|---|---|
| TXT轉譯 | 已停用 | 已停用 |
| HTML轉譯 | 已停用 | 已停用 |
| JSON轉譯 | 已啟用 | 已啟用 |
| XML轉譯 | 已停用 | 已停用 |
| json.maximumresults | 1000 | 100 |
| 自動索引 | 已停用 | 已停用 |
