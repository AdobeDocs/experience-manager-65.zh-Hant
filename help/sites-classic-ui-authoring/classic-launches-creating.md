---
title: 建立 Launch
description: 建立啟動以啟用更新現有網頁的新版本以供將來激活。 建立「啟動」時，指定標題和源頁。
uuid: e67608a9-e6c9-42f3-bd1d-63a5fa87ae18
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 48826f03-6731-49c5-a6c5-6e2fb718f912
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 8ab21067-c19a-4faa-8bf0-cd9f21f6df70
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 15%

---

# 建立 Launch{#creating-launches}

建立啟動以啟用更新現有網頁的新版本以供將來激活。 建立「啟動」時，可指定標題和源頁：

* 標題將出現在 **側腳**&#x200B;從那裡，作者們可以接觸到他們，對他們進行工作。
* 預設情況下，源頁面的子頁面將包括在啟動中。 如果需要，只能使用源頁。
* 預設情況下， [即時拷貝](/help/sites-administering/msm.md) 在源頁更改時自動更新啟動頁。 可以指定建立靜態副本以防止自動更改。

(可選) 您可以指定 **啟動日期**  (和時間)，以定義啟動頁面要升級和啟動的時間。不過，「 **啟動日期** 」只會搭配「生產就緒 **」旗標運作(請** 參閱編輯啟動設定 [](/help/sites-classic-ui-authoring/classic-launches-editing.md#editing-a-launch-configuration));要讓動作實際自動發生，必須同時設定。

## 建立啟動 {#creating-a-launch}

以下過程建立啟動。

1. 開啟網站管理頁([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin))。
1. 按一下 **新建……** 然後 **新建啟動……**。
1. 在 **建立啟動** 對話框，指定以下屬性的值：

   * **啟動標題**:啟動的名稱。 該名稱對作者應有意義。
   * **「源」頁**:要為其建立啟動的頁面的路徑。 預設情況下，所有子頁都包括在內。
   * **排除子頁**:選擇此選項僅為源頁面而不是子頁面建立啟動。 預設情況下，未選擇此選項。
   * **保持同步**:選擇此選項可在源頁面更改時自動更新啟動頁面的內容。 這是通過使發射 [即時拷貝](/help/sites-administering/msm.md)。
   * **啟動日期**:激活啟動副本的日期和時間(取決於 **生產就緒** 標誌；見 [啟動 — 事件順序](/help/sites-authoring/launches.md#launches-the-order-of-events))。

   ![chlimage_1-99](assets/chlimage_1-99a.png)

1. 按一下&#x200B;**建立**。

## 刪除啟動 {#deleting-a-launch}

您也可以刪除啟動。

1. 在 [啟動控制台](/help/sites-classic-ui-authoring/classic-launches.md)，選擇所需的啟動。
1. 按一下 **刪除**  — 需要確認：

   ![chlimage_1-100](assets/chlimage_1-100a.png)

   >[!CAUTION]
   >
   >刪除嵌套啟動時，應先刪除較低級別。
