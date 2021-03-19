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
feature: 設定
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---


# 記錄{#logging}

AEM提供您設定：

* 中央記錄服務的全局參數
* 要求資料記錄；要求資訊的專用記錄設定
* 個別服務的特定設定；例如，日誌消息的單個日誌檔案和格式

這些都是[OSGi配置](/help/sites-deploying/configuring-osgi.md)。

>[!NOTE]
>
>登入是AEM以Sling原則為基礎。 如需詳細資訊，請參閱[Sling Logging](https://sling.apache.org/site/logging.html)。

## 全局記錄{#global-logging}

[Apache Sling Logging ](/help/sites-deploying/osgi-configuration-settings.md) Configurationis used to configure the root logger.這定義了登入的全域設定AEM:

* 記錄級別
* 中央日誌檔案的位置
* 要保存的版本數
* 版本輪換；最大大小或時間間隔
* 寫入日誌消息時使用的格式

>[!NOTE]
>
>此[知識庫文章](https://helpx.adobe.com/experience-manager/kb/HowToRotateRequestAndAccessLog.html)說明如何旋轉request.log和access.log檔案。

## 個別服務的記錄員和寫入者{#loggers-and-writers-for-individual-services}

除了全域記錄設定外，還AEM允許您為個別服務配置特定設定：

* 特定記錄級別
* 單個日誌檔案的位置
* 要保存的版本數
* 版本輪換；最大大小或時間間隔
* 寫入日誌消息時使用的格式
* the logger(the OSGi service suppliding the log messages)

這可讓您將單一服務的記錄訊息傳送至個別檔案。 這在開發或測試時特別有用；例如，當您需要特定服務的日誌級別提高時。

使AEM用下列方法將日誌消息寫入檔案：

1. **OSGi服務**（記錄器）寫入日誌消息。
1. **Logging Logger**&#x200B;會擷取此訊息，並根據您的規格設定其格式。
1. **記錄寫入器**&#x200B;將所有這些消息寫入已定義的物理檔案。

這些元素會依下列參數連結至適當的元素：

* **Logger(Logging Logger)**

   定義生成消息的服務。

* **記錄檔（記錄檔）**

   定義用於儲存日誌消息的物理檔案。

   This is used to link a Logging Logger with a Logging Writer. 該值必須與要建立的連接的記錄寫入器配置中的相同參數相同。

* **日誌檔案（記錄寫入器）**

   定義日誌消息將寫入的物理檔案。

   此參數必須與記錄寫入器配置中的相同參數相同，否則不會進行匹配。 如果沒有匹配項，則將使用預設配置（每日日誌旋轉）建立隱式寫入器。

### 標準記錄程式和寫入程式{#standard-loggers-and-writers}

標準安裝中包含某些記錄程式和寫AEM入程式。

第一個是特殊情況，因為它同時控制`request.log`和`access.log`檔案：

* The Logger:

   * Apache Sling Customized Request Data Logger

      (org.apache.sling.engine.impl.log.RequestLoggerService)

   * 將有關請求內容的消息寫入`request.log`。

* 連結至：

   * Apache Sling Request Logger

      (org.apache.sling.engine.impl.log.RequestLogger)

   * 將消息寫入`request.log`或`access.log`。

如果需要，可自訂這些設定，但標準組態適合大部分安裝。

其他配對遵循標準配置：

* The Logger:

   * Apache Sling Logging Logger Configuration

      (org.apache.sling.commons.log.LogManager.factory.config)

   * 將`Information`消息寫入`logs/error.log`。

* Links to the Writer:

   * Apache Sling Logging Writer Configuration

      (org.apache.sling.commons.log.LogManager.factory.writer)

* The Logger:

   * Apache Sling Logging Logger Configuration
(org.apache.sling.commons.log.LogManager.factory.config.649d51b7-6425-45c9-81e6-2697a03d6be7)

   * 將`Warning`消息寫入`../logs/error.log`服務`org.apache.pdfbox`。

* 不連結到特定寫入器，因此將建立並使用具有預設配置的隱式寫入器（每日日誌旋轉）。

### 建立您自己的記錄程式和寫入程式{#creating-your-own-loggers-and-writers}

您可以定義自己的記錄器／寫入器對：

1. 建立Factory Configuration [Apache Sling Logging Logger Configuration](/help/sites-deploying/osgi-configuration-settings.md)的新例項。

   1. 指定「記錄檔」。
   1. 指定記錄器。
   1. 視需要設定其他參數。

1. 建立Factory Configuration [Apache Sling Logging Writer Configuration](/help/sites-deploying/osgi-configuration-settings.md)的新例項。

   1. 指定Log File - this must match that specified for the Logger.
   1. 視需要設定其他參數。

>[!NOTE]
>
>在某些情況下，您可能希望建立[自定義日誌檔案](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file)。

