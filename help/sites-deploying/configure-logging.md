---
title: 記錄
seo-title: Logging
description: 了解如何為中央記錄服務配置全域參數、個別服務的特定設定，或如何請求資料記錄。
seo-description: Learn how to configure global parameters for the central logging service, specific settings for the individual services or how to request data logging.
uuid: 8c9e3628-2f2c-445d-9706-5c7725b85fe2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5aa69b10-2cd0-4d34-8104-8c3b88405926
feature: Configuring
exl-id: b32001a1-0078-43f6-89d6-781d6d2e9c94
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# 記錄{#logging}

AEM可讓您設定：

* 中央記錄服務的全局參數
* 要求資料記錄；要求資訊的專用記錄設定
* 個別服務的特定設定；例如，日誌消息的單個日誌檔案和格式

這些都是 [OSGi配置](/help/sites-deploying/configuring-osgi.md).

>[!NOTE]
>
>登入AEM是根據Sling原則。 請參閱 [Sling記錄](https://sling.apache.org/site/logging.html) 以取得更多資訊。

## 全域記錄 {#global-logging}

[Apache Sling記錄設定](/help/sites-deploying/osgi-configuration-settings.md) 用於配置根記錄器。 這會定義登入AEM的全域設定：

* 記錄級別
* 中央日誌檔案的位置
* 要保留的版本數
* 版本輪換；最大大小或時間間隔
* 寫入日誌消息時要使用的格式

>[!NOTE]
>
>此 [知識庫文章](https://helpx.adobe.com/experience-manager/kb/HowToRotateRequestAndAccessLog.html) 說明如何旋轉request.log和access.log檔案。

## 個人服務的記錄器和撰寫器 {#loggers-and-writers-for-individual-services}

除了全域記錄設定外，AEM還可讓您設定個別服務的特定設定：

* 特定記錄級別
* 個別記錄檔的位置
* 要保留的版本數
* 版本輪換；最大大小或時間間隔
* 寫入日誌消息時要使用的格式
* 記錄器（提供記錄消息的OSGi服務）

這可讓您將單一服務的記錄訊息通道至個別檔案。 這在開發或測試時特別有用；例如，當您需要為特定服務增加日誌級別時。

AEM使用下列方式將記錄訊息寫入檔案：

1. 安 **OSGi服務** （記錄器）寫入日誌消息。
1. A **記錄器** 根據您的規範擷取此訊息並格式化。
1. A **記錄寫入程式** 將所有這些消息寫入已定義的物理檔案。

這些元素會透過下列參數連結至適當的元素：

* **記錄器（記錄器）**

   定義產生訊息的服務。

* **記錄檔（記錄檔）**

   定義用於儲存日誌消息的物理檔案。

   這用於將記錄器與記錄寫入器連結。 該值必須與要建立連接的日誌記錄寫入器配置中的相同參數相同。

* **日誌檔案（日誌寫入器）**

   定義將寫入日誌消息的物理檔案。

   這必須與記錄寫入程式配置中的相同參數相同，否則不會進行匹配。 如果沒有匹配項，則將使用預設配置（每日日誌旋轉）建立隱式寫入器。

### 標準記錄器和撰寫器 {#standard-loggers-and-writers}

標準AEM安裝中包含某些記錄器和寫入程式。

第一個是特殊情況，因為它可控制 `request.log` 和 `access.log` 檔案：

* 記錄器：

   * Apache Sling Customized Request Data Logger

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * 將有關請求內容的消息寫入 `request.log`.

* 連結至：

   * Apache Sling Request Logger

      (org.apache.sling.engine.impl.log.RequestLogger)

   * 將消息寫入 `request.log` 或 `access.log`.

雖然標準配置適用於大多數安裝，但您仍可視需要自定義這些配置。

其他配對會遵循標準設定：

* 記錄器：

   * Apache Sling Logging Logger Configuration

      (org.apache.sling.commons.log.LogManager.factory.config)

   * 寫入 `Information` 訊息 `logs/error.log`.

* Writer連結：

   * Apache Sling Logging Writer設定

      (org.apache.sling.commons.log.LogManager.factory.writer)

* 記錄器：

   * Apache Sling Logging Logger Configuration(org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * 寫入 `Warning` 訊息 `../logs/error.log` 服務 `org.apache.pdfbox`.

* 不連結到特定寫入程式，因此將建立並使用帶有預設配置的隱式寫入程式（每日日誌輪轉）。

### 建立您自己的記錄器和作者 {#creating-your-own-loggers-and-writers}

您可以定義自己的記錄器/寫入器組：

1. 建立工廠配置的新實例 [Apache Sling Logging Logger Configuration](/help/sites-deploying/osgi-configuration-settings.md).

   1. 指定日誌檔案。
   1. 指定記錄器。
   1. 視需要設定其他參數。

1. 建立工廠配置的新實例 [Apache Sling Logging Writer設定](/help/sites-deploying/osgi-configuration-settings.md).

   1. 指定日誌檔案 — 此檔案必須與為記錄器指定的檔案匹配。
   1. 視需要設定其他參數。

>[!NOTE]
>
>在特定情況下，您可能想要建立 [自訂記錄檔](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).
