---
title: 建立及組織頁面
description: 本節說明如何使用AEM建立和管理頁面，以便您接著在這些頁面上建立內容。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
exl-id: bd2636d1-6f13-4c6c-b8cd-3bed9e83a101
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1892'
ht-degree: 1%

---

# 建立及組織頁面{#creating-and-organizing-pages}

本節說明如何使用Adobe Experience Manager (AEM)建立和管理頁面，以便您之後可以 [建立內容](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md) 這些頁面上的。

>[!NOTE]
>
>您的帳戶需要 [適當的存取許可權](/help/sites-administering/security.md) 和 [許可權](/help/sites-administering/security.md#permissions) 在頁面上執行動作，例如，建立、複製、移動、編輯、刪除。
>
>如果您遇到任何問題，我們建議您連絡系統管理員。

## 組織您的網站 {#organizing-your-website}

身為作者，您必須在AEM中組織您的網站。 這涉及建立和命名內容頁面，以便：

* 您可以在作者環境中輕鬆找到他們
* 您網站的訪客可以輕鬆地在發佈環境中瀏覽它們

您也可以使用 [資料夾](#creating-a-new-folder) 協助組織您的內容。

網站的結構可視為一個 *樹狀結構* 內含內容頁面的物件。 這些內容頁面的名稱會用於組成URL，而標題則會在您檢視頁面內容時顯示。

以下顯示從Geometrixx網站擷取的內容；例如 `Triangle` 將會存取頁面：

* 作者環境

  `http://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

* 發佈環境

  `http://localhost:4503/content/geometrixx/en/products/triangle.html`

  根據您執行個體的設定，使用 `/content` 在發佈環境中可能是選用的。

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

此結構可從網站主控台檢視，您可將它用於 [瀏覽樹狀結構](/help/sites-classic-ui-authoring/author-env-basic-handling.md#main-pars-text-15).

![chlimage_1-151](assets/chlimage_1-151.png)

### 頁面命名慣例 {#page-naming-conventions}

建立頁面時，有兩個索引鍵欄位：

* **[標題](#title)**:

   * 主控台會向使用者顯示這項資訊，並在編輯時顯示在頁面內容的頂端。
   * 此欄位為必填.

* **[名稱](#name)**:

   * 這會用來產生URI。
   * 此欄位的使用者輸入為選用。 如果未指定，則會從標題衍生名稱。

建立頁面時，AEM [根據慣例驗證頁面名稱](/help/sites-developing/naming-conventions.md) 由AEM和JCR所強制。

實作和允許的字元清單因UI而略有不同（觸控式UI允許範圍更廣），但允許的最低字元為：

* &#39;a&#39;到&#39;z&#39;
* &#39;A&#39;到&#39;Z&#39;
* &#39;0&#39;到&#39;9&#39;
* _ （底線）
* `-` （連字型大小/減號）

如果您想要確定這些字元會被接受/使用(如果您需要所有允許字元的完整詳細資訊，請參閱 [命名慣例](/help/sites-developing/naming-conventions.md))。

#### 標題 {#title}

如果您只提供頁面 **標題** 建立頁面時，AEM會衍生頁面 **名稱** 來自此字串和 [根據慣例驗證名稱](/help/sites-developing/naming-conventions.md) 由AEM和JCR所強制。 在這兩個UI中 **標題** 系統將接受包含無效字元的欄位，但衍生的名稱會取代無效字元。 例如：

| 標題 | 衍生名稱 |
|---|---|
| Schon | schoen.html |
| SC%&amp;&amp;ast；c+ | sc---c-.html |

#### 名稱 {#name}

如果您提供頁面 **名稱** 建立頁面時，AEM [根據慣例驗證名稱](/help/sites-developing/naming-conventions.md) 由AEM和JCR所強制。

在Classic UI中，您 **無法輸入無效的字元** 在 **名稱** 欄位。

>[!NOTE]
>在觸控式UI中，您 **無法提交無效的字元** 在 **名稱** 欄位。 當AEM偵測到無效字元時，將會反白顯示欄位，並顯示說明訊息，指出需要移除/取代的字元。

>[!NOTE]
>
>除非是語言根，否則應避免使用ISO-639-1定義的雙字母代碼。
>
>另請參閱 [準備翻譯內容](/help/sites-administering/tc-prep.md) 以取得詳細資訊。

### 範本 {#templates}

在AEM中，範本會指定特殊型別的頁面。 範本會用作任何建立新頁面的基礎。

範本定義頁面的結構，包括縮圖影像和其他屬性。 例如，您可以為產品頁面、Sitemap和聯絡資訊使用不同的範本。 範本包括 [元件](#components).

AEM隨附幾個現成可用的範本。 提供的範本取決於個別網站，而需要提供的資訊（建立新頁面時）取決於使用的UI。 主要欄位包括：

* **標題**
在產生的網頁上顯示的標題。

* **名稱**
用於命名頁面。

* **範本**
可在產生新頁面時使用的範本清單。

### 元件 {#components}

元件是AEM提供的元素，可供您新增特定型別的內容。 AEM隨附一系列現成可用的元件，提供完善的功能；這些元件包括：

* 文字
* 影像
* Slideshow
* 影片
* 更多專案

建立並開啟頁面後，您可以 [使用元件新增內容](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#insertinganewparagraph)，可從取得 [sidekick](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick).

## 管理頁面 {#managing-pages}

### 建立新頁面 {#creating-a-new-page}

除非所有頁面都已預先為您建立，否則您必須先建立頁面，然後才能開始建立內容：

1. 從 **網站** 控制檯中，選取您要建立頁面的層級。

   在下列範例中，您會在層級下建立頁面 **產品**  — 顯示在左窗格中；右窗格顯示已存在於下列層級的頁面 **產品**.

   ![screen_shot_2012-02-15at114413am](assets/screen_shot_2012-02-15at114413am.png)

1. 在 **新增……** 功能表（按一下旁邊的箭頭） **新增……**)，選取 **新增頁面……**. 此 **建立頁面** 視窗會開啟。

   按一下 **新增……** 本身也可做為的捷徑 **新增頁面……** 選項。

1. 此 **建立頁面** 對話方塊可讓您：

   * 提供 **標題**；這會向使用者顯示。
   * 提供 **名稱**；這可用來產生URI。 如果未指定，則會從標題衍生名稱。

      * 如果您提供頁面 **名稱** 建立頁面時，AEM [根據慣例驗證名稱](/help/sites-developing/naming-conventions.md) 由AEM和JCR佔用。
      * 在傳統UI中 **無法輸入無效的字元** 在 **名稱** 欄位。

   * 按一下您要用來建立新頁面的範本。

     範本是用作新頁面的基礎；例如，用來決定內容頁面的基本版面。

   >[!NOTE]
   >
   >另請參閱 [頁面命名慣例](#page-naming-conventions).

   建立頁面所需的最低資訊為 **標題** 以及所需的範本。

   ![screen_shot_2012-02-15at114845am](assets/screen_shot_2012-02-15at114845am.png)

   >[!NOTE]
   >
   >如果您想要在URL中使用Unicode字元，請設定別名( `sling:alias`)屬性([頁面屬性](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md))。

1. 按一下 **建立** 以建立頁面。 您會返回 **網站** 主控台，您可在此檢視新頁面的專案。

   主控台會視需要提供頁面相關資訊（例如上次編輯時間及更新者）。

   >[!NOTE]
   >
   >您也可以在編輯現有頁面時建立頁面。 使用 **建立子頁面** 從 **頁面** sidekick的索引標籤會直接在正在編輯的頁面下方建立頁面。

### 開啟頁面進行編輯 {#opening-a-page-for-editing}

您可以開啟頁面以 [已編輯](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#editing-a-component-content-and-properties) 方法如下：

* 從 **網站** 主控台，您可以 **按兩下** 開啟以進行編輯的頁面專案。

* 從 **網站** 主控台，您可以 **按一下右鍵** （快顯功能表）頁面專案，然後選取 **開啟** 功能表中。

* 開啟頁面後，您可以按一下超連結，導覽至網站內的其他頁面（以進行編輯）。

### 複製和貼上頁面 {#copying-and-pasting-a-page}

複製時，您可以複製：

* 單次頁面
* 包含所有子頁面的頁面

1. 從 **網站** 控制檯中，選取您要複製的頁面。

   >[!NOTE]
   >
   >在此階段，不論您是要複製單一頁面，還是複製基礎子頁面，都無關緊要。

1. 按一下 **複製**.

1. 導覽至新位置，然後按一下：

   * **貼上**  — 貼上頁面及所有子頁面
   * **Shift +貼上**  — 僅貼上選取的頁面

   頁面會貼到新位置。

   >[!NOTE]
   >
   >如果現有頁面已有相同名稱，頁面名稱可能會自動調整。

   >[!NOTE]
   >
   >您也可以使用 **複製頁面** 從 **頁面** 索引標籤。 這會開啟一個對話方塊，您可以在其中指定目的地等等。

### 移動或重新命名頁面 {#moving-or-renaming-page}

>[!NOTE]
>
>重新命名頁面也必須遵循 [頁面命名慣例](#page-naming-conventions) 指定新頁面名稱時。

移動或重新命名頁面的程式相同。 透過相同的動作，您可以：

* 將頁面移至新位置
* 重新命名相同位置的頁面
* 將頁面移至新位置並同時重新命名

AEM提供更新要重新命名或移動之頁面的內部連結的功能。 您可以逐頁進行，提供完整的彈性。

若要移動或重新命名頁面：

1. 觸發移動的方法有很多：

   * 從 **網站** 主控台，按一下以選取頁面，然後選取 **移動……**
   * 從 **網站** 控制檯中，您也可以選取頁面專案，然後 **按一下右鍵** 並選取 **移動……**
   * 編輯頁面時，您可以選取 **移動頁面** 從 **頁面** 索引標籤。

1. 此 **移動** 視窗會開啟；您可以在此指定新位置、頁面的新名稱或兩者。

   ![screen_shot_2012-02-15at121336pm](assets/screen_shot_2012-02-15at121336pm.png)

   頁面也會列出參照所移動頁面的頁面。 根據參照頁面的狀態，您或許可以調整這些連結和/或重新發佈頁面。

1. 視情況填寫下列欄位：

   * **目的地**

     使用Sitemap （可透過下拉式選擇器取得）來選取頁面應該移動到的位置。

     如果您只重新命名頁面，請忽略此欄位。

   * **移動**

     指定要移動的頁面 — 這通常會根據您啟動移動動作的方式和位置預設填入。

   * **重新命名為**

     依預設，目前頁面標籤會顯示。 視需要指定新頁面標籤。

   * **調整**

     更新列出頁面上指向已移動頁面的連結：例如，如果頁面A有頁面B的連結，AEM會調整頁面A的連結，以防您移動頁面B。

     可以為每個單獨引用頁面選擇/取消選擇此選項。

   * **重新發佈**

     重新發佈引用頁面；再次可以為每個單獨頁面選擇此選項。

   >[!NOTE]
   >
   >如果頁面已啟動，移動頁面會自動將其停用。 依預設，移動完成時會將其重新啟用，但您可以取消勾選 **重新發佈** 中的頁面欄位 **移動** 視窗。

1. 按一下 **移動**. 需要確認。 按一下 **確定** 以確認。

   >[!NOTE]
   >
   >不會更新頁面標題。

### 刪除頁面 {#deleting-a-page}

1. 您可以從各種位置刪除頁面：

   * 在 **網站** 主控台，按一下以選取頁面，然後按一下右鍵並選取 **刪除** 從產生的功能表。
   * 在 **網站** 主控台，按一下以選取頁面，然後選取 **刪除** 工具列功能表中的。
   * 在sidekick中使用 **頁面** 標籤以選取 **刪除頁面**  — 這將會刪除目前開啟的頁面。

1. 選取刪除頁面後，您必須確認請求，因為動作無法復原。

   >[!NOTE]
   >
   >刪除後，如果頁面已發佈，您可以還原最新（或特定）版本，但若已進行進一步修改，此版本的內容可能會與您的上一個版本不完全相同。 另請參閱 [如何還原頁面](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoringpages) 以取得更多詳細資料。

>[!NOTE]
>
>如果頁面已啟動，則在刪除前會自動將其停用。

### 鎖定頁面 {#locking-a-page}

您可以 [鎖定/解鎖頁面](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#locking-a-page) 從主控台或編輯個別頁面時。 有關鎖定頁面的資訊也會顯示在這兩個位置。

### 建立新資料夾 {#creating-a-new-folder}

>[!NOTE]
>
>資料夾也必須遵守 [頁面命名慣例](#page-naming-conventions) 指定新資料夾名稱時。

1. 開啟 **網站** 主控台並導覽至所需位置。
1. 在 **新增……** 功能表（按一下旁邊的箭頭） **新增……**)，選取 **新增資料夾……**.
1. 此 **建立資料夾** 對話方塊開啟。 您可在此輸入 **名稱** 和 **標題**：

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. 選取 **建立** 以建立資料夾。
