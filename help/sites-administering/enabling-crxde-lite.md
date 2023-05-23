---
title: 啟用CRXDE LiteAEM
seo-title: Enabling CRXDE Lite in AEM
description: 瞭解如何在中啟用CRXDE LiteAEM。
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

# 啟用CRXDE LiteAEM{#enabling-crxde-lite-in-aem}

為了確保安AEM裝盡可能安全，安全檢查表建議 [禁用WebDAV](/help/sites-administering/security-checklist.md#disable-webdav) 在生產環境中。

然而，CRXDE Lite取決於 `org.apache.sling.jcr.davex` 捆綁即可正常運行，因此禁用WebDAV也將有效地禁用CRXDE Lite。

當發生這種情況時，瀏覽到 `https://serveraddress:4502/crx/de/index.jsp` 將顯示空的根節點，所有CRXDE Lite資源的HTTP請求都將失敗：

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

雖然此建議旨在盡可能減少攻擊面，但系統管理員有時可能需要訪問CRXDE Lite，以便瀏覽內容或調試生產實例上的問題。

您可以啟用CRXDE Lite [OSGi設定](#enabling-crxde-lite-osgi) 或 [cURL命令](#enabling-crxde-lite-curl)。

>[!WARNING]
>
>由於這些方法的操作方式略有不同，您應使用 ***或*** 奧斯吉 ***或*** cURL。
>
>這兩種方法是 ***不*** 可互換。

## 啟用與OSGI的CRXDE Lite {#enabling-crxde-lite-osgi}

如果禁用，則可以按以下步驟開啟CRXDE Lite:

1. 轉至OSGi元件控制台，位於 `http://localhost:4502/system/console/components`
1. 搜索以下元件：

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. 按一下其旁邊的扳手錶徵圖以查看其配置選項：

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. 建立以下配置：

   * **根路徑:** `/crx/server`
   * 在下面勾選框 **使用絕對URI**。

1. 使用完CRXDE Lite後，請確保再次禁用WebDAV。

## 啟用cURLCRXDE Lite {#enabling-crxde-lite-curl}

您還可以通過cURL啟用CRXDE Lite，方法是運行以下命令：

```shell
curl -u admin:admin -F "jcr:primaryType=sling:OsgiConfig" -F "alias=/crx/server" -F "dav.create-absolute-uri=true" -F "dav.create-absolute-uri@TypeHint=Boolean" http://localhost:4502/apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
```

## 其他資源 {#other-resources}

有關6個安全功AEM能的詳細資訊，請參閱以下頁：

* [安AEM全核對表](/help/sites-administering/security-checklist.md)
* [在生AEM產就緒模式下運行](/help/sites-administering/production-ready.md)
