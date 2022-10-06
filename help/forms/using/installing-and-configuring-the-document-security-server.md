---
title: 安裝和配置文檔安全伺服器
seo-title: Installing and configuring the document security server
description: 使用文檔安全性來安全地分發您以支援的格式保存的任何資訊。 只有授權用戶才能訪問受保護的文檔。
seo-description: Use document security to safely distribute any information that you have saved in a supported format. Only authorized users can access protected documents.
uuid: 04c67a84-01ad-45b7-a590-822b1c067d52
contentOwner: khsingh
discoiquuid: 600d13e7-6655-41c5-aab4-c8e9e2a8d14f
role: Admin
exl-id: 4a4bad4a-3e68-43cb-b55c-03b509a5d304
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# 安裝和配置文檔安全伺服器 {#installing-and-configuring-the-document-security-server}

使用文檔安全性來安全地分發您以支援的格式保存的任何資訊。 只有授權用戶才能訪問受保護的文檔。

Adobe Experience Manager Forms檔案安全性可確保只有獲授權的使用者才能使用您的檔案。 使用文檔安全性，您可以安全地分發以支援格式保存的任何資訊。 支援的檔案格式包括Adobe可移植文檔格式(PDF)和Microsoft Word、Excel和PowerPoint檔案。

您可以使用策略保護文檔。 您在策略中指定的機密設定決定了收件人如何使用應用策略的文檔。 例如，您可以指定收件者是否可以打印或複製文本、編輯文本，或向受保護的文檔添加簽名和注釋。

策略儲存在Document Security伺服器上；通過客戶端應用程式將策略應用到文檔。 將策略應用於文檔時，策略中指定的機密設定將保護文檔包含的資訊。 您可以將受策略保護的文檔分發給受策略授權的收件人。

文檔安全性還提供了客戶端、查看器和索引器，以保護文檔、查看受保護的文檔以及為受保護的文檔編製索引。 有關文檔安全性的詳細資訊，請參見 [關於檔案安全性](/help/forms/using/admin-help/document-security.md).

## 部署拓撲  {#deployment-topology}

檔案安全性功能僅可在JEE上的AEM Forms中使用。 在JEE上需要單一AEM Forms例項。 您也可以視需要建立AEM Forms伺服器的叢集或伺服器陣列。 以下拓撲是運行文檔安全功能的指示性拓撲。 有關拓撲的詳細資訊，請參見 [適用於AEM Forms的架構和部署拓撲](aem-forms-architecture-deployment.md).

<!--fix above link-->

![](do-not-localize/document-security-server_topology.png)

下圖顯示AEM Forms檔案安全性的典型架構：

![](do-not-localize/document-security-typical-environment.png)

## 在JEE安裝AEM Forms {#installing-aem-forms-on-jee}

執行下列步驟以在JEE上安裝和設定AEM Forms:

1. 從下載AEM 6.5 Forms on JEE安裝程式 [Adobe授權網站(LWS)](https://licensing.adobe.com/). 您需要有效的維護和支援合同才能下載安裝程式。
1. 閱讀 [AEM Forms on JEE支援平台檔案](/help/forms/using/aem-forms-jee-supported-platforms.md) 並確保軟體、硬體、作業系統、應用程式伺服器、資料庫、JDK和其他基礎架構已準備好在JEE上安裝AEM Forms。
1. （僅非全包安裝）閱讀 [準備安裝AEM Forms單一伺服器](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64) 或 [準備安裝AEM Forms伺服器叢集](https://www.adobe.com/go/learn_aemforms_prepareInstallcluster_64) 並準備好您的環境，以在JEE上安裝和設定AEM Forms。
1. 根據您的環境和應用程式伺服器，選擇以下文檔之一，然後按照說明完成安裝

   * [使用JBoss統包在JEE上安裝和部署AEM Forms](https://www.adobe.com/go/learn_aemforms_installTurnkey_64)
   * [在JEE for JBoss上安裝和部署AEM Forms](https://www.adobe.com/go/learn_aemforms_installJBoss_64)
   * [在JEE for WebLogic上安裝和部署AEM Forms](https://www.adobe.com/go/learn_aemforms_installWebLogic_64)
   * [在JEE for WebSphere上安裝和部署AEM Forms](https://www.adobe.com/go/learn_aemforms_installWebSphere_64)
   * [在JBoss叢集上的JEE上設定AEM Forms](https://www.adobe.com/go/learn_aemforms_clusterJBoss_64)
   * [在WebLogic叢集上的JEE上設定AEM Forms](https://www.adobe.com/go/learn_aemforms_clusterWebLogic_64)
   * [在WebSphere叢集上的JEE上設定AEM Forms](https://www.adobe.com/go/learn_aemforms_clusterWebSphere_64)

   >[!NOTE]
   >
   >在JEE設定管理員上AEM Forms的「模組選取」畫面上，選取「檔案安全性」選項。 「文檔安全性」選項不要求選擇任何其他模組。

## 後續步驟 {#next-steps}

* [配置客戶端和伺服器選項](/help/forms/using/admin-help/configuring-client-server-options.md)
* [建立和管理策略](/help/forms/using/admin-help/creating-policies.md)
* [建立和管理策略集](/help/forms/using/admin-help/creating-policy-sets.md)
