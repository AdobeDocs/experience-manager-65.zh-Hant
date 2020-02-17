---
title: 在生產就緒模式中執行AEM
seo-title: 在生產就緒模式中執行AEM
description: 瞭解如何在「生產就緒模式」中執行AEM。
seo-description: 瞭解如何在「生產就緒模式」中執行AEM。
uuid: f48c8bae-c72f-4772-967e-f1526f096399
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 32da99f0-f058-40ae-95a8-2522622438ce
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# 在生產就緒模式中執行AEM{#running-aem-in-production-ready-mode}

有了AEM 6.1,Adobe推出全新的 `"nosamplecontent"` 執行模式，旨在自動化準備AEM例項以在生產環境中部署所需的步驟。

新的執行模式不僅會自動設定執行個體，以符合安全性檢查清單中所述的安全性最佳實務，還會移除程式中的所有範例geometrixx應用程式和設定。

>[!NOTE]
>
>由於AEM Production Ready Mode僅涵蓋保護例項所需的大部分工作，因此強烈建議您先參閱 [Security Checklist](/help/sites-administering/security-checklist.md) ，再與生產環境一起上線。
>
>此外，請注意，在「生產就緒模式」中執行AEM將有效停用對CRXDE Lite的存取。 如果您需要它以進行除錯，請參 [閱「在AEM中啟用CRXDE Lite」](/help/sites-administering/enabling-crxde-lite.md)。

![chlimage_1-83](assets/chlimage_1-83a.png)

若要在生產就緒模式中執行AEM，您只需透過執行模式開關將 `nosamplecontent` AEM新 `-r` 增至您現有的啟動引數：

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

例如，您可以使用生產就緒來啟動具有MongoDB永續性的作者實例，如下所示：

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## 更改生產就緒模式的一部分 {#changes-part-of-the-production-ready-mode}

更具體地說，當AEM以生產就緒模式執行時，將會執行下列組態變更：

1. 在生 **產就緒模式下** ,CRXDE支援包( `com.adobe.granite.crxde-support`)預設禁用。 它可隨時從Adobe公用Maven儲存庫安裝。 AEM 6.1需使用3.0.0版。

1. Apache Sling Simple webDAV Access to repositories **(** )bundle將僅適用於作 `org.apache.sling.jcr.webdav`者例項 **** 。

1. 新建立的使用者必須在第一次登入時變更密碼。 這不適用於管理員使用者。
1. **對於** Apache Java Script Handler **，將禁用生成**&#x200B;調試資訊。

1. **已針對** Apache Sling JSP Script Handler停用 **Mapped content** 和Generate debug info ****。

1. The **Day CQ WCM Filter** is set to `edit` on author **and** on publish `disabled`**** instances.

1. **Adobe Granite HTML Library manager已設定** ，並設定下列設定：

   1. **** 精簡： `enabled`
   1. **** 除錯： `disabled`
   1. **** Gzip: `enabled`
   1. **** 時機： `disabled`

1. 依預 **設，Apache Sling GET Servlet** 已設為支援安全組態，如下所示：

| **設定** | **作者** | **發佈** |
|---|---|---|
| TXT轉譯 | 已停用 | 已停用 |
| HTML轉譯 | 已停用 | 已停用 |
| JSON轉譯 | 已啟用 | 已啟用 |
| XML轉譯 | 已停用 | 已停用 |
| json.maximumresults | 1000 | 100 |
| 自動索引 | 已停用 | 已停用 |

