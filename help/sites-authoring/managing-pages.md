---
title: 建立及組織頁面
description: 如何使用AEM建立和管理頁面
translation-type: tm+mt
source-git-commit: 90364cdf6044616d43c1851b3def9b1f063449ca
workflow-type: tm+mt
source-wordcount: '2523'
ht-degree: 6%

---


# 建立及組織頁面 {#creating-and-organizing-pages}

本節說明如何使用Adobe Experience Manager(AEM)建立和管理頁面，以便您接著可以[在這些頁面上建立內容](/help/sites-authoring/editing-content.md)。

>[!NOTE]
>
>您的帳戶需要[適當的存取權限](/help/sites-administering/security.md)和[權限](/help/sites-administering/security.md#permissions)才能在建立、複製、移動、編輯和刪除等頁面上採取動作。
>
>如果您遇到任何問題，我們建議您與系統管理員聯繫。

>[!NOTE]
>
>您可從網站主控台使用許多[鍵盤快速鍵](/help/sites-authoring/keyboard-shortcuts.md)，讓組織頁面更有效率。

## 組織您的網站{#organizing-your-website}

身為作者，您將需要在AEM中組織您的網站。 這包括建立和命名您的內容頁面，以便：

* 您可在作者環境中輕鬆找到它們
* 瀏覽您網站的訪客可在發佈環境中輕鬆瀏覽他們

您也可以使用[資料夾](#creating-a-new-folder)協助組織您的內容。

網站的結構可視為包含您內容頁面的樹狀結構。 這些內容頁面的名稱用於形成URL，而標題則會在檢視頁面內容時顯示。

以下顯示We.Retail網站的範例，可存取遠足短褲頁面(`desert-sky-shorts`):

* 作者環境
   `https://localhost:4502/editor.html/content/we-retail/us/en/products/equipment/hiking/desert-sky-shorts.html`

* 發佈環境
   `https://localhost:4503/content/we-retail/us/en/products/equipment/hiking/desert-sky-shorts.html`

根據實例的配置，在發佈環境中使用`/content`可能是可選的。

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

此結構可從&#x200B;**Sites**&#x200B;主控台檢視，您可在此處[瀏覽您網站的頁面，並在頁面上執行動作。 ](/help/sites-authoring/basic-handling.md#navigating)您也可以建立新網站和[新頁面](#creating-a-new-page)。

從任何點上，您都可從標題列的階層連結中看到向上的分支：

![caop-01](assets/caop-01.png)

### 頁面命名慣例{#page-naming-conventions}

建立新頁面時，有兩個鍵字欄位：

* **[標題](#title)**:

   * 這會在主控台中向使用者顯示，並在編輯時顯示在頁面內容的頂端。
   * 此欄位為必填.

* **[名稱](#name)**:

   * 這用於生成URI。
   * 此欄位的使用者輸入為選擇性。 如果未指定，則名稱是從標題衍生而來。 如需詳細資訊，請參閱以下章節[頁面名稱限制和最佳實務](/help/sites-authoring/managing-pages.md#page-name-restrictions-and-best-practices)。

#### 頁面名稱限制與最佳實務{#page-name-restrictions-and-best-practices}

頁面 **標題****和名稱可以單獨建立** ，但是是相關的：

* 建立頁面時，只需&#x200B;**Title**&#x200B;欄位。 如果建立頁面時未提供&#x200B;**Name**,AEM將從標題的前64個字元產生名稱（遵循下列的驗證）。 僅使用前64個字元，以支援簡短頁面名稱的最佳實務。

* 如果作者手動指定頁面名稱，則64個字元的限制不適用，但頁面名稱長度的其他技術限制可能不適用。

>[!NOTE]
>
>定義頁面名稱時，最佳的經驗法則是保持頁面名稱簡短，但盡可能具表現力和記憶力，讓讀者更容易理解。 如需詳細資訊，請參閱`title`元素的[W3C樣式指南](https://www.w3.org/Provider/Style/TITLE.html)。
>
>同時請記住，有些瀏覽器（例如舊版IE）只能接受一定長度的URL，因此也有技術理由保留頁面名稱簡短。

建立新頁面時，AEM會根據AEM和JCR所強加的慣例[驗證頁面名稱。](/help/sites-developing/naming-conventions.md)

允許的字元數量下限為：

* &#39;a&#39;到&#39;z&#39;
* A到Z
* &#39;0&#39;到&#39;9&#39;
* `_` （底線）
* `-` （連字型大小／減號）

[命名約定](/help/sites-developing/naming-conventions.md)中可找到所有允許字元的完整詳細資訊。

>[!NOTE]
>
>如果AEM在[MongoMK永續性管理器部署](/help/sites-deploying/recommended-deploys.md)上執行，則頁面名稱限制為150個字元。

#### 標題 {#title}

如果您在建立新頁面時只提供頁面 **Title** ,AEM會從此字串衍生頁面 **Name**[ ，並根據AEM和JCR所強加的慣例來驗證名稱。](/help/sites-developing/naming-conventions.md)將接受包含無效字元的&#x200B;**Title**&#x200B;欄位，但派生的名稱將替換無效字元。 例如：

| 標題 | 衍生名稱 |
|---|---|
| 捨恩 | schoen.html |
| SC%&amp;*ç+ | sc---c-.html |

#### 名稱 {#name}

當您建立新頁面時提供頁面&#x200B;**Name**&#x200B;時，AEM會根據AEM和JCR所強制的慣例[驗證名稱。 ](/help/sites-developing/naming-conventions.md)您不能在&#x200B;**Name**&#x200B;欄位中提交無效字元。 當AEM偵測到無效字元時，欄位會以說明性訊息反白顯示。

![caop-02](assets/caop-02.png)

>[!NOTE]
>
>您應避免使用由ISO-639-1定義的雙字母代碼作為頁面名稱，除非它是語言根目錄。
>
>有關詳細資訊，請參閱[準備翻譯內容](/help/sites-administering/tc-prep.md)。

### 範本 {#templates}

在AEM中，範本會指定專用的頁面類型。 範本將用作建立任何新頁面的基礎。

範本會定義包含縮圖影像和其他屬性的頁面結構。 例如，您可能有個別的產品頁面、網站地圖和連絡資訊範本。 範本由[元件](#components)組成。

AEM隨附數個現成可用的範本。 可用的範本取決於個別網站。 主要欄位包括：

* **標**
題顯示在結果網頁上的標題。

* **命名**
頁面時使用的名稱。

* **范**
本產生新頁面時可用的範本清單。

>[!NOTE]
>
>如果在實例上配置了[模板作者，則可以使用模板編輯器](/help/sites-authoring/templates.md)建立模板。

### 元件 {#components}

元件是AEM提供的元素，讓您可以新增特定類型的內容。 AEM隨附一系列[現成可用的元件](/help/sites-authoring/default-components-console.md)，提供完整的功能。 其中包括：

* 文字
* 影像
* Slideshow
* 影片
* 還有更多

建立並開啟頁面後，您就可使用](/help/sites-authoring/editing-content.md#insertinganewparagraph)元件瀏覽器[提供的元件[新增內容。](/help/sites-authoring/author-environment-tools.md#componentbrowser)

>[!NOTE]
>
>[Components Console](/help/sites-authoring/default-components-console.md)提供實例上元件的概述。

## 管理頁面{#managing-pages}

### 建立新頁面{#creating-a-new-page}

除非所有頁面都事先已為您建立，否則您必須先建立頁面，才能開始建立內容：

1. 開啟網站主控台(例如[https://localhost:4502/sites.html/content](https://localhost:4502/sites.html/content))。
1. 導覽至您要建立新頁面的位置。
1. 使用工具列中的「建立」 **** ，開啟下拉式選取器，然後從清單中選 **取「頁面** 」:

   ![caop-03](assets/caop-03.png)

1. 從精靈的第一階段，您可以：

   * 選擇您要用來建立新頁面的範本，然後按一下／點選&#x200B;**Next**&#x200B;繼續。

   * **取消** 以中止進程。

   ![caop-04](assets/caop-04.png)

1. 從精靈的最後階段，您可以：

   * 使用這三個標籤輸入要指派給新頁面的[頁面屬性](/help/sites-authoring/editing-page-properties.md)，然後按一下／點選&#x200B;**建立**&#x200B;以實際建立頁面。

   * 使用&#x200B;**Back**&#x200B;返回到模板選擇。

   主要欄位包括：

   * **標題**:

      * 這會顯示給使用者，而且是必備的。
   * **名稱**:

      * 這用於生成URI。 如果未指定，則名稱是從標題衍生而來。
      * 如果您在建立新頁面時提供頁面&#x200B;**Name**,AEM會根據AEM和JCR所強制的慣例[驗證名稱。](/help/sites-developing/naming-conventions.md)

      * **無法在**&#x200B;名稱&#x200B;**欄位中提交無效字元**。 當AEM偵測到無效字元時，欄位會反白顯示，並顯示說明訊息，指出需要移除／取代的字元。
   >[!NOTE]
   >
   >請參閱[頁面命名慣例](#page-naming-conventions)。

   建立新頁面所需的最低資訊為&#x200B;**Title**。

   ![caop-05](assets/caop-05.png)

1. 使用&#x200B;**Create**&#x200B;完成流程並建立新頁面。 確認對話框將詢問您是要立即&#x200B;**開啟**&#x200B;頁面，還是返回控制台(**Done**):

   ![chlimage_1-118](assets/chlimage_1-118.png)

   >[!NOTE]
   >
   >如果您使用該位置已存在的名稱建立頁面，系統將通過附加數字自動生成名稱的變化。 例如，如果`winter`已存在，則新頁面將變為`winter0`。

1. 如果您返回主控台，您會看到新頁面：

   ![caop-06](assets/caop-06.png)

>[!CAUTION]
>
>建立頁面後，其範本便無法變更——除非您[使用新範本](/help/sites-authoring/launches-creating.md#create-launch-with-new-template)建立啟動，但這會遺失任何已存在的內容。

### 開啟頁面進行編輯{#opening-a-page-for-editing}

建立頁面或導覽至現有頁面（在主控台中）後，您可以開啟它以進行編輯：

1. 開啟&#x200B;**Sites**&#x200B;控制台。
1. 導覽，直到您找到要編輯的頁面。
1. 使用下列任一項來選取您的頁面：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選取](/help/sites-authoring/basic-handling.md#navigatingandselectionmode) 模式和工具列

   然後選擇&#x200B;**編輯**&#x200B;表徵圖：

   ![screen_shot_2018-03-22at105355](assets/screen_shot_2018-03-22at105355.png)

1. 頁面將會開啟，您可以視需要編輯頁面[。](/help/sites-authoring/editing-content.md#touchoptimizedui)

>[!NOTE]
>
>只有在「預覽」模式下，才能從頁面編輯器導航到其他頁面，因為連結在「編輯」模式下不處於活動狀態。

### 複製和貼上頁面{#copying-and-pasting-a-page}

您可以將頁面及其所有子頁面複製到新位置：

1. 在&#x200B;**Sites**&#x200B;主控台中，導覽直到您找到要複製的頁面。
1. 使用下列任一項選擇您的頁面：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選取](/help/sites-authoring/basic-handling.md#navigatingandselectionmode) 模式和工具列

   然後，**Copy**&#x200B;頁面圖示：

   ![screen_shot_2018-03-22at105425](assets/screen_shot_2018-03-22at105425.png)

   >[!NOTE]
   >
   >如果您處於選擇模式，則複製頁面時，系統會立即自動退出。

1. 導覽至頁面新復本的位置。
1. **貼上**&#x200B;圖示可用，右側是下拉箭頭：

   ![貼上](assets/paste-without-children.png)

   您可以:
   * 選擇&#x200B;**貼上**&#x200B;頁面圖示本身：將在此位置建立原始頁面和任何子頁面的副本。
   * 選擇下拉箭頭以顯示「不含子代的貼上」選項。 ****&#x200B;原始頁面的復本將在此位置建立；子頁面將不會複製。

   >[!NOTE]
   >
   >如果將頁面複製到與原始頁面同名的頁面已存在的位置，系統會通過附加數字自動生成名稱的變化。 例如，如果`winter`已存在`winter`，則會變成`winter1`。

### 移動或更名頁面{#moving-or-renaming-a-page}

>[!NOTE]
>
>在指定新頁面名稱時，重新命名頁面也應遵循[頁面命名慣例](#page-naming-conventions)。

>[!NOTE]
>
>頁面只能移動到允許基於該頁面的模板的位置。 如需詳細資訊，請參閱[範本可用性](/help/sites-developing/templates.md#template-availability)。

移動或更名頁面的過程基本相同，由同一嚮導處理。 使用此嚮導，您可以：

* 重新命名頁面，而不移動它。
* 移動頁面而不重新命名。
* 同時移動和重新命名。

AEM提供您更新任何參照重新命名／移動之頁面的內部連結的功能。 這可逐頁執行，以提供完整的彈性。

1. 導覽，直到您找到要移動的頁面。
1. 使用下列任一項選擇您的頁面：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選取](/help/sites-authoring/basic-handling.md#navigatingandselectionmode) 模式和工具列

   然後選擇&#x200B;**Move**&#x200B;頁面表徵圖：

   ![screen_shot_2018-03-22at105534](assets/screen_shot_2018-03-22at105534.png)

   這將開啟移動頁嚮導。

1. 在嚮導的&#x200B;**Rename**&#x200B;階段中，您可以執行以下任一操作：

   * 指定在頁面移動後您想要擁有的名稱，然後按一下／點選&#x200B;**Next**&#x200B;繼續。

   * **取消** 以中止進程。

   ![caop-07](assets/caop-07.png)

   如果您只移動頁面，頁面名稱可維持不變。

   >[!NOTE]
   >
   >如果您將頁面移至已有相同名稱之頁面的位置，系統會附加數字以自動產生名稱的變更。 例如，如果`winter`已存在`winter`，則會變成`winter1`。

1. 在嚮導的&#x200B;**選擇目標**&#x200B;階段中，您可以執行以下操作：

   * 使用[列視圖](/help/sites-authoring/basic-handling.md#column-view)導航到頁面的新位置：

      * 按一下目標的縮略圖，選擇目標。
      * 按一下&#x200B;**Next**&#x200B;繼續。
   * 使用&#x200B;**Back**&#x200B;返回頁面名稱規範。

   >[!NOTE]
   >
   >依預設，您要移動／重新命名的頁面的父項會被選取為目標。

   ![caop-08](assets/caop-08.png)

   >[!NOTE]
   >
   >如果您將頁面移至已有相同名稱之頁面的位置，系統會附加數字以自動產生名稱的變更。 例如，如果`winter`已存在`winter`，則會變成`winter1`。

1. 如果頁面已連結或參考，或已發佈，則詳細資訊將列在&#x200B;**調整／重新發佈**&#x200B;步驟中。

   您可以指出應視需要調整和／或重新發佈哪些內容。

   >[!NOTE]
   >
   >如果頁面既未連結也未參考，則此步驟將無法使用。

   ![caop-09](assets/caop-09.png)

1. 選擇&#x200B;**Move**&#x200B;將完成該過程並根據需要移動／更名頁面。

>[!NOTE]
>
>如果頁面已發佈，移動頁面會自動解除發佈。預設情況下，移動完成時將重新發佈，但可以通過取消選中&#x200B;**調整／重新發佈**&#x200B;步驟中的&#x200B;**重新發佈**&#x200B;欄位來更改。

>[!NOTE]
>
>如果頁面未以任何方式參考，則會跳過&#x200B;**調整／重新發佈**&#x200B;步驟。

#### 非同步動作{#asynchronous-actions}

通常頁面移動或重新命名動作會立即執行。 這會視為同步處理，而UI中的進一步動作會遭到封鎖，直到動作完成為止。

不過，如果受影響的頁數超過定義的限制，動作會以非同步方式處理，讓使用者可不受頁面移動或重新命名動作的影響，在UI中繼續製作。

* 當按一下上述最後一個步驟中的&#x200B;**Move**&#x200B;時，AEM會檢查已設定的限制。
* 如果受影響的頁數低於限制，則會執行同步作業。
* 如果受影響的頁數超過限制，則會執行非同步作業。
   * 用戶必須定義何時應執行非同步操作
      * **現在** 會立即開始執行非同步作業。
      * **此** 外，還允許用戶定義非同步作業的啟動時間。

         ![非同步頁面移動](assets/asynchronous-page-move.png)

在&#x200B;[**非同步作業狀態**&#x200B;儀表板](/help/sites-administering/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations)的&#x200B;**全局導航** ->**工具** ->**操作** -> **作業**&#x200B;中，可以檢查非同步作業的狀態

>[!NOTE]
>
>有關非同步作業處理以及如何配置頁面移動／更名操作限制的詳細資訊，請參閱「管理」使用手冊中的[非同步作業](/help/sites-administering/asynchronous-jobs.md)文檔。

>[!NOTE]
>
>非同步頁面移動處理需要AEM 6.5.3.0或更新版本。

### 刪除頁面{#deleting-a-page}

1. 導覽，直到您看到要刪除的頁面。
1. 使用[選擇模式](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)選擇所需頁面，然後使用工具欄中的&#x200B;**刪除**:

   ![screen_shot_2018-03-22at105622](assets/screen_shot_2018-03-22at105622.png)

   >[!NOTE]
   >
   >為了安全起見，「刪 **** 除」頁面圖示不能作為快速動作使用。

1. 有對話方塊會要求您確認，請使用:

   * **取消**&#x200B;來中止動作
   * **刪除**&#x200B;來確認動作：

      * 如果頁面沒有任何參考，則會刪除頁面。
      * 如果頁面有參考，則會出現訊息方塊通知您&#x200B;**已參考一或多個頁面。**&#x200B;您可以選取&#x200B;**強制刪除**&#x200B;或&#x200B;**取消**。

>[!NOTE]
>
>如果頁面已發佈，則會在刪除前自動取消發佈。

### 鎖定頁面{#locking-a-page}

您可以從控制台或編輯個別頁面時，[鎖定／解除鎖定頁面](/help/sites-authoring/editing-content.md#locking-a-page)。 有關頁面是否被鎖定的資訊也會顯示在這兩個位置。

![screen_shot_2018-03-22at105713](assets/screen_shot_2018-03-22at105713.png) ![screen_shot_2018-03-22at105720](assets/screen_shot_2018-03-22at105720.png)

### 建立新資料夾{#creating-a-new-folder}

您可以建立檔案夾，協助組織您的檔案和頁面。

>[!NOTE]
>
>指定新資料夾名稱時，資料夾也受[頁面命名約定](#page-naming-conventions)的約束。

>[!CAUTION]
>
>* 只能在&#x200B;**Sites**&#x200B;下或在其他資料夾下建立資料夾。 無法在頁面下建立。
>* 標準動作可在資料夾上執行移動、複製、貼上、刪除、發佈、取消發佈和檢視／編輯屬性。
>* 資料夾不可用於即時拷貝中的選擇。

>



1. 開啟&#x200B;**Sites**&#x200B;控制台並導航到所需位置。
1. 要開啟選項清單，請從工具欄中選擇&#x200B;**建立**
1. 選擇&#x200B;**資料夾**&#x200B;以開啟對話框。 在此處，您可以輸入&#x200B;**Name**&#x200B;和&#x200B;**Title**:

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. 選擇&#x200B;**建立**&#x200B;以建立資料夾。
