---
title: 在AEM中啟用CRXDE Lite
description: 瞭解如何啟用Adobe Experience Manager中的CRXDE Lite。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: bf51def2-1dd4-4bd3-b989-685058f0ead8
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# 在AEM中啟用CRXDE Lite{#enabling-crxde-lite-in-aem}

為確保AEM安裝儘可能安全，安全性檢查清單建議 [正在停用WebDAV](/help/sites-administering/security-checklist.md#disable-webdav) 在生產環境中。

不過，CRXDE Lite取決於 `org.apache.sling.jcr.davex` 套件組合以正常運作，因此停用WebDAV也會有效地停用CRXDE Lite。

發生此情況時，瀏覽至 `https://serveraddress:4502/crx/de/index.jsp` 將顯示一個空的根節點，並且對CRXDE Lite資源的所有HTTP請求都將失敗：

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

雖然此建議的目的是為了儘可能減少攻擊面，但系統管理員有時可能需要存取CRXDE Lite來瀏覽內容或偵錯生產執行個體上的問題。

您可以透過以下任一方式啟用CRXDE Lite： [OSGi設定](#enabling-crxde-lite-osgi) 或使用 [cURL命令](#enabling-crxde-lite-curl).

>[!WARNING]
>
>由於這些方法的操作方式略有差異，您應該使用 ***兩者之一*** OSGI ***或*** cURL。
>
>兩種方法為 ***非*** 可互換。

## 使用OSGI啟用CRXDE Lite {#enabling-crxde-lite-osgi}

如果停用，您可以依照下列程式開啟CRXDE Lite：

1. 前往位於的OSGi元件主控台 `http://localhost:4502/system/console/components`
1. 搜尋下列元件：

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. 按一下旁邊的扳手圖示以檢視其設定選項：

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. 建立下列設定：

   * **根路徑：** `/crx/server`
   * 勾選下方的方塊 **使用絕對URI**.

1. 完成使用CRXDE Lite時，請確定您再次停用WebDAV。

## 使用cURL啟用CRXDE Lite {#enabling-crxde-lite-curl}

您也可以執行此命令，透過cURL啟用CRXDE Lite：

```shell
curl -u admin:admin -F "jcr:primaryType=sling:OsgiConfig" -F "alias=/crx/server" -F "dav.create-absolute-uri=true" -F "dav.create-absolute-uri@TypeHint=Boolean" http://localhost:4502/apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
```

## 其他資源 {#other-resources}

如需AEM 6安全性功能的詳細資訊，請參閱下列頁面：

* [AEM安全性檢查清單](/help/sites-administering/security-checklist.md)
* [以生產就緒模式執行AEM](/help/sites-administering/production-ready.md)
