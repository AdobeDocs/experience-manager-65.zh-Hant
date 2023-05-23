---
title: 建立和組織頁面
description: 本節介紹如何建立和管理頁AEM面，以便隨後可以在這些頁面上建立內容。
uuid: 47ce137a-7a85-4b79-b4e0-fdf08a9e77bd
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 14b8758b-f164-429a-b299-33b0703f8bec
exl-id: bd2636d1-6f13-4c6c-b8cd-3bed9e83a101
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 3%

---

# 建立及組織頁面{#creating-and-organizing-pages}

本節介紹如何使用Adobe Experience Manager()建立和管AEM理頁面，以便 [建立內容](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md) 那幾頁。

>[!NOTE]
>
>您的帳戶需要 [適當的訪問權限](/help/sites-administering/security.md) 和 [權限](/help/sites-administering/security.md#permissions) 對頁面執行操作，例如，建立、複製、移動、編輯和刪除。
>
>如果您遇到任何問題，我們建議您與系統管理員聯繫。

## 組織您的網站 {#organizing-your-website}

作為作者，您需要在中組織您的網AEM站。 這包括建立和命名內容頁，以便：

* 在作者環境中很容易找到
* 訪問您網站的訪問者可以輕鬆地在發佈環境中瀏覽這些網站

您還可以使用 [資料夾](#creating-a-new-folder) 來組織內容。

網站的結構可以看作 *樹結構* 保存內容頁面。 這些內容頁的名稱用於形成URL，而標題在查看頁面內容時顯示。

下面顯示了從Geometrixx站點的摘要；例如， `Triangle` 頁面：

* 作者環境

   `http://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

* 發佈環境

   `http://localhost:4503/content/geometrixx/en/products/triangle.html`

   根據實例的配置，使用 `/content` 在發佈環境中可能是可選的。

```xml
  /content
    /geometrixx
      /en
        /toolbar...
        /products
          /triangle
            /overview
            /features
          /square...
          /circle...
          /...
        /...
      /fr...
      /de...
      /es...
      /...
    /...
```

可以從網站控制台查看此結構，您可以使用它 [在樹結構中導航](/help/sites-classic-ui-authoring/author-env-basic-handling.md#main-pars-text-15)。

![chlimage_1-151](assets/chlimage_1-151.png)

### 頁面命名約定 {#page-naming-conventions}

建立新頁面時，有兩個鍵欄位：

* **[標題](#title)**:

   * 這將在控制台中顯示給用戶，並在編輯時顯示在頁面內容的頂部。
   * 此欄位為必填.

* **[名稱](#name)**:

   * 這用於生成URI。
   * 此欄位的用戶輸入是可選的。 如果未指定，則從標題派生名稱。

建立新頁面時AEM, [根據約定驗證頁名](/help/sites-developing/naming-conventions.md) 和JCRAEM強加的。

根據UI，實現和允許的字元清單略有不同（對於啟用觸摸的UI，它更加廣泛），但允許的最小值為：

* 「a」到「z」
* 「A」到「Z」
* 「0」到「9」
* _（下划線）
* `-` （連字元/減號）

如果希望確保接受/使用這些字元，請僅使用這些字元(如果需要所有允許字元的完整詳細資訊，請參閱 [命名約定](/help/sites-developing/naming-conventions.md))。

#### 標題 {#title}

如果您在建立新頁面時只提供頁面 **Title** ,AEM會從此字串衍生頁面 **Name**[ ，並根據AEM和JCR所強加的慣例來驗證名稱。](/help/sites-developing/naming-conventions.md)在兩個UI中a **標題** 將接受包含無效字元的欄位，但派生的名稱將包含無效字元。 例如：

| 標題 | 派生名稱 |
|---|---|
| 捨恩 | schoen.html |
| &amp;SC%&amp;;Ç+ | sc---c-.html |

#### 名稱 {#name}

如果您提供頁面 **名稱** 建立新頁面時，AEM將 [根據約定驗證名稱](/help/sites-developing/naming-conventions.md) 和JCRAEM強加的。

在經典UI中 **無法輸入無效字元** 的 **名稱** 的子菜單。

>[!NOTE]
>在啟用觸摸的UI中 **無法提交無效字元** 的 **名稱** 的子菜單。 檢測AEM到無效字元時，該欄位將突出顯示，並顯示一條說明性消息，指示需要刪除/替換的字元。

>[!NOTE]
>
>您應避免使用ISO-639-1定義的雙字母代碼，除非它是語言根。
>
>請參閱 [準備翻譯內容](/help/sites-administering/tc-prep.md) 的子菜單。

### 範本 {#templates}

在AEM中，模板指定專用的頁面類型。 模板將用作建立任何新頁面的基礎。

模板定義頁面結構；包括縮略圖和其他屬性。 例如，您可能有單獨的產品頁面、模板和聯繫資訊模板。 模板由 [元件](#components)。

附AEM帶了幾個現成的模板。 提供的模板取決於單個網站，需要提供的資訊（在建立新頁面時）取決於所使用的UI。 關鍵欄位為：

* **標題**
結果網頁上顯示的標題。

* **名稱**
在命名頁面時使用。

* **模板**
生成新頁時可用的模板清單。

### 元件 {#components}

元件是提供的元AEM素，以便您可以添加特定類型的內容。 AEM附帶一系列提供全面功能的現成元件；這些包括：

* 文字
* 影像
* Slideshow
* 影片
* 更多

建立並開啟頁面後，您可以 [使用元件添加內容](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#insertinganewparagraph)，可從 [側衛](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick)。

## 管理頁面 {#managing-pages}

### 建立新頁面 {#creating-a-new-page}

除非所有頁面都已預先為您建立，否則在開始建立內容之前，您必須建立一個頁面：

1. 從 **網站** console，選擇要建立新頁面的級別。

   在下例中，您正在級別下建立頁面 **產品**  — 顯示在左窗格中；右窗格顯示已存在於以下級別的頁面 **產品**。

   ![screen_shot_2012-02-15at114413am](assets/screen_shot_2012-02-15at114413am.png)

1. 在 **新建……** 菜單（按一下旁邊的箭頭） **新建……**)，選擇 **新建頁面……**。 的 **建立頁** 的下界。

   按一下 **新建……** 它本身也是一條捷徑 **新建頁面……** 的雙曲餘切值。

1. 的 **建立頁** 對話框允許您：

   * 提供 **標題**;這將顯示給用戶。
   * 提供 **名稱**;這用於生成URI。 如果未指定，則名稱將從標題派生。

      * 如果您提供頁面 **名稱** 建立新頁面時，AEM將 [根據約定驗證名稱](/help/sites-developing/naming-conventions.md) 和JCRAEM的。
      * 在經典UI中 **無法輸入無效字元** 的 **名稱** 的子菜單。
   * 按一下要用於建立新頁面的模板。

      模板用作新頁面的基礎；例如，確定內容頁面的基本佈局。
   >[!NOTE]
   >
   >請參閱 [頁面命名約定](#page-naming-conventions)。

   建立新頁面所需的最低資訊是 **標題** 和所需的模板。

   ![screen_shot_2012-02-15at114845am](assets/screen_shot_2012-02-15at114845am.png)

   >[!NOTE]
   >
   >如果要在URL中使用Unicode字元，請設定別名( `sling:alias`)屬性([頁屬性](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md))。

1. 按一下 **建立** 的子菜單。 返回到 **網站** 控制台，您可以在其中查看新頁的條目。

   控制台提供有關頁面（例如上次編輯頁面時和由誰編輯頁面時）的資訊，這些資訊將根據需要進行更新。

   >[!NOTE]
   >
   >編輯現有頁面時，也可以建立頁面。 使用**建立子頁** **頁面** 的子菜單。

### 開啟頁面進行編輯 {#opening-a-page-for-editing}

您可以開啟要 [編輯](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#editing-a-component-content-and-properties) 通過幾種方法：

* 從 **網站** 控制台， **按兩下** 開啟以供編輯的頁面條目。

* 從 **網站** 控制台， **按一下右鍵** （上下文菜單）頁項，然後選擇 **開啟** 的子菜單。

* 開啟頁面後，可通過按一下超連結導航到站點內的其他頁面（以編輯這些頁面）。

### 複製和貼上頁面 {#copying-and-pasting-a-page}

複製時，您可以複製以下任一項：

* 單頁
* 頁面及所有子頁

1. 從 **網站** 控制台，選擇要複製的頁面。

   >[!NOTE]
   >
   >在此階段，無論您是要複製單頁還是基礎子頁，都無關緊要。

1. 按一下 **複製**。

1. 導航到新位置，然後按一下：

   * **貼上**  — 將頁面與所有子頁面一起貼上
   * **Shift +貼上**  — 僅貼上選定的頁面

   頁面將貼上到新位置。

   >[!NOTE]
   >
   >如果現有頁面已具有相同名稱，則可能會自動調整頁面名稱。

   >[!NOTE]
   >
   >您還可以使用 **複製頁** 從 **頁面** 擊中了。 這將開啟一個對話框，您可以在其中指定目標等。

### 移動或更名頁 {#moving-or-renaming-page}

>[!NOTE]
>
>更名頁面也受 [頁面命名約定](#page-naming-conventions) 指定新頁名時。

移動或更名頁面的過程相同。 使用相同的操作，您可以：

* 將頁面移動到新位置
* 在同一位置更名頁面
* 將頁面移到新位置，並同時更名

提AEM供了更新要更名或移動的頁面的內部連結的功能。 這可以逐頁完成，以提供完全的靈活性。

要移動或更名頁面：

1. 觸發移動的方法有多種：

   * 從 **網站** 控制台，按一下選擇頁，然後選擇 **移動……**
   * 從 **網站** 控制台，您也可以選擇頁面項， **按一下右鍵** 選擇 **移動……**
   * 編輯頁面時，可以選擇 **移動頁面** 從 **頁面** 擊中了。

1. 的 **移動** 窗口；在此，您可以指定新位置，或為頁面指定新名稱，或同時指定兩者。

   ![screen_shot_2012-02-15at121336pm](assets/screen_shot_2012-02-15at121336pm.png)

   該頁面還列出引用所移動頁面的所有頁面。 根據引用頁面的狀態，您可能能夠調整頁面上的連結和/或重新發佈頁面。

1. 根據需要填寫以下欄位：

   * **目的地**

      使用站點地圖（可通過下拉選擇器獲得）選擇頁面應移動到的位置。

      如果僅更名頁面，請忽略此欄位。

   * **移動**

      指定要移動的頁面 — 預設情況下，這通常會被填充，具體取決於您啟動移動操作的方式和位置。

   * **重新命名為**

      預設情況下，將顯示當前頁面標籤。 如果需要，指定新頁面標籤。

   * **調整**

      更新所列指向已移動頁面的頁面上的連結：例如，如果頁A具有到頁B的連結，AEM則調整頁A中的連結以防您移動頁B。

      可以為每個單獨的引用頁選擇/取消選擇此選項。

   * **重新發佈**

      重新發佈引用頁面；同樣，可以為每個頁面選擇此選項。
   >[!NOTE]
   >
   >如果已激活頁面，則移動頁面將自動停用它。 預設情況下，移動完成時將重新激活它，但可以通過取消選中 **重新發佈** 中的 **移動** 的子菜單。

1. 按一下 **移動**。 需要確認。 按一下 **確定** 確認。

   >[!NOTE]
   >
   >將不更新頁面標題。

### 刪除頁面 {#deleting-a-page}

1. 可以從不同位置刪除頁面：

   * 在 **網站** 控制台，按一下選擇頁面，然後按一下右鍵並選擇 **刪除** 的上界。
   * 在 **網站** 控制台，按一下選擇頁，然後選擇 **刪除** 的子菜單。
   * 在旁邊使用 **頁面** 頁籤 **刪除頁**  — 這將刪除當前開啟的頁面。

1. 選擇刪除頁面後，必須確認請求 — 因為操作無法撤消。

   >[!NOTE]
   >
   >刪除後，如果已發佈該頁面，則可以恢復最新（或特定）版本，但如果進行了進一步修改，則其內容可能與上次版本不完全相同。 請參閱 [如何還原頁面](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoringpages) 的上界。

>[!NOTE]
>
>如果已激活某個頁面，則在刪除前將自動停用該頁面。

### 鎖定頁面 {#locking-a-page}

你可以 [鎖定/解鎖頁面](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#locking-a-page) 從控制台或編輯單個頁面時。 有關頁面是否已鎖定的資訊也顯示在這兩個位置。

### 建立新資料夾 {#creating-a-new-folder}

>[!NOTE]
>
>資料夾也受 [頁面命名約定](#page-naming-conventions) 指定新資料夾名稱時。

1. 開啟 **網站** 控制台並導航到所需位置。
1. 在 **新建……** 菜單（按一下旁邊的箭頭） **新建……**)，選擇 **新建資料夾……**。
1. 的 **建立資料夾** 對話框。 在此，您可以輸入 **名稱** 和 **標題**:

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. 選擇 **建立** 的子菜單。
