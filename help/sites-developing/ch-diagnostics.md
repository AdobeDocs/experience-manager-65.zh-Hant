---
title: ContextHub 診斷
description: ContextHub提供診斷頁面，您可在其中檢視ContextHub架構的概觀
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: b833c28b-76c6-42a2-b690-3e81ddf91bc2
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 1%

---

# ContextHub 診斷 {#contexthub-diagnostics}

ContextHub提供診斷頁面，您可在其中檢視ContextHub架構的概觀。 若要開啟頁面，請前往AEM作者執行個體的`contexthub.diagnostics.html`頁面，例如：

`http://<host>:<port>/conf/<tenant>/settings/cloudsettings/default/contexthub.diagnostics.html`

「ContextHub診斷」頁面提供有關已建立之存放區和UI模組、已載入的使用者端程式庫資料夾以及有用頁面連結的資訊。

>[!NOTE]
>
>為了傳回診斷資訊，必須啟用偵錯模式，否則診斷頁面將為空白。 如需如何啟用偵錯模式的詳細資訊，請參閱[此檔案](ch-configuring.md#debugging-contexthub)。

>[!NOTE]
>
>對於ContextHub設定仍位於其舊路徑下的情況，診斷頁面的位置是`http://<host>:<port>/libs/settings/cloudsettings/legacy/contexthub.diagnostics.html`。

## 商店 {#stores}

存放區區段會列出所有已設定的ContextHub存放區。 清單中的每個專案都包含下列資訊：

* **標題：**&#x200B;存放區所依據的[存放區型別](/help/sites-developing/ch-samplestores.md)。
* **路徑：**&#x200B;儲存設定的存放庫節點的路徑。
* **resourceType：**&#x200B;定義存放區型別的存放庫節點路徑。
* **clientlibs：**&#x200B;已載入且實作存放區型別之使用者端資料庫的類別。

## 模組 {#modules}

模組區段會列出所有已設定的ContextHub UI模組。 清單中的每個專案都包含下列資訊：

* **標題：** UI模組所依據的[UI模組型別](/help/sites-developing/ch-samplemodules.md)。
* **路徑：**&#x200B;儲存設定的存放庫節點的路徑。
* **resourceType：**&#x200B;定義UI模組型別的存放庫節點的路徑。
* **clientlibs：**&#x200B;已載入且實作UI模組型別之使用者端程式庫的類別。

## Clientlibs {#clientlibs}

「Clientlibs」區段會列出ContextHub已載入的所有使用者端程式庫資料夾。 使用者端程式庫會進行分類：

* **kernel.js：**&#x200B;實作ContextHub架構、區段引擎和存放區型別的使用者端資料庫。
* **ui.js：**&#x200B;實作ContextHub UI和UI模組型別的使用者端資料庫。
* **style.css：**&#x200B;從使用者端資料庫載入的CSS檔案。

## URL {#urls}

URL區段包含ContextHub功能的連結：

* **組態編輯器：**&#x200B;開啟[ContextHub組態頁面](ch-configuring.md)，您可以在其中設定存放區、UI模式和UI模組。

* **ContextHub模組的組態：**&#x200B;開啟/etc/cloudsettings/default/contexthub.config.kernel.js檔案，其中包含ContextHub存放區組態的JavaScript物件表示法。
* **ContextHub UI的設定：**&#x200B;開啟/etc/cloudsettings/default/contexthub.config.ui.js檔案，其中包含ContextHub UI模式設定的JavaScript物件表示。
* **kernel.js：**&#x200B;開啟/etc/cloudsettings/default/contexthub.kernel.js檔案，其中包含實作ContextHub架構、區段引擎和存放區型別的使用者端程式庫原始碼。
* **ui.js：**&#x200B;開啟/etc/cloudsettings/default/contexthub.ui.js檔案，其中包含實作ContextHub UI和UI模組型別的使用者端程式庫原始碼。
* **style.css：**&#x200B;開啟/etc/cloudsettings/default/contexthub.styles.css檔案，其中包含ContextHub UI和UI模組的CSS樣式。
