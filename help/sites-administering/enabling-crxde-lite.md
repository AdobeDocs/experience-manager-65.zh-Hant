---
title: 在AEM中啟用CRXDE Lite
seo-title: Enabling CRXDE Lite in AEM
description: 了解如何在AEM中啟用CRXDE Lite。
seo-description: Learn how to enable CRXDE Lite in AEM.
uuid: d7a3db67-6384-463b-9aa9-f08ecc6c99c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 72df3ece-badf-466b-8f9a-0ec985d87741
exl-id: bf51def2-1dd4-4bd3-b989-685058f0ead8
source-git-commit: a4183bb9d72763ebea3b464c77fce978c723e053
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 1%

---

# 在AEM中啟用CRXDE Lite{#enabling-crxde-lite-in-aem}

為確保AEM安裝盡可能安全，安全性檢查清單建議 [禁用WebDAV](/help/sites-administering/security-checklist.md#disable-webdav) 在生產環境中。

然而，CRXDE Lite取決於 `org.apache.sling.jcr.davex` 捆綁以正常運行，因此禁用WebDAV將有效地禁用CRXDE Lite。

發生此情況時，請瀏覽至 `https://serveraddress:4502/crx/de/index.jsp` 將顯示空的根節點，而所有CRXDE Lite資源的HTTP請求將會失敗：

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

雖然此建議旨在盡可能減少攻擊面，但系統管理員有時需要存取CRXDE Lite，才能瀏覽生產執行個體的內容或除錯問題。

您可以使用 [OSGi設定](#enabling-crxde-lite-osgi) 或 [cURL命令](#enabling-crxde-lite-curl).

>[!WARNING]
>
>由於這些方法的運作方式稍有差異，您應使用 ***heer*** OSGI ***或*** cURL。
>
>兩種方法為 ***not*** 可互換。

## 使用OSGI啟用CRXDE Lite {#enabling-crxde-lite-osgi}

如果禁用，則可以按照以下過程開啟CRXDE Lite:

1. 前往OSGi元件主控台，網址為 `http://localhost:4502/system/console/components`
1. 搜尋下列元件：

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. 按一下扳手旁的圖示，即可查看其設定選項：

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. 建立下列設定：

   * **根路徑:** `/crx/server`
   * 勾選下方的方塊 **使用絕對URI**.

1. 使用完CRXDE Lite後，請務必再次停用WebDAV。

## 使用cURL啟用CRXDE Lite {#enabling-crxde-lite-curl}

您也可以執行以下命令，透過cURL啟用CRXDE Lite:

```shell
curl -u admin:admin -F "jcr:primaryType=sling:OsgiConfig" -F "alias=/crx/server" -F "dav.create-absolute-uri=true" -F "dav.create-absolute-uri@TypeHint=Boolean" http://localhost:4502/apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
```

## 其他資源 {#other-resources}

如需AEM 6安全性功能的詳細資訊，請參閱下列頁面：

* [AEM安全性檢查清單](/help/sites-administering/security-checklist.md)
* [以生產就緒模式執行AEM](/help/sites-administering/production-ready.md)
