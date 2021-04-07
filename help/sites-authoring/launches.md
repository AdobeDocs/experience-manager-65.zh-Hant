---
title: 啟動
seo-title: 啟動
description: 啟動可讓您有效率地開發未來版本的內容。 它們可讓您做好變更，以備日後出版，同時仍能維持目前的頁面
seo-description: 啟動可讓您有效率地開發未來版本的內容。 它們可讓您做好變更，以備日後出版，同時仍能維持目前的頁面
uuid: 4bbd9865-735d-4232-b69c-b64193ac5d83
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: e145afd8-7391-47aa-b389-16fb303749d0
docset: aem65
exl-id: b25d3f8e-5687-49ab-95e1-19ec75c87f6e
translation-type: tm+mt
source-git-commit: 47870c05d231bacc424cfbf308f78bc1eaeb907b
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 6%

---

# 啟動{#launches}

啟動可讓您有效率地開發未來版本的內容。

會建立啟動，讓您做好變更，以備日後出版（同時維持目前的頁面）。 在編輯和更新啟動頁面後，您會將其提升回來源頁面，然後啟動來源頁面（頂層）。 升級會將啟動內容複製回來源頁面，並可手動或自動執行（取決於建立和編輯啟動時設定的欄位）。

例如，您線上商店的季節性產品頁面會每季更新一次，因此精選產品會與目前的季節一致。 為準備下一季度更新，您可以建立適當網頁的啟動。 在整個季度中，產品發佈副本中會累計下列變更：

* 對因正常維護任務而發生的源頁面進行更改。 這些變更會自動在啟動頁面中複製。
* 直接在啟動頁面上執行的編輯，以備下一季度使用。

下一季到來時，您會促銷啟動頁面，以便發佈來源頁面（保有更新的內容）。 您可以升級所有頁面，或僅升級已修改的頁面。

啟動也可以是：

* 為多個根分支建立。 雖然您可以建立整個網站的啟動（並在此進行變更），但是這可能不切實際，因為整個網站需要複製。 當涉及數百頁甚至數千頁時，複製動作以及升級工作所需的比較都會影響系統需求和效能。
* 巢狀內嵌（啟動中的啟動），可讓您從現有的啟動建立啟動，讓作者可以利用已做的變更，而不必針對每次啟動進行多次相同的變更。

本節說明如何從「網站」主控台或「啟動」主控台](#the-launches-console)中建立、編輯和升級（如有必要，請[delete](/help/sites-authoring/launches-creating.md#deleting-a-launch)）啟動頁面：[

* [建立啟動 ](/help/sites-authoring/launches-creating.md)
* [編輯啟動](/help/sites-authoring/launches-editing.md)
* [提升啟動](/help/sites-authoring/launches-promoting.md)

## 啟動——事件順序{#launches-the-order-of-events}

啟動可讓您有效率地開發內容，以供日後發行的一或多個已啟動網頁使用。

啟動可讓您：

* 建立來源頁面的復本：

   * 復本是您的啟動。
   * 頂層來源頁面稱為「生 **產」**。

      * 來源頁面可從多個（個別）分支取用。

   ![chlimage_1-111](assets/chlimage_1-111.png)

* 編輯啟動設定：

   * 在啟動中新增或移除頁面和／或分支。
   * 編輯啟動屬性；例如 **Title**、Launch Date **、Production Ready****** 旗標。

* 您可以手動或自動促銷和發佈內容：

   * 手動:

      * 當您的啟動內容準備好發佈時，將其提升回&#x200B;**Target**（來源頁面）。
      * 從來源（在向後促銷後）頁面發佈內容。
      * 升級所有頁面，或僅升級修改的頁面。
   * 自動——這涉及下列事項：

      * **Launch**(**Live**)**date**&#x200B;欄位：這可在建立或編輯啟動時設定。

      * **Production Ready**&#x200B;標幟：這只能在編輯啟動時設定。
      * 如果設定了&#x200B;**Production Ready**&#x200B;標幟，則啟動會自動升級至指定&#x200B;**Launch**(**Live**)**date**&#x200B;的生產頁面。 促銷後，生產頁面會自動發佈。\
         如果尚未設定日期，則旗標將無效。


* 同時更新來源和啟動頁面：

   * 對源頁面的更改會自動在啟動副本中實現(如果設定為繼承；即即即即時副本)。
   * 您可以變更啟動副本，而不中斷這些自動更新或來源頁面。

   ![chlimage_1-112](assets/chlimage_1-112.png)

* [建立巢狀啟動](/help/sites-authoring/launches-creating.md#creating-a-nested-launch) -啟動中的啟動：

   * 來源是現有的啟動。
   * 您可以[將巢狀啟動](/help/sites-authoring/launches-promoting.md#promoting-a-nested-launch)提升至任何目標；這可以是父級啟動或頂層來源頁面（生產）。

   ![chlimage_1-113](assets/chlimage_1-113.png)

   >[!CAUTION]
   >
   >刪除啟動會移除啟動本身和所有子系巢狀啟動。

>[!NOTE]
>
>建立和編輯啟動需要對`/content/launches`的訪問權限——與預設組`content-authors`一樣。
>
>如果您遇到任何問題，請聯絡您的系統管理員。

>[!CAUTION]
>
>不支援在啟動頁面上重新排序元件。
>
>當促銷頁面時，會反映任何內容變更，但元件位置不會變更。


### 啟動控制台{#the-launches-console}

「啟動」控制台提供啟動的概述，並可讓您對所列的動作採取動作。 可通過以下方式訪問控制台：

* **工具**&#x200B;控制台：**Tools**、**Sites**、**Launches**。

* 或直接使用[https://localhost:4502/libs/launches/content/launches.html](https://localhost:4502/libs/launches/content/launches.html)

## 在參考(Sites Console){#launches-in-references-sites-console}中啟動

1. 在&#x200B;**Sites**&#x200B;控制台中，瀏覽至啟動的源。
1. 開啟&#x200B;**參考**&#x200B;邊欄並選取來源頁面。
1. 選擇&#x200B;**啟動**，將列出現有啟動：

   ![screen-shot_2019-03-05at121901-1](assets/screen-shot_2019-03-05at121901-1.png)

1. 點選／按一下適當的啟動，將會顯示可能動作的清單：

   ![screen-shot_2019-03-05at121952-1](assets/screen-shot_2019-03-05at121952-1.png)
