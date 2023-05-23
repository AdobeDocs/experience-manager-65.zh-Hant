---
title: 安裝和配置文檔安全伺服器
seo-title: Installing and configuring the document security server
description: 使用文檔安全性可安全分發您以支援格式保存的任何資訊。 只有授權用戶才能訪問受保護的文檔。
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

使用文檔安全性可安全分發您以支援格式保存的任何資訊。 只有授權用戶才能訪問受保護的文檔。

Adobe Experience Manager Forms文檔安全性確保只有授權用戶才能使用您的文檔。 使用文檔安全性，您可以安全地分發以支援格式保存的任何資訊。 支援的檔案格式包括Adobe可移植文檔格式(PDF)和MicrosoftWord、Excel和PowerPoint檔案。

可以使用策略保護文檔。 在策略中指定的機密性設定決定了收件人如何使用您應用策略的文檔。 例如，您可以指定收件人是否可以打印或複製文本、編輯文本，或向受保護文檔添加簽名和注釋。

策略儲存在Document Security伺服器上；通過客戶端應用程式將策略應用於文檔。 將策略應用於文檔時，策略中指定的機密性設定會保護文檔包含的資訊。 您可以將受策略保護的文檔分發給受策略授權的收件人。

文檔安全性還提供客戶端、查看器和索引器以保護文檔、查看受保護的文檔和索引受保護的文檔。 有關文檔安全性的詳細資訊，請參見 [關於文檔安全性](/help/forms/using/admin-help/document-security.md)。

## 部署拓撲  {#deployment-topology}

文檔安全功能僅在JEE上的AEM Forms提供。 您需要JEE上的單個AEM Forms實例。 如有必要，您還可以建立AEM Forms伺服器的群集或伺服器場。 以下拓撲是運行文檔安全功能的指示拓撲。 有關拓撲的詳細資訊，請參見 [用於AEM Forms的體系結構和部署拓撲](aem-forms-architecture-deployment.md)。

<!--fix above link-->

![](do-not-localize/document-security-server_topology.png)

下圖顯示了AEM Forms文檔安全的典型體系結構：

![](do-not-localize/document-security-typical-environment.png)

## 在JEE上安裝AEM Forms {#installing-aem-forms-on-jee}

執行以下步驟以在JEE上安裝和配置AEM Forms:

1. 從AEM下載JEE安裝程式上的6.5Forms [Adobe許可網站(LWS)](https://licensing.adobe.com/)。 下載安裝程式需要有效的維護和支援合同。
1. 閱讀 [AEM FormsJEE支援平台文檔](/help/forms/using/aem-forms-jee-supported-platforms.md) 並確保軟體、硬體、作業系統、應用程式伺服器、資料庫、JDK和其他基礎架構已準備好在JEE上安裝AEM Forms。
1. （僅限非交鑰匙安裝）閱讀 [準備安裝AEM Forms單伺服器](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64) 或 [準備安裝AEM Forms伺服器群集](https://www.adobe.com/go/learn_aemforms_prepareInstallcluster_64) 並準備好在JEE上安裝和配置AEM Forms。
1. 根據您的環境和應用程式伺服器，選擇以下文檔之一併按照說明完成安裝

   * [使用JBoss全包在JEE上安裝和部署AEM Forms](https://www.adobe.com/go/learn_aemforms_installTurnkey_64)
   * [在JEE上安裝和部署JBoss的AEM Forms](https://www.adobe.com/go/learn_aemforms_installJBoss_64)
   * [在用於WebLogic的JEE上安裝和部署AEM Forms](https://www.adobe.com/go/learn_aemforms_installWebLogic_64)
   * [在JEE上安裝和部署WebSphere的AEM Forms](https://www.adobe.com/go/learn_aemforms_installWebSphere_64)
   * [在JBoss群集上的JEE上配置AEM Forms](https://www.adobe.com/go/learn_aemforms_clusterJBoss_64)
   * [在WebLogic群集上的JEE上配置AEM Forms](https://www.adobe.com/go/learn_aemforms_clusterWebLogic_64)
   * [在WebSphere群集上的JEE上配置AEM Forms](https://www.adobe.com/go/learn_aemforms_clusterWebSphere_64)

   >[!NOTE]
   >
   >在JEE配置管理器上AEM Forms的「模組選擇」螢幕上，選擇「文檔安全」選項。 「文檔安全性」選項不需要選擇任何其他模組。

## 後續步驟 {#next-steps}

* [配置客戶端和伺服器選項](/help/forms/using/admin-help/configuring-client-server-options.md)
* [建立和管理策略](/help/forms/using/admin-help/creating-policies.md)
* [建立和管理策略集](/help/forms/using/admin-help/creating-policy-sets.md)
