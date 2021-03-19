---
title: 設定啟用功能
seo-title: 設定啟用功能
description: 在社群中設定啟用功能
seo-description: 在社群中設定啟用功能
uuid: 27be3128-1a7d-412e-99a9-6e3b3b0aec1c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 765a3d9b-4552-403e-872c-fdf684ac271d
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 1%

---


# 設定啟用功能{#configuring-enablement-features}

## 概覽 {#overview}

啟用功能提供建立[啟用社群](overview.md#enablement-community)的能力。

* 此功能需要額外的授權才能用於生產環境。

使用啟用功能需要：

安裝：

* **SCORM**

   可共用內容物件參考模型(SCORM)是數位學習的標準與規格集合。 SCORM也定義如何將內容封裝在可轉讓的ZIP檔案中。

* **MySQL**

   MySQL是關係型資料庫，主要用於SCORM追蹤和報告資料以用於「啟用」，以及用於追蹤視訊進度的表格。 用於啟用功能包的SCORM需要MySQL JDBC驅動程式。

* **FFmpeg**

   FFmpeg是轉換和串流音訊和視訊的解決方案，當安裝時，會用來正確轉碼[視訊資產](../../help/sites-authoring/default-components-foundation.md#video)。 對於啟用社群，它會用於作者環境，以取得已上傳資源的中繼資料，並產生縮圖以在列出資源時顯示。

設定：

* **社群管理員**

   對於啟用社群，只能將`Community Enablement Managers`使用者群組的成員指派為`Community Site Enablement Manager`的角色，其權限可能包括在發佈環境中建立內容、指派和成員管理。

可選配置：

* **Adobe Analytics**

   與Adobe Analytics的整合新增了完整的報告功能，並支援Analytics的視訊心率新增功能。

* **Dispatcher**

## 配置步驟{#configuration-steps}

以下是啟用社群的必要步驟。

每個步驟都會連結至提供必要詳細資訊的檔案。

**在所有作者／發佈例項上：**

1. **[安裝MySQL的JDBC驅動程式](deploy-communities.md#jdbc-driver-for-mysql)**

   使用Web Console（捆綁包）:*http://localhost:4502/system/console/bundles*

   安裝&#x200B;*before*&#x200B;安裝SCORM軟體包

1. **[安裝SCORM套件](deploy-communities.md#scorm-package)**


   使用包管理器：*http://localhost:4502/crx/packmgr/*

**在任何伺服器上：**

1. **[安裝MySQL、MySQL Workbench](mysql.md)**

1. **[安裝MySQL資料庫](mysql.md#database-setup)**

   執行從作者實例下載的SQL指令碼

   使用MySQL工作台

**在裝載作者例項的相同伺服器上：**

1. **[安裝FFmpeg](ffmpeg.md)**

**在所有作者／發佈例項上：**

1. **[配置JDBC連接池](mysql.md#configure-jdbc-connections)**

   使用Web控制台(configMgr):*http://localhost:4502/system/console/configMgr*

1. **[設定SCORM引擎服務](mysql.md#aem-communities-scormengine-service)**

   使用Web控制台(configMgr):*http://localhost:4502/system/console/configMgr*

1. **[設定CSRF篩選器](mysql.md#adobe-granite-csrf-filter)**

   使用Web控制台(configMgr):*http://localhost:4502/system/console/configMgr*

**在作者實例上：**

1. （*可選*）**[設定Analytics服務](analytics.md)**

   使用工具、部署、Cloud Services控制台：*http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[設定FFmpeg](ffmpeg.md#configure-ffmpeg-transcoding-service)**

   使用工作流程／模型控制台

1. **[啟用隧道服務](deploy-communities.md#tunnel-service-on-author)**

   使用Web控制台(configMgr):*http://localhost:4502/system/console/configMgr*

1. **[建立社群管理員](users.md#creating-community-members)**

   對於作者環境，請使用classic-UI安全控制台：*http://localhost:4502/useradmin*

   使用路徑= /home/users/community建立使用者

   * 將成員添加到以下組：

      * 社群支援經理
      * 社群管理員

## Dispatcher {#dispatcher}

當部署包含[AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)時，為了使啟用功能正常運作，`clientheader`和`filter`區段需要修改。 請參閱[配置Dispatcher for Communities](dispatcher.md#enablement)。
