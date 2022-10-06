---
title: 建立啟動
seo-title: Creating Launches
description: 建立啟動，以啟用更新新版本的現有網頁，以供日後啟用。 建立Launch時，需指定標題和來源頁面。
seo-description: Create a launch to enable the updating of a new version of existing web pages for future activation. When you create a Launch, you specify a title and the source page.
uuid: e67608a9-e6c9-42f3-bd1d-63a5fa87ae18
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 48826f03-6731-49c5-a6c5-6e2fb718f912
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 8ab21067-c19a-4faa-8bf0-cd9f21f6df70
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 15%

---

# 建立啟動 {#creating-launches}

建立啟動，以啟用更新新版本的現有網頁，以供日後啟用。 建立Launch時，需指定標題和來源頁面：

* 標題會顯示在 **Sidekick**，供作者存取，以便使用。
* 依預設，來源頁面的子頁面會包含在啟動中。 您只能視需要使用來源頁面。
* 依預設， [Live Copy](/help/sites-administering/msm.md) 源頁面變更時，會自動更新launch頁面。 您可以指定建立靜態副本以防止自動更改。

(可選) 您可以指定 **啟動日期**  (和時間)，以定義啟動頁面要升級和啟動的時間。不過，「 **啟動日期** 」只會搭配「生產就緒 **」旗標運作(請** 參閱編輯啟動設定 [](/help/sites-classic-ui-authoring/classic-launches-editing.md#editing-a-launch-configuration));要讓動作實際自動發生，必須同時設定。

## 建立啟動 {#creating-a-launch}

以下過程將建立啟動。

1. 開啟「網站管理」頁面([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin))。
1. 按一下 **新……** then **新啟動……**.
1. 在 **建立Launch** 對話框，指定以下屬性的值：

   * **啟動標題**:Launch的名稱。 名稱對作者應有意義。
   * **源頁**:建立啟動的頁面路徑。 預設會包含所有子頁面。
   * **排除子頁面**:選擇此選項可僅建立源頁面的啟動，而不建立子頁面的啟動。 依預設，不會選取此選項。
   * **保持同步**:選取此選項，可在來源頁面變更時自動更新啟動頁面的內容。 這是透過讓啟動 [即時副本](/help/sites-administering/msm.md).
   * **啟動日期**:啟動副本的啟動日期和時間(取決於 **生產就緒** 標誌；請參閱 [啟動 — 事件順序](/help/sites-authoring/launches.md#launches-the-order-of-events))。

   ![chlimage_1-99](assets/chlimage_1-99a.png)

1. 按一下&#x200B;**建立**。

## 刪除啟動 {#deleting-a-launch}

您也可以刪除啟動。

1. 在 [啟動主控台](/help/sites-classic-ui-authoring/classic-launches.md)，請選取所需的啟動。
1. 按一下 **刪除**  — 需要確認：

   ![chlimage_1-100](assets/chlimage_1-100a.png)

   >[!CAUTION]
   >
   >刪除巢狀啟動時，您應先刪除較低層級。
