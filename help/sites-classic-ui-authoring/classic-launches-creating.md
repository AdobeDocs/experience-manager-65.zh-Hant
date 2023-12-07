---
title: 建立啟動
description: 建立啟動項，以更新現有網頁的新版本，以供日後啟用。 建立啟動項時，您可以指定標題和來源頁面。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 8ab21067-c19a-4faa-8bf0-cd9f21f6df70
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 16%

---

# 建立啟動{#creating-launches}

建立啟動項，以更新現有網頁的新版本，以供日後啟用。 建立啟動項時，您可以指定標題和來源頁面：

* 標題會顯示在 **Sidekick**，作者可從中存取縮圖，進而加以處理。
* 預設情況下，啟動會包含來源頁面的子頁面。 您可以視需要使用來源頁面。
* 根據預設， [即時副本](/help/sites-administering/msm.md) 當來源頁面變更時，會自動更新啟動頁面。 您可以指定建立靜態副本，以防止自動變更。

(可選) 您可以指定 **啟動日期**  (和時間)，以定義啟動頁面要升級和啟動的時間。不過，「 **啟動日期** 」只會搭配「生產就緒 **」旗標運作(請** 參閱編輯啟動設定 [](/help/sites-classic-ui-authoring/classic-launches-editing.md#editing-a-launch-configuration));要讓動作實際自動發生，必須同時設定。

## 建立啟動項 {#creating-a-launch}

下列程式會建立啟動。

1. 開啟網站管理頁面([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin))。
1. 按一下 **新增……** 則 **新增啟動項……**.
1. 在 **建立啟動項** 對話方塊，指定下列屬性的值：

   * **啟動項標題**：啟動項的名稱。 這個名稱應該對作者有意義。
   * **來源頁面**：要建立啟動項的頁面路徑。 依預設，會包含所有子頁面。
   * **排除子頁面**：選取此選項，僅針對來源頁面建立啟動，不針對子頁面。 依預設，不會選取此選項。
   * **保持同步**：選取此選項，可在來源頁面變更時自動更新啟動頁面的內容。 這是透過將啟動設為 [即時副本](/help/sites-administering/msm.md).
   * **啟動日期**：啟動副本的啟動日期和時間(取決於 **生產就緒** 標幟；請參閱 [啟動 — 事件順序](/help/sites-authoring/launches.md#launches-the-order-of-events))。

   ![chlimage_1-99](assets/chlimage_1-99a.png)

1. 按一下&#x200B;**建立**。

## 刪除啟動項 {#deleting-a-launch}

您也可以刪除啟動項。

1. 在 [啟動主控台](/help/sites-classic-ui-authoring/classic-launches.md)，選取所需的啟動。
1. 按一下 **刪除**  — 需要確認：

   ![chlimage_1-100](assets/chlimage_1-100a.png)

   >[!CAUTION]
   >
   >刪除巢狀啟動時，您應該先刪除較低層級。
