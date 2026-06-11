---
title: 針對JEE上的AEM Forms，將JBoss EAP從7.4.10升級至7.4.23
description: 針對JEE獨立環境中的AEM Forms，將JBoss EAP從7.4.10升級至7.4.23的步驟。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
exl-id: 8f4c2a91-6b3d-4e7f-9c12-5d8e1f0a2b34
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms Upgrade,AEM Forms on JEE
role: User, Developer
source-git-commit: 652162941dd716ae797ce50709e91757dad99054
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 3%

---

# 針對JEE上的AEM Forms，將JBoss EAP從7.4.10升級至7.4.23 {#upgrade-jboss-eap-from-7-4-10-to-7-4-23}

## 概觀 {#overview}

在JEE獨立環境上的AEM Forms上，將JBoss EAP從7.4.10版升級至7.4.23版。 升級需要將組態檔、資料庫認證和CRX儲存區域移轉至新的JBoss安裝，並執行Configuration Manager以完成安裝。

## 套用至 {#applies-to}

本文適用於：

* 在獨立環境中於JBoss EAP 7.4.10上執行的JEE上的AEM Forms
* Windows和Linux上的Turnkey和Partial Turnkey安裝模式

>[!NOTE]
>
> 如果您要升級JBoss叢集環境，請先完成本文中的步驟，然後在[將JEE上的AEM Forms的JBoss EAP叢集從7.4.10升級為7.4.23 ](/help/forms/using/upgrade-jboss-eap-cluster-from-7-4-10-to-7-4-23.md)中執行其他步驟。

## 先決條件 {#prerequisites}

開始之前：

* 從[Adobe軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)下載JBoss 7.4.23套件。
* 確保您對目標環境具有管理存取權。
* 對現有JBoss安裝進行完整備份。

## 步驟 {#steps}

若要將JBoss EAP從7.4.10升級至7.4.23，請執行以下步驟：

### 下載並解壓縮JBoss {#download-and-extract-jboss}

1. 從Adobe軟體發佈入口網站下載JBoss 7.4.23 ZIP套件。
1. 將ZIP檔案解壓縮至本機目錄。
1. 重新命名擷取的JBoss資料夾，以符合現有JBoss安裝目錄的確切名稱。

### 備份現有的安裝 {#back-up-the-existing-installation}

1. 建立目前JBoss安裝目錄的完整備份。
1. 確認備份包含所有組態檔和自訂。

### 設定資料庫檔案 {#configure-database-files}

1. 導覽至組態目錄：

   * Windows： `<JBoss_Home>\standalone\configuration`
   * Linux： `<JBoss_Home>/standalone/configuration`

1. 根據您的安裝模式設定資料庫檔案：

   **立即可用模式：**

   1. 將`lc_mysql.xml`重新命名為`lc_turnkey.xml`。
   1. 刪除下列檔案：

      * `lc_oracle.xml`
      * `lc_mssql.xml`

   **部分立即可用模式：**

   1. 只保留與資料庫引擎相對應的`lc_db.xml`檔案。
   1. 刪除其他兩個`lc_db.xml`組態檔。

### 更新資料庫認證 {#update-database-credentials}

1. 從備份的JBoss安裝開啟`lc_turnkey.xml`檔案。
1. 複製下列值：

   * 資料來源URL
   * 資料庫使用者名稱
   * 資料庫密碼

1. 更新新`lc_turnkey.xml`檔案中對應的專案。

### 移轉CRX存放庫 {#migrate-crx-repository}

1. 導覽至舊版JBoss安裝中的下列目錄：

   `<old_jboss>\bin\`

1. 複製`crx-quickstart`資料夾。
1. 將資料夾貼入：

   `<new_jboss>\bin\`

### 執行Configuration Manager {#run-configuration-manager}

1. 啟動升級的JBoss環境。
1. 啟動LiveCycle Configuration Manager (LCM)。
1. 執行完整的端對端Configuration Manager工作流程
1. 確認所有組態工作都順利完成。

### 升級後驗證 {#post-upgrade-validation}

升級後，請確認下列專案：

* 所有服務都成功啟動。
* 已驗證資料庫連線。
* 應用程式功能已驗證。
