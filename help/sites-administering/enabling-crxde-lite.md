---
title: 在AEM中啟用CRXDE Lite
seo-title: 在AEM中啟用CRXDE Lite
description: 了解如何在AEM中啟用CRXDE Lite。
seo-description: 了解如何在AEM中啟用CRXDE Lite。
uuid: d7a3db67-6384-463b-9aa9-f08ecc6c99c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 72df3ece-badf-466b-8f9a-0ec985d87741
exl-id: bf51def2-1dd4-4bd3-b989-685058f0ead8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# 在AEM{#enabling-crxde-lite-in-aem}中啟用CRXDE Lite

為確保AEM安裝盡可能安全，安全性檢查清單建議在生產環境中[停用WebDAV](/help/sites-administering/security-checklist.md#disable-webdav)。

但是，CRXDE Lite取決於`org.apache.sling.jcr.davex`捆綁包才能正常工作，因此禁用WebDAV將有效地禁用CRXDE Lite。

發生此情況時，瀏覽`https://serveraddress:4502/crx/de/index.jsp`會顯示空的根節點，而所有CRXDE Lite資源的HTTP請求將會失敗：

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

雖然此建議旨在盡可能減少攻擊面，但系統管理員有時需要存取CRXDE Lite，才能瀏覽生產執行個體的內容或除錯問題。

如果禁用，則可以按照以下過程開啟CRXDE Lite:

1. 前往`http://localhost:4502/system/console/components`的OSGi元件主控台
1. 搜尋下列元件：

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. 按一下扳手旁的圖示，即可查看其設定選項：

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. 建立下列設定：

   * **根路徑:** `/crx/server`
   * 在&#x200B;**使用絕對URI**&#x200B;下勾選該框。

1. 使用完CRXDE Lite後，請務必再次停用WebDAV。

您也可以執行以下命令，透過cURL啟用CRXDE Lite:

```shell
curl -u admin:admin -F "jcr:primaryType=sling:OsgiConfig" -F "alias=/crx/server" -F "dav.create-absolute-uri=true" -F "dav.create-absolute-uri@TypeHint=Boolean" http://localhost:4502/apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
```

## 其他資源{#other-resources}

如需AEM 6安全性功能的詳細資訊，請參閱下列頁面：

* [AEM安全性檢查清單](/help/sites-administering/security-checklist.md)
* [以生產就緒模式執行AEM](/help/sites-administering/production-ready.md)
