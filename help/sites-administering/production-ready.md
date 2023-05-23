---
title: 在生AEM產就緒模式下運行
seo-title: Running AEM in Production Ready Mode
description: 瞭解如何在生產就AEM緒模式下運行。
seo-description: Learn how to run AEM in Production Ready Mode.
uuid: f48c8bae-c72f-4772-967e-f1526f096399
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 32da99f0-f058-40ae-95a8-2522622438ce
exl-id: 3c342014-f8ec-4404-afe5-514bdb651aae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 4%

---

# 在生AEM產就緒模式下運行{#running-aem-in-production-ready-mode}

在AEM6.1中，Adobe介紹了 `"nosamplecontent"` runmode旨在自動執行準備實例以在生AEM產環境中部署所需的步驟。

新運行模式不僅將自動配置實例以遵循安全檢查表中描述的安全最佳做法，還將刪除流程中所有示例幾何應用程式和配置。

>[!NOTE]
>
>由於實際原因，AEM生產就緒模式將僅涵蓋保護實例所需的大部分任務，因此強烈建議您咨詢 [安全核對表](/help/sites-administering/security-checklist.md) 在與生產環境共存之前。
>
>另請注意，在生AEM產就緒模式下運行將有效禁用對CRXDE Lite的訪問。 如果需要它用於調試，請參見 [啟用CRXDE LiteAEM](/help/sites-administering/enabling-crxde-lite.md)。

![chlimage_1-83](assets/chlimage_1-83a.png)

要在生產就緒AEM模式下運行，您只需添加 `nosamplecontent` 通過 `-r` runmode切換到您現有的啟動參數：

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

例如，您可以使用生產就緒啟動具有MongoDB持久性的作者實例，如下所示：

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## 更改生產就緒模式的一部分 {#changes-part-of-the-production-ready-mode}

更具體地說，在生產就緒模式下運行時AEM將執行以下配置更改：

1. 的 **CRXDE支援包** ( `com.adobe.granite.crxde-support`)在生產就緒模式下預設為禁用。 它可以隨時從Adobe公共Maven儲存庫安裝。 6.1需AEM要3.0.0版。

1. 的 **Apache Sling簡單WebDAV對儲存庫的訪問** ( `org.apache.sling.jcr.webdav`)捆綁包僅在 **作者** 實例。

1. 新建立的用戶將需要在首次登錄時更改密碼。 這不適用於管理員用戶。
1. **生成調試資訊** 已禁用 **Apache Sling Java指令碼處理程式**。

1. **映射的內容** 和 **生成調試資訊** 已禁用 **Apache Sling JSP指令碼處理程式**。

1. 的 **第CQ WCM篩選器** 設定為 `edit` 上 **作者** 和 `disabled` 上 **發佈** 實例。

1. 的 **Adobe花崗岩HTML庫經理** 配置了以下設定：

   1. **微型：** `enabled`
   1. **調試：** `disabled`
   1. **Gzip:** `enabled`
   1. **時間：** `disabled`

1. 的 **Apache SlingGETServlet** 預設設定為支援安全配置，如下所示：

| **設定** | **作者** | **發佈** |
|---|---|---|
| TXT格式副本 | 已停用 | 已停用 |
| HTML格式副本 | 已停用 | 已停用 |
| JSON格式副本 | 已啟用 | 已啟用 |
| XML格式副本 | 已停用 | 已停用 |
| json.maximumresults | 1000 | 100 |
| 自動索引 | 已停用 | 已停用 |
