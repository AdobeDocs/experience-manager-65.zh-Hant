---
title: 設定帳戶環境
seo-title: Configuring Your Account Environment
description: AEM可讓您設定帳戶，以及製作環境的某些方面
seo-description: AEM provides you with the capability to configure your account and certain aspects of the author environment
uuid: ef31be29-5c18-4dc9-ad51-fb001588b31e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b610e19c-f8d9-4ae2-b056-9fd5cf541261
docset: aem65
exl-id: 6079431d-7d08-4973-8bb4-a8d10626a795
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 10%

---

# 設定帳戶環境{#configuring-your-account-environment}

AEM可讓您設定帳戶，以及製作環境的某些方面。

使用頁 [首和相關「我的首選項](/help/sites-authoring/user-properties.md#user-settings) 」對話框中的「用戶」選項 [](/help/sites-authoring/basic-handling.md#the-header)[](#userpreferences) ，可以修改用戶選項，例如。

首先，存取 [使用者](/help/sites-authoring/user-properties.md#user-settings) 選項。

## 使用者設定 {#user-settings}

此 **使用者** 「設定」對話方塊可讓您存取：

* 模擬為

   * 使用 [模擬為](/help/sites-administering/security.md#impersonating-another-user) 功能使用者可以代表其他使用者運作。

* 設定檔

   * 提供您 [使用者設定](/help/sites-administering/security.md))

* [我的喜好設定](/help/sites-authoring/user-properties.md#my-preferences)

   * 指定您的使用者專屬的各種偏好設定

![screen_shot_2018-03-20at103808](assets/screen_shot_2018-03-20at103808.png)

### 我的喜好設定 {#my-preferences}

此 **我的偏好設定** 對話方塊是透過 [使用者](/help/sites-authoring/user-properties.md#user-settings) 選項。

每個使用者都可為自己設定特定屬性。

![screen-shot_2019-03-05at100322](assets/screen-shot_2019-03-05at100322.png)

* **語言**

   這會定義用於製作環境UI的語言。 從可用清單中選取所需語言。

   傳統UI也會使用此設定。

* **視窗管理**

   這會定義行為或開啟視窗。 選擇以下任一項：

   * **多個視窗** （預設）

      * 頁面將在新視窗中開啟。
   * **單一視窗**

      * 將在當前窗口中開啟頁面。


* **顯示資產桌面動態**

   此選項需要AEM案頭應用程式才能使用。

* **附註顏色**

   這會定義進行註解時使用的預設顏色。

   * 按一下顏色塊以開啟色板選擇器以選取顏色。
   * 或者，在欄位中輸入所需顏色的十六進位代碼。

* **相對日期顯示**

   為了改善可讀性，AEM會將過去七天內的日期轉譯為相對日期（例如三天前），並將舊日期轉譯為確切日期（例如2017年3月20日）。

   此選項會定義系統中日期的顯示方式。 可使用下列選項：

   * **一律顯示確切日期**:一律會顯示確切日期（從不會顯示相對日期）。
   * **1天**:相對日期會顯示在一天內，否則會顯示確切日期。

   * **7天（預設）**:相對日期會在七天內顯示，否則會顯示確切日期。

   * **1個月**:相對日期會顯示在一個月內，否則會顯示確切日期。

   * **1年**:相對日期會顯示為一年內的日期，否則會顯示確切的日期。

   * **一律顯示相對日期**:系統不會顯示確切日期，只會顯示相對日期。

* **啟用快捷方式**

   AEM支援許多鍵盤快速鍵，讓編寫更有效率。

   * [編輯頁面的鍵盤快速鍵](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
   * [控制台的鍵盤快速鍵](/help/sites-authoring/keyboard-shortcuts.md)

   此選項啟用鍵盤快速鍵。 預設會啟用，但例如若使用者有特定的協助工具需求，則可停用。

* **使用傳統製作體驗**

   此選項啟用 [傳統UI](/help/sites-classic-ui-authoring/home.md)頁面編寫。 預設會使用標準UI。

* **啟用資產首頁**

   只有在系統管理員已為整個組織啟用資產首頁體驗時，才可使用此選項。

* **Stock 設定**

   此選項可指定慣用的Adobe Stock配置，且僅在系統管理員已啟用時才可用 [Adobe Stock整合](/help/assets/aem-assets-adobe-stock.md).
