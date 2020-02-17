---
title: 啟動和停止服務
seo-title: 啟動和停止服務
description: 瞭解如何啟動和停止與AEM Forms模組以及應用程式伺服器和資料庫相關的服務。
seo-description: 瞭解如何啟動和停止與AEM Forms模組以及應用程式伺服器和資料庫相關的服務。
uuid: 8c831cb2-4165-4118-8a09-764cec4e5e05
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b93060bd-c6e1-40d2-8acd-ccafb8ed56da
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 啟動和停止服務 {#starting-and-stopping-services}

AEM表單包含兩種服務類型：

* 控制AEM表單應用程式伺服器和資料庫的服務。
* 控制AEM表單模組的服務

## 啟動或停止與AEM表單模組相關的服務 {#start-or-stop-the-services-associated-with-aem-forms-modules}

AEM表單模組（例如Forms、Rights Management、Output）會以服務的形式運作。 有時，您可能需要停止或啟動這些AEM表單模組的服務。 例如，您必須在變更服務的設定後停止並重新啟動AEM表單服務。

1. 在管理控制台中，按一 **下「服務** >應 **用程式與服務** > **服務管理**」。
1. 在「服務管理」頁面上，選擇服務旁的複選框以停止或啟動，然後按一下停止或啟動。

## 啟動或停止應用程式伺服器和資料庫的服務 {#start-or-stop-services-for-the-application-server-and-database}

AEM表單的完整實作包括應用程式伺服器和資料庫服務：

* *`[application server]`* for AEM forms
* *`[database]`* for AEM forms

在Windows上，可透過「管理工具 **>服務」面** 板存取 **這些服務**。 例如，如果您使用統包方法將AEM表單安裝在JBoss上，您的系統可使用下列服務：

* JBoss for Adobe Experience Manager表單
* MySQL for Adobe Experience Manager表單

從「服務」面板的清單中選取這些服務，然後按一下面板上的適當動作按鈕，即可啟動或停止這些服務。

在UNIX®或Linux上，從命令行輸入以下文本，其 *`[service name]`* 中是正在驗證的服務的名稱：

```as3
     ps -A | grep [service name]
```

