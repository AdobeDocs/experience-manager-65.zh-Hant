---
title: 安裝和設定Document Security伺服器
seo-title: 安裝和設定Document Security伺服器
description: '使用檔案安全性，安全地散布您以支援格式儲存的任何資訊。 只有授權的使用者才能存取受保護的檔案。 '
seo-description: '使用檔案安全性，安全地散布您以支援格式儲存的任何資訊。 只有授權的使用者才能存取受保護的檔案。 '
uuid: 04c67a84-01ad-45b7-a590-822b1c067d52
contentOwner: khsingh
discoiquuid: 600d13e7-6655-41c5-aab4-c8e9e2a8d14f
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---


# 安裝和配置Document Security Server {#installing-and-configuring-the-document-security-server}

使用檔案安全性，安全地散布您以支援格式儲存的任何資訊。 只有授權的使用者才能存取受保護的檔案。

Adobe Experience Manager Forms檔案安全性可確保只有授權使用者才能使用您的檔案。 使用檔案安全性，您可以安全地散布您以支援格式儲存的任何資訊。 支援的檔案格式包括Adobe可攜式檔案格式(PDF)和Microsoft Word、Excel和PowerPoint檔案。

您可以使用原則來保護檔案。 您在原則中指定的機密設定會決定收件者如何使用您套用原則的檔案。 例如，您可以指定收件者是否可以列印或複製文字、編輯文字，或在受保護的檔案中新增簽名和留言。

這些原則會儲存在Document Security伺服器上；您可以透過用戶端應用程式將原則套用至檔案。 將原則套用至檔案時，原則中指定的機密設定會保護檔案所包含的資訊。 您可以將受原則保護的檔案分發給受原則授權的收件者。

檔案安全性也提供用戶端、檢視器和索引器，以保護檔案、檢視受保護的檔案，以及為受保護的檔案建立索引。 如需檔案安全性的詳細資訊，請參閱[關於檔案安全性](/help/forms/using/admin-help/document-security.md)。

## 部署拓撲{#deployment-topology}

檔案安全性功能僅適用於JEE的AEM Forms。 您需要JEE上的單一AEM Forms實例。 如有必要，您也可以建立一個群集或群集的AEM Forms伺服器。 以下拓撲是指示性拓撲，用於運行文檔安全功能。 有關拓撲的詳細資訊，請參見[AEM Forms](aem-forms-architecture-deployment.md)的體系結構和部署拓撲。

<!--fix above link-->

![](do-not-localize/document-security-server_topology.png)

下圖顯示了AEM FormsDocument Security的典型架構：

![](do-not-localize/document-security-typical-environment.png)

## 在JEE上安裝AEM Forms{#installing-aem-forms-on-jee}

在JEE上安裝和配置AEM Forms，請執行以下步驟：

1. 從&lt;AEMa0/>Adobe授權網站(LWS)](https://licensing.adobe.com/)下載JEE版6.5Forms安裝程式。 [您需要有效的維護與支援合約才能下載安裝程式。
1. 閱讀[AEM Forms的JEE支援的平台文檔](/help/forms/using/aem-forms-jee-supported-platforms.md)，並確保軟體、硬體、作業系統、應用程式伺服器、資料庫、JDK和其他基礎架構已準備好在JEE上安裝AEM Forms。
1. （僅限非交鑰匙安裝）閱讀[準備安裝AEM Forms單伺服器](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64)或[準備安裝AEM Forms伺服器群集](https://www.adobe.com/go/learn_aemforms_prepareInstallcluster_64)並準備讓您的環境在JEE上安裝和配置AEM Forms。
1. 根據您的環境和應用程式伺服器，選擇以下文檔之一併按照說明完成安裝

   * [在JEE上使用JBoss統包安裝和部署AEM Forms](https://www.adobe.com/go/learn_aemforms_installTurnkey_64)
   * [在JEE for JBoss上安裝和部署AEM Forms](https://www.adobe.com/go/learn_aemforms_installJBoss_64)
   * [在WebLogic的JEE上安裝和部署AEM Forms](https://www.adobe.com/go/learn_aemforms_installWebLogic_64)
   * [在JEE for WebSphere上安裝和部署AEM Forms](https://www.adobe.com/go/learn_aemforms_installWebSphere_64)
   * [在JBoss群集上配置JEE上的AEM Forms](https://www.adobe.com/go/learn_aemforms_clusterJBoss_64)
   * [在WebLogic群集上配置JEE上的AEM Forms](https://www.adobe.com/go/learn_aemforms_clusterWebLogic_64)
   * [在WebSphere群集上配置JEE上的AEM Forms](https://www.adobe.com/go/learn_aemforms_clusterWebSphere_64)

   >[!NOTE]
   >
   >在JEE配置管理器上AEM Forms的「模組選擇」螢幕上，選擇「Document Security」（文檔安全）選項。 「Document Security」(Document Security)選項不需要選取任何其他模組。

## 後續步驟{#next-steps}

* [配置客戶端和伺服器選項](/help/forms/using/admin-help/configuring-client-server-options.md)
* [建立和管理策略](/help/forms/using/admin-help/creating-policies.md)
* [建立和管理策略集](/help/forms/using/admin-help/creating-policy-sets.md)
