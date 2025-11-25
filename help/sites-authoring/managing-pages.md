---
title: 使用AEM建立及組織頁面
description: 瞭解如何使用Adobe Experience Manager建立和管理頁面。
exl-id: 74576e51-4b4e-464e-a0b8-0fae748a505d
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '2476'
ht-degree: 2%

---

# 建立及組織頁面 {#creating-and-organizing-pages}

本節說明如何使用Adobe Experience Manager (AEM)建立和管理頁面，以便您接著可以在這些頁面上[建立內容](/help/sites-authoring/editing-content.md)。

>[!NOTE]
>
>您的帳戶需要[適當的存取許可權](/help/sites-administering/security.md)和[許可權](/help/sites-administering/security.md#permissions)，才能在頁面上執行建立、複製、移動、編輯和刪除等動作。
>
>如果您遇到任何問題，我們建議您連絡系統管理員。

>[!NOTE]
>
>您可從網站主控台使用數個[鍵盤快速鍵](/help/sites-authoring/keyboard-shortcuts.md)，以更有效率地組織您的頁面。

## 組織您的網站 {#organizing-your-website}

以作者身分，在AEM中組織您的網站。 這涉及建立和命名內容頁面，以便：

* 您可以在作者環境中輕鬆找到他們
* 您網站的訪客可在發佈環境中輕鬆瀏覽這些專案

您也可以使用[資料夾](#creating-a-new-folder)來協助組織您的內容。

網站的結構可視為儲存內容頁面的樹狀結構。 這些內容頁面的名稱會用於組成URL，而標題則會在您檢視頁面內容時顯示。

以下顯示We.Retail網站的範例，其中存取了健行短褲頁面( `desert-sky-shorts`)：

* 作者環境
  `https://localhost:4502/editor.html/content/we-retail/us/en/products/equipment/hiking/desert-sky-shorts.html`

* 發佈環境
  `https://localhost:4503/content/we-retail/us/en/products/equipment/hiking/desert-sky-shorts.html`

根據您執行個體的設定，發佈環境上可能會選擇使用`/content`。

```xml
 /content
 /we-retail
  /us
   /en
    /products
     /equipment
      /hiking
       /desert-sky-shorts
       /hiking-poles
       /...
      /running...
      /surfing...
      /...
     /seasonal...
     /...
    /about-us
    /experience
    /...
   /es...
  /de...
  /fr...
  /...
 /...
```

您可以從&#x200B;**網站**&#x200B;主控台檢視此結構，您可以[瀏覽您網站的各個頁面](/help/sites-authoring/basic-handling.md#navigating)，並在這些頁面上執行動作。 您也可以建立新網站和[新頁面](#creating-a-new-page)。

從任何點開始，您都可以從標頭列的階層連結看到向上分支：

![caop-01](assets/caop-01.png)

### 頁面命名慣例 {#page-naming-conventions}

建立頁面時，有兩個索引鍵欄位：

* **[標題](#title)**：

   * 主控台會向使用者顯示這項資訊，並在編輯時顯示在頁面內容的頂端。
   * 此字段是必填字段。

* **[名稱](#name)**：

   * 這會用來產生URI。
   * 此欄位的使用者輸入為選用。 如果未指定，則會從標題衍生名稱。 如需詳細資訊，請參閱下列章節[頁面名稱限制和最佳實務](/help/sites-authoring/managing-pages.md#page-name-restrictions-and-best-practices)。

#### 頁面名稱限制和最佳實務 {#page-name-restrictions-and-best-practices}

頁面 **標題**&#x200B;**和名稱可以單獨建立** ，但是是相關的：

* 建立頁面時，只需要&#x200B;**標題**&#x200B;欄位。 如果建立頁面時未提供&#x200B;**Name**，AEM將會從標題的前64個字元產生名稱（遵循以下設定的驗證）。 僅前64個字元用於支援短頁面名稱的最佳做法。

* 如果作者手動指定頁面名稱，64字元限制不適用，但頁面名稱長度的其他技術限制可能適用。

>[!NOTE]
>
>定義頁面名稱時，一個好的經驗法則是保持頁面名稱簡短，但儘可能表達到位且容易記憶，讓讀者容易理解。 如需詳細資訊，請參閱[專案的](https://www.w3.org/Provider/Style/TITLE.html)W3C樣式指南`title`。
>
>也請記住，某些瀏覽器（例如舊版的IE）只能接受一定長度的URL，因此還有技術原因需縮短頁面名稱。

建立頁面時，AEM [會依據AEM和JCR所強加的慣例](/help/sites-developing/naming-conventions.md)驗證頁面名稱。

允許的最小字元為：

* &#39;a&#39;到&#39;z&#39;
* &#39;A&#39;到&#39;Z&#39;
* &#39;0&#39;到&#39;9&#39;
* `_` （底線）
* `-` （連字型大小/減號）

可在[命名慣例](/help/sites-developing/naming-conventions.md)中找到所有允許字元的完整詳細資料。

>[!NOTE]
>
>如果AEM在[MongoMK持續性管理員部署](/help/sites-deploying/recommended-deploys.md)上執行，頁面名稱限製為150個字元。

#### 標題 {#title}

如果您在建立頁面時只提供頁面&#x200B;**Title**，AEM會從此字串衍生頁面&#x200B;**Name**，並[依據AEM和JCR所強加的慣例](/help/sites-developing/naming-conventions.md)驗證名稱。 將接受包含無效字元的&#x200B;**Title**&#x200B;欄位，但衍生的名稱會將無效的字元替換掉。 例如：

| 標題 | 衍生名稱 |
|---|---|
| Schon | schoen.html |
| SC%&amp;&#42;c+ | sc---c-.html |

#### 名稱 {#name}

當您在建立頁面時提供頁面&#x200B;**Name**&#x200B;時，AEM [會依據AEM和JCR所強加的慣例](/help/sites-developing/naming-conventions.md)驗證名稱。 您無法在&#x200B;**名稱**&#x200B;欄位中提交無效的字元。 當AEM偵測到無效字元時，該欄位將會以說明訊息強調顯示。

![caop-02](assets/caop-02.png)

>[!NOTE]
>
>除非是語言根，否則應避免使用ISO-639-1定義的雙字母代碼作為頁面名稱。
>
>如需詳細資訊，請參閱[準備翻譯內容](/help/sites-administering/tc-prep.md)。

### 範本 {#templates}

在AEM中，範本會指定特殊型別的頁面。 範本會用作任何建立新頁面的基礎。

範本定義包含縮圖影像和其他屬性的頁面結構。 例如，您可以為產品頁面、Sitemap和聯絡資訊使用不同的範本。 範本由[個元件](#components)組成。

AEM隨附數種現成可用的範本。 可用的範本視個別網站而定。 主要欄位包括：

* **標題**
在產生的網頁上顯示的標題。

* **名稱**
用於命名頁面。

* **範本**
可在產生新頁面時使用的範本清單。

>[!NOTE]
>
>若已在您的執行個體上設定，[範本作者可以使用範本編輯器](/help/sites-authoring/templates.md)建立範本。

### 元件 {#components}

元件是AEM所提供的元素，可供您新增特定型別的內容。 AEM隨附一系列[現成可用的元件](/help/sites-authoring/default-components-console.md)，提供完整的功能。 這些類別包括：

* 文字
* 影像
* Slideshow
* 影片
* 以及更多功能

建立並開啟頁面後，您就可以使用[元件瀏覽器](/help/sites-authoring/editing-content.md#insertinganewparagraph)提供的元件[來](/help/sites-authoring/author-environment-tools.md#componentbrowser)新增內容。

>[!NOTE]
>
>[元件主控台](/help/sites-authoring/default-components-console.md)提供您執行個體上元件的概觀。

## 管理頁面 {#managing-pages}

### 建立新頁面 {#creating-a-new-page}

除非所有頁面都已預先為您建立，否則您必須先建立頁面，然後才能開始建立內容：

1. 開啟Sites主控台(例如，[https://localhost:4502/sites.html/content](https://localhost:4502/sites.html/content))。
1. 導覽至您要建立新頁面的位置。
1. 使用工具列中的&#x200B;**Create**&#x200B;開啟下拉式選取器，然後從清單中選取&#x200B;**Page**：

   ![caop-03](assets/caop-03.png)

1. 從精靈的第一階段，您可以：

   * 選取您要用來建立新頁面的範本，然後按一下[下一步] **以繼續。**

   * **取消**&#x200B;以中止程式。

   ![caop-04](assets/caop-04.png)

1. 在精靈的最後階段，您可以：

   * 使用三個索引標籤來輸入您要指派給新頁面的[頁面屬性](/help/sites-authoring/editing-page-properties.md)，然後按一下[建立]&#x200B;**來實際建立頁面。**

   * 使用&#x200B;**上一步**&#x200B;返回範本選取範圍。

   主要欄位包括：

   * **標題**：

      * 這會向使用者顯示，且是強制性的。

   * **名稱**：

      * 這會用來產生URI。 如果未指定，則會從標題衍生名稱。
      * 如果您在建立頁面時提供頁面&#x200B;**Name**，AEM [會依據AEM和JCR所強加的慣例](/help/sites-developing/naming-conventions.md)驗證名稱。

      * 您&#x200B;**無法在**&#x200B;名稱&#x200B;**欄位中提交無效的字元**。 當AEM偵測到無效字元時，該欄位將會反白顯示，並顯示說明訊息以指出需要移除/取代的字元。

   >[!NOTE]
   >
   >請參閱[頁面命名慣例](#page-naming-conventions)。

   建立頁面所需的最少資訊是&#x200B;**標題**。

   ![caop-05](assets/caop-05.png)

1. 使用&#x200B;**建立**&#x200B;完成程式並建立新頁面。 確認對話方塊會詢問您是要立即&#x200B;**開啟**&#x200B;頁面，還是返回主控台（**完成**）：

   ![chlimage_1-118](assets/chlimage_1-118.png)

   >[!NOTE]
   >
   >如果您使用該位置已存在的名稱來建立頁面，系統將藉由附加一個編號來自動產生名稱的變體。 例如，如果`winter`已存在，則新頁面將變成`winter0`。

1. 如果您返回主控台，則會看到新頁面：

   ![caop-06](assets/caop-06.png)

>[!CAUTION]
>
>建立頁面後，無法變更其範本 — 除非您[使用新範本](/help/sites-authoring/launches-creating.md#create-launch-with-new-template)建立啟動項，不過這樣會遺失任何現有的內容。

### 開啟頁面進行編輯 {#opening-a-page-for-editing}

建立頁面或（在主控台中）導覽至現有頁面後，您可以開啟頁面進行編輯：

1. 開啟&#x200B;**網站**&#x200B;主控台。
1. 導覽至找到您要編輯的頁面為止。
1. 使用下列任一專案選取您的頁面：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#navigatingandselectionmode)和工具列

   然後選取&#x200B;**編輯**&#x200B;圖示：

   ![screen_shot_2018-03-22at105355](assets/screen_shot_2018-03-22at105355.png)

1. 此頁面將會開啟，您可以視需要[編輯頁面](/help/sites-authoring/editing-content.md#touchoptimizedui)。

>[!NOTE]
>
>只有在「預覽」模式中才能從頁面編輯器導覽至其他頁面，因為連結在「編輯」模式中無效。

### 複製和貼上頁面 {#copying-and-pasting-a-page}

您可以將頁面及其所有子頁面複製到新位置：

1. 在&#x200B;**Sites**&#x200B;主控台中，導覽至找到您要複製的頁面。
1. 使用以下其中一種方式選取您的頁面：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#navigatingandselectionmode)和工具列

   然後&#x200B;**複製**&#x200B;頁面圖示：

   ![screen_shot_2018-03-22at105425](assets/screen_shot_2018-03-22at105425.png)

   >[!NOTE]
   >
   >如果您處於選取模式，這會在頁面複製後立即自動退出。

1. 導覽至頁面新復本的位置。
1. **貼上**&#x200B;圖示可使用直接右側的下拉式箭頭顯示：

   ![貼上](assets/paste-without-children.png)

   下列兩個動作您可以擇一執行：
   * 選取&#x200B;**貼上**&#x200B;頁面圖示本身：將在此位置建立原始頁面及任何子頁面的復本。
   * 選取下拉箭頭以顯示不含子項的&#x200B;**貼上**&#x200B;選項。 將在此位置建立原始頁面的復本；不會複製子頁面。

   >[!NOTE]
   >
   >如果您將頁面複製到某個位置，而該位置已經存在名稱與原始名稱相同的頁面，則系統將藉由附加一個編號來自動產生名稱的變體。 例如，如果`winter`已經存在，`winter`將變成`winter1`。

### 移動或重新命名頁面 {#moving-or-renaming-a-page}

>[!NOTE]
>
>在指定新頁面名稱時，重新命名頁面也需遵循[頁面命名慣例](#page-naming-conventions)。

>[!NOTE]
>
>只能將頁面移至允許該頁面所依據的範本位置。 如需詳細資訊，請參閱[範本可用性](/help/sites-developing/templates.md#template-availability)。

移動或重新命名頁面的程式基本相同，並由同一精靈處理。 使用此精靈，您可以：

* 重新命名頁面而不移動頁面。
* 移動頁面而不重新命名。
* 同時移動和重新命名。

AEM提供可更新任何內部連結的功能，這些連結會參照正在重新命名/移動的頁面。 您可以逐頁進行，提供完整的彈性。

1. 導覽，直到找到您要移動的頁面為止。
1. 使用以下其中一種方式選取您的頁面：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#navigatingandselectionmode)和工具列

   然後選取「**移動**」頁面圖示：

   ![screen_shot_2018-03-22at105534](assets/screen_shot_2018-03-22at105534.png)

   這會開啟移動頁面精靈。

1. 精靈的&#x200B;**重新命名**&#x200B;步驟提供您&#x200B;**頁面相關資訊**，包括建立日期、路徑和直接參照數目。 您可從這裡：

   * 指定移動頁面後您要使用的名稱，然後按一下[下一步] **繼續。**
   * **取消**&#x200B;以中止程式。

   ![caop-07](assets/caop-07.png)

   如果您只移動頁面，頁面名稱可以維持不變。

   >[!NOTE]
   >
   >如果您將頁面移至相同名稱的頁面已經存在的位置，系統將藉由附加編號來自動產生名稱的變體。 例如，如果`winter`已經存在，`winter`將變成`winter1`。

1. 在精靈的&#x200B;**選取目的地**&#x200B;階段中，您可以：

   * 使用[欄檢視](/help/sites-authoring/basic-handling.md#column-view)瀏覽至頁面的新位置：

      * 按一下目的地的縮圖，以選取目的地。
      * 按一下[下一步]&#x200B;**&#x200B;**&#x200B;繼續。

   * 使用&#x200B;**上一步**&#x200B;返回頁面名稱規格。

   >[!NOTE]
   >
   >依預設，將會選取您要移動/重新命名的頁面的父頁面作為目的地。

   ![caop-08](assets/caop-08.png)

   >[!NOTE]
   >
   >如果您將頁面移至相同名稱的頁面已經存在的位置，系統將藉由附加編號來自動產生名稱的變體。 例如，如果`winter`已經存在，`winter`將變成`winter1`。

1. 如果頁面已連結或參考，或已發佈，則詳細資料將列在&#x200B;**調整/重新發佈**&#x200B;步驟中。

   您可以指出哪些頁面應適當地調整及/或重新發佈。

   >[!NOTE]
   >
   >* 如果頁面既未連結也未參考，則無法使用此步驟。
   >* 此步驟會列出直接和間接參照。 這可能與在精靈的&#x200B;**重新命名**&#x200B;步驟上報告的數量以及參考邊欄報告的參考不同，兩者都僅報告基於效能原因的直接參考。

   ![caop-09](assets/caop-09.png)

1. 選取「移動&#x200B;**&#x200B;**」將會完成程式，並視需要移動/重新命名您的頁面。

>[!NOTE]
>
>如果頁面已發佈，移動頁面會自動解除發佈。依預設，移動完成時會重新發佈它，但是這可透過取消勾選&#x200B;**調整/重新發佈**&#x200B;步驟中的&#x200B;**重新發佈**&#x200B;欄位來變更。

>[!NOTE]
>
>如果頁面未以任何方式參考，則會略過&#x200B;**調整/重新發佈**&#x200B;步驟。

#### 非同步動作 {#asynchronous-actions}

頁面移動動作一律會以非同步方式處理，讓使用者能不受阻礙地繼續在UI中編寫。

* 使用者必須定義何時應執行非同步操作
   * **現在**&#x200B;立即開始執行非同步工作。
   * **稍後**&#x200B;可讓使用者定義非同步工作何時開始。

  ![非同步頁面移動](assets/asynchronous-page-move.png)

可在&#x200B;[**全域導覽** > &#x200B;](/help/sites-administering/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations)工具&#x200B;**>**&#x200B;作業&#x200B;**>**&#x200B;作業&#x200B;**的**&#x200B;非同步作業狀態&#x200B;**儀表板**&#x200B;中檢查非同步作業的狀態

>[!NOTE]
>
>如需有關非同步作業處理以及如何設定頁面移動/重新命名動作限制的詳細資訊，請參閱「管理」使用指南中的[非同步作業](/help/sites-administering/asynchronous-jobs.md)檔案。

>[!NOTE]
>
>非同步頁面移動處理需要AEM 6.5.3.0或更新版本。

### 刪除頁面 {#deleting-a-page}

1. 導覽，直到您可以看見要刪除的頁面為止。
1. 使用[選取模式](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)來選取必要的頁面，然後使用工具列中的&#x200B;**刪除**：

   ![screen_shot_2018-03-22at105622](assets/screen_shot_2018-03-22at105622.png)

   >[!NOTE]
   >
   >為了安全起見，「刪 **&#x200B;**&#x200B;除」頁面圖示不能作為快速動作使用。

1. 對話方塊將會要求確認，使用：

   * **取消**&#x200B;以中止動作
   * **刪除**&#x200B;以確認動作：

      * 如果頁面沒有引用，則會刪除該頁面。
      * 如果頁面有參照，訊息方塊會通知您&#x200B;**已參照一或多個頁面。**&#x200B;您可以選取&#x200B;**強制刪除**&#x200B;或&#x200B;**取消**。

>[!NOTE]
>
>如果頁面已發佈，則在刪除前會自動取消發佈。

### 鎖定頁面 {#locking-a-page}

您可以從主控台或編輯個別頁面時[鎖定/解除鎖定頁面](/help/sites-authoring/editing-content.md#locking-a-page)。 有關鎖定頁面的資訊也會顯示在這兩個位置。

![screen_shot_2018-03-22at105713](assets/screen_shot_2018-03-22at105713.png) ![screen_shot_2018-03-22at105720](assets/screen_shot_2018-03-22at105720.png)

### 建立新資料夾 {#creating-a-new-folder}

您可以建立資料夾來協助組織您的檔案和頁面。

>[!NOTE]
>
>指定新資料夾名稱時，資料夾也須遵守[頁面命名慣例](#page-naming-conventions)。

>[!CAUTION]
>
>* 資料夾只能直接在&#x200B;**網站**&#x200B;或其他資料夾下建立。 無法在頁面下建立縮圖。
>* 您可以在資料夾上執行移動、複製、貼上、刪除、發佈、取消發佈和檢視/編輯屬性的標準動作。
>* 無法在即時副本中選取資料夾。
>

1. 開啟&#x200B;**網站**&#x200B;主控台，並導覽至所需位置。
1. 若要開啟選項清單，請從工具列選取&#x200B;**建立**
1. 選取&#x200B;**資料夾**&#x200B;以開啟對話方塊。 您可以在這裡輸入&#x200B;**名稱**&#x200B;和&#x200B;**標題**：

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. 選取&#x200B;**建立**&#x200B;以建立資料夾。
