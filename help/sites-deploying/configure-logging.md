---
title: 記錄
seo-title: Logging
description: 瞭解如何配置中央日誌記錄服務的全局參數、單個服務的特定設定或如何請求資料記錄。
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

提AEM供了配置：

* 中央日誌記錄服務的全局參數
* 請求資料記錄；請求資訊的專用日誌記錄配置
* 具體設定；例如，日誌消息的單個日誌檔案和格式

這些都是 [OSGi配置](/help/sites-deploying/configuring-osgi.md)。

>[!NOTE]
>
>登錄AEM基於Sling原則。 請參閱 [Sling日誌記錄](https://sling.apache.org/site/logging.html) 的上界。

## 全局日誌記錄 {#global-logging}

[Apache Sling日誌記錄配置](/help/sites-deploying/osgi-configuration-settings.md) 用於配置根記錄器。 這定義了登錄的全局設定AEM:

* 記錄級別
* 中央日誌檔案的位置
* 要保留的版本數
* 版本旋轉；最大大小或時間間隔
* 寫入日誌消息時使用的格式

>[!NOTE]
>
>此 [知識庫文章](https://helpx.adobe.com/experience-manager/kb/HowToRotateRequestAndAccessLog.html) 介紹如何旋轉request.log和access.log檔案。

## 個人服務的伐木者和作家 {#loggers-and-writers-for-individual-services}

除了全局日誌記錄設定AEM外，還允許您為單個服務配置特定設定：

* 特定日誌級別
* 單個日誌檔案的位置
* 要保留的版本數
* 版本旋轉；最大大小或時間間隔
* 寫入日誌消息時使用的格式
* 記錄器（提供日誌消息的OSGi服務）

這允許您將單個服務的日誌消息傳送到單獨的檔案中。 這在開發或測試中特別有用；例如，當您需要為特定服務增加日誌級別時。

使AEM用以下方法將日誌消息寫入檔案：

1. 安 **OSGi服務** （記錄器）寫入日誌消息。
1. A **日誌記錄器** 根據您的規範獲取並格式化此消息。
1. A **日誌記錄寫入程式** 將所有這些消息寫入您定義的物理檔案。

這些元素通過以下相應元素的參數連結：

* **記錄器（記錄器）**

   定義生成消息的服務。

* **日誌檔案（記錄記錄程式）**

   定義用於儲存日誌消息的物理檔案。

   這用於將日誌記錄器與日誌記錄寫入器連結。 該值必須與要建立連接的日誌記錄寫入器配置中的相同參數相同。

* **日誌檔案（日誌記錄寫入程式）**

   定義日誌消息將寫入的物理檔案。

   這必須與日誌記錄寫入程式配置中的相同參數相同，否則不會進行匹配。 如果沒有匹配項，將使用預設配置（每日日誌輪替）建立隱式編寫器。

### 標準伐木工和作者 {#standard-loggers-and-writers}

某些記錄程式和寫入程式包含在標準AEM安裝中。

第一個是特殊情況，因為它控制 `request.log` 和 `access.log` 檔案：

* 記錄器：

   * Apache Sling可自定義請求資料記錄器

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * 將有關請求內容的消息寫入 `request.log`。

* 連結至：

   * Apache Sling請求記錄器

      (org.apache.sling.engine.impl.log.RequestLogger)

   * 將消息寫入 `request.log` 或 `access.log`。

如果需要，可以自定義這些配置，但標準配置適用於大多數安裝。

其他對遵循標準配置：

* 記錄器：

   * Apache Sling日誌記錄器配置

      (org.apache.sling.commons.log.LogManager.factory.config)

   * 寫入 `Information` 消息 `logs/error.log`。

* 指向編寫器的連結：

   * Apache Sling日誌記錄寫入程式配置

      (org.apache.sling.commons.log.LogManager.factory.writer)

* 記錄器：

   * Apache Sling日誌記錄記錄器配置(org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * 寫入 `Warning` 消息 `../logs/error.log` 服務 `org.apache.pdfbox`。

* 不連結到特定寫入程式，因此將建立並使用預設配置（每日日誌輪替）的隱式寫入程式。

### 建立您自己的伐木工和作者 {#creating-your-own-loggers-and-writers}

您可以定義自己的記錄器/寫入器對：

1. 建立工廠配置的新實例 [Apache Sling日誌記錄器配置](/help/sites-deploying/osgi-configuration-settings.md)。

   1. 指定日誌檔案。
   1. 指定記錄器。
   1. 根據需要配置其他參數。

1. 建立工廠配置的新實例 [Apache Sling日誌記錄寫入程式配置](/help/sites-deploying/osgi-configuration-settings.md)。

   1. 指定日誌檔案 — 必須與為記錄器指定的檔案匹配。
   1. 根據需要配置其他參數。

>[!NOTE]
>
>在某些情況下，您可能要建立 [自定義日誌檔案](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file)。
