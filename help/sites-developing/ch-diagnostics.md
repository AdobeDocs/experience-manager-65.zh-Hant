---
title: ContextHub 診斷
seo-title: ContextHub Diagnostics
description: ContextHub提供診斷頁面，您可在其中查看ContextHub架構的概觀
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

ContextHub提供診斷頁面，您可在其中查看ContextHub架構的概觀。 若要開啟頁面，請前往 `contexthub.diagnostics.html` AEM author例項的頁面，例如：

`http://<host>:<port>/conf/<tenant>/settings/cloudsettings/default/contexthub.diagnostics.html`

「ContextHub診斷」頁提供了有關已建立的儲存和UI模組、已載入的客戶端庫資料夾以及指向有用頁的連結的資訊。

>[!NOTE]
>
>要返回診斷資訊，必須啟用調試模式，否則診斷頁將為空。 請參閱 [此文檔](ch-configuring.md#debugging-contexthub) 以取得如何啟用偵錯模式的詳細資訊。

>[!NOTE]
>
>若ContextHub設定仍位於其舊有路徑下，則診斷頁面的位置為 `http://<host>:<port>/libs/settings/cloudsettings/legacy/contexthub.diagnostics.html`.

## 商店 {#stores}

「儲存」區段會列出所有已設定的ContextHub儲存。 清單中的每個項目都包含下列資訊：

* **標題：** 此 [儲存類型](/help/sites-developing/ch-samplestores.md) 店的基礎。
* **路徑：** 保存配置的儲存庫節點的路徑。
* **resourceType:** 定義儲存類型的儲存庫節點的路徑。
* **clientlibs:** 載入的用戶端程式庫類別，用於實作儲存類型。

## 模組 {#modules}

「模組」區段會列出所有已設定的ContextHub UI模組。 清單中的每個項目都包含下列資訊：

* **標題：** 此 [UI模組類型](/help/sites-developing/ch-samplemodules.md) UI模組所依據之資訊。
* **路徑：** 保存配置的儲存庫節點的路徑。
* **resourceType:** 定義UI模組類型的儲存庫節點路徑。
* **clientlibs:** 載入並實作UI模組類型的用戶端程式庫的類別。

## Clientlibs {#clientlibs}

Clientlibs區段會列出ContextHub已載入的所有用戶端程式庫資料夾。 用戶端程式庫會分類：

* **kernel.js:** 實作ContextHub架構、區段引擎和儲存類型的用戶端程式庫。
* **ui.js:** 實作ContextHub UI和UI模組類型的用戶端程式庫。
* **style.css:** 從用戶端程式庫載入的CSS檔案。

## URL {#urls}

「URL」區段包含ContextHub功能的連結：

* **配置編輯器：** 開啟 [「ContextHub配置」頁](ch-configuring.md) 您可以在此設定商店、UI模式和UI模組。

* **ContextHub模組的設定：** 開啟/etc/cloudsettings/default/contexthub.config.kernel.js檔案，該檔案包含ContextHub存放區設定的Javascript物件表示。
* **ContextHub UI的設定：** 開啟/etc/cloudsettings/default/contexthub.config.ui.js檔案，其中包含ContextHub UI模式設定的Javascript物件表示。
* **kernel.js:** 開啟/etc/cloudsettings/default/contexthub.kernel.js檔案，其中包含實作ContextHub架構、區段引擎和儲存類型之用戶端程式庫的原始碼。
* **ui.js:** 開啟/etc/cloudsettings/default/contexthub.ui.js檔案，其中包含實作ContextHub UI和UI模組類型之用戶端程式庫的原始碼。
* **style.css:** 開啟/etc/cloudsettings/default/contexthub.styles.css檔案，其中包含ContextHub UI和UI模組的CSS樣式。
