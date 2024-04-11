---
title: 使用Launches開發未來版本的內容
description: 啟動可讓您有效率地開發未來版本的內容。 它們可讓您進行變更，以供未來發佈，同時維護您目前的頁面。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
exl-id: b25d3f8e-5687-49ab-95e1-19ec75c87f6e
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Launches
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 81%

---

# 啟動{#launches}

啟動可讓您有效率地開發未來版本的內容。

系統隨即會建立啟動，讓您將來的變更準備就緒，以便發佈（同時維護目前頁面）。 在編輯和更新您的啟動頁面後，您將它們提升回來源，然後啟動來源頁面 (頂層)。提升功能會將啟動內容複製回來源頁面，可以手動或自動完成 (視建立和編輯啟動時設定的欄位)。

例如，您的線上商店的季節性產品頁面每季更新一次，以便特色產品符合目前季節。為準備下一季的更新，您可以建立一個相應網頁的啟動。在整個季度中，以下變更會累積在啟動副本中：

* 因正常維護工作而產生的來源頁面變更。這些變更會自動複製到啟動頁面中。
* 直接在啟動頁面上執行的編輯，為下一季做準備。

下一季到來時，您提升啟動頁面，以便您可以發佈來源頁面 (包含更新的內容)。您可以提升所有頁面，也可僅提升您修改過的頁面。

啟動也可以：

* 為多個根分支建立。雖然您可以為整個網站建立啟動 (並在其中進行變更)，但這可能是不切實際的，因為需要複製整個網站。當涉及數百甚至數千頁時，複製動作和之後提升工作所需的比較作業，會影響系統要求和效能。
* 巢狀 (啟動中有啟動) 可讓您在現有啟動中建立啟動，如此作者可以利用已完成的變更，而不用對每個啟動重複進行相同的變更。

本節說明如何建立、編輯和提升（以及如有需要） [刪除](/help/sites-authoring/launches-creating.md#deleting-a-launch))從Sites主控台內啟動頁面，或 [啟動主控台](#the-launches-console)：

* [建立啟動](/help/sites-authoring/launches-creating.md)
* [編輯啟動](/help/sites-authoring/launches-editing.md)
* [提升啟動](/help/sites-authoring/launches-promoting.md)

## 啟動 - 事件順序 {#launches-the-order-of-events}

啟動可讓您有效率地為一或多個已啟動網頁的未來版本開發內容。

啟動可讓您：

* 建立來源頁面的副本：

   * 副本是您的啟動。
   * 頂層來源頁面稱為&#x200B;**生產**。

      * 來源頁面可以取自多個 (獨立的) 分支。

  ![啟動動作概觀](assets/chlimage_1-111.png)

* 編輯啟動設定：

   * 在啟動中新增或移除頁面和/或分支。
   * 編輯啟動屬性；例如&#x200B;**標題**、**啟動日期**、**生產就緒**&#x200B;標幟。

* 您可以手動或自動提升和發佈內容：

   * 手動：

      * 當準備好發佈時，將啟動內容推回 **Target** (來源頁面)。
      * 從來源頁面 (推回後) 發佈內容。
      * 提升所有頁面，或僅提升修改後的頁面。

   * 自動 - 這涉及以下項目：

      * **啟動** (**上線**) **日期**&#x200B;欄位：這可在建立或編輯啟動時設定。

      * **生產就緒**&#x200B;標幟：這只能在編輯 Launch 時設定。
      * 如果&#x200B;**生產就緒**&#x200B;標幟已設定，Launch 將於 **Launch** (**上線**) **日期**&#x200B;自動提升至生產頁面。提升後，生產頁面會自動發佈。\
        如果未設定日期，則該標幟將無效。

* 並行更新來源頁面和啟動頁面：

   * 對來源頁面的變更會自動實作在啟動副本 (如果設定為繼承，即為 Live Copy)。
   * 可以在不中斷這些自動更新或來源頁面的情況下，對啟動副本進行變更。

  ![更新概觀](assets/chlimage_1-112.png)

* [建立巢狀啟動](/help/sites-authoring/launches-creating.md#creating-a-nested-launch) - 啟動中的啟動：

   * 來源是現有的啟動。
   * 您可以[將巢狀啟動](/help/sites-authoring/launches-promoting.md#promoting-a-nested-launch)提升到任何目標，這可以是父啟動或頂層來源頁面 (生產)。

  ![巢狀啟動概述](assets/chlimage_1-113.png)

  >[!CAUTION]
  >
  >刪除啟動將移除啟動本身和所有子系巢狀啟動。

>[!NOTE]
>
>建立和編輯啟動需要 `/content/launches` 的存取權 - 與預設群組 `content-authors` 相同。
>
>如果您遇到任何問題，請聯絡您的系統管理員。

>[!CAUTION]
>
>不支援在Launch頁面上重新排序元件。
>
>頁面升級時，將會反映任何內容變更，但元件位置不會變更。


### 啟動主控台 {#the-launches-console}

啟動主控台可提供對您的啟動的概觀，並讓您對清單上的執行動作。主控台可透過以下方式存取：

* **工具**&#x200B;主控台：**工具**、**Sites**、**啟動**。

* 或直接使用 [https://localhost:4502/libs/launches/content/launches.html](https://localhost:4502/libs/launches/content/launches.html)

## 啟動在在參考內 (Sites 主控台) {#launches-in-references-sites-console}

1. 在 **Sites** 主控台中，導覽至啟動來源。
1. 開啟&#x200B;**參考**&#x200B;邊欄並選取來源頁面。
1. 選取 **啟動**，則會列出現有的啟動：

   ![參考標籤 — 啟動](assets/screen-shot_2019-03-05at121901-1.png)

1. 按一下適當的啟動，畫面會顯示可執行的動作清單：

   ![選取啟動以顯示可能的動作](assets/screen-shot_2019-03-05at121952-1.png)
