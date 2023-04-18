---
title: 建立和組織頁面
description: 本節說明如何使用AEM建立和管理頁面，以便您接著在這些頁面上建立內容。
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

本節說明如何使用Adobe Experience Manager(AEM)建立和管理頁面，以便您 [建立內容](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md) 在那幾頁。

>[!NOTE]
>
>您的帳戶需要 [適當的訪問權限](/help/sites-administering/security.md) 和 [權限](/help/sites-administering/security.md#permissions) 在頁面上執行動作，例如建立、複製、移動、編輯、刪除。
>
>如果您遇到任何問題，建議您與系統管理員聯繫。

## 組織您的網站 {#organizing-your-website}

身為作者，您需要在AEM中組織網站。 這包括建立和命名您的內容頁面，以便：

* 您可輕鬆在製作環境中找到它們
* 您網站的訪客可輕鬆在發佈環境中瀏覽

您也可以使用 [資料夾](#creating-a-new-folder) 協助組織內容。

網站的結構可視為 *樹結構* 可保留您的內容頁面。 這些內容頁面的名稱會用來形成URL，而標題會在檢視頁面內容時顯示。

以下顯示Geometrixx網站的擷取；例如， `Triangle` 頁面存取：

* 製作環境

   `http://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

* 發佈環境

   `http://localhost:4503/content/geometrixx/en/products/triangle.html`

   視您執行個體的設定而定，請使用 `/content` 在發佈環境中可能是選用項目。

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

此結構可從網站主控台檢視，您可使用 [瀏覽樹結構](/help/sites-classic-ui-authoring/author-env-basic-handling.md#main-pars-text-15).

![chlimage_1-151](assets/chlimage_1-151.png)

### 頁面命名慣例 {#page-naming-conventions}

建立新頁面時，有兩個索引鍵欄位：

* **[標題](#title)**:

   * 這會在主控台中向使用者顯示，並在編輯時顯示在頁面內容頂端。
   * 此欄位為必填.

* **[名稱](#name)**:

   * 這用於生成URI。
   * 此欄位的用戶輸入為可選。 如果未指定，則從標題派生名稱。

建立新頁面時，AEM將 [根據慣例驗證頁面名稱](/help/sites-developing/naming-conventions.md) 由AEM和JCR強加。

實作和允許的字元清單會因UI而稍有不同（觸控式UI的範圍較廣），但允許的最小值為：

* &#39;a&#39;到&#39;z&#39;
* &#39;A&#39;到&#39;Z&#39;
* &#39;0&#39;到&#39;9&#39;
* _（下划線）
* `-` （連字型大小/減號）

如果您想要確定是否接受/使用這些字元，請只使用這些字元(如果您需要所有允許字元的完整詳細資訊，請參閱 [命名慣例](/help/sites-developing/naming-conventions.md))。

#### 標題 {#title}

如果您在建立新頁面時只提供頁面 **Title** ,AEM會從此字串衍生頁面 **Name**[ ，並根據AEM和JCR所強加的慣例來驗證名稱。](/help/sites-developing/naming-conventions.md)在兩個UI中a **標題** 將接受包含無效字元的欄位，但派生的名稱將替換無效字元。 例如：

| 標題 | 衍生名稱 |
|---|---|
| 捨恩 | schoen.html |
| SC%&amp;&amp;ast;ç+ | sc---c-.html |

#### 名稱 {#name}

如果您提供頁面 **名稱** 建立新頁面時，AEM將 [根據慣例驗證名稱](/help/sites-developing/naming-conventions.md) 由AEM和JCR強加。

在傳統UI中，您 **不能輸入無效字元** 在 **名稱** 欄位。

>[!NOTE]
>在觸控式UI中，您 **無法提交無效字元** 在 **名稱** 欄位。 當AEM偵測到無效字元時，欄位會反白顯示，並顯示說明訊息，指出需要移除/取代的字元。

>[!NOTE]
>
>除非是語言根，否則應避免使用ISO-639-1所定義的雙字母代碼。
>
>請參閱 [準備翻譯內容](/help/sites-administering/tc-prep.md) 以取得更多資訊。

### 範例 {#templates}

在AEM中，範本會指定專用的頁面類型。 模板將用作建立任何新頁面的基礎。

範本定義頁面結構；包括縮圖影像和其他屬性。 例如，您可能有不同的產品頁面、網站地圖和聯絡資訊範本。 模板由 [元件](#components).

AEM隨附數個現成可用的範本。 提供的範本取決於個別網站，而需要提供的資訊（建立新頁面時）取決於使用的UI。 關鍵欄位為：

* **標題**
產生的網頁上顯示的標題。

* **名稱**
為頁面命名時使用。

* **範本**
可在生成新頁面時使用的模板清單。

### 元件 {#components}

元件是AEM提供的元素，可讓您新增特定類型的內容。 AEM隨附一系列現成可用的元件，提供全面功能；包括：

* 文字
* 影像
* Slideshow
* 影片
* 更多

建立並開啟頁面後，您可以 [使用元件新增內容](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#insertinganewparagraph)，可從 [sidekick](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick).

## 管理頁面 {#managing-pages}

### 建立新頁面 {#creating-a-new-page}

除非您事先已為您建立所有頁面，否則您必須先建立頁面，才能開始建立內容：

1. 從 **網站** 控制台，選擇要建立新頁面的級別。

   在以下範例中，您要在層級下建立頁面 **產品**  — 顯示在左窗格中；右窗格顯示下層已存在的頁面 **產品**.

   ![screen_shot_2012-02-15at114413am](assets/screen_shot_2012-02-15at114413am.png)

1. 在 **新……** 功能表（按一下旁邊的箭頭） **新……**)，選取 **新頁面……**. 此 **建立頁面** 窗口。

   按一下 **新……** 它本身也是通往 **新頁面……** 選項。

1. 此 **建立頁面** 對話框允許您：

   * 提供 **標題**;這會顯示給使用者。
   * 提供 **名稱**;這用於生成URI。 若未指定，則會從標題衍生名稱。

      * 如果您提供頁面 **名稱** 建立新頁面時，AEM將 [根據慣例驗證名稱](/help/sites-developing/naming-conventions.md) 被AEM和JCR所取代。
      * 在傳統UI中，您 **不能輸入無效字元** 在 **名稱** 欄位。
   * 按一下您要用來建立新頁面的範本。

      範本是新頁面的基礎；例如，決定內容頁面的基本配置。
   >[!NOTE]
   >
   >請參閱 [頁面命名慣例](#page-naming-conventions).

   建立新頁面所需的最低資訊為 **標題** 和所需的範本。

   ![screen_shot_2012-02-15at114845am](assets/screen_shot_2012-02-15at114845am.png)

   >[!NOTE]
   >
   >如果要在URL中使用Unicode字元，請設定別名( `sling:alias`)屬性([頁面屬性](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md))。

1. 按一下 **建立** 來建立頁面。 您返回 **網站** 可在其中看到新頁面項目的主控台。

   主控台會提供頁面的相關資訊（例如上次編輯頁面的時間，以及依誰），並視需要更新。

   >[!NOTE]
   >
   >您也可以在編輯現有頁面時建立頁面。 使用**建立子頁** **頁面** 標籤，將直接在編輯的頁面下建立新頁面。

### 開啟頁面進行編輯 {#opening-a-page-for-editing}

您可以開啟要 [編輯](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#editing-a-component-content-and-properties) 方法之一：

* 從 **網站** 主控台，您可以 **按兩下** 要開啟以進行編輯的頁面項目。

* 從 **網站** 主控台，您可以 **按一下右鍵** （內容功能表），然後選取 **開啟** 的上界。

* 開啟頁面後，您可以按一下超連結來導覽至網站內的其他頁面（以編輯它們）。

### 複製和貼上頁面 {#copying-and-pasting-a-page}

複製時，您可以複製下列任一項：

* 單頁
* 頁面與所有子頁面

1. 從 **網站** 控制台，選擇要複製的頁面。

   >[!NOTE]
   >
   >此階段無論您要複製單一頁面或基礎子頁面，都無關緊要。

1. 按一下 **複製**.

1. 導覽至新位置，然後按一下：

   * **貼上**  — 將頁面與所有子頁面一起貼上
   * **Shift +貼上**  — 僅貼上選定頁面

   頁面會貼到新位置。

   >[!NOTE]
   >
   >如果現有頁面已有相同名稱，頁面名稱可能會自動調整。

   >[!NOTE]
   >
   >您也可以使用 **複製頁面** 從 **頁面** sidekick的標籤。 這會開啟一個對話方塊，您可在其中指定目的地等。

### 移動或重新命名頁面 {#moving-or-renaming-page}

>[!NOTE]
>
>重新命名頁面也受 [頁面命名慣例](#page-naming-conventions) 指定新頁面名稱時。

移動或更名頁面的過程相同。 使用相同的動作，您可以：

* 將頁面移至新位置
* 重新命名相同位置的頁面
* 將頁面移至新位置並同時重新命名

AEM可讓您更新重新命名或移動之頁面的內部連結。 您可以逐頁完成這項作業，以提供完全的彈性。

移動或更名頁面：

1. 觸發移動的方法有多種：

   * 從 **網站** 主控台，按一下以選取頁面，然後選取 **移動……**
   * 從 **網站** 主控台，您也可以選取頁面項目，然後 **按一下右鍵** 選取 **移動……**
   * 編輯頁面時，您可以選取 **移動頁面** 從 **頁面** sidekick的標籤。

1. 此 **移動** 窗口開啟；您可以在此處指定新位置、頁面的新名稱，或兩者皆指定。

   ![screen_shot_2012-02-15at121336pm](assets/screen_shot_2012-02-15at121336pm.png)

   該頁面還列出參考所移動頁面的任何頁面。 視參考頁面的狀態而定，您可以調整頁面上的這些連結及/或重新發佈頁面。

1. 視情況填入下列欄位：

   * **目的地**

      使用Sitemap（可透過下拉式選取器取得）來選取應將頁面移至的位置。

      如果您只更名頁面，請忽略此欄位。

   * **移動**

      指定要移動的頁面 — 這通常會根據您啟動移動動作的方式和位置填入。

   * **重新命名為**

      預設會顯示目前的頁面標籤。 視需要指定新的頁面標籤。

   * **調整**

      更新所列指向已移動頁面的頁面上的連結：例如，如果頁面A有連結至頁面B,AEM會調整頁面A中的連結，以防您移動頁面B。

      可針對每個個別參考頁面選取/取消選取此選項。

   * **重新發佈**

      重新發佈參考頁面；同樣地，您也可以為每個個別頁面選取此選項。
   >[!NOTE]
   >
   >如果頁面已啟用，移動頁面會自動停用它。 依預設，移動完成時會重新啟動它，但您可以取消勾選 **重新發佈** 欄位中 **移動** 窗口。

1. 按一下 **移動**. 需要確認。 按一下 **確定** 確認。

   >[!NOTE]
   >
   >不會更新頁面標題。

### 刪除頁面 {#deleting-a-page}

1. 您可以從各種位置刪除頁面：

   * 在 **網站** 主控台，按一下以選取頁面，然後按一下滑鼠右鍵並選取 **刪除** 從產生的功能表。
   * 在 **網站** 主控台，按一下以選取頁面，然後選取 **刪除** 的上界。
   * 在sidekick內使用 **頁面** 索引標籤 **刪除頁面**  — 這會刪除目前開啟的頁面。

1. 選取刪除頁面後，您必須確認請求，因為動作無法還原。

   >[!NOTE]
   >
   >刪除後，如果頁面已發佈，您可以還原最新（或特定）版本，但如果進行進一步修改，則此版本可能與上一個版本的內容不完全相同。 請參閱 [如何還原頁面](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoringpages) 以取得詳細資訊。

>[!NOTE]
>
>如果頁面已啟用，則會在刪除前自動停用。

### 鎖定頁面 {#locking-a-page}

您可以 [鎖定/解除鎖定頁面](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#locking-a-page) 或編輯個別頁面時傳送。 關於頁面是否已鎖定的資訊也會顯示在兩個位置中。

### 建立新資料夾 {#creating-a-new-folder}

>[!NOTE]
>
>資料夾也受 [頁面命名慣例](#page-naming-conventions) 指定新資料夾名稱時。

1. 開啟 **網站** 控制台並導覽至所需位置。
1. 在 **新……** 功能表（按一下旁邊的箭頭） **新……**)，選取 **新資料夾……**.
1. 此 **建立資料夾** 對話框將開啟。 您可以在此輸入 **名稱** 和 **標題**:

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. 選擇 **建立** 來建立資料夾。
