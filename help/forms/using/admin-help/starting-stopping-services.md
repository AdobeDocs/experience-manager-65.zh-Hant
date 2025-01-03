---
title: 啟動和停止服務
description: 瞭解如何啟動和停止與AEM Forms模組、應用程式伺服器和資料庫關聯的服務。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 55bf5196-22c6-4286-8c92-ff44d81dde49
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# 啟動和停止服務 {#starting-and-stopping-services}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

AEM表單中有兩種型別的服務：

* 控制AEM表單應用程式伺服器和資料庫的服務。
* 控制AEM表單模組的服務

## 啟動或停止與AEM表單模組關聯的服務 {#start-or-stop-the-services-associated-with-aem-forms-modules}

AEM表單模組(例如Forms、Rights Management、輸出)可作為服務運作。 有時您可能需要停止或啟動這些AEM表單模組的服務。 例如，在變更服務的設定後，您必須停止並重新啟動AEM表單服務。

>[!NOTE]
>
> 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式）可能會導致AEM開發環境不一致。

1. 在管理主控台中，按一下&#x200B;**服務** > **應用程式及服務** > **服務管理**。
1. 在「服務管理」頁面中，選取要停止或啟動之服務旁的核取方塊，然後按一下停止或啟動。

## 啟動或停止應用程式伺服器和資料庫的服務 {#start-or-stop-services-for-the-application-server-and-database}

AEM表單的完整實作包括應用程式伺服器和資料庫服務：

* AEM表單的&#x200B;*`[application server]`*
* AEM表單的&#x200B;*`[database]`*

在Windows上，這些服務可透過&#x200B;**系統管理工具** > **服務面板**&#x200B;存取。 例如，如果您使用turnkey方法在JBoss上安裝AEM表單，則您的系統上可以使用以下服務：

* 適用於Adobe Experience Manager表單的JBoss
* 適用於Adobe Experience Manager的MySQL表單

從「服務」面板的清單中選取這些服務，然後按一下面板上的適當動作按鈕，即可啟動或停止這些服務。

在UNIX®或Linux上，從命令列輸入下列文字，其中&#x200B;*`[service name]`*&#x200B;是您正在驗證的服務名稱：

```java
     ps -A | grep [service name]
```
