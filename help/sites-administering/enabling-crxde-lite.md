---
title: 在AEM中啟用CRXDE Lite
seo-title: 在AEM中啟用CRXDE Lite
description: 瞭解如何在AEM中啟用CRXDE Lite。
seo-description: 瞭解如何在AEM中啟用CRXDE Lite。
uuid: d7a3db67-6384-463b-9aa9-f08ecc6c99c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 72df3ece-badf-466b-8f9a-0ec985d87741
translation-type: tm+mt
source-git-commit: a833a34bbeb938c72cdb851a46b2ffd97aee9f6d

---


# 在AEM中啟用CRXDE Lite{#enabling-crxde-lite-in-aem}

為確保AEM安裝盡可能安全，安全性檢查清單建議在生產環 [境中停用WebDAV](/help/sites-administering/security-checklist.md#disable-webdav) 。

不過，CRXDE Lite依賴搭售才能正 `org.apache.sling.jcr.davex` 常運作，因此停用WebDAV也可有效停用CRXDE Lite。

發生此情況時，瀏覽至 `https://serveraddress:4502/crx/de/index.jsp` 將顯示空的根節點，而對CRXDE Lite資源的所有HTTP請求將失敗：

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

雖然此建議的目的是盡可能減少攻擊面，但系統管理員有時可能需要存取CRXDE Lite，以瀏覽生產例項的內容或除錯問題。

如果禁用，則可通過以下過程開啟CRXDE Lite:

1. 前往OSGi元件主控台，網址為 `http://localhost:4502/system/console/components`
1. 搜尋下列元件：

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. 按一下其旁的扳手圖示，以檢視其設定選項：

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. 建立下列設定：

   * **根路徑:** `/crx/server`
   * 勾選「使用絕 **對URI」(Use absolute URIs)下方的方塊**。

1. 使用完CRXDE Lite後，請務必再次停用WebDAV。

您也可以透過cURL啟用CRXDE Lite，方法是執行下列命令：

```shell
curl -u admin:admin -F "jcr:primaryType=sling:OsgiConfig" -F "alias=/crx/server" -F "dav.create-absolute-uri=true" -F "dav.create-absolute-uri@TypeHint=Boolean" http://localhost:4502/apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
```

## 其他資源 {#other-resources}

如需AEM 6安全性功能的詳細資訊，請參閱下列頁面：

* [AEM安全性檢查清單](/help/sites-administering/security-checklist.md)
* [在生產就緒模式中執行AEM](/help/sites-administering/production-ready.md)

