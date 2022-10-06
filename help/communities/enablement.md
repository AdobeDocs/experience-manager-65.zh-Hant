---
title: 配置啟用功能
seo-title: Configuring Enablement Features
description: 在Communities中設定啟用功能
seo-description: Configure enablement features in Communities
uuid: 27be3128-1a7d-412e-99a9-6e3b3b0aec1c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 765a3d9b-4552-403e-872c-fdf684ac271d
role: Admin
exl-id: b635e2ed-4637-4b2f-a746-ec8dc7541bab
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 1%

---

# 配置啟用功能 {#configuring-enablement-features}

## 總覽 {#overview}

啟用功能可讓您建立 [啟用社群](overview.md#enablement-community).

* 若要在生產環境中使用，此功能需要額外的授權。

使用啟用功能需要下列項目：

安裝：

* **SCORM**

   可共用內容物件參考模型(SCORM)是數位學習的標準與規格集合。 SCORM也定義了如何將內容封裝成可傳輸的ZIP檔案。

* **MySQL**

   MySQL是關係資料庫，主要用於SCORM追蹤和報告啟用資料，以及用於追蹤視訊進度的表格。 啟用功能包的SCORM需要MySQL JDBC驅動程式。

* **FFmpeg**

   FFmpeg是轉換和串流音訊和視訊的解決方案，安裝後用於適當轉碼 [影片資產](../../help/sites-authoring/default-components-foundation.md#video). 針對啟用社群，製作環境會使用它來取得上傳資源的中繼資料，並產生縮圖以在列出資源時顯示。

設定：

* **社群管理員**

   針對啟用社群，僅限 `Community Enablement Managers` 使用者群組可被指派為 `Community Site Enablement Manager`，其權限可能包括發佈環境中的內容建立、指派和成員管理。

可選配置：

* **Adobe Analytics**

   與Adobe Analytics的整合新增了完整的報表功能，並支援將視訊心率新增至Analytics。

* **Dispatcher**

## 配置步驟 {#configuration-steps}

以下是啟用社群的必要步驟。

每個步驟都會連結至提供必要詳細資料的檔案。

**在所有製作/發佈例項上：**

1. **[為MySQL安裝JDBC驅動程式](deploy-communities.md#jdbc-driver-for-mysql)**

   使用Web控制台（套件組合）: *http://localhost:4502/system/console/bundles*

   安裝 *befor* 安裝SCORM套件

1. **[安裝SCORM套件](deploy-communities.md#scorm-package)**


   使用包管理器： *http://localhost:4502/crx/packmgr/*

**在任何伺服器上：**

1. **[安裝MySQL、MySQL Workbench](mysql.md)**

1. **[安裝MySQL資料庫](mysql.md#database-setup)**

   執行從製作執行個體下載的SQL指令碼

   使用MySQL Workbench

**在托管作者例項的相同伺服器上：**

1. **[安裝FFmpeg](ffmpeg.md)**

**在所有製作/發佈例項上：**

1. **[配置JDBC連接池](mysql.md#configure-jdbc-connections)**

   使用Web控制台(configMgr): *http://localhost:4502/system/console/configMgr*

1. **[配置SCORM引擎服務](mysql.md#aem-communities-scormengine-service)**

   使用Web控制台(configMgr): *http://localhost:4502/system/console/configMgr*

1. **[設定CSRF篩選器](mysql.md#adobe-granite-csrf-filter)**

   使用Web控制台(configMgr): *http://localhost:4502/system/console/configMgr*

**在製作例項上：**

1. (*可選*) **[設定Analytics服務](analytics.md)**

   使用工具、部署、Cloud Services控制台： *http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[配置FFmpeg](ffmpeg.md#configure-ffmpeg-transcoding-service)**

   使用工作流/模型控制台

1. **[啟用通道服務](deploy-communities.md#tunnel-service-on-author)**

   使用Web控制台(configMgr): *http://localhost:4502/system/console/configMgr*

1. **[建立社群管理員](users.md#creating-community-members)**

   針對製作環境，請使用傳統UI安全性主控台： *http://localhost:4502/useradmin*

   使用路徑= /home/users/community建立使用者

   * 將成員添加到以下組：

      * 社群培訓經理
      * Communities管理員

## Dispatcher {#dispatcher}

當部署包含 [AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)，為了讓啟用功能正常運作， `clientheader` 和 `filter` 章節需要修改。 請參閱 [為社群設定Dispatcher](dispatcher.md#enablement).
