---
title: 以生產就緒模式執行AEM
seo-title: 以生產就緒模式執行AEM
description: 了解如何以生產就緒模式執行AEM。
seo-description: 了解如何以生產就緒模式執行AEM。
uuid: f48c8bae-c72f-4772-967e-f1526f096399
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 32da99f0-f058-40ae-95a8-2522622438ce
exl-id: 3c342014-f8ec-4404-afe5-514bdb651aae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 3%

---

# 在生產就緒模式下運行AEM{#running-aem-in-production-ready-mode}

透過AEM 6.1,Adobe推出新的`"nosamplecontent"`執行模式，旨在自動化準備AEM執行個體以在生產環境中部署所需的步驟。

新的執行模式不僅會自動設定執行個體以遵循安全性檢查清單中所述的安全性最佳實務，也會移除程式中的所有範例geometrixx應用程式和設定。

>[!NOTE]
>
>由於出於實際原因，AEM生產就緒模式將僅涵蓋保護實例所需的大部分任務，因此強烈建議您先參閱[安全檢查清單](/help/sites-administering/security-checklist.md)，再與生產環境上線。
>
>另外，請注意，在生產就緒模式中執行AEM將會有效停用CRXDE Lite存取權。 如果您需要它進行偵錯，請參閱[在AEM](/help/sites-administering/enabling-crxde-lite.md)中啟用CRXDE Lite。

![chlimage_1-83](assets/chlimage_1-83a.png)

若要在生產就緒模式中執行AEM，您只需透過`-r`執行模式切換器將`nosamplecontent`新增至您現有的啟動引數：

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

例如，您可以使用生產就緒，啟動具有MongoDB永續性的製作例項，如下所示：

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## 更改生產就緒模式的一部分{#changes-part-of-the-production-ready-mode}

更具體來說，當AEM以生產就緒模式執行時，將執行下列設定變更：

1. 預設情況下，在生產就緒模式下，將禁用&#x200B;**CRXDE支援包**(`com.adobe.granite.crxde-support`)。 您可以隨時從Adobe公用Maven存放庫安裝。 AEM 6.1需要3.0.0版。

1. **Apache Sling Simple WebDAV存取存放庫**(`org.apache.sling.jcr.webdav`)套件僅可在&#x200B;**author**&#x200B;例項上使用。

1. 新建立的使用者必須在首次登入時變更密碼。 這不適用於管理員使用者。
1. **針對Apache** Sling Java指令碼處理常式 **停用產生除錯資訊**。

1. **Apache Sling** JSP指令 **碼處理常** 式會停用「對應內容」 **和「產生除錯資訊」**。

1. 在&#x200B;**author**&#x200B;和&#x200B;**publish**&#x200B;例項上，**Day CQ WCM Filter**&#x200B;設為`edit`。`disabled`

1. **AdobeGranite HTML Library Manager**&#x200B;設定有下列設定：

   1. **Minify:** `enabled`
   1. **調試：** `disabled`
   1. **Gzip:** `enabled`
   1. **時間：** `disabled`

1. **Apache SlingGETServlet**&#x200B;預設為支援安全設定，如下所示：

| **設定** | **作者** | **發佈** |
|---|---|---|
| TXT轉譯 | 已停用 | 已停用 |
| HTML轉譯 | 已停用 | 已停用 |
| JSON轉譯 | 已啟用 | 已啟用 |
| XML格式副本 | 已停用 | 已停用 |
| json.maximumresults | 1000 | 100 |
| 自動索引 | 已停用 | 已停用 |
