---
title: 設定帳戶環境
description: AEM提供您設定帳戶及製作環境某些方面的功能
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 6079431d-7d08-4973-8bb4-a8d10626a795
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 5%

---

# 設定帳戶環境{#configuring-your-account-environment}

AEM提供您設定帳戶及製作環境某些方面的功能。

使用頁 [首和相關「我的首選項](/help/sites-authoring/user-properties.md#user-settings) 」對話框中的「用戶」選項 [](/help/sites-authoring/basic-handling.md#the-header)[](#userpreferences) ，可以修改用戶選項，例如。

首先，存取 [使用者](/help/sites-authoring/user-properties.md#user-settings) 選項來識別。

## 用戶設定 {#user-settings}

此 **使用者** 設定對話方塊可讓您存取：

* 模擬為

   * 使用 [模擬為](/help/sites-administering/security.md#impersonating-another-user) 使用者可以代表其他使用者工作的功能。

* 設定檔

   * 提供便利的連結，讓您連結至 [使用者設定](/help/sites-administering/security.md))

* [我的喜好設定](/help/sites-authoring/user-properties.md#my-preferences)

   * 指定使用者專屬的各種偏好設定設定

![screen_shot_2018-03-20at103808](assets/screen_shot_2018-03-20at103808.png)

### 我的喜好設定 {#my-preferences}

此 **我的偏好設定** 對話方塊可透過 [使用者](/help/sites-authoring/user-properties.md#user-settings) 選項來識別。

每個使用者都可以為自己設定某些屬性。

![screen-shot_2019-03-05at100322](assets/screen-shot_2019-03-05at100322.png)

* **語言**

  這會定義用於編寫環境UI的語言。 從可用清單中選取所需的語言。

  此設定也用於傳統UI。

* **視窗管理**

  這會定義開啟視窗的行為。 選取：

   * **多視窗** （預設）

      * 頁面會在新視窗中開啟。

   * **單一視窗**

      * 頁面會在目前視窗中開啟。

* **顯示資產的案頭動作**

  此選項需要AEM案頭應用程式才能使用。

* **附註顏色**

  這會定義製作註解時使用的預設顏色。

   * 按一下顏色區塊，即可開啟色票選取器並選取顏色。
   * 或者，在欄位中輸入所需顏色的十六進位代碼。

* **相對日期顯示**

  為了改善可讀性，AEM會將過去七天內的日期轉譯為相對日期（例如3天前），並將較舊的日期轉譯為確切日期（例如2017年3月20日）。

  此選項定義系統中日期的顯示方式。 下列選項可供使用：

   * **一律顯示確切日期**：一律顯示確切日期（從不顯示相對日期）。
   * **1天**：對於一天內的日期顯示相對日期，其他情況則顯示確切日期。

   * **7天（預設）**：對於七天內的日期顯示相對日期，其他情況則顯示確切日期。

   * **1個月**：對於一個月內的日期顯示相對日期，其他情況則顯示確切日期。

   * **1年**：對於一年內的日期顯示相對日期，其他情況則顯示確切日期。

   * **一律顯示相對日期**：絕對不會顯示確切日期，而只會顯示相對日期。

* **啟用捷徑**

  AEM支援數個鍵盤快速鍵，讓撰寫更有效率。

   * [用於編輯頁面的鍵盤快速鍵](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
   * [主控台的鍵盤快速鍵](/help/sites-authoring/keyboard-shortcuts.md)

  此選項可啟用鍵盤快速鍵。 預設會啟用這些功能，但也可以停用，例如，如果使用者有特定的協助工具要求。

* **使用傳統製作體驗**

  此選項會啟用 [傳統UI](/help/sites-classic-ui-authoring/classic-page-author-first-steps.md)-based頁面製作。 依預設，會使用標準UI。

* **啟用資產首頁**

  只有在系統管理員已啟用整個組織的資產首頁體驗時，才可使用此選項。

* **Stock設定**

  此選項可讓您指定偏好的Adobe Stock設定，且僅在您的系統管理員已啟用時可用 [Adobe Stock整合](/help/assets/aem-assets-adobe-stock.md).
