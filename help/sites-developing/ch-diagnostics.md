---
title: ContextHub 診斷
seo-title: ContextHub Diagnostics
description: ContextHub提供診斷頁，在該頁中可以查看ContextHub框架的概述
seo-description: ContextHub provides a diagnostics page where you can see an overview of the ContextHub framework
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: b833c28b-76c6-42a2-b690-3e81ddf91bc2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 1%

---

# ContextHub 診斷 {#contexthub-diagnostics}

ContextHub提供診斷頁，在該頁中可以查看ContextHub框架的概述。 要開啟頁面，請轉到 `contexthub.diagnostics.html` 例AEM如：

`http://<host>:<port>/conf/<tenant>/settings/cloudsettings/default/contexthub.diagnostics.html`

「ContextHub診斷」頁提供有關已建立的儲存和UI模組、已載入的客戶端庫資料夾以及到有用頁面的連結的資訊。

>[!NOTE]
>
>要返回診斷資訊，必須啟用調試模式，否則診斷頁將為空。 請參閱 [此文檔](ch-configuring.md#debugging-contexthub) 的子菜單。

>[!NOTE]
>
>對於仍位於其舊路徑下的ContextHub配置，診斷頁的位置為 `http://<host>:<port>/libs/settings/cloudsettings/legacy/contexthub.diagnostics.html`。

## 商店 {#stores}

「儲存」部分列出已配置的所有ContextHub儲存。 清單中的每個項目都包含以下資訊：

* **標題：** 的 [儲存類型](/help/sites-developing/ch-samplestores.md) 店裡的基礎。
* **路徑：** 保存配置的儲存庫節點的路徑。
* **resourceType:** 定義儲存類型的儲存庫節點的路徑。
* **客戶端：** 載入的實現儲存類型的客戶端庫的類別。

## 模組 {#modules}

「模組」部分列出了已配置的所有ContextHub UI模組。 清單中的每個項目都包含以下資訊：

* **標題：** 的 [UI模組類型](/help/sites-developing/ch-samplemodules.md) UI模組所基於的。
* **路徑：** 保存配置的儲存庫節點的路徑。
* **resourceType:** 定義UI模組類型的儲存庫節點的路徑。
* **客戶端：** 載入的實現UI模組類型的客戶端庫的類別。

## Clientlibs {#clientlibs}

「客戶端庫」部分列出了ContextHub已載入的所有客戶端庫資料夾。 客戶端庫被分類：

* **kernel.js:** 實現ContextHub框架、段引擎和儲存類型的客戶端庫。
* **ui.js:** 實現ContextHub UI和UI模組類型的客戶端庫。
* **樣式.css:** 從客戶端庫載入的CSS檔案。

## URL {#urls}

URL節包含指向ContextHub功能的連結：

* **配置編輯器：** 開啟 [「上下文中心配置」頁](ch-configuring.md) 可在其中配置儲存、UI模式和UI模組。

* **ContextHub模組的配置：** 開啟/etc/cloudsettings/default/contexthub.config.kernel.js檔案，該檔案包含ContextHub儲存配置的Javascript對象表示。
* **ContextHub UI的配置：** 開啟/etc/cloudsettings/default/contexthub.config.ui.js檔案，該檔案包含ContextHub UI模式配置的Javascript對象表示。
* **kernel.js:** 開啟/etc/cloudsettings/default/contexthub.kernel.js檔案，該檔案包含實現ContextHub框架、段引擎和儲存類型的客戶端庫的原始碼。
* **ui.js:** 開啟/etc/cloudsettings/default/contexthub.ui.js檔案，該檔案包含實現ContextHub UI和UI模組類型的客戶端庫的原始碼。
* **樣式.css:** 開啟/etc/cloudsettings/default/contexthub.styles.css檔案，該檔案包含ContextHub UI和UI模組的CSS樣式。
