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
translation-type: tm+mt
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---


# 設定啟用功能 {#configuring-enablement-features}

## 概覽 {#overview}

啟用功能提供建立啟用社群 [的能力](overview.md#enablement-community)。

* 此功能需要額外的授權才能用於生產環境。

使用啟用功能需要：

安裝：

* **SCORM**&#x200B;可分享內容物件參考模型(SCORM)是數位學習的標準與規格集合。 SCORM也定義如何將內容封裝在可轉讓的ZIP檔案中。

* **MySQL** MySQL是關係型資料庫，主要用於SCORM追蹤和報告資料以用於啟用，以及用於追蹤視訊進度的表格。 用於啟用功能包的SCORM需要MySQL JDBC驅動程式。

* **FFmpeg** FFmpeg是轉換和串流音訊和視訊的解決方案，安裝時會用來正確轉碼視訊 [資產](../../help/sites-authoring/default-components-foundation.md#video)。 對於啟用社群，它會用於作者環境，以取得已上傳資源的中繼資料，並產生縮圖以在列出資源時顯示。

設定：

* **社群管理**&#x200B;員對於啟用社群，只能指派使用者群組的成員角色 `Community Enablement Managers``Community Site Enablement Manager`，其權限可能包括內容建立、指派和發佈環境中的成員管理。

可選配置：

* **Adobe Analytics**&#x200B;與Adobe Analytics整合可新增完整的報表功能，並支援Analytics的視訊心率新增功能。

* **Dispatcher**

## 配置步驟 {#configuration-steps}

以下是啟用社群的必要步驟。

每個步驟都會連結至提供必要詳細資訊的檔案。

**在所有作者／發佈例項上：**

1. **[安裝MySQL的JDBC驅動程式](deploy-communities.md#jdbc-driver-for-mysql)**使用Web控制台（捆綁包）:*http://localhost:4502/system/console/bundles安*裝&#x200B;*SCORM套件之前*，請先安裝

1. **[安裝SCORM套件](deploy-communities.md#scorm-package)**使用套件管理員：*http://localhost:4502/crx/packmgr/*

**在任何伺服器上：**

1. **[安裝MySQL、MySQL Workbench](mysql.md)**

1. **[安裝MySQL資料庫](mysql.md#database-setup)**從作者實例下載的執行SQL指令碼使用MySQL Workbench

**在裝載作者例項的相同伺服器上：**

1. **[安裝FFmpeg](ffmpeg.md)**

**在所有作者／發佈例項上：**

1. **[配置JDBC連接池](mysql.md#configure-jdbc-connections)**使用Web控制台(configMgr):*http://localhost:4502/system/console/configMgr*

1. **[配置SCORM引擎服務](mysql.md#aem-communities-scormengine-service)**使用Web控制台(configMgr):*http://localhost:4502/system/console/configMgr*

1. **[配置CSRF篩選器](mysql.md#adobe-granite-csrf-filter)**使用Web控制台(configMgr):*http://localhost:4502/system/console/configMgr*

**在作者實例上：**

1. (可&#x200B;*選*) **[設定Analytics服務](analytics.md)**使用工具、部署、雲端服務主控台：*http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[設定Fmpeg](ffmpeg.md#configure-ffmpeg-transcoding-service)**使用Workflow/Models主控台

1. **[啟用通道服務](deploy-communities.md#tunnel-service-on-author)**使用Web控制台(configMgr):*http://localhost:4502/system/console/configMgr*

1. **[建立社群管理員](users.md#creating-community-members)**：製作環境使用傳統UI安全性主控台：http://localhost:4502/useradmin **建立路徑= /home/users/community的使用者

   * 將成員添加到以下組：

      * 社群支援經理
      * 社群管理員

## Dispatcher {#dispatcher}

當部署包含 [AEM的Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)，為了讓啟用功能正常運作，需要修改 `clientheader` 和 `filter` 區段。 請參 [閱配置Dispatcher for Communities](dispatcher.md#enablement)。
