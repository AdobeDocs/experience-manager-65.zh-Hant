---
title: 記錄
seo-title: 記錄
description: 瞭解如何為中央記錄服務設定全域參數、個別服務的特定設定，或如何要求資料記錄。
seo-description: 瞭解如何為中央記錄服務設定全域參數、個別服務的特定設定，或如何要求資料記錄。
uuid: 8c9e3628-2f2c-445d-9706-5c7725b85fe2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5aa69b10-2cd0-4d34-8104-8c3b88405926
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 記錄{#logging}

AEM提供您設定：

* 中央記錄服務的全局參數
* 要求資料記錄；要求資訊的專用記錄設定
* 個別服務的特定設定；例如，日誌消息的單個日誌檔案和格式

這些都是 [OSGi配置](/help/sites-deploying/configuring-osgi.md)。

>[!NOTE]
>
>登入AEM是以Sling原則為基礎。 如需詳 [細資訊，請參閱Sling](https://sling.apache.org/site/logging.html) Logging。

## 全域記錄 {#global-logging}

[Apache Sling Logging Configuration](/help/sites-deploying/osgi-configuration-settings.md) is used to configure the root logger. 這會定義登入AEM的全域設定：

* 記錄級別
* 中央日誌檔案的位置
* 要保存的版本數
* 版本輪換；最大大小或時間間隔
* 寫入日誌消息時使用的格式

>[!NOTE]
>
>本知 [識庫文章](https://helpx.adobe.com/experience-manager/kb/HowToRotateRequestAndAccessLog.html) ，說明如何旋轉request.log和access.log檔案。

## 個人服務的記錄者和撰寫者 {#loggers-and-writers-for-individual-services}

除了全域記錄設定外，AEM還可讓您設定個別服務的特定設定：

* 特定記錄級別
* 單個日誌檔案的位置
* 要保存的版本數
* 版本輪換；最大大小或時間間隔
* 寫入日誌消息時使用的格式
* the logger(the OSGi service suppliding the log messages)

這可讓您將單一服務的記錄訊息傳送至個別檔案。 這在開發或測試時特別有用；例如，當您需要特定服務的日誌級別提高時。

AEM使用下列功能將記錄訊息寫入檔案：

1. An **OSGi service** (logger)writes a log message.
1. A **Logging Logger** takes this message and formats it according your specification.
1. 記 **錄寫入器** (Logging Writer)將所有這些消息寫入您定義的物理檔案。

這些元素會依下列參數連結至適當的元素：

* **Logger(Logging Logger)**

   定義生成消息的服務。

* **記錄檔（記錄檔）**

   定義用於儲存日誌消息的物理檔案。

   This is used to link a Logging Logger with a Logging Writer. 該值必須與要建立的連接的記錄寫入器配置中的相同參數相同。

* **日誌檔案（記錄寫入器）**

   定義日誌消息將寫入的物理檔案。

   此參數必須與記錄寫入器配置中的相同參數相同，否則不會進行匹配。 如果沒有匹配項，則將使用預設配置（每日日誌旋轉）建立隱式寫入器。

### 標準記錄工具和作者 {#standard-loggers-and-writers}

標準AEM安裝中包含某些記錄程式和撰寫程式。

第一個是特殊情況，因為它同時控制 `request.log` 和文 `access.log` 件：

* The Logger:

   * Apache Sling Customized Request Data Logger

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * 將請求內容的相關訊息寫入 `request.log`。

* 連結至：

   * Apache Sling Request Logger

      (org.apache.sling.engine.impl.log.RequestLogger)

   * 將消息寫入或 `request.log` 中 `access.log`。

如果需要，可自訂這些設定，但標準組態適合大部分安裝。

其他配對遵循標準配置：

* The Logger:

   * Apache Sling Logging Logger Configuration

      (org.apache.sling.commons.log.LogManager.factory.config)

   * 將消 `Information` 息寫入 `logs/error.log`。

* Links to the Writer:

   * Apache Sling Logging Writer Configuration

      (org.apache.sling.commons.log.LogManager.factory.writer)

* The Logger:

   * Apache Sling Logging Logger Configuration(org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * 將消 `Warning` 息寫入 `../logs/error.log` 服務的消息 `org.apache.pdfbox`。

* 不連結到特定寫入器，因此將建立並使用具有預設配置的隱式寫入器（每日日誌旋轉）。

### 建立您自己的記錄工具和作者 {#creating-your-own-loggers-and-writers}

您可以定義自己的記錄器／寫入器對：

1. 建立Factory Configuration [Apache Sling Logger Configuration的新例項](/help/sites-deploying/osgi-configuration-settings.md)。

   1. 指定「記錄檔」。
   1. 指定記錄器。
   1. 視需要設定其他參數。

1. 建立Factory Configuration [Apache Sling Logging Writer Configuration的新例項](/help/sites-deploying/osgi-configuration-settings.md)。

   1. 指定Log File - this must match that specified for the Logger.
   1. 視需要設定其他參數。

>[!NOTE]
>
>在某些情況下，您可能想要建立自 [訂記錄檔](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file)。

