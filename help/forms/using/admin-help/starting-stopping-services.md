---
title: 啟動和停止服務
seo-title: Starting and stopping services
description: 瞭解如何啟動和停止與AEM Forms模組以及應用程式伺服器和資料庫相關的服務。
seo-description: Learn how to start and stop services associated with AEM Forms modules and the application server and database.
uuid: 8c831cb2-4165-4118-8a09-764cec4e5e05
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b93060bd-c6e1-40d2-8acd-ccafb8ed56da
exl-id: 55bf5196-22c6-4286-8c92-ff44d81dde49
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# 啟動和停止服務 {#starting-and-stopping-services}

有兩種服務屬於表單的一AEM部分：

* 控制Forms應用程式服AEM務器和資料庫的服務。
* 控制表單模AEM塊的服務

## 啟動或停止與表單模組關聯AEM的服務 {#start-or-stop-the-services-associated-with-aem-forms-modules}

表AEM單模組(例如，Forms、Rights Management、輸出)作為服務運行。 有時，您可能需要停止或啟動這些表單模AEM塊的服務。 例如，在更改服務設定後，必AEM須停止並重新啟動表單服務。

1. 在管理控制台中按一下 **服務** > **應用程式和服務** > **服務管理**。
1. 在「服務管理」頁上，選中要停止或啟動的服務旁邊的複選框，然後按一下停止或啟動。

## 啟動或停止應用程式伺服器和資料庫的服務 {#start-or-stop-services-for-the-application-server-and-database}

表單的完AEM整實現包括應用伺服器和資料庫服務：

* *`[application server]`* 表AEM單
* *`[database]`* 表AEM單

在Windows上，可通過 **管理工具** > **服務面板**。 例如，如果您使用AEM統包方法在JBoss上安裝了表單，則系統上提供以下服務：

* Adobe Experience Manager表格
* MySQL forAdobe Experience Manager表單

通過從「服務」面板的清單中選擇這些服務，然後按一下面板上的相應操作按鈕，啟動或停止這些服務。

在UNIX®或Linux上，從命令行輸入以下文本，其中 *`[service name]`* 是您正在驗證的服務的名稱：

```java
     ps -A | grep [service name]
```
